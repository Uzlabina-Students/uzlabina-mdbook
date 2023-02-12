# Hardware a sítě - Cvičení (MU)

## 1. Hodina 2020-09-09

Práce na síťovém hardwaru

### Kopírování aktuální konfigurace zařízení přes TFTP

- Zkopírování konfigurace jako soubor na server
```
copy running-config tftp
[ip adresa tftp serveru]
[název souboru]
```
- Zkopírování souboru ze serveru jako konfigurace do zařízení
```
copy tftp running-config
[ip adresa tftp serveru]
[název souboru]
```