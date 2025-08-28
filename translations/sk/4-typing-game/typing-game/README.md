<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "e982871b8388c59c22a41b73b5fca70f",
  "translation_date": "2025-08-28T00:10:59+00:00",
  "source_file": "4-typing-game/typing-game/README.md",
  "language_code": "sk"
}
-->
# Vytvorenie hry pomocou udalostí

## Kvíz pred prednáškou

[Kvíz pred prednáškou](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/21)

## Programovanie riadené udalosťami

Pri vytváraní aplikácie prehliadača poskytujeme grafické používateľské rozhranie (GUI), ktoré používateľ využíva na interakciu s tým, čo sme vytvorili. Najbežnejší spôsob interakcie s prehliadačom je kliknutie a písanie do rôznych prvkov. Výzvou, ktorej čelíme ako vývojári, je, že nevieme, kedy tieto operácie vykonajú!

[Programovanie riadené udalosťami](https://en.wikipedia.org/wiki/Event-driven_programming) je názov pre typ programovania, ktorý potrebujeme na vytvorenie nášho GUI. Ak rozložíme tento výraz, vidíme, že kľúčové slovo je **udalosť**. [Udalosť](https://www.merriam-webster.com/dictionary/event), podľa Merriam-Webster, je definovaná ako "niečo, čo sa stane". To dokonale opisuje našu situáciu. Vieme, že sa niečo stane, na čo chceme reagovať vykonaním kódu, ale nevieme, kedy sa to stane.

Spôsob, akým označíme časť kódu, ktorú chceme vykonať, je vytvorenie funkcie. Pri [procedurálnom programovaní](https://en.wikipedia.org/wiki/Procedural_programming) sa funkcie volajú v konkrétnom poradí. To isté platí aj pre programovanie riadené udalosťami. Rozdiel je v tom, **ako** sa funkcie volajú.

Na spracovanie udalostí (kliknutie na tlačidlo, písanie atď.) registrujeme **poslucháčov udalostí**. Poslucháč udalostí je funkcia, ktorá čaká na udalosť a vykoná sa ako reakcia. Poslucháči udalostí môžu aktualizovať používateľské rozhranie, vykonávať volania na server alebo čokoľvek iné, čo je potrebné urobiť ako reakcia na akciu používateľa. Poslucháča udalostí pridáme pomocou [addEventListener](https://developer.mozilla.org/docs/Web/API/EventTarget/addEventListener) a poskytneme funkciu na vykonanie.

> **NOTE:** Stojí za zmienku, že existuje mnoho spôsobov, ako vytvoriť poslucháčov udalostí. Môžete použiť anonymné funkcie alebo vytvoriť pomenované. Môžete použiť rôzne skratky, ako nastavenie vlastnosti `click` alebo použitie `addEventListener`. V našom cvičení sa zameriame na `addEventListener` a anonymné funkcie, pretože je to pravdepodobne najbežnejšia technika, ktorú používajú weboví vývojári. Je tiež najflexibilnejšia, pretože `addEventListener` funguje pre všetky udalosti a názov udalosti môže byť poskytnutý ako parameter.

### Bežné udalosti

Existuje [množstvo udalostí](https://developer.mozilla.org/docs/Web/Events), ktoré môžete počúvať pri vytváraní aplikácie. Prakticky všetko, čo používateľ urobí na stránke, vyvolá udalosť, čo vám dáva veľkú moc zabezpečiť, že dostane požadovaný zážitok. Našťastie budete zvyčajne potrebovať len malú časť udalostí. Tu je niekoľko bežných (vrátane dvoch, ktoré použijeme pri vytváraní našej hry):

- [click](https://developer.mozilla.org/docs/Web/API/Element/click_event): Používateľ klikol na niečo, zvyčajne tlačidlo alebo hypertextový odkaz
- [contextmenu](https://developer.mozilla.org/docs/Web/API/Element/contextmenu_event): Používateľ klikol pravým tlačidlom myši
- [select](https://developer.mozilla.org/docs/Web/API/Element/select_event): Používateľ označil nejaký text
- [input](https://developer.mozilla.org/docs/Web/API/Element/input_event): Používateľ zadal nejaký text

## Vytvorenie hry

Vytvoríme hru, aby sme preskúmali, ako udalosti fungujú v JavaScripte. Naša hra bude testovať schopnosť hráča písať, čo je jedna z najviac podceňovaných zručností, ktorú by mal mať každý vývojár. Mali by sme všetci trénovať písanie! Všeobecný priebeh hry bude vyzerať takto:

- Hráč klikne na tlačidlo štart a zobrazí sa mu citát na písanie
- Hráč píše citát čo najrýchlejšie do textového poľa
  - Po dokončení každého slova sa zvýrazní ďalšie
  - Ak hráč urobí chybu, textové pole sa zmení na červené
  - Keď hráč dokončí citát, zobrazí sa správa o úspechu s uplynutým časom

Poďme postaviť našu hru a naučiť sa o udalostiach!

### Štruktúra súborov

Budeme potrebovať celkovo tri súbory: **index.html**, **script.js** a **style.css**. Začnime ich nastavením, aby sme si uľahčili prácu.

- Vytvorte nový priečinok pre svoju prácu otvorením konzoly alebo terminálového okna a zadaním nasledujúceho príkazu:

```bash
# Linux or macOS
mkdir typing-game && cd typing-game

# Windows
md typing-game && cd typing-game
```

- Otvorte Visual Studio Code

```bash
code .
```

- Pridajte do priečinka vo Visual Studio Code tri súbory s nasledujúcimi názvami:
  - index.html
  - script.js
  - style.css

## Vytvorenie používateľského rozhrania

Ak preskúmame požiadavky, vieme, že budeme potrebovať niekoľko prvkov na našej HTML stránke. Je to niečo ako recept, kde potrebujeme nejaké ingrediencie:

- Miesto na zobrazenie citátu, ktorý má používateľ písať
- Miesto na zobrazenie správ, ako je správa o úspechu
- Textové pole na písanie
- Tlačidlo štart

Každý z nich bude potrebovať ID, aby sme s nimi mohli pracovať v našom JavaScripte. Pridáme tiež odkazy na CSS a JavaScript súbory, ktoré vytvoríme.

Vytvorte nový súbor s názvom **index.html**. Pridajte nasledujúci HTML:

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

### Spustenie aplikácie

Vždy je najlepšie vyvíjať iteratívne, aby ste videli, ako veci vyzerajú. Spustime našu aplikáciu. Existuje skvelé rozšírenie pre Visual Studio Code s názvom [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer&WT.mc_id=academic-77807-sagibbon), ktoré bude hostiť vašu aplikáciu lokálne a obnoví prehliadač pri každom uložení.

- Nainštalujte [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer&WT.mc_id=academic-77807-sagibbon) podľa odkazu a kliknutím na **Install**
  - Prehliadač vás vyzve na otvorenie Visual Studio Code a potom vás Visual Studio Code vyzve na vykonanie inštalácie
  - Reštartujte Visual Studio Code, ak budete vyzvaní
- Po nainštalovaní kliknite vo Visual Studio Code na Ctrl-Shift-P (alebo Cmd-Shift-P) na otvorenie príkazovej palety
- Zadajte **Live Server: Open with Live Server**
  - Live Server začne hostiť vašu aplikáciu
- Otvorte prehliadač a prejdite na **https://localhost:5500**
- Teraz by ste mali vidieť stránku, ktorú ste vytvorili!

Pridajme nejakú funkcionalitu.

## Pridanie CSS

S naším HTML vytvoreným pridajme CSS pre základné štýlovanie. Potrebujeme zvýrazniť slovo, ktoré by mal hráč písať, a zafarbiť textové pole, ak to, čo napísal, je nesprávne. Urobíme to pomocou dvoch tried.

Vytvorte nový súbor s názvom **style.css** a pridajte nasledujúcu syntax.

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

✅ Pokiaľ ide o CSS, môžete si stránku usporiadať podľa svojich predstáv. Venujte trochu času a urobte stránku atraktívnejšou:

- Vyberte iné písmo
- Zafarbite nadpisy
- Zmeňte veľkosť prvkov

## JavaScript

S naším používateľským rozhraním vytvoreným je čas zamerať našu pozornosť na JavaScript, ktorý poskytne logiku. Rozdelíme to na niekoľko krokov:

- [Vytvorenie konštánt](../../../../4-typing-game/typing-game)
- [Poslucháč udalostí na spustenie hry](../../../../4-typing-game/typing-game)
- [Poslucháč udalostí na písanie](../../../../4-typing-game/typing-game)

Najprv však vytvorte nový súbor s názvom **script.js**.

### Pridanie konštánt

Budeme potrebovať niekoľko položiek, aby sme si uľahčili programovanie. Opäť, podobne ako recept, tu je to, čo budeme potrebovať:

- Pole so zoznamom všetkých citátov
- Prázdne pole na uloženie všetkých slov aktuálneho citátu
- Priestor na uloženie indexu slova, ktoré hráč práve píše
- Čas, kedy hráč klikol na štart

Budeme tiež chcieť odkazy na prvky používateľského rozhrania:

- Textové pole (**typed-value**)
- Zobrazenie citátu (**quote**)
- Správa (**message**)

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

✅ Pridajte do svojej hry viac citátov

> **NOTE:** Prvky môžeme kedykoľvek v kóde získať pomocou `document.getElementById`. Pretože tieto prvky budeme pravidelne odkazovať, vyhneme sa preklepom v reťazcových literáloch použitím konštánt. Frameworky ako [Vue.js](https://vuejs.org/) alebo [React](https://reactjs.org/) vám môžu pomôcť lepšie spravovať centralizáciu vášho kódu.

Venujte chvíľu času sledovaniu videa o používaní `const`, `let` a `var`

[![Typy premenných](https://img.youtube.com/vi/JNIXfGiDWM8/0.jpg)](https://youtube.com/watch?v=JNIXfGiDWM8 "Typy premenných")

> 🎥 Kliknite na obrázok vyššie pre video o premenných.

### Pridanie logiky štartu

Na začatie hry hráč klikne na štart. Samozrejme, nevieme, kedy klikne na štart. Tu prichádza na rad [poslucháč udalostí](https://developer.mozilla.org/docs/Web/API/EventTarget/addEventListener). Poslucháč udalostí nám umožní počúvať, kedy sa niečo stane (udalosť) a vykonať kód ako reakciu. V našom prípade chceme vykonať kód, keď používateľ klikne na štart.

Keď používateľ klikne na **štart**, musíme vybrať citát, nastaviť používateľské rozhranie a nastaviť sledovanie aktuálneho slova a času. Nižšie je JavaScript, ktorý budete potrebovať pridať; rozoberieme ho hneď po bloku skriptu.

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

Rozoberme kód!

- Nastavenie sledovania slov
  - Použitie [Math.floor](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Math/floor) a [Math.random](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Math/random) nám umožňuje náhodne vybrať citát z poľa `quotes`
  - Citát konvertujeme na pole `words`, aby sme mohli sledovať slovo, ktoré hráč práve píše
  - `wordIndex` nastavíme na 0, pretože hráč začne na prvom slove
- Nastavenie používateľského rozhrania
  - Vytvoríme pole `spanWords`, ktoré obsahuje každé slovo vo vnútri prvku `span`
    - To nám umožní zvýrazniť slovo na displeji
  - `join` pole na vytvorenie reťazca, ktorý môžeme použiť na aktualizáciu `innerHTML` na `quoteElement`
    - To zobrazí citát hráčovi
  - Nastavíme `className` prvého prvku `span` na `highlight`, aby sme ho zvýraznili ako žltý
  - Vyčistíme `messageElement` nastavením `innerText` na `''`
- Nastavenie textového poľa
  - Vyčistíme aktuálnu `value` na `typedValueElement`
  - Nastavíme `focus` na `typedValueElement`
- Spustíme časovač volaním `getTime`

### Pridanie logiky písania

Keď hráč píše, vyvolá sa udalosť `input`. Tento poslucháč udalostí skontroluje, či hráč píše slovo správne, a spracuje aktuálny stav hry. Vráťte sa do **script.js** a pridajte nasledujúci kód na koniec. Rozoberieme ho hneď potom.

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

Rozoberme kód! Začíname získaním aktuálneho slova a hodnoty, ktorú hráč zatiaľ napísal. Potom máme logiku typu "vodopád", kde kontrolujeme, či je citát dokončený, slovo je dokončené, slovo je správne alebo (nakoniec), či je chyba.

- Citát je dokončený, čo je indikované tým, že `typedValue` je rovné `currentWord` a `wordIndex` je rovné jednej menej ako `length` `words`
  - Vypočítame `elapsedTime` odčítaním `startTime` od aktuálneho času
  - Rozdelíme `elapsedTime` 1 000, aby sme ho konvertovali z milisekúnd na sekundy
  - Zobrazíme správu o úspechu
- Slovo je dokončené, čo je indikované tým, že `typedValue` končí medzerou (koniec slova) a `typedValue` je rovné `currentWord`
  - Nastavíme `value` na `typedElement` na `''`, aby sme umožnili napísanie ďalšieho slova
  - Zvýšime `wordIndex`, aby sme prešli na ďalšie slovo
  - Prejdeme všetky `childNodes` `quoteElement`, aby sme nastavili `className` na `''`, čím sa vrátime k predvolenému zobrazeniu
  - Nastavíme `className` aktuálneho slova na `highlight`, aby sme ho označili ako ďalšie slovo na písanie
- Slovo je aktuálne napísané správne (ale nie je dokončené), čo je indikované tým, že `currentWord` začína s `typedValue`
  - Zabezpečíme, že `typedValueElement` je zobrazený ako predvolený vymazaním `className`
- Ak sme sa dostali až sem, máme chybu
  - Nastavíme `className` na `typedValueElement` na `error`

## Otestujte svoju aplikáciu

Dostali ste sa na koniec! Posledným krokom je zabezpečiť, aby naša aplikácia fungovala. Vyskúšajte ju! Nebojte sa, ak sú tam chyby; **všetci vývojári** majú chyby. Preskúmajte správy a podľa potreby ich opravte.

Kliknite na **štart** a začnite písať! Malo by to vyzerať trochu ako animácia, ktorú sme videli predtým.

![Animácia hry v akcii](../../../../4-typing-game/images/demo.gif)

---

## 🚀 Výzva

Pridajte viac funkcií

- Deaktivujte poslucháč udalostí `input` po dokončení a znova ho aktivujte, keď sa klikne na tlačidlo
- Deaktivujte textové pole, keď hráč dokončí citát
- Zobrazte modálne dialógové okno so správou o úspechu
- Ukladajte najvyššie skóre pomocou [localStorage](https://developer.mozilla.org/docs/Web/API/Window/localStorage)

## Kvíz po prednáške

[Kvíz po prednáške](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/22)

## Prehľad a samostatné štúdium

Prečítajte si o [všetkých dostupných udalostiach](https://developer.mozilla.org/docs/Web/Events), ktoré má vývojár k dispozícii prostredníctvom webového prehliadača, a zvážte scenáre, v ktorých by ste ich použili.

## Zadanie

[Vytvorte novú hru na klávesnici](assignment.md)

---

**Upozornenie**:  
Tento dokument bol preložený pomocou služby AI prekladu [Co-op Translator](https://github.com/Azure/co-op-translator). Aj keď sa snažíme o presnosť, prosím, berte na vedomie, že automatizované preklady môžu obsahovať chyby alebo nepresnosti. Pôvodný dokument v jeho pôvodnom jazyku by mal byť považovaný za autoritatívny zdroj. Pre kritické informácie sa odporúča profesionálny ľudský preklad. Nie sme zodpovední za akékoľvek nedorozumenia alebo nesprávne interpretácie vyplývajúce z použitia tohto prekladu.