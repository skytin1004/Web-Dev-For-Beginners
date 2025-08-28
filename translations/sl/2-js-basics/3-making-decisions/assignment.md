<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "bf62b82567e6f9bdf4abda9ae0ccb64a",
  "translation_date": "2025-08-27T23:53:28+00:00",
  "source_file": "2-js-basics/3-making-decisions/assignment.md",
  "language_code": "sl"
}
-->
# Operatorji

## Navodila

Preizkusite operaterje. Tukaj je predlog za program, ki ga lahko implementirate:

Imate skupino študentov iz dveh različnih ocenjevalnih sistemov.

### Prvi ocenjevalni sistem

En ocenjevalni sistem določa ocene od 1 do 5, pri čemer ocena 3 ali več pomeni, da študent opravi predmet.

### Drugi ocenjevalni sistem

Drugi ocenjevalni sistem ima naslednje ocene: `A, A-, B, B-, C, C-`, pri čemer je `A` najvišja ocena, `C` pa najnižja ocena, ki še pomeni opravljen predmet.

### Naloga

Glede na naslednjo tabelo `allStudents`, ki predstavlja vse študente in njihove ocene, sestavite novo tabelo `studentsWhoPass`, ki vsebuje vse študente, ki so opravili predmet.

> TIP: uporabite for-zanko, if...else in primerjalne operaterje:

```javascript
let allStudents = [
  'A',
  'B-',
  1,
  4,
  5,
  2
]

let studentsWhoPass = [];
```

## Merila

| Merilo   | Odlično                        | Zadostno                      | Potrebna izboljšava             |
| -------- | ------------------------------ | ----------------------------- | ------------------------------- |
|          | Predstavljena je popolna rešitev | Predstavljena je delna rešitev | Predstavljena je rešitev z napakami |

---

**Omejitev odgovornosti**:  
Ta dokument je bil preveden z uporabo storitve za strojno prevajanje [Co-op Translator](https://github.com/Azure/co-op-translator). Čeprav si prizadevamo za natančnost, vas prosimo, da upoštevate, da lahko avtomatizirani prevodi vsebujejo napake ali netočnosti. Izvirni dokument v njegovem izvirnem jeziku je treba obravnavati kot avtoritativni vir. Za ključne informacije priporočamo strokovno človeško prevajanje. Ne prevzemamo odgovornosti za morebitna nesporazumevanja ali napačne razlage, ki izhajajo iz uporabe tega prevoda.