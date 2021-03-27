---
title: Use Github with Mercurial
date: 2021-03-27T23:17:25+0100
description: Instructions on how to use a Git repository with the Mercurial version management system by means of the hg-git plugin
categories:
- OSBN
- General
tags:
- Github
- Mercurial
- Hg-git
slug: use-github-with-mercurial
---
A week or two ago I broke one of my git repositories. Because the solution cost me a lot of time, too many nerves and two commits, I have now returned to [Mercurial](https://www.mercurial-scm.org). This tool may not be as powerful as Git, but the error messages and documentation are much easier to understand in my opinion.

However, I still want to use Github because of its widespread use. Be it to publish something there myself or to participate in third-party projects. Mercurial offers a plugin called [hg-git](https://foss.heptapod.net/mercurial/hg-git) for this purpose. With it, you can download a Git repository and it is automatically converted into a Mercurial repository locally. If you now make changes, they are then changed to be compatible with Git before being uploaded to a Git repository. Setting up hg-git is also quite simple.

For the following instructions, I assume that both Mercurial and python-dulwich are installed on the computer and that the directory Projects exists in the home directory. Of course, you can give the directory a different name.

First, change to the Projects directory in the terminal emulator of your choice and download the hg-git files there.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">cd ~/Projects
hg clone https://foss.heptapod.net/mercurial/hg-git hg-git</code>
</pre>

Alternatively, you can install hg-git via the package management of your distribution. 

Next, add the following content to the .hgrc file in the home directory. If the file does not yet exist, simply create it and enter the three lines.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">[extensions]
hgext.bookmarks =
hggit = ~/Projects/hg-git/hggit</code>
</pre>

Line two activates the plugin Bookmarks, which in this case simulates branches. Line three activates the hg-git plugin that we just downloaded.

In the Projects directory, we now download a Git repository with the following command (please adapt the Github address and the target directory fryboyter.git to your own circumstances).

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">hg clone git@github.com:Fryboyter/Hugo.git fryboyter.hg</code>
</pre>

Because this converts from Git to Merurial, it may take some time depending on the size of the repository.

Next, change to the directory in which the Mercurial repository now created is located. In this example, this is fryboyter.hg. Finally, execute the command <mark>hg bookmark -f main</mark> there. Instead of main, you must enter the name of the main branch. Otherwise Mercurial will not recognise any changes during a push.

Now everything should work. In my tests, I was able to pull from Github and push to Github without any problems. That's all I really need in my case. What I noticed during the whole process is that the local Mercurial repository is less than 30 MB in size. The local Git repository, on the other hand, takes up a bit more than 60 MB of space. That's not the end of the world, but it's still an interesting detail.
