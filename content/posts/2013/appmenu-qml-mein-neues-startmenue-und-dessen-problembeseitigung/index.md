---
title: AppMenu QML - Mein neues Startmenü und dessen Problembeseitigung
date: 2013-08-19T20:12:00+0100
categories:
- Linux
- OSBN
tags:
- QML
- KDE
- Plasma
- Startmenü
slug: appmenu-qml-mein-neues-startmenue-und-dessen-problembeseitigung
---
Ich heute mal wieder auf kde-look.org gewesen und habe mir mal wieder neue Plasmoids angesehen. Dabei bin ich auf das [Startmenu AppMenu QML](http://kde-look.org/content/show.php/AppMenu+QML?content=146098 "AppMenu QML") gestoßen, dass in QML und Javascript geschrieben ist.

Im Grunde ist es kein Plasmoid, dass an unbedingt haben muss, da es keinen wirklichen Mehrwert bringt. Aber es gefällt mir optisch ganz gut, von daher behalte ich es erst einmal.

Nur hat bzw. hatte das ganze mal wieder einen Haken. Alle Schaltflächen die zum Beispiel für das Abmelden, für das direkte Herunterfahren oder zum Benutzer wechseln gut sind, haben nicht funktioniert. Also musste ich mal wieder Hand anlegen. Unter ~/.kde4/share/apps/plasma/plasmoids/appmenu-qml/contents/ui/ findet man die Datei LeaveToolBar.qml. In dieser findet man folgenden Abschnitt, der für die funktionslosen Schaltflächen zuständig ist.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">function doAction(action) {
    // see http://api.kde.org/4.10-api/kde-workspace-apidocs/libs/kworkspace/html/namespaceKWorkSpace.html
    if (action == "lockScreen")
        plasmoid.runCommand("qdbus", ["org.freedesktop.ScreenSaver", "/ScreenSaver", "Lock"]);
    else if (action == "requestShutDown")
        plasmoid.runCommand("qdbus", ["org.kde.ksmserver", "/KSMServer", "org.kde.KSMServerInterface.logout", "1", "-1", "-1"]); // ShutdownConfirmYes, ShutdownTypeDefault, ShutdownModeDefault
    else if (action == "logOut")
        plasmoid.runCommand("qdbus", ["org.kde.ksmserver", "/KSMServer", "org.kde.KSMServerInterface.logout", "0", "3", "-1"]); // ShutdownConfirmNo, ShutdownTypeLogout, ShutdownModeDefault
    else if (action == "turnOff")
        plasmoid.runCommand("qdbus", ["org.kde.ksmserver", "/KSMServer", "org.kde.KSMServerInterface.logout", "0", "2", "-1"]); // ShutdownConfirmNo, ShutdownTypeHalt, ShutdownModeDefault
    else if (action == "restart")
        plasmoid.runCommand("qdbus", ["org.kde.ksmserver", "/KSMServer", "org.kde.KSMServerInterface.logout", "0", "1", "-1"]); // ShutdownConfirmNo, ShutdownTypeReboot, ShutdownModeDefault
    else if (action == "suspendToRam")
        plasmoid.runCommand("qdbus", ["org.kde.Solid.PowerManagement", "/org/kde/Solid/PowerManagement", "org.kde.Solid.PowerManagement.suspendToRam"]);
    else if (action == "suspendToDisk")
        plasmoid.runCommand("qdbus", ["org.kde.Solid.PowerManagement", "/org/kde/Solid/PowerManagement", "org.kde.Solid.PowerManagement.suspendToDisk"]);
    else if (action == "switchUser")
        plasmoid.runCommand("qdbus", ["org.kde.krunner", "/App", "org.kde.krunner.App.switchUser"]);
}
</code></pre>

Nur was nun? Ich habe mir erst einmal einen der Befehle in der Konsole nachgebaut (qdbus org.kde.ksmserver /KSMServer org.kde.KSMServerInterface.logout -1 -1 -1). Und schon mault die zsh, dass sie Befehl qdbus nicht kennt. Das dürfte das Problem sein. Da ich zufälliger weise wusste, dass der Befehl unter Arch im Paket qt4 enthalten ist, habe ich mir den Paketinhalt unter https://www.archlinux.org/packages/extra/x86_64/qt4/ mal genauer angesehen. Hier wird eine Datei mit dem Namen qdbus-qt4 gelistet. Das dürfte dann wohl die Lösung des Problems sein. Aber wieso nicht qdbus sondern qdbus-qt4? Ein paar Minuten später hatte ich die Antwort. Arch bietet auch das Paket qt5-tools an. Und hier gibt es den Befehl qdbus. Somit wollte man hier wohl Probleme vermeiden, wenn beide Pakete installiert werden würden. Da ich noch nicht qt5 installieren möchte, habe ich mich also dazu entschieden die genannte Konfigurationsdatei anzupassen.

Von daher habe ich die Datei nach qdbus durchsucht und diesen Befehl durch qdbus-qt4 ersetzt, so dass z. B. folgender Eintrag zustande kam.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">plasmoid.runCommand("qdbus-qt4", ["org.kde.ksmserver", "/KSMServer", "org.kde.KSMServerInterface.logout", "1", "-1", "-1"]); // ShutdownConfirmYes, ShutdownTypeDefault, ShutdownModeDefault</code></pre>

Diese Änderungen werden nicht sofort übernommen, sondern vermutlich erst nachdem man sich aus- und wieder eingeloggt hat. Ich habe einfach die Kiste komplett neu gestartet. Und schon kann ich die Schaltflächen die vorher ohne Funktion waren, nutzen.
