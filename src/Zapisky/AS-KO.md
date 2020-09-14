# Aplikační Software (KO)

## 1. Hodina 2020-09-14

### Makra v programu Microsoft Excel
- Soubor, Možnosti, Přizpůsobit pás karet, zaškrtnout "Vývojář"
__
- Makro s vložením textu na právě aktivní buňku
```
Sub NazevMakra()

ActiveCell.FormulaR1C1 = "text v bunce"

End Sub
```  
- Makro co obarví momentálně zvolené buňky
```
Sub NazevMakra()
Selection.Interior.Color = RGB(255, 255, 128)
End Sub
```