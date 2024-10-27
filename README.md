### Anggota Kelompok
| Nama | NRP |
| ---- | --- |
| Diandra Naufal Abror | 5027231004 |
| Acintya Edria Sudarsono | 5027231020 |

### Topologi
![Screenshot 2024-10-27 203445](https://github.com/user-attachments/assets/97d50dfb-084b-4e13-97be-dd7f136ddb73)

### Tabel IP
| Node | IP | 
| ---- | -- |
| Paradis | 10.85.1.1 |
| | 10.85.2.1 |
| | 10.85.3.1 |
| | 10.85.4.1 |
| Annie | 10.85.1.2 |
| Bertholdt | 10.85.1.3 |
| Reiner | 10.85.1.4 |
| Armin | 10.85.2.2 |
| Eren | 10.85.2.3 |
| Mikasa | 10.85.2.4 |
| Beast | 10.85.3.2 |
| Colossal | 10.85.3.3 |
| Warhammer | 10.85.3.4 |
| Fritz | 10.85.4.2 |
| Tybur | 10.85.4.3 |

### Konfigurasi
1. Paradis
```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 10.85.1.1
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 10.85.2.1
	netmask 255.255.255.0

auto eth3
iface eth3 inet static
	address 10.85.3.1
	netmask 255.255.255.0

auto eth4
iface eth4 inet static
	address 10.85.4.1
	netmask 255.255.255.0
```
2. Annie
```
auto eth0
iface eth0 inet static
	address 10.85.1.2
	netmask 255.255.255.0
	gateway 10.85.1.1
```
3. Bertholdt
```
auto eth0
iface eth0 inet static
    address 10.85.1.3
    netmask 255.255.255.0
    gateway 10.85.1.1
```
4. Reiner
```
auto eth0
iface eth0 inet static
    address 10.85.1.4
    netmask 255.255.255.0
    gateway 10.85.1.1
```
5. Armin
```
auto eth0
iface eth0 inet static
    address 10.85.2.2
    netmask 255.255.255.0
    gateway 10.85.2.1
```
6. Eren
```
auto eth0
iface eth0 inet static
    address 10.85.2.3
    netmask 255.255.255.0
    gateway 10.85.2.1
```
7. Mikasa
```
auto eth0
iface eth0 inet static
    address 10.85.2.4
    netmask 255.255.255.0
    gateway 10.85.2.1
```
8. Beast
```
auto eth0
iface eth0 inet static
    address 10.85.3.2
    netmask 255.255.255.0
    gateway 10.85.3.1
```
9. Colossal
```
auto eth0
iface eth0 inet static
    address 10.85.3.3
    netmask 255.255.255.0
    gateway 10.85.3.1
```
10. Warhammer
```
auto eth0
iface eth0 inet static
    address 10.85.3.4
    netmask 255.255.255.0
    gateway 10.85.3.1
```
11. Fritz
```
auto eth0
iface eth0 inet static
    address 10.85.4.2
    netmask 255.255.255.0
    gateway 10.85.4.1
```
12. Tybur
```
auto eth0
iface eth0 inet static
    address 10.85.4.3
    netmask 255.255.255.0
    gateway 10.85.4.1
```
13. Erwin & Zeke
```
auto eth0
iface eth0 inet dhcp
```

Jalankan port forwarding pada Paradis 
```
sysctl -w net.ipv4.ip_forward=1
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
```
