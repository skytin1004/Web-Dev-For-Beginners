<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "9a6b22a2eff0f499b66236be973b24ad",
  "translation_date": "2025-08-27T23:33:54+00:00",
  "source_file": "5-browser-extension/solution/translation/README.it.md",
  "language_code": "sl"
}
-->
# Razširitev brskalnika Carbon Trigger: koda za začetek

Uporabili bomo API Signal CO2 podjetja tmrow za spremljanje porabe električne energije, da ustvarimo razširitev za brskalnik, ki bo omogočala neposreden opomnik v brskalniku o tem, kako obremenjujoča je poraba električne energije v vaši regiji. Uporaba te prilagojene razširitve bo pomagala oceniti vaše dejavnosti na podlagi teh informacij.

![posnetek zaslona razširitve](../../../../../translated_images/extension-screenshot.0e7f5bfa110e92e3875e1bc9405edd45a3d2e02963e48900adb91926a62a5807.sl.png)

## Začetek

Potrebno je imeti nameščen [npm](https://npmjs.com). Prenesite kopijo te kode v mapo na svojem računalniku.

Namestite vse potrebne pakete:

```
npm install
```

Ustvarite razširitev z uporabo webpack:

```
npm run build
```

Za namestitev na Edge uporabite meni s "tremi pikami" v zgornjem desnem kotu brskalnika, da odprete ploščo Razširitve. Če še ni omogočen, omogočite Način razvijalca (v spodnjem levem kotu). Izberite "Naloži razpakirano", da naložite novo razširitev. Na pozivu odprite mapo "dist" in razširitev bo naložena. Za uporabo boste potrebovali API ključ za API CO2 Signal (lahko ga [pridobite tukaj preko e-pošte](https://www.co2signal.com/) - vnesite svoj e-poštni naslov v polje na tej strani) in [kodo za svojo regijo](http://api.electricitymap.org/v3/zones), ki ustreza [električni karti](https://www.electricitymap.org/map) (na primer za Boston "US-NEISO").

![namestitev](../../../../../translated_images/install-on-edge.78634f02842c48283726c531998679a6f03a45556b2ee99d8ff231fe41446324.sl.png)

Ko vmesnik razširitve vsebuje API ključ in regijo, bi se morala barvna pika v orodni vrstici razširitve brskalnika spremeniti, da odraža porabo energije v regiji, ter ponuditi namige o tem, katere dejavnosti z visoko porabo energije bi bile primerne za izvedbo. Koncept tega sistema "točk" je bil navdihnjen z [razširitvijo Energy Lollipop](https://energylollipop.com/) za emisije v Kaliforniji.

---

**Omejitev odgovornosti**:  
Ta dokument je bil preveden z uporabo storitve za prevajanje z umetno inteligenco [Co-op Translator](https://github.com/Azure/co-op-translator). Čeprav si prizadevamo za natančnost, vas prosimo, da upoštevate, da lahko avtomatizirani prevodi vsebujejo napake ali netočnosti. Izvirni dokument v njegovem izvirnem jeziku je treba obravnavati kot avtoritativni vir. Za ključne informacije priporočamo profesionalni človeški prevod. Ne prevzemamo odgovornosti za morebitna nesporazumevanja ali napačne razlage, ki bi nastale zaradi uporabe tega prevoda.