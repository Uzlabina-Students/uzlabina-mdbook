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

> Default username a password na virtuálech je `fresh:fresh`

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

## 3. Hodina 2020-10-01

### Šifrování pomocí LUKS2

```
# fdisk /dev/vdb
```

- Poté příkazy

```
g
n (default, default - 2x enter)
+2.5G
w
```

- Dále šifrování - je potřeba nainstalovat `cryptsetup`

```
# apt install cryptsetup
```

- Používání cryptsetup

```
# cryptsetup luksFormat /dev/vdb1
(YES) - doporučené heslo je ahoj
# cryptsetup open /dev/vdb1 <nazev>
```

*po zadání hesla se šifrovaný disk objeví v `/dev/mapper/<nazev>`*

- Nyní je potřeba ho naformátovat

```
# mkfs.ext4 /dev/mapper/<nazev>
```

- Poté vytvoření LVM

```
# apt install lvm2
# pvcreate /dev/mapper/<nazev>
# vgcreate storage /dev/mapper/<nazev>
# lvcreate --name=data --size=1G storage
# lvcreate --name=swap --size=1G storage
# mkfs.ext4 storage-data
# mkswap storage-swap
# swapon /dev/mapper/storage-swap
```

- Vytvoření klíče

```
# dd if=/dev/urandom of=/root/cryptkey bs=1024 count=4
# cryptsetup luksAddKey /dev/vdb1 /root/cryptkey
# cryptsetup luksDump /dev/vdb1 #pouze kontrola
```

- Automatické spouštění šifrování
	- Zjistit UUID
```
# blkid /dev/vdb1
```
(toto UUID bude poté vloženo do následujícího souboru)

*soubor `/etc/crypttab`*

```
sifrovane	UUID=<UUID>	/root/cryptkey	luks
```

**Nyní je potřeba restart systému a hodně štěstí gg**

Pokud vše proběhlo úspěšně, nyní můžeme nastavit mount v `/etc/fstab`

- Vytvoření nějakého mountpointu
```
# mkdir /mnt/data
```
a následně úprava souboru `/etc/fstab`
```
#mount úložiště
/dev/mapper/storage-data	/mnt/data	ext4	defaults	0	0
#mount swapu
/dev/mapper/storage-swap	none		swap	defaults	0	0
```

- Po uložení souboru provést remount

```
# mount -a -o remount,rw
```

**Poté opět reboot**

- Zkontrolovat zda existuje /mnt/data (adresář)