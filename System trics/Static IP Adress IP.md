# Static IP Adress IP

Niby zadziałało, były błędy, zrezygnowałem z tego rozwiązania po znalezieniu możliwości rezerwacji IP  na routerze
Utworzyć nowy plik
`sudo vim /etc/netplan/01-netcfg.yaml`

```
# This file describes the network interfaces available on your system
# For more information, see netplan(5).
network:
  version: 2
  renderer: networkd
  ethernets:
    eth0:
      dhcp4: no
      # Ser IP address & subnet mask
      addresses: [10.10.1.5/24]
      # Set default gateway
      gateway4: 10.10.1.1
      nameservers:
        # Set DNS name servers
        addresses: [10.10.1.1,8.8.8.8]
      dhcp6: no
```

Zmienić w nim nazwę eth0 na właściwą

Aplikacja zmian
`sudo netplan apply`
[source](https://computingforgeeks.com/how-to-configure-static-ip-address-on-ubuntu/?utm_content=cmp-true)
