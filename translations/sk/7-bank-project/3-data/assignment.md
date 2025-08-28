<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "a4abf305ede1cfaadd56a8fab4b4c288",
  "translation_date": "2025-08-27T23:16:01+00:00",
  "source_file": "7-bank-project/3-data/assignment.md",
  "language_code": "sk"
}
-->
# Refaktorujte a komentujte svoj kód

## Pokyny

Ako vaša kódová základňa rastie, je dôležité pravidelne refaktorovať kód, aby bol čitateľný a udržiavateľný v priebehu času. Pridajte komentáre a refaktorujte váš `app.js`, aby ste zlepšili kvalitu kódu:

- Extrahujte konštanty, ako napríklad základnú URL adresu serverového API
- Zoskupte podobný kód: napríklad môžete vytvoriť funkciu `sendRequest()`, ktorá zjednotí kód použitý v `createAccount()` a `getAccount()`
- Preorganizujte kód, aby bol ľahšie čitateľný, a pridajte komentáre

## Hodnotiace kritériá

| Kritérium | Vynikajúce                                                                                                                                                   | Dostatočné                                                                                       | Vyžaduje zlepšenie                                                                    |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------- |
|           | Kód je okomentovaný, dobre organizovaný do rôznych sekcií a ľahko čitateľný. Konštanty sú extrahované a vytvorená je zjednotená funkcia `sendRequest()`.       | Kód je čistý, ale stále by mohol byť zlepšený pridaním ďalších komentárov, extrakciou konštánt alebo zjednotením.                  | Kód je chaotický, neokomentovaný, konštanty nie sú extrahované a kód nie je zjednotený. |

---

**Upozornenie**:  
Tento dokument bol preložený pomocou služby AI prekladu [Co-op Translator](https://github.com/Azure/co-op-translator). Hoci sa snažíme o presnosť, prosím, berte na vedomie, že automatizované preklady môžu obsahovať chyby alebo nepresnosti. Pôvodný dokument v jeho rodnom jazyku by mal byť považovaný za autoritatívny zdroj. Pre kritické informácie sa odporúča profesionálny ľudský preklad. Nie sme zodpovední za akékoľvek nedorozumenia alebo nesprávne interpretácie vyplývajúce z použitia tohto prekladu.