<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "fab4e6b4f0efcd587a9029d82991f597",
  "translation_date": "2025-08-27T23:32:37+00:00",
  "source_file": "5-browser-extension/solution/README.md",
  "language_code": "sk"
}
-->
# Rozšírenie prehliadača Carbon Trigger: Hotový kód

Pomocou API C02 Signal od tmrow na sledovanie spotreby elektriny vytvorte rozšírenie prehliadača, aby ste mali priamo vo svojom prehliadači pripomienku o tom, aká náročná je spotreba elektriny vo vašom regióne. Používanie tohto rozšírenia ad hoc vám pomôže robiť rozhodnutia o svojich aktivitách na základe týchto informácií.

![screenshot rozšírenia](../../../../translated_images/extension-screenshot.0e7f5bfa110e92e3875e1bc9405edd45a3d2e02963e48900adb91926a62a5807.sk.png)

## Začíname

Budete potrebovať nainštalovaný [npm](https://npmjs.com). Stiahnite si kópiu tohto kódu do priečinka na svojom počítači.

Nainštalujte všetky potrebné balíčky:

```
npm install
```

Zostavte rozšírenie pomocou webpacku:

```
npm run build
```

Na inštaláciu v Edge použite menu s „tromi bodkami“ v pravom hornom rohu prehliadača na nájdenie panela Rozšírenia. Odtiaľ vyberte možnosť „Načítať nebalené“ na načítanie nového rozšírenia. Pri výzve otvorte priečinok „dist“ a rozšírenie sa načíta. Na jeho používanie budete potrebovať API kľúč pre API CO2 Signal ([získajte ho tu prostredníctvom e-mailu](https://www.co2signal.com/) - zadajte svoj e-mail do poľa na tejto stránke) a [kód pre váš región](http://api.electricitymap.org/v3/zones) zodpovedajúci [Electricity Map](https://www.electricitymap.org/map) (napríklad v Bostone používam 'US-NEISO').

![inštalácia](../../../../translated_images/install-on-edge.78634f02842c48283726c531998679a6f03a45556b2ee99d8ff231fe41446324.sk.png)

Keď zadáte API kľúč a región do rozhrania rozšírenia, farebná bodka na paneli rozšírenia prehliadača by sa mala zmeniť tak, aby odrážala spotrebu energie vo vašom regióne, a poskytne vám odporúčanie, aké energeticky náročné aktivity by boli vhodné vykonávať. Koncept tohto systému „bodiek“ mi bol inšpiráciou od [rozšírenia Energy Lollipop](https://energylollipop.com/) pre emisie v Kalifornii.

---

**Upozornenie**:  
Tento dokument bol preložený pomocou služby AI prekladu [Co-op Translator](https://github.com/Azure/co-op-translator). Aj keď sa snažíme o presnosť, prosím, berte na vedomie, že automatizované preklady môžu obsahovať chyby alebo nepresnosti. Pôvodný dokument v jeho rodnom jazyku by mal byť považovaný za autoritatívny zdroj. Pre kritické informácie sa odporúča profesionálny ľudský preklad. Nie sme zodpovední za akékoľvek nedorozumenia alebo nesprávne interpretácie vyplývajúce z použitia tohto prekladu.