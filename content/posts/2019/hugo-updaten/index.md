---
title: Hugo updaten
date: 2019-05-03T20:40:35+0200
categories:
- OSBN
- Allgemein
tags:
- Hugo
- Update
slug: hugo-updaten
---
Hugo ist auf meine Webspace nicht von Haus aus installiert. Daher muss ich neue Versionen manuell installieren. Um mir dies zu erleichtern habe ich mir ein kleines Script gebaut.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">#!/bin/bash
BIN_DIR=$HOME/bin
CUR_VERSION="$("$BIN_DIR"/hugo version 2>/dev/null | cut -d'v' -f2 | cut -c 1-6)"
NEW_VERSION=$(curl --silent "https://api.github.com/repos/gohugoio/hugo/tags" | jq -r '.[0].name' | tr -d v)

echo "Hugo:  Aktuelle Version: $CUR_VERSION => Neue Version: $NEW_VERSION"

if ! [ "$NEW_VERSION" = "$CUR_VERSION" ]; then

  curl -L --output hugo.tar.gz "https://github.com/gohugoio/hugo/releases/download/v${NEW_VERSION}/hugo_${NEW_VERSION}_Linux-64bit.tar.gz"
  tar -C "${BIN_DIR}" -xvzf hugo.tar.gz hugo
  rm hugo.tar.gz
else
    echo "Die aktuelle Version von Hugo ist bereits installiert"
fi
</code>
</pre>

Hiermit wird geprüft, ob die aktuelle Version die auf Github angeboten wird, aktueller ist als die, die auf dem Webspace vorhanden ist. Wenn ja, wird die aktuelle Version von Github heruntergeladen und auf dem Webspace gespeichert.