---
title: Git - Merge already sent commits
date: 2021-01-08T01:36:51+0100
categories:
- OSBN
tags:
- Git
- Commit
slug: git-merge-already-sent-commits
---
I have made the same change to several files in a Git repository. I created a commit for each file and submitted it to Github. In this case, one commit would have been sufficient. Now how can I merge the relevant commits into one commit afterwards?

First, run <mark>git rebase -i HEAD~X</mark> in the local working directory. Instead of X, enter the number of the latest commits you want to merge.

Now an editor should open automatically and in the first lines you should find, for example, the following.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">pick 67426ab Commit-Message
pick 56432tz Commit-Message
pick 45643io Commit-Message</code>
</pre>

To make one commit out of these three, replace the <mark>pick</mark> in lines 2 and 3 with <mark>squash</mark>. The "pick" in the first line remains unchanged. Finally, save the file. 

Now an editor should be reopened in which you can adjust the commit message if necessary. Because I used the same message for all three commits, I did not make any changes.

Finally, run <mark>git push --force origin HEAD</mark> to send the changes to Github. If you used a different alias for the repository (origin is the default) you have to change the command accordingly. If you are not sure, you can check the config file in the .git directory in your local working directory.

If you are not the only person making changes to the files, it is better to use [--force-with-lease](https://git-scm.com/docs/git-push#Documentation/git-push.txt---no-force-with-lease) instead of --force.

If you now look at the history of the repository, the relevant commits have been combined into one commit.
