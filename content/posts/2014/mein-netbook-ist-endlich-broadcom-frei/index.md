---
title: Mein Netbook ist endlich broadcom-frei
date: 2014-07-18T15:25:00+0100
categories:
 - Linux
 - OSBN
tags:
- Notebook
- Broadcom
- X130e
slug: mein-netbook-ist-endlich-broadcom-frei
---
Ich nenne ein X130e von Lenovo mein Eigen. An sich ein wirklich gutes Gerät in dieser Klasse. Allerdings ist als Wlan-Karte ein Exemplar von Broadcom verbaut. Letztes Jahr hatte ich damit schon mal üble [Probleme](/warum-man-immer-erst-die-sufu-nutzen-sollte/). Seit einiger Zeit fällt die Datenrate bei jedem größeren Datenverkehr bis auf knappe 100 K/s. Normalerweise würde man an dieser Stelle einfach eine andere Karte einbauen. Vorzugsweise von Intel. Dank der Whitelist im Bios des Geräts kann es sich allerdings an die Backe schmieren. Selbst mit einem modifizierten Bios bin ich hier nicht weitergekommen.

Vor ein paar Tagen hatte ich jetzt endgültig die Schnauze voll und ich habe mir einen WLAN-USB-Stick gekauft. Da ich mich derzeit oft auf Raspberry-Pi-Seiten herumtreibe ist mir der Stick EW-781Un (Version 1.0A) von Edimax bereits das eine oder andere mal aufgefallen. Hierbei handelt es sich um einen Nano-USB-Stick und stört somit am Netbook nicht wirklich. Er bietet zudem eine maximale Rate von 150 Mbps und kommt mit WPA2 zurecht. Nachdem ich die WLAN-Karte von Broadcom deaktiviert hatte, lief der Stick auf "out of the box" unter Arch Linux. Lediglich die Interface-Bezeichnung im Profil von netctl musste ich noch anpassen. Größere Dateitransfere laufen damit endlich so wie sie sollen. Nämlich schnell und stabil.

Was bleibt mir also abschließend zu sagen? Wer einen WLAN-USB-Stick für Linux sucht, ist mit diesem Teil gut beraten. Positiv hervorheben möchte ich auch, dass auf der Verpackung neben Windows auch Mac und Linux als unterstütztes Betriebssystem genannt wird. Was den Preis betrifft, ist man mit ungefähr 7 Euro dabei.
