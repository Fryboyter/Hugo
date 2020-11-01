---
title: Bitbucket verabschiedet sich von Mercurial
date: 2019-08-21T19:37:59+0200
categories:
- OSBN
- Allgemein
tags:
- Bitbucket
- Mercurial
slug: bitbucket-verabschiedet-sich-von-mercurial
---
Wer als Versionsverwaltung [Mercurial](https://www.mercurial-scm.org/) verwendet und diese nicht selbst hosten will nutzt vermutlich meist das Angebot von [Bitbucket](https://bitbucket.org/product/).

Auf dem offiziellen [Blog](https://bitbucket.org/blog/sunsetting-mercurial-support-in-bitbucket) wurde nun bekannt gegeben, dass in einigen Monaten die Unterstützung für Mercurial eingestellt wird. Bitbucket setzt dann wie andere Anbieter (z. B. Github oder Gitlab) nur noch auf Git.

Ab dem 01. Februar 2020 kann man bei Bitbucket keine Mercurial-Repositories anlegen. Ab dem 01. Juni 2020 ist dann endgültig Schluss und die vorhandenen Repositories werden gelöscht.

Wer also Projekte bei Bitbucket hostet, sollte bis spätestens 31. Mai seine Daten sichern und sich nach einer Alternative umsehen.

Ich vermute die Entscheidung von Bitbucket wird dazu führen, dass einige Projekte nun zu Git wechseln.

Wer weiterhin Mercurial nutzen will, kann sich [https://www.mercurial-scm.org/wiki/MercurialHosting](https://www.mercurial-scm.org/wiki/MercurialHosting) ansehen. Dort werden einige alternative Anbieter (die mich auf den ersten Blick alle nicht beigeistern) aufgeführt.

Ebenfalls werden dort Möglichkeiten zu selber hosten genannt. Hier finde ich vor allem [Heptapod](https://heptapod.net/) interessant. Hierbei handelt es sich um einen Fork von Gitlab der Mercurial unterstützt. Zudem sind die Entwickler von Gitlab dem Fork postiv gesinnt und unterstützen die Entwicklung. Laut den Entwicklern ist Heptapod allerdings noch in einem frühen Entwicklungsphase. Wer also Mercurial für wichtige Projekte nutzt, sollte daher noch abwarten.