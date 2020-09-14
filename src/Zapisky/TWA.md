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