<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "d9da6dc61fb712b29f65e108c79b8a5d",
  "translation_date": "2025-08-27T23:49:31+00:00",
  "source_file": "6-space-game/1-introduction/README.md",
  "language_code": "sl"
}
-->
# Ustvari vesoljsko igro, 1. del: Uvod

![video](../../../../6-space-game/images/pewpew.gif)

## Predhodni kviz

[Predhodni kviz](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/29)

### Dedovanje in kompozicija pri razvoju iger

V prejšnjih lekcijah ni bilo veliko potrebe po skrbi za arhitekturo aplikacij, ki ste jih ustvarili, saj so bili projekti zelo majhnega obsega. Ko pa vaše aplikacije rastejo v velikosti in obsegu, postanejo arhitekturne odločitve pomembnejše. Obstajata dva glavna pristopa k ustvarjanju večjih aplikacij v JavaScriptu: *kompozicija* ali *dedovanje*. Oba imata svoje prednosti in slabosti, vendar ju bomo razložili v kontekstu igre.

✅ Ena najbolj znanih knjig o programiranju govori o [oblikovalskih vzorcih](https://en.wikipedia.org/wiki/Design_Patterns).

V igri imate `objekte igre`, ki so objekti, ki obstajajo na zaslonu. To pomeni, da imajo lokacijo v kartezijskem koordinatnem sistemu, ki jo označujeta koordinati `x` in `y`. Ko razvijate igro, boste opazili, da imajo vsi vaši objekti igre standardne lastnosti, skupne za vsako igro, ki jo ustvarite, in sicer elemente, ki so:

- **lokacijsko osnovani** Večina, če ne vsi, elementi igre so lokacijsko osnovani. To pomeni, da imajo lokacijo, `x` in `y`.
- **premični** To so objekti, ki se lahko premaknejo na novo lokacijo. To je običajno junak, pošast ali NPC (ne-igralni lik), ne pa na primer statični objekt, kot je drevo.
- **samouničujoči** Ti objekti obstajajo le določen čas, preden se pripravijo na izbris. Običajno je to predstavljeno z logično vrednostjo `dead` ali `destroyed`, ki signalizira igralnemu pogonu, da tega objekta ni več treba prikazovati.
- **časovno omejeni** 'Časovna omejitev' je tipična lastnost kratkoživih objektov. Tipičen primer je kos besedila ali grafični učinek, kot je eksplozija, ki naj bo viden le nekaj milisekund.

✅ Pomislite na igro, kot je Pac-Man. Ali lahko v tej igri prepoznate štiri zgoraj navedene tipe objektov?

### Izražanje vedenja

Vse, kar smo opisali zgoraj, so vedenja, ki jih lahko imajo objekti igre. Kako jih torej kodiramo? To vedenje lahko izrazimo kot metode, povezane bodisi s klasami bodisi z objekti.

**Klase**

Ideja je uporabiti `klase` v kombinaciji z `dedovanjem`, da dodamo določeno vedenje klasi.

✅ Dedovanje je pomemben koncept za razumevanje. Več o tem preberite v [članku MDN o dedovanju](https://developer.mozilla.org/docs/Web/JavaScript/Inheritance_and_the_prototype_chain).

V kodi je objekt igre običajno videti takole:

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

✅ Vzemite si nekaj minut in si zamislite junaka iz Pac-Mana (na primer Inky, Pinky ali Blinky) ter kako bi bil napisan v JavaScriptu.

**Kompozicija**

Drugačen način obravnavanja dedovanja objektov je uporaba *kompozicije*. Nato objekti izražajo svoje vedenje takole:

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

**Kateri vzorec naj uporabim?**

Odločitev je vaša, kateri vzorec boste izbrali. JavaScript podpira oba paradigmi.

--

Drug pogost vzorec pri razvoju iger obravnava problem upravljanja uporabniške izkušnje in zmogljivosti igre.

## Vzorec Pub/Sub

✅ Pub/Sub pomeni 'publish-subscribe' (objavi-naroči se)

Ta vzorec obravnava idejo, da različni deli vaše aplikacije ne bi smeli vedeti drug o drugem. Zakaj? To močno olajša razumevanje dogajanja na splošno, če so različni deli ločeni. Prav tako olajša nenadno spremembo vedenja, če je to potrebno. Kako to dosežemo? To storimo z vzpostavitvijo nekaterih konceptov:

- **sporočilo**: Sporočilo je običajno besedilni niz, ki ga spremlja neobvezna vsebina (kos podatkov, ki pojasnjuje, za kaj gre pri sporočilu). Tipično sporočilo v igri je lahko `KEY_PRESSED_ENTER`.
- **objavljalec**: Ta element *objavi* sporočilo in ga pošlje vsem naročnikom.
- **naročnik**: Ta element *posluša* določena sporočila in izvede neko nalogo kot rezultat prejetega sporočila, na primer izstreli laser.

Implementacija je zelo majhna, vendar je to zelo močan vzorec. Tukaj je, kako ga lahko implementiramo:

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

Za uporabo zgornje kode lahko ustvarimo zelo majhno implementacijo:

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

Zgoraj povežemo dogodek tipkovnice, `ArrowLeft`, in pošljemo sporočilo `HERO_MOVE_LEFT`. Poslušamo to sporočilo in premaknemo `hero` kot rezultat. Prednost tega vzorca je, da poslušalec dogodkov in junak ne vesta drug o drugem. Lahko premapirate `ArrowLeft` na tipko `A`. Poleg tega bi bilo mogoče narediti nekaj povsem drugega na `ArrowLeft` z nekaj urejanja funkcije `on` v eventEmitterju:

```javascript
eventEmitter.on(Messages.HERO_MOVE_LEFT, () => {
  hero.move(5,0);
});
```

Ko se stvari zapletejo, ko vaša igra raste, ta vzorec ostane enako zapleten in vaša koda ostane čista. Zelo priporočljivo je, da sprejmete ta vzorec.

---

## 🚀 Izziv

Razmislite, kako lahko vzorec pub-sub izboljša igro. Kateri deli naj oddajajo dogodke in kako naj igra nanje reagira? Zdaj imate priložnost, da postanete kreativni in razmislite o novi igri ter kako bi se njeni deli obnašali.

## Zaključni kviz

[Zaključni kviz](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/30)

## Pregled in samostojno učenje

Več o Pub/Sub preberite [tukaj](https://docs.microsoft.com/azure/architecture/patterns/publisher-subscriber/?WT.mc_id=academic-77807-sagibbon).

## Naloga

[Ustvarite osnutek igre](assignment.md)

---

**Omejitev odgovornosti**:  
Ta dokument je bil preveden z uporabo storitve za prevajanje z umetno inteligenco [Co-op Translator](https://github.com/Azure/co-op-translator). Čeprav si prizadevamo za natančnost, vas prosimo, da upoštevate, da lahko avtomatizirani prevodi vsebujejo napake ali netočnosti. Izvirni dokument v njegovem maternem jeziku je treba obravnavati kot avtoritativni vir. Za ključne informacije priporočamo profesionalni človeški prevod. Ne prevzemamo odgovornosti za morebitne nesporazume ali napačne razlage, ki bi nastale zaradi uporabe tega prevoda.