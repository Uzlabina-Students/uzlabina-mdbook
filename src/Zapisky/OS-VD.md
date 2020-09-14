# Operační Systémy (VD)

## 1. Hodina

### Přihlášení k místním účtům

Uživatel: `Lab130`
Heslo: `Laborator130`

IP adresa virtuálů: `10.1.1.184` (Pravděpodobně dočasná)

### Kopírování účtů

```
$ cp /zlabshare/I4X/3_machines/image.d/* image.d
$ cp /zlabshare/.zshinit_source .zshinit
```
## 2. Hodina 2020-09-10

### Konfigurace Linux zařízení jako router

- 3 stroje: client, server, router
- změna konfigurace v /etc/network/interfaces a /etc/sysctl.conf

#### Konfigurace klienta
*/etc/network/interfaces/*
```
source /etc/network/interfaces.d/*


auto lo
iface lo inet loopback

allow-hotplug ens3
iface ens3 inet dhcp

allow-hotplug ens4
iface ens4 inet static
address 10.0.1.10/24
post-up ip route add 10.0.2.0/24 dev ens4 via 10.0.1.1
```
#### Konfigurace serveru
*/etc/network/interfaces/*
```
source /etc/network/interfaces.d/*


auto lo
iface lo inet loopback

allow-hotplug ens3
iface ens3 inet dhcp

allow-hotplug ens4
iface ens4 inet static
address 10.0.1.1/24

allow-hotplug ens5
iface ens5 inet staitc
address 10.0.2.1/24
```
*/etc/sysctl.conf*


Odkomentovat řádek obsahující ``net.ipv4.ip_forward=1``
#### Konfigurace routeru
*/etc/network/interfaces/*
```
source /etc/network/interfaces.d/*


auto lo
iface lo inet loopback

allow-hotplug ens3
iface ens3 inet dhcp

allow-hotplug ens4
iface ens4 inet static
address 10.0.2.2/24
post-up ip route add 10.0.1.0/24 dev ens4 via 10.0.2.1
```