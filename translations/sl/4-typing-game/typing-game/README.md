<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "e982871b8388c59c22a41b73b5fca70f",
  "translation_date": "2025-08-28T00:12:21+00:00",
  "source_file": "4-typing-game/typing-game/README.md",
  "language_code": "sl"
}
-->
# Ustvarjanje igre z uporabo dogodkov

## Predhodni kviz

[Predhodni kviz](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/21)

## Programiranje, ki temelji na dogodkih

Pri ustvarjanju aplikacije za brskalnik uporabniku omogočimo grafični uporabniški vmesnik (GUI), ki ga uporablja za interakcijo z našim izdelkom. Najpogostejši način interakcije z brskalnikom je prek klikanja in tipkanja v različnih elementih. Izziv, s katerim se soočamo kot razvijalci, je, da ne vemo, kdaj bo uporabnik izvedel te operacije!

[Programiranje, ki temelji na dogodkih](https://en.wikipedia.org/wiki/Event-driven_programming) je ime za vrsto programiranja, ki ga potrebujemo za ustvarjanje našega GUI-ja. Če to frazo nekoliko razčlenimo, vidimo, da je ključna beseda tukaj **dogodek**. [Dogodek](https://www.merriam-webster.com/dictionary/event), po definiciji Merriam-Webster, pomeni "nekaj, kar se zgodi". To popolnoma opisuje našo situacijo. Vemo, da se bo nekaj zgodilo, za kar želimo izvesti kodo kot odziv, vendar ne vemo, kdaj se bo to zgodilo.

Način, kako označimo del kode, ki ga želimo izvesti, je z ustvarjanjem funkcije. Ko razmišljamo o [proceduralnem programiranju](https://en.wikipedia.org/wiki/Procedural_programming), se funkcije kličejo v določenem vrstnem redu. Enako velja za programiranje, ki temelji na dogodkih. Razlika je v tem, **kako** se funkcije kličejo.

Za obravnavo dogodkov (klikanje gumbov, tipkanje itd.) registriramo **poslušalce dogodkov**. Poslušalec dogodkov je funkcija, ki posluša, da se zgodi dogodek, in se nato izvede kot odziv. Poslušalci dogodkov lahko posodobijo uporabniški vmesnik, opravijo klice na strežnik ali karkoli drugega, kar je potrebno kot odziv na uporabnikovo dejanje. Poslušalca dogodkov dodamo z uporabo [addEventListener](https://developer.mozilla.org/docs/Web/API/EventTarget/addEventListener) in podajanjem funkcije za izvedbo.

> **NOTE:** Pomembno je poudariti, da obstaja veliko načinov za ustvarjanje poslušalcev dogodkov. Uporabite lahko anonimne funkcije ali ustvarite poimenovane. Uporabite lahko različne bližnjice, kot je nastavitev lastnosti `click` ali uporaba `addEventListener`. V naši vaji se bomo osredotočili na `addEventListener` in anonimne funkcije, saj je to verjetno najpogostejša tehnika, ki jo uporabljajo spletni razvijalci. Prav tako je najbolj prilagodljiva, saj `addEventListener` deluje za vse dogodke, ime dogodka pa je mogoče podati kot parameter.

### Pogosti dogodki

Na voljo je [na desetine dogodkov](https://developer.mozilla.org/docs/Web/Events), ki jih lahko poslušate pri ustvarjanju aplikacije. V bistvu vse, kar uporabnik naredi na strani, sproži dogodek, kar vam daje veliko moč, da zagotovite želeno izkušnjo. Na srečo boste običajno potrebovali le nekaj dogodkov. Tukaj je nekaj pogostih (vključno z dvema, ki ju bomo uporabili pri ustvarjanju naše igre):

- [click](https://developer.mozilla.org/docs/Web/API/Element/click_event): Uporabnik je kliknil nekaj, običajno gumb ali hiperpovezavo
- [contextmenu](https://developer.mozilla.org/docs/Web/API/Element/contextmenu_event): Uporabnik je kliknil desni gumb miške
- [select](https://developer.mozilla.org/docs/Web/API/Element/select_event): Uporabnik je označil nekaj besedila
- [input](https://developer.mozilla.org/docs/Web/API/Element/input_event): Uporabnik je vnesel nekaj besedila

## Ustvarjanje igre

Ustvarili bomo igro, da raziščemo, kako dogodki delujejo v JavaScriptu. Naša igra bo preizkusila tipkarske spretnosti igralca, kar je ena najbolj podcenjenih spretnosti, ki bi jih moral imeti vsak razvijalec. Vsi bi morali vaditi tipkanje! Splošni potek igre bo videti takole:

- Igralec klikne gumb za začetek in mu je prikazan citat za tipkanje
- Igralec čim hitreje vtipka citat v besedilno polje
  - Ko je vsaka beseda dokončana, je naslednja označena
  - Če ima igralec tipkarsko napako, se besedilno polje obarva rdeče
  - Ko igralec dokonča citat, se prikaže sporočilo o uspehu z izmerjenim časom

Zgradimo igro in se naučimo o dogodkih!

### Struktura datotek

Potrebovali bomo tri datoteke: **index.html**, **script.js** in **style.css**. Začnimo z nastavitvijo teh datotek, da si olajšamo delo.

- Ustvarite novo mapo za svoje delo tako, da odprete konzolo ali terminal in izvedete naslednji ukaz:

```bash
# Linux or macOS
mkdir typing-game && cd typing-game

# Windows
md typing-game && cd typing-game
```

- Odprite Visual Studio Code

```bash
code .
```

- Dodajte tri datoteke v mapo v Visual Studio Code z naslednjimi imeni:
  - index.html
  - script.js
  - style.css

## Ustvarite uporabniški vmesnik

Če preučimo zahteve, vemo, da bomo na naši HTML strani potrebovali nekaj elementov. To je podobno receptu, kjer potrebujemo nekaj sestavin:

- Prostor za prikaz citata, ki ga mora uporabnik vtipkati
- Prostor za prikaz sporočil, kot je sporočilo o uspehu
- Besedilno polje za tipkanje
- Gumb za začetek

Vsak od teh elementov bo potreboval ID-je, da bomo lahko z njimi delali v našem JavaScriptu. Dodali bomo tudi reference na datoteke CSS in JavaScript, ki jih bomo ustvarili.

Ustvarite novo datoteko z imenom **index.html**. Dodajte naslednji HTML:

```html
<!-- inside index.html -->
<html>
<head>
  <title>Typing game</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <h1>Typing game!</h1>
  <p>Practice your typing skills with a quote from Sherlock Holmes. Click **start** to begin!</p>
  <p id="quote"></p> <!-- This will display our quote -->
  <p id="message"></p> <!-- This will display any status messages -->
  <div>
    <input type="text" aria-label="current word" id="typed-value" /> <!-- The textbox for typing -->
    <button type="button" id="start">Start</button> <!-- To start the game -->
  </div>
  <script src="script.js"></script>
</body>
</html>
```

### Zagon aplikacije

Vedno je najbolje razvijati iterativno, da vidimo, kako stvari izgledajo. Zaženimo našo aplikacijo. Obstaja čudovita razširitev za Visual Studio Code, imenovana [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer&WT.mc_id=academic-77807-sagibbon), ki bo gostila vašo aplikacijo lokalno in osvežila brskalnik vsakič, ko shranite.

- Namestite [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer&WT.mc_id=academic-77807-sagibbon) tako, da sledite povezavi in kliknete **Install**
  - Brskalnik vas bo pozval, da odprete Visual Studio Code, nato pa vas bo Visual Studio Code pozval, da izvedete namestitev
  - Po potrebi znova zaženite Visual Studio Code
- Ko je nameščen, v Visual Studio Code pritisnite Ctrl-Shift-P (ali Cmd-Shift-P), da odprete paleto ukazov
- Vnesite **Live Server: Open with Live Server**
  - Live Server bo začel gostiti vašo aplikacijo
- Odprite brskalnik in pojdite na **https://localhost:5500**
- Zdaj bi morali videti stran, ki ste jo ustvarili!

Dodajmo nekaj funkcionalnosti.

## Dodajte CSS

Ko smo ustvarili naš HTML, dodajmo CSS za osnovno oblikovanje. Označiti moramo besedo, ki jo mora igralec vtipkati, in obarvati besedilno polje, če je vneseno besedilo napačno. To bomo storili z dvema razredoma.

Ustvarite novo datoteko z imenom **style.css** in dodajte naslednjo sintakso.

```css
/* inside style.css */
.highlight {
  background-color: yellow;
}

.error {
  background-color: lightcoral;
  border: red;
}
```

✅ Pri CSS-ju lahko svojo stran oblikujete, kakor želite. Vzemite si nekaj časa in naredite stran bolj privlačno:

- Izberite drugačno pisavo
- Obarvajte naslove
- Spremenite velikost elementov

## JavaScript

Ko smo ustvarili uporabniški vmesnik, se osredotočimo na JavaScript, ki bo zagotovil logiko. Razdelili bomo to na nekaj korakov:

- [Ustvarite konstante](../../../../4-typing-game/typing-game)
- [Poslušalec dogodkov za začetek igre](../../../../4-typing-game/typing-game)
- [Poslušalec dogodkov za tipkanje](../../../../4-typing-game/typing-game)

Najprej pa ustvarite novo datoteko z imenom **script.js**.

### Dodajte konstante

Potrebovali bomo nekaj elementov, da si olajšamo programiranje. Spet, podobno kot recept, tukaj je, kaj bomo potrebovali:

- Tabelo s seznamom vseh citatov
- Prazno tabelo za shranjevanje vseh besed trenutnega citata
- Prostor za shranjevanje indeksa besede, ki jo igralec trenutno tipka
- Čas, ko je igralec kliknil začetek

Prav tako bomo želeli reference na elemente uporabniškega vmesnika:

- Besedilno polje (**typed-value**)
- Prikaz citata (**quote**)
- Sporočilo (**message**)

```javascript
// inside script.js
// all of our quotes
const quotes = [
    'When you have eliminated the impossible, whatever remains, however improbable, must be the truth.',
    'There is nothing more deceptive than an obvious fact.',
    'I ought to know by this time that when a fact appears to be opposed to a long train of deductions it invariably proves to be capable of bearing some other interpretation.',
    'I never make exceptions. An exception disproves the rule.',
    'What one man can invent another can discover.',
    'Nothing clears up a case so much as stating it to another person.',
    'Education never ends, Watson. It is a series of lessons, with the greatest for the last.',
];
// store the list of words and the index of the word the player is currently typing
let words = [];
let wordIndex = 0;
// the starting time
let startTime = Date.now();
// page elements
const quoteElement = document.getElementById('quote');
const messageElement = document.getElementById('message');
const typedValueElement = document.getElementById('typed-value');
```

✅ Dodajte več citatov v svojo igro

> **NOTE:** Elemente lahko kadar koli pridobimo v kodi z uporabo `document.getElementById`. Ker bomo te elemente redno uporabljali, se bomo izognili tipkarskim napakam z uporabo konstant. Okviri, kot sta [Vue.js](https://vuejs.org/) ali [React](https://reactjs.org/), vam lahko pomagajo bolje upravljati centralizacijo vaše kode.

Vzemite si minuto in si oglejte video o uporabi `const`, `let` in `var`.

[![Vrste spremenljivk](https://img.youtube.com/vi/JNIXfGiDWM8/0.jpg)](https://youtube.com/watch?v=JNIXfGiDWM8 "Vrste spremenljivk")

> 🎥 Kliknite zgornjo sliko za video o spremenljivkah.

### Dodajte logiko za začetek

Za začetek igre bo igralec kliknil na začetek. Seveda ne vemo, kdaj bo kliknil na začetek. Tukaj pride v poštev [poslušalec dogodkov](https://developer.mozilla.org/docs/Web/API/EventTarget/addEventListener). Poslušalec dogodkov nam omogoča poslušanje, da se nekaj zgodi (dogodek), in izvedbo kode kot odziv. V našem primeru želimo izvesti kodo, ko uporabnik klikne na začetek.

Ko uporabnik klikne **start**, moramo izbrati citat, nastaviti uporabniški vmesnik in nastaviti sledenje trenutni besedi ter čas. Spodaj je JavaScript, ki ga morate dodati; razložimo ga takoj po bloku kode.

```javascript
// at the end of script.js
document.getElementById('start').addEventListener('click', () => {
  // get a quote
  const quoteIndex = Math.floor(Math.random() * quotes.length);
  const quote = quotes[quoteIndex];
  // Put the quote into an array of words
  words = quote.split(' ');
  // reset the word index for tracking
  wordIndex = 0;

  // UI updates
  // Create an array of span elements so we can set a class
  const spanWords = words.map(function(word) { return `<span>${word} </span>`});
  // Convert into string and set as innerHTML on quote display
  quoteElement.innerHTML = spanWords.join('');
  // Highlight the first word
  quoteElement.childNodes[0].className = 'highlight';
  // Clear any prior messages
  messageElement.innerText = '';

  // Setup the textbox
  // Clear the textbox
  typedValueElement.value = '';
  // set focus
  typedValueElement.focus();
  // set the event handler

  // Start the timer
  startTime = new Date().getTime();
});
```

Razčlenimo kodo!

- Nastavitev sledenja besedam
  - Z uporabo [Math.floor](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Math/floor) in [Math.random](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Math/random) naključno izberemo citat iz tabele `quotes`
  - `quote` pretvorimo v tabelo `words`, da lahko sledimo besedi, ki jo igralec trenutno tipka
  - `wordIndex` nastavimo na 0, saj bo igralec začel z prvo besedo
- Nastavitev uporabniškega vmesnika
  - Ustvarimo tabelo `spanWords`, ki vsebuje vsako besedo znotraj elementa `span`
    - To nam omogoča označevanje besede na prikazu
  - Tabelo `join` pretvorimo v niz, ki ga lahko uporabimo za posodobitev `innerHTML` na `quoteElement`
    - To bo prikazalo citat igralcu
  - Nastavimo `className` prvega elementa `span` na `highlight`, da ga označimo kot rumenega
  - Očistimo `messageElement` tako, da nastavimo `innerText` na `''`
- Nastavitev besedilnega polja
  - Počistimo trenutno `value` na `typedValueElement`
  - Nastavimo `focus` na `typedValueElement`
- Začnemo časovnik z uporabo `getTime`

### Dodajte logiko za tipkanje

Ko igralec tipka, se sproži dogodek `input`. Ta poslušalec dogodkov bo preveril, ali igralec pravilno tipka besedo, in obravnaval trenutni status igre. Vrnite se v **script.js** in na konec dodajte naslednjo kodo. Razčlenili jo bomo takoj zatem.

```javascript
// at the end of script.js
typedValueElement.addEventListener('input', () => {
  // Get the current word
  const currentWord = words[wordIndex];
  // get the current value
  const typedValue = typedValueElement.value;

  if (typedValue === currentWord && wordIndex === words.length - 1) {
    // end of sentence
    // Display success
    const elapsedTime = new Date().getTime() - startTime;
    const message = `CONGRATULATIONS! You finished in ${elapsedTime / 1000} seconds.`;
    messageElement.innerText = message;
  } else if (typedValue.endsWith(' ') && typedValue.trim() === currentWord) {
    // end of word
    // clear the typedValueElement for the new word
    typedValueElement.value = '';
    // move to the next word
    wordIndex++;
    // reset the class name for all elements in quote
    for (const wordElement of quoteElement.childNodes) {
      wordElement.className = '';
    }
    // highlight the new word
    quoteElement.childNodes[wordIndex].className = 'highlight';
  } else if (currentWord.startsWith(typedValue)) {
    // currently correct
    // highlight the next word
    typedValueElement.className = '';
  } else {
    // error state
    typedValueElement.className = 'error';
  }
});
```

Razčlenimo kodo! Začnemo z zajemom trenutne besede in vrednosti, ki jo je igralec doslej vnesel. Nato imamo logiko, kjer preverimo, ali je citat dokončan, beseda dokončana, beseda pravilna ali (končno), ali je prišlo do napake.

- Citat je dokončan, kar je označeno z `typedValue`, ki je enak `currentWord`, in `wordIndex`, ki je enak enemu manj kot `length` tabele `words`
  - Izračunamo `elapsedTime` tako, da od trenutnega časa odštejemo `startTime`
  - `elapsedTime` delimo z 1.000, da ga pretvorimo iz milisekund v sekunde
  - Prikažemo sporočilo o uspehu
- Beseda je dokončana, kar je označeno z `typedValue`, ki se konča s presledkom (konec besede) in `typedValue`, ki je enak `currentWord`
  - Nastavimo `value` na `typedElement` na `''`, da omogočimo tipkanje naslednje besede
  - Povečamo `wordIndex`, da preidemo na naslednjo besedo
  - Prehodimo vse `childNodes` elementa `quoteElement`, da nastavimo `className` na `''`, da se vrnemo na privzeti prikaz
  - Nastavimo `className` trenutne besede na `highlight`, da jo označimo kot naslednjo besedo za tipkanje
- Beseda je trenutno pravilno vtipkana (vendar ne dokončana), kar je označeno z `currentWord`, ki se začne z `typedValue`
  - Poskrbimo, da je `typedValueElement` prikazan kot privzet tako, da počistimo `className`
- Če smo prišli do sem, imamo napako
  - Nastavimo `className` na `typedValueElement` na `error`

## Preizkusite svojo aplikacijo

Prišli ste do konca! Zadnji korak je, da zagotovite, da vaša aplikacija deluje. Preizkusite jo! Ne skrbite, če so napake; **vsi razvijalci** imajo napake. Preučite sporočila in odpravljajte težave po potrebi.

Kliknite na **start** in začnite tipkati! Videti bi moralo približno tako kot animacija, ki smo jo videli prej.

![Animacija igre v akciji](../../../../4-typing-game/images/demo.gif)

---

## 🚀 Izziv

Dodajte več funkcionalnosti

- Onemogočite poslušalca dogodkov `input` ob zaključku in ga znova omogočite, ko je gumb kliknjen
- Onemogočite besedilno polje, ko igralec dokonča citat
- Prikažite modalno pogovorno okno s sporočilom o uspehu
- Shranite najvišje rezultate z uporabo [localStorage](https://developer.mozilla.org/docs/Web/API/Window/localStorage)

## Kviz po predavanju

[Kviz po predavanju](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/22)

## Pregled in samostojno učenje

Preberite več o [vseh dogodkih, ki so na voljo](https://developer.mozilla.org/docs/Web/Events) razvijalcem prek spletnega brskalnika, in razmislite o scenarijih, v katerih bi uporabili posameznega.

## Naloga

[Ustvarite novo igro s tipkovnico](assignment.md)

---

**Omejitev odgovornosti**:  
Ta dokument je bil preveden z uporabo storitve AI za prevajanje [Co-op Translator](https://github.com/Azure/co-op-translator). Čeprav si prizadevamo za natančnost, vas prosimo, da upoštevate, da lahko avtomatizirani prevodi vsebujejo napake ali netočnosti. Izvirni dokument v njegovem izvirnem jeziku je treba obravnavati kot avtoritativni vir. Za ključne informacije priporočamo profesionalni človeški prevod. Ne prevzemamo odgovornosti za morebitna nesporazumevanja ali napačne razlage, ki bi nastale zaradi uporabe tega prevoda.