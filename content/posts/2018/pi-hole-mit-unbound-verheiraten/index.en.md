---
title: Combine Pi-Hole with Unbound
date: 2018-07-03T20:57:00+0100
categories:
- Linux
- OSBN
tags:
- Pi-Hole
- Unbound
slug: combine-pi-hole-with-unbound
---
[Pi-Hole](https://pi-hole.net) is a so called "DNS-Sinkhole" for the own network with which you can filter out unwanted advertisements from websites. Yesterday I installed it on a unused Raspberry Pi.

Since Pi-Hole does not officially support Arch Linux and therefore problems may occur, I installed Raspbian without further ado. Funnily enough there is a package for Pi-Hole for Arch in the AUR while you have to install this package for Rasppian via "curl -sSL https://install.pi-hole.net | bash". This is the official way, by the way, even if you normally warn against such instructions. The whole process is quite unspectacular in the end and works simple in the end.

During the installation I had the idea to combine Pi-Hole with [Unbound](https://www.unbound.net). Unbound used to be my caching DNS resolver, so I don't need DNS like 8.8.8.8 (Google).

So first install Unbound with "sudo apt install unbound".

With the command "sudo wget -O /var/lib/unbound/root.hints https://www.internic.net/domain/named.root" we now download the list of DNS root servers.

Now it's time to configure Unbound. We create the file /etc/unbound/unbound.conf.d/pi-hole.conf and fill it with the following content.

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

If you can''t get anything out of my comments, you can read a more detailed description at [https://www.unbound.net/documentation/unbound.conf.html](https://www.unbound.net/documentation/unbound.conf.html). At the moment only the third and the last line are important. In the third line, the port is specified on which Unbound should listen. And in the last one you enter your address range for your own LAN.

With "systemctl start unbound.service" you test if unbound starts without problems. With "systemctl enable unbound.service" Unbound is started automatically.

Now enter Unbound at Pi-Hole as DNS. Just enter $PI-IP/admin in your browser (instead of $IP-IP use the IP under which the Raspberry is reachable in the LAN). Now the dashboard of Pi-Hole should be displayed. There we click on Login on the left side and log in. Now we select Settings -&gt; DNS on the left. Here I noticed that in the stable version of Pi-Hole you can enter the IP of your own DNS, but no port. After some Google-Fu I found out that it only works with the current beta version. Since I have nothing to lose, I switched to the current beta version with the following commands.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">echo "FTLDNS" | sudo tee /etc/pihole/ftlbranch
pihole checkout core FTLDNS 
pihole checkout web FTLDNS</code>
</pre>

Now you can enter 127.0.0.1#12345 under Settings -&gt; DNS (instead of 12345 you use the port specified in the configuration file (# is intentional and must be specified here).

Now we have to tell the devices in the network to use the Pi-Hole as DNS. To do this we either store the IP of the Raspberry Pi in the router or adjust the DNS settings on the respective devices (/etc/resolv.conf, netctl profiles etc.).

As a conclusion after about 24 hours with the combination of Pi-Hole and Unbound I can make the following statements so far:

- Apt is damn slow compared to pacman
- I'll never make friends with a distribution that uses sudo for every crap, so I'll probably activate the root account or install Arch again.
- If Unbound doesn't know the IP of a website yet, there will be a short delay until the page is displayed. After that everything goes very fast.
- If you look at the statistics of Pi-Hole, you will notice how much crap is filtered. With me it is up to 30.4 percent of all inquiries which disappear in the hole.

As far as the statistics are concerned, I noticed that they are updated every minute. Since I don't need current statistics and to avoid unnecessary write operations on the memory card I created the file /etc/pihole/pihole-FTL.conf and entered DBINTERVAL=60.0 there. Now the write process is still done every 60 minutes. This is absolutely sufficient for me, since the filter process continues as normal.

But this solution has a disadvantage for me. For various things like geo-blocking I use a VPN provider. The current provider (which will probably also apply to most other providers) unfortunately does not allow you to enter your own DNS to prevent so-called DNS leaks. So I will continue to use uBlock Origin in my browser. Especially since Pi-Hole can't filter some things like these annoying cookie hints.
