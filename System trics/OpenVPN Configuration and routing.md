# OpenVPN Configuration and routing 

## Różnice w plikach konfiguracyjnych
server/server.conf
```.patch
index 42ff3c3..bc1e457 100644
--- a/server/server.conf
+++ b/server/server.conf
@@ -9,23 +9,13 @@ dh dh.pem
 auth SHA512
 tls-crypt tc.key
 topology subnet
-server 11.8.0.0 255.255.255.248
-# push "redirect-gateway def1 bypass-dhcp"
-# PZ now push "redirect-gateway tun1 bypass-dhcp"
+server 10.8.0.0 255.255.255.0
+push "redirect-gateway def1 bypass-dhcp"
 ifconfig-pool-persist ipp.txt
-push "dhcp-option DNS 12.0.0.3"
-push "dhcp-option DNS 1.1.1.1"
-push "dhcp-option DNS 1.0.0.1"
 push "dhcp-option DNS 8.8.8.8"
 push "dhcp-option DNS 8.8.4.4"
-push "topology subnet"
-push "route 10.0.0.0 255.0.0.0"
-# Consider do use push "route 10.4.1.0 255.255.255.0"
-push "route 12.0.0.0 255.0.0.0"
-route 11.8.0.1 255.255.255.255 tun1
-
+push "block-outside-dns"
 keepalive 10 120
-cipher AES-256-CBC
 user nobody
 group nogroup
 persist-key

```

server/client-common.txt
```.patch
index 3d7539d..4575318 100644
--- a/server/client-common.txt
+++ b/server/client-common.txt
@@ -1,14 +1,12 @@
 client
 dev tun
 proto udp
-remote 192.168.68.110 1194
+remote 195.116.75.252 1194
 resolv-retry infinite
 nobind
 persist-key
 persist-tun
 remote-cert-tls server
 auth SHA512
-cipher AES-256-CBC
-# PZ now ignore-unknown-option block-outside-dns
-# PZ now block-outside-dns
+ignore-unknown-option block-outside-dns
 verb 3

```

plik u klienta
```
client
dev tun
# dev tap
proto udp
remote 192.168.68.110 1194
resolv-retry infinite
nobind
persist-key
persist-tun
remote-cert-tls server
auth SHA512
cipher AES-256-CBC
# PZ now ignore-unknown-option block-outside-dns
# PZ now block-outside-dns
verb 3
# PZ now route-nopull
# PZ now route 10.4.1.0 255.255.255.0
<ca>
-----BEGIN CERTIFICATE-----
MIIDQjCCAiqgAwIBAgIUYRCXovK1L4YT6yKRfsK3+Us6qLswDQYJKoZIhvcNAQEL
BQAwEzERMA8GA1UEAwwIQ2hhbmdlTWUwHhcNMjEwOTEzMjAyOTUzWhcNMzEwOTEx
MjAyOTUzWjATMREwDwYDVQQDDAhDaGFuZ2VNZTCCASIwDQYJKoZIhvcNAQEBBQAD
ggEPADCCAQoCggEBANhD99LkcssRbqm5+DWkRbfhajkiaU0GW4H01k5S0V7/G9gR
lejLNtvbZ7Y+5t7+PsSdS0N81+cHHcspAquY0zMv1DcIfORmqWWEElDIYJKxBU9x
qzVhrQ24gs9DOEBJvKG12LciNri1uSEYvlUKLpbDhoaZIZZaxDP6kYHxHKA3uUxL
Fgc0OBXDNvNUexijtbYyckjnDtQ6it3+TAS+6E9wCmw5t4oWG1mzlJ+3NvTyxXvp
IqhyNZ/xxOdtgmm9dyvMxewNItYSSXzUu6lSVeRYKSv6KY7jV8rPDDNtmdWRPF7X
KdLomnakmaRJ+G2FQS4fseNGjsMWaz2Coo1D5AMCAwEAAaOBjTCBijAdBgNVHQ4E
FgQUQJG2LTCA5TzjvH3b3OKVFgymmHAwTgYDVR0jBEcwRYAUQJG2LTCA5TzjvH3b
3OKVFgymmHChF6QVMBMxETAPBgNVBAMMCENoYW5nZU1lghRhEJei8rUvhhPrIpF+
wrf5SzqouzAMBgNVHRMEBTADAQH/MAsGA1UdDwQEAwIBBjANBgkqhkiG9w0BAQsF
AAOCAQEAspUkRiLvNfqssLh+K4eqVZqO4k6QIyz97FULx9nuMBqgoZ5yeQu1bqDI
IeZtkXIaRiuDXMXawO7csCacUzCVkCUxJDlJdnZKKSBOn3QaF1gcLLElJQjtmIKi
LBIKbdBRPGymyB2ZmDYkv9vmx4raqFms6oKr+Zhrhx73bxdeP9OZQ1h9f6RbyVWQ
KPq/CAVikCyUJGDfDkEDSYvWOWa82z/QA4E69kdNgcs5Was6ktircB80hZVM6KAz
6u0aHg6lH6AK+fds5L3tPK+9mdolMUwC7FH7jmKgBoGFNluLPJpJe5vmDBID0FAh
82cKzrGawTeLQzbVGgqbEoo8XToJSA==
-----END CERTIFICATE-----
</ca>
<cert>
-----BEGIN CERTIFICATE-----
MIIDUDCCAjigAwIBAgIRAMLH9ABes6gBII3sLVNOoJMwDQYJKoZIhvcNAQELBQAw
EzERMA8GA1UEAwwIQ2hhbmdlTWUwHhcNMjEwOTEzMjAyOTU0WhcNMzEwOTExMjAy
OTU0WjASMRAwDgYDVQQDDAdkZXZlbG9wMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8A
MIIBCgKCAQEAzJNRvjf7QOnPiHUikXObL7JsVteHVS5D/XvL0fddr3PlyLIelR5L
tJCfC5NkYuI1L1gCX6+skwxZwbSof7hl+l2evUtRcjqIrSabiOtTc5fYxY0tvBJ/
sYb522uZI8Vb8IlZtkYMheM26za482vbRGqUeekOFzNbl+E+/QDwLfoJQRaJsIO4
9j8JEZw2KcJBdZEoVhbFSyE2igKC8nHVb+imvlHg3/3f5VaTs5cPYpHWO/HZTMj2
9NElmr+Oiavv6dqqKYUnYRa81ZDN+1ODbNQKSdwF/4snNzoORUZGLNoOxdPCMn0u
rQVnW4K37IGDrmoPVTKqv94quIL3Fef7YwIDAQABo4GfMIGcMAkGA1UdEwQCMAAw
HQYDVR0OBBYEFD7M1OM2FgHeJFDgvTeEinebJLrXME4GA1UdIwRHMEWAFECRti0w
gOU847x929zilRYMpphwoRekFTATMREwDwYDVQQDDAhDaGFuZ2VNZYIUYRCXovK1
L4YT6yKRfsK3+Us6qLswEwYDVR0lBAwwCgYIKwYBBQUHAwIwCwYDVR0PBAQDAgeA
MA0GCSqGSIb3DQEBCwUAA4IBAQDKuvcCtphyCF5FBpia6BVoo9OWil7K5U/iKgu2
vhKN/v2HgniuzOsXd4vOEc+xeWZaMMQ3V5PamK1OsJ0D0mcJHrLd95YwpkD4gsEo
tPVWDasbq6BtjeFeEdlB15DNK2R36N737ZBhkherQlISXcJ0Zg2EjVp15GBfO9nh
P8ZpMeLyGKK7sgGhAxgiD55Y1sTS/0kZi4WV/Sp4wv7Kju8mkqLwFGbCtETNzLns
YQXEay+piZUhapYwQ83x0kP5fhV3pEQSIrN3NILNcPOGQUCUGYgeOLYJNr7ELvhK
Sf+uZu/1qXr7eE+1+hk+a5lqghOrFD1N3L44+0y01QOK+tB2
-----END CERTIFICATE-----
</cert>
<key>
-----BEGIN PRIVATE KEY-----
MIIEvgIBADANBgkqhkiG9w0BAQEFAASCBKgwggSkAgEAAoIBAQDMk1G+N/tA6c+I
dSKRc5svsmxW14dVLkP9e8vR912vc+XIsh6VHku0kJ8Lk2Ri4jUvWAJfr6yTDFnB
tKh/uGX6XZ69S1FyOoitJpuI61Nzl9jFjS28En+xhvnba5kjxVvwiVm2RgyF4zbr
Nrjza9tEapR56Q4XM1uX4T79APAt+glBFomwg7j2PwkRnDYpwkF1kShWFsVLITaK
AoLycdVv6Ka+UeDf/d/lVpOzlw9ikdY78dlMyPb00SWav46Jq+/p2qophSdhFrzV
kM37U4Ns1ApJ3AX/iyc3Og5FRkYs2g7F08IyfS6tBWdbgrfsgYOuag9VMqq/3iq4
gvcV5/tjAgMBAAECggEAaM7xCitUJiWjlZ2tYCeCUiVvK+6v/wv8+Vj7S08YSFNw
XiojUPJ8hr2xPhT9UUvjQ6YrUSqHl660LXGJAiZO2L4uHX0A9SzX6R3mgXdPAeHB
xTRXQguYMDOevrOZeaIbQFieBaxNriqCcG9QwiV36M1R1EN6XJiLTHyx8J0Sb/rH
UsGp479wGDRH/WwygJNwIMsfsOBn2Ma2IQFKjJGLE1XwnffSaxaKAnAWvWpNuPNr
/BMnMzluV5Dmo7CarKs92o9nk9G1MF0QLlZW8WkVKtNbvJ1f5xSusXkszqHJsQLU
tj6lEisVDcQXxJ4UFrNMBcVQOAZPJnViCsTDu5nfwQKBgQDm+maH1cCqeMvVmcbz
qiQm+3kl33zgjInP0+kSxdz0wvTo+C37m+F98d1vN21LayhTfwm/+MC7/PQUQe+d
omlhM/gk5XHWJDApkgLKeX9ahn6oHWZWx8dMEggxkf+j/+XU1HiUeHKCAW4JSuR3
cUKyzUg4K3iKHXuS5bUr9IwABwKBgQDivLUI0+uW8NIrli1WptqLh/nfueECYSgX
im5BporQ5sS+iYHD8Kk+kONEONDPOdP41HUoWHrkCphWyUtox/wmHoOImJslywEL
GFHkdkzhsAsKVvck94/3KBAFwIXSpWLzi5beTcXQ5TlE/XtbWB3L3p8E/cKcuYdu
SLfYqyraxQKBgHUngsPZFm0g8fp4kiHbJZUkLhGYpsVaYzgnuutLssPu8rwLzX72
VMxF1lPn4CbFxmF7aR2W9WMkbUStIPVqgFrOOkm0myXLmyYqqgG62G65ExsANn1D
vYGHD+Lcs7aiQBfQYQylfycTxJUwCGvQ5cy9NKlQ20XqqFgc7OTLmAsXAoGBAK3y
I9i/7A+CdVqm/eVqYGOHT/WJfsv6iW118BxBjmGxiOK8T2do7A5pzVD7XYZ9UNem
9rKbHrxwPGroRwf91L3RzwsuOGiIEybV442oDFdgXTfze+tKWZI9k/01s/TkmMNL
JdUqSUZ3dLYu2UI8ma9b/RcxLupZk0LSWujIeDoZAoGBAJtYo5d1HbxS1V6i85Tv
1RFFD8t1c7gTKcjy9OQLCEB1hcWJUOM8bBmZW964bFJ6SDO8igjzTlJC6BBy5z7V
kz16AOpHZ8sq/iTdC5Zyqu9OojlVDlA2DBgfTv2tg+wJaT/t160Gj3bBRqsjrGC3
XiQcWWKsAuhFMZ4w0z/qgUul
-----END PRIVATE KEY-----
</key>
<tls-crypt>
-----BEGIN OpenVPN Static key V1-----
01be5f56c3917ab3ebfe5297db02d207
8a7e1d1a6314b9679d6db8b6c132a206
adf6e6e9b1cbafc27a4bfcbac4365e34
38ca2bcdc41df75f41a2ddb1c09f7822
6926fc273e6f7c309cc43911d6c7fd0f
d3fc20e0daafd7c7d9897c4036aceb40
1ef4605226e63197f75d502cb96c684d
15699025fdbf97b56905b5076cebb364
917c54e66df5420a19b46e666ed8b645
9c801ff78f70f795ee6a329aa70f31dd
7dc7158c14753db2b821c76b9ce10a96
2410e5955cec61658c6aedef7760807b
2a171588bb0a0cab0fbbe8b1ced6dbaa
a810e81d7680cde4f48ca92a3de02148
32ae8f553b459d9c684c989d5067fad9
e2c3915caafd2a390b06086c4e8575ba
-----END OpenVPN Static key V1-----
</tls-crypt>
```

## Ostatnio

Wydaje się, że nic nie zmieniłem i zadziałało
Jak chcę przekierować ruch z maszyny mojej na tą z którą ona jest połączona to dodałem do konfiguracji
`route 192.168.10.0 255.255.255.0 tun1`
Powyższe nie jest chyba potrzebne, skasowałem i działa

Po stronie klienta dopisałem 
`route-nopull`
`route 10.4.1.0 255.255.255.0`'

Debugowanie, zobacz jaki interfejs sieciowy jest używany do połączenia we wskazany adres [Find interface for tracerout route to specific host](:/c6d040315a844dfba1aac9370419563a)

No i masquarade oczywiście

## OpenVPN client

Umieścić pliki konfiguracyjne w `/etc/openvpn/client`
Tak aby w tym katalogu był główny `conf`/ `ovpn`  klucze w podfoldeze i ścieżki do `pem` i spółki absolutne i `askpass`. Wówczas wystarczy `systemctl start openvpn-client@MyVpn`
[źródło](https://askubuntu.com/questions/1048429/what-is-the-purpose-of-openvpns-etc-openvpn-client-server-directories)

The file /etc/openvpn/jdoe.pass just contains the password. You can
chmod this file to 600. This method save my life... ;-)
[source](https://stackoverflow.com/questions/11240184/pass-private-key-password-to-openvpn-command-directly-in-ubuntu-10-10)

Zmienić w plikach konfiguracyjnych `dev tun` na np.: `tun_gunb`

# Przekazywanie połączeń, przez VPN
Wystarczy tylko to
`sudo iptables -t nat -A POSTROUTING -o tun_gunb -j MASQUERADE`

Doszedłem do tego, że napewnoo MASQUERADE robi się na wyjściu czyli w obecnym przypadku na VPN GUNB czyli tun_gunb
 `sudo iptables -t nat -A POSTROUTING -o tun_gunb -j MASQUERADE`
 Przetestwoałem to robiąc na świeżym systemi (po restarcie) naprzemiennie `-A` i `-D` z opcją pierwszą działa, a z drugą nie, zgodnie z oczekiwaniem

# Automatyczne uruchamiania MASQUERADE
`/etc/systemd/system/openvpn-iptables.service`
```
ExecStart=/usr/sbin/iptables -t nat -A POSTROUTING -o tun_pzdevel -j MASQUERADE
ExecStop=/usr/sbin/iptables -t nat -D POSTROUTING -o tun_pzdevel -j MASQUERADE
```
Te wpisy są jako pierwsza, nadal coś nie działa automatycznie
procedura jest taka
```
sudo service openvpn-client@gunb start
sudo service openvpn-iptables stop
sudo service openvpn-iptables start
```
restart nie działa

# Pytanie o klucz

Niby startuje, ale później wyrzuca błąd
```
Broadcast message from root@pzdevel (Mon 2023-12-11 22:33:16 UTC):

Password entry required for 'Enter Private Key Password:' (PID 549267).
Please enter password with the systemd-tty-ask-password-agent tool.
```

Być może (dopiero wprowadziłem i nie znam rezultatu)
`sudoedit /etc/ssl/openssl.cnf`

```
[provider_sect]
default = default_sect
legacy = legacy_sect     # Add this.

# The fips section name should match the section name inside the
# included fipsmodule.cnf.
# fips = fips_sect

# If no providers are activated explicitly, the default one is activated implicitly.
# See man 7 OSSL_PROVIDER-default for more details.
#
# If you add a section explicitly activating any other provider(s), you most
# probably need to explicitly activate the default provider, otherwise it
# becomes unavailable in openssl.  As a consequence applications depending on
# OpenSSL may not work correctly which could lead to significant system
# problems including inability to remotely access the system.
[default_sect]
# activate = 1    # Enable this.
activate = 1

[legacy_sect]     # Add these.
activate = 1
```

# Dodanie na innym linuksie routingu na komputer dostępny przez VPN
`sudo ip route add 192.168.10.0/24 via 192.168.100.11`
Gdzie `192.168.10.0` to maszyna dostępna poprzez zewnętrzny VPN, a `192.168.68.112` to komputer, na którym jest zestawiony klliencki VPN.

# GUNB
```
sudo ip route replace 192.168.10.0/24 via 192.168.8.137
sudo ip route replace 192.168.200.0/24 via 192.168.8.137
sudo ip route replace 20.215.0.0/16 via 192.168.8.137
sudo ip route replace 20.50.0.0/16 via 192.168.8.137
sudo ip route replace 13.69.0.0/16 via 192.168.8.137
sudo ip route replace 74.248.0.0/16 via 192.168.8.137
````