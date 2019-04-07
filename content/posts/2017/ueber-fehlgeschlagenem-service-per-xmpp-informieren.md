---
title: Über fehlgeschlagenen Service per XMPP informieren
date: 2017-09-11T17:36:00+0100
categories:
- Linux
- OSBN
tags:
- XMPP
- Sendxmpp
- Systemd
slug: ueber-fehlgeschlagenem-service-per-xmpp-informieren
---
Auf meinen Raspberry Pi's laufen einige Dienste wie ein Q3A-Server. Diese zum Beispiel mit Zabbix zu überwachen ist mir dann doch etwas übertrieben, da diese Dienste entweder rein privat genutzt werden oder ich einfach keine Uptime garantiere.

Trotzdem wäre es dann doch interessant wenn ich darüber informiert werde wenn zum Beispiel ein Dienst nicht gestartet werden konnte. Vor allem wenn man nicht daheim ist. Da ich auf meinem Smartphone auch einen XMPP-Client installiert habe, würde sich eine Lösungen mittels XMPP und systemd anbieten.

Um die Nachrichten zu versenden habe ich mir sendxmpp installiert. Unter Arch findet man das Paket im AUR. Um zu testen ob das Versenden überhaupt funktioniert, habe ich es gleich einmal ausprobiert.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">echo 'Hallo Welt' | sendxmpp -t  -u fryboyter -j jabjab.de -p 'strenggeheim' empfänger@deshalbfrei.org</code>
</pre>

Und schon knallt es und ich bekomme die Fehlermeldung "Invalid or unreadable path specified for ssl_ca_path. at /usr/share/perl5/vendor_perl/XML/Stream.pm line 641" vor den Latz geknallt. Dann schauen wir uns die Datei doch mal an. Zeile 641 verrät mir allerdings recht wenig. Allerdings gibt es in besagter Datei die Zeile $self-&gt;{SIDS}-&gt;{default}-&gt;{ssl_ca_path} = '';. An deren Ende habe ich zwischen die beiden '' einfach mal&nbsp;/etc/ssl/certs eingetragen.

Nächster Versuch, nächste Fehlermeldung.&nbsp;Error 'AuthSend': error: bad-protocol[?]. Na das ist ja mal sehr aussagekräftig. Nach etwas Google-Fu konnte ich das Problem in der Datei&nbsp;/usr/share/perl5/vendor_perl/Net/XMPP/Protocol.pm ausfindig machen. In Zeile 2104 steht&nbsp;return $ self-&gt; AuthSASL (% args);. Diese Zeile kommentieren wir einfach mal mit einem # am Anfang aus. Ich bin mir allerdings nicht sicher, ob das nicht irgendwelche Nebenwirkungen hat.

Und wieder ein neuer Anlauf. Und plötzlich informiert mich mein XMPP-Client dass ich für empfänger@deshalbfrei.org eine Nachricht erhalten habe. Yeehaa!

Da nun die Benachrichtungen per XMPP funktionieren, erstellen wir unter /usr/bin ein Shellscript (nennen wir es mal xmpp.sh) mit folgendem Inhalt.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">#!/bin/bash

UNIT=$1

UNITSTATUS=$(systemctl status $UNIT)
ALERT=$(echo -e "\u26A0")

echo "$ALERT Unit failed $UNIT $ALERT Status: $UNITSTATUS" | /usr/bin/site_perl/sendxmpp -t  -u fryboyter -j jabjab.de -p 'strenggeheim' empfänger@deshalbfrei.org</code>
</pre>

Nun erstellen wir unter /etc/systemd/system die Servicedatei xmpp@.service mit folgendem Inhalt.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">[Unit]
Description=Benachrichtigung mittels XMPP
After=network.target

[Service]
Type=simple
ExecStart=/usr/bin/xmpp.sh %I</code>
</pre>

Zum Schluss editieren wir noch die Service-Dateien der Dienste die wir überwachen wollen und packen unter dem Bereich [Unit] die Zeile&nbsp;OnFailure=xmpp@%n.service.

Startet nun ein Service nicht erhält man automatisch eine Nachricht per XMPP die beispielsweise so aussieht.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">⚠ Unit failed monitorhell.service ⚠ Status: ● monitorhell.service - Tastaturbeleuchtung automatisch aktivieren
   Loaded: loaded (/etc/systemd/system/monitorhell.service; enabled; vendor preset: disabled)
   Active: failed (Result: exit-code) since Mon 2017-09-11 16:36:13 CEST; 1min 18s ago
  Process: 510 ExecStart=/bin/bashx -c echo 2219 &gt; /sys/class/backlight/intel_backlight/brightness (code=exited, status=203/EXEC)
 Main PID: 510 (code=exited, status=203/EXEC)

Warning: Journal has been rotated since unit was started. Log output is incomplete or unavailable.</code>
</pre>
