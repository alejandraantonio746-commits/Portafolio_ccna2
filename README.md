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


# **CONFIGURACION DEL ROUTER (R1-CORE)**

````
interface gigabitEthernet 0/0/0
 no ip address
 no shutdown
 exit
interface gigabitEthernet 0/0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.254 255.255.255.0
 exit
interface gigabitEthernet 0/0/0.20
 encapsulation dot1Q 20
 ip address 192.168.20.254 255.255.255.0
 exit
interface gigabitEthernet 0/0/0.30
 encapsulation dot1Q 30
 ip address 192.168.30.254 255.255.255.0
 exit
interface gigabitEthernet 0/0/0.99
 encapsulation dot1Q 99
 ip address 192.168.99.254 255.255.255.0
 exit
interface gigabitEthernet 0/0/0.111
 encapsulation dot1Q 111 native
 no ip address
 exit
end

````

