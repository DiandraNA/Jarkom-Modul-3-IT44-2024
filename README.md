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
4. **Client** mendapatkan DNS dari keluarga **Fritz** dan dapat terhubung dengan internet melalui DNS tersebut.
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
---------------------------------------------------------------------------------------------------
## REVISI
Install DHCP di Tybur
```
apt-get update
apt install isc-dhcp-server
```
Lalu edit konfigurasi DHCP Server di ``/etc/dhcp/dhcpd.conf`` dan tambahkan config di atas kemudian restart DHCP-nya
```
service isc-dhcp-server restart
```
Install DHCP Relay di Paradis
```
apt-get update
apt-get install isc-dhcp-relay -y
```
Konfigurasi DHCP relay pada ``/etc/default/isc-dhcp-relay``
```
SERVERS="10.85.4.3"  # IP dari DHCP server (Tybur)
INTERFACES="eth1 eth2 eth3 eth4" 
```
Kemudian Restart DHCP Paradis
```
service isc-dhcp-relay restart
```
----------------------------------------------------------------------------------------------------------
Install BIND9 di Fritz
```
apt-get update
apt-get install bind9 -y
```
Konfigurasi forwarders BIND9 di ``/etc/bind/named.conf.options``
```
options {
    directory "/var/cache/bind";
    forwarders {
        192.168.122.1;  #     };
    allow-query { any; };
    listen-on-v6 { any; };
};
```
Tambahkan DNS zone untuk marley.it44.com dan eldia.it44.com di ``/etc/bind/named.conf.local``
```
zone "marley.it44.com" {
    type master;
    file "/etc/bind/jarkom/marley.it44.com";
};

zone "eldia.it44.com" {
    type master;
    file "/etc/bind/jarkom/eldia.it44.com";
};

```
Buat direktori untuk file zone
```
mkdir /etc/bind/jarkom
```
Buat file zone untuk marley.it44.com ``nano /etc/bind/jarkom/marley.it44.com``
```
;
; BIND data file for local loopback interface
;
$TTL    604800
@    IN    SOA    marley.it44.com. root.marley.it44.com. (
             2024102701        ; Serial
             604800        ; Refresh
             86400        ; Retry
             2419200        ; Expire
             604800 )    ; Negative Cache TTL
;
@    IN    NS    marley.it44.com.
@    IN    A     10.85.1.2        # IP untuk domain marley.it44.com (sesuaikan dengan IP dari Annie/Marley)

```
Buat file zona untuk eldia.it44.com ``nano /etc/bind/jarkom/eldia.it44.com``
```
;
; BIND data file for local loopback interface
;
$TTL    604800
@    IN    SOA    eldia.it44.com. root.eldia.it44.com. (
             2024102701        ; Serial
             604800        ; Refresh
             86400        ; Retry
             2419200        ; Expire
             604800 )    ; Negative Cache TTL
;
@    IN    NS    eldia.it44.com.
@    IN    A     10.85.2.2        # IP untuk domain eldia.it45.com (sesuaikan dengan IP dari Armin/Eldia)

```
Restart BIND9 di Fritz
```
service bind9 restart
```
Selanjutnya periksa IP Address untuk memastikan Zeke sudah mendapat IP yang benar ``ifconfig`` <br />
Tes koneksi dengan cara ping domain yang sudah dikonfigurasi
```
ping marley.it44.com
ping eldia.it44.com
```
