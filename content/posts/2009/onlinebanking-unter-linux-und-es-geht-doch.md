---
title: Onlinebanking unter Linux - Und es geht doch
date: 2009-10-25T17:19:00+0100
categories:
- GNU/LINUX
- OSBN
tags:
- Onlinebanking
- Linux
- ReinerSCT
- Moneyplex
- Matrica
slug: onlinebanking-unter-linux-und-es-geht-doch
---
Ich habe es mal wieder gewagt. Den Versuch Onlinebanking nicht mehr unter Windows sondern unter Linux zu tätigen.

Auslöser war im Grunde genommen der Wechsel auf Windows 7. Für meinen bisherigen Kartenleser aus dem Hause Kobil gibt es im Moment leider nur Treiber im Betastadium, mit denen es auf meinem Hauptrechner ziemliche Probleme gab. Vielleicht hatte auch "nur" VR-Networld so seine Probleme mit dem Treiber. Auf jeden Fall hat es nicht wirklich zufriedenstellend funktioniert. Da der vorhandene Kartenleser unter Linux auch nicht gerade bequem zu installieren ist und ich keine Zeit habe auf stabile Treiber zu warten, habe ich mich spontan entschlossen mir das Bundle, bestehend aus Moneyplex 2009 für Linux und den Kartenleser ReinertSCT Cyberjack e-com zu kaufen. Gut das war mit knapp 120 Euro mal wieder nicht gerade billig, aber "Geiz ist geil" sollte man gerade bei solch einem Thema lieber vergessen. Mitten in der Nacht bei matrica bestellt, und bereits am nächsten Tag vor 12 Uhr verschickt. Die haben scheinbar auf meine Bestellung gewartet.

Als dann am nächsten Tag die Bestellung bei mir aufschlug, wollte ich das Ganze gleich Abends installieren. Als mir plötzlich aufgefallen ist, dass ich ja meine Datensicherung von VR-Networld nicht einfach so importieren kann. Klasse... Nach einer Installations- und Updateorgie (hatte nur eine Uraltversion hier herumliegen) auf einem Testsystem mit XP konnte ich endlich die Datensicherung einspielen und als CSV-Dateien exportieren. Tja wieso einfach, wenn es auch kompliziert geht.

So nun aber...

Naja was soll ich sagen. Es gibt bei ReinerSCT zwar fertige Pakete für meine Distribution (Mandriva), aber leider nur für die Version 2007. Aktuell ist 2009.1 und die 2010 steht auch schon fast vor der Tür.  Ok Mandriva ist in Deutschland ja nicht so verbreitet. Dann ist eben mal wieder Marke Eigenbau mit den Sourcen angesagt. Mir schwant schon mal schlimmes... So ähnlich hat es beim Kartenleser von Kobil auch angefangen. Also los. Sourcen heruntergeladen und nach /opt entpackt. Das hat immerhin schon mal geklappt. Dadurch ermutigt schnell eine ./configure ausgeführt. Wusste ich es doch... Es fehlen Pakete. Naja die Ausgabe von ./configure war wenigstens aufschlussreich, so dass ich mit urpm schnell alles nötige nachinstallieren konnte. Keine Minute später also ./configure Teil 2. Geht doch. Als nächstes make. Keine Fehler. Ich bin kurz davor den Champagner zu öffnen. Als nächstes noch ein make install mit Rootrechten ausgeführt. Der Champagnerkorken knallt, trifft aber Gott sei dank niemanden.

Als nächstes also Moneyplex. CD gemountet, Shellskript ausgeführt, der Anleitung gefolgt, fertig. Lässt man mal die Geschichte VR-Networld und der Datensicherung außer acht, hat das ganze keine 10 Minuten gedauert. Geht doch. Gut dann starten wir das Programm einfach mal. Der Kartenleser lässt sich nachdem ich die korrekte CTAPI ausgewählt habe, sofort ansprechen. Die Einrichtung der Bankverbindung und der Konten klappt auch ohne Probleme. Der Datenexport aus VR-Networld wird auch ohne murren geschluckt. Das kann eigentlich nur ein ganz dickes Ende bedeuten (nein ich bin kein Pesimist. Nur Realist mit jahrelanger Erfahrung)... Dann aktualisieren wir mal das Programm und die Konten. Nichts. Rein gar nichts ist schief gegangen. Kurz gesagt, es funktioniert alles. 

Einen Minuspunkt gibt es bei der Geschichte aber dennoch. Die Optik von Moneyplex ist ziemlich gewöhnungsbedürftig. Aber wenigstens funktioniert es. Und ich habe auch schon mit schlimmeren Programmen gearbeitet. Von daher ist im Moment alles im grünen Bereich. 
