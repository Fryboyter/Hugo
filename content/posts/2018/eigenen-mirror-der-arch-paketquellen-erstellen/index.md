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

Als Webserver nehme ich [Caddy](/caddy-webserver/) mit folgender Konfigurationsdatei.

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
# Copyright (C) 2007 Woody Gilk &lt;woody@archlinux.org&gt;
# Modifications by Dale Blount &lt;dale@archlinux.org&gt;
# and Roman Kyrylych &lt;roman@archlinux.org&gt;
# Comments translated to German by Dirk Sohler &lt;dirk@0x7be.de&gt;
# Licensed under the GNU GPL (version 2)

# Speicherorte f&uuml;r den Synchronisationsvorgang
SYNC_HOME=&quot;/home/pi&quot;
SYNC_LOGS=&quot;$SYNC_HOME/archpakete/logs/&quot;
SYNC_FILES=&quot;$SYNC_HOME/archpakete&quot;
SYNC_LOCK=&quot;$SYNC_HOME/archpakete/mirrorsync.lck&quot;

# Auswahl der zu synchronisierenden Repositorys
# G&uuml;ltige Optionen sind: core, extra, testing, community, iso
# Leer lassen, um den gesammten Mirror zu synchronisieren
# SYNC_REPO=(core extra testing community iso)
SYNC_REPO=(core extra community)

# Server, von dem synchronisiert werden soll
# Nur offizielle, &ouml;ffentliche Mirrors d&uuml;rfen rsync.archlinux.org verwenden
# SYNC_SERVER=rsync.archlinux.org::ftp
SYNC_SERVER=rsync.selfnet.de::archlinux
# An dieser Stelle weicht die Lokalisierte Version des Scripts von der
# Originalversion ab, da der Mirror in der Originalversion seit einigen
# Tagen nicht mehr synchronisiert wurde, und daher nur alte Pakete
# bereit stellte. Selfnet hat eine Quota von 50 GB fullspeed am Tag, und
# wird danach auf 16 KByte/s runtergestuft.

# Format des Logfile-Namens
# Das beispiel gibt etwas wie &bdquo;sync_20091019-3.log&ldquo; aus
LOG_FILE=&quot;pkgsync_$(date +%Y%m%d-%H).log&quot;

# Logfile anlegen und Timestamp einf&uuml;gen
touch &quot;$SYNC_LOGS/$LOG_FILE&quot;
echo &quot;=============================================&quot; &gt;&gt; &quot;$SYNC_LOGS/$LOG_FILE&quot;
echo &quot;&gt;&gt; Starting sync on $(date --rfc-3339=seconds)&quot; &gt;&gt; &quot;$SYNC_LOGS/$LOG_FILE&quot;
echo &quot;&gt;&gt; ---&quot; &gt;&gt; &quot;$SYNC_LOGS/$LOG_FILE&quot;

if [ -z $SYNC_REPO ]; then
  # Sync a complete mirror
  rsync -rptlv \
        --delete-after \
        --safe-links \
        --max-delete=1000 \
        --copy-links \
        --progress \
        --delay-updates $SYNC_SERVER &quot;$SYNC_FILES&quot; \
        | tee &quot;$SYNC_LOGS/$LOG_FILE&quot;
else
  # Alle Repositorys synchronisieren, die in $SYNC_REPO angegeben wurden
  for repo in ${SYNC_REPO[@]}; do
    repo=$(echo $repo | tr [:upper:] [:lower:])
    echo &quot;&gt;&gt; Syncing $repo to $SYNC_FILES/$repo&quot; &gt;&gt; &quot;$SYNC_LOGS/$LOG_FILE&quot;

    # Wenn man nur i686-Pakete synchronisieren will, kann man in dem
    # rsync-Aufruf dies nach &bdquo;--delete-after&ldquo; inzuf&uuml;gen:
    # &bdquo; --exclude=os/x86_64&ldquo;
    # 
    # Will man stattdessen nur die x86_64-Pakete synchronisieren, verwendet
    # man stattdessen &bdquo;--exclude=os/i686&ldquo;
    #
    # Will man beide Architekturen auf dem eigenen Mirror anbieten, l&auml;sst
    # den rsync-Aufruf einfach, wie er ist
    #
    rsync -rptlv \
          --delete-after \
          --safe-links \
          --max-delete=1000 \
          --copy-links \
          --progress \
          --delay-updates $SYNC_SERVER/$repo &quot;$SYNC_FILES&quot; \
          | tee &quot;$SYNC_LOGS/$LOG_FILE&quot;

    # Erstellt eine Datei &bdquo;$repo.lastsync&ldquo;, die den Timestamp der synchronisation
    # beinhaltet (z. B. &bdquo;2009-10-19 03:14:28+02:00&ldquo;). Dies kann n&uuml;tzlich sein,
    # um einen Hinweis darauf zu haben, wann der eigene Mirror zuletzt mit
    # dem angegebenen Mirror abgeglichen wurde. Zum Verwenden einkommentieren.
    # date --rfc-3339=seconds &gt; &quot;$SYNC_FILES/$repo.lastsync&quot;

    # Nach jedem Repository f&uuml;nf Sekunden warten, um zu viele gleichzeitige 
    # Verbindungen zum rsync-Server zu verhindern, fall die Verbindung nach
    # dem synchronisieren des vorherigen Repositorys vom Server nicht
    # zeitig geschlossen wurde
    sleep 5 
  done
fi

# Weiteren Timestamp ins Logfile schreiben, und es schlie&szlig;en
echo &quot;&gt;&gt; ---&quot; &gt;&gt; &quot;$SYNC_LOGS/$LOG_FILE&quot;
echo &quot;&gt;&gt; Finished sync on $(date --rfc-3339=seconds)&quot; &gt;&gt; &quot;$SYNC_LOGS/$LOG_FILE&quot;
echo &quot;=============================================&quot; &gt;&gt; &quot;$SYNC_LOGS/$LOG_FILE&quot;
echo &quot;&quot; &gt;&gt; &quot;$SYNC_LOGS/$LOG_FILE&quot;

# Die lock-Datei zum Sperren des Script-Durchlaufs l&ouml;schen und das
# Script beenden
rm -f &quot;$SYNC_LOCK&quot;
exit 0</code></pre>

Nun habe ich unter "archpakete" noch schnell ein Verzeichnis "logs" erstellt und obiges Script ausgeführt.

Sobald das Script seine Arbeit getan hat, kann man nun auf seinem Ansible-Test-System in /etc/pacman.d/mirrorlist folgenden Eintrag am Anfang der Datei eintragen.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code>Server = http://$IP_DES_RASPBERRY:$PORT_VON_CADDY/$repo/os/$arch</code>
</pre>

Nun laufen alle Downloads der Pakete über den lokalen Mirror und nicht mehr über die offiziellen Spiegelserver.
