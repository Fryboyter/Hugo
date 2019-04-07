---
title: Runwhen - Eine Alternative zu cron
date: 2013-06-04T14:37:00+0100
categories:
- Linux
- OSBN
tags:
- Runwhen
- Ersatz
- Cron
slug: runwhen-eine-alternative-zu-cron
---
Ich merke mir irgendwie schlecht, wie die richtige Reihenfolge für die Einträge in die [Crontab](http://de.wikipedia.org/wiki/Cron\ "Cron") ist. Ist die erste Stelle nun für die Minuten zuständig? Oder waren es die Stunden? Jedes mal das selbe Drama. Lars von Suckup.de hat deswegen heute einen [Tipp](http://suckup.de/linux/crontab-tipp "Crontab Tipp") in seinem Blog veröffentlicht, mit dem man diese Unsicherheit aus dem Weg räumen kann.

An dieser Stelle möchte ich nicht noch einen Tipp für cron veröffentlichen, sondern eine Alternative vorstellen. [Runwehn](http://code.dogmap.org/runwhen "runwhen"). Hiermit finde ich es wesentlich angenehmer einen Cronjob zu erstellen.

Nehmen wir mal an, man möchte etwas täglich um 5.30 Uhr am Morgen ausführen. Hier wäre der Eintrag **RUNWHEN=",H=5,M=30"** nötig. Oder es soll nur etwas am fünften Tag vor Monatsende ausgeführt werden? Dann wäre **RUNWHEN=",d-5"** das Richtige.

Das Ganze lässt sich beliebig kombinieren. Um zu zeigen, was neben H,M und d noch alles möglich ist, hier mal ein Auszug aus meiner Konfigurationsdatei:

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash"># The constraint string consists of a sequence of unit constraints. Each unit
# constraint consists of a comma, one of the following letters indicating which
# unit is constrained:
#
# * y: year.
# * m: month (in the range 1-12).
# * d: day of the month (in the range 1-28, 1-29, 1-30, or 1-31, as
# appropriate for the month in question).
# * w: day of the week (in the range 0-6, with 0 representing Sunday).
# * H: hour of the day (in the range 0-23).
# * M: minute of the hour (in the range 0-59).
# * S: second of the minute (in the range 0-59).
#
# and finally one of the following:
#
# * =n: matches times when the given unit is exactly n.
# * -n: matches times when the given unit is exactly m, where m+n is one
# more than the largest value of the unit. (For example, n+m=24 for H,
# so ,H-1 is equivalent to ,H=23.
# * /n: matches times when the given unit is divisible by n.</code>
</pre>

Persönlich finde ich das irgendwie angenehmer. Ist aber vermutlich Geschmackssache. Einen etwas ausführlicheren Artikel zu dem Thema Runwhen findet man im [Wiki](http://uberspace.de/dokuwiki/system:runwhen "Uberspace Wiki") von Uberspace.
