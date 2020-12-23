---
title: Btrfs - Eine erste Zwischenbilanz
date: 2013-08-11T11:38:00+0100
categories:
- Linux
- OSBN
tags:
- Btrfs
- Dateisystem
- Zwischenbilanz
slug: btrfs-eine-erste-zwischenbilanz
---
Vor etwas mehr als einen Monat habe ich meine Root-Partition nun auf Btrfs [umgestellt](/btrfs-no-risk-no-fun/). In dieser Zeit hatte ich mehrere größere Updates meiner Distribution eingespielt und auch zwei mal das System zu Absturz gebracht. Einmal durch ein Programm eines Bekannten, dass ich testen sollte und einmal dadurch, dass ich in der Steckdosenleiste leider den falschen Stecker gezogen habe.

Wirklich interessiert hat es aber mein System nicht. Es funktioniert alles wie es soll. Da es auch keine anderen Probleme gibt und ich z. B. die Snapshot-Funktion immer mehr mag, habe ich nun mittels folgender Befehle das Image der ext4-Partition, dass beim Umwandeln auf btrfs automatisch angelegt wurde, nun endgültig entfernt.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">rm /ext2_saved/*
nbtrfs subvolume delete /ext2_saved</code>
</pre>

Derzeit kann ich also das neue Dateisystem, soweit man das nach einem Monat machen kann, nur empfehlen. Zumindest für private Rechner.

Zwischenzeitlich wurde ich auch schon gefragt, ob ich eventuell Benchmarks machen könnte. Ja, ich könnte. Ich werde es allerdings nicht machen. Mir geht es dabei nicht darum, ein noch schnelleres Dateisystem zu verwenden. Mir geht es hauptsächlich um die Funktionen wie Snapshots, Subvolumes oder die Dateisystemprüfung im laufendem Betrieb usw.
