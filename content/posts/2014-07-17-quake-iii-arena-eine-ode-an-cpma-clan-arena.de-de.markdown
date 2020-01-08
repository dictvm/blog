---
layout: post
title: 'Quake III Arena: Eine Ode an CPMA & Clan Arena'
date: '2014-07-17 02:45:08'
---

Ich liebe Quake III Arena. Seit ich das Spiel am Tag des Erscheinens irgendwann im Jahr 1999 in Form eines frisch gebrannten CD-R-Rohlings in der Hand hielt hat es mich gepackt. Irgendwann ging ich allerdings mit Unreal Tournament fremd, weil mir die Spielphysik und das Movement eher zusagten. Erst als ich dann auf einer LAN-Party auf die Promode-Mod CPMA (Challenge ProMode Arena) gestoßen wurde, hat mich Quake III wieder gepackt.

![Quake III Arena Screenshot](/content/images/2014/Jul/IMG_20140717_031518.jpg)

Seit dem passiert es mindestens einmal im Jahr, dass mich die Lust packt, mal wieder einen gewissen Level in UT, UT2004 und Quake III zu erreichen. Insbesondere Quake III schafft mich aber jedes Mal wieder, weil man dem Spiel und dessen Konfiguration so langsam das Alter anmerkt. Ich spiele zur Zeit auf einem Retina Macbook Pro 13” und ich brauchte durchaus einige Zeit, bis ich mir die nötigen Konfigurationszeilen herausgesucht habe. Also halte ich die nun hier einfach mal fest, damit ich nicht jedes Mal von neuem suchen muss: 

* [ioquake3](http://ioquake3.org/) ist die freie Implementierung von Quake III, es fehlen allerdings sämtliche Spielinhalte. Es wird also die [pak0.pk3 des Originalspiels](magnet:?xt=urn:btih:bd0912637dfa533263f9c30918ba6a7d7ef09d72&dn=Quake+3+Arena+pak0.pk3+file&tr=udp%3A%2F%2Ftracker.openbittorrent.com%3A80&tr=udp%3A%2F%2Ftracker.publicbt.com%3A80&tr=udp%3A%2F%2Ftracker.istole.it%3A6969&tr=udp%3A%2F%2Fopen.demonii.com%3A1337) benötigt.
* CPMA gibt es bei [playmorepromode](https://playmorepromode.org)

Quake III stammt noch aus einer Zeit, in der Displays primär eine Aspect Ratio von 4:3 hatten. Heutzutage dürfte 16:10 die größte Verbreitung haben, gefolgt von 16:9. Für ein Retina Macbook Pro überschreiben wir die AR wie folgt und setzen gleich die passende Auflösung, indem wir folgende Zeilen in der q3config.cfg editieren:

`r_mode -1`  
`r_customwidth 1440`  
`r_customheight 900`

Soweit ich erkennen kann, scheint Quake III in dieser Auflösung tatsächlich die maximale Auflösung des Displays zu verwenden, obwohl nicht die native Auflösung angegeben wird. In der nativen Auflösung habe das Spiel leider nicht starten können. Es sieht jedenfalls dem Alter entsprechend ganz passabel aus. Die Auflösung müsstet ihr dann ggfs. eurem Display entsprechend anpassen. 

Es gibt noch ein weiteres Goodie, nämlich neue hochaufgelöste Texturen. Einfach [herunterladen](http://ioquake3.org/files/xcsv_hires.zip), entpacken und die Datei `xcsv_bq3hi-res.pk3` im baseq3-Verzeichnis der Quake-Installation hinterlegen.

![Quake III Arena on 13inch MBP Retina](/content/images/2014/Jul/IMG_20140717_031527.jpg)

CPMA: Wer CPMA Clan Arena spielen möchte, steht erstmal vor dem Problem, dass keine Maps gefunden werden. Um Clan Arena zu spielen, muss nämlich erst einmal der Game-Mode umstellt werden - nachdem man bereits ein Spiel in z.B. dem Tournament-Modus gestartet hat. Dort löst man dann einen Callvote für Clan Arena aus: 

`/cv game ca`

Ärgerlich ist, dass standardmäßig der Selfdamage für die Panzerung aktiv ist. Den Selfdamage deaktivieren wir dann also auch mittels Callvote: 

`/cv selfdamage off`

Das sollte erstmal reichen um sich wieder warm zu spielen.