---
title: VSCode - Snippet für Front Matter anlegen
date: 2021-01-02T13:41:39+0100
categories:
- OSBN
- Allgemein
tags:
- VSCode
- Snippet
- Frontmatter
slug: vs-code-snippet-für-front-matter-anlegen
---
Meine Artikel erzeuge ich mittels Markdown-Dateien. Am Beginn dieser Datei ist der sogenannte [Front-Matter-Bereich](https://gohugo.io/content-management/front-matter#readout) vorhanden in dem Informationen wie der Titel, das Datum der Veröffentlichung oder die Tags eines Artikels hinterlegt werden.

Diesen Bereich jedes mal manuell zu erzeugen ist auf Dauer nervig. Der von mir verwendete statische Website-Generator Hugo bietet hierfür [Templates](https://gohugo.io/content-management/archetypes/) an, so dass man mit einem Befehl wie <mark>hugo new vscode-snippet-fuer-front-matter-anlegen.md</mark> einen neuen Artikel anlegen kann.

Ich bevorzuge es allerdings alles mit dem Editor zu machen. Aktuell nutze ich VSCode. Dieser bietet sogenannte [Snippets](https://code.visualstudio.com/docs/editor/userdefinedsnippets) mit denen man Vorlagen erstellen kann.

Hierfür wählt man in den Einstellungen im Menü "Datei" "Benutzerausschnitte" aus. Im nun angezeigten Drop-Down-Menü wählt man "Neue globale Codeausschnittsdatei..." aus und gibt der Snippet-Datei einen aussagekräftigen Dateinamen.

Die nun angezeigte Datei füllt man mit folgendem Inhalt.

<pre class="line-numbers language-json" style="white-space:pre-wrap;">
<code class="language-json">{
  "Blog post frontmatter": {
    "prefix": "fmc",
    "description": "Erzeugt Frontmatter für Hugo-Artikel",
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

In der ersten Zeile gibt man den Namen des Snippets an der im Editor angezeigt wird. Der Prefix dient als Shortcode mit dem man den Inhalt des Snippets schnell einfügen kann. Hier kann man auch etwas anderes eintragen. Ich habe mir für fmc (**f**ront **m**atter **c**reate) entschieden.

Im Body wird der Inhalt des Snippets angelegt, der automatisch eingefügt werden soll. In meinem Fall wird mit \-\-\- der Front-Matter-Bereich begonnen. Dann folgt der Titel, das Datum, die Kategorieren, die Tags sowie der Slug über den der Artikel erreichbar ist. Mit \-\-\- wird der Front-Matter-Bereich wieder beendet.

Abschließend speichert man die Datei ab. Legt man nun einen neuen Artikel an, trägt man in der Datei <mark>fmc</mark> ein. Dies sollte bewirken, dass ein Menü erscheint in dem man das Snippet ausführen kann. Macht man das, sollte automatisch folgender Inhalt eingetragen werden.

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

Im obigen Code-Beispiel werden dem einen oder anderen sicherlich ${1}, ${2} usw. aufgefallen sein. Dies sind Sprungmarken. Hat man mittels <mark>fmc</mark> das Snippet eingefügt, kann man mit der Tabulator-Taste diese Stellen der Reihe nach anspringen und somit die betreffenden Bereiche ausführen.
