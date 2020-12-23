---
title: Hooks under Mercurial
date: 2019-05-05T10:31:55+0200
categories:
- OSBN
- General
tags:
- Mercurial
- Hooks
slug: hooks-under-mercurial
---
Yesterday I had published an [article](/git-zu-mercurial-konvertieren/) about the version control Mercurial. The project in question was managed with Git. There were also some hooks present. For example, you can use them to execute commands automatically when a new commit is uploaded. For this you use the hook "post-receive" as I recently described it in an [article](/fryboyter-wird-nun-mit-hugo-erzeugt/). Tux also commented that this is also possible with Mercurial.

Absolutely correct in itself, but either the documentation is in need of improvement or I didn't get it. I assume the latter at this point. 

Under [https://www.mercurial-scm.org/wiki/Hook](https://www.mercurial-scm.org/wiki/Hook) the whole thing is described. Every time I add a commit, a hook should be executed. So I entered the following in the configuration file hgrc.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">[hooks]
commit = /pfad/zur/Datei/commithook
</code>
</pre>

Under /path/to/file/ I created the commithook file and entered the script that should be executed. Then I made the file executable.

But it didn't work. The commits arrived, but the hook was not executed. After some Google-Fu I noticed why. The commit hook only seems to work if you commit it directly in the repository. Not if you push it in, though.

Therefore you have to enter the following into the file hgrc.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">[hooks]
changegroup = /pfad/zur/Datei/commithook
</code>
</pre>

Herewith the hook is always executed when committing.
