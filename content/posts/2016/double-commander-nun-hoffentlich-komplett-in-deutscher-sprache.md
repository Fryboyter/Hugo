---
title: Double Commander nun hoffentlich komplett in deutscher Sprache
date: 2016-01-08T17:53:00+0100
categories:
- Linux
- OSBN
tags:
- Double Commander
- Übersetzung
slug: double-commander-nun-hoffentlich-komplett-in-deutscher-sprache
---
Obwohl ich mit meinem derzeitigen Setup zufrieden bin, werfe ich ab und zu mal einen Blick auf alternative Programme. Wenn es um einen Dateimanager geht, setze ich seit Jahren schon auf [Krusader](http://www.krusader.org "Krusader"). Gestern habe ich mir aber einmal den [Double Commander](http://doublecmd.sourceforge.net "Double Commander") genauer angesehen. Für **meinen** Geschmack ist das derzeit die beste Alternativ zu Krusader.

Nur eine Kleinigkeit hat mich sehr gestört. Der Commander ist so eingestellt, dass er das Programm in deutscher Sprache anzeigen soll. An einigen Stellen hat es geklappt, andere wurden in englischer Sprache angezeigt. So einen Mischmasch kann ich gar nicht haben. Entweder oder. Nicht mal so mal so.

Ich habe mir dann mal unter /usr/lib/doublecmd/language/ die Sprachdatei angesehen, welche für die deutsche Sprache zuständig ist. Jede Stelle die im Programm nicht in Deutsch angezeigt wurde, war in der Sprachdatei als "Fuzzy" gekennzeichnet. Das passiert zum Beispiel dann, wenn das Programm an sich geändert wird und somit die jeweilige Übersetzung eventuell nicht mehr passt. Somit kann der Übersetzer, der die PO-Datei erstellt hat sich die betreffenden Stellen ansehen und ggf. anpassen. Da ich keine Lust habe, so lange zu warten habe ich mich mal selbst ans Werk gemacht. Nach einigem Hin und Her habe ich mich für das Programm [Lokalize](https://userbase.kde.org/Lokalize "Lokalize") entschieden. Da ich KDE 5 (ja es gibt kein KDE 5) benutze war es eh schon installiert. Mit diesem Tool habe ich einfach mal die betreffenden Fuzzy-Lines angesehen und geprüft. Viele habe ich einfach bestätigt, viele habe ich aber auch geändert. Die eine oder andere Übersetzung die eigentlich gar nicht betroffen war, habe ich ebenfalls angepasst, da mir die vorhandene nicht wirklich gefallen hat.

Circa 5 Stunden später (den Aufwand habe ich ernsthaft unterschätzt) "erstrahlt" der Double Commander nun komplett in deutscher Sprache. Außer ich habe etwas übersehen. Mit der einen oder anderen Übersetzung (sowohl von mir als auch vom ursprünglichen Übersetzer) bin ich allerdings immer noch nicht zufrieden. Zum einen ist mir teilweise nichts besseres eingefallen, zum anderen war der vorhandene Platz in der grafischen Oberfläche einfach zu klein.

Abschließend bleibt aber noch ein Problem. Naja eigentlich zwei. Um die Übersetzung in die Entwicklung einfließen zu lassen, müsste ich die Datei mit einem Subersion-Zugang hochladen. Von Subversion habe ich allerdings keinen blassen Schimmer. Und was noch viel schlimmer ist, das Projekt wird bei Sourceforge gehostet. Nach deren [Aktion](https://mail.gnome.org/archives/gimp-developer-list/2015-May/msg00144.html) vor ein paar Monaten will ich mit dem Verein eigentlich gar nichts zu tun haben. Mal schauen wie ich das ganze löse. Bis mir etwas, für mich, sinnvolles eingefallen ist, kann man die Datei auch [hier](https://copy.com/ZccL3w4LcjiAQQDt) herunterladen.
