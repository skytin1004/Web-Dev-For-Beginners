<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "dd58ae1b7707034f055718c1b68bc8de",
  "translation_date": "2025-08-27T23:33:25+00:00",
  "source_file": "5-browser-extension/solution/translation/README.hi.md",
  "language_code": "sl"
}
-->
# Carbon Trigger Brskalni dodatek: Končna koda

Uporaba tmrow API-ja C02 Signal za sledenje porabi električne energije, izdelava brskalnega dodatka, ki vas opomni, kako obremenjena je poraba električne energije v vašem območju. Uporaba tega dodatka vam bo pomagala sprejemati odločitve glede vaših aktivnosti na podlagi teh informacij.

![Posnetek zaslona dodatka](../../../../../translated_images/extension-screenshot.0e7f5bfa110e92e3875e1bc9405edd45a3d2e02963e48900adb91926a62a5807.sl.png)

## Začetek

Namestiti morate [npm](https://npmjs.com). Prenesite kopijo te kode v mapo na vašem računalniku.

Namestite vse potrebne pakete:

```
npm install
```

Ustvarite dodatek z uporabo Webpacka:

```
npm run build
```

Za namestitev v Edge uporabite meni 'tri pike' v zgornjem desnem kotu brskalnika, da poiščete ploščo za dodatke. Od tam izberite 'Naloži nepakiran' za nalaganje novega dodatka. Na poziv odprite mapo 'dist' in dodatek bo naložen. Za uporabo potrebujete API ključ CO2 Signal ([pridobite ga tukaj preko e-pošte](https://www.co2snal.com/) - vnesite svoj e-poštni naslov v polje na tej strani) in [kodo za vaše območje](http://api.electricitymap.org/v3/zones) [električni zemljevid](https://www.electricitymap.org/map) (na primer, v Bostonu uporabljam 'US-NEISO').

![nameščanje](../../../../../translated_images/install-on-edge.78634f02842c48283726c531998679a6f03a45556b2ee99d8ff231fe41446324.sl.png)

Ko vmesnik dodatka vnesete API ključ in območje, bi se morala barvna pika v vrstici brskalnega dodatka spremeniti, da odraža porabo energije v vašem območju, ter vam dati indikator, katere energijsko intenzivne aktivnosti so primerne za vaše delovanje. Koncept za to 'pikčasto' sistem mi je bil navdihnjen z [Energy Lollipop dodatkom](https://energylollipop.com/) za emisije v Kaliforniji.

---

**Omejitev odgovornosti**:  
Ta dokument je bil preveden z uporabo storitve za prevajanje z umetno inteligenco [Co-op Translator](https://github.com/Azure/co-op-translator). Čeprav si prizadevamo za natančnost, vas prosimo, da upoštevate, da lahko avtomatizirani prevodi vsebujejo napake ali netočnosti. Izvirni dokument v njegovem izvirnem jeziku je treba obravnavati kot avtoritativni vir. Za ključne informacije priporočamo profesionalni človeški prevod. Ne prevzemamo odgovornosti za morebitna nesporazumevanja ali napačne razlage, ki bi nastale zaradi uporabe tega prevoda.