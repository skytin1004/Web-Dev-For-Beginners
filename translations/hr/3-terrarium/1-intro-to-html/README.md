<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "46a0639e719b9cf1dfd062aa24cad639",
  "translation_date": "2025-08-27T23:59:59+00:00",
  "source_file": "3-terrarium/1-intro-to-html/README.md",
  "language_code": "hr"
}
-->
# Projekt Terarij, 1. dio: Uvod u HTML

![Uvod u HTML](../../../../translated_images/webdev101-html.4389c2067af68e98280c1bde52b6c6269f399eaae3659b7c846018d8a7b0bbd9.hr.png)
> Sketchnote autor [Tomomi Imura](https://twitter.com/girlie_mac)

## Kviz prije predavanja

[Kviz prije predavanja](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/15)

> Pogledajte video

> 
> [![Video o osnovama Gita i GitHuba](https://img.youtube.com/vi/1TvxJKBzhyQ/0.jpg)](https://www.youtube.com/watch?v=1TvxJKBzhyQ)

### Uvod

HTML, ili HyperText Markup Language, je 'kostur' weba. Ako CSS 'odijeva' vaš HTML, a JavaScript ga oživljava, HTML je tijelo vaše web aplikacije. Sintaksa HTML-a čak odražava tu ideju, jer uključuje oznake "head", "body" i "footer".

U ovoj lekciji koristit ćemo HTML za postavljanje 'kostura' sučelja našeg virtualnog terarija. Imat će naslov i tri stupca: desni i lijevi stupac gdje će se nalaziti biljke koje se mogu povlačiti, te središnji dio koji će biti stvarni terarij koji izgleda kao staklo. Na kraju ove lekcije moći ćete vidjeti biljke u stupcima, ali sučelje će izgledati pomalo čudno; ne brinite, u sljedećem dijelu dodati ćete CSS stilove kako bi sučelje izgledalo bolje.

### Zadatak

Na svom računalu stvorite mapu pod nazivom 'terrarium' i unutar nje datoteku pod nazivom 'index.html'. To možete učiniti u Visual Studio Code nakon što stvorite mapu terarija tako da otvorite novi prozor VS Code-a, kliknete 'open folder' i odete do svoje nove mape. Kliknite mali gumb 'file' u Explorer panelu i stvorite novu datoteku:

![explorer u VS Code](../../../../translated_images/vs-code-index.e2986cf919471eb984a0afef231380c8b132b000635105f2397bd2754d1b689c.hr.png)

Ili

Koristite ove naredbe u svom git bashu:
* `mkdir terrarium`
* `cd terrarium`
* `touch index.html`
* `code index.html` ili `nano index.html`

> Datoteke index.html označavaju pregledniku da je to zadana datoteka u mapi; URL-ovi poput `https://anysite.com/test` mogu biti izgrađeni pomoću strukture mapa koja uključuje mapu pod nazivom `test` s `index.html` unutar nje; `index.html` ne mora biti prikazan u URL-u.

---

## DocType i html oznake

Prvi redak HTML datoteke je njezin doctype. Pomalo je iznenađujuće da morate imati ovaj redak na samom vrhu datoteke, ali on govori starijim preglednicima da stranica treba biti prikazana u standardnom načinu rada, slijedeći trenutnu HTML specifikaciju.

> Savjet: u VS Code-u možete zadržati pokazivač iznad oznake i dobiti informacije o njezinoj upotrebi iz MDN Reference vodiča.

Drugi redak trebao bi biti početna oznaka `<html>`, odmah praćena zatvarajućom oznakom `</html>`. Ove oznake su korijenski elementi vašeg sučelja.

### Zadatak

Dodajte ove retke na vrh svoje datoteke `index.html`:

```HTML
<!DOCTYPE html>
<html></html>
```

✅ Postoji nekoliko različitih načina rada koji se mogu odrediti postavljanjem DocType-a s upitnim nizom: [Quirks Mode i Standards Mode](https://developer.mozilla.org/docs/Web/HTML/Quirks_Mode_and_Standards_Mode). Ovi načini rada koristili su se za podršku stvarno starim preglednicima koji se danas obično ne koriste (Netscape Navigator 4 i Internet Explorer 5). Možete se držati standardne deklaracije doctype-a.

---

## Dokumentov 'head'

Područje 'head' HTML dokumenta uključuje ključne informacije o vašoj web stranici, poznate i kao [metadata](https://developer.mozilla.org/docs/Web/HTML/Element/meta). U našem slučaju, web poslužitelju kojem će ova stranica biti poslana za prikazivanje, govorimo ove četiri stvari:

-   naslov stranice
-   metapodaci stranice uključujući:
    -   'character set', koji govori o tome koja se kodna stranica koristi na stranici
    -   informacije o pregledniku, uključujući `x-ua-compatible` koji označava da je podržan preglednik IE=edge
    -   informacije o tome kako bi se viewport trebao ponašati kada se učita. Postavljanje viewporta na početnu skalu od 1 kontrolira razinu zumiranja kada se stranica prvi put učita.

### Zadatak

Dodajte blok 'head' svom dokumentu između početne i završne oznake `<html>`.

```html
<head>
	<title>Welcome to my Virtual Terrarium</title>
	<meta charset="utf-8" />
	<meta http-equiv="X-UA-Compatible" content="IE=edge" />
	<meta name="viewport" content="width=device-width, initial-scale=1" />
</head>
```

✅ Što bi se dogodilo ako postavite meta oznaku viewporta ovako: `<meta name="viewport" content="width=600">`? Pročitajte više o [viewportu](https://developer.mozilla.org/docs/Web/HTML/Viewport_meta_tag).

---

## Dokumentov `body`

### HTML oznake

U HTML-u dodajete oznake svojoj .html datoteci kako biste stvorili elemente web stranice. Svaka oznaka obično ima početnu i završnu oznaku, poput ove: `<p>hello</p>` za označavanje paragrafa. Stvorite tijelo svog sučelja dodavanjem skupa `<body>` oznaka unutar para `<html>` oznaka; vaš markup sada izgleda ovako:

### Zadatak

```html
<!DOCTYPE html>
<html>
	<head>
		<title>Welcome to my Virtual Terrarium</title>
		<meta charset="utf-8" />
		<meta http-equiv="X-UA-Compatible" content="IE=edge" />
		<meta name="viewport" content="width=device-width, initial-scale=1" />
	</head>
	<body></body>
</html>
```

Sada možete početi graditi svoju stranicu. Obično koristite `<div>` oznake za stvaranje zasebnih elemenata na stranici. Stvorit ćemo niz `<div>` elemenata koji će sadržavati slike.

### Slike

Jedna HTML oznaka koja ne treba završnu oznaku je `<img>` oznaka, jer ima element `src` koji sadrži sve informacije potrebne stranici za prikazivanje stavke.

Stvorite mapu u svojoj aplikaciji pod nazivom `images` i u nju dodajte sve slike iz [source code folder](../../../../3-terrarium/solution/images); (ima 14 slika biljaka).

### Zadatak

Dodajte te slike biljaka u dva stupca između oznaka `<body></body>`:

```html
<div id="page">
	<div id="left-container" class="container">
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant1" src="./images/plant1.png" />
		</div>
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant2" src="./images/plant2.png" />
		</div>
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant3" src="./images/plant3.png" />
		</div>
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant4" src="./images/plant4.png" />
		</div>
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant5" src="./images/plant5.png" />
		</div>
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant6" src="./images/plant6.png" />
		</div>
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant7" src="./images/plant7.png" />
		</div>
	</div>
	<div id="right-container" class="container">
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant8" src="./images/plant8.png" />
		</div>
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant9" src="./images/plant9.png" />
		</div>
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant10" src="./images/plant10.png" />
		</div>
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant11" src="./images/plant11.png" />
		</div>
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant12" src="./images/plant12.png" />
		</div>
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant13" src="./images/plant13.png" />
		</div>
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant14" src="./images/plant14.png" />
		</div>
	</div>
</div>
```

> Napomena: Spans vs. Divs. Divs se smatraju 'blok' elementima, a Spans 'inline'. Što bi se dogodilo ako biste ove divove pretvorili u spanove?

S ovim markupom biljke se sada prikazuju na ekranu. Izgleda prilično loše, jer još nisu stilizirane pomoću CSS-a, a to ćemo učiniti u sljedećoj lekciji.

Svaka slika ima alt tekst koji će se pojaviti čak i ako ne možete vidjeti ili prikazati sliku. Ovo je važan atribut za uključivanje radi pristupačnosti. Saznajte više o pristupačnosti u budućim lekcijama; za sada, zapamtite da atribut alt pruža alternativne informacije za sliku ako korisnik iz nekog razloga ne može vidjeti (zbog sporog povezivanja, pogreške u atributu src ili ako korisnik koristi čitač ekrana).

✅ Jeste li primijetili da svaka slika ima isti alt tag? Je li to dobra praksa? Zašto ili zašto ne? Možete li poboljšati ovaj kod?

---

## Semantički markup

Općenito, poželjno je koristiti značajne 'semantike' prilikom pisanja HTML-a. Što to znači? To znači da koristite HTML oznake za predstavljanje vrste podataka ili interakcije za koje su dizajnirane. Na primjer, glavni naslov na stranici trebao bi koristiti oznaku `<h1>`.

Dodajte sljedeći redak odmah ispod svoje početne oznake `<body>`:

```html
<h1>My Terrarium</h1>
```

Korištenje semantičkog markupa, poput korištenja zaglavlja `<h1>` i nedefiniranih popisa kao `<ul>`, pomaže čitačima ekrana da se kreću kroz stranicu. Općenito, gumbi bi trebali biti napisani kao `<button>` a popisi kao `<li>`. Iako je _moguće_ koristiti posebno stilizirane `<span>` elemente s click handlerima za simulaciju gumba, bolje je za korisnike s invaliditetom koristiti tehnologije za određivanje gdje se na stranici nalazi gumb i interakciju s njim, ako se element pojavljuje kao gumb. Iz tog razloga, pokušajte koristiti semantički markup što je više moguće.

✅ Pogledajte čitač ekrana i [kako komunicira s web stranicom](https://www.youtube.com/watch?v=OUDV1gqs9GA). Možete li vidjeti zašto bi nesemantički markup mogao frustrirati korisnika?

## Terarij

Posljednji dio ovog sučelja uključuje stvaranje markupa koji će biti stiliziran za stvaranje terarija.

### Zadatak:

Dodajte ovaj markup iznad posljednje oznake `</div>`:

```html
<div id="terrarium">
	<div class="jar-top"></div>
	<div class="jar-walls">
		<div class="jar-glossy-long"></div>
		<div class="jar-glossy-short"></div>
	</div>
	<div class="dirt"></div>
	<div class="jar-bottom"></div>
</div>
```

✅ Iako ste dodali ovaj markup na ekran, apsolutno ništa se ne prikazuje. Zašto?

---

## 🚀Izazov

Postoje neki zanimljivi 'stariji' HTML tagovi koji su još uvijek zabavni za igranje, iako ne biste trebali koristiti zastarjele oznake poput [ovih oznaka](https://developer.mozilla.org/docs/Web/HTML/Element#Obsolete_and_deprecated_elements) u svom markupu. Ipak, možete li koristiti staru oznaku `<marquee>` da učinite da naslov h1 klizi vodoravno? (ako to učinite, ne zaboravite je ukloniti nakon toga)

## Kviz nakon predavanja

[Kviz nakon predavanja](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/16)

## Pregled i samostalno učenje

HTML je 'provjereni' sustav gradnje koji je pomogao izgraditi web u ono što je danas. Naučite malo o njegovoj povijesti proučavajući neke stare i nove oznake. Možete li shvatiti zašto su neke oznake zastarjele, a neke dodane? Koje oznake bi mogle biti uvedene u budućnosti?

Saznajte više o izradi stranica za web i mobilne uređaje na [Microsoft Learn](https://docs.microsoft.com/learn/modules/build-simple-website/?WT.mc_id=academic-77807-sagibbon).

## Zadatak

[Vježbajte svoj HTML: Izradite mockup bloga](assignment.md)

---

**Odricanje od odgovornosti**:  
Ovaj dokument je preveden pomoću AI usluge za prevođenje [Co-op Translator](https://github.com/Azure/co-op-translator). Iako nastojimo osigurati točnost, imajte na umu da automatski prijevodi mogu sadržavati pogreške ili netočnosti. Izvorni dokument na izvornom jeziku treba smatrati autoritativnim izvorom. Za kritične informacije preporučuje se profesionalni prijevod od strane čovjeka. Ne preuzimamo odgovornost za bilo kakve nesporazume ili pogrešne interpretacije koje proizlaze iz korištenja ovog prijevoda.