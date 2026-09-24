# Restart docker and openvpn

Listowanie serwisów
`sudo systemctl list-units --type=service`

Wyłączenie
```
sudo service snap.docker.dockerd stop
sudo service openvpn-iptables stop
sudo service openvpn-server@server stop
service openvpn stop
```

Start
```
sudo service snap.docker.dockerd start
sudo service openvpn-iptables start
sudo service openvpn-server@server start
sudo service openvpn start
```