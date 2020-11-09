---
title: Pi-Hole mit Unbound verheiraten
date: 2018-07-03T20:57:00+0100
categories:
- Linux
- OSBN
tags:
- Pi-Hole
- Unbound
slug: pi-hole-mit-unbound-verheiraten
---
[Pi-Hole](https://pi-hole.net) ist ein sogenanntes "DNS-Sinkhole" für das eigene Netzwerk mit dem man unerwünschte Werbung von Webseiten herausfiltern kann. Gestern habe ich mir das ganze auf einem freigewordenen Raspberry Pi installiert.

Da Pi-Hole Arch Linux offiziell nicht unterstützt und es wohl ab und zu zu Problemen kommt, habe ich mir kurzerhand Raspbian installiert. Lustigerweise gibt es für Arch im AUR ein Paket für Pi-Hole während man hingegen bei Rasppian das ganze über "curl -sSL https://install.pi-hole.net | bash" installieren muss. Das ist übrigens der offizielle Weg, auch wenn normalerweise vor solchen Anleitungen gewarnt wird. Der ganze Vorgang ist unterm Strich recht unspektakulär und funktioniert unterm Strich einfach.

Während der Installation ist mir die Idee gekommen, ob man nicht Pi-Hole mit [Unbound](https://www.unbound.net) kombinieren kann. Unbound lief bei mir bisher als caching DNS Resolver, so dass ich nicht auf DNS wie 8.8.8.8 (Google) angewiesen bin.

Also erst einmal Unbound mittels "sudo apt install unbound" installieren.

Mit dem Befehl "sudo wget -O /var/lib/unbound/root.hints https://www.internic.net/domain/named.root" laden wir uns nun die Liste der DNS-Root-Server herunter.

Jetzt geht es an das Konfigurieren von Unbound. Hierfür legen wir die Datei /etc/unbound/unbound.conf.d/pi-hole.conf an und füllen sie folgendem Inhalt.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">server:
    verbosity: 1
    port: 12345
    do-ip4: yes
    do-udp: yes
    do-tcp: yes

    # Wenn IPv6 genutzt wird auf yes ändern
    do-ip6: no

    # Liste der Root-Server
    root-hints: "/var/lib/unbound/root.hints"

    # Vertraut glue nur wenn innerhalb von servers authority
    harden-glue: yes

    # Um DNSSEC zu deaktivieren auf no setzen
    harden-dnssec-stripped: yes

    # Großbuchstaben um Spoof zu erschweren
    use-caps-for-id: yes
    
    # EDNS Buffergroeße
    edns-buffer-size: 1472

    # TTL für Cache
    cache-min-ttl: 3600
    cache-max-ttl: 86400

    # Oft genutzte Einträge bleiben im Cache
    prefetch: yes

    # Anzahl der Threads (1 reicht fuer kleines LAN)
    num-threads: 1
    
    # Cache-Speicher. rrset sollte doppelt so groß wie msg sein
    msg-cache-size: 50m
    rrset-cache-size: 100m
    
    # UDP schneller mit Multithreading (Tux only).
    so-reuseport: yes
    
    # Stellt sicher, dass Kernel-Buffer groß genug ist wenn Traffic stark ansteigt 
    so-rcvbuf: 1m

    # IP werden nicht aufgelöst
    private-address: 192.168.1.1/16
    </code></pre>

Wer mit meinen Kommentaren nichts anfangen kann, kann unter [https://www.unbound.net/documentation/unbound.conf.html](https://www.unbound.net/documentation/unbound.conf.html) eine genauere Beschreibung nachlesen. Im Moment ist nur die dritte und die letzte Zeile wichtig. In der dritten wird der Port angegeben auf den Unbound lauschen soll. Und in der letzten trägt man seinen Adressbereich für das eigene LAN ein.

Mittels "systemctl start unbound.service" testet man nun, ob Unbound ohne Probleme startet. Mit "systemctl enable unbound.service" wird Unbound automatisch gestartet

Jetzt noch Unbound bei Pi-Hole als DNS eintragen. Hierfür einfach $PI-IP/admin im Browser eingeben (anstelle von $IP-IP nimmt man die IP unter der der Raspberry im LAN erreichbar ist). Nun sollte das Dashboard von Pi-Hole angezeigt werden. Dort klicken wir dann links auf Login und melden uns an. Nun wählen wir links Settings -&gt; DNS aus. Hier habe ich festgestellt, dass man in der stabilen Version von Pi-Hole zwar die IP eines eigenen DNS eintragen kann, aber keinen Port. Nach etwas Google-Fu habe ich herausgefunden, dass die erst mit der aktuellen Beta-Version funktioniert. Da ich nichts zu verlieren habe, bin ich mit folgenden Befehlen auf die aktuelle Beta-Version gewechselt.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">echo "FTLDNS" | sudo tee /etc/pihole/ftlbranch
pihole checkout core FTLDNS 
pihole checkout web FTLDNS</code>
</pre>

Nun lässt sich unter Settings -&gt; DNS 127.0.0.1#12345 eintragen (anstelle von 12345 nimmt man den in der Konfigurationsdatei angegebenen Port (# ist hier Absicht und muss angegeben werden).

Nun müssen wir nun noch den Geräten im Netzwerk beibringen, das Pi-Hole als DNS zu nutzen. Hierzu hinterlegen wir die IP des Raspberry Pi entweder im Router oder passen die DNS-Einstellungen auf den jeweiligen Geräten an (/etc/resolv.conf, netctl Profile usw.).

Als Fazit nach ca. 24 Stunden mit der Kombination aus Pi-Hole und Unbound kann ich bisher folgende Aussagen treffen:

- Apt ist verglichen mit pacman verflucht langsam
- Ich werde mich nie mit einer Distribution anfreunden die für jeden Mist sudo nutzt, so dass ich vermutlich das Root-Konto aktivieren oder doch wieder Arch installieren werde.
- Wenn Unbound die IP einer Internetseite noch nicht kennt, gibt es eine knappe Gedenksekunde bis die Seite angezeigt wird. Danach geht alles sehr schnell.
- Wenn man sich die Statistik von Pi-Hole so ansieht, merkt man erst wie viel Mist gefiltert wird. Bei mir sind es aktuell 30,4 Prozent aller Anfragen die im Loch verschwinden.

Was die Statistik betrifft, habe ich gemerkt, dass diese jede Minute aktualisiert wird. Da ich keine aktuellen Statistiken benötige und um daher unnötige Schreibvorgänge auf der Speicherkarte zu vermeiden habe ich die Datei /etc/pihole/pihole-FTL.conf angelegt und dort DBINTERVAL=60.0 eingetragen. Somit erfolgt der Schreibvorgang nun noch alle 60 Minuten. Für mich absolut ausreichend, da zwischenzeitlich der Filtervorgang ganz normal weiterläuft.

Einen Nachteil hat diese Lösung für mich aber. Für diverse Sachen wie Geo-Blocking nutze ich einen VPN-Anbieter. Beim derzeitigen Anbieter (was vermutlich auch auf die meisten anderen Anbieter zutreffen wird) lässt sich leider kein eigener DNS eintragen um sogenannte DNS Leaks zu verhindern. Somit werde ich auch weiterhin im Browser zusätzlich uBlock Origin nutzen. Zumal Pi-Hole manche Sachen wie diese nervigen Cookie-Hinweise nicht filtern kann.
