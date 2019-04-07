---
title: Spam mit zwei Zeichen bekämpfen
date: 2016-10-12T17:05:00+0100
categories:
- OSBN
- Allgemein
tags:
- Spam
- Bekämpfen
slug: spam-mit-zwei-zeichen-bekaempfen
---
Seit ein paar Wochen erhalte ich alle paar Tage Spam-Kommentare bei denen der Text nur aus zwei Buchstaben besteht. Antispam Bee hat hiermit wohl (noch) Probleme, da es immer unterschiedliche Zeichen sind. IP und die Spam-Adresse sind auch immer unterschiedlich. Leider finde ich in Wordpress nirgends die Möglichkeit die Mindestlänge eines Kommentars einzustellen.

Daher musste die functions.php meines Themes mal wieder herhalten.In diese habe ich folgendes hinterlegt:

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">add_filter( 'preprocess_comment', 'minimum_comment_length' );
function minimum_comment_length( $commentdata ) {
    $minimumCommentLength = 3;
    if ( strlen( trim( $commentdata['comment_content'] ) ) < $minimumCommentLength ){
    wp_die( 'Your comment must be at least ' . $minimumCommentLength . ' characters long.' );
    }
    return $commentdata;
}</code>
</pre>

In Zeile 3 kann man angeben, wie lange der Kommentar mindestens sein muss. In Zeile 5 kann man die Meldung angeben, die angezeigt wird, wenn der Kommentar nicht lang genug ist.

Mal schauen was passiert...