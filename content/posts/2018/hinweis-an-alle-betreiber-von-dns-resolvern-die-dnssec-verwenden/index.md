---
title: Hinweis an alle Betreiber von DNS-Resolvern die DNSSEC verwenden
date: 2018-10-05T15:32:00+0100
categories:
- Linux
- OSBN
tags:
- ICANN
- Hinweis
slug: hinweis-an-alle-betreiber-von-dns-resolvern-die-dnssec-verwenden
---
Der eine oder andere wird sicherlich einen DNS-Resolver im eigenen Netzwerk einsetzen um damit beispielsweise die Anfragen zu beschleunigen oder um die Privatsphäre zu vergrößern. Wer hierbei DNSSEC einsetzt, sollte sich den 11.10.2018 im Kalender anstreichen.

Denn an diesem Tag will ICANN den bisherigen Vertrauensanker (Trust Anchor) gegen einen neuen tauschen. Wer ab dann noch den alten Anker nutzt, wird hinsichtlich DNS ein Problem haben.

Wer zum Beispiel DNSSEC auf seinem Pi Hole nutzt, kann wie folgt nachsehen.

<pre class="line-numbers language-bash">
<code class="language-bash">cat /etc/dnsmasq.d/01-pihole.conf

...

trust-anchor=.,19036,8,2,49AAC11D7B6F6446702E54A1607371607A1A41855200FD2CE1CDDE32F24E8FB5
trust-anchor=.,20326,8,2,E06D44B80B8F1D39A95C0B0D7C65D08458E880409BBC683457104237C7F8EC8D
</code>
</pre>

Die erste Zeile entspricht hier dem bisherigen Anker und die zweite dem neuen Anker. Somit sollten Pi-Hole-Nutzer nichts von der Umstellung bemerken.

Wer Unbound nutzt, kann mittels unbound-anchor -l nachsehen. Bei den von mir getesteten Versionen 1.6.0-3 (Raspbian) sowie 1.8.0-1 (Arch) ist ebenfalls alles im grünen Bereich. Nutzer anderer DNS-Resolver müssen leider selbst schauen wie sie an die nötigen Informationen kommen.

Wer aber seinen DNS-Resolver händisch installiert hat bzw. diesen schon wirklich lange nicht mehr aktualisiert hat, sollte vorsichtshalber einmal nachsehen. ICANN geht selbst davon aus, dass nach der Umstellung nur eine überschaubare Anzahl an Nutzern betroffen sein werden.
