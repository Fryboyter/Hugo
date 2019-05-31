---
title: Update Hugo
date: 2019-05-03T20:40:35+0200
categories:
- OSBN
- General
tags:
- Hugo
- Update
slug: update-hugo
---
Hugo is not installed on my webspace by default. Therefore I have to install new versions manually. To make this easier I built a small script.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">#!/bin/bash
BIN_DIR=$HOME/bin
CUR_VERSION="$("$BIN_DIR"/hugo version 2>/dev/null | cut -d'v' -f2 | cut -c 1-6)"
NEW_VERSION=$(curl --silent "https://api.github.com/repos/gohugoio/hugo/tags" | jq -r '.[0].name' | tr -d v)

echo "Hugo:  Current Version: $CUR_VERSION => New Version: $NEW_VERSION"

if ! [ "$NEW_VERSION" = "$CUR_VERSION" ]; then

  curl -L --output hugo.tar.gz "https://github.com/gohugoio/hugo/releases/download/v${NEW_VERSION}/hugo_${NEW_VERSION}_Linux-64bit.tar.gz"
  tar -C "${BIN_DIR}" -xvzf hugo.tar.gz hugo
  rm hugo.tar.gz
else
    echo "Die current Version of Hugo ist allready installed"
fi
</code>
</pre>

This checks whether the current version offered on Github is more current than the one available on the web space. If so, the current version of Github will be downloaded and installed on the webspace.