# CCNA

|How To|Commands|Attention|Show|
|--- |--- |--- |--- |
|Switch#|Show|Spanning-tree [vlan 2] run ip int brief int fa0/1 Int switchport Version Vlan Vtp status Int trunk|STP (Root/bridge info) inside RAM/ Saved Conf  ports situations FA0/1 info Vlan info of int version info Vlan status Vtp Info Trunked Interfaces|
|S#|Copy|[running-conf startup]||
|S#|Write|||
|SConfig#|Hostname||Changing name|
|SC#|Enable|[pass] [secret]|Privilege Mode Login pass|
|SC#|Banner|[motd]||
|SC#|IP|[domain-lookup]|[prevent from telneting to wrong comand]|
|SC#|Line|[console 0]||
|SC#|Interface|[fa0/1][range fa0/8-9]|Config mode of fa0/1|
|SC-line#|Password||Setting password for console port|
|SC-line#|Login||Enable password|
|SC-line#|Exec-timeout|[Number]|Logout after Idle|
|SC-if#|Switchport|Access Mode|Vlan 10 Trunk/dynamic auto/…|
|SC-interface#|Vtp|Mode Domain Password|Server/client /Transparent AAA XXX|
|SC#|Spanning-tree|Vlan <Nr.> priority <Nr.> Vlan <Nr.> root <Prim,Sec> Mode rapid-pvst <or PVST Def>|Changing switch priority Setting priorities  between vlans Changing types4|
|RC#|Ip dhcp|Pool <name> Excluded-address <ip>|Start new Pool Reserved IP|
|RC-pool#|Network  Default-router Dns-server|<net ip> <mask>  <ip>  <ip>|IP range Default gateway DNS|
|RC-if#|Ip helper-address|<ip>|Crossing DHCP packages to DHCP Server/router IP|
|RC-if#|Encapsulation|dot1Q <Vlan Nr>|Turning ON Trunk|
|RC#|Int fa0/1.2||Making Sub interface|
|RC#|Ip route|<Destination IP Net.0> <Mask>  <C IP>|Static Routing|
|R#|Show|Ip route Int ip brief|Show Routing Info|
|SVI#|Switchport|Trunk encaps dot1q Mode trunk|Turning Trunk ON|
|SVI#|No switchport||Make it port as router mode|
|SVI#|Ip routing||Turing ON Router|
|RC#|Router|Ergip [Nr]|Making/connecting to 50 Ergip|
|RC-ergip#|passive-interface|fa0/5|Disconnecting Hand fa0/5 to not sending RouteTable|
|RC-ergip#|redistribute static||Define as Marginal Router|
|RC#|ip route 0 0 IPDes||Global route-last route|
|Change Device Name|c# hostname <name>|||
|Set Type 7 Pass|C# Enable password <pass> C# service password-encrypt|Crack able Can be seen in Run|Show run|
|Set MD5 pass|C# Enable secret <pass>|||
|Set Console pass|C#line console 0 Password <pass> Login|||
|Idle LogOut from console|C#line console 0 Exec-timeout 5|||
|Make Banner|C#banner motd $ msg $|Shown before login||
|Turn off DNS lookup|C#no ip domain-lookup|||
|Add port to a VLAN|C-i# switch access vlan <Num>||Show vlan|
|Change Port mode|C-I# switch mode truck/access/dynamic auto||Show int trunk|
|Set Vtp Switches|C#vtp mode server(Def)-client-transparent vtp domain <name> Vtp pass 123||Show vtp status|
|STP|C#spanning-tree vlan 1 priority <NR> ---------- C#spanning-tree vlan 2 root primary/secondary|NR==Multiple of 4096|Show spanning-tree Show span vlan 2|
|Change STP mode-tech|C#spanning-tree mode rapid-pvst|PVST/Rapid PVST||
|Port Security|C-i# sw mode access Sw port-security Sw port-sec mac xx:xx:xx:xx:xx:xx Sw port-sec violation shut\protect\restrick|Must set as Access Turing ON Mac Filter (Allowed) After violation what happen (Shut Port\BLKPort\BLK+Log)|Sh port-security|
|MAC Port-Security Sticky|C-i#sw port-sec mac sticky Sw port max <Nr>|<Nr>==Max MAC can stick||
|EtherChannel|C#Int  range fa0/1-2 Channel-group 1 mode (ON\Desirable\Active\Auto\Passive)|ON-Manual Desirable\Active == PagP (Cisco) Auto\Passive == LACP (IEEE)|Sh ether summery|
|Set IP in Router|C#ip address -ip- -mask-||Show ip route Show ip int brief|
|Router on stick Sub int on Router|C# int fa0/1.<VLAN Nr> Encapsulation dot1q <VLAN Nr> Ip address …|||
|DHCP on Router|C#ip dhcp exclude 192.168.1.1  Ip dhcp pool <POOL NAME> Network 192.168.1.0 255.255.255.0 Default-gateway <IP> Dns-server <IP>|<-- Reserved IP||
|DHCP Routing|C # Ip helper-address <DHCP IP>|Cmd which lid\route DHCP pkg to DHCP Server  USER--*R*--R--DHCP Server  USER--*R*--R--DHCP Server  Need to Config in (*R*)||
|MLS SVI (Switch Virtual Interface)|C-i# sw trunk encapsulation dot1q Sw mode trunk Int vlan 2|Trunking  SVI 2||
|Turning on MLS router|C#ip routing|||
|Static Routing|# ip route 0.0.0.0 0.0.0.0 DestIP|||
|EIGRP|C# router EIGRP 1 No auto-summery Network 192.1.1.0 0.0.0.255  Passive-interface fa0/1 Redistribute static|Dynamic Routing •Don’t for get to set HANDS •Using 224.0.0.10 for RIGRP Multicast <-- Not sending Routing Table to fa0/1 Set the router as Last resort Router (مرزی)|Sh ip eigrp neighbors\topology Sh ip route|
|Changing INT delay \ BW|C-I # delay 100 Bandwidth 1000|||
|OSPF|C# router ospf 1 Router-id 5.5.5.5 Network 192.168.1.0 0.0.0.255 area 0  Passive-interface fa0/1 Default-info originate|<-- Not sending Routing Table to fa0/1 Last Resort|Sh ip ospf neighbor\... Sh ip route|
|NAT - PAT||||
|NAT Static||||
|NAT Dynamic||||
|ACL||||

* >User mode / #Privilege Mode / C# Global Mode
* Ctrl Z  go to en mode
* Ctrl shift 6 cancel command
* Sc# int range fa0/1-2 
* No + X   will cancel X
* Sc# enable pass XXX (Env pass which is viewable in Show Run)
* SC# enable secret XXXX (MD5)
* SC# banner motd $ xx $
* S# show int fa0/1| show int + brief
* SCI# no shut | shut
* SCI# ip address <IP address> <subnet mask>
* SC# hostname XX
* RC# ip route [destination_network] [mask] [next-hop]
* MLS-int# sw trunk encapsulation dot1q

## Telnet

* R1(config)#line vty 0
* R1(config-line)#password Pass12
* R1(config-line)#login
* R1(config-line)#logging synchronous
* R1(config-line)#exec-timeout 4
* R1(config-line)#motd-banner
* R1(config-line)#exit