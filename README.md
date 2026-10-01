# SpaceX Falcon 9 – Colectarea datelor prin Web Scraping

Notebook de laborator (IBM Data Science – Capstone, Modulul 1) în care se extrag date despre lansările Falcon 9 și Falcon Heavy din tabelele paginii Wikipedia *List of Falcon 9 and Falcon Heavy launches*, folosind `requests` și `BeautifulSoup`.

## Conținut

Fișier: `module1_Complete_the_Data_Collection_with_Web_Scraping_lab.ipynb`

## Ce conține notebook-ul

1. **Importuri**: `requests`, `BeautifulSoup` (bs4), `re`, `unicodedata`, `pandas`.
2. **Funcții helper** pentru parsarea celulelor din tabelul HTML:
   - `date_time` – extrage data și ora lansării
   - `booster_version` – extrage versiunea boosterului
   - `landing_status` – extrage starea aterizării
   - `get_mass` – extrage masa încărcăturii (în kg) și normalizează textul Unicode
   - `extract_column_from_header` – curăță antetele coloanelor (elimină `<br>`, `<a>`, `<sup>`) și ignoră numele formate doar din cifre
3. **Configurare request**:
   - `static_url` – versiune arhivată a paginii Wikipedia (`oldid=1027686922`), pentru rezultate reproductibile
   - `headers` cu un `User-Agent` de browser
4. **Request și parsare**: se face `requests.get(...)`, se afișează codul de status și se creează obiectul `BeautifulSoup`, apoi se verifică titlul paginii.

## Stadiul curent

Notebook-ul este **incomplet**. Ultima celulă rulată a returnat:

```
403
Wikimedia Error
```

Wikipedia a respins cererea (HTTP 403), deci tabelele nu au fost încă extrase și `DataFrame`-ul final nu a fost construit. Ce urmează în laborator:

- găsirea tuturor tabelelor cu `soup.find_all('table')`
- extragerea antetelor și a rândurilor cu funcțiile helper
- construirea unui dicționar de coloane (`Flight No.`, `Launch site`, `Payload`, `Payload mass`, `Orbit`, `Customer`, `Launch outcome`, `Version Booster`, `Booster landing`, `Date`, `Time`) și conversia într-un `DataFrame`
- salvarea rezultatului într-un CSV

## Depanarea erorii 403

Politica Wikimedia cere un `User-Agent` care identifică clar aplicația, iar cei care imită un browser sunt adesea blocați. Variante:

- folosește un User-Agent descriptiv, cu date de contact, de exemplu:
  `"SpaceXLab/1.0 (contact: adresa_ta@example.com)"`
- încearcă API-ul oficial Wikipedia (`action=parse` sau REST) în loc de scraping direct
- folosește varianta statică a paginii oferită de curs, dacă există în materialele laboratorului
- pe mașini din rețele partajate (VPN, cloud), IP-ul poate fi blocat; încearcă din altă rețea

## Cerințe

- Python 3.8+
- Jupyter Notebook / JupyterLab
- Pachete: `requests`, `beautifulsoup4`, `pandas`

```bash
pip install requests beautifulsoup4 pandas
```

> Notă: metadatele notebook-ului indică Python 2.7 (`language_info`), dar codul necesită Python 3. Kernelul folosit la rulare trebuie să fie Python 3.

## Rulare

```bash
jupyter notebook module1_Complete_the_Data_Collection_with_Web_Scraping_lab.ipynb
```

Rulează celulele în ordine. Este nevoie de conexiune la internet.

## Sursă de date

- Wikipedia: *List of Falcon 9 and Falcon Heavy launches* (revizia arhivată `1027686922`)

## Legătură cu restul proiectului

Datele obținute prin scraping completează datele din SpaceX API (notebook-ul *Data Collection API*) și formează baza pentru etapele de data wrangling, EDA și modelare.
