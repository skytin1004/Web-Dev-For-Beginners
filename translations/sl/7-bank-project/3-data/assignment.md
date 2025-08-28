<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "a4abf305ede1cfaadd56a8fab4b4c288",
  "translation_date": "2025-08-27T23:16:15+00:00",
  "source_file": "7-bank-project/3-data/assignment.md",
  "language_code": "sl"
}
-->
# Refaktorirajte in komentirajte svojo kodo

## Navodila

Ko vaša baza kode raste, je pomembno, da kodo pogosto refaktorirate, da ostane berljiva in vzdrževana skozi čas. Dodajte komentarje in refaktorirajte svoj `app.js`, da izboljšate kakovost kode:

- Izločite konstante, kot je osnovni URL strežniškega API-ja
- Poenotite podobno kodo: na primer, lahko ustvarite funkcijo `sendRequest()`, da združite kodo, uporabljeno v `createAccount()` in `getAccount()`
- Preuredite kodo, da bo bolj berljiva, in dodajte komentarje

## Merila

| Merila   | Odlično                                                                                                                                                       | Zadostno                                                                                         | Potrebno izboljšanje                                                                  |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------- |
|          | Koda je komentirana, dobro organizirana v različnih razdelkih in enostavna za branje. Konstante so izločene, ustvarjena je poenotena funkcija `sendRequest()`. | Koda je čista, vendar jo je mogoče izboljšati z več komentarji, izločanjem konstant ali poenotenjem. | Koda je neurejena, ni komentirana, konstante niso izločene in koda ni poenotena.      |

---

**Omejitev odgovornosti**:  
Ta dokument je bil preveden z uporabo storitve za prevajanje z umetno inteligenco [Co-op Translator](https://github.com/Azure/co-op-translator). Čeprav si prizadevamo za natančnost, vas prosimo, da upoštevate, da lahko avtomatizirani prevodi vsebujejo napake ali netočnosti. Izvirni dokument v njegovem izvirnem jeziku je treba obravnavati kot avtoritativni vir. Za ključne informacije priporočamo profesionalni človeški prevod. Ne prevzemamo odgovornosti za morebitne nesporazume ali napačne razlage, ki bi nastale zaradi uporabe tega prevoda.