---
title: Repository mit Submodulen klonen
date: 2020-07-04T15:57:04+0200
categories:
- OSBN
- Allgemein
tags:
- Git  
- Submodule
slug: repository-mit-submodulen-klonen
---
Ich habe eben ein Repository bei Github auf einen meiner Rechner geklont und festgestellt, das ein Teil der Daten nicht vorhanden ist. Was daran lag, dass der fehlenden Teil als [Submodul](https://git-scm.com/book/de/v2/Git-Tools-Submodule) eingebunden ist. Die Daten liegen also in einem anderen Repository. Um ein Projekt inklusive der Submodule zu klonen kann man folgende Befehl nutzen.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">git clone --recursive &lt;LINK-ZUM-REPOSITORY&gt;</code>
</pre>

Was aber wenn man das Hauptprojekt bereits geklont hat? Man wechselt einfach in das Verzeichnis und führt folgende Befehle aus. Hiermit werden nachträglich auch die Dateien der Submodule heruntergeladen.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">git submodule init
git submodule update</code>
</pre>
