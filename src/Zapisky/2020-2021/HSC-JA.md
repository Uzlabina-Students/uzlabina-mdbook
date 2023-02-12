# Hardware a sítě - Cvičení (JA)

## 1. Hodina 2020-09-18

- Provozní řád učebny

### Témata předmětu

- Úvod, RouterBOARD, RouterOS
- Konfigurace, upgrade, licence
- Statický routing, bridging
- Bezdrátové sítě
- DHCP klient a server
- Nástroje, technická podpora
- Firewall, filtr provozu, NAT
- Tunelování, QoSw

#### Zdroje informací
- [jakubec.lab.uzlabina.cz](https://jakubec.lab.uzlabina.cz/)
- [Mikrotik](https://mikrotik.com/)

### RouterOS software a RouterBOARD hardware
- Motání kabelů (pozor na to)
- Resetování RouterBOARDu - [chování reset tlačítka](https://www.mikrotik.com.my/reset-to-factory-default-settings/)
- Nastavení sekundární síťové karty v PC jako DHCP klienta
- Možnost využití aplikace WinBox
- Možnost připojení pomocí MAC adresy, komunikace pomocí raw ethernet rámců

#### Představení firmy Mikrotik
- 1995
- Začala jako wireless výrobce
- Vlastní systém RouterOS
	- Linux based
- RouterBOARD
	- Předinstalovaný RouterOS
	- Obvykle dodávané s boxy a napájecími zdroji
		- Indoor a outdoot
		- I od jiných firem
		- Výběr na základě odolnosti, rozhraní...
	- Možnost nákup samotných desek
- WispAP

#### Příklad výrobku (hotový router)

- [RB951G-2HnD](https://mikrotik.com/product/RB951G-2HnD)
![Mikrotik RB951G-2HnD](https://img.alza.cz/Foto/LegendFoto/photos/PW023a5_1.jpg)
	- Malé kaanceláře
	- 5x Gigabit
- [SXT Sixpack](https://mikrotik.com/product/RBSXTKit)
![SXT Sixpack](https://cdn10.bigcommerce.com/s-5db3f7/products/2373/images/1967/RBSXTKit_1__30485.1412800927.1280.1280.jpg)
	- Wireless
	- 5x 100mbit (OmniTik)
	- 5GHz 802.11a/n
	- Pokrytí širokého území
- [CCR1036-12G-4S](https://mikrotik.com/product/CCR1036-12G-4S-EM)
![Mikrotik CCR1036-12G-4S](https://www.wifihw.cz/attachstore/StoItem/_2/2662/AIR1271.jpg)
	- Flagship
	- 1U rack
	- 12x gigabit
	- Serial, USB, touchscreen
	- 4 - 16 GB RAM

#### Schéma názvů
- Názvy voleny na základě funkcí
	- CCR: Cloud Core Router
	- RB: Router Board
	- 2 / 5: WiFi pásma
	- H: Vysoký výkon
	- S: SFP
	- U: USB
	- i: PoE
	- G: Gigabit

#### Vlastní router - příklady
- Upravitelné CPE
- Modularita
- Box třetí strany
- SD karta

### Úvod do RouterOS
- Připojení přes WinBox
- V podstatě jen proklikávání položek v menu
- Interfaces, DHCP Client, DHCP Server, Pool...
- Safe Mode (rollbackne nastavení když něco přeruší management spojení)

## 2. Hodina 2020-10-02

### Konfigurace, upgrade, licence RouterOS

#### Konektivita
- Sériová linka
- SSH, telnet
- CLI
	- Skripty

#### Úvodní konfigurace
- Wan port s DHCP klientem
- Lan porty vč. WiFi jsou bridge
- DHCP server na LAN
- Základní Firewall
- NAT pro překlad LAN/WAN
- IP adresa pro LAN `192.168.88.0/24`

##### Alternativně žádná konfigurace
- V RouterOS nabídka System > Reset Configuration (No Default Configuration)

#### Upgrade firmware routeru
- Kdy upgradovat?
	- Oprava problému
	- Potřeba nové funkce
	- Zlepšení výkonu
- Číst changelog  

**Před upgradem**
- Zjistit architekturu (mipsbe)
- Kde získat balíčky pro upgrade
	- [Software downloads](https://mikrotik.com/download)  

**Manuální upgrade**
- Položka *Files*
- Po restartu se načte nová verze  

**Automatický upgrade**
- System > Packages  

**Automatický (distribuovaný) upgrade**
- Možnost použít router na místní síti jako zdroj pro upgrade

#### Upgrade bootloaderu RouterBOOT
- System > Routerboard (> Upgrade)
- Poté restartovat

#### Správa IP služeb
- System > IP Services
- Možnost omezení využívání sys. prostředků, zavřít porty

#### Typy záloh
- Binární záloha
	- Files > Backup
	- Obnovení zálohy doporučeno na identickém zařízení
- Export zálohy
	- Textová forma konfigurace

##### Archivace souborů se zálohami
- IP > Services povolit fileserver
- Kopírování přes FTP, SFTP

### Licence RouterOS
- Šest úrovní
	1. Demo (24 hodin)
	2. Free (velmi omezeno)
	3. WISP CPE (WiFi klient)
	4. WISP (WiFi access point)
	5. WISP (méně omezení)
	6. Controller (bez omezení)

#### Použití licencí
- Úroveň nelze měnit, je ideální použít vhodnou licenci od začátku
- Pozor při flashování úložiště, riziko ztráty licence

## 3. Hodina 2020-12-04

### Bezdrátové standardy