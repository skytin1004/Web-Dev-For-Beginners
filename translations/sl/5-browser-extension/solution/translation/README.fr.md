<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "9361268ca430b2579375009e1eceb5e5",
  "translation_date": "2025-08-27T23:35:51+00:00",
  "source_file": "5-browser-extension/solution/translation/README.fr.md",
  "language_code": "sl"
}
-->
# Razširitev brskalnika Carbon Trigger: Končana koda

Z uporabo API-ja C02 Signal podjetja tmrow za spremljanje porabe električne energije ustvarite razširitev brskalnika, ki vam omogoča, da imate neposreden opomnik v brskalniku o porabi električne energije v vaši regiji. Uporaba te razširitve vam bo pomagala sprejemati odločitve o vaših dejavnostih na podlagi teh informacij.

![posnetek razširitve](../../../../../translated_images/extension-screenshot.0e7f5bfa110e92e3875e1bc9405edd45a3d2e02963e48900adb91926a62a5807.sl.png)

## Začetek

Imeti morate nameščen [npm](https://npmjs.com). Prenesite kopijo te kode v mapo na vašem računalniku.

Namestite vse potrebne pakete:

```
npm install
```

Razširitev zgradite z uporabo webpacka:

```
npm run build
```

Za namestitev na Edge uporabite meni 'tri pike' v zgornjem desnem kotu brskalnika, da odprete ploščo Razširitve. Tam izberite 'Naloži razširitev v nekompresirani obliki', da naložite novo razširitev. Na poziv odprite mapo 'dist' in razširitev se bo naložila. Za uporabo boste potrebovali API ključ za API CO2 Signal ([pridobite ga tukaj po e-pošti](https://www.co2signal.com/) - vnesite svoj e-poštni naslov v polje na tej strani) ter [kodo za vašo regijo](http://api.electricitymap.org/v3/zones), ki ustreza [Zemljevidu električne energije](https://www.electricitymap.org/map) (na primer v Bostonu uporabljam 'US-NEISO').

![namestitev](../../../../../translated_images/install-on-edge.78634f02842c48283726c531998679a6f03a45556b2ee99d8ff231fe41446324.sl.png)

Ko vmesnik razširitve vnesete API ključ in regijo, se mora barvna pika v vrstici razširitev brskalnika spremeniti, da odraža porabo energije v vaši regiji, ter vam dati indikator za energijsko intenzivne dejavnosti, ki bi jih bilo primerno izvajati. Koncept za ta sistem 'pik' mi je bil navdihnjen z [razširitvijo Energy Lollipop](https://energylollipop.com/) za emisije v Kaliforniji.

---

**Omejitev odgovornosti**:  
Ta dokument je bil preveden z uporabo storitve za prevajanje z umetno inteligenco [Co-op Translator](https://github.com/Azure/co-op-translator). Čeprav si prizadevamo za natančnost, vas prosimo, da upoštevate, da lahko avtomatizirani prevodi vsebujejo napake ali netočnosti. Izvirni dokument v njegovem maternem jeziku je treba obravnavati kot avtoritativni vir. Za ključne informacije priporočamo profesionalni človeški prevod. Ne prevzemamo odgovornosti za morebitna nesporazumevanja ali napačne razlage, ki bi nastale zaradi uporabe tega prevoda.