# 1	Static NAT
**Specify the interfaces**
```
Gateway(config)# interface <inside_interface>
Gateway(config-if)# ip nat inside
Gateway(config-if)# interface <outside_interface>
Gateway(config-if)# ip nat outside
```

**Configure static mapping**
```
Gateway(config)# ip nat inside source static <private_IP>/<inside_IP> <public_IP>/<outside_IP>
```

## 1.1	Static PAT - Port Forwarding
```
Gateway(config)#ip nat inside source static tcp <inside_IP> <inside_port> <outside_IP> <outside_port>
```

# 2	Dynamic NAT - PAT
```
Gateway(config)# interface <inside_interface>
Gateway(config-if)# ip address <IP> <MASK>
Gateway(config-if)# ip nat inside
Gateway(config-if)# exit
Gateway(config)# interface <outside_interface>
Gateway(config-if)# ip address <IP> <MASK>
Gateway(config-if)# ip nat outside
...
Gateway(config)# access-list 1 permit <inside_network_IP> <wildcard>
Gateway(config)# ip nat inside source list 1 interface <outside_interface> overload
```

# 3	NAT Troubleshooting
| Command | Description |
| - | - |
| # show ip nat statistics | Literally statistics about configured NAT |
| # show ip nat translations | Displays IPs for NAT translations |
