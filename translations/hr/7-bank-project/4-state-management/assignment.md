<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "f23a868536c07da991b1d4e773161e25",
  "translation_date": "2025-08-27T23:23:51+00:00",
  "source_file": "7-bank-project/4-state-management/assignment.md",
  "language_code": "hr"
}
-->
# Implementirajte dijalog "Dodaj transakciju"

## Upute

Našoj aplikaciji za bankarstvo još uvijek nedostaje jedna važna značajka: mogućnost unosa novih transakcija. 
Koristeći sve što ste naučili u prethodne četiri lekcije, implementirajte dijalog "Dodaj transakciju":

- Dodajte gumb "Dodaj transakciju" na stranici nadzorne ploče
- Ili kreirajte novu stranicu s HTML predloškom, ili koristite JavaScript za prikaz/sakrivanje HTML dijaloga bez napuštanja stranice nadzorne ploče (možete koristiti svojstvo [`hidden`](https://developer.mozilla.org/docs/Web/HTML/Global_attributes/hidden) za to, ili CSS klase)
- Osigurajte da obradite [pristupačnost za tipkovnicu i čitače ekrana](https://developer.paciellogroup.com/blog/2018/06/the-current-state-of-modal-dialog-accessibility/) za dijalog
- Implementirajte HTML obrazac za unos podataka
- Kreirajte JSON podatke iz podataka obrasca i pošaljite ih na API
- Ažurirajte stranicu nadzorne ploče s novim podacima

Pogledajte [specifikacije API poslužitelja](../api/README.md) kako biste vidjeli koji API trebate pozvati i koji je očekivani JSON format.

Evo primjera rezultata nakon dovršetka zadatka:

![Snimka zaslona koja prikazuje primjer dijaloga "Dodaj transakciju"](../../../../translated_images/dialog.93bba104afeb79f12f65ebf8f521c5d64e179c40b791c49c242cf15f7e7fab15.hr.png)

## Rubrika

| Kriterij | Izvrsno                                                                                          | Zadovoljavajuće                                                                                                        | Potrebno poboljšanje                        |
| -------- | ------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------- | ------------------------------------------- |
|          | Dodavanje transakcije je potpuno implementirano slijedeći sve najbolje prakse iz lekcija.        | Dodavanje transakcije je implementirano, ali ne slijedi najbolje prakse iz lekcija, ili djeluje samo djelomično.       | Dodavanje transakcije uopće ne radi.        |

---

**Odricanje od odgovornosti**:  
Ovaj dokument je preveden pomoću AI usluge za prevođenje [Co-op Translator](https://github.com/Azure/co-op-translator). Iako nastojimo osigurati točnost, imajte na umu da automatski prijevodi mogu sadržavati pogreške ili netočnosti. Izvorni dokument na izvornom jeziku treba smatrati autoritativnim izvorom. Za kritične informacije preporučuje se profesionalni prijevod od strane čovjeka. Ne preuzimamo odgovornost za bilo kakve nesporazume ili pogrešne interpretacije koje proizlaze iz korištenja ovog prijevoda.