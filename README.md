# Portafolio_ccna2
###### **ASIGNATURA: Manejo de tecnologías de conmutación y enrutamiento**
###### **ALUMNO:** Alejandra Monserrat Antonio Morelos
###### **Grupo:** 5101
###### **INSTITUCIÓN:** Plantel Conalep 039

# **TOPOLOGIA LAN**
<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/4dd0ce26-fce4-4b97-803f-c3c5a7ea4a8b" />

<br>
<br>
<br>

# **TABLA DE SUBREDES**
<br>

| DISPOSITIVO | VLAN | IP |
| ----------- | ----------- | -----------|
|Pc ADMIN | VLAN10 | 192.168.10.0/24 |
|PC ALUMNOS | VLAN20 | 192.168.20.0/24 |
|Pc DIRECCION | VLAN30 | 192.168.30.0/24 |
|Pc GESTION | VLAN99 | 92.168.99.0/24 |

<br>
<br>

# **AIGNACION DE VLAN Y PUERTOS (SW-Lab1, SW-Lab2)**

<br>
<br>

````
Switch>enable
Switch#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#vlan 10
Switch(config-vlan)#name ADMIN
Switch(config-vlan)#exit
Switch(config)#vlan 20
Switch(config-vlan)#name ALUMNOS
Switch(config-vlan)#exit
Switch(config)#vlan 30
Switch(config-vlan)#name DIRECCION
Switch(config-vlan)#exit
Switch(config)#end
Switch#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#interface range fa0/1-3
Switch(config-if-range)#switchport mode access
Switch(config-if-range)#switchport access vlan 10
Switch(config-if-range)#end
Switch#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#interface range fa0/4-6
Switch(config-if-range)#switchport mode access
Switch(config-if-range)#switchport access vlan 20
Switch(config-if-range)#exit
Switch(config)#interface fa0/7
Switch(config-if)#switchport mode access
Switch(config-if)#switchport access vlan 30
Switch(config-if)#end

````

<br>
<br>

# **CONFIGURACION DEL ROUTER (R1-CORE)**

````
R1-CORE>enable
R1-CORE#configure terminal
R1-CORE(config)#interface gigabitEthernet 0/0/0
R1-CORE(config-if)#no ip address
R1-CORE(config-if)#no shutdown
R1-CORE(config-if)#exit
R1-CORE(config)#interface gigabitEthernet 0/0/0.10
R1-CORE(config-subif)#encapsulation dot1Q 10
R1-CORE(config-subif)#ip address 192.168.10.254 255.255.255.0
R1-CORE(config-subif)#exit
R1-CORE(config)#interface gigabitEthernet 0/0/0.20
R1-CORE(config-subif)#encapsulation dot1Q 20
R1-CORE(config-subif)#ip address 192.168.20.254 255.255.255.0
R1-CORE(config-subif)#exit
R1-CORE(config)#interface gigabitEthernet 0/0/0.30
R1-CORE(config-subif)#encapsulation dot1Q 30
R1-CORE(config-subif)#ip address 192.168.30.254 255.255.255.0
R1-CORE(config-subif)#exit
R1-CORE(config)#interface gigabitEthernet 0/0/0.99
R1-CORE(config-subif)#encapsulation dot1Q 99
R1-CORE(config-subif)#ip address 192.168.99.254 255.255.255.0
R1-CORE(config-subif)#exit
R1-CORE(config)#interface gigabitEthernet 0/0/0.111
R1-CORE(config-subif)#encapsulation dot1Q 111 native
R1-CORE(config-subif)#no ip address
R1-CORE(config-subif)#exit
R1-CORE(config)#end

````
<br>
<br>


# **CONFIGURACION DE SW-CORE**

````

SW-CORE(config)#interface fa0/1
SW-CORE(config-if)#switchport mode trunk
SW-CORE(config-if)#switchport trunk native vlan 111
SW-CORE(config-if)#switchport trunk allowed vlan 10,20,30,99,111
SW-CORE(config-if)#no shutdown
SW-CORE(config-if)#exit
SW-CORE(config)#interface range fa0/2-3
SW-CORE(config-if-range)#switchport mode trunk
SW-CORE(config-if-range)#switchport trunk native vlan 111
SW-CORE(config-if-range)#switchport trunk allowed vlan 10,20,30,99,111
SW-CORE(config-if-range)#no shutdown
SW-CORE(config-if-range)#exit
SW-CORE(config)#interface fa0/9
SW-CORE(config-if)#switchport mode access
SW-CORE(config-if)#switchport access vlan 99
SW-CORE(config-if)#spanning-tree portfast
SW-CORE(config-if)#no shutdown
SW-CORE(config-if)#exit
SW-CORE(config)#interface vlan 99
SW-CORE(config-if)#ip address 192.168.99.1 255.255.255.0
SW-CORE(config-if)#no shutdown
SW-CORE(config-if)#exit
SW-CORE(config)#ip default-gateway 192.168.99.254
SW-CORE(config)#interface range fa0/4-8
SW-CORE(config-if-range)#switchport mode access
SW-CORE(config-if-range)#switchport access vlan 999
SW-CORE(config-if-range)#shutdown
SW-CORE(config-if-range)#exit
SW-CORE(config)#interface range fa0/10-24
SW-CORE(config-if-range)#switchport mode access
SW-CORE(config-if-range)#switchport access vlan 999
SW-CORE(config-if-range)#shutdown
SW-CORE(config-if-range)#exit
SW-CORE(config)#end
SW-CORE#copy running-config startup-config

````

| CREACION DE NOMBRE Y CONTRASEÑA SW-Lab1 |
| - |
| <img width="619" height="219" alt="image" src="https://github.com/user-attachments/assets/67610b12-5543-481b-8a2e-76806af79b73" />
 |

 <br>
 <br>

 |ASIGNACION DE ENLACES TRONCALES |
 | - |
 | <img width="619" height="458" alt="image" src="https://github.com/user-attachments/assets/551eb975-1b4a-4529-b5e4-8ff75506d404" /> |

 <br>
 <br>

# **CONFIGURACION DEL SW-Lab1**

````
SW-Lab1(config)#interface range fa0/1-3
SW-Lab1(config-if-range)#switchport mode access
SW-Lab1(config-if-range)#switchport access vlan 10
SW-Lab1(config-if-range)#spanning-tree portfast
SW-Lab1(config-if-range)#no shutdown
SW-Lab1(config-if-range)#exit
SW-Lab1(config)#interface range fa0/4-6
SW-Lab1(config-if-range)#switchport mode access
SW-Lab1(config-if-range)#switchport access vlan 20
SW-Lab1(config-if-range)#spanning-tree portfast
SW-Lab1(config-if-range)#no shutdown
SW-Lab1(config-if-range)#exit
SW-Lab1(config)#interface fa0/7
SW-Lab1(config-if)#switchport mode access
SW-Lab1(config-if)#switchport access vlan 30
SW-Lab1(config-if)#spanning-tree portfast
SW-Lab1(config-if)#no shutdown
SW-Lab1(config-if)#exit
SW-Lab1(config)#interface fa0/24
SW-Lab1(config-if)#switchport mode trunk
SW-Lab1(config-if)#switchport trunk native vlan 111
SW-Lab1(config-if)#switchport trunk allowed vlan 10,20,30,99,111
SW-Lab1(config-if)#no shutdown
SW-Lab1(config-if)#exit
SW-Lab1(config)#interface vlan 99
SW-Lab1(config-if)#ip address 192.168.99.2 255.255.255.0
SW-Lab1(config-if)#no shutdown
SW-Lab1(config-if)#exit
SW-Lab1(config)#ip default-gateway 192.168.99.254
SW-Lab1(config)#interface range fa0/8-23
SW-Lab1(config-if-range)#switchport mode access
SW-Lab1(config-if-range)#switchport access vlan 999
SW-Lab1(config-if-range)#shutdown
SW-Lab1(config-if-range)#exit
SW-Lab1(config)#end
SW-Lab1#copy running-config startup-config

````

| ASIGNACION DE NOMBRE Y CONTRASEÑA SW-Lab2 |
| - |
| <img width="624" height="249" alt="image" src="https://github.com/user-attachments/assets/4f92fd32-8d5a-4f4c-888f-8ea34aa20651" />
 |

| CONFIGURACION MODO TRONCAL SW_Lab2|
| - |
|<img width="621" height="334" alt="image" src="https://github.com/user-attachments/assets/c2c37af7-ba81-4107-b8fd-28ade8a6a247" /> |

# ** CONFIGURACION DE SW-LAB2 **

````
SW-Lab2(config-line)#inteface range fa0/1-3
                     ^
% Invalid input detected at '^' marker.
	
SW-Lab2(config-line)#interface range fa0/1-3
SW-Lab2(config-if-range)#switchport mode access
SW-Lab2(config-if-range)#
%CDP-4-NATIVE_VLAN_MISMATCH: Native VLAN mismatch discovered on FastEthernet0/24 (1), with SW-CORE FastEthernet0/3 (111).

SW-Lab2(config-if-range)#switchport access vlan 10
SW-Lab2(config-if-range)#spanning-tree portfast
%Warning: portfast should only be enabled on ports connected to a single
host. Connecting hubs, concentrators, switches, bridges, etc... to this
interface  when portfast is enabled, can cause temporary bridging loops.
Use with CAUTION

%Portfast has been configured on FastEthernet0/1 but will only
have effect when the interface is in a non-trunking mode.
%Warning: portfast should only be enabled on ports connected to a single
host. Connecting hubs, concentrators, switches, bridges, etc... to this
interface  when portfast is enabled, can cause temporary bridging loops.
Use with CAUTION

%Portfast has been configured on FastEthernet0/2 but will only
have effect when the interface is in a non-trunking mode.
%Warning: portfast should only be enabled on ports connected to a single
host. Connecting hubs, concentrators, switches, bridges, etc... to this
interface  when portfast is enabled, can cause temporary bridging loops.
Use with CAUTION

%Portfast has been configured on FastEthernet0/3 but will only
have effect when the interface is in a non-trunking mode.
SW-Lab2(config-if-range)#
%CDP-4-NATIVE_VLAN_MISMATCH: Native VLAN mismatch discovered on FastEthernet0/24 (1), with SW-CORE FastEthernet0/3 (111).

SW-Lab2(config-if-range)#no shutdown
SW-Lab2(config-if-range)#
SW-Lab2(config-if-range)#exit
SW-Lab2(config)#
%CDP-4-NATIVE_VLAN_MISMATCH: Native VLAN mismatch discovered on FastEthernet0/24 (1), with SW-CORE FastEthernet0/3 (111).

%CDP-4-NATIVE_VLAN_MISMATCH: Native VLAN mismatch discovered on FastEthernet0/24 (1), with SW-CORE FastEthernet0/3 (111).

%CDP-4-NATIVE_VLAN_MISMATCH: Native VLAN mismatch discovered on FastEthernet0/24 (1), with SW-CORE FastEthernet0/3 (111).

SW-Lab2(config)#
%CDP-4-NATIVE_VLAN_MISMATCH: Native VLAN mismatch discovered on FastEthernet0/24 (1), with SW-CORE FastEthernet0/3 (111).
interface range fa0/4-6
SW-Lab2(config-if-range)#switchport mode access
SW-Lab2(config-if-range)#switchport access 
%CDP-4-NATIVE_VLAN_MISMATCH: Native VLAN mismatch discovered on FastEthernet0/24 (1), with SW-CORE FastE
SW-Lab2(config-if-range)#switchport access vlan 20
SW-Lab2(config-if-range)#spanning-tree portfast
%Warning: portfast should only be enabled on ports connected to a single
host. Connecting hubs, concentrators, switches, bridges, etc... to this
interface  when portfast is enabled, can cause temporary bridging loops.
Use with CAUTION

%Portfast has been configured on FastEthernet0/4 but will only
have effect when the interface is in a non-trunking mode.
%Warning: portfast should only be enabled on ports connected to a single
host. Connecting hubs, concentrators, switches, bridges, etc... to this
interface  when portfast is enabled, can cause temporary bridging loops.
Use with CAUTION

%Portfast has been configured on FastEthernet0/5 but will only
have effect when the interface is in a non-trunking mode.
%Warning: portfast should only be enabled on ports connected to a single
host. Connecting hubs, concentrators, switches, bridges, etc... to this
interface  when portfast is enabled, can cause temporary bridging loops.
Use with CAUTION

%Portfast has been configured on FastEthernet0/6 but will only
have effect when the interface is in a non-trunking mode.
SW-Lab2(config-if-range)#no shutdown
SW-Lab2(config-if-range)#exit
SW-Lab2(config)#interface
%CDP-4-NATIVE_VLAN_MISMATCH: Native VLAN mismatch discovered on FastEthernet0/24 (1), with SW-CORE FastEthernet0/3 (111).

% Incomplete command.
SW-Lab2(config)#interface fa0/7
SW-Lab2(config-if)#switchport mode access
SW-Lab2(config-if)#switchport access vlan 30
SW-Lab2(config-if)#spanning-tree portfast
%Warning: portfast should only be enabled on ports connected to a single
host. Connecting hubs, concentrators, switches, bridges, etc... to this
interface  when portfast is enabled, can cause temporary bridging loops.
Use with CAUTION

%Portfast has been configured on FastEthernet0/7 but will only
have effect when the interface is in a non-trunking mode.
SW-Lab2(config-if)#
%CDP-4-NATIVE_VLAN_MISMATCH: Native VLAN mismatch discovered on FastEthernet0/24 (1), with SW-CORE FastEthernet0/3 (111).

SW-Lab2(config-if)#no shutdown
SW-Lab2(config-if)#exit
SW-Lab2(config)#
SW-Lab2(config)#interface fa0/24
SW-Lab2(config-if)#switchport mode trunk
SW-Lab2(config-if)#switchport trunk native vlan 111
SW-Lab2(config-if)#%SPANTREE-2-UNBLOCK_CONSIST_PORT: Unblocking FastEthernet0/24 on VLAN0111. Port consistency restored.

%SPANTREE-2-UNBLOCK_CONSIST_PORT: Unblocking FastEthernet0/24 on VLAN0001. Port consistency restored.


SW-Lab2(config-if)#switchport trunk allowed vlan 10,20,30,99,111
SW-Lab2(config-if)#no shut down
SW-Lab2(config-if)#exit
SW-Lab2(config)#
SW-Lab2(config)#interface vlan 99
SW-Lab2(config-if)#
%LINK-5-CHANGED: Interface Vlan99, changed state to up

%LINEPROTO-5-UPDOWN: Line protocol on Interface Vlan99, changed state to up

SW-Lab2(config-if)#ip address 192.168.99.3 255.255.255.0
SW-Lab2(config-if)#no shutdown
SW-Lab2(config-if)#exit
SW-Lab2(config)#
SW-Lab2#
%SYS-5-CONFIG_I: Configured from console by console



````

