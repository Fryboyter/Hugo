---
title: Defer und Prism
date: 2019-01-01T11:59:00+0100
categories:
- OSBN
- Allgemein
tags:
- Prism
- Defer
slug: defer-und-prism
---
Binde Javascript mit defer ein, haben sie gesagt. Für die Syntaxhervorhebung nutze ich Prism. Aufgrund des Ratschlags habe ich daher das Script per &lt;script defer src=\"<a href="https://fryboyter.de/theme/fryboyter/js/prism.js?d46722219d" target="_blank">/theme/fryboyter/js/prism.js</a>"&gt;&lt;/script&gt; eingebunden. Keine gute Idee wie ich festgestellt habe.

In einigen Fällen habe ich zum Beispiel folgenden Code hervorgehoben:

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">$IP_DES_RASPBERRY:$PORT_VON_CADDY
root /pfad/zum/Mirrorverzeichnis
gzip
browse</code>
</pre>

Beim ersten Aufruf des Artikels wurde allerdings folgendes angezeigt:

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">$IP_DES_RASPBERRY:$PORT_VON_CADDY
root /pfad/zum/Mirrorverzeichnis
gzip
browse
$IP_DES_RASPBERRY:$PORT_VON_CADDY</code>
</pre>

Kurz gesagt die erste Zeile wird am Ende des Blocks noch einmal angezeigt. Nicht gut. Aktualisiert man die Seite, wird es aber korrekt angezeigt. Beim jeweils ersten Aufruf ist mir dann aufgefallen, dass folgender Fehler in den Entwicklerwerkzeugen des Browsers angezeigt wird.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-javascript">Uncaught TypeError: Cannot read property 'children' of null
    at prism.js?d46722219d:18
    at Array.forEach (&lt;anonymous&gt;)
    at n (prism.js?d46722219d:18)
    at NodeList.forEach (&lt;anonymous&gt;)
    at prism.js?d46722219d:18</code>
</pre>

Ok Zeile 18 der Datei prism.js ist wohl das Problem.

<pre class="line-numbers language-javascript" style="white-space:pre-wrap;">
<code class="language-javascript">!function(){if(&quot;undefined&quot;!=typeof self&amp;&amp;self.Prism&amp;&amp;self.document){var e=&quot;line-numbers&quot;,t=/\n(?!$)/g,n=function(e){var n=r(e),s=n[&quot;white-space&quot;];if(&quot;pre-wrap&quot;===s||&quot;pre-line&quot;===s){var l=e.querySelector(&quot;code&quot;),i=e.querySelector(&quot;.line-numbers-rows&quot;),a=e.querySelector(&quot;.line-numbers-sizer&quot;),o=l.textContent.split(t);a||(a=document.createElement(&quot;span&quot;),a.className=&quot;line-numbers-sizer&quot;,l.appendChild(a)),a.style.display=&quot;block&quot;,o.forEach(function(e,t){a.textContent=e||&quot;\n&quot;;var n=a.getBoundingClientRect().height;i.children[t].style.height=n+&quot;px&quot;}),a.textContent=&quot;&quot;,a.style.display=&quot;none&quot;}},r=function(e){return e?window.getComputedStyle?getComputedStyle(e):e.currentStyle||null:null};window.addEventListener(&quot;resize&quot;,function(){Array.prototype.forEach.call(document.querySelectorAll(&quot;pre.&quot;+e),n)}),Prism.hooks.add(&quot;complete&quot;,function(e){if(e.code){var r=e.element.parentNode,s=/\s*\bline-numbers\b\s*/;if(r&amp;&amp;/pre/i.test(r.nodeName)&amp;&amp;(s.test(r.className)||s.test(e.element.className))&amp;&amp;!e.element.querySelector(&quot;.line-numbers-rows&quot;)){s.test(e.element.className)&amp;&amp;(e.element.className=e.element.className.replace(s,&quot; &quot;)),s.test(r.className)||(r.className+=&quot; line-numbers&quot;);var l,i=e.code.match(t),a=i?i.length+1:1,o=new Array(a+1);o=o.join(&quot;&lt;span&gt;&lt;/span&gt;&quot;),l=document.createElement(&quot;span&quot;),l.setAttribute(&quot;aria-hidden&quot;,&quot;true&quot;),l.className=&quot;line-numbers-rows&quot;,l.innerHTML=o,r.hasAttribute(&quot;data-start&quot;)&amp;&amp;(r.style.counterReset=&quot;linenumber &quot;+(parseInt(r.getAttribute(&quot;data-start&quot;),10)-1)),e.element.appendChild(l),n(r),Prism.hooks.run(&quot;line-numbers&quot;,e)}}}),Prism.hooks.add(&quot;line-numbers&quot;,function(e){e.plugins=e.plugins||{},e.plugins.lineNumbers=!0}),Prism.plugins.lineNumbers={getLine:function(t,n){if(&quot;PRE&quot;===t.tagName&amp;&amp;t.classList.contains(e)){var r=t.querySelector(&quot;.line-numbers-rows&quot;),s=parseInt(t.getAttribute(&quot;data-start&quot;),10)||1,l=s+(r.children.length-1);s&gt;n&amp;&amp;(n=s),n&gt;l&amp;&amp;(n=l);var i=n-s;return r.children[i]}}}}}();</code>
</pre>

Ok, ich verstehe so ziemlich rein gar nichts. Es hilft mir also nicht weiter. Nachdem ich etwas im Bugtracker von Prism gesucht habe, habe ich dort ein bereits behobenen Problem mit bezüglich der Einbindung per defer gefunden. Dessen Symptome waren aber nicht mit meinem Problem vergleichbar. Trotzdem habe ich mal schaut was passiert, wenn ich Prism nicht mit defer einbinde. Und schon ist mein Problem verschwunden. Da es hinsichtlich der Ladezeit gefühlt keinen Unterschied gibt ob ich nun defer verwende oder nicht, habe ich defer einfach wieder entfernt. Und was lernen wir daraus? Nicht jeder Tipp zur Seitenoptimierung macht pauschal Sinn.