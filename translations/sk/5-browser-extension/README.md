<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "b121a279a6ab39878491f3e572673515",
  "translation_date": "2025-08-27T23:26:28+00:00",
  "source_file": "5-browser-extension/README.md",
  "language_code": "sk"
}
-->
# Vytváranie rozšírenia pre prehliadač

Vytváranie rozšírení pre prehliadače je zábavný a zaujímavý spôsob, ako premýšľať o výkonnosti vašich aplikácií pri vytváraní iného typu webového aktíva. Tento modul obsahuje lekcie o tom, ako fungujú prehliadače, ako nasadiť rozšírenie pre prehliadač, ako vytvoriť formulár, volať API, používať lokálne úložisko, a ako hodnotiť výkonnosť vašej webovej stránky a zlepšiť ju.

Vytvoríte rozšírenie pre prehliadač, ktoré funguje na Edge, Chrome a Firefox. Toto rozšírenie, ktoré je ako mini webová stránka prispôsobená veľmi špecifickej úlohe, kontroluje [C02 Signal API](https://www.co2signal.com) pre elektrickú spotrebu a uhlíkovú intenzitu danej oblasti a poskytuje údaje o uhlíkovej stope regiónu.

Toto rozšírenie môže byť používateľom volané ad hoc po zadaní API kľúča a kódu regiónu do formulára, aby sa určila lokálna elektrická spotreba a tým poskytli údaje, ktoré môžu ovplyvniť rozhodnutia používateľa o elektrickej energii. Napríklad môže byť vhodné odložiť používanie sušičky na oblečenie (činnosť s vysokou uhlíkovou intenzitou) počas obdobia vysokej elektrickej spotreby vo vašom regióne.

### Témy

1. [O prehliadači](1-about-browsers/README.md)
2. [Formuláre a lokálne úložisko](2-forms-browsers-local-storage/README.md)
3. [Pozadie úloh a výkonnosť](3-background-tasks-and-performance/README.md)

### Kredity

![zelené rozšírenie prehliadača](../../../translated_images/extension-screenshot.0e7f5bfa110e92e3875e1bc9405edd45a3d2e02963e48900adb91926a62a5807.sk.png)

## Kredity

Myšlienku pre tento webový uhlíkový spúšťač ponúkol Asim Hussain, vedúci tímu Green Cloud Advocacy v Microsoft a autor [Green Principles](https://principles.green/). Pôvodne to bol [projekt webovej stránky](https://github.com/jlooper/green).

Štruktúra rozšírenia pre prehliadač bola ovplyvnená [Adebola Adeniranovým COVID rozšírením](https://github.com/onedebos/covtension).

Koncept systému ikon „bodiek“ bol inšpirovaný štruktúrou ikon rozšírenia prehliadača [Energy Lollipop](https://energylollipop.com/) pre emisie v Kalifornii.

Tieto lekcie boli napísané s ♥️ od [Jen Looper](https://www.twitter.com/jenlooper)

---

**Upozornenie**:  
Tento dokument bol preložený pomocou služby AI prekladu [Co-op Translator](https://github.com/Azure/co-op-translator). Aj keď sa snažíme o presnosť, prosím, berte na vedomie, že automatizované preklady môžu obsahovať chyby alebo nepresnosti. Pôvodný dokument v jeho pôvodnom jazyku by mal byť považovaný za autoritatívny zdroj. Pre kritické informácie sa odporúča profesionálny ľudský preklad. Nie sme zodpovední za akékoľvek nedorozumenia alebo nesprávne interpretácie vyplývajúce z použitia tohto prekladu.