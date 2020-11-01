---
title: Fryboyter is now generated with Hugo
date: 2019-04-07T20:44:00+0100
categories:
- OSBN
- General
tags:
- Fryboyter
- Hugo
- Git
slug: fryboyter-is-now-generated-with-hugo
---
So far I have used the CMS [Bolt](https://bolt.cm/) for fryboyter.de. Basically I am satisfied with it. But somehow I have lately less and less desire to install the updates.

Therefore I looked at various tools in the last weeks, with which one can create static web pages. So you don't need PHP, no database, etc. Thus also the annoying updating of the side is unnecessary.

Finally I ended up with [ Hugo ](https://gohugo.io/). There are basically two reasons for this. On the one hand Hugo consists of only one file and on the other hand the static pages are created very fast.

But what kept me busy was how to create the website when I added new articles and how to upload it to the webspace. 

In the [Lab](https://lab.uberspace.de/guide_hugo.html) of Uberspace there is a manual how to install Hugo. Hugo runs as a service in the background and recreates the page as soon as something has changed. But as a consequence I have to take care of possible updates as soon as possible. It would be better if Hugo is started only to create the page and then shut down again. The easiest way would be to connect to the webspace via SSH, create the new article and then run Hugo manually. Simple? Yes. Cumbersome? Definitely. So it's out of the question.

The solution is, as so often, Git. First you create a directory on the webspace outside the document root. In this directory you create a so called bare-respository with " git init --bare". In comparison to a normal repository, this has no working tree. If you now look at the directory again, you will find the subdirectory "hooks" there. With these hooks certain tasks can be automated. For example, commands can be executed when the repository has received new data. For this you create the file post-receive in the directory "hooks" and add the following data and make it executable.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">GIT_REPO=$HOME/repository/fryboyter.git
TMP_GIT_CLONE=$HOME/tmp/git/fryboyter
PUBLIC_WWW=/var/www/virtual/$USER/html/fryboyter
git clone $GIT_REPO $TMP_GIT_CLONE
~/bin/hugo -s $TMP_GIT_CLONE --cleanDestinationDir -d $PUBLIC_WWW
rm -Rf $TMP_GIT_CLONE
exit
</code>
</pre>

This clones the contents of the repository into a temporary directory. Then Hugo deletes the already published website and recreates it. Then the temporary directory is deleted.

What is still missing is the data with which the website is created. These are created on your own computer. When this is done, you change to the respective directory and execute the following commands.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">git init
git add .
git commit -m "Beschreibung des Commit"
</code>
</pre>

With this you create a local repository, add all files of the directory and create a commit. If you upload it with "git push $adresse_des_repository" the file post-receive will be executed and the website will be created automatically. To update the page in the future, create / change the file in the local repository, create a new commit and upload the changes using git push.