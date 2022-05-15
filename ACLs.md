# 1	Standard ACL
- Permit or deny packets based only on the **source** IPv4 address

- **Conditions (ACEs) are matched in top to down order and once a match is found, no further conditions are matched !!!**

## 1.1	Classical approach (numbered)
```
Router(config)# access-list <ACL_ID> permit/deny <matching_parameters>
```

- ACL_ID
	- Standard ACL uses **1 - 99** and **1300 - 1999**
- Permit/Deny
	- Allow or block traffic matching the \<matching_parameters>
- Matching_Parameters
	- **any** -> Match literally everything
	- **host \<IP>** -> match just the one IP address
	- **\<subnet_IP> \<wildcard>** -> match range of addresses

**Example**
```
Router(config)#access-list 10 permit 20.0.0.10 0.0.0.255  
Router(config)#access-list 10 deny any
```


## 1.2	Modern approach (numbered or named)
- start command with `ip access-list` instead of `access-list`

**Example**
```
Router(config)#ip access-list standard Secure_telnet  
Router(config-std-nacl)#permit 20.0.0.10 0.0.0.0  
Router(config-std-nacl)#exit  
Router(config)
```

OR

```
Router(config)#ip access-list standard 10  
Router(config-std-nacl)#permit 20.0.0.10 0.0.0.0  
Router(config-std-nacl)#exit  
Router(config)#
```


## 1.3	Enabling Standard IP ACL
```
Router(config)#interface type [slot_#]port_#  		// Get to interface config
Router(config-if)#ip access-group <ACL_ID> in|out
```

- IN -> Filter inbound traffic
- OUT -> Filter outbound traffic

**Example**
```
Router(config)#interface serial 0/0/0  
Router(config-if)#ip access-group 10 in
```

OR

```
Router(config)#interface serial 0/0/0  
Router(config-if)#ip access-group Secure_telnet out
```


# 2	Extended ACL

- Permit or deny packets based on **source IP, destination IP, protocol info, port number, message typce for ICMP and TCP/IP protocol such as FTP, HTTP, SSH, Telnet...**
- Basically more intelligent filter


## 2.1	Classical approach (numbered)
```
Router(config)# access-list ACL_ID permit/deny IP_protocol  
source_address source_wildcard_mask [protocol_information]  
destination_address destination_wildcard_mask [protocol_information] [log]
```

- ACL_ID
	- Extended ACL uses **100 - 199** and **2000 - 2699**
- Permit/Deny
	- Permit or deny traffic matching the following specified parameters

- IP_protocol -> two options
	- Host level filtering -> Filters which source addresses are able to access destination IP address
	- Application level filtering -> Filtering based on protocols


### 2.1.1	Host level filtering
- for **host level filtering** use keyword `ip`

```
Router(config)#access-list 100-199|2000-2699 permit/deny ip 
source_address source_wildcard_mask  
destination_address destination_wildcard_mask [log]
```

### 2.1.2	Application level filtering
**TCP/UDP**
- port numbers are used to distinguish between different applications adata

```
Router(config)#access-list 100-199|2000-2699 permit|deny  
tcp|udp source_address source_wildcard_mask [operator source_port_#]  
destination_address destination_wildcard_mask [operator destination_port_#]  
[established] [log]
```

- OPERATORS -> (optional, if not specified, ACL will match all TCP/UDP packets)

| Operator | Description |
| ------ | - |
| **lt** | Less than |
| **gt** | Greater than |
| **neq** | Not equal to |
| **eq** | Equal to |
| **Range** | Range of port numbers |

- Established
	- Used only with TCP packets
	- Allow traffic only if it is originated from inside
- Log
	- Log a message every time when an ACL is hit


**ICMP**

```
Router(config)# access-list 100-199|2000-2699 permit|deny icmp  
source_address source_wildcard_mask destination_address  
destination_wildcard_mask [icmp_message] [log]
```

ICMP Messages

| Message | Description | 
| - | -|
| **echo** | Used to check the status of destination (up/down)|
| **echo-reply** | Reply from the destination on "echo" request |
| **host-unreachable** | Network is reachable, but particular host is not responding |
| **net-unreachable** | Network is not reachable |
| **traceroute** | Filter traceroute information |
| **administrativelyprohibited** | Packet filtered by ACL |

**OTHER**
- Besides IP, TCP, UDP and ICMP we can filter a lot of other protocols...


## 2.2	 Modern approach (numbered or named)
```
Router(config)# ip access-list extended ACL_name_number  
Router(config-ext-acl)# permit|deny IP_protocol source_IP_address  
wildcard_mask [protocol_information]  
destination_IP_address wildcard_mask [protocol_information] [log]
```

## 2.3	Enabling Extended ACL
```
Router(config)#interface interface_number  
Router(config-if)#ip access-group ACL_Number_name in|Out
```


#	3 Delete ACL

**For standard approach**
```
Router(config)#no access-list ACL_Identifier_number
```

**For modern approach**
```
Router(config)# no ip access-list extended ACL_name_number
```
