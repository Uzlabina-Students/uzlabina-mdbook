# Hardware a sítě - cvičení (JA)

## 1. Hodina 2021-10-22

### Konfigurace OSPFv2

## 2. Hodina 2021-11-04

### Winbox, Netinstall, Licencování, dokumentace MikroTik

#### Komunikace s RouterBoard zařízením
* WinBox
	* MAC adresa - používá ethernetové rámce
	* IP Adresa
* Konzolový port
* SSH

#### Úvodní komunikace
* System > Reset Configuration
* *No Default Configuration*

#### Miminální default konfigurace
* LAN IP adresa, gateway, DNS
* WAN IP adresa, gateway, DNS
* FW, NAT
* SNTP (čas)

#### Upgrade
* Nahrání npk souborů, automatický upgrade
* Upgrade bootloaderu
	* System > RouterBOARD > Current Firmware/Upgrade Firmware (tlačítko Upgrade)

#### Správa IP služeb
* 80 http, 443 https, 8291 winbox

#### Zálohy
* File List, Backup
* Soubory .backup, automatické vytváření názvu souboru

#### Úrovně RouterOS Licence
* Šest úrovní

|Úroveň|Typ|Omezení|
|---|---|---|
|0|Demo|24 hodin|
|1|Free|Velmi omezeno|
|3|WISP CPE|WiFi klient|
|4|WISP|pro Access Point|
|5|WISP|méně omezení|
|6|Controller|bez omezení|

* Zjištění licence: System > Licence
* Licence uložena ve flash paměti, při použití externích nástrojů na úpravu paměti hrozí ztráta licence
* Více info o licencích se dá nalézt v [MikroTik dokumentaci](https://help.mikrotik.com/docs/display/ROS/RouterOS+license+keys)
* Úroveň licence nelze měnit v provozu

#### NetInstall
* Přeinstalace RouterOS v případě problémů s přístupem do rozhraní zařízení RouterBoard
* [Stažení na stránkách MikroTik](https://mikrotik.com/download)

## 22. Hodina 2022-02-25

### Protokoly CDP, LLDP, NTP (Cisco IOS)

## 23. Hodina 2022-03-31

### RouterOS QoS

#### [Queues](https://wiki.mikrotik.com/wiki/Manual:Queue)

Queue (fronty) - kolekce data paketů, které čekají na přenesení po síti. Fungují podobně jako např. fronty v supermarketech nebo bankách, kde je zákazník (paket) obsloužen v momentě, kdy přijde na řadu.

##### Využití

* Omezení rychlosti pro konkrétní IP adresy, subnety, protokoly, porty...
* Omezení P2P provozu
* Priorita paketů
* Nastavení výkyvů provozu pro zrychlení sítě
* Nastavení časovaných limitů
* Sdílení dostupné šířky sítě rovnoměrně mezi uživateli, nebo na základě zatížení kanálu

#### Rate Limiting

**Dva způsoby**:  
1. **Zahození** paketů které přesahují limit
2. **Zpoždění** paketů které přesahují limit

![Principles of rate limiting and equalizing](https://help.mikrotik.com/docs/download/attachments/328088/Image8001.png)

##### Druhy

* Simple Queue
	* `/queue simple`
	* Jednoduchý způsob omezení provozu
	* Možnost použití simple queues pro vytvoření pokročilých QoS
	* Užitečné built-in funkce
		* Omezení P2P provozu
		* Nastavení pravidel podle času
		* Prioritizace
		* "Tvarovaní" provozu nebo bidirekcionální omezení
* Queue Tree
* Queue Typy
	* FIFO
		* First In, First Out
	* RED
		* Random Early Drop
	* SFQ
		* Stochastic Fairness Queuing (hasing, round-robin)
	* PCQ
		* Využívání jednolivých FIFO po zvolení označení
	* CoDel
	* FQ-Codel
	* CAKE
* Interface Queue