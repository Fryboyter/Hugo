---
title: Eigenen Mirror der Arch-Paketquellen erstellen
date: 2018-12-30T12:46:00+0100
categories:
- Linux
- OSBN
tags:
- Mirror
- Paketquelle
- Arch
slug: eigenen-mirror-der-arch-paketquellen-erstellen
---
Wie bereits angekündigt, will ich mittels Ansible die Installation und Konfiguration von Arch automatisieren. Um unabhängig von den offiziellen Mirrors zu sein, habe ich mir daher einfach einen eigenen erstellt. Somit kann ich so lange herumspielen wie ich will.

Da das ganze nur intern für Tests gedacht ist, habe ich es relativ einfach gehalten.

Als erstes habe ich mir auf einem Raspberry ein Verzeichnis erstellt in dem die ganzen Pakete landen sollen. Nennen wir es "archpakete".

Als Webserver nehme ich [Caddy](https://fryboyter.de/caddy-webserver) mit folgender Konfigurationsdatei.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">$IP_DES_RASPBERRY:$PORT_VON_CADDY
root /pfad/zum/Mirrorverzeichnis
gzip
browse</code>
</pre>

Gzip, also die komprimierte Datenübertragung und browse (das anzeigen von Verzeichnisinhalten) kann man sich im Grunde auch sparen. Es schadet allerdings auch nicht.

Startet man nun Caddy sollte man nicht viel sehen, da das Verzeichnis "archpakete" noch leer ist. Zeit es zu befüllen. Hierfür habe ich mal wieder im Wiki von Arch gestöbert und folgendes Script gefunden, was ich allerdings etwas angepasst habe (Anzeige des Fortschritts (--progress und | tee) hinzugefügt und den Download auf die Paketquellen "core" "extra" "community" beschränkt.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">#!/bin/bash
#
# The script to sync a local mirror of the Arch Linux repositories and ISOs
#
# Copyright (C) 2007 Woody Gilk <woody@archlinux.org>
# Modifications by Dale Blount <dale@archlinux.org>
# and Roman Kyrylych <roman@archlinux.org>
# Comments translated to German by Dirk Sohler <dirk@0x7be.de>
# Licensed under the GNU GPL (version 2)

# Speicherorte für den Synchronisationsvorgang
SYNC_HOME="/home/pi"
SYNC_LOGS="$SYNC_HOME/archpakete/logs/"
SYNC_FILES="$SYNC_HOME/archpakete"
SYNC_LOCK="$SYNC_HOME/archpakete/mirrorsync.lck"

# Auswahl der zu synchronisierenden Repositorys
# Gültige Optionen sind: core, extra, testing, community, iso
# Leer lassen, um den gesammten Mirror zu synchronisieren
# SYNC_REPO=(core extra testing community iso)
SYNC_REPO=(core extra community)

# Server, von dem synchronisiert werden soll
# Nur offizielle, öffentliche Mirrors dürfen rsync.archlinux.org verwenden
# SYNC_SERVER=rsync.archlinux.org::ftp
SYNC_SERVER=rsync.selfnet.de::archlinux
# An dieser Stelle weicht die Lokalisierte Version des Scripts von der
# Originalversion ab, da der Mirror in der Originalversion seit einigen
# Tagen nicht mehr synchronisiert wurde, und daher nur alte Pakete
# bereit stellte. Selfnet hat eine Quota von 50 GB fullspeed am Tag, und
# wird danach auf 16 KByte/s runtergestuft.

# Format des Logfile-Namens
# Das beispiel gibt etwas wie „sync_20091019-3.log“ aus
LOG_FILE="pkgsync_$(date +%Y%m%d-%H).log"

# Logfile anlegen und Timestamp einfügen
touch "$SYNC_LOGS/$LOG_FILE"
echo "=============================================" >> "$SYNC_LOGS/$LOG_FILE"
echo ">> Starting sync on $(date --rfc-3339=seconds)" >> "$SYNC_LOGS/$LOG_FILE"
echo ">> ---" >> "$SYNC_LOGS/$LOG_FILE"

if [ -z $SYNC_REPO ]; then
  # Sync a complete mirror
  rsync -rptlv \
        --delete-after \
        --safe-links \
        --max-delete=1000 \
        --copy-links \
        --progress \
        --delay-updates $SYNC_SERVER "$SYNC_FILES" \
        | tee "$SYNC_LOGS/$LOG_FILE"
else
  # Alle Repositorys synchronisieren, die in $SYNC_REPO angegeben wurden
  for repo in ${SYNC_REPO[@]}; do
    repo=$(echo $repo | tr [:upper:] [:lower:])
    echo ">> Syncing $repo to $SYNC_FILES/$repo" >> "$SYNC_LOGS/$LOG_FILE"

    # Wenn man nur i686-Pakete synchronisieren will, kann man in dem
    # rsync-Aufruf dies nach „--delete-after“ inzufügen:
    # „ --exclude=os/x86_64“
    # 
    # Will man stattdessen nur die x86_64-Pakete synchronisieren, verwendet
    # man stattdessen „--exclude=os/i686“
    #
    # Will man beide Architekturen auf dem eigenen Mirror anbieten, lässt
    # den rsync-Aufruf einfach, wie er ist
    #
    rsync -rptlv \
          --delete-after \
          --safe-links \
          --max-delete=1000 \
          --copy-links \
          --progress \
          --delay-updates $SYNC_SERVER/$repo "$SYNC_FILES" \
          | tee "$SYNC_LOGS/$LOG_FILE"

    # Erstellt eine Datei „$repo.lastsync“, die den Timestamp der synchronisation
    # beinhaltet (z. B. „2009-10-19 03:14:28+02:00“). Dies kann nützlich sein,
    # um einen Hinweis darauf zu haben, wann der eigene Mirror zuletzt mit
    # dem angegebenen Mirror abgeglichen wurde. Zum Verwenden einkommentieren.
    # date --rfc-3339=seconds > "$SYNC_FILES/$repo.lastsync"

    # Nach jedem Repository fünf Sekunden warten, um zu viele gleichzeitige 
    # Verbindungen zum rsync-Server zu verhindern, fall die Verbindung nach
    # dem synchronisieren des vorherigen Repositorys vom Server nicht
    # zeitig geschlossen wurde
    sleep 5 
  done
fi

# Weiteren Timestamp ins Logfile schreiben, und es schließen
echo ">> ---" >> "$SYNC_LOGS/$LOG_FILE"
echo ">> Finished sync on $(date --rfc-3339=seconds)" >> "$SYNC_LOGS/$LOG_FILE"
echo "=============================================" >> "$SYNC_LOGS/$LOG_FILE"
echo "" >> "$SYNC_LOGS/$LOG_FILE"

# Die lock-Datei zum Sperren des Script-Durchlaufs löschen und das
# Script beenden
rm -f "$SYNC_LOCK"
exit 0</code></pre>

Nun habe ich unter "archpakete" noch schnell ein Verzeichnis "logs" erstellt und obiges Script ausgeführt.

Sobald das Script seine Arbeit getan hat, kann man nun auf seinem Ansible-Test-System in /etc/pacman.d/mirrorlist folgenden Eintrag am Anfang der Datei eintragen.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code>Server = http://$IP_DES_RASPBERRY:$PORT_VON_CADDY/$repo/os/$arch</code>
</pre>

Nun laufen alle Downloads der Pakete über den lokalen Mirror und nicht mehr über die offiziellen Spiegelserver.
