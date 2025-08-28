<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "bf62b82567e6f9bdf4abda9ae0ccb64a",
  "translation_date": "2025-08-27T23:53:12+00:00",
  "source_file": "2-js-basics/3-making-decisions/assignment.md",
  "language_code": "sk"
}
-->
# Operátory

## Pokyny

Vyskúšajte operátory. Tu je návrh programu, ktorý môžete implementovať:

Máte skupinu študentov z dvoch rôznych hodnotiacich systémov.

### Prvý hodnotiaci systém

Jeden hodnotiaci systém je definovaný známkami od 1 do 5, pričom známka 3 a vyššie znamená, že študent úspešne absolvoval kurz.

### Druhý hodnotiaci systém

Druhý hodnotiaci systém má nasledujúce známky: `A, A-, B, B-, C, C-`, pričom `A` je najlepšia známka a `C` je najnižšia známka, ktorá znamená úspešné absolvovanie.

### Úloha

Na základe nasledujúceho poľa `allStudents`, ktoré reprezentuje všetkých študentov a ich známky, vytvorte nové pole `studentsWhoPass`, ktoré bude obsahovať všetkých študentov, ktorí úspešne absolvovali.

> TIP: Použite for-cyklus, if...else a porovnávacie operátory:

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

## Hodnotiace kritériá

| Kritérium | Vynikajúce                    | Dostatočné                   | Vyžaduje zlepšenie             |
| --------- | ----------------------------- | ---------------------------- | ------------------------------ |
|           | Predložené kompletné riešenie | Predložené čiastočné riešenie | Predložené riešenie s chybami |

---

**Upozornenie**:  
Tento dokument bol preložený pomocou služby AI prekladu [Co-op Translator](https://github.com/Azure/co-op-translator). Hoci sa snažíme o presnosť, prosím, berte na vedomie, že automatizované preklady môžu obsahovať chyby alebo nepresnosti. Pôvodný dokument v jeho rodnom jazyku by mal byť považovaný za autoritatívny zdroj. Pre kritické informácie sa odporúča profesionálny ľudský preklad. Nie sme zodpovední za akékoľvek nedorozumenia alebo nesprávne interpretácie vyplývajúce z použitia tohto prekladu.