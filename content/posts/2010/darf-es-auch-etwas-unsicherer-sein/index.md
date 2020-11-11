---
title: Darf es auch etwas unsicherer sein?
date: 2010-07-20T07:05:00+0100
categories:
- Linux
- OSBN
tags:
- Unsicher
- Damn Vulnerable Linux
- Thorsten Schneider
- Universität Bielefeld
slug: darf-es-auch-etwas-unsicherer-sein
---
Eigentlich versuchen die Distributoren, dass ihre Distributionen zum Zeitpunkt der Veröffentlichung so sicher wie möglich sind. Eigentlich... Bei der Distribution DVL ist genau das Gegenteil der Fall. Es wurde soviel falsch konfigurierte, defekte, veraltete und angreifbare Software wie möglich eingebaut. Die Idee für solch eine Distribution stammt von Herrn Dr. Thorsten Schneider, welcher an der Universität Bielefeld Kurse wie "Ethical Hacking - Binary Auditing &amp; RCE" hält.

Was soll das jetzt? Mit DVL soll es primär IT-Studenten als Trainingssystem dienen und ihnen ermöglichen sich in Themen wie Reverse Code Engineering, Buffer Overflows, Shellcode Entwicklung, Web Exploitation und SQL injection einzuarbeiten. Aber auch ganz normale Menschen können sich diese "Spielwiese" herunterladen und damit lernen. Solch ein Wissen kann ja auch dazu dienen z. B. Schwachstellen verwendeter Software zu erkennen und zu beheben bzw. den Entwicklern zu melden. Oder die Software zu wechseln.

Zu finden ist DVL unter [http://www.damnvulnerablelinux.org](http://www.damnvulnerablelinux.org "Damn Vulnerable Linux"). Dort findet man neben diverser Informationen auch die Downloadmöglichkeit.

DVL sollte **nicht** als Produktivsystem verwendet werden. Am besten installiert man es unter einer virtuellen Umgebung wie [VirtualBox](http://www.virtualbox.org "VirtualBox") oder als Live-DVD. Eine direkte Verbindung ins Internet würde ich ebenfalls nicht empfehlen. Warum, sollte eigentlich klar sein.

Dass man mit dem damit erworbenem Wissen keinen Mist anstellt, sollte klar sein. Und ja, das meine ich ernst.
