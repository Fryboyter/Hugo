---
title: Wie oft bekomme ich Spam-Kommentare von einer bestimmten IP-Adresse
date: 2013-04-03T17:55:00+0100
categories:
- OSBN
- Allgemein
tags:
- Anzahl
- Spam
- IP-Adresse
slug: wie-oft-bekomme-ich-spam-kommentare-von-einer-bestimmten-ip-adresse
---
Das von mir eingesetzte Antispam-Plugin Antispam Bee macht heute wieder Überstunden. Allein heute wurden schon Spam-Kommentare im dreistelligem Bereich erfolgreich gefiltert. Da ich gerade mit DBeaver auf der Wordpress-Datenbank war, hat es mich mal interessiert, wie oft Spam von einer bestimmten IP-Adresse bei mir abgeladen wurde. Hierzu habe ich mir eine kleine Abfrage gebastelt.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-sql">SELECT comment_author_IP
COUNT(comment_author_IP) AS haeufigkeit
FROM wp_comments
WHERE comment_approved="spam"
GROUP BY comment_author_ip
ORDER BY haeufigkeit DESC
</code>
</pre>

Hiermit wird angezeigt welche IP wie oft einen als Spam gekennzeichneten Kommentar abgelassen hat. Das ganze wird dann nach der Häufigkeit absteigend sortiert.

{{< image src="Spam_IP_Statistik.png" alt="Statistik Spam IP" >}}

<p>Wie man sieht, geben manche IP-Adressen (ich habe diese mal wegen Datenschutz verpixelt. Nur soviel, die Top 2 gehören zu OVH) einfach keine Ruhe.

Wie handhabt ihr solche "Dauernerver"? Lasst ihr sie einfach weiterspammen und von eurem Spamschutz ausfiltern? Oder setzt ihr ab einer gewissen Grenze dem ganzen Einhalt? Zum Beispiel über einen Eintrag in der .htaccess-Datei?
