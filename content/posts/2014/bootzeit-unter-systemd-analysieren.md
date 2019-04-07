---
title: Bootzeit unter systemd analysieren
date: 2014-08-18T11:43:00+0100
categories:
- Linux
- OSBN
tags:
- Bootzeit
- Systemd
slug: bootzeit-unter-systemd-analysieren
---
Wenn man herausfinden will, welcher Service beim Booten mit systemd den Bootprozess verlangsamt, kann man dies mittels "systemd-analyze critical-chain" recht gut darstellen. 

<pre class="line-numbers language-bash">
<code class="language-bash">multi-user.target @28.246s
└─clamav-freshclam.service @27.657s +247ms
  └─clamav-daemon.service @3.042s +24.604s
    └─basic.target @3.026s
      └─sockets.target @3.023s
        └─dbus.socket @3.021s
          └─sysinit.target @3.017s
            └─ferm.service @2.756s +259ms
              └─network.target @2.752s
                └─networking.service @427ms +2.323s
                  └─local-fs.target @410ms
                    └─run-lock.mount @396ms +11ms
                      └─local-fs-pre.target @384ms
                        └─systemd-udevd.service @303ms +20ms
                          └─systemd-tmpfiles-setup-dev.service @208ms +80ms
                            └─systemd-journald.socket @114ms
                              └─-.mount @100ms</code>
</pre>

Die Angabe nach dem @ zeigt an, wie lange der Service aktiv ist. Die Zahl hinter dem + zeigt an, wie lange der Service zum Starten gebraucht hat. So kann man recht gut herausfinden, welcher Probleme macht.
