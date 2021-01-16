---
title: Update to Wallabag 2.4.0 - Row size to large
date: 2020-12-15T20:47:05+0100
categories:
- OSBN
- General
tags:
- Wallabag
- Mariadb
slug: wallabag-row-size-to-large
---
[Wallabag](https://wallabag.org/en) is a self-hosting tool that allows you to save interesting web pages for later reading. A few days ago version 2.4.0 was released to which I wanted to update my instance.

Unfortunately the update aborted with the (abbreviated) error message "Syntax error or access violation: 1118 [Row size too large](https://mariadb.com/kb/en/innodb-row-formats-overview/#maximum-row-size)." and the installation was no longer usable.

The reason is that at least one table in the Wallabag database has the row format "REDUNDANT" or "COMPACT". You can display the affected tables with the following database query.

<pre class="line-numbers language-sql" style="white-space:pre-wrap;">
<code class="language-sql">SELECT CONCAT(TABLE_SCHEMA, '.', TABLE_NAME) 
FROM information_schema.TABLES 
WHERE ENGINE = 'InnoDB' AND ROW_FORMAT IN('Redundant', 'Compact') 
AND TABLE_NAME NOT IN('SYS_DATAFILES', 'SYS_FOREIGN', 'SYS_FOREIGN_COLS', 'SYS_TABLESPACES', 'SYS_VIRTUAL', 'SYS_ZIP_DICT', 'SYS_ZIP_DICT_COLS');</code>
</pre>

As the output was limited to only a few tables and I don't want to do a more complex solution, I changed the row format manually to "DYNAMIC" with the following command.

<pre class="line-numbers language-sql" style="white-space:pre-wrap;">
<code class="language-sql">ALTER TABLE $TABLENAME ROW_FORMAT=DYNAMIC;</code>
</pre>

Instead of $TABLENAME, enter one of the tables that were displayed with the database query. 

Once you have changed the relevant tables accordingly, the update should complete without errors and the relevant Wallabag instance should be usable afterwards.
