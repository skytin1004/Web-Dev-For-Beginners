<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "23f088add24f0f1fa51014a9e27ea280",
  "translation_date": "2025-08-27T23:40:45+00:00",
  "source_file": "6-space-game/3-moving-elements-around/README.md",
  "language_code": "sl"
}
-->
# Izdelava vesoljske igre, 3. del: Dodajanje gibanja

## Kviz pred predavanjem

[Kviz pred predavanjem](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/33)

Igre niso prav zabavne, dokler se vesoljci ne začnejo premikati po zaslonu! V tej igri bomo uporabili dva tipa gibanja:

- **Gibanje s tipkovnico/miško**: ko uporabnik uporablja tipkovnico ali miško za premikanje objekta na zaslonu.
- **Gibanje, ki ga sproži igra**: ko igra premika objekt v določenih časovnih intervalih.

Kako torej premikamo stvari na zaslonu? Vse temelji na kartezičnih koordinatah: spremenimo lokacijo (x, y) objekta in nato ponovno narišemo zaslon.

Običajno potrebujete naslednje korake za izvedbo *gibanja* na zaslonu:

1. **Nastavite novo lokacijo** za objekt; to je potrebno, da zaznamo, da se je objekt premaknil.
2. **Počistite zaslon**, zaslon je treba počistiti med posameznimi risanji. To lahko storimo tako, da narišemo pravokotnik, ki ga zapolnimo z barvo ozadja.
3. **Ponovno narišite objekt** na novi lokaciji. S tem dosežemo premik objekta z ene lokacije na drugo.

Tako lahko to izgleda v kodi:

```javascript
//set the hero's location
hero.x += 5;
// clear the rectangle that hosts the hero
ctx.clearRect(0, 0, canvas.width, canvas.height);
// redraw the game background and hero
ctx.fillRect(0, 0, canvas.width, canvas.height)
ctx.fillStyle = "black";
ctx.drawImage(heroImg, hero.x, hero.y);
```

✅ Ali lahko pomislite na razlog, zakaj bi lahko pogosto risanje vašega junaka večkrat na sekundo povzročilo težave z zmogljivostjo? Preberite več o [alternativah temu vzorcu](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial/Optimizing_canvas).

## Obdelava dogodkov tipkovnice

Dogodke obdelujete tako, da določene dogodke povežete s kodo. Dogodki tipkovnice se sprožijo na celotnem oknu, medtem ko so dogodki miške, kot je `click`, lahko povezani s klikom na določen element. V tem projektu bomo uporabljali dogodke tipkovnice.

Za obdelavo dogodka morate uporabiti metodo `addEventListener()` okna in ji podati dva vhodna parametra. Prvi parameter je ime dogodka, na primer `keyup`. Drugi parameter je funkcija, ki naj se izvede, ko se dogodek zgodi.

Tukaj je primer:

```javascript
window.addEventListener('keyup', (evt) => {
  // `evt.key` = string representation of the key
  if (evt.key === 'ArrowUp') {
    // do something
  }
})
```

Za dogodke tipk obstajata dve lastnosti dogodka, ki ju lahko uporabite za ugotavljanje, katera tipka je bila pritisnjena:

- `key`, to je nizovna predstavitev pritisnjene tipke, na primer `ArrowUp`
- `keyCode`, to je številčna predstavitev, na primer `37`, kar ustreza `ArrowLeft`.

✅ Manipulacija dogodkov tipk je uporabna tudi zunaj razvoja iger. Za katere druge namene bi lahko uporabili to tehniko?

### Posebne tipke: opozorilo

Obstajajo nekatere *posebne* tipke, ki vplivajo na okno. To pomeni, da če poslušate dogodek `keyup` in uporabite te posebne tipke za premikanje junaka, bo to povzročilo tudi horizontalno pomikanje. Zato boste morda želeli *izklopiti* to privzeto vedenje brskalnika, ko gradite svojo igro. Potrebujete kodo, kot je ta:

```javascript
let onKeyDown = function (e) {
  console.log(e.keyCode);
  switch (e.keyCode) {
    case 37:
    case 39:
    case 38:
    case 40: // Arrow keys
    case 32:
      e.preventDefault();
      break; // Space
    default:
      break; // do not block other keys
  }
};

window.addEventListener('keydown', onKeyDown);
```

Zgornja koda bo zagotovila, da bodo puščične tipke in preslednica imele svoje *privzeto* vedenje izklopljeno. Mehanizem za izklop se zgodi, ko pokličemo `e.preventDefault()`.

## Gibanje, ki ga sproži igra

Objekte lahko premikamo sami s pomočjo časovnikov, kot sta funkciji `setTimeout()` ali `setInterval()`, ki posodabljata lokacijo objekta ob vsakem kliku ali časovnem intervalu. Tako lahko to izgleda:

```javascript
let id = setInterval(() => {
  //move the enemy on the y axis
  enemy.y += 10;
})
```

## Igralna zanka

Igralna zanka je koncept, ki je v bistvu funkcija, ki se izvaja v rednih intervalih. Imenuje se igralna zanka, ker se v njej nariše vse, kar naj bo vidno uporabniku. Igralna zanka uporablja vse igralne objekte, ki so del igre, in jih nariše, razen če iz kakšnega razloga ne bi smeli biti več del igre. Na primer, če je objekt sovražnik, ki ga zadene laserski žarek in eksplodira, ni več del trenutne igralne zanke (o tem boste izvedeli več v naslednjih lekcijah).

Tako lahko igralna zanka običajno izgleda, izražena v kodi:

```javascript
let gameLoopId = setInterval(() =>
  function gameLoop() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    ctx.fillStyle = "black";
    ctx.fillRect(0, 0, canvas.width, canvas.height);
    drawHero();
    drawEnemies();
    drawStaticObjects();
}, 200);
```

Zgornja zanka se izvaja vsakih `200` milisekund za ponovno risanje platna. Sami lahko izberete najboljši interval, ki ustreza vaši igri.

## Nadaljevanje vesoljske igre

Obstoječo kodo boste razširili. Lahko začnete s kodo, ki ste jo dokončali v prvem delu, ali uporabite kodo iz [2. dela - začetna](../../../../6-space-game/3-moving-elements-around/your-work).

- **Premikanje junaka**: dodali boste kodo, da boste lahko junaka premikali s puščičnimi tipkami.
- **Premikanje sovražnikov**: dodali boste tudi kodo, da se bodo sovražniki premikali od zgoraj navzdol z določeno hitrostjo.

## Priporočeni koraki

Poiščite datoteke, ki so bile ustvarjene za vas v podmapi `your-work`. Vsebujejo naslednje:

```bash
-| assets
  -| enemyShip.png
  -| player.png
-| index.html
-| app.js
-| package.json
```

Svoj projekt začnete v mapi `your_work` tako, da vtipkate:

```bash
cd your-work
npm start
```

Zgornji ukaz bo zagnal HTTP strežnik na naslovu `http://localhost:5000`. Odprite brskalnik in vnesite ta naslov. Trenutno bi moral prikazati junaka in vse sovražnike; nič se še ne premika!

### Dodajte kodo

1. **Dodajte namenski objekt** za `hero`, `enemy` in `game object`, ki naj imajo lastnosti `x` in `y`. (Spomnite se dela o [Dedovanju ali kompoziciji](../README.md)).

   *NAMIG*: `game object` naj bo tisti, ki ima lastnosti `x` in `y` ter sposobnost, da se nariše na platno.

   >nasvet: začnite z dodajanjem novega razreda GameObject s konstruktorjem, kot je spodaj, in ga nato narišite na platno:
  
    ```javascript
        
    class GameObject {
      constructor(x, y) {
        this.x = x;
        this.y = y;
        this.dead = false;
        this.type = "";
        this.width = 0;
        this.height = 0;
        this.img = undefined;
      }
    
      draw(ctx) {
        ctx.drawImage(this.img, this.x, this.y, this.width, this.height);
      }
    }
    ```

    Zdaj razširite ta GameObject, da ustvarite Hero in Enemy.
    
    ```javascript
    class Hero extends GameObject {
      constructor(x, y) {
        ...it needs an x, y, type, and speed
      }
    }
    ```

    ```javascript
    class Enemy extends GameObject {
      constructor(x, y) {
        super(x, y);
        (this.width = 98), (this.height = 50);
        this.type = "Enemy";
        let id = setInterval(() => {
          if (this.y < canvas.height - this.height) {
            this.y += 5;
          } else {
            console.log('Stopped at', this.y)
            clearInterval(id);
          }
        }, 300)
      }
    }
    ```

2. **Dodajte obdelovalce dogodkov tipk** za upravljanje navigacije (premikanje junaka gor/dol, levo/desno).

   *SPOMNITE SE*: gre za kartezični sistem, zgornji levi kot je `0,0`. Prav tako ne pozabite dodati kode za zaustavitev *privzetega vedenja*.

   >nasvet: ustvarite svojo funkcijo onKeyDown in jo povežite z oknom:

   ```javascript
    let onKeyDown = function (e) {
	      console.log(e.keyCode);
	        ...add the code from the lesson above to stop default behavior
	      }
    };

    window.addEventListener("keydown", onKeyDown);
   ```
    
   Preverite konzolo brskalnika na tej točki in opazujte, kako se beležijo pritiski tipk.

3. **Implementirajte** [vzorec Pub-Sub](../README.md), da bo vaša koda ostala čista, ko boste sledili preostalim delom.

   Za izvedbo tega zadnjega dela lahko:

   1. **Dodate poslušalca dogodkov** na okno:

       ```javascript
        window.addEventListener("keyup", (evt) => {
          if (evt.key === "ArrowUp") {
            eventEmitter.emit(Messages.KEY_EVENT_UP);
          } else if (evt.key === "ArrowDown") {
            eventEmitter.emit(Messages.KEY_EVENT_DOWN);
          } else if (evt.key === "ArrowLeft") {
            eventEmitter.emit(Messages.KEY_EVENT_LEFT);
          } else if (evt.key === "ArrowRight") {
            eventEmitter.emit(Messages.KEY_EVENT_RIGHT);
          }
        });
        ```

    1. **Ustvarite razred EventEmitter** za objavljanje in naročanje na sporočila:

        ```javascript
        class EventEmitter {
          constructor() {
            this.listeners = {};
          }
        
          on(message, listener) {
            if (!this.listeners[message]) {
              this.listeners[message] = [];
            }
            this.listeners[message].push(listener);
          }
        
          emit(message, payload = null) {
            if (this.listeners[message]) {
              this.listeners[message].forEach((l) => l(message, payload));
            }
          }
        }
        ```

    1. **Dodajte konstante** in nastavite EventEmitter:

        ```javascript
        const Messages = {
          KEY_EVENT_UP: "KEY_EVENT_UP",
          KEY_EVENT_DOWN: "KEY_EVENT_DOWN",
          KEY_EVENT_LEFT: "KEY_EVENT_LEFT",
          KEY_EVENT_RIGHT: "KEY_EVENT_RIGHT",
        };
        
        let heroImg, 
            enemyImg, 
            laserImg,
            canvas, ctx, 
            gameObjects = [], 
            hero, 
            eventEmitter = new EventEmitter();
        ```

    1. **Inicializirajte igro**

    ```javascript
    function initGame() {
      gameObjects = [];
      createEnemies();
      createHero();
    
      eventEmitter.on(Messages.KEY_EVENT_UP, () => {
        hero.y -=5 ;
      })
    
      eventEmitter.on(Messages.KEY_EVENT_DOWN, () => {
        hero.y += 5;
      });
    
      eventEmitter.on(Messages.KEY_EVENT_LEFT, () => {
        hero.x -= 5;
      });
    
      eventEmitter.on(Messages.KEY_EVENT_RIGHT, () => {
        hero.x += 5;
      });
    }
    ```

1. **Nastavite igralno zanko**

   Preoblikujte funkcijo window.onload, da inicializirate igro in nastavite igralno zanko na ustrezen interval. Dodali boste tudi laserski žarek:

    ```javascript
    window.onload = async () => {
      canvas = document.getElementById("canvas");
      ctx = canvas.getContext("2d");
      heroImg = await loadTexture("assets/player.png");
      enemyImg = await loadTexture("assets/enemyShip.png");
      laserImg = await loadTexture("assets/laserRed.png");
    
      initGame();
      let gameLoopId = setInterval(() => {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
        ctx.fillStyle = "black";
        ctx.fillRect(0, 0, canvas.width, canvas.height);
        drawGameObjects(ctx);
      }, 100)
      
    };
    ```

5. **Dodajte kodo** za premikanje sovražnikov v določenih intervalih.

    Preoblikujte funkcijo `createEnemies()`, da ustvarite sovražnike in jih dodate v nov razred gameObjects:

    ```javascript
    function createEnemies() {
      const MONSTER_TOTAL = 5;
      const MONSTER_WIDTH = MONSTER_TOTAL * 98;
      const START_X = (canvas.width - MONSTER_WIDTH) / 2;
      const STOP_X = START_X + MONSTER_WIDTH;
    
      for (let x = START_X; x < STOP_X; x += 98) {
        for (let y = 0; y < 50 * 5; y += 50) {
          const enemy = new Enemy(x, y);
          enemy.img = enemyImg;
          gameObjects.push(enemy);
        }
      }
    }
    ```
    
    in dodajte funkcijo `createHero()`, da naredite podoben postopek za junaka.
    
    ```javascript
    function createHero() {
      hero = new Hero(
        canvas.width / 2 - 45,
        canvas.height - canvas.height / 4
      );
      hero.img = heroImg;
      gameObjects.push(hero);
    }
    ```

    in na koncu dodajte funkcijo `drawGameObjects()`, da začnete risanje:

    ```javascript
    function drawGameObjects(ctx) {
      gameObjects.forEach(go => go.draw(ctx));
    }
    ```

    Vaši sovražniki bi morali začeti napredovati proti vašemu vesoljskemu plovilu!

---

## 🚀 Izziv

Kot lahko vidite, se vaša koda lahko spremeni v 'špagetno kodo', ko začnete dodajati funkcije, spremenljivke in razrede. Kako lahko bolje organizirate svojo kodo, da bo bolj berljiva? Narišite sistem za organizacijo kode, tudi če še vedno ostane v eni datoteki.

## Kviz po predavanju

[Kviz po predavanju](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/34)

## Pregled in samostojno učenje

Čeprav svojo igro pišemo brez uporabe ogrodij, obstaja veliko ogrodij za razvoj iger na osnovi JavaScripta in platna. Vzemite si čas za [branje o teh](https://github.com/collections/javascript-game-engines).

## Naloga

[Komentirajte svojo kodo](assignment.md)

---

**Omejitev odgovornosti**:  
Ta dokument je bil preveden z uporabo storitve za prevajanje z umetno inteligenco [Co-op Translator](https://github.com/Azure/co-op-translator). Čeprav si prizadevamo za natančnost, vas prosimo, da upoštevate, da lahko avtomatizirani prevodi vsebujejo napake ali netočnosti. Izvirni dokument v njegovem maternem jeziku je treba obravnavati kot avtoritativni vir. Za ključne informacije priporočamo profesionalni človeški prevod. Ne odgovarjamo za morebitne nesporazume ali napačne razlage, ki bi nastale zaradi uporabe tega prevoda.