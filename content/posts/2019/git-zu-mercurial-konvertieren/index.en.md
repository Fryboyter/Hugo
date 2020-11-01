---
title: Convert Git to Mercurial
date: 2019-05-04T01:45:03+0200
categories:
- OSBN
- General
tags:
- Git
- Convert
- Mercurial
slug: convert-git-to-mercurial
---
It often happens that someone switches from one version control system to Git. Sometimes, however, someone wants to switch from Git to another solution. Recently I had such a request. Mercurial was wanted.

The relevant git repository was still quite fresh, but there were already commits in the low three-digit range. Too many to create manually in Mercurial.

Which is not necessary. Mercurial offers the possibility to convert.

Let's assume that the home directory contains the directory repository. In this directory there is the directory blog.git where the Git repository is located. 

First you have to create the subdirectory blog.hg in the repository directory and switch to it. There you create a Mercurial repository with "hg init". This creates the directory .hg. In this directory you create the file hgrc with the following content.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">[extensions]
hgext.convert=
</code>
</pre>

This enables the extension with which the conversion can be performed.

Now execute the following command in the directory blog.hg.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">hg convert --datesort ~/repository/blog.git ~/repository/blog.hg
</code>
</pre>

It'll take a while. But if everything goes as planned, you should get a Mercurial repository with all commits, files, etc. as in the Git repository. If you look at the directory blog.hg, you will still only see the subdirectory .hg. The problem can be solved by executing the command "hg update". If you then look in the directory blog.hg you can also see all the files you originally added to the Git repository.