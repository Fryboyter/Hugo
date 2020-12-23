---
title: Suche von fzf beschleunigen
date: 2018-09-25T23:53:00+0100
categories:
- Linux
- OSBN
tags:
- Fuzzy Finder
- Beschleunigen
slug: suche-mit-fzf-beschleunigen
---
Vor einigen Wochen habe ich einen [Artikel](/fuzzy-finder-fuer-die-zsh/) über fzf veröffentlicht. In diesem habe ich angemerkt, dass fzf zum suchen den Befehl find verwendet, was in bestimmten Fällen nicht gerade schnell ist. Was kann man also dagegen unternehmen?

Die Lösung lautet FZF_DEFAULT_COMMAND und fd. Wie in einem anderen Artikel [angemerkt](/fd-finden-einmal-anders/) handelt es sich bei fd um eine schnellere Alternative zu find. Damit fzf fd verwendet, trägt man folgendes unter die bereits vorhandenen Einträge für fzf in der .zshrc ein.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">export FZF_DEFAULT_COMMAND='fd --type f'</code>
</pre>

Wenn man nun noch den Terminal Emulator neu startet bzw. die Konfiguration der zsh neu einliest, sollte fzf deutlich schneller Ergebnisse ausspucken. Anstelle von fd kann man auch [ripgrep](/ripgrep-grep-auf-steroide/) nutzen. Hier würde der Eintrag zum Beispiel folgendermaßen aussehen.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">export FZF_DEFAULT_COMMAND='rg --files --no-ignore --hidden --follow'</code>
</pre>

Das beide Einträge sollten auch unter anderen Shells wie der Bash funktionieren.
