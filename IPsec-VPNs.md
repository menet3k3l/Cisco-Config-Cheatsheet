# 1	IPsec VPNs
## 1.1	Phase 1 - IKE + ISAKMP setup
**IKE setup + ISAKMP**
```
Router(config)# crypto isakmp policy 1
Router(config-isakmp)# authentication pre-share
Router(config-isakmp)# encryption {des|3des|aes 128|aes 192|aes 256}
Router(config-isakmp)# hash {md5|sha}
Router(config-isakmp)# group {1|2|5}
Router(config-isakmp)# lifetime 86400
```

 **PSK setup**

```
Router(config)# crypto isakmp key <SECRET_KEY> address <OPPOSITE_ROUTER_IP>
```


## 1.2	Phase 2 - IPsec config
```
Router(config)# crypto ipsec transform-set ESP-AES esp-aes 256 esp-sha-hmac
Router(config)# ip access-list extended <eACL_NAME>
Router(config-ext-nacl)# permit ip <source_network_IP> <source_wildcard> <destination_network_IP> <destination_wildcard>
Router(config)# crypto map <IPSEC_MAP_NAME> 1 ipsec-isakmp
Router(config-crypto-map)# match address <eACL_NAME>
Router(config-crypto-map)# set peer <OPPOSITE_ROUTER_IP> default
Router(config-crypto-map)# set transform-set ESP-AES
Router(config-crypto-map)# set pfs group2
Router(config-crypto-map)# set security-association lifetime seconds 86400
Router(config)# interface <interface>
Router(config-if)# crypto map <IPSEC_MAP_NAME>
```


# 2 IPsec-VPNs Troubleshooting
| Command | Description |
| - | - |
| # ***show crypto isakmp sa*** | info about the VPN tunnel |
| # ***show crypto isakmp key*** | info about the VPN tunnel |
| # ***show crypto ipsec sa*** | info about the VPN tunnel |