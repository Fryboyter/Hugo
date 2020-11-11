---
title: Auf wiedersehen Kmail2
date: 2011-09-06T18:29:00+0100
categories:
 - Linux
 - OSBN
tags:
- Kmail2
- Maildir
- Mbox
slug: auf-wiedersehen-kmail2
---
<p>Eigentlich bin ich ja recht leidensfähig, wenn eine Lösung in Sichtweite ist. Aber in dem Fall habe ich die Nerven einfach nicht. Kmail2 stürzt wegen dieser ver... Konfliktlösung mehrmals täglich bei mir ab (https://bugs.kde.org/show_bug.cgi?id=250797). Jetzt habe ich die Schnauze erst mal voll von dem Programm. Nun darf mich, zumindest vorübergehend, Claws Mail terrorisieren. Das ganze hatte nur einen Haken. Kmail2 verwendet Maildir. Claws Mail unterstützt das nur leider nicht wirklich. Daher musste ich jetzt erst einmal meine ganzen Emails (und das sind nicht wenige) von Maildir in Mbox konvertieren. Für denn Fall, dass sich jemand die Zähne daran ausbeißt, hier nun ein kleines Python-Script, mit dem es bei mir einwandfrei funktioniert hat.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">#!/usr/bin/python 
# -*- coding: utf-8 -*-
 
import mailbox
import sys
import email
 
mdir = mailbox.Maildir(sys.argv [-2], email.message_from_file)
outfile = file(sys.argv[-1], 'w')
 
for mdir_msg in mdir:
    # parse the message:
    msg = email.message_from_string(str(mdir_msg))
    outfile.write(str(msg))
    outfile.write('\n')
 
outfile.close()</code>
</pre>

Das Script, nennen wir es maildir2mbox.py, lässt man dann mit folgendem Befehl auf das jeweilige Maildir-Verzeichnis los: python maildir2mbox.py /pfad/zum/maildir/verzeichnis outbox.mbox So wird für das jeweilige Maildirverzeichnis eine Mbox-Datei erzeugt, welche man problemlos in Claws Mail importieren kann. Unter Arch Linux musste ich allerdings anstelle von phython python2.7 verwenden. Das Script ist übrigens nicht auf meinem Mist gewachsen, sondern stammt von [http://yergler.net/projects/one-off/maildir-to-mbox/](http://yergler.net/projects/one-off/maildir-to-mbox "http://yergler.net/projects/one-off/maildir-to-mbox"). Danke (thank you) Nathan. :)
