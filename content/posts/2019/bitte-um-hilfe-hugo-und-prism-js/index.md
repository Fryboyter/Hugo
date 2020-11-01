---
title: Bitte um Hilfe - Hugo und Prism.js
date: 2019-03-22T17:35:00+0100
categories:
- OSBN
- Allgemein
tags:
- Hugo
- Prism
slug: bitte-um-hilfe-hugo-und-prism-js
---
Um mal wieder über den Tellerrand zu schauen, bin ich gerade dabei mich in Hugo einzuarbeiten. Als Grundlage dient hierfür fryboyter.de und die dort veröffentlicheten Artikel.

Da der Code-Highlighter von Hugo für mich einige Nachteile hat, wollte ich weiter Prism nutzen. Am Artikel https://fryboyter.de/index-twig-des-fryboyter-themes beiße ich mir allerdings die Zähne aus. Obwohl der Code in &lt;pre&gt; und &lt;code&gt; Tags gepackt ist interpretiert Hugo scheinbar die &lt;div&gt; Tags. In Zeile 2 wird unter Hugo also nur "Fryboyter" angezeigt. Und nicht "&lt;div class="header"&gt;&lt;h1&gt;&lt;a href="{{ paths.hosturl }}"&gt;Fryboyter&lt;/a&gt;&lt;/h1&gt;&lt;/div&gt;". Bei Code-Beispielen ist das irgendwie blöd...

Ausgehend davon, dass es ein Problem von Hugo in Kombination mit Prism ist, habe ich im Forum von Hugo eine [Support-Anfrage](https://discourse.gohugo.io/t/problems-with-hugo-and-prism-js/17357) gestellt. Leider konnte mir bisher aber noch niemand helfen.

Wegen der Support-Anfrage habe ich ich ein [Repository](https://codeberg.org/Fryboyter/hugo) auf Codeberg veröffentlicht in dem zwei Artikel vorhanden sind. [Einer](https://codeberg.org/Fryboyter/hugo/src/branch/master/content/posts/2017/nachbesserungen-an-bolt-cms.md) bei dem das Hervorheben des Codes klappt und [einer](https://codeberg.org/Fryboyter/hugo/src/branch/master/content/posts/2017/index-twig-des-fryboyter-themes.md) bei dem es nicht klappt. Ruft man den "Problem-Artikel" direkt bei Codeberg auf, kommt es zu gleichen fehlerhaften Anzeige. Und das obwohl hier Prism gar nicht geladen werden sollte. Also ich vermutlich eher Hugo oder Markdown an sich das Problem.

Daher möchte ich kurz in die Runde fragen, ob jemand eine Idee hat wie man das Problem lösen kann?&nbsp;Auf einen anderen Code-Highlighter möchte ich möglichst nicht umsteigen.