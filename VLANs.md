# 1	VLAN config
## 1.1	Creating VLAN
```
Switch# configure terminal  
Switch(config)# vlan <vlan_ID>		// creating VLAN with <ID> (number)  
Switch(config-vlan)# name <VLAN_NAME> //  assigning a name to created VLAN
Switch(config-vlan)# end
```

## 1.2	Interface ACCESS mode and VLAN assignment
```
Switch# configure terminal  
Switch(config)# interface <interface_ID>  
Switch(config-if)# switchport mode access  		// enabling ACCESS mode
Switch(config-if)# switchport access vlan <vlan_ID>	// vlan assignment 
Switch(config-if)# exit
```

## 1.3	TRUNK mode
```
Switch# configure terminal  
Switch(config)# interface <interface_ID>  
Switch(config-if)# switchport mode trunk  
Switch(config-if)# exit
```

## 1.4	Router - virtual interfaces, 802.1q trunking
```
RX1(config)#interface fastEthernet 0/1.10 		// VLAN 10  
RX1(config-subif)#encapsulation dot1Q 10 		// VLAN 10
```



# 2	VLAN troubleshooting
| Command | Description |
| ---------- | ----------- |
| # ***show running-config*** | Prints current configuration |
| # ***show ip interface brief*** | Info about all interfaces |
| # ***show vlan*** | VLAN table and assigned interfaces |
| # ***show mac address-table*** | Prints MAC table |
| # ***show interfaces status*** | Status of all interfaces |