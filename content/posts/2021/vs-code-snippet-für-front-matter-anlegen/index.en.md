---
title: VSCode - Create snippet for Front Matter
date: 2021-01-02T13:41:39+0100
categories:
- OSBN
- General
tags:
- VSCode
- Snippet
- Frontmatter
slug: vs-code-create-snippet-for-front-matter
---
I create my articles using Markdown files. At the beginning of this file is the so-called [front matter area](https://gohugo.io/content-management/front-matter#readout) where information such as the title, the date of publication or the tags of an article are entered.

Creating this area manually every time is annoying in the long run. Hugo, the static website generator I use, offers [templates](https://gohugo.io/content-management/archetypes/) for this purpose, so you can create a new article with a command like <mark>hugo new vscode-snippet-fuer-front-matter-anlegen.md</mark>.

However, I prefer to do everything with the editor. Currently I use VSCode. This editor offers so-called [snippets](https://code.visualstudio.com/docs/editor/userdefinedsnippets) with which you can create templates.

To do this, select "User snippets" under preferences in the "File" menu. In the drop-down menu that now appears, select "New global code snippet file..." and give the snippet file a meaningful file name.

Fill the file that now appears with the following content.

<pre class="line-numbers language-json" style="white-space:pre-wrap;">
<code class="language-json">{
  "Blog post frontmatter": {
    "prefix": "fmc",
    "description": "Creates frontmatter for Hugo articles",
    "body": [
      "---",
      "title: ${1}",
      "date: ${2:${CURRENT_YEAR}-${CURRENT_MONTH}-${CURRENT_DATE}T${CURRENT_HOUR}:${CURRENT_MINUTE}:${CURRENT_SECOND}+0100}",
	  "categories:", 
	  "- ${3}", 
	  "tags:",
    "- ${4}",
    "slug: ${5}",
      "---",
      "$0"
    ]
  }
}</code>
</pre>

In the first line you enter the name of the snippet that is displayed in the editor. The prefix serves as a shortcode with which you can quickly insert the content of the snippet. You can also enter something else here. I have chosen fmc (**f**ront **m**atter **c**reate).

The content of the snippet that is to be inserted automatically is created in the body. In my case, the front matter area is started with \-\-\-. This is followed by the title, the date, the categories, the tags and the slug through which the article can be reached. The front matter area is ended again with \-\-\-.

Finally, save the file. If you now create a new article, enter <mark>fmc</mark> in the file. This should cause a menu to appear in which you can execute the snippet. If you do this, the following content should be entered automatically.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">---
title: 
date: 2021-01-02T13:01:02+0100
categories:
- 
tags:
- 
slug: 
---

</code>
</pre>

In the code example above, some of you will have noticed ${1}, ${2} etc. These are jump marks.These are jump marks. Once you have inserted the snippet using <mark>fmc</mark>, you can use the tab key to jump to these places one after the other and thus fill in the relevant fields.
