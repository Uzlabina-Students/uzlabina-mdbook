# Tvorba Webových Aplikací
 	
## 1. Hodina 2020-03-09

- Informace o projektech
- Vytváření statické stránky "Registrační značka vozidla"
- Začali jsme probírat JavaScript

### Základy JS

- Formát JS v HTML
```html
<script type="text/javascript">
</script>
```  
- JS se buďto vloží přímo do HTML nebo se includne jako samostatný .js soubor
- Print v JS
```js
document.write("Hello World");
```  
- Proměnné
```js
var a;		// Deklarování proměnné a
var b = 40;	// Deklarování proměnné b, která obsahuje číslo 40
c = 30;		// Deklarování proměnné c, která obsahuje číslo 30
```  
- Sčítání proměnných
```js
a = 1;
b = 2;
c = a + b;
document.write(c); // Vypíše se 3

d = "1";
e = "2";
f = d + e;
document.write(f); // Vypíše se 12
```  
- Vypsání aktuálního datumu
```js
a = new Date();
document.write(a.getDate); // Vypíše aktuální den v měsíci
```

## 2. Hodina 2020-09-10

- Přičítání hodnot přímo v `document.write`
```js
document.write(". " + ((d.getMonth()) + 1));
```  
- Ořezávání mezer (whitespace) pomocí trim
```js
var s = "    Bruh Moment    ";
s=s.trim();
document.write(s);	// Vypíše se "Bruh Moment"
```  
- Nahrazování stringů pomocí replace
```js
var str = "Umíme PHP";
var b = str.replace("PHP", "JS");
document.write(b);
```  
- Zjištění jestli je string číslo
```js
necislo= "Mario";
if (isNaN(necislo))
{
	document.write(necislo + " není číslo");
} else
{
	document.write(necislo + " je čislo");
}
```  
- Matematika - Pi
```js
var pi = Math.PI;
document.write(pi);
```  
- Mocniny
```js
document.write(Math.pow(2, 3));
```  
- If else statement
```js
d = new Date();

if ((d.getHours() > 7) && (d.getHours() < 20))
{
		document.write("<br> Dobrý den");
}
else
{
		document.write("<br> Dobrý věčěr");
}
```  
- Switch
```js
var veta = "";
switch (d.getHours())
{
	case 0:
	case 1:
	case 2:
	case 3:
	case 4:
		veta = "Dobrý večer";
		break;
	case 5:
	case 6:
	case 7:
	case 8:
	case 9:
	case 10:
		veta = "Dobré ráno";
		break;
	case 11:
	case 12:
	case 13:
	case 14:
		veta = "Dobré dopoledne";
		break;
	case 15:
	case 16:
	case 17:
	case 18:
		veta = "Dobré odpoledne";
		break;
	case 19:
	case 20:
	case 21:
	case 22:
	case 23:
		veta = "Dobrý večer";
	break;
	default:
		veta = "Zdravím";
}
document.write(veta);
```  
- Cykly
```js
for (var i = 1; i < 100; i++) {
	document.write(i+", ");
} // Bude přičítat do 100
```

## 2. Hodina 2020-09-xx

### Regex v JS a HTML5, validace vstupu formulářů

## 3. Hodina 2020-10-01

### DOM struktura, funkce, časování, hledání tagů

- Hledání ID
```js
document.getElementById('id sem');
```

- Intervaly
```js
window.setInterval(funkce, milisekundy);
```
	- Uložení intervalu do proměnné
```js
promenna = window.setInterval(xx, yy);
```
	- Zastavení intervalu po kliknutí na ID
```js
document.getElementById("id sem").onclick = function() { window.clearInterval(casovac); }
```
	- Zastavení intervalu po změně obsahu stránky
```js

```