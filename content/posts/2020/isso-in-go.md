---
title: Isso in Go
date: 2020-05-10T13:36:13+0200
categories:
- OSBN
- General
tags:
- Isso  
- Go
- Kommentare
slug: isso-in-go
---
Isso ist aktuell mein bevorzugtes Kommentarsystem für Internetseiten, da man hierfür nur eine SQLite-Datenbank benötigt. Leider war die Installation in der Vergangenheit oft etwas problematisch. Aktuell ist wohl eine Installation über PyPI gar nicht bzw. nur über Umwege möglich ([https://github.com/posativ/isso/issues/617](https://github.com/posativ/isso/issues/617)).

Durch Zufall bin ich heute bei Github auf [go-isso](https://github.com/budui/go-isso) gestoßen. Der Entwickler möchte eine API kompatible Alternative zu Isso anbieten für die er die Programmiersprache Go nutzt. Somit braucht man im besten Fall nach Veröffentlichung einer neuen Version nur eine einzelne Datei herunterladen und ausführen. Bei [Hugo](https://gohugo.io/) klappt das zumindest sehr gut.

Der Entwickler weist aber aktuell darauf hin, das go-isso noch mit Vorsicht zu genießen ist, da es sich um sein erstes Projekt mit Go handelt, so dass der Code vermutlich qualitative Verbesserungen vertragen kann. Bugs sind ebenfalls nicht ausgeschlossen. Kurz gesagt, Benutzung auf eigene Gefahr.

Vielleicht hat ja der eine oder andere Leser dieses Artikels Lust und Zeit, sich an go-isso zu beteiligen. Gesucht werden auch Leute die sich mit Javascript auskennen. Da ich weder das eine noch das andere beherrsche, werde ich wohl selbst nur testen und ggf. Bugs melden.