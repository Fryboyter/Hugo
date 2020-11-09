---
title: Warum ich mich mit aktuellen Browsern nicht anfreunden kann
date: 2014-12-05T16:48:00+0100
categories:
- OSBN
- Allgemein
tags:
- Browser
- Mist
slug: warum-ich-mich-mit-aktuellen-browsern-nicht-anfreunden-kann
---
Da mir aktuell das Youtube-Problem unter QupZilla zu sehr auf den Zeiger geht (sobald man an eine noch nicht geladene Stelle springt, stürzt der Browser ab. Problem ist hier die aktuelle stabile Version von qt-webkit), habe ich mal anhand von Seamonkey getestet, was ich alles machen muss, bis mir der Browser halbwegs zusagt.

**Folgendes ist hochgradig subjektiv! Und ziemlich wahrscheinlich hätte ich einige Sachen besser lösen können.**

Ich brauche Mausgesten. Das ist für mich wichtiger als zum Beispiel ein Werbefilter. Seamonkey bietet das leider von Haus aus nicht an. Also habe ich mich nach der Installation des Browsers erst einmal auf die Suche nach einem entsprechenden Plugin gemacht (ich mag keine Plugins...). Von einem Bekannten der leidenschaftlicher Firefox-Nutzer ist, wurde mir FireGestures empfohlen. Leider hat der Entwickler das Plugin nur für den Firefox aber nicht für Seamonkey ausgelegt, so dass eine einfache Installation nicht möglich war. Nach einigem Suchen bin ich dann bei [Mouse Gestures Suite](https://addons.mozilla.org/en-US/seamonkey/addon/mouse-gestures-suite "Mouse Gestures Suite") gelandet. Der Entwickler hält sein Plugin kompatibel zu Seamonkey und Firefox. Das Thema wäre also schon mal erledigt. Aber das nächste Problem lies nicht lange auf sich warten...

Auch wenn ich nun ein Plugin für Mausgesten gefunden habe, habe ich mir dennoch ein paar andere Alternativen angesehen. Auf eine wurde mittels eines Textlinks verwiesen. Anklicken war also nicht möglich. Na kein Problem. Link markiert, rechte Maustaste und dann im Kontextmenü "Gehe zur Web-Adresse" (oder wie sich der Punkt bei Seamonkey auch immer nennt) aufrufen. Tja solch einen Punkt gibt es nicht. Also nächstes Plugin. Die Wahl fiel auf [Selection Links](https://addons.mozilla.org/en-US/firefox/addon/selection-links "Selection Links") auch wenn das Plugin schon ziemlich lange nicht mehr aktualisiert wurde. Leider ist auch dieses Plugin nicht für Seamonkey ausgelegt. Von Dexter, einem Boardie vom [ngb.to](http://ngb.to "ngb.to") habe ich hier allerdings eine [Lösung](http://addonconverter.fotokraina.com) erhalten. Auf dieser Seite kann man Plugins so abändern lassen, dass Sie in der Regel auch mit Semonkey funktionieren. Was in dem Fall auch der Fall war.

Was brauche ich jetzt noch an zusätzlichen Funktionen, die mir der Browser nicht bietet? Adblock und der Element Hiding Helper wären nicht schlecht. Überraschung! Auch hier gibt es die Plugins nur für Firefox. Also wieder bereits genannte Seite aufgemacht und die Plugins für den Seamonkey lauffähig gemacht.

Als nächstes ist die grafische Oberfläche des Browsers an der Reihe. Hier passen mir so einige Dinge auch nicht. Von Haus aus sieht Seamonkey wie auf folgendem Bild aus.

{{< image src="SeaMonkey.png" alt="SeaMonkey.png" >}}

Was mich hier stört sind links oben diese schraffierten Bereiche am Anfang der Menü- URL- und Lesezeichenzeile. Mit diesen kann man die jeweilige Zeile minimieren. Ich möchte so etwas entweder komplett anzeigen lassen oder eben komplett ausblenden. Manche Elemente in den Leisten lassen sich per wie zum Beispiel bei Opera per Drag and Drop entfernen. Diese nicht. Hätte mich auch gewundert... Also tricksen wir mal etwas mit CSS. Also habe ich mal eben im Profilverzeichnis von Seamonkey das Verzeichnis chrome erstellt und in diesem die Datei userChrome.css. Um die schraffierten Flächen auszublenden sind hier folgende Einträge nötig.

.toolbar-grippy { display: none !important; }
.toolbar-primary-grippy { display: none !important; }

Ok, was kommt als nächstes? Dass die Tabbar ganz am Ende angebracht ist, gefällt mir kein Stück. Ich bin es einfach zu sehr gewohnt, dass die Tabs über der Adresszeile angezeigt werden. Alle Lösungen die ich hierzu im Internet gefunden habe, bezogen sich auf ältere Versionen und funktionieren mit der aktuellen scheinbar nicht mehr. Überraschung! Ich habe daher als Kompromiss die Leiste mit den Lesezeichen über die Adresszeile verlegt, so dass die Tab-Zeile sowie Adresszeile zumindest nahe beieinander sind.

In der Zeile für die Tabs gibt es schon das nächste "Problem". Ganz links gibt es eine Schaltfläche mit der man einen neuen Tab öffnen kann. Man muss also nach ganz links, klickt und bekommt dann am rechten Ende der Zeile einen Tab erstellt. Warum zur Hölle wird diese Schaltfläche nicht einfach nach dem letzten offenen Tab angezeigt? Trägt man ".tabs-stack vbox hbox stack { -moz-box-ordinal-group:10!important; }" in die userChrome.css ein, bekommt man die Schaltfläche zwar nach rechts, aber eben ganz nach rechts neben dem Pfeil und dem X. Gleicher Blödsinn nur auf der anderen Seite. Nach langem Suchen bin ich dann auf das Plugin seatabxplus gestoßen. Mit diesem wird zum einen bei jedem Tag die Schaltfläche zum Schließen des Tabs angezeigt (warum es die nicht von Haus aus gibt, will ich lieber gar nicht wissen) und zum anderen wird im jeweils aktiven Tab ein Schaltfläche erzeugt, mit der man einen neuen Tab aufrufen kann. Immer noch nicht ideal aber besser als nichts. Nun habe ich allerdings ein paar Schaltflächen zuviel. Zum einen die für den neuen Tab ganz links und die für das Schließen ganz rechts. Da ich den Pfeil mit dem man sich die Liste der offenen Tabs anzeigen kann, auch nicht brauche, habe ich folgendes in die userChrome.css eingetragen.

.tabs-stack vbox hbox stack { display: none; !important; }

Und weg sind alle drei überflüssige Schaltflächen.

Da ich nur die Browser-Komponente von Seamonkey nutzen möchte, benötige ich die Schaltflächen ganz links unten ebenfalls nicht, mit denen man z. B. den Composer oder das E-Mail-Programm aufrufen kann. Hier wurde ich überrascht. Auch diese lassen sich nicht mal eben per Drag and Drop entfernen. Also habe ich die userChrome.css um folgende Einträge erweitert und die Schaltflächen auszublenden.

#mini-nav {display:none;}
#mini-comp {display:none;}
#mini-mail {display:none;}
#mini-addr {display:none;}
#mini-irc {display:none;}

So langsam wird es doch... Nur wie stelle ich geschlossene Tabs her? Und damit meine ich jetzt nicht alle einer Session auf einen Schlag sondern je nach Bedarf. Hier gibt es im Menü "Gehe" einen entsprechenden Punkt. Aber scheinbar auch nur dort. Wieso nicht auch als Schaltfläche z. B. neben der Adresszeile? Jedes mal über das Menü zu gehen ist doch nervig. Da ich schon länger kein Plugin installiert habe, ist es wohl mal wieder soweit... Die Wahl fiel auf [Undo Closed Tabs Button](https://addons.mozilla.org/de/firefox/addon/undo-closed-tabs-button "Undo Closed Tabs Button"). Auch das ist offiziell nur für den Firefox. Also übergebe ich es weiter oben genannter Seite und lasse es kompatibel machen. Das ist scheinbar so einfach, dass es die Plugin-Entwickler doch eigentlich auch gleich machen könnten. Wegen mir dann auch ohne Garantie bezüglich Seamonkey.

Abschließend habe ich noch ein paar Elemente der grafischen Oberfläche per Drag and Drop verschoben (Vor, Zurück, Neu und Halt nach rechts usw.), was ich in dem Fall auch machen durfte.

Davon abgesehen, dass die Zeile für die Tabs nicht über der Adresszeile ist und die Schaltfläche für einen neuen Tab noch immer nicht rechts neben dem letzten Tab, ist Seamonkey für mich jetzt nutzbar und sieht nun bei mir so aus (als Theme habe das bereits im Lieferumfang enthaltene \"modern\" gewählt). Das verpixelte ist die Leiste mit den Lesezeichen.

{{< image src="Seamonkey3.png" alt="Seamonkey3.png" >}}

Der durchschnittliche Nutzer dürfte, vor allem bei den Änderungen in der userChrome.css, aber wohl scheitern. Vor allem bei .toolbar-grippy und .toolbar-primary-grippy. Die Bezeichnungen habe ich nämlich mit nur dem DOM und dem Element Inspector (letzten musste ich ebenfalls noch als Plugin installieren) herausgefunden.

Aber dafür kann ich jetzt in einem Youtube-Video an eine noch nicht geladene Stelle springen. Da hat sich er ganze Aufwand doch schon fast gelohnt. :D
