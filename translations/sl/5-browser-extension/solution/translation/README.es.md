<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "cbaf73f94a9ab4c680a10ef871e92948",
  "translation_date": "2025-08-27T23:34:52+00:00",
  "source_file": "5-browser-extension/solution/translation/README.es.md",
  "language_code": "sl"
}
-->
# Razširitev brskalnika Carbon Trigger: Celotna koda

Z uporabo API-ja CO2 Signal podjetja tmrow za sledenje porabi električne energije ustvarite razširitev za brskalnik, ki vam bo omogočila, da imate neposreden opomnik o porabi električne energije v vaši regiji. Uporaba te prilagojene razširitve vam bo pomagala sprejemati odločitve o vaših dejavnostih na podlagi teh informacij.

![posnetek zaslona razširitve](../../../../../translated_images/extension-screenshot.352c4c3ba54e4041ad2f6af749d562cc5705f527b5826efd53d11c3528f5ae45.sl.png)

## Začetek

Imeti morate nameščen [npm](https://npmjs.com). Prenesite kopijo te kode v mapo na svojem računalniku.

Namestite vse potrebne pakete:

```
npm install
```

Sestavite razširitev z uporabo webpack:

```
npm run build
```

Za namestitev v Edge uporabite meni s 'tremi pikami' v zgornjem desnem kotu brskalnika, da odprete ploščo Razširitve. Tam izberite 'Naloži razpakirano', da naložite novo razširitev. Ko vas sistem pozove, odprite mapo 'dist' in razširitev bo naložena. Za uporabo boste potrebovali API ključ za CO2 Signal API ([pridobite ga tukaj po e-pošti](https://www.co2signal.com/) - vnesite svoj e-poštni naslov v polje na tej strani) in [kodo za vašo regijo](http://api.electricitymap.org/v3/zones), ki ustreza [zemljevidu električne energije](https://www.electricitymap.org/map) (na primer v Bostonu uporabljam 'US-NEISO').

![nameščanje](../../../../../translated_images/install-on-edge.8bd0ee3ca7dcda1c5334b5195603a43c864e3b38d088b03d57376d25e77b9459.sl.png)

Ko vmesnik razširitve vnesete API ključ in regijo, bi se morala barvna pika v orodni vrstici brskalnika spremeniti, da odraža porabo energije v vaši regiji, in vam dati indikator o dejavnostih z visoko porabo energije, ki bi bile primerne za vas. Koncept tega sistema "pik" sem dobil pri [razširitvi Energy Lollipop](https://energylollipop.com/) za emisije v Kaliforniji.

---

**Omejitev odgovornosti**:  
Ta dokument je bil preveden z uporabo storitve za prevajanje z umetno inteligenco [Co-op Translator](https://github.com/Azure/co-op-translator). Čeprav si prizadevamo za natančnost, vas prosimo, da upoštevate, da lahko avtomatizirani prevodi vsebujejo napake ali netočnosti. Izvirni dokument v njegovem maternem jeziku je treba obravnavati kot avtoritativni vir. Za ključne informacije priporočamo profesionalni človeški prevod. Ne prevzemamo odgovornosti za morebitna nesporazumevanja ali napačne razlage, ki bi nastale zaradi uporabe tega prevoda.