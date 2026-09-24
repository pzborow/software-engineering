# Find interface for tracerout route to specific host

Dla Ubuntu
`ip route get 192.168.10.50`
[źródło](https://serverfault.com/questions/531751/find-interface-for-route-to-specific-host)

Dla Windows
`Find-NetRoute -RemoteIPAddress "192.168.10.50" | Select-Object ifIndex,InterfaceAlias,DestinationPrefix,NextHop,RouteMetric -Last 1`
[źródło](https://superuser.com/questions/346347/on-windows-how-to-determine-route-for-ip-destination)