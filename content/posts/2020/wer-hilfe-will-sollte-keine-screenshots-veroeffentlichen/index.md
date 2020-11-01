---
title: Wer Hilfe will sollte keine Screenshots veröffentlichen
date: 2020-03-26T14:27:46+0100
categories:
- OSBN
- General
tags:
- Hilfe  
- Screenshots
- Termbin
slug: wer-hilfe-will-sollte-keine-screenshots-veroeffentlichen
---
Derzeit versuche ich wieder verstärkt auf diversen Plattformen den Nutzern bei Ihren Computerproblemen zu helfen. Hierbei ist mir aufgefallen, dass aktuell einige Nutzer beispielswese einen Screenshot einer Konfigurationsdatei erstellen (teilweise sogar mit einem Mobiltelefon), diesen dann auf eine Seite wie [picflash.org](https://picflash.org/) hochzuladen und das Bild dann im Beitrag einzubinden mit dem um Hilfe gebeten wird.

Lasst das! Bitte. Zum einen macht ihr euch damit selbst nur unnötig viel Arbeit. Und zum anderen verschreckt ihr damit viele der Leute die euch helfen wollen. Wenn ich zum Beispiel eure Konfigurationsdatei auf Fehler testen will möchte ich diese nicht erst von einem Screenshot abtippen müssen. Eher helfe ich gar nicht.

Sofern es also sinnvoll ist, kopiert den Text einfach in den Beitrag. Oder nutzt einen Pastebin-Dienst wie [termbin.com](https://termbin.com/). 

Um Termbin nutzen zu können, muss nur cat und netcat auf dem Rechner installiert sein. Nehmen wir beispielsweise einmal an, man hat Probleme mit Schriftarten und will die Datei fonts.conf veröffentlichen. Hierfür reicht folgender Befehl.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">cat fonts.conf | nc termbin.com 9999
</code>
</pre>

Als Ergebnis erhält man einen Link wie zum Beispiel [https://termbin.com/92e6](https://termbin.com/92e6) der auf den Dateiinhalt verweist. Gerade bei längeren Konfigurationsdateien wie der /etc/ssl/sshd_config ist es besser darauf zu verlinken als diese komplett in den Beitrag zu packen.

Serverseitig wird bei Termbin [https://github.com/solusipse/fiche](https://github.com/solusipse/fiche) eingesetzt. Wer also will, kann einen eigenen Pastebin-Dienst betreiben.