# 1	Port Security
- Checks if MAC address of a connected device is allowed to communicate

```
Switch(config)# interface <interface>  
switch(config-if)# switchport mode access  	// ACCESS mode
Switch(config-if)# switchport port-security		//enable port security
Switch(config-if)# switchport port-security maximum <MAX_ADDRESSES> 
Switch(config-if)# switchport port-security mac-address <MAC_ADDRESS>	// manual entry  
Switch(config-if)# switchport port-security mac-address sticky  // dynamic MAC addr. learning
Switch(config-if)# switchport port-security violation {shutdown/restrict/protect}
```

- MAX_ADDRESSES
	- How many MAC addresses can connect to the port
- Manual vs. Dynamic
	- Manual entry -> Manually specify allowed MAC address
	- Dynamic (sticky) -> Connect something and it will learn the MAC address of the device
- 3 modes of reactions when a security violation occurs:
	- **protect**
		- Allowed MAC addresses can communicate, traffic from unauthorized MAC addresses is discarded
	- **restrict**
		- Same as *protect* but error message is logged and if SNMP is configured, SNMP trap is sent to the SNMP server
	- **shutdown**
		- All communication is discarded (even from allowed addresses)
		- Port is switched to the `error-disable` state (basically shutdown)
		- Admin has to manually enable the port again


# 2	DHCP Snooping
-	**DHCP Spoofing** protection

*Note: DHCP spoofing occurs when an attacker attempts to respond to DHCP requests and trying to list themselves (spoofs) as the default gateway or DNS server, hence, initiating a man in the middle attack.*

**How it works?**
- Divides ports into **trusted** and **untrusted**
	- If a genuine DHCP server is connected to the port -> **trusted**
	- If a PC or some other switch WITHOUT DHCP Snooping is connected to the port -> **untrusted**
- Switch with DHCP Snooping checks if DHCP Responses are sent from trusted ports, block responses from untrusted ports
- Limits the ammount of DHCP requests
- Can build a **DHCP Snooping Binding Database** -> used to protect against other attacks
	- Connections between MAC addr., IP addr., time of lease, port to which the device is connected... -> Used by Dynamic ARP Inspection (DAI) -> protection against ARP Cache Poisoning


**Config**
```
Switch(config)# ip dhcp snooping
Switch(config)# no ip dhcp snooping information option
Switch(config)# ip dhcp snooping vlan <VLAN_ID>/<VLAN_Range>
Switch(config)# interface fastethernet <PORT_ID>
Switch(config-if)# ip dhcp snooping trust
Switch(config-if)# ip dhcp snooping limit rate <rate>
```

- DHCP Snooping Binding Database -> enable
```
Switch(config)# ip dhcp snooping database flash:/dhcpbind.txt
```


# 3	Dynamic ARP Inspection (DAI)

- protection against **ARP Cache Poisoning/ARP Spoofing** attack

*Note: ARP Spoofing is a way to initiate the MITM attack. Consider 3 devices in the network 1) Attacker, 2) Victim, 3) Gateway. The Attacker sends an ARP Reply packet to the Victim, claiming that he's the Gateway. Then the Attacker sends an ARP Reply packet to the Gateway, claiming that he's the Victim. This poisons the ARP cache on both Gateway and Victim and now when Victim and Gateway want to talk to each other, they both talk to the Attacker - and you have MITM.*

*The issue is that you can just change the IP address in the ARP cache with a spoofed ARP Reply packet...that no one even asked for!*


**How DAI works?**
- Uses the DHCP Snooping Binding Database (created with DHCP Snooping)
- If an ARP packets arrives to a trusted port, it's forwarded
- If an ARP packets arrives to an untrusted port, it's further analyzed
	- If it's an ARP Request message, network processor checks if MAC and IP address of the PC requesting the translation belong together. If yes -> forward packet. If no -> discard.
	- In the case of an ARP Reply message, MAC and IP of the PC responding to the ARP Request message are checked to see if they belong together.
	- Combinations of IP and MAC addresses are taken from the database created by DHCP Snooping

**Config**
```
Switch(config)# ip arp inspection vlan <VLAN_ID>	// enabling DAI
Switch# show ip arp inspection vlan <VLAN_ID>		// watched VLANs
Switch(config)# interface fasethernet <PORT_ID>
Switch(config-if)# ip arp inspection trust		// trusted port, disable DAI for this port
```


# 4	IP Source Guard
- Checks spoofed IP addresses
- Allows for blocking unauthorized IP addresses on given ports
- Uses DHCP Snooping Binding Database

**Config**
```
Switch(config)# interface <interface>
Switch(config-if)# ip verify source port-security
```
