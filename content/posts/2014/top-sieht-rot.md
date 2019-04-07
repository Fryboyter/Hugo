---
title: Top sieht rot
date: 2014-11-15T22:46:00+0100
categories:
- Linux
- OSBN
tags:
- Top
- Schrift
- Rot
slug: top-sieht-rot
---
Den Befehl top mit dem man sich die laufenden Prozesse anzeigen lassen kann, kennt vermutlich jeder Linux-Nutzer. Das die Ausgabe von top nun allerdings in rot/orange erfolgt ist neu. Und meiner Meinung nach schlecht zu ertragen. Wie gut, dass ich eigentlich immer nur htop nutze.

![Top1](/files/top1.png)

Um wie gewohnt die alte Ausgabe zu erzeugen muss man wie folgt vorgehen. Als erstes startet man top. Nun drückt folgende Tasten z V 1 y m m t t t W Nun sollte top wieder wie gewohnt aussehen.

![Top2](/files/top2.png)

Bei obiger Tastenkombination wird in ~ die Datei .toprc erzeugt. Sowei ja kein Problem. Ich habe mir die Datei dann allerdings mal in einem Editor angesehen. Und was soll ich sagen? An der Datei ändere ich von Hand bestimmt nichts...

<pre>
<code class="language-bash">top's Config File (Linux processes with windows)
Id:i, Mode_altscr=0, Mode_irixps=1, Delay_time=1.500, Curwin=0
Def     fieldscur=�&K�����@���56�F�')*+,-./0128<>?ABCGHIJLMNOPQRSTUVWXYZ[\]^_`a$
        winflags=192564, sortindx=18, maxtasks=0, graph_cpus=0, graph_mems=0
        summclr=1, msgsclr=1, headclr=3, taskclr=1
Job     fieldscur=�����(��Ļ�@<�Ż)*+,-./012568>?ABCFGHIJKLMNOPQRSTUVWXYZ[\]^_`ab$
        winflags=163124, sortindx=0, maxtasks=0, graph_cpus=2, graph_mems=0
        summclr=6, msgsclr=6, headclr=7, taskclr=6
Mem     fieldscur=���<�����MBN�D34��&'()*+,-./0125689FGHIJKLOPQRSTUVWXYZ[\]^_`a$
        winflags=163124, sortindx=21, maxtasks=0, graph_cpus=2, graph_mems=0
        summclr=5, msgsclr=5, headclr=4, taskclr=5
Usr     fieldscur=�����������)+,-./1234568;<=>?@ABCFGHIJKLMNOPQRSTUVWXYZ[\]^_`a$
        winflags=163124, sortindx=3, maxtasks=0, graph_cpus=2, graph_mems=0
        summclr=3, msgsclr=3, headclr=2, taskclr=3
Fixed_widest=0, Summ_mscale=2, Task_mscale=1, Zero_suppress=0</code>
</pre>
