---
title: VSCode friert nach dem Starten ein
date: 2021-05-16T10:59:19+0200
categories:
  - OSBN
  - Allgemein
tags:
  - VSCode
slug: vs-code-friert-nach-dem-starten-ein
---

Wenn ich aktuell unter Arch Linux die OSS-Version des Editor VSCode starten will, startet diese zwar, friert sofort ein so dass man das Programm nur noch gewaltsam beenden kann. Die Lösung ist aber erfreulicherweise ziemlich einfach.

Öffnet man die Datei /usr/bin/code-oss mit einem Editor (vorzugsweise nicht VSCode ;-) ) sollte der Inhalt wie folgt aussehen.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">ELECTRON_RUN_AS_NODE=1 exec electron11 /usr/lib/code/out/cli.js /usr/lib/code/code.js "$@"</code>
</pre>

Alles was man machen muss ist electron11 auf electron zu ändern. Danach sollte VSCode wieder normal starten.

Vermutlich handelt es sich hierbei um einen Bug seitens Arch Linux. VSCode benötigt als Abhängigkeit das Paket electron (aktuell Version 12). Mit diesem wird die Datei /usr/bin/electron installiert. Im Paket code wurde allerdings letzten Monat /usr/bin/electron auf /usr/bin/electron11 geändert (https://github.com/archlinux/svntogit-community/commit/412cf018280fd9b9f612eb84075354b9fe555af8). Vermutlich weil VSCode zu der Zeit noch von Version 11 von electron abhängig war. Und nach dem Update auf Version 12 wurde vermutlich vergessen es entsprechend anzupassen. Aber das ist nur eine Vermutung. Eventuell betrifft das Problem auch andere Distributionen (und ggf. auch die normale Version von VSCode)
