<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "2e83e38c35dc003f046d7cc0bbfd4920",
  "translation_date": "2025-08-27T23:43:32+00:00",
  "source_file": "6-space-game/4-collision-detection/README.md",
  "language_code": "sk"
}
-->
# Vytvorenie vesmírnej hry, časť 4: Pridanie lasera a detekcia kolízií

## Kvíz pred prednáškou

[Kvíz pred prednáškou](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/35)

V tejto lekcii sa naučíte, ako strieľať lasery pomocou JavaScriptu! Do našej hry pridáme dve veci:

- **Laser**: tento laser sa vystrelí z lode hrdinu a pohybuje sa vertikálne nahor
- **Detekcia kolízií**, ako súčasť implementácie schopnosti *strieľať*, pridáme aj niekoľko pravidiel hry:
   - **Laser zasiahne nepriateľa**: Nepriateľ zomrie, ak ho zasiahne laser
   - **Laser zasiahne hornú časť obrazovky**: Laser sa zničí, ak zasiahne hornú časť obrazovky
   - **Kolízia nepriateľa a hrdinu**: Nepriateľ aj hrdina sa zničia, ak sa zrazia
   - **Nepriateľ zasiahne spodnú časť obrazovky**: Nepriateľ aj hrdina sa zničia, ak nepriateľ zasiahne spodnú časť obrazovky

Stručne povedané, vy -- *hrdina* -- musíte zasiahnuť všetkých nepriateľov laserom skôr, než sa dostanú na spodnú časť obrazovky.

✅ Urobte si malý prieskum o úplne prvej počítačovej hre, ktorá bola kedy napísaná. Aká bola jej funkčnosť?

Buďme spolu hrdinami!

## Detekcia kolízií

Ako vykonáme detekciu kolízií? Musíme si predstaviť naše herné objekty ako obdĺžniky, ktoré sa pohybujú. Prečo, pýtate sa? No, obrázok použitý na vykreslenie herného objektu je obdĺžnik: má `x`, `y`, `šírku` a `výšku`.

Ak sa dva obdĺžniky, napríklad hrdina a nepriateľ, *pretínajú*, máte kolíziu. Čo by sa malo stať, závisí od pravidiel hry. Na implementáciu detekcie kolízií potrebujete nasledovné:

1. Spôsob, ako získať obdĺžnikovú reprezentáciu herného objektu, niečo takéto:

   ```javascript
   rectFromGameObject() {
     return {
       top: this.y,
       left: this.x,
       bottom: this.y + this.height,
       right: this.x + this.width
     }
   }
   ```

2. Porovnávaciu funkciu, ktorá môže vyzerať takto:

   ```javascript
   function intersectRect(r1, r2) {
     return !(r2.left > r1.right ||
       r2.right < r1.left ||
       r2.top > r1.bottom ||
       r2.bottom < r1.top);
   }
   ```

## Ako ničíme objekty

Na zničenie objektov v hre musíte dať hre vedieť, že tento objekt už nemá byť vykreslený v hernej slučke, ktorá sa spúšťa v určitých intervaloch. Spôsob, ako to urobiť, je označiť herný objekt ako *mŕtvy*, keď sa niečo stane, napríklad takto:

```javascript
// collision happened
enemy.dead = true
```

Potom môžete vyradiť *mŕtve* objekty pred opätovným vykreslením obrazovky, napríklad takto:

```javascript
gameObjects = gameObject.filter(go => !go.dead);
```

## Ako vystreliť laser

Vystrelenie lasera znamená reagovať na udalosť stlačenia klávesy a vytvoriť objekt, ktorý sa pohybuje určitým smerom. Preto musíme vykonať nasledujúce kroky:

1. **Vytvoriť objekt lasera**: z vrchnej časti lode hrdinu, ktorý sa po vytvorení začne pohybovať nahor smerom k hornej časti obrazovky.
2. **Pripojiť kód k udalosti stlačenia klávesy**: musíme vybrať kláves na klávesnici, ktorý bude predstavovať hráča strieľajúceho laser.
3. **Vytvoriť herný objekt, ktorý vyzerá ako laser**, keď je kláves stlačený.

## Časový odstup pre laser

Laser musí vystreliť vždy, keď stlačíte kláves, napríklad *medzerník*. Aby sme zabránili hre vytvárať príliš veľa laserov v krátkom čase, musíme to opraviť. Oprava spočíva v implementácii tzv. *časového odstupu*, časovača, ktorý zabezpečí, že laser môže byť vystrelený len v určitých intervaloch. Môžete to implementovať nasledovne:

```javascript
class Cooldown {
  constructor(time) {
    this.cool = false;
    setTimeout(() => {
      this.cool = true;
    }, time)
  }
}

class Weapon {
  constructor {
  }
  fire() {
    if (!this.cooldown || this.cooldown.cool) {
      // produce a laser
      this.cooldown = new Cooldown(500);
    } else {
      // do nothing - it hasn't cooled down yet.
    }
  }
}
```

✅ Pozrite si lekciu 1 zo série vesmírnych hier, aby ste si pripomenuli *časové odstupy*.

## Čo vytvoriť

Vezmite existujúci kód (ktorý by ste mali vyčistiť a refaktorovať) z predchádzajúcej lekcie a rozšírte ho. Buď začnite s kódom z časti II, alebo použite kód z [časti III - štartovací kód](../../../../../../../../../your-work).

> tip: laser, s ktorým budete pracovať, je už vo vašom priečinku s prostriedkami a je referencovaný vaším kódom

- **Pridajte detekciu kolízií**, keď laser narazí na niečo, mali by platiť nasledujúce pravidlá:
   1. **Laser zasiahne nepriateľa**: nepriateľ zomrie, ak ho zasiahne laser
   2. **Laser zasiahne hornú časť obrazovky**: laser sa zničí, ak zasiahne hornú časť obrazovky
   3. **Kolízia nepriateľa a hrdinu**: nepriateľ aj hrdina sa zničia, ak sa zrazia
   4. **Nepriateľ zasiahne spodnú časť obrazovky**: nepriateľ aj hrdina sa zničia, ak nepriateľ zasiahne spodnú časť obrazovky

## Odporúčané kroky

Vyhľadajte súbory, ktoré boli pre vás vytvorené v podpriečinku `your-work`. Mali by obsahovať nasledovné:

```bash
-| assets
  -| enemyShip.png
  -| player.png
  -| laserRed.png
-| index.html
-| app.js
-| package.json
```

Spustite svoj projekt v priečinku `your_work` zadaním:

```bash
cd your-work
npm start
```

Vyššie uvedené spustí HTTP server na adrese `http://localhost:5000`. Otvorte prehliadač a zadajte túto adresu, momentálne by sa mal zobraziť hrdina a všetci nepriatelia, zatiaľ sa nič nehýbe :).

### Pridajte kód

1. **Nastavte obdĺžnikovú reprezentáciu herného objektu na spracovanie kolízií** Nasledujúci kód umožňuje získať obdĺžnikovú reprezentáciu `GameObject`. Upraviť triedu GameObject tak, aby ju rozšírila:

    ```javascript
    rectFromGameObject() {
        return {
          top: this.y,
          left: this.x,
          bottom: this.y + this.height,
          right: this.x + this.width,
        };
      }
    ```

2. **Pridajte kód, ktorý kontroluje kolízie** Toto bude nová funkcia, ktorá testuje, či sa dva obdĺžniky pretínajú:

    ```javascript
    function intersectRect(r1, r2) {
      return !(
        r2.left > r1.right ||
        r2.right < r1.left ||
        r2.top > r1.bottom ||
        r2.bottom < r1.top
      );
    }
    ```

3. **Pridajte schopnosť vystreliť laser**
   1. **Pridajte správu o udalosti stlačenia klávesy**. Kláves *medzerník* by mal vytvoriť laser tesne nad loďou hrdinu. Pridajte tri konštanty do objektu Messages:

       ```javascript
        KEY_EVENT_SPACE: "KEY_EVENT_SPACE",
        COLLISION_ENEMY_LASER: "COLLISION_ENEMY_LASER",
        COLLISION_ENEMY_HERO: "COLLISION_ENEMY_HERO",
       ```

   1. **Spracujte kláves medzerník**. Upraviť funkciu `window.addEventListener` pre stlačenie klávesy, aby spracovala medzerník:

      ```javascript
        } else if(evt.keyCode === 32) {
          eventEmitter.emit(Messages.KEY_EVENT_SPACE);
        }
      ```

    1. **Pridajte poslucháčov**. Upraviť funkciu `initGame()`, aby hrdina mohol strieľať, keď je stlačený medzerník:

       ```javascript
       eventEmitter.on(Messages.KEY_EVENT_SPACE, () => {
        if (hero.canFire()) {
          hero.fire();
        }
       ```

       a pridajte novú funkciu `eventEmitter.on()`, aby ste zabezpečili správanie, keď nepriateľ narazí na laser:

          ```javascript
          eventEmitter.on(Messages.COLLISION_ENEMY_LASER, (_, { first, second }) => {
            first.dead = true;
            second.dead = true;
          })
          ```

   1. **Pohyb objektu**, Zabezpečte, aby sa laser postupne pohyboval k hornej časti obrazovky. Vytvoríte novú triedu Laser, ktorá rozširuje `GameObject`, ako ste to už urobili predtým: 
   
      ```javascript
        class Laser extends GameObject {
        constructor(x, y) {
          super(x,y);
          (this.width = 9), (this.height = 33);
          this.type = 'Laser';
          this.img = laserImg;
          let id = setInterval(() => {
            if (this.y > 0) {
              this.y -= 15;
            } else {
              this.dead = true;
              clearInterval(id);
            }
          }, 100)
        }
      }
      ```

   1. **Spracujte kolízie**, Implementujte pravidlá kolízií pre laser. Pridajte funkciu `updateGameObjects()`, ktorá testuje objekty na kolízie:

      ```javascript
      function updateGameObjects() {
        const enemies = gameObjects.filter(go => go.type === 'Enemy');
        const lasers = gameObjects.filter((go) => go.type === "Laser");
      // laser hit something
        lasers.forEach((l) => {
          enemies.forEach((m) => {
            if (intersectRect(l.rectFromGameObject(), m.rectFromGameObject())) {
            eventEmitter.emit(Messages.COLLISION_ENEMY_LASER, {
              first: l,
              second: m,
            });
          }
         });
      });

        gameObjects = gameObjects.filter(go => !go.dead);
      }  
      ```

      Uistite sa, že ste pridali `updateGameObjects()` do hernej slučky v `window.onload`.

   4. **Implementujte časový odstup** pre laser, aby mohol byť vystrelený len v určitých intervaloch.

      Nakoniec upravte triedu Hero tak, aby mohla mať časový odstup:

       ```javascript
      class Hero extends GameObject {
        constructor(x, y) {
          super(x, y);
          (this.width = 99), (this.height = 75);
          this.type = "Hero";
          this.speed = { x: 0, y: 0 };
          this.cooldown = 0;
        }
        fire() {
          gameObjects.push(new Laser(this.x + 45, this.y - 10));
          this.cooldown = 500;
    
          let id = setInterval(() => {
            if (this.cooldown > 0) {
              this.cooldown -= 100;
            } else {
              clearInterval(id);
            }
          }, 200);
        }
        canFire() {
          return this.cooldown === 0;
        }
      }
      ```

V tomto bode má vaša hra určitú funkčnosť! Môžete sa pohybovať pomocou šípok, strieľať laser pomocou medzerníka a nepriatelia zmiznú, keď ich zasiahnete. Skvelá práca!

---

## 🚀 Výzva

Pridajte explóziu! Pozrite sa na herné prostriedky v [repozitári Space Art](../../../../6-space-game/solution/spaceArt/readme.txt) a skúste pridať explóziu, keď laser zasiahne mimozemšťana.

## Kvíz po prednáške

[Kvíz po prednáške](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/36)

## Prehľad a samostatné štúdium

Experimentujte s intervalmi vo vašej hre doteraz. Čo sa stane, keď ich zmeníte? Prečítajte si viac o [časových udalostiach v JavaScripte](https://www.freecodecamp.org/news/javascript-timing-events-settimeout-and-setinterval/).

## Zadanie

[Preskúmajte kolízie](assignment.md)

---

**Upozornenie**:  
Tento dokument bol preložený pomocou služby AI prekladu [Co-op Translator](https://github.com/Azure/co-op-translator). Hoci sa snažíme o presnosť, prosím, berte na vedomie, že automatizované preklady môžu obsahovať chyby alebo nepresnosti. Pôvodný dokument v jeho rodnom jazyku by mal byť považovaný za autoritatívny zdroj. Pre kritické informácie sa odporúča profesionálny ľudský preklad. Nie sme zodpovední za akékoľvek nedorozumenia alebo nesprávne interpretácie vyplývajúce z použitia tohto prekladu.