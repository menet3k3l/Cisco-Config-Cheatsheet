# Modes

| Command | Description |
| -----------|-------------|
| > ***enable*** | Enter privileged EXEC mode |
| # ***configure terminal*** | Enter configuration mode |
| (config)# ***interface \<ID>*** | Enter interface mode |

# Basic config
| Command | Description |
| -----------| ------------ |
| (config)# ***hostname \<HOSTNAME>*** | Configure hostname |
| (config-if)# ***ip address \<IP> \<MASK>*** | Assign IP address |
| (config-if)# ***shutdown*** | Disable interface |
| (config-if)# ***no shutdown*** | Enable interface |

### Serial interface config
```
Router# configure terminal  
Router(config)# interface <serial_ID>  
Router(config-if)# clock rate <64000> // DCE -setting serial speed to 64 kbit/s 
Router(config-if)# no shutdown  
Router(config-if)# end
```
### Telnet access
```
Switch# configure terminal 
Switch(config)# enable secret <password>	// password for privileged mode
Switch(config)# line vty 0 4		// VTY 0-4 config  
Switch(config-line)# login 		// will require a password <password> when connecting via TELNET  
Switch(config-line)#password <password> // specifies the TELNET password
```

### Interface description
```
RX1#configure terminal    
RX1(config)#interface <interface_ID>  
RX1(config-if)#description <DESCRIPTION>
```