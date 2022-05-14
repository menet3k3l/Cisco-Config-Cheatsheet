# VLAN config
## Creating VLAN
```
Switch# configure terminal  
Switch(config)# vlan <vlan_ID>		// creating VLAN with <ID> (number)  
Switch(config-vlan)# name <VLAN_NAME> //  assigning a name to created VLAN
Switch(config-vlan)# end
```

## Interface ACCESS mode and VLAN assignment
```
Switch# configure terminal  
Switch(config)# interface <interface_ID>  
Switch(config-if)# switchport mode access  		// enabling ACCESS mode
Switch(config-if)# switchport access vlan <vlan_ID>	// vlan assignment 
Switch(config-if)# exit
```

## TRUNK mode
```
Switch# configure terminal  
Switch(config)# interface <interface_ID>  
Switch(config-if)# switchport mode trunk  
Switch(config-if)# exit
```


# Troubleshooting
| Command | Description |
| ---------- | ----------- |
| # show running-config | Prints current configuration |
| # show ip interface brief | Info about all interfaces |
| # show vlan | VLAN table and assigned interfaces |
| # show mac address-table | Prints MAC table |
| # show interfaces status | Status of all interfaces |