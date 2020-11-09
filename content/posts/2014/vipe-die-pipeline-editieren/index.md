---
title: Vipe - Die Pipeline editieren
date: 2014-10-19T10:53:00+0100
categories:
- Linux
- OSBN
tags:
- Vipe
- Pipeline
- Editieren
slug: vipe-die-pipeline-editieren
---
Ab und an kann es vorkommen, dass man die Daten, die man per Pipe an einen anderen Befehl weiterleitet vorher noch editieren möchte. Hierfür kann man beispielsweise vipe nutzen.

Nehmen wir mal folgendes, billiges Beispiel. In einem Verzeichnis befinden sich diverse Bilddateien.

{{< image src="vipe1.png" alt="vipe1.png" >}}

Diese Dateien wollen wir nun mittels ls | xargs echo ausgeben lassen (sagte ich bereits, dass das Beispiel billig ist? :D). Dabei kommt dann folgendes heraus.

{{< image src="vipe2.png" alt="vipe2.png" >}}

Bei den Dateinamen fällt nun auf, dass eine der Dateien (bild_3.jpg) vom Dateinamen anders aufgebaut ist als die anderen Dateien. An der Stelle kommt nun vipe ins Spiel. Ändert man den Befehl nun in ls | vipe | xargs echo ab, kann man die Informationen, die man durch ls erhält erst noch mit einem Editor verändern bevor sie an xargs übergeben werden.

{{< image src="vipe3.png" alt="vipe3.png" >}}

Bei diesem Beispiel habe ich nun den Unterstrich entfernt um die Ausgabe zu vereinheitlichen.

{{< image src="vipe4.png" alt="vipe4.png" >}}

Zu finden ist vipe, zumindest unter Arch Linux, im Paket moreutils. In diesem Paket sind auch noch einige andere, interessante Befehle zu finden. Ansehen lohnt sich also meiner Meinung nach.
