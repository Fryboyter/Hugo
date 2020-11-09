---
title: Wie Probleme zwischen sddm und den Nvidia-Treibern mein Problem mit Steam gelöst haben
date: 2017-03-06T12:04:00+0100
categories:
- Linux
- OSBN
tags:
- Probleme
- Sddm
- Nvidia
- Steam
slug: wie-probleme-zwischen-sddm-und-den-nvidia-treibern-mein-problem-mit-steam-geloest-haben
---
Vor ein paar Wochen wurden die Nvidia-Treiber unter Arch auf Version 378.13 aktualisiert. Eine Installation und ein Neustart hatten immer einen black Screen auf beiden Monitoren zur Folge. Journalctl war der Meinung dass sddm nichts mit der OpenGL-Version anfangen kann (Unrecognized OpenGL Version).

Da alle Suchergebnisse, die sich auf "Unrecognized OpenGL Version" beziehen, absolut nichts gebracht haben, habe ich ein Downgrade der Pakete nvidia-dkms sowie nvidia-utils gewagt. Hierzu habe ich das Tool [downgrade](https://aur.archlinux.org/packages/downgrade) aus dem AUR verwendet und beide Pakete in Version 375.26-2 installiert. Und siehe da, sddm hat wieder funktioniert und ich konnte mich normal an KDE Plasma anmelden.

Am Wochenende hatte ich jetzt mal etwas Zeit und ich habe mich auf das Problem gestürzt, da man Downgrades unter Arch eigentlich vermeiden sollte. Da Version 375.26-2 ja funktioniert ging ich davon aus, dass Version 378.13 das Problem ist. Und ich sollte mich irren. Nach x Fehlversuchen habe ich wieder die alte, funktionierende Version der Nvidia-Treiber installiert und wollte fürs erste erst einmal aufgeben. Irgendwie bin ich dann noch auf die Idee gekommen mir glxinfo aus dem AUR zu installieren. Nachdem ich dann glxinfo | grep OpenGL ausgeführt habe, ist mir mein Gesicht mal so richtig eingeschlafen. Eigentlich hatte ich erwartet, dass die Ausgabe etwas mit Nvidia ausspuckt. Statt dessen wurde ich mit Mesa konfrontiert. Um es mal mit dem fränkischen Fragewort auszudrücken... Hä?

Böses ahnend habe ich dann mal nachgeschaut, ob die Pakete nvidia-libgl und lib32-nvidia-libgl installiert sind. Natürlich nicht. Aber warum nicht? Ich bin mir absolut sicher, dass ich diese Pakete installiert hatte. Und ich habe absolut keinen Schimmer warum ich diese deinstalliert haben sollte. Hier wären wir dann wieder beim fränkischen Fragewort mit zwei Buchstaben.

Nachdem ich dann beide Pakete installiert und die Nvidia-Treiber aktualisiert hatte, hatte auch sddm wieder ein Einsehen und der Rechner konnte wie gewohnt gestartet werden.

Einen schönen Nebeneffekt hat das Ganze auch noch. Vor einigen Wochen hatte ich nach einem Update von Steam festgestellt, dass alle Spiele total ruckeln und quasi unspielbar waren. Da ich aktuell fast nur Overwatch bzw. Quake Live unter Windows spiele, habe ich mich damit aber nicht befasst. Aber wenigstens hatte ich am Wochenende mal einen halbwegs vorzeigbaren Geistesblitz und habe 1 und 1 zusammengezählt. Nach mehreren Runden CS:GO war ich mir sicher, dass das Problem mit Steam ebenfalls an den fehlenden libgl-Paketen lag.

Warum aber Version 375.26-2 funktioniert und wieso die libgl-Pakete bei mir nicht (mehr) installiert waren, wird wohl ein Rätsel bleiben. Allerdings haben auch einige andere Arch-Nutzer die sddm einsetzen mit den aktuellen Nvidia-Treibern einen Blackscreen. Vielleicht liegt das Problem dieses eine mal nicht auf meiner Seite...
