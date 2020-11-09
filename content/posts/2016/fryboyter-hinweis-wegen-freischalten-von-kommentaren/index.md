---
title: Fryboyter - Hinweis wegen Freischalten von Kommentaren
date: 2016-12-30T15:08:00+0100
categories:
- Linux
- OSBN
tags:
- Fryboyter
- Hinweis
- Kommentare
slug: fryboyter-hinweis-wegen-freischalten-von-kommentaren
---
Ab und zu fragen bei mir Leute nach, wo denn ihre kürzlich geschriebenen Kommentare abgeblieben sind, da diese nicht sofort angezeigt werden. Dies liegt bei mir daran, dass alle Kommentare erst einmal von mir freigeschaltet werden (oder auch nicht). Einen Hinweis hierzu gab es bisher allerdings nicht.

Gestern habe ich mal wieder eine Nachfrage wegen eines nicht angezeigten Kommentars erhalten. Da ich gerade Urlaub habe, habe ich mich mal ein paar Minuten damit beschäftigt und die functions.php meines Wordpress-Themes erweitert. Wenn nun ein Kommentar abgeschickt wird, wird dieser für den Ersteller mit einem Hinweis angezeigt.

{{< image src="freischalten.png" alt="Kommentare freischalten" >}}

Unterm Strich ist diese Änderung kein Hexenwerk (hier nur der betreffende Codeteil der erstellen Funktion):

><?php if ( $comment->comment_approved == '0' ) : ?>
>< em class="comment-approved"><?php _e( 'Your comment is awaiting moderation.', 'fryboyter' ); ?>< /em>
><br />
><?php endif; ?>

Im Grunde wird nur geprüft ob in der Datenbank beim betreffenden Kommentar comment_approved den Wert 0 hat. Wenn ja, wird der Hinweis angezeigt. Dieser ist hier in Englisch angegeben. Das _e bewirkt in dem Fall eine automatische Übersetzung. In diesem Fall in die deutsche Sprache.
