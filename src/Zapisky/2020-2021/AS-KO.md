# Aplikační Software (KO)

## 1. Hodina 2020-09-14

### Makra v programu Microsoft Excel
- Soubor, Možnosti, Přizpůsobit pás karet, zaškrtnout "Vývojář"
__
- Makro s vložením textu na právě aktivní buňku
```vbnet
Sub NazevMakra()

ActiveCell.FormulaR1C1 = "text v bunce"

End Sub
```  
- Makro co obarví momentálně zvolené buňky
```vbnet
Sub NazevMakra()

Selection.Interior.Color = RGB(255, 255, 128)

End Sub
```  
- Makro co kopíruje momentálně vybranou buňku do buňky X9
```vbnet
Sub NazevMakra()

Selection.Copy
Range("X9").Select
ActiveSheet.Paste
Application.CutCopyMode = False

End Sub
```  
- Makro co kopíruje z buňky A1 do buňky X9
```vbnet
Sub NazevMakra()

    Range("A1").Copy
    Range("X9").Select
    ActiveSheet.Paste

End Sub
```  
- Násobení velikosti textu vybrané buňky 2
```vbnet
Sub NazevMakra()

Selection.Font.Size = Selection.Font.Size * 2
Selection.Font.Bold = True

End Sub
```