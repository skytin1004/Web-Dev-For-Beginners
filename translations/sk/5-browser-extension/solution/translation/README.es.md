<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "cbaf73f94a9ab4c680a10ef871e92948",
  "translation_date": "2025-08-27T23:34:33+00:00",
  "source_file": "5-browser-extension/solution/translation/README.es.md",
  "language_code": "sk"
}
-->
# Rozšírenie prehliadača Carbon Trigger: Kompletný kód

Pomocou API CO2 Signal od tmrow na sledovanie spotreby elektriny vytvorte rozšírenie prehliadača, ktoré vám priamo v prehliadači pripomenie spotrebu elektriny vo vašom regióne. Používanie tohto rozšírenia vám pomôže robiť rozhodnutia o vašich aktivitách na základe týchto informácií.

![screenshot rozšírenia](../../../../../translated_images/extension-screenshot.352c4c3ba54e4041ad2f6af749d562cc5705f527b5826efd53d11c3528f5ae45.sk.png)

## Začíname

Musíte mať nainštalovaný [npm](https://npmjs.com). Stiahnite si kópiu tohto kódu do priečinka vo vašom počítači.

Nainštalujte všetky potrebné balíčky:

```
npm install
```

Vytvorte rozšírenie pomocou webpacku:

```
npm run build
```

Na inštaláciu v Edge použite menu „tri bodky“ v pravom hornom rohu prehliadača na vyhľadanie panela Rozšírenia. Odtiaľ vyberte „Načítať rozbalené“ na načítanie nového rozšírenia. Keď sa zobrazí výzva, otvorte priečinok „dist“ a rozšírenie sa načíta. Na jeho používanie budete potrebovať API kľúč pre API CO2 Signal ([získajte ho tu e-mailom](https://www.co2signal.com/) - zadajte svoj e-mail do políčka na tejto stránke) a [kód pre váš región](http://api.electricitymap.org/v3/zones) zodpovedajúci [Elektrickej mape](https://www.electricitymap.org/map) (napríklad v Bostone používam 'US-NEISO').

![inštalácia](../../../../../translated_images/install-on-edge.8bd0ee3ca7dcda1c5334b5195603a43c864e3b38d088b03d57376d25e77b9459.sk.png)

Keď zadáte API kľúč a región do rozhrania rozšírenia, farebný bod na paneli rozšírenia prehliadača by sa mal zmeniť tak, aby odrážal spotrebu energie vo vašom regióne a poskytol vám indikátor o aktivitách s vysokou spotrebou energie, ktoré by pre vás boli vhodné. Koncept za týmto systémom „bodov“ mi poskytlo [rozšírenie Energy Lollipop](https://energylollipop.com/) pre emisie v Kalifornii.

---

**Upozornenie**:  
Tento dokument bol preložený pomocou služby na automatický preklad [Co-op Translator](https://github.com/Azure/co-op-translator). Hoci sa snažíme o presnosť, upozorňujeme, že automatické preklady môžu obsahovať chyby alebo nepresnosti. Pôvodný dokument v jeho pôvodnom jazyku by mal byť považovaný za záväzný zdroj. Pre dôležité informácie odporúčame profesionálny ľudský preklad. Nezodpovedáme za akékoľvek nedorozumenia alebo nesprávne interpretácie vyplývajúce z použitia tohto prekladu.