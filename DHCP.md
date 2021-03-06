# 1	DHCP
| Command | Description |
| - | - |
| (config)# ***ip dhcp excluded-address {First_IP} {Last_IP}*** | Exclude assigned IPs |
| (config)# ***ip dhcp pool {pool_name}*** | Create a new pool with a name |
| (dhcp-config)# ***network {network_IP} {mask}*** | Subnet to alocate IPs from |
| (dhcp-config)# ***default-router {default_GW_IP}*** | Default GW IP assigned to devices |
| (dhcp-config)# ***dns-server {DNS_IP}*** | DNS server IP assigned to devices |
|  (dhcp-config)# ***lease {days} {hours} {minutes}*** | Defines lease time |


**Example**
```
R1(config)#ip dhcp excluded-address 192.168.0.1 192.168.0.50  
R1(config)#ip dhcp pool Floor1DHCP  
R1(dhcp-config)#network 192.168.0.0 255.255.255.0  
R1(dhcp-config)#default-router 192.168.0.1  
R1(dhcp-config)#dns-server 192.168.0.1
```


# 1.1	DHCP helper
- Used when I want to use a "remote" DHCP server

**Situation**
- I have 2 PCs connected to the R1 router
- There's an "external" DHCP server connected to the R1 router
- I want to use the "external" DHCP server for those 2 PCs, I don't wanna configure DHCP on R1

```
R1(config)# interface <interface_connected_to_client_1>
R1(config-if)# ip helper-address <DHCP_server_IP>
R1(config-if)# exit
R1(config)# interface <interface_connected_to_client_2>
R1(config-if)# ip helper-address <DHCP_server_IP>
```


# 2	DHCP Troubleshooting
| Command | Description |
| - | - |
| # ***show ip dhcp binding*** | Currently leased IP addresses |
| # ***show ip dhcp pool*** | Configured DHCP pools |
