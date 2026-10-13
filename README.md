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

| ASIGNACION DE NOMBRE Y CONTRASEÑA AL ROUTER|
| - |
| <img width="537" height="305" alt="image" src="https://github.com/user-attachments/assets/c3e38645-832e-42ae-a03d-9eb869a767e2" /> |


| SUBINTERFACES DEL ROUTER |
| - |
|<img width="628" height="509" alt="image" src="https://github.com/user-attachments/assets/73d7e7bc-1702-4785-994d-22aa59893b1f" />
|
|<img width="634" height="453" alt="image" src="https://github.com/user-attachments/assets/7d938f15-83bc-48c4-a278-2a3bf67cc4d5" />
|
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
