---
title: Piwik wurde kompromittiert
date: 2012-11-27T11:04:00+0100
categories:
- OSBN
- Allgemein 
tags:
- Piwik
- Kompromittierung
- Backdoor
slug: piwik-wurde-kompromittiert
---
Die aktuellen Downloadpakete der Webanalyse-Software Piwik wurden kompromittiert. So wie es aussieht gelang es Dritten die Pakete zu ändern und ein Backdoor zu installieren. Geändert wurde die Datei /piwik/core/Loader.php. Hier wurde Base64-codierte Befehle eingebaut (eval(gzuncompress(base64_decode(...), die Daten an prostoivse.com übertragen. Weiterhin legen die Befehle scheinbar die Datei lic.log und piwik/core/DataTable/Filter/Megre.php an. Darüber hinaus ist es Dritten möglich per PHP weitere Befehle abzusetzen und somit das jeweilige System noch weiter zu kompromittieren. Betroffen ist scheinbar die aktuelle Version 1.9.2.

Nutzern von Piwik würde ich dringend dazu raten, ihre Installation zu prüfen und ggf. Maßnahmen zu ergreifen. Genauere Informationen kann man unter [http://forum.piwik.org/read.php?2,97666](http://forum.piwik.org/read.php?2,97666 "Piwik Forum") nachlesen.

**Nachtrag:** Laut dem genannten Foren-Thread sieht es wohl so aus, als ob Nutzer, die Piwik schon vor einigen Tagen auf Version 1.9.2 aktualisiert haben, nicht betroffen sind. Hoffen wir mal, dass das stimmt. Auch scheint wohl "nur" der Download und nicht auch noch das Repository betroffen zu sein. Zwischenzeitlich gibt es [hier](http://piwik.org/blog/2012/11/security-report-piwik-org-webserver-hacked-for-a-few-hours-on-2012-nov-26th "Stellungnahme Piwik") eine Stellungnahme der Betreiber zu dem Ereignis.