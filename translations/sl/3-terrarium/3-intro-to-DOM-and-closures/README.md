<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "30f8903a1f290e3d438dc2c70fe60259",
  "translation_date": "2025-08-28T00:05:36+00:00",
  "source_file": "3-terrarium/3-intro-to-DOM-and-closures/README.md",
  "language_code": "sl"
}
-->
# Projekt Terrarij, 3. del: Manipulacija DOM in zaprtje

![DOM in zaprtje](../../../../translated_images/webdev101-js.10280393044d7eaaec7e847574946add7ddae6be2b2194567d848b61d849334a.sl.png)
> Sketchnote avtorja [Tomomi Imura](https://twitter.com/girlie_mac)

## Predhodni kviz

[Predhodni kviz](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/19)

### Uvod

Manipulacija DOM, ali "Document Object Model", je ključen vidik spletnega razvoja. Po [MDN](https://developer.mozilla.org/docs/Web/API/Document_Object_Model/Introduction) je "Document Object Model (DOM) podatkovna predstavitev objektov, ki sestavljajo strukturo in vsebino dokumenta na spletu." Izzivi pri manipulaciji DOM na spletu so pogosto razlog za uporabo JavaScript ogrodij namesto čistega JavaScripta za upravljanje DOM, vendar bomo tokrat delali sami!

Poleg tega bo ta lekcija predstavila idejo [JavaScript zaprtja (closure)](https://developer.mozilla.org/docs/Web/JavaScript/Closures), ki si ga lahko predstavljate kot funkcijo, ki je zaprta znotraj druge funkcije, tako da ima notranja funkcija dostop do obsega zunanje funkcije.

> JavaScript zaprtja so obsežna in kompleksna tema. Ta lekcija se dotika osnovne ideje, da boste v kodi za ta terarij našli zaprtje: notranjo funkcijo in zunanjo funkcijo, ki sta zgrajeni tako, da omogočata notranji funkciji dostop do obsega zunanje funkcije. Za več informacij o tem, kako to deluje, obiščite [obsežno dokumentacijo](https://developer.mozilla.org/docs/Web/JavaScript/Closures).

Zaprtje bomo uporabili za manipulacijo DOM.

DOM si predstavljajte kot drevo, ki predstavlja vse načine, kako je mogoče manipulirati dokument spletne strani. Različni API-ji (Application Program Interfaces) so bili napisani, da lahko programerji s svojim programskim jezikom dostopajo do DOM in ga urejajo, spreminjajo, preurejajo in drugače upravljajo.

![Predstavitev DOM drevesa](../../../../translated_images/dom-tree.7daf0e763cbbba9273f9a66fe04c98276d7d23932309b195cb273a9cf1819b42.sl.png)

> Predstavitev DOM in HTML označbe, ki se nanj nanaša. Avtor: [Olfa Nasraoui](https://www.researchgate.net/publication/221417012_Profile-Based_Focused_Crawler_for_Social_Media-Sharing_Websites)

V tej lekciji bomo dokončali naš interaktivni projekt terarija z ustvarjanjem JavaScript kode, ki bo uporabniku omogočila manipulacijo rastlin na strani.

### Predpogoj

Imeti morate zgrajen HTML in CSS za vaš terarij. Do konca te lekcije boste lahko premikali rastline v in iz terarija z vlečenjem.

### Naloga

V mapi za vaš terarij ustvarite novo datoteko z imenom `script.js`. To datoteko uvozite v razdelek `<head>`:

```html
	<script src="./script.js" defer></script>
```

> Opomba: uporabite `defer` pri uvažanju zunanje JavaScript datoteke v HTML datoteko, da omogočite izvajanje JavaScripta šele po tem, ko je HTML datoteka popolnoma naložena. Lahko bi uporabili tudi atribut `async`, ki omogoča izvajanje skripte med analiziranjem HTML datoteke, vendar je v našem primeru pomembno, da so HTML elementi popolnoma na voljo za vlečenje, preden omogočimo izvajanje skripte za vlečenje.
---

## DOM elementi

Prva stvar, ki jo morate narediti, je ustvariti reference na elemente, ki jih želite manipulirati v DOM. V našem primeru je to 14 rastlin, ki trenutno čakajo v stranskih vrsticah.

### Naloga

```html
dragElement(document.getElementById('plant1'));
dragElement(document.getElementById('plant2'));
dragElement(document.getElementById('plant3'));
dragElement(document.getElementById('plant4'));
dragElement(document.getElementById('plant5'));
dragElement(document.getElementById('plant6'));
dragElement(document.getElementById('plant7'));
dragElement(document.getElementById('plant8'));
dragElement(document.getElementById('plant9'));
dragElement(document.getElementById('plant10'));
dragElement(document.getElementById('plant11'));
dragElement(document.getElementById('plant12'));
dragElement(document.getElementById('plant13'));
dragElement(document.getElementById('plant14'));
```

Kaj se tukaj dogaja? Sklicujete se na dokument in iščete po njegovem DOM, da najdete element z določenim Id-jem. Se spomnite iz prve lekcije o HTML, da ste vsakemu slikovnemu elementu rastline dodelili posamezen Id (`id="plant1"`)? Zdaj boste to delo uporabili. Ko identificirate vsak element, ta element posredujete funkciji `dragElement`, ki jo boste ustvarili čez trenutek. Tako bo element v HTML zdaj omogočen za vlečenje, ali pa bo kmalu.

✅ Zakaj se sklicujemo na elemente po Id-ju? Zakaj ne po njihovem CSS razredu? Morda se vrnite na prejšnjo lekcijo o CSS, da odgovorite na to vprašanje.

---

## Zaprtje

Zdaj ste pripravljeni ustvariti zaprtje `dragElement`, ki je zunanja funkcija, ki zapira notranjo funkcijo ali funkcije (v našem primeru bomo imeli tri).

Zaprtja so uporabna, ko ena ali več funkcij potrebuje dostop do obsega zunanje funkcije. Tukaj je primer:

```javascript
function displayCandy(){
	let candy = ['jellybeans'];
	function addCandy(candyType) {
		candy.push(candyType)
	}
	addCandy('gumdrops');
}
displayCandy();
console.log(candy)
```

V tem primeru funkcija `displayCandy` obdaja funkcijo, ki potisne nov tip sladkarije v že obstoječe polje v funkciji. Če bi zagnali to kodo, bi bilo polje `candy` nedoločeno, saj je lokalna spremenljivka (lokalna za zaprtje).

✅ Kako lahko naredite polje `candy` dostopno? Poskusite ga premakniti izven zaprtja. Na ta način bo polje postalo globalno, namesto da bi ostalo dostopno le v lokalnem obsegu zaprtja.

### Naloga

Pod deklaracijami elementov v `script.js` ustvarite funkcijo:

```javascript
function dragElement(terrariumElement) {
	//set 4 positions for positioning on the screen
	let pos1 = 0,
		pos2 = 0,
		pos3 = 0,
		pos4 = 0;
	terrariumElement.onpointerdown = pointerDrag;
}
```

`dragElement` dobi svoj objekt `terrariumElement` iz deklaracij na vrhu skripte. Nato nastavite nekaj lokalnih položajev na `0` za objekt, ki je posredovan funkciji. To so lokalne spremenljivke, ki bodo manipulirane za vsak element, ko dodate funkcionalnost vlečenja in spuščanja znotraj zaprtja za vsak element. Terrarij bo napolnjen s temi vlečenimi elementi, zato mora aplikacija slediti, kje so postavljeni.

Poleg tega je elementu `terrariumElement`, ki je posredovan tej funkciji, dodeljen dogodek `pointerdown`, ki je del [web API-jev](https://developer.mozilla.org/docs/Web/API), zasnovanih za pomoč pri upravljanju DOM. `onpointerdown` se sproži, ko je gumb pritisnjen, ali v našem primeru, ko je dotaknjen vlečljiv element. Ta obdelovalec dogodkov deluje tako na [spletnih kot mobilnih brskalnikih](https://caniuse.com/?search=onpointerdown), z nekaj izjemami.

✅ [Obdelovalec dogodkov `onclick`](https://developer.mozilla.org/docs/Web/API/GlobalEventHandlers/onclick) ima veliko večjo podporo med brskalniki; zakaj ga tukaj ne bi uporabili? Razmislite o točnem tipu interakcije zaslona, ki jo želite ustvariti.

---

## Funkcija Pointerdrag

Element `terrariumElement` je pripravljen za vlečenje; ko je dogodek `onpointerdown` sprožen, se pokliče funkcija `pointerDrag`. Dodajte to funkcijo takoj pod to vrstico: `terrariumElement.onpointerdown = pointerDrag;`:

### Naloga 

```javascript
function pointerDrag(e) {
	e.preventDefault();
	console.log(e);
	pos3 = e.clientX;
	pos4 = e.clientY;
}
```

Dogaja se več stvari. Najprej preprečite privzete dogodke, ki se običajno zgodijo ob `pointerdown`, z uporabo `e.preventDefault();`. Na ta način imate več nadzora nad vedenjem vmesnika.

> Vrnite se k tej vrstici, ko boste popolnoma zgradili datoteko skripte, in poskusite brez `e.preventDefault()` - kaj se zgodi?

Drugič, odprite `index.html` v oknu brskalnika in preglejte vmesnik. Ko kliknete rastlino, lahko vidite, kako je dogodek 'e' zajet. Raziščite dogodek, da vidite, koliko informacij je zbranih z enim dogodkom pointer down!  

Nato opazite, kako sta lokalni spremenljivki `pos3` in `pos4` nastavljeni na e.clientX. Te vrednosti zajamejo x in y koordinate rastline v trenutku, ko jo kliknete ali se je dotaknete. Potrebovali boste natančen nadzor nad vedenjem rastlin, ko jih kliknete in vlečete, zato sledite njihovim koordinatam.

✅ Ali postaja bolj jasno, zakaj je celotna aplikacija zgrajena z enim velikim zaprtjem? Če ne bi bila, kako bi ohranili obseg za vsako od 14 vlečljivih rastlin?

Dokončajte začetno funkcijo z dodajanjem dveh dodatnih manipulacij dogodkov pointer pod `pos4 = e.clientY`:

```html
document.onpointermove = elementDrag;
document.onpointerup = stopElementDrag;
```
Zdaj označujete, da želite, da se rastlina premika skupaj s kazalcem, ko ga premikate, in da se vlečenje ustavi, ko rastlino odznačite. `onpointermove` in `onpointerup` sta del istega API-ja kot `onpointerdown`. Vmesnik bo zdaj metalo napake, saj še niste definirali funkcij `elementDrag` in `stopElementDrag`, zato jih zgradite naslednje.

## Funkciji elementDrag in stopElementDrag

Zaprtje boste dokončali z dodajanjem dveh dodatnih notranjih funkcij, ki bodo upravljale, kaj se zgodi, ko vlečete rastlino in ko prenehate vleči. Želeno vedenje je, da lahko kadar koli vlečete katero koli rastlino in jo postavite kamor koli na zaslon. Ta vmesnik je precej neobremenjen (na primer ni območja za spuščanje), da vam omogoči oblikovanje terarija točno tako, kot želite, z dodajanjem, odstranjevanjem in prestavljanjem rastlin.

### Naloga

Dodajte funkcijo `elementDrag` takoj za zapiralno zavito oklepaj funkcije `pointerDrag`:

```javascript
function elementDrag(e) {
	pos1 = pos3 - e.clientX;
	pos2 = pos4 - e.clientY;
	pos3 = e.clientX;
	pos4 = e.clientY;
	console.log(pos1, pos2, pos3, pos4);
	terrariumElement.style.top = terrariumElement.offsetTop - pos2 + 'px';
	terrariumElement.style.left = terrariumElement.offsetLeft - pos1 + 'px';
}
```
V tej funkciji veliko urejate začetne položaje 1-4, ki ste jih nastavili kot lokalne spremenljivke v zunanji funkciji. Kaj se tukaj dogaja?

Med vlečenjem ponovno dodelite `pos1`, tako da ga nastavite na `pos3` (ki ste ga prej nastavili kot `e.clientX`) minus trenutno vrednost `e.clientX`. Podobno operacijo izvedete za `pos2`. Nato ponastavite `pos3` in `pos4` na nove X in Y koordinate elementa. Te spremembe lahko opazujete v konzoli med vlečenjem. Nato manipulirate s slogom css rastline, da nastavite njen nov položaj na podlagi novih položajev `pos1` in `pos2`, pri čemer izračunate zgornje in leve X in Y koordinate rastline na podlagi primerjave njenega odmika s temi novimi položaji.

> `offsetTop` in `offsetLeft` sta CSS lastnosti, ki nastavljata položaj elementa glede na njegov nadrejeni element; njegov nadrejeni element je lahko kateri koli element, ki ni pozicioniran kot `static`. 

Vse to ponovno izračunavanje položajev vam omogoča fino nastavitev vedenja terarija in njegovih rastlin.

### Naloga 

Zadnja naloga za dokončanje vmesnika je dodati funkcijo `stopElementDrag` za zapiralno zavito oklepaj funkcije `elementDrag`:

```javascript
function stopElementDrag() {
	document.onpointerup = null;
	document.onpointermove = null;
}
```

Ta majhna funkcija ponastavi dogodka `onpointerup` in `onpointermove`, tako da lahko znova začnete premikati rastlino ali začnete premikati novo rastlino.

✅ Kaj se zgodi, če teh dogodkov ne nastavite na null?

Zdaj ste dokončali svoj projekt!

🥇Čestitke! Dokončali ste svoj čudovit terarij. ![dokončan terarij](../../../../translated_images/terrarium-final.0920f16e87c13a84cd2b553a5af9a3ad1cffbd41fbf8ce715d9e9c43809a5e2c.sl.png)

---

## 🚀Izziv

Dodajte nov obdelovalec dogodkov v svoje zaprtje, da naredite nekaj več z rastlinami; na primer, z dvojnim klikom na rastlino jo premaknite v ospredje. Bodite ustvarjalni!

## Kviz po predavanju

[Kviz po predavanju](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/20)

## Pregled in samostojno učenje

Čeprav se zdi premikanje elementov po zaslonu trivialno, obstaja veliko načinov za to in veliko pasti, odvisno od učinka, ki ga želite doseči. Pravzaprav obstaja celoten [API za vlečenje in spuščanje](https://developer.mozilla.org/docs/Web/API/HTML_Drag_and_Drop_API), ki ga lahko preizkusite. Nismo ga uporabili v tem modulu, ker je bil učinek, ki smo ga želeli, nekoliko drugačen, vendar poskusite ta API na svojem projektu in preverite, kaj lahko dosežete.

Poiščite več informacij o dogodkih kazalca v [dokumentaciji W3C](https://www.w3.org/TR/pointerevents1/) in na [MDN spletni dokumentaciji](https://developer.mozilla.org/docs/Web/API/Pointer_events).

Vedno preverite zmogljivosti brskalnika z uporabo [CanIUse.com](https://caniuse.com/).

## Naloga

[Delajte še malo z DOM](assignment.md)

---

**Omejitev odgovornosti**:  
Ta dokument je bil preveden z uporabo storitve za prevajanje z umetno inteligenco [Co-op Translator](https://github.com/Azure/co-op-translator). Čeprav si prizadevamo za natančnost, vas prosimo, da upoštevate, da lahko avtomatizirani prevodi vsebujejo napake ali netočnosti. Izvirni dokument v njegovem maternem jeziku je treba obravnavati kot avtoritativni vir. Za ključne informacije priporočamo profesionalni človeški prevod. Ne prevzemamo odgovornosti za morebitna nesporazume ali napačne razlage, ki bi nastale zaradi uporabe tega prevoda.