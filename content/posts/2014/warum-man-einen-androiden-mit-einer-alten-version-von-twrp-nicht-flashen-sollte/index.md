---
title: Warum man einen Androiden mit einer alten Version von TWRP nicht flashen sollte
date: 2014-05-12T08:53:00+0100
categories:
- OSBN
- Allgemein
tags:
- Layer 8
- TWRP
- Veraltet
- Omni ROM
slug: warum-man-einen-androiden-mit-einer-alten-version-von-twrp-nicht-flashen-sollte
---
<p>Gestern war mal wieder Bastelzeit. Und Layer-8-Zeit. Ich wollte schon vor längerem einmal das [Omni-Rom](http://omnirom.org "Omni-ROM") auf meinem Mobiltelefon installieren. Gestern habe ich mir mal die Zeit genommen, zumal sonst keiner daheim war und endlich mal Ruhe geherrscht hat.

Also schnell mal Windows gebootet, [MyPhoneExplorer](http://www.fjsoft.at/de "MyPhoneExplorer") gestartet (warum gibt es eigentlich kein vergleichbares Programm das direkt unter Linux läuft? Naja egal.) und Kontakte, SMS usw. gesichert. Sowie noch so gut.. Was brauche ich jetzt? Das Omni-Rom... Gut also selbiges in der aktuellen Version heruntergeladen und die MD5-Summe verglichen. Passt. Nun noch die aktuelle Google-Apps besorgen und beides auf das Mobiltelefon kopieren. Dabei habe ich gemerkt, dass noch einige ROM von Paranoid Android auf dem Hande liegen. Weg damit. Ready to roll? Jep! Also Mobiltelefon neu gebootet und [TWRP](http://teamw.in "TWRP") gestartet. Wie ging das jetzt noch gleich. Ach ja... Cache und Davlik Cache plätten. Gesagt getan. Und nun das neue ROM installieren. Genau an der Stelle hätte mir jemand auf die Finger klopfen sollen. War nur leider keiner da. Das Flashen ging mit einem netten Failure nach hinten los. Nach ein paar Sekunden nervösem googlen hatte ich den Grund gefunden. Meine Version von TWRP ist zu alt. Verdammte Axt! Was nun? Datensicherung vorhanden? Check. Datensicherung auf dem Mobiltelefon vorhanden? Natürlich nicht. Da sich das Mobiltelefon nicht mehr unter Windows oder Linux mounten lässt, habe ich jetzt wohl ein kleines Problem.

Kurz davor, mir schon mal ein neues Mobiltelefon zu bestellen, habe ich über Google das Tool adb.exe gefunden. Damit lässt sich wohl jede Menge Blödsinn anstellen. Unter anderem soll man damit wohl auch flashen können, wenn man, so wie ich, Mist gebaut hat. Da ja nicht wirklich mehr schief gehen kann, habe ich mir dann gleich mal [Android SDK](http://developer.android.com/sdk/index.html?hl=sk "Android SDK") installiert. ADB ist ein Bestandteil davon. Als nächstes habe ich mein Telefon in den Recovery-Modus gebootet, ADB Sideload gestartet und versucht mittels adb.exe ein aktuelles Image von TWRP hochzuladen. Hat auch geklappt. Als ich über die Installationsfunktion installieren wollte, wurde die Datei aber nicht gefunden. Nur Zip-Dateien. Also gut, dann packen wir das Image in eine ZIP-Datei und laden Sie noch einmal hoch. Mit dem Ergebnis, dass die Datei angeblich nicht geöffnet werden kann. Unter Windows klappt es aber problemlos. Hmm... Google schlägt mir als weitere Lösung fastboot.exe (ebenfalls Bestandteil des SDK) vor. Da selbiges auch auf der Seite von Omni-Rom empfohlen wird, kann es Versuch ja nicht schaden. Also starten wir das Telefon mal in den Fastboot-Modus und geben in die Konsole unter Windows mal "fastboot flash recovery twrp.img" ein und drücken beherzt auf Return. So wie es aussieht tut sich etwas, und es wird erfolgreich abgeschlossen.

Nach einem Neustart begrüßt mich TWRP in der aktuellen Version. Sollte ich mal wieder mehr Glück als Verstand haben? Ein erneuter Versuch Omni-Rom zu installieren wird erfolgreich abgeschlossen. Eindeutig mehr Glück als Verstand.

Lange Rede, kurzer Sinn... Für den Notfall sollte man immer ein funktionsfähiges Backup auf dem Telefon haben, nicht nur auf dem Rechner. Und RTFM schadet auch nicht. Hätte ich letzteres gemacht, wäre mir das mit der alten Version von TWRP schon vorher aufgefallen.