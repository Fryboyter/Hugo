---
title: Insert date in Sublime Text
date: 2019-04-27T22:46:29+0200
categories: 
- OSBN
- General
tags:
- Sublime Text
- Date
- Hugo
slug: insert-date-in-sublime-text
---
If you create an article with Hugo you have to enter the date in the markdown file in the form of 2019-04-27T22:18:13+0200. In contrast to [Jörg](https://blog.jkip.de/fuer-pcmanfm-als-datumsformat-iso-8601-einstellen/) this annoys me quite a bit. 

So I thought about how I could automate the input. For my preferred editor Sublime Text there is the plugin [InsertDate](https://packagecontrol.io/packages/InsertDate) available. After the installation you choose the correct time zone. After that, it's best to create a shortcut to insert the date. To do this, select "Key Bindings" from the "Preferences" menu. In the right window enter the following code between the square brackets and save the file.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">{ "keys": ["shift+f5"], "command": "insert_date", "args": {"format": "%Y-%m-%dT%H:%M:%S%z"} },
</code>
</pre>

Instead of shift+f5 you can also use another key combination. From now on you can insert the current date including time and the difference to UTC in ISO 8601 format with the defined shortcut.