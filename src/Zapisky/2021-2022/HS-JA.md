# Hardware a Sítě (Jakubec)

## 1. Hodina 2021-09-03

### Seznámení s plánem učiva

## 2. Hodina 2021-09-07

### Opakování 3. ročníku

* Je dobré mít dokumentaci sítě
	* Číslovací schéma IP adres
* Nastavení IP adres portů na routeru
`/home/czechball/packettracer/saves/hs-demo.pkt`

## 3. Hodina 2021-09-10

### OSPF (Open Shortest Path First)

#### Funkce a vlastnosti

* OSPFv2 se používá pro IPv4, OSPFv3 se používá pro IPv6
* OSPF vyhodnocuje nejrychlejší spoj v síti a optimalizuje provoz
* Jedná se o **link-state routing protokol**
* Alternativa zastaralého protokolu RIP
* Využití algoritmu SPF, SPF tree, vytvoření routovacích pravidel

#### OSPF Pakety

* Hello packets
* Database description packets
* Link-state request packets
* Link-state update packets
* Link-state acknowledgements packets

#### Data struktura

* Adjacency database (neighbor table)
* Link-state database (LSDB) - topology
* Forwarding database (routing table)

#### Link-State Operation

Pořadí akcí:

1. Navázání "Neighbor Adjacencies"
	* Detekce ostatních OSPF routerů
	* Odeslání *Hello* packetů
	* Navázání "sousednosti" (adjacency)
2. Výměna Link-State "Advertisements"
	* Výměna LSAs (link-state advertisements)
	* LSA obsahuje informace o "ceně" (cost) a stav linku
	* Routery "zaplavují" (flood) svoje LSAs sousedům
3. Sestavení tabulky (databáze) s Link-State informacemi
	* Po příjmu LSAs sestaví routery topology table
4. Spuštění SPF algoritmu
	* SPF vytvoří "SPF Tree"
5. Vybrání nejlepší cesty (routy)
	* Počítání ceny

#### Single a Multi Area OSPF

* Single-Area OSPF - všechny routery jsou v jedné oblasti, je dobré označit ji číslem 0
* Multi-Area OSPF - OSPF používá více oblastí, všechny musí být napojené na "backbone area". Routery které se tam napojují se jmenují Area Border Routers (ABRs)

## 4. Hodina 2021-09-14

### Typy OSPF paketů

|Typ|Název Paketu|Popis|
|---|---|---|
|1|Hello|Detekce sousedů a navázání "sousedství" (adjacency)|
|2|Database Description **(DBD)**|Konroluje synchronizaci databází mezi routery|
|3|Link-State Request **(LSR)**|Výměna specifických link-state informací mezi routery|
|4|Link-State Update **(LSU)**|Pošle specificky vyžádané link-state informace|
|5|Link-State Acknowledgment **(LSAck)**|Potvrzuje přijetí ostatních typů paketů|

* Typ 4 (LSU) může být odeslán bez vyžádání

#### Link-State Updates (LSU)

* Routery si na začátku pošlou pakety typu 2 (DBD), což je zkrácený seznam LSDB zdrojového routeru. Je to použito příjemcem ke kontole lokální LSDB
* Paket typu 3 (LSR) je používaný příjemcem k vyžádání více informací o záznamu v DBD
* Paket typu 4 (LSU) se používá jako odpověď na paket typu 3 (LSR)
* Paket typu 5 (LSack) se používá k potvrzení příjmu paketu typu 4 (LSU)

### Hello Packet

* Objevují sousedy a navazují adjacencies
* Propagují parametry na základě kterých se dva routery stanou sousedy
* Nastaví routery jako Designated Router **(DR)** a Backup Designated Router **(BDR)** v multiaccess sítích (Ethernet) (P2P nevyžaduje multiaccess)

## 5. Hodina 2021-10-01

### Konfigurace OSPF routerů
* Router ID - 32 bitová hodnota, zapsaná jako IPv4 adresa
* Pokud není přiřazena ručně, generuje se automaticky

Možnosti konfigurace OSPF ID
1. Router ID je explicitně nastavené pomocí router-id příkazu
2. Router ID není explicitně nastaveno, router použije nejvyšší IPv4 adresu jakéhokoliv loopback rozhraní
3. Pokud neexistují loopback zařízení, router si vybere nejvyšší IPv4 adresu jakéhokoliv fyzického rozhraní

## 6. Hodina 2021-10-05

### Maska sítě u OSPF ID

* Spočítání wildcard masky: `255.255.255.255 - subnet`
	* Např.: `255.255.255.255 - 255.255.255.192 (subnet /26 sítě) = 0.0.0.63 (wildcard maska)`

### Konfigurace sítě pro OSPF ID

Jsou dvě možnosti:

#### Použití příkazu *network*
```
R1(config)# router ospf 10
R1(config-router)# network 10.10.1.0 0.0.0.255 area 0
R1(config-router)# network 10.1.1.4 0.0.0.3 area 0
R1(config-router)# network 10.1.1.12 0.0.0.3 area 0
R1(config-router)#
```

#### Použití příkazu *ip ospf*
* Template
```
Router(config-if)# ip ospf process-id area area-id
```
* Příklad
```
R1(config)# router ospf 10
R1(config-router)# no network 10.10.1.1 0.0.0.0 area 0
R1(config-router)# no network 10.1.1.5 0.0.0.0 area 0
R1(config-router)# no network 10.1.1.14 0.0.0.0 area 0
R1(config-router)# interface GigabitEthernet 0/0/0
R1(config-if)# ip ospf 10 area 0
R1(config-if)# interface GigabitEthernet 0/0/1 
R1(config-if)# ip ospf 10 area 0
R1(config-if)# interface Loopback 0
R1(config-if)# ip ospf 10 area 0
R1(config-if)#
```
```
interface lo0		# přepnutí do rozhraní
ip ospf 10 area 0	# asociace rozhraní
interface g0/0/0
ip ospf 10 area 0
interface g0/0/1
ip ospf 10 area 0
```

### Pasivní rozhraní
* Není potřeba posílat OSPF pakety na všechna dostupná rozhraní, stačí je poslat pouze na rozhraní na OSPF routerech
* Nepřítomnost OSPF rozhraní může způsobit zbytečné rozesílání hello packetů
* Může způsobit:
	* Zahlcení sítě
	* Zahlcení zařízení
	* Bezpečnostní riziko - OSPF pakety mohou být zachyceny, upraveny a poslány zpět

#### Konfigurace pasivního rozhraní
* Příkaz `passive-interface` (konfigurační režim)
* Zabrání posílání routovacích zpráv na daném rozhraní, ale stále mu umožní propagaci ostatním routerům
* Příklad konfigurace R1 loopback 0/0/0 rozhraní jako pasivní
```
R1(config)# router ospf 10
R1(config-router)# passive-interface loopback 0
R1(config-router)# end
R1#
*May 23 20:24:39.309: %SYS-5-CONFIG_I: Configured from console by console
R1# show ip protocols
*** IP Routing is NSF aware ***
(output omitted)
Routing Protocol is "ospf 10"
  Outgoing update filter list for all interfaces is not set
  Incoming update filter list for all interfaces is not set
  Router ID 1.1.1.1
  Number of areas in this router is 1. 1 normal 0 stub 0 nssa
  Maximum path: 4
  Routing for Networks:
  Routing on Interfaces Configured Explicitly (Area 0):
    Loopback0
    GigabitEthernet0/0/1
    GigabitEthernet0/0/0
  Passive Interface(s):
    Loopback0
  Routing Information Sources:
    Gateway         Distance      Last Update
    3.3.3.3              110      01:01:48
    2.2.2.2              110      01:01:38
  Distance: (default is 110)
R1#
```