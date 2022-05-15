# 1	Routing
## 1.1	Static route
| Command | Description |
| ---------- | ---------- |
| (config)# ***ip route <DESTINATION_NETWORK_IP> \<MASK> <NEXT_HOP_IP>*** | Static route |
| (config)# ***ip route <DESTINATION_NETWORK_IP> \<MASK> <OUTGOING_INTERFACE>*** | Static route |

## 1.2	RIP
```
RX1(config)#router rip  				// enabling RIP
RX1(config-router)#version 2  			// use version 2
RX1(config-router)#network <NETWORK_IP>  // activate interfaces that belong to this network
RX1(config-router)#no auto-summary  
RX1(config-router)#end
```

- the `network` commands basically advertises specified networks

**Default route in RIP**
- First add static default route
```
R1(config)#ip route 0.0.0.0 0.0.0.0 <NEXT_HOP>/<OUTGOING_INTERFACE>
```

- Then advertise it to others with RIP
```
R1(config)#router rip
R1(config-router)#default-information originate 
```



# 2	Routing Troubleshooting
| Command | Description |
| -----------| -----------|
| # ***show running-config*** | Prints current configuration |
| # ***show ip interface brief*** | Info about all interfaces |
| # ***show ip route*** | Prints routing table |
| # ***show ip protocols*** | Info about configured routing protocols |
| # ***show cdp neighbors*** | Info about connected (neighbor) devices |


