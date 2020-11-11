---
title: Meine Konfigurationsdatei von nano
date: 2012-12-08T14:15:00
categories:
- Linux
- OSBN
tags:
- Nano
- Konfigurationsdatei
slug: meine-konfigurationsdatei-von-nano
---
Bis Ende des Jahres will ich diverse Konfigurationsdateien anpassen und ggf. aufräumen. Bei dieser Gelegenheit werde ich diese dann veröffentlichen. Heute habe ich mit nano angefangen. Nano ist mein bevorzugter Editor wenn ich keine grafische Oberfläche zur Verfügung habe oder ich einfach keine Lust habe größere Geschütze wie Bluefish zu starten. Das ist nun dabei herausgekommen.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">## Sample initialization file for GNU nano.
##
## Please note that you must have configured nano with --enable-nanorc
## for this file to be read! Also note that this file should not be in
## DOS or Mac format, and that characters specially interpreted by the
## shell should not be escaped here.
##
## To make sure a value is disabled, use "unset ".
##
## For the options that take parameters, the default value is given.
## Other options are unset by default.
##
## Quotes inside string parameters don't have to be escaped with
## backslashes. The last double quote in the string will be treated as
## its end. For example, for the "brackets" option, ""')>]}" will match
## ", ', ), >, ], and }.

## Backup files to filename~.
set backup

## The directory to put unique backup files in.
set Backupdir  "/home/nutzer/Dokumente/nanobackup"

## Constantly display the cursor position in the statusbar. Note that
## this overrides "quickblank".
set const

## Enable ~/.nano_history for saving and reading search/replace strings.
set historylog
## Don't convert files from DOS/Mac format.
set noconvert
## Fix numeric keypad key confusion problem.
set rebindkeypad
## Make the Home key smarter. When Home is pressed anywhere but at the
## very beginning of non-whitespace characters on a line, the cursor
## will jump to that beginning (either forwards or backwards). If the
## cursor is already at that position, it will jump to the true
## beginning of the line.
set smarthome

## Use smooth scrolling as the default.
set smooth

## Enable soft line wrapping (AKA full line display).
set softwrap

## Allow nano to be suspended.
set suspend

bind ^S research main

## Syntax-Highlightning
## Nanorc files
include "/usr/share/nano/nanorc.nanorc"

## Makefiles
include "/usr/share/nano/makefile.nanorc"

## Cascading Style Sheets
include "/usr/share/nano/css.nanorc"

## HTML
include "/usr/share/nano/html.nanorc"

## PHP
include "/usr/share/nano/php.nanorc"

## TeX
include "/usr/share/nano/tex.nanorc"

## Patch
files include "/usr/share/nano/patch.nanorc"

## Manpages
include "/usr/share/nano/man.nanorc"

## Perl
include "/usr/share/nano/perl.nanorc"

## Python
include "/usr/share/nano/python.nanorc"

## Ruby
include "/usr/share/nano/ruby.nanorc"

## Java
include "/usr/share/nano/java.nanorc"

## Bourne shell scripts
include "/usr/share/nano/sh.nanorc"

## XML-type files
include "/usr/share/nano/xml.nanorc"</code>
</pre>

Eventuell kann es ja jemand als Grundlage gebrauchen. Alles was ich nicht benötigt habe, habe ich aus der Datei entfernt. Die komplette Datei nanorc findet man unter /etc/. Diese am besten nicht editieren sondern als .nanorc in das Homeverzeichnis kopieren.
