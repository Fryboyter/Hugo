---
title: Googles FLoC auf fryboyter.de blockiert
date: 2021-04-16T17:02:28+0200
description: Anleitung wie man FloC bei Uberspace.de blockiert
categories:
- Allgemein
tags:
- Google
- FLoC
- Uberspace
slug: googles-floc-auf-fryboyter-de-blockiert
---
Wenn es um das Tracking bei Werbung geht, kommen oft Third-Party-Cookies zum Einsatz. Was viele Nutzer nicht so gut finden. Daher hat sich Google überlegt diese abzuschaffen und hat sich als Alternative [FloC](https://github.com/WICG/floc/blob/main/README.md) (Federated Learning of Cohorts) ausgedacht.

Wie zu erwarten kommt es nicht gut an. Die EFF bezeichnet es als "[schreckliche Idee](https://www.eff.org/deeplinks/2021/03/googles-floc-terrible-idea)". Den Entwicklern des Browsers Vivaldi ist es ein "[FloC off!](https://vivaldi.com/blog/no-google-vivaldi-users-will-not-get-floced/)" wert. Die Betreiber der Suchmaschine DuckDuckGo finden es [auch nicht gut](https://spreadprivacy.com/block-floc-with-duckduckgo/). Genauso wie die Leute die den Browser [Brave](https://brave.com/why-brave-disables-floc/) entwickeln. Und vermutlich halten viele andere FloC für eine scheiß Idee.

Mir geht es genauso, zumal der Mist auch noch [opt-out](https://de.wikipedia.org/wiki/Opt-out_(Permission_Marketing)) ist. Dies gilt auch für Webseitenbetreiber. Damit man nicht mitmacht, kann man den Header seiner Internetseite ändern so das bei jedem HTTP-REPLY <mark>Permissions-Policy „interest-cohort=()“</mark> mitgegeben wird.

Wer seine Seite bei Uberspace.de hostet, hat es einfach. Hierfür genügt einfach sich bei SSH einzuloggen und den Befehl <mark>uberspace web header set / Permissions-Policy "interest-cohort=()"</mark> auszuführen. Nutzer anderer durchschnittlicher Webspaces können vermutlich oft nichts unternehmen bzw. sollten beim jeweiligen Anbieter den Support kontaktieren und hoffen das dieser positiv reagiert. Wer einen eigenen Webserver betreibt, sollte sich schlau machen wie man die Konfiguration seines Webservers entsprechend anpasst.
