<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "d9da6dc61fb712b29f65e108c79b8a5d",
  "translation_date": "2025-08-27T23:48:49+00:00",
  "source_file": "6-space-game/1-introduction/README.md",
  "language_code": "sk"
}
-->
# Vytvorenie vesmírnej hry, časť 1: Úvod

![video](../../../../6-space-game/images/pewpew.gif)

## Kvíz pred prednáškou

[Kvíz pred prednáškou](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/29)

### Dedičnosť a kompozícia v tvorbe hier

V predchádzajúcich lekciách nebolo potrebné venovať veľkú pozornosť návrhu architektúry aplikácií, ktoré ste vytvorili, pretože projekty boli veľmi malé. Avšak, keď vaše aplikácie rastú vo veľkosti a rozsahu, rozhodnutia o architektúre sa stávajú dôležitejším problémom. Existujú dva hlavné prístupy k vytváraniu väčších aplikácií v JavaScripte: *kompozícia* alebo *dedičnosť*. Obe majú svoje výhody a nevýhody, ale poďme si ich vysvetliť v kontexte hry.

✅ Jedna z najznámejších kníh o programovaní sa zaoberá [návrhovými vzormi](https://en.wikipedia.org/wiki/Design_Patterns).

V hre máte `herné objekty`, ktoré sú objekty existujúce na obrazovke. To znamená, že majú polohu v karteziánskom súradnicovom systéme, charakterizovanú `x` a `y` súradnicou. Pri vývoji hry si všimnete, že všetky vaše herné objekty majú štandardné vlastnosti, spoločné pre každú hru, ktorú vytvoríte, konkrétne prvky, ktoré sú:

- **založené na polohe** Väčšina, ak nie všetky, herné prvky sú založené na polohe. To znamená, že majú polohu, `x` a `y`.
- **pohyblivé** Sú to objekty, ktoré sa môžu presunúť na novú polohu. Typicky ide o hrdinu, monštrum alebo NPC (nehráčsku postavu), ale nie napríklad o statický objekt ako strom.
- **samodeštrukčné** Tieto objekty existujú len určitý čas, kým sa pripravia na vymazanie. Zvyčajne je to reprezentované booleanom `dead` alebo `destroyed`, ktorý signalizuje hernému enginu, že tento objekt už nemá byť vykreslený.
- **cool-down** 'Cool-down' je typická vlastnosť krátkodobých objektov. Typickým príkladom je kúsok textu alebo grafický efekt, ako napríklad explózia, ktorá by mala byť viditeľná len niekoľko milisekúnd.

✅ Premýšľajte o hre ako Pac-Man. Dokážete identifikovať štyri typy objektov uvedené vyššie v tejto hre?

### Vyjadrenie správania

Všetko, čo sme vyššie opísali, sú správania, ktoré herné objekty môžu mať. Ako ich teda zakódujeme? Toto správanie môžeme vyjadriť ako metódy priradené buď ku triedam alebo objektom.

**Triedy**

Myšlienka je použiť `triedy` v spojení s `dedičnosťou`, aby sme dosiahli pridanie určitého správania do triedy.

✅ Dedičnosť je dôležitý koncept na pochopenie. Viac sa dozviete v [článku MDN o dedičnosti](https://developer.mozilla.org/docs/Web/JavaScript/Inheritance_and_the_prototype_chain).

Vyjadrené kódom, herný objekt môže typicky vyzerať takto:

```javascript

//set up the class GameObject
class GameObject {
  constructor(x, y, type) {
    this.x = x;
    this.y = y;
    this.type = type;
  }
}

//this class will extend the GameObject's inherent class properties
class Movable extends GameObject {
  constructor(x,y, type) {
    super(x,y, type)
  }

//this movable object can be moved on the screen
  moveTo(x, y) {
    this.x = x;
    this.y = y;
  }
}

//this is a specific class that extends the Movable class, so it can take advantage of all the properties that it inherits
class Hero extends Movable {
  constructor(x,y) {
    super(x,y, 'Hero')
  }
}

//this class, on the other hand, only inherits the GameObject properties
class Tree extends GameObject {
  constructor(x,y) {
    super(x,y, 'Tree')
  }
}

//a hero can move...
const hero = new Hero();
hero.moveTo(5,5);

//but a tree cannot
const tree = new Tree();
```

✅ Venujte pár minút tomu, aby ste si predstavili hrdinu z Pac-Mana (napríklad Inky, Pinky alebo Blinky) a ako by bol napísaný v JavaScripte.

**Kompozícia**

Iný spôsob riešenia dedičnosti objektov je použitie *kompozície*. Potom objekty vyjadrujú svoje správanie takto:

```javascript
//create a constant gameObject
const gameObject = {
  x: 0,
  y: 0,
  type: ''
};

//...and a constant movable
const movable = {
  moveTo(x, y) {
    this.x = x;
    this.y = y;
  }
}
//then the constant movableObject is composed of the gameObject and movable constants
const movableObject = {...gameObject, ...movable};

//then create a function to create a new Hero who inherits the movableObject properties
function createHero(x, y) {
  return {
    ...movableObject,
    x,
    y,
    type: 'Hero'
  }
}
//...and a static object that inherits only the gameObject properties
function createStatic(x, y, type) {
  return {
    ...gameObject
    x,
    y,
    type
  }
}
//create the hero and move it
const hero = createHero(10,10);
hero.moveTo(5,5);
//and create a static tree which only stands around
const tree = createStatic(0,0, 'Tree'); 
```

**Ktorý vzor by som mal použiť?**

Je na vás, ktorý vzor si vyberiete. JavaScript podporuje oba tieto paradigmy.

--

Ďalší vzor, ktorý je bežný pri vývoji hier, rieši problém správy používateľského zážitku a výkonu hry.

## Vzor Pub/Sub

✅ Pub/Sub znamená 'publish-subscribe'

Tento vzor rieši myšlienku, že rôzne časti vašej aplikácie by nemali vedieť o sebe navzájom. Prečo je to tak? Umožňuje to oveľa jednoduchšie pochopiť, čo sa deje vo všeobecnosti, ak sú rôzne časti oddelené. Tiež to uľahčuje náhle zmeniť správanie, ak je to potrebné. Ako to dosiahneme? Robíme to zavedením niekoľkých konceptov:

- **správa**: Správa je zvyčajne textový reťazec sprevádzaný voliteľným payloadom (dátami, ktoré objasňujú, o čom správa je). Typická správa v hre môže byť `KEY_PRESSED_ENTER`.
- **vydavateľ**: Tento prvok *publikuje* správu a posiela ju všetkým odberateľom.
- **odberateľ**: Tento prvok *počúva* konkrétne správy a vykonáva nejakú úlohu ako výsledok prijatia tejto správy, napríklad vystrelenie lasera.

Implementácia je pomerne malá, ale je to veľmi silný vzor. Tu je, ako môže byť implementovaný:

```javascript
//set up an EventEmitter class that contains listeners
class EventEmitter {
  constructor() {
    this.listeners = {};
  }
//when a message is received, let the listener to handle its payload
  on(message, listener) {
    if (!this.listeners[message]) {
      this.listeners[message] = [];
    }
    this.listeners[message].push(listener);
  }
//when a message is sent, send it to a listener with some payload
  emit(message, payload = null) {
    if (this.listeners[message]) {
      this.listeners[message].forEach(l => l(message, payload))
    }
  }
}

```

Na použitie vyššie uvedeného kódu môžeme vytvoriť veľmi malú implementáciu:

```javascript
//set up a message structure
const Messages = {
  HERO_MOVE_LEFT: 'HERO_MOVE_LEFT'
};
//invoke the eventEmitter you set up above
const eventEmitter = new EventEmitter();
//set up a hero
const hero = createHero(0,0);
//let the eventEmitter know to watch for messages pertaining to the hero moving left, and act on it
eventEmitter.on(Messages.HERO_MOVE_LEFT, () => {
  hero.move(5,0);
});

//set up the window to listen for the keyup event, specifically if the left arrow is hit, emit a message to move the hero left
window.addEventListener('keyup', (evt) => {
  if (evt.key === 'ArrowLeft') {
    eventEmitter.emit(Messages.HERO_MOVE_LEFT)
  }
});
```

Vyššie sme pripojili udalosť klávesnice, `ArrowLeft`, a poslali správu `HERO_MOVE_LEFT`. Počúvame túto správu a ako výsledok presúvame `hrdinu`. Silou tohto vzoru je, že event listener a hrdina o sebe navzájom nevedia. Môžete premapovať `ArrowLeft` na kláves `A`. Okrem toho by bolo možné urobiť niečo úplne iné na `ArrowLeft` vykonaním niekoľkých úprav funkcie `on` eventEmittera:

```javascript
eventEmitter.on(Messages.HERO_MOVE_LEFT, () => {
  hero.move(5,0);
});
```

Keď sa veci komplikujú, keď vaša hra rastie, tento vzor zostáva rovnako zložitý a váš kód zostáva čistý. Je naozaj odporúčané prijať tento vzor.

---

## 🚀 Výzva

Premýšľajte o tom, ako môže vzor pub-sub zlepšiť hru. Ktoré časti by mali emitovať udalosti a ako by na ne mala hra reagovať? Teraz máte šancu byť kreatívni a premýšľať o novej hre a o tom, ako by sa jej časti mohli správať.

## Kvíz po prednáške

[Kvíz po prednáške](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/30)

## Prehľad a samostatné štúdium

Dozviete sa viac o Pub/Sub [čítaním o ňom](https://docs.microsoft.com/azure/architecture/patterns/publisher-subscriber/?WT.mc_id=academic-77807-sagibbon).

## Zadanie

[Navrhnite hru](assignment.md)

---

**Upozornenie**:  
Tento dokument bol preložený pomocou služby AI prekladu [Co-op Translator](https://github.com/Azure/co-op-translator). Hoci sa snažíme o presnosť, prosím, berte na vedomie, že automatizované preklady môžu obsahovať chyby alebo nepresnosti. Pôvodný dokument v jeho rodnom jazyku by mal byť považovaný za autoritatívny zdroj. Pre kritické informácie sa odporúča profesionálny ľudský preklad. Nie sme zodpovední za akékoľvek nedorozumenia alebo nesprávne interpretácie vyplývajúce z použitia tohto prekladu.