# 1	Modes

| Command | Description |
| -----------|-------------|
| > ***enable*** | Enter privileged EXEC mode |
| # ***configure terminal*** | Enter configuration mode |
| (config)# ***interface \<ID>*** | Enter interface mode |

# 2	Basic config
| Command | Description |
| -----------| ------------ |
| (config)# ***hostname \<HOSTNAME>*** | Configure hostname |
| (config-if)# ***ip address \<IP> \<MASK>*** | Assign IP address |
| (config-if)# ***shutdown*** | Disable interface |
| (config-if)# ***no shutdown*** | Enable interface |

## 2.1	Serial interface config
```
Router# configure terminal  
Router(config)# interface <serial_ID>  
Router(config-if)# clock rate <64000> // DCE -setting serial speed to 64 kbit/s 
Router(config-if)# no shutdown  
Router(config-if)# end
```
## 2.2	Telnet access
```
Switch# configure terminal 
Switch(config)# enable secret <password>	// password for privileged mode
Switch(config)# line vty 0 4		// VTY 0-4 config  
Switch(config-line)# login 		// will require a password <password> when connecting via TELNET  
Switch(config-line)#password <password> // specifies the TELNET password
```

## 2.3	Interface description
```
RX1#configure terminal    
RX1(config)#interface <interface_ID>  
RX1(config-if)#description <DESCRIPTION>
```

## 2.4	Some stuff that's good just to be sure?
- Synchronised console output
```
Router(config)#line console 0  
Router(config-line)#logging synchronous
```

- Disable automatic domain name to IP translation
```
Router(config)#no ip domain-lookup
```
