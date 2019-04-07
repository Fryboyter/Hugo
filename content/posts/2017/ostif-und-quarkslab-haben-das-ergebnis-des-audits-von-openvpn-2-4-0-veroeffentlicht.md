---
title: OSTIF und Quarkslab haben das Ergebnis des Audits von OpenVPN 2.4.0 veröffentlicht
date: 2017-05-12T11:36:00+0100
categories:
- Linux
- OSBN
tags:
- OpenVPN
- Audit
slug: ostif-und-quarkslab-haben-das-ergebnis-des-audits-von-openvpn-2-4-0-veroeffentlicht
---
OSTIF und Quarkslab habe OpenVPN 2.4.0 einem Audit unterzogen. Die Ergebnisse wurden nun veröffentlicht. Gefunden wurde 1 kritische und 1 mittlere Schwachstelle. Weiterhin gibt es 5 verbesserungswürdige Bereiche.

Die kritische Schwachstelle ist unter [CVE-2017-7478](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2017-7478) und die mittlere unter [CVE-2017-7479](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2017-7479)protokolliert. Über diese Schwachstellen kann ein Angriff mittels DoS durchgeführt werden, der zu einem Ausnahmefehler führt und die Prozessausführung beendet.

OpenVPN bietet für die beiden Lücken bereits aktualisierte Versionen an, welche schon bei der einen oder anderen Distribution verteilt werden. Eine genauere Zusammenfassung sowie den gesamten Audit findet man auf der [Seite von OSTIF](https://ostif.org/the-openvpn-2-4-0-audit-by-ostif-and-quarkslab-results).
