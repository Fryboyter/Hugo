---
title: Mausgesten der Marke Eigenbau
date: 2013-06-07T12:13:00+0100
categories:
- Linux
- OSBN
tags:
- Mausgesten
- Easystroke
slug: mausgesten-der-marke-eigenbau
---
Auf meinem Netbook nutze ich derzeit Chromium, da mein Lieblingsbrowser Opera zu zäh läuft und Midori leider regelmäßig abstürzt. Unter Opera nutze ich schon seit Jahren die Mausgesten. Chromium unterstützt von Haus aus keine und die Erweiterungen die ich auf die schnelle gefunden habe, gefallen mir alle nicht so richtig. In den Weiten des Internets bin ich dann auf [Easystroke](http://sourceforge.net/apps/trac/easystroke "easystroke") gestoßen.

Der Vorteil an Easystroke ist, dass man damit eigentlich jedes Programm mit Mausgesten ausrüsten kann. Der Nachteil, es ist eben kein Plugin, sondern ein extra Programm das gestartet werden muss. Naja auf eines mehr oder weniger kommt es bei halbwegs aktuellen Rechnern auch nicht an.

Nachdem man das Tool installiert und gestartet hat, wird einem erst einmal eine mehr oder weniger leere grafische Oberfläche angezeigt. Als erstes klicken auf den Reiter "Preferences" und wählen unter "Behavior" die Schaltfläche "Gesture Button" aus. Im nun erscheinenden Fenster wählen wir recht unten anstelle des voreingestellten Button 2 (Mausrad) Button 3 aus (rechte Maustaste) und bestätigen mit "OK". Natürlich kann man hier verwenden was man will. Wer das Mausrad nutzen will kann auch Button 2 lassen usw.

Nun wechseln wir wieder auf den Reiter "Actions" und klicken auf den kleinen Pfeil neben Applications und öffnen somit das Untermenü.

{{< image src="easystroke_2.png" alt="easystroke_2" >}}

Als nächstes starten wir das gewünschte Programm, dass wir mit Mausgesten ausstatten wollen. Danach klicken wir unter easystroke auf die Schaltfläche "Add Application". Nun sollte sich der Mauszeiger in ein Fadenkreuz verwandelt haben, mit welchem wir das gewünschte Fenster klicken. In diesem Fall Chromium. Nun sollte in Easystroke neben dem bereits vorhandenen Eintrag "default" auch Chromium gelistet sein.

Diesen Eintrag wählen wir nun mit einem Mausklick aus. Wenn der Eintrag markiert ist, klicken wir in easystroke auf die Schaltfläche "Add Action", welche man am unteren Rand findet. Nun erscheint bereit die erste Aktion, welche den voreingestellten Namen "chromium Gesture 1" trägt. Diesen Namen ändern wir als erstes. Zum Beispiel in "Zurück", da wir als erstes die Mausgeste anlegen wollen, die die vorherige Internetseite aufruft. Nun wechseln wir mit TAB in die Spalte "Type" Nun erhalten wir eine Auswahlliste mit diversen Einträgen. Hier kann man sich je nach Anwendung, die mit Mausgesten ausgestattet werden soll, austoben. Bei diesem Beispiel ist "Key" das was wir brauchen. Nachdem wir das ausgewählt den Cursortasten ausgewählt haben (alternativ mit der Maus), erscheint in der Spalte Details der Eintrag "Key combination...". An dieser Stelle drücken wir nun die gewünschte Tastenkombination. In diesem Fall wäre dies die Taste ALT und die Cursortaste nach Links. Die genauen Shortcuts für Chrome/Chromium kann man sich [hier](https://support.google.com/chrome/answer/171571?hl=de&amp;ref_topic=25799 "Chrome Shortcuts") ansehen. Das Ganze müsste nun wie folgt aussehen.

{{< image src="easystroke_3.png" alt="easystroke_3" >}}

Nun müssen wir nur noch die Mausgeste bestimmen, mit der dieser Eintrag ausgeführt wird. Da ich, wie schon angemerkt, ein Fan von Opera bin, kopiere ich einfach mal die Mausgesten dieses Browsers. Diese findet man [hier](http://help.opera.com/Linux/12.10/de/gestures.html "Opera Mausgesten"). Für unser Beispiel müssten wir also die rechte Maustaste drücken, gedrückt halten und mit der Maus eine Bewegung nach Links ausführen. Also gut. Damit auch easystroke das kapiert klicken wir nun auf "Record Stroke". Hier erhalten wir den Hinweis, dass nun alles aufgezeichnet wird, was wir nun mit der Maus anstellen. Also klicken wir auf die rechte Maustaste, halten diese und ziehen die Maus ein Stück nach links und lassen die rechte Maustaste wieder los. Nun sollte der von uns erstelle Eintrag für "Zurück" wie folgt aussehen.

{{< image src="easystroke_4.png" alt="easystroke_4" >}}

Das wiederholen wir nun für alle gewünschten Mausgesten. Mehr gibt es eigentlich nicht zu tun. Easystroke zeigt in den mit Mausgesten ausgestatteten Anwendungen beim Ausführen der Gesten diese auch grafisch an. Dies kann man im Reiter "Preferences" unter "Apperence" ändern bzw. abstellen. Hier gibt es auch eine Möglichkeit anzugeben, dass easystroke automatisch gestartet werden soll. Denn läuft easystroke nicht, funktionieren die Mausgesten auch nicht.
