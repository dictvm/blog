---
layout: post
title: Moderner Quake3-Server unter CentOS 7
date: '2014-08-26 13:32:40'
---

Wie [bereits](https://blog.dictvm.org/quake-iii-arena-eine-ode-an-cpma-clan-arena/) erwähnt, bin ich in punkto Quake 3 wieder auf den Geschmack gekommen. Nun, da einige aus dem Hackerspace gelegentlich ebenfalls Spaß am Beben entdeckt haben, wird es wohl etwas länger dauern, bis ich wieder die Lust verliere. Insofern dachte ich mir, kann ich auch gleich mal einen eigenen Server aufsetzen - und das dann gleich richtig. Das heisst: Kein `screen`-Gefrickel, kein "ach, packen wir's in `tmux` und gut ist". Zudem ist die ganze Dokumentation für den Betrieb von Quake 3-Servern im Netz hoffnungslos veraltetet. Und es war ohnehin an der Zeit mal eine eigene systemd-Unit zu stricken. Also los. 

Ich habe seit irgendeiner "du kriegst 40% Rabatt wenn du jetzt zuschlägst"-Aktion eine 512MB-Kiste bei [ramnode](http://ramnode.com/), die ich monatlich bezahle. Als Distribution verwende ich CentOS 7. Die Schritte dürften sich sich bei einer Debian-basierten Distribution aber nicht großartig unterscheiden. 

Wir brauchen erstmal zwei Dateien von ioquake.org: Den Installer für ioquake und den Installer der das letzte Pointrelease sowie die Spieldaten - wobei wir letzteres schlichtweg manuell erledigen: 

```
wget http://ioquake3.org/files/1.36/installer/ioquake3-1.36-7.1.x86_64.run  
sh ioquake3-1.36-7.1.x86_64.run  
wget http://ioquake3.org/files/1.36/data/ioquake3-q3a-1.32-9.run  
sh ioquake3-q3a-1.32-9.run
```

Beides führt uns jeweils durch einen ncurses-Installer. Der eine fragt nach einem Installations-Pfad für die ioquake3-Binaries, der andere will für uns die Installation der Spieldaten von einem optischen Medium erleichtern. In erstem Falle habe ich schlichtweg den Default übernommen und die Dateien in `/usr/local/bin/ioquake/` schreiben lassen. Die Spieldaten sind dann nach `/usr/local/games/ioquake3` installiert worden. Da wir aber kein optisches Medium haben, wählen wir einfach alles ab, was danach klingt, als wollten wir von CD nachinstallieren. Diesen Schritt holen wir nämlich sofort manuell nach. 

Nun soll der Rest aber nicht mehr systemweit installiert werden. Also legen wir zuerst einen neuen User an, in dessen Kontext später auch der dedizierte Server laufen soll: 
```
adduser q3a  
su - q3a  
mkdir -p .q3a/baseq3  
```
Die [pak0.pk3](http://files.anitalink.com/gamecache/quake3/baseq3/pak0.pk3) mit den proprietären Inhalten (Sounds, Texturen, Models, etc) kippen wir in /home/q3a/.q3a/baseq3: 

`mv pak0.pk3 /home/q3a/.q3a/baseq3`

Damit wir nicht nur langweiliges Vanilla-Quake spielen können, besorgen wir uns noch Challenge Promode Arena (CPMA): 
```
wget http://playmorepromode.org/CPMA148.zip
unzip CPMA148.zip
mv cpma /home/q3a/.q3a/
```

Im weiteren brauchen wir auch noch eine einfache Server-Konfiguration. In meinem Fall erlaube ich explizit das Voting~~, damit ich jederzeit Clan Arena spielen kann, ohne es vorher konfigurieren zu müssen~~. ~~(Ich weiß nämlich noch nicht, wie das geht.)~~

```
cat <<__EOF__ >> /home/q3a/.q3a/baseq/server.cfg
seta rconpassword ""
seta g_allowvote 1
seta sv_maxRate 10000
seta g_gametype 0
seta fraglimit 30
seta timelimit 25
seta sv_maxclients 8
seta sv_hostname "dictvm's CPMA server"
seta g_motd "don't fuck around, behave, play fair."
seta sv_maxPing "500"
seta g_slowmoDuelEnd 1
seta mode ca
seta selfdamage off
seta teamdamage off
seta limit 10
 __EOF__
```

Nun erstellen wir noch unsere systemd-Unit: 
```
cat <<__EOF__ >> [Unit]
Description=This service spawns a ioquake3 dedicated server with sane defaults
# However, these defaults may not apply to all use cases.

[Service]
User=q3a
ExecStart=/usr/local/games/ioquake3/ioq3ded.x86_64 +set net_port 27960 +set fs_game cpma +set dedicated 2 +set sv_pure 1 +set com_hunkmegs 128 +exec server.cfg
Restart=on-abort
# there are several options to tweak the server's performance:
# net_port defines the UDP-port used for connections to the server
# fs_game should be the mod you want to play. Not necessary for vanilla-q3/FFA
# dedicated 0 and 1 are LAN, 1 is Internet
# sv_pure 1 prevents clients from using their own pk3-files
# com_hunkmegs defaults to 56, should be 128/192/256 on a modern system(?)
# rate 25000 defines the rate in which client & server communicate
# snaps 40 defines gamestate-snapshots client & server exchange in secs# cl_maxpackets 125 max amount of FPS being counted on the server-side

[Install]
WantedBy=multi-user.target
 __EOF__
```

Veranlassen wir systemd dazu, seine Unit-Files neu einzulesen und aktivieren unsere q3a-Unit per Symlink:
```
systemctl daemon-reload
systemctl enable q3a  
```

Nun muss der Port noch geöffnet werden, per default sind ausser SSH nämlich sämtliche Ports geschlossen. Das geht ganz trivial, dank firewalld:

`firewall-cmd --zone=public --add-port=27960/udp`

Meinen Server erreicht ihr unter ramnode.dictvm.org:27960

__Update__: Habe das Unit-File mit Kommentaren für relevante Server-Parameter versehen.

__Update #2__: Habe die server.cfg noch etwas angepasst. Nun läuft auch CPMA Clan Arena per default. 