---
layout: post
title: Höhere skalierte Retina-Auflösung unter Mac OS X
date: '2015-05-25 00:29:00'
---

Seit Apple seine HiDPI-Retina-Displays verkauft, kommt Mac OS X mit einer netten Funktion daher, um durch geringe Einbussen in der Bildqualität mehr Platz auf dem Display zu haben. Dadurch wird schlichtweg eine Auflösung jenseits der nativen Display-Auflösung "off-screen" dargestellt, um sie dann wiederum auf dem tatsächlichen Display herunter zu skalieren. Das geht zu Lasten der Bildqualität, aber auch der Grafik-Leistung, da jede Textur die das User Interface benötigt, in einer höheren Auflösung vorgehalten werden muss.

Der Vorteil ist, dass auf dem Display eines 13" Macbook Pro mit einer Retina-Auflösung von 1280x800 (nativ: 2560x1600) skalierte Auflösungen von 1440x900 (off-screen: 2880x1800) bzw. 1680x1080 (off-screen: 3360x2160) einstellbar sind. Beim 15" Macbook Pro gesellt sich noch 1920x1200 (off-screen: 3840x2400) hinzu. Mac OS X stellt das wie folgt dar:

![](/content/images/2015/05/Screen-Shot-2015-05-25-at-17-02-39.png)

Auf meinem 15" Macbook Pro bin ich mit der höchsten Skalierungsstufe recht zu frieden, auf dem 13" erscheinen mir UI-Elemente auf der höchsten Stufe (die, wie wir eben gelernt haben, bei 1680x1080 liegt) aber noch etwas zu groß. Mein Early Adopter Late 2012er-Modell performt aufgrund der Intel HD4000 ohnehin nicht mehr so so gut. Also dachte ich mir: Irgendwie wird man OS X ja wohl noch 3840x2400 als Auflösung unterjubeln können, die dann auf 1920x1200 skaliert wird.

Ich sollte Recht behalten und bin auf das Tool [SwitchResX](http://www.madrau.com/srx_download/download.html) gestoßen. Das ist zwar Shareware, wir brauchen es aber ohnehin nur einmal und für 10 Tage steht uns der volle Funktionsumfang zur Verfügung. Nach der Installation der [Preference Pane](http://en.wikipedia.org/wiki/Preference_Pane) (es reicht, es als User nach _~/Library_ zu installieren, wenn danach gefragt wird) tragen wir noch unsere Wunsch-Auflösung nach. Das soll im Falle des 13" Macbook Pro also **3840x2400** sein:

![](/content/images/2015/05/Screen-Shot-2015-05-25-at-17-11-57.png)

Daraufhin braucht es einen Reboot. OS X verbirgt allerdings die Auflösung weiterhin vor uns, schließlich gibt es keine weitere Option in den Display-Settings. Wir brauchen dafür ein weiteres Tool, nämlich [Retina DisplayMenu](https://static.horrendum.de/RDM.zip) von [phoenixdev](https://twitter.com/phoenixdev). RDM nutzt laut des Disassemblers keine auffälligen APIs die auf Funktionen jenseits der versprochenen Änderung der Display-Auflösung hindeuten. Nach dem Start wählen wir im Menü nun **1920 x 1200 (HiDPI)** aus und schon läuft der Desktop in der gewünschten skalierten HiDPI-Auflösung:

![](/content/images/2015/05/Screen-Shot-2015-05-25-at-17-21-09.png)

Ich habe bisher keine Nachteile feststellen können. Die Performance hat sich nicht spürbar verschlechtert und auch Schriften sehen weiterhin nicht ausgefranst aus. Dafür habe ich nun deutlich mehr Platz auf dem Display. Ich werde nun im Auge behalten, wie sich die neue Auflösung auf die ohnehin eher knappe Akkulaufzeit auswirkt.