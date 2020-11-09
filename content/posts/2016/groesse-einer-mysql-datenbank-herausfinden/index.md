---
title: Größe einer MySQL-Datenbank herausfinden
date: 2016-01-13T20:29:00+0100
categories:
- Linux
- OSBN
tags:
- MySQL
- Datenbank
- Größe
slug: groesse-einer-mysql-datenbank-herausfinden
---
Heute hat es mich mal interessiert, wie groß die MySQL-Datenbank sind, welche auf meinem Uberspace laufen. Daher habe ich mir mal etwas mit SQL-Abfragen gebaut.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-sql">SELECT sum(round(((data_length + index_length) / 1024 / 1024), 2)) as "Größe in MB" 
FROM information_schema.TABLES 
WHERE table_schema = "Datenbankname"
</code>
</pre>

Hier wird der Wert aus data_length und index_length der Datenbank welche man anstelle von Datenbankname angibt zusammengezählt und das Ergebnis auf zwei Stellen gerundet.

Hat man mehrere Datenbanken kann man deren Größe auch auf einen Schlag anzeigen lassen. Hierzu kann man folgende Abfrage nutzen.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-sql">SELECT table_schema, sum(round(((data_length + index_length ) / 1024 / 1024),2)) "Größe in MB"
FROM information_schema.TABLES
GROUP BY table_schema ;
</code>
</pre>
