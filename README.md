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

### Soal
1. Semua **Client** harus menggunakan konfigurasi ip address dari keluarga **Tybur (dhcp)**.
2. **Client** yang melalui bangsa marley mendapatkan range IP dari [prefix IP].1.05 - [prefix IP].1.25 dan [prefix IP].1.50 - [prefix IP].1.100.
4. **Client** yang melalui bangsa eldia mendapatkan range IP dari [prefix IP].2.09 - [prefix IP].2.27 dan [prefix IP].2 .81 - [prefix IP].2.243.
4.**Client** mendapatkan DNS dari keluarga **Fritz** dan dapat terhubung dengan internet melalui DNS tersebut.
5. Dikarenakan keluarga **Tybur** tidak menyukai kaum **eldia**, maka mereka hanya meminjamkan ip address ke kaum **eldia** selama 6 menit. Namun untuk kaum **marley**, keluarga **Tybur** meminjamkan ip address selama 30 menit. Waktu maksimal dialokasikan untuk peminjaman alamat IP selama 87 menit.
```
#Konfigurasi Tybur

echo 'INTERFACESv4="eth0"' > /etc/default/isc-dhcp-server

echo 'subnet 10.85.1.0 netmask 255.255.255.0 {
#Range IP Marley
        range 10.85.1.05 10.85.1.25;
        range 10.85.1.50 10.85.1.100;
        option routers 10.85.1.1;
#DNS Server Fritz
        option broadcast-address 10.85.1.255;
        option domain-name-servers 10.85.4.2;
#Durasi DHCP Marley
        default-lease-time 1800;
        max-lease-time 5220;
}

subnet 10.85.2.0 netmask 255.255.255.0 {
#Range IP Eldia
        range 10.85.2.09 10.85.2.27;
        range 10.85.2.81 10.85.2.243;
        option routers 10.85.2.1;
#DNS Server Fritz
        option broadcast-address 10.85.2.255;
        option domain-name-servers 10.85.4.2;
#Durasi DHCP Eldia
        default-lease-time 360;
        max-lease-time 5220;
}

subnet 10.85.3.0 netmask 255.255.255.0 {
        option routers 10.85.3.1;
}

subnet 10.85.4.0 netmask 255.255.255.0 {
        option routers 10.85.4.1;
}
' > /etc/dhcp/dhcpd.conf

service isc-dhcp-server restart
```
