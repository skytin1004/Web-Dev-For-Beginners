<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "4e8250db84b027c9ff816b4e4c093457",
  "translation_date": "2025-08-27T23:42:10+00:00",
  "source_file": "6-space-game/5-keeping-score/README.md",
  "language_code": "sl"
}
-->
# Ustvari vesoljsko igro, 5. del: Točkovanje in življenja

## Kviz pred predavanjem

[Kviz pred predavanjem](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/37)

V tej lekciji se boste naučili, kako dodati točkovanje v igro in izračunati življenja.

## Risanje besedila na zaslon

Da bi lahko prikazali rezultat igre na zaslonu, morate vedeti, kako postaviti besedilo na zaslon. Odgovor je uporaba metode `fillText()` na objektu canvas. Prav tako lahko nadzorujete druge vidike, kot so izbira pisave, barva besedila in celo poravnava (levo, desno, sredina). Spodaj je nekaj kode, ki riše besedilo na zaslon.

```javascript
ctx.font = "30px Arial";
ctx.fillStyle = "red";
ctx.textAlign = "right";
ctx.fillText("show this on the screen", 0, 0);
```

✅ Preberite več o [tem, kako dodati besedilo na canvas](https://developer.mozilla.org/docs/Web/API/Canvas_API/Tutorial/Drawing_text), in se poigrajte, da bo vaše videti še bolj privlačno!

## Življenje kot koncept v igri

Koncept življenja v igri je zgolj številka. V kontekstu vesoljske igre je običajno dodeliti določeno število življenj, ki se odštevajo eno za drugim, ko vaša ladja prejme škodo. Lepo je, če lahko to prikažete grafično, na primer z mini ladjicami ali srčki, namesto s številko.

## Kaj bomo zgradili

Dodajmo naslednje elemente v vašo igro:

- **Rezultat igre**: Za vsako uničeno sovražno ladjo naj junak prejme nekaj točk, predlagamo 100 točk na ladjo. Rezultat igre naj bo prikazan v spodnjem levem kotu.
- **Življenja**: Vaša ladja ima tri življenja. Izgubite eno življenje vsakič, ko sovražna ladja trči v vas. Število življenj naj bo prikazano v spodnjem desnem kotu in naj bo sestavljeno iz naslednje grafike ![slika življenja](../../../../translated_images/life.6fb9f50d53ee0413cd91aa411f7c296e10a1a6de5c4a4197c718b49bf7d63ebf.sl.png).

## Priporočeni koraki

Poiščite datoteke, ki so bile ustvarjene za vas v podmapi `your-work`. Vsebujejo naslednje:

```bash
-| assets
  -| enemyShip.png
  -| player.png
  -| laserRed.png
-| index.html
-| app.js
-| package.json
```

Svoj projekt začnete v mapi `your_work` z vnosom:

```bash
cd your-work
npm start
```

Zgornji ukaz bo zagnal HTTP strežnik na naslovu `http://localhost:5000`. Odprite brskalnik in vnesite ta naslov. Trenutno bi morali videti junaka in vse sovražnike, in ko pritisnete levo in desno puščico, se junak premika in lahko strelja na sovražnike.

### Dodajanje kode

1. **Kopirajte potrebne vire** iz mape `solution/assets/` v mapo `your-work`; dodali boste datoteko `life.png`. Dodajte `lifeImg` v funkcijo window.onload: 

    ```javascript
    lifeImg = await loadTexture("assets/life.png");
    ```

1. Dodajte `lifeImg` na seznam virov:

    ```javascript
    let heroImg,
    ...
    lifeImg,
    ...
    eventEmitter = new EventEmitter();
    ```
  
2. **Dodajte spremenljivke**. Dodajte kodo, ki predstavlja vaš skupni rezultat (0) in preostala življenja (3), ter prikažite te vrednosti na zaslonu.

3. **Razširite funkcijo `updateGameObjects()`**. Razširite funkcijo `updateGameObjects()`, da bo obravnavala trke s sovražniki:

    ```javascript
    enemies.forEach(enemy => {
        const heroRect = hero.rectFromGameObject();
        if (intersectRect(heroRect, enemy.rectFromGameObject())) {
          eventEmitter.emit(Messages.COLLISION_ENEMY_HERO, { enemy });
        }
      })
    ```

4. **Dodajte `življenja` in `točke`**. 
   1. **Inicializirajte spremenljivke**. Pod `this.cooldown = 0` v razredu `Hero` nastavite življenje in točke:

        ```javascript
        this.life = 3;
        this.points = 0;
        ```

   1. **Narišite spremenljivke na zaslon**. Prikažite te vrednosti na zaslonu:

        ```javascript
        function drawLife() {
          // TODO, 35, 27
          const START_POS = canvas.width - 180;
          for(let i=0; i < hero.life; i++ ) {
            ctx.drawImage(
              lifeImg, 
              START_POS + (45 * (i+1) ), 
              canvas.height - 37);
          }
        }
        
        function drawPoints() {
          ctx.font = "30px Arial";
          ctx.fillStyle = "red";
          ctx.textAlign = "left";
          drawText("Points: " + hero.points, 10, canvas.height-20);
        }
        
        function drawText(message, x, y) {
          ctx.fillText(message, x, y);
        }

        ```

   1. **Dodajte metode v zanko igre**. Prepričajte se, da ste te funkcije dodali v funkcijo window.onload pod `updateGameObjects()`:

        ```javascript
        drawPoints();
        drawLife();
        ```

1. **Uvedite pravila igre**. Uvedite naslednja pravila igre:

   1. **Za vsako trčenje junaka in sovražnika** odštejte eno življenje.
   
      Razširite razred `Hero`, da izvedete to odštevanje:

        ```javascript
        decrementLife() {
          this.life--;
          if (this.life === 0) {
            this.dead = true;
          }
        }
        ```

   2. **Za vsak laser, ki zadene sovražnika**, povečajte rezultat igre za 100 točk.

      Razširite razred `Hero`, da izvedete to povečanje:
    
        ```javascript
          incrementPoints() {
            this.points += 100;
          }
        ```

        Dodajte te funkcije v svoje oddajnike dogodkov trčenja:

        ```javascript
        eventEmitter.on(Messages.COLLISION_ENEMY_LASER, (_, { first, second }) => {
           first.dead = true;
           second.dead = true;
           hero.incrementPoints();
        })

        eventEmitter.on(Messages.COLLISION_ENEMY_HERO, (_, { enemy }) => {
           enemy.dead = true;
           hero.decrementLife();
        });
        ```

✅ Raziščite, katere druge igre so ustvarjene z uporabo JavaScript/Canvas. Katere so njihove skupne značilnosti?

Ko boste končali to delo, bi morali videti majhne ladjice za življenja v spodnjem desnem kotu, točke v spodnjem levem kotu, in videti, kako se število življenj zmanjšuje ob trkih s sovražniki ter točke povečujejo, ko streljate na sovražnike. Odlično! Vaša igra je skoraj končana.

---

## 🚀 Izziv

Vaša koda je skoraj končana. Ali si lahko zamislite naslednje korake?

## Kviz po predavanju

[Kviz po predavanju](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/38)

## Pregled in samostojno učenje

Raziščite načine, kako lahko povečujete in zmanjšujete točke in življenja v igri. Obstajajo zanimivi igralni pogoni, kot je [PlayFab](https://playfab.com). Kako bi uporaba enega od teh izboljšala vašo igro?

## Naloga

[Ustvari igro s točkovanjem](assignment.md)

---

**Omejitev odgovornosti**:  
Ta dokument je bil preveden z uporabo storitve za strojno prevajanje [Co-op Translator](https://github.com/Azure/co-op-translator). Čeprav si prizadevamo za natančnost, vas prosimo, da upoštevate, da lahko avtomatizirani prevodi vsebujejo napake ali netočnosti. Izvirni dokument v njegovem maternem jeziku je treba obravnavati kot avtoritativni vir. Za ključne informacije priporočamo profesionalni človeški prevod. Ne prevzemamo odgovornosti za morebitne nesporazume ali napačne razlage, ki izhajajo iz uporabe tega prevoda.