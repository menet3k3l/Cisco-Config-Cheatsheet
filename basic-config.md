# Modes

| Command | Description |
| -----------|-------------|
| > ***enable*** | Enter privileged EXEC mode |
| # ***configure terminal*** | Enter configuration mode |
| (config) ***interface \<ID>*** | Enter interface mode |

# Basic config
| Command | Description |
| -----------| ------------ |
| (config) ***hostname \<HOSTNAME>*** | Configure hostname |
| (config-if) ***ip address \<IP> \<MASK>*** | Assign IP address |
| (config-if) ***shutdown*** | Disable interface |
| (config-if) ***no shutdown*** | Enable interface |

# Telnet access
```
Switch# configure terminal 
Switch(config)# enable secret <password>	// password for privileged mode
Switch(config)# line vty 0 4		// VTY 0-4 config  
Switch(config-line)# login 		// will require a password <password> when connecting via TELNET  
Switch(config-line)#password <password> // specifies the TELNET password
```




