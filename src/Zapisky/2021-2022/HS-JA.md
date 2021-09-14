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