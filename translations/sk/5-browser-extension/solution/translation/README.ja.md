<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "3f5e6821e0febccfc5d05e7c944d9e3d",
  "translation_date": "2025-08-27T23:34:05+00:00",
  "source_file": "5-browser-extension/solution/translation/README.ja.md",
  "language_code": "sk"
}
-->
# Rozšírenie prehliadača Carbon Trigger: Hotový kód

Vytvorte rozšírenie prehliadača, ktoré pomocou API CO2 Signal od tmrow sleduje spotrebu elektrickej energie vo vašej oblasti a zobrazuje pripomienku o tom, aká vysoká je spotreba energie vo vašom regióne. Toto rozšírenie môžete používať ad hoc na základe tejto informácie, aby ste mohli lepšie rozhodovať o svojich aktivitách.

![screenshot rozšírenia](../../../../../translated_images/extension-screenshot.0e7f5bfa110e92e3875e1bc9405edd45a3d2e02963e48900adb91926a62a5807.sk.png)

## Začíname

Musíte mať nainštalovaný [npm](https://npmjs.com). Stiahnite si kópiu tohto projektu do priečinka na vašom počítači.

Nainštalujte všetky potrebné balíčky.

```
npm install
```

Vytvorte rozšírenie pomocou webpacku.

```
npm run build
```

Ak chcete rozšírenie nainštalovať do Edge, otvorte panel „Rozšírenia“ cez menu „tri bodky“ v pravom hornom rohu prehliadača. Tam vyberte možnosť „Load Unpacked“ a načítajte nové rozšírenie. Keď sa zobrazí výzva, otvorte priečinok „dist“ a rozšírenie sa načíta. Na používanie budete potrebovať API kľúč CO2 Signal ([získajte ho tu cez email](https://www.co2signal.com/) - zadajte svoj email do políčka na stránke) a [kód pre váš región](http://api.electricitymap.org/v3/zones) zodpovedajúci [Electricity Map](https://www.electricitymap.org/map) (napríklad pre Boston použite 'US-NEISO').

![inštalácia](../../../../../translated_images/install-on-edge.78634f02842c48283726c531998679a6f03a45556b2ee99d8ff231fe41446324.sk.png)

Po zadaní API kľúča a regiónu do rozhrania rozšírenia sa farba bodky, ktorá sa zobrazí na lište rozšírení prehliadača, zmení. Táto bodka odráža energetickú spotrebu vo vašej oblasti a naznačuje, aké aktivity vyžadujúce energiu sú vhodné vykonávať. Koncept systému „bodky“ mi bol inšpiráciou od rozšírenia [Energy Lollipop](https://energylollipop.com/) pre emisie v Kalifornii.

---

**Upozornenie**:  
Tento dokument bol preložený pomocou služby AI prekladu [Co-op Translator](https://github.com/Azure/co-op-translator). Aj keď sa snažíme o presnosť, prosím, berte na vedomie, že automatizované preklady môžu obsahovať chyby alebo nepresnosti. Pôvodný dokument v jeho rodnom jazyku by mal byť považovaný za autoritatívny zdroj. Pre kritické informácie sa odporúča profesionálny ľudský preklad. Nenesieme zodpovednosť za akékoľvek nedorozumenia alebo nesprávne interpretácie vyplývajúce z použitia tohto prekladu.