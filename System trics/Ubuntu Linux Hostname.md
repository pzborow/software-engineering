# Ubuntu Linux Hostname

Odczyt
`hostname`

Zapis
`sudo hostnamectl set-hostname NEW_NAME`

Weryfikacja
`hostnamectl`

Propagacja
Zainstalować avahi-discovery
`sudo apt-get install avahi-discover`
Reszta powinna zadziać się automatycznie

Problemem z może być propagacja IPv6 zamiast IPv4. Długo się przez to łączy OpenVPN
Pomogło ustawienia `/etc/avahi/avahi-daemon.conf`
```
#publish-aaaa-on-ipv4=yes
#publish-a-on-ipv6=no

#ByPZ
publish-aaaa-on-ipv4=no
publish-a-on-ipv6=no
`````