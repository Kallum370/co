LAYER 3 SWITCH CONFIGUATUION

! Create VLANs
Switch(config)# vlan 10
Switch(config-vlan)# name Sales
Switch(config-vlan)# exit
Switch(config)# vlan 20
Switch(config-vlan)# name HR
Switch(config-vlan)# exit

! Configure SVI interfaces for inter-VLAN routing
Switch(config)# interface vlan 10
Switch(config-if)# ip address 192.168.10.1 255.255.255.0
Switch(config-if)# no shutdown
Switch(config-if)# exit
Switch(config)# interface vlan 20
Switch(config-if)# ip address 192.168.20.1 255.255.255.0
Switch(config-if)# no shutdown
Switch(config-if)# exit

! Configure trunk ports to access switches
Switch(config)# interface gigabitEthernet 0/1
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk allowed vlan 10,20
Switch(config-if)# exit
Switch(config)# interface gigabitEthernet 0/2
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk allowed vlan 10,20
Switch(config-if)# exit

! Configure uplink to router/firewall
Switch(config)# interface gigabitEthernet 0/24
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk allowed vlan 10,20
Switch(config-if)# exit

! Enable IP routing for inter-VLAN communication
Switch(config)# ip routing


SALES DEPT SWITCH

! Create VLAN
Switch(config)# vlan 10
Switch(config-vlan)# name Sales
Switch(config-vlan)# exit

! Configure access ports for Sales PCs
Switch(config)# interface range fastEthernet 0/1-10
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 10
Switch(config-if-range)# exit

! Configure trunk uplink to core switch
Switch(config)# interface gigabitEthernet 0/1
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk allowed vlan 10,20
Switch(config-if)# exit



HR DEPT SWITCH

! Create VLAN
Switch(config)# vlan 20
Switch(config-vlan)# name HR
Switch(config-vlan)# exit

! Configure access ports for HR PCs
Switch(config)# interface range fastEthernet 0/1-10
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 20
Switch(config-if-range)# exit

! Configure trunk uplink to core switch
Switch(config)# interface gigabitEthernet 0/1
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk allowed vlan 10,20
Switch(config-if)# exit
