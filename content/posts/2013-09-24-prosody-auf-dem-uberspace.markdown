---
layout: post
title: Prosody auf dem Uberspace
date: '2013-09-24 12:56:34'
---

**Hinweis:** Diese Anleitung wird in absehbarer Zeit durch eine Ansible-Role ersetzt und ich erkläre sie hiermit **für überholt**. Wenn ihr lieber händisch Prosody aufsetzen wollt und Wert auf vernünftige Crypto legt, seid ihr bei der Anleitung vom [cosmofox](https://how.cosmofox.net/prosody-auf-Uberspace/) besser aufgehoben. Dort steht unter anderem, wie ihr lua mit einem aktuellen OpenSSL verdrahtet.

[Prosody](http://prosody.im) ist ein freier, in der Programmiersprache Lua geschriebener XMPP-Server. [XMPP](http://en.wikipedia.org/wiki/XMPP) ist auch unter dem etwas zungenkompatibleren Namen Jabber bekannt und wird vornehmlich verwendet um eigene Chat-Server zu betreiben, etwa als freie und unabhängige Alternative zu alten Instant Messaging-Hengsten; etwa wie ICQ oder dem sich erst kürzlich von XMPP abgeschotteten Google Talk. Bei Prosody handelt es sich um eine von vielen freien Implementierungen dieses Protokolls, allerdings geht prosody dabei sehr schonend mit den System-Ressourcen um und eigent sich daher besonders für den Shared Hosting-Einsatz bei Uberspace.

Im folgenden wird beschrieben wie sich Prosody auf einem [Uberspace](https://uberspace.de) einrichten lässt.

## Installation

Zuerst übergeben wir toast den Pfad zum aktuellsten prosody-Tarball.

    dictvm@lynx ~ % toast arm https://prosody.im/downloads/source/prosody-0.9.3.tar.gz
    

## Konfiguration:

prosody soll seine Daten möglichst in einem Verzeichnis anlegen, das nicht unter
`~.toast` liegt, damit sie niemals durch toast überschrieben werden können. Ergo: 

    mkdir -p ~/var/prosody/data

Der folgende Block ist die prosody-Konfigurationsdatei. Meine sieht wie folgt aus. Der ganze Block lässt sich einfach durch Copy/Paste mit korrekter Formatierung übertragen. Mit "**FIXME**" oder "**jabber.fix.me**" Kommentierte Zeilen müssen nachträglich angepasst werden - das lässt sich nicht trivial automatisieren. Die Pfade hingegen werden beim Ausführen direkt korrekt in die Datei geschrieben. Ausserdem betreibst du einen eigenen, im Internet erreichbaren Dienst. Wenn du nicht ganz genau weißt was du hier tust, dann solltest du die Absicht ohnehin nochmal überdenken.

```
cat <<__EOF__ > /home/$USER/var/prosody/data/prosody.cfg.lua
    admins = { "me@jabber.fix.me" }
    modules_enabled = {
                "roster";
                "saslauth";
                "tls";
                "dialback";
                "disco";
                "private";
                "vcard";
                "privacy";
                "version";
                "uptime";
                "time";
                "ping";
                "posix";
                "pep";
                "register";
                "admin_adhoc";
                "motd";
                "welcome";
};
daemonize = false; -- IMPORTANT for daemontools! DO NOT EDIT!
data_path = "/home/$USER/var/prosody/data";
log = { "*console" } -- IMPORTANT for daemontools! DO NOT EDIT!
allow_registration = false;
s2s_ports = { FIXME } -- freien Port suchen & eintragen!
c2s_ports = { FIXME } -- freien Port (+1) suchen & eintragen!
c2s_require_encryption = true
s2s_require_encryption = true
authentication = "internal_hashed" -- do not save passphrases in cleartext!

VirtualHost "jabber.fix.me" -- anpassen!
        enabled = true

ssl = {
        key = "/home/$USER/.ssl/wildcard.fix.me.key"; -- FIXME
        certificate = "/home/$USER/.ssl/wildcard.fix.me.crt"; -- FIXME
        ciphers = "kEDH:AESGCM:HIGH:MEDIUM:TLSv1:!RC4:!RC2:!3DES:!DES:!MD5:!DSS:!aNULL:!eNULL"; -- FUCK THE SCHLAPPHUETE!
        options = { "no_ticket", "no_compression", "no_sslv2", "no_sslv3" }
}
__EOF__
```

Die config erzwingt sichere TLS-Cipher, loggt verbose nach `~/service/prosody/log/main/current` und speichert keine Passwörter im Klartext. Vorhandene Passwörter werden ausserdem gehashsalzen und ersetzt.  Vielen Dank an [@marudor](https://twitter.com/marudor) und [Christopher](https://jonaspasche.com/app/about_us/ch) für Hinweise und Ergänzungen. Nun brauchen müssen wir noch einen automatisch erstellten Symlink löschen und ihn ersetzen: 

	rm /home/$USER/.toast/armed/etc/prosody/prosody.cfg.lua
    ln -s /home/$USER/var/prosody/data/prosody.cfg.lua /home/$USER/.toast/armed/etc/prosody/prosody.cfg.lua

Bei den C2S-/S2S-Ports ist zu beachten, dass die Ports noch von den Kollegen bei hallo@uberspace.de freigegeben werden müssen. Da reicht eine formlose ~~~nette~~~ Mail.

Nun richten wir prosody noch als Service mit den [daemontools](https://uberspace.de/dokuwiki/system:daemontools) ein:

    uberspace-setup-service prosody ~/.toast/armed/bin/prosody
    
Wir haben prosody nun zum Dienst gemacht. Wenn prosody also einmal abstürzt wird er automatisch neugestartet. Muss der Uberspace-Host z.B. wegen eines wichtigen Kernel-Updates neugestartet werden, so kommt prosody automatisch wieder hoch.

Steuern lässt sich prosody nun mit diesen simplen Befehlen:

	svc -d ~/service/prosody
    svc -u ~/service/prosody
    svc -du ~/service/prosody
    
Ersterer beendet prosody, zweiterer startet ihn, letzteres startet eine laufende Instanz neu. Das wird beim Einrichten des Services aber auch nochmal im Detail erklärt. Generell empfiehlt sie die [Lektüre zu daemontools](https://uberspace.de/dokuwiki/system:daemontools) im Uberspace-Wiki.

Wer auf Log-Ausgaben steht, der hängt praktischerweise einfach ein 
`| tail -F ~/service/prosody/log/main/current` an obige Befehle.

## Account(s) erstellen

Als nächstes muss ein Account erstellt werden: 

    prosodyctl adduser me@jabber.fix.me
    
Wer aufgepasst hat sieht direkt, dass wir damit direkt auch unseren **Admin-Account** erstellt haben. Wer nicht aufgepasst hat, der wirft am besten nochmal einen Blick auf die erste Zeile der _prosody.cfg.lua_.

## Prosody upgraden

Vor einem prosody-Upgrade ist dringend anzuraten, den Service zu stoppen: 

    svc -d ~/service/prosody | tail -F ~/service/prosody/log/main/current

Da toast prosody nicht mehr findet, empfiehlt es sich, den [Release-Feed auf prosody.im](https://prosody.im/doc/release) zu abonnieren, um bei neuen Versionen mittels  `toast arm https://prosody.im/downloads/source/prosody-{$VERSION}.tar.gz` ein Update anzustoßen. Aber Obacht: Der Symlink `/home/$USER/.toast/armed/etc/prosody/prosody.cfg.lua` zeigt auf `/home/$USER/.toast/pkg/prosody/{$VERSION}/1/root/etc/prosody/prosody.cfg.lua` und wird beim Upgrade ohne Rücksicht auf Verluste überschrieben! 

Da die Syntax der Konfigurationsdatei aber sehr stabil ist, sollten an der eigentlichen Konfiguration keine Änderungen nötig sein. Den Symlink müssen wir hingegen händisch anpassen. Am besten nehmen wir uns dazu die letzte uns als funktionierend bekannte `prosody.cfg.lua` und kopieren sie nach `/home/$USER/var/prosody/data`. Nun haben wir unsere Konfiguration in eine Verzeichnis liegen, das durch toast nicht modifiziert wird. Den von toast bei der Installation der neuen Prosody-Version eingerichteten Symlink löschen wir nun: 

	rm /home/$USER/.toast/armed/etc/prosody/prosody.cfg.lua
    
Und erstellen ihn neu: 

	ln -s /home/$USER/var/prosody/data/prosody.cfg.lua /home/$USER/.toast/armed/etc/prosody/prosody.cfg.lua

Wenn der Kompiliervorgang keine Fehler geworfen hat, können wir Prosody nun neustarten und sollten uns aus direkt wieder damit verbinden können: 

    svc -u ~/service/prosody | tail -F ~/service/prosody/log/main/current
    
## DNS: SRV-Records

Der Jabber-Server muss der Aussenwelt irgendwie noch mitteilen, über welche Ports er die CS2- und S2S-Kommunikation abwickeln kann. Im DNS braucht es also noch 3 SRV-Records:

	_jabber._tcp.jabber.fix.me. in SRV 0 0 $S2SPORT jabber.fix.me.
	_xmpp-client._tcp.jabber.fix.me. in SRV 0 0 $C2SPORT jabber.fix.me.
	_xmpp-server._tcp.jabber.fix.me. in SRV  0 0 $S2SPORT jabber.fix.me.