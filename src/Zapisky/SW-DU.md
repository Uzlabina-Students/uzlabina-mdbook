# Software (DU)

## 1. Hodina 2020-09-07

**Ukládání dat v počítači**

- Porovnávání číselných soustav
- Převody mezi číselnými soustavami
- Sčitání, odčítání, násobení a dělení ve dvojkové, osmičkové a šestnáctkové soustavě

## 2. Hodina 2020-09-14

### Datové typy, číselné soustavy

- ASCII (American Standard Code for Information Interchange)
	- Písmena anglické abecedy
	- Číslice
	- Jiné znaky - závorky, matematika...
	- Interpunkce
	- Speciální znaky (@, $, ~)
	- Řídicí netisknutelné znaky
	- 128 znaků, 32 řídicích znaků
		- Rozšíření na diakritiku, 256 znaků
- UNICODE
	- 16 bitů
- Soubor může být uložen
	- Jen s jedním kódováním
	- S více kodováními (špatně)

## 3. Hodina 2020-09-16 - Jednoduché datové typy
- Datový typ určuje
	- množinu přípustných dat
	- množinu přípustných operací
	- způsob uložení dat v počítači
- Jednoduché
	- Pouze 1 hodnota na proměnnou
- Strukturované
	- Několik hodnot na proměnnou

### Datové typy jednoduché
- Celá čísla
	- Kladná - byte, ushort, uint, ulong
	- Kladná/Záporná - sbyte, short, int, long
- Reálná čísla
	- S pevnou řádovou čárkou
	- S pohyblivou řádovou čárkou
- Znaky
- Bool (logické hodnoty)
- Enum (výčet)

|      | byte      |
|------|-----------|
| 0    | 0000 0000 |
| 1    | 0000 0001 |
| ...  | ...       |
| 255  | 1111 1111 |

|       | sbyte     |
|-------|-----------|
| -128  | 1000 0000 |
| -127  | 1000 0001 |
|   -1  | 1111 1111 |
|    0  | 0000 0000 |
|    1  | 0000 0001 |
|  127  | 0111 1111 |

- double 64b
- float 32b
- decimal 128b

- nepřesnost
	- (0,3)<sub>10</sub> = (0,10011001100110011...)<sub>2</sub>

| 0,3 | 2 |
|-----|---|
|   0 | 6 |
|   1 | 2 |
|   0 | 4 |
|   0 | 8 |
|   1 | 6 |
|   1 | 2 |

## 4. Hodina 2020-09-21

### [Komprimování textových souborů](http://uzlabina2.aspone.cz/kompresetextu.aspx)

- Vždy musí být bezztrátová
- Komprimovat lze jen soubory, kdy se data vyskytují s různou četností

#### Příklad 1
Biologové popisují geny jako posloupnosti složené ze 4 písmen
- A, T, G, C
- Kódujeme zprávu `A A A C A G T A A C`
	- 1. Vytvoříme kód - 2 binární číslice pro každý znak  

	| A | C | G | T | A A A C A G T A A C| AAACAGTAAC |
	|---|---|---|---|--------------------|------------|
	|00 |01 |10 | 11|00 00 00 01 00 11 10 00 00 01 |00000001001110000001|

	- 2. Využijeme skutečnosti, že se jednotlivé znaky vyskytují v posloupnosti s různou četností (znak A se vyskytuje 6x, znak C 2x, znaky G a T 1x). Vytvoříme nový kód  

	| A | C | G | T | A A A C A G T A A C| AAACAGTAAC|
	|---|---|---|---|--------------------|-----------|
	|0  |10 |110|111|0 0 0 10 0 110 111 0 0 10|0001001101110010|