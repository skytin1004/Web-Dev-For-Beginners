<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "5301875c55bb305e6046bed3a4fd06d2",
  "translation_date": "2025-08-28T00:06:54+00:00",
  "source_file": "quiz-app/README.md",
  "language_code": "hr"
}
-->
# Aplikacija za kviz

Ovi kvizovi su predavanja i kvizovi nakon predavanja za kurikulum znanosti o podacima na https://aka.ms/webdev-beginners

## Dodavanje prevedenog seta kvizova

Dodajte prijevod kviza stvaranjem odgovarajućih struktura kvizova u mapama `assets/translations`. Izvorni kvizovi nalaze se u `assets/translations/en`. Kvizovi su podijeljeni u nekoliko grupa. Pazite da uskladite numeraciju s odgovarajućim odjeljkom kviza. Ukupno postoji 40 kvizova u ovom kurikulumu, a brojanje počinje od 0.

  
<details>
<summary>Evo kako izgleda datoteka s prijevodom:</summary>

```
[
    {
        "title": "A title",
        "complete": "A complete button title",
        "error": "An error message upon selecting the wrong answer",
        "quizzes": [
            {
                "id": 1,
                "title": "Title",
                "quiz": [
                    {
                        "questionText": "The question asked",
                        "answerOptions": [
                            {
                                "answerText": "Option 1 title",
                                "isCorrect": true
                            },
                            {
                                "answerText": "Option 2 title",
                                "isCorrect": false
                            }
                        ]
                    }
                ]
            }
        ]
    }
]
```
</details>

Nakon uređivanja prijevoda, uredite datoteku index.js u mapi za prijevode kako biste uvezli sve datoteke prema konvencijama u `en`.

Uredite datoteku `index.js` u `assets/translations` kako biste uvezli nove prevedene datoteke. 

Na primjer, ako je vaš JSON prijevod u `ex.json`, koristite 'ex' kao ključ za lokalizaciju, a zatim ga unesite kao što je prikazano dolje za uvoz:

<details>
<summary>index.js</summary>

```
import ex from "./ex.json";

// if 'ex' is localization key then enter it like so in `messages` to expose it 

const messages = {
  ex: ex[0],
};

export default messages;
```

</details>

## Pokretanje aplikacije za kviz lokalno

### Preduvjeti

- GitHub račun
- [Node.js i Git](https://nodejs.org/)

### Instalacija i postavljanje

1. Stvorite repozitorij iz ovog [predloška](https://github.com/new?template_name=Web-Dev-For-Beginners&template_owner=microsoft) 

1. Klonirajte svoj novi repozitorij i idite na mapu quiz-app

   ```bash
   git clone https://github.com/your-github-organization/repo-name
   cd repo-name/quiz-app
   ```

1. Instalirajte npm pakete i ovisnosti

   ```bash
   npm install
   ```

### Izgradnja aplikacije

1. Za izgradnju rješenja pokrenite:

   ```bash
   npm run build
   ```

### Pokretanje aplikacije

1. Za pokretanje rješenja pokrenite:

    ```bash
    npm run dev
    ```

### [Opcionalno] Linting

1. Kako biste osigurali da je kod provjeren, pokrenite:

    ```bash
    npm run lint
    ```

## Postavljanje aplikacije za kviz na Azure 

### Preduvjeti
- Azure pretplata. Prijavite se za besplatnu [ovdje](https://aka.ms/azure-free).

    _Procjena troškova za postavljanje ove aplikacije za kviz: BESPLATNO_

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.StaticApp)

Nakon što se prijavite na Azure putem gornje poveznice, odaberite pretplatu i grupu resursa, a zatim:

- Detalji o statičkoj web aplikaciji: Unesite naziv i odaberite plan hostinga
- GitHub prijava: Postavite izvor implementacije kao GitHub, zatim se prijavite i ispunite potrebna polja u obrascu:
    - *Organizacija* – Odaberite svoju organizaciju.
    - *Repozitorij* – Odaberite repozitorij kurikuluma Web Dev for Beginners. 
    - *Grana* - Odaberite granu (main) 
- Predlošci za izgradnju: Azure Static Web Apps koristi algoritam za otkrivanje okvira korištenog u vašoj aplikaciji. 
    - *Lokacija aplikacije* - ./quiz-app
    - *Lokacija API-ja* -
    - *Lokacija izlaza* - dist
- Implementacija: Kliknite 'Review + Create', zatim 'Create'

    Nakon implementacije, datoteka tijeka rada bit će stvorena u *.github* direktoriju vašeg repozitorija. Ova datoteka tijeka rada sadrži upute o događajima koji će pokrenuti ponovnu implementaciju aplikacije na Azure, na primjer, _**push** na granu **main**_ itd.

    <details>
    <summary>Primjer datoteke tijeka rada</summary>
    Evo primjera kako bi datoteka tijeka rada za GitHub Actions mogla izgledati:
    name: Azure Static Web Apps CI/CD

    ```
    on:
    push:
        branches:
        - main
    pull_request:
        types: [opened, synchronize, reopened, closed]
        branches:
        - main

    jobs:
    build_and_deploy_job:
        runs-on: ubuntu-latest
        name: Build and Deploy Job
        steps:
        - uses: actions/checkout@v2
        - name: Build And Deploy
            id: builddeploy
            uses: Azure/static-web-apps-deploy@v1
            with:
            azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN }}
            repo_token: ${{ secrets.GITHUB_TOKEN }}
            action: "upload"
            app_location: "quiz-app" # App source code path
            api_location: ""API source code path optional
            output_location: "dist" #Built app content directory - optional
    ```

    </details>

- Nakon implementacije: Nakon što je implementacija dovršena, kliknite na 'Go to Deployment', a zatim 'View app in browser'.

Nakon što se vaš GitHub Action (tijek rada) uspješno izvrši, osvježite stranicu uživo kako biste vidjeli svoju aplikaciju.

---

**Odricanje od odgovornosti**:  
Ovaj dokument je preveden pomoću AI usluge za prevođenje [Co-op Translator](https://github.com/Azure/co-op-translator). Iako nastojimo osigurati točnost, imajte na umu da automatski prijevodi mogu sadržavati pogreške ili netočnosti. Izvorni dokument na izvornom jeziku treba smatrati autoritativnim izvorom. Za ključne informacije preporučuje se profesionalni prijevod od strane ljudskog prevoditelja. Ne preuzimamo odgovornost za bilo kakve nesporazume ili pogrešne interpretacije koje proizlaze iz korištenja ovog prijevoda.