# Warmline Hierarchy Design

**Data:** 2026-04-15
**Scop:** Reorganizarea gamei Warmline in sectiunea Produse pentru navigare mai usoara si mai intuitiva.

## Context

Pagina `produse.html` actuala are carduri individuale pentru fiecare cazan Warmline (ex: Premium 17 kW, Premium 27 kW), amestecate cu celelalte branduri. Pe termoshop.ro insa gama Warmline are mult mai multe variante KW pentru fiecare model (Premium, Uni, Eco, Black Pellet, Monogravity). Daca pur si simplu adaugam toate variantele in `produse.html`, pagina devine foarte lunga si greu de scanat.

Utilizatorii cauta in general dupa:
1. **Tip combustibil** (lemne, peleti, gaz, electric)
2. **Putere / suprafata incalzita** (cat KW imi trebuie pentru casa mea?)
3. **Buget / nivel de automatizare**

## Decizie: Ierarhie pe 3 niveluri

```
produse.html           - hub general, carduri pe branduri/categorii
  │
  └─ warmline.html     - pagina brand, cele 5 modele Warmline
        │
        ├─ warmline-premium.html        - variantele KW pentru Premium
        ├─ warmline-uni.html            - variantele KW pentru Uni
        ├─ warmline-eco.html            - variantele KW pentru Eco
        ├─ warmline-black-pellet.html   - variantele KW pentru Black Pellet
        └─ warmline-monogravity.html    - variantele KW pentru Monogravity
```

**De ce pagini separate si nu totul in produse.html:**
- URL curat per model → bun pentru SEO (Google indexeaza fiecare model)
- Pagini mai scurte, se incarca rapid
- Scalabil: cand adaugam TIS, Neus, Kronas folosim acelasi pattern (`tis.html`, `tis-<model>.html` etc.)
- Navbar-ul arata tot "Produse" ca activ pe toate aceste pagini → vizitatorul percepe totul ca o singura sectiune

## Pagina brand: `warmline.html`

**Layout:** 5 carduri "pentru cine e potrivit" (grid 3+2 pe desktop, stack pe mobile).

Fiecare card contine:
- Imagine reprezentativa a modelului
- Nume mare (ex: "PREMIUM")
- Tagline emotional ("Pentru confort si performanta")
- 3 bullet-uri diferentiatoare (combustibil, eficienta, nr. variante)
- CTA "Vezi variantele" → `warmline-<model>.html`

Scop: vizitatorul intelege in 10 secunde care model e pentru el, fara sa citeasca specs tehnice.

**Sectiune secundara pe pagina:** Un mic FAQ / comparatie rapida intre cele 5 modele pentru cei care vor mai multe detalii (decidem in implementare daca o adaugam acum sau later).

## Pagina model: `warmline-premium.html` (si celelalte 4)

**Layout:**

1. **Hero** cu numele modelului si o descriere de 1-2 fraze
2. **Caseta verde "De cata putere ai nevoie?"** cu:
   - Input numeric pentru suprafata (m²)
   - Buton "Calculeaza"
   - Formula: `KW necesar ≈ m² / 10` (standard termic uzual pentru case izolate normal)
3. **Grid variante KW:** carduri cu putere, suprafata estimata, eficienta, combustibil, PDF manual, buton "Vreau oferta"
4. **Highlight interactiv:** dupa calcul, varianta cea mai apropiata de nevoia user-ului primeste:
   - Border colorat (verde)
   - Badge "POTRIVIT PENTRU TINE"
   - Scroll auto catre ea pe mobile
5. **Sectiune "Ce inseamna specs?"** (optional): explicatii scurte pentru eficienta, randament, tiraj etc. pentru vizitatorii care nu sunt tehnici

**CTA final** trimite la `contact.html` cu parametru URL pentru pre-completare: `?produs=Warmline+Premium+22kW`.

## Formula KW → m²

Standard uzual in HVAC pentru case cu izolatie normala: **~100 W/m² = 0.1 kW/m²**.

Deci: `KW_necesar = suprafata_m² / 10`

Exemple:
- 100 m² → 10 kW
- 170 m² → 17 kW
- 250 m² → 25 kW

In implementare, vom alege varianta cu KW >= necesarul calculat (nu undersize niciodata).

**Nota:** Adaugam o nota pe pagina ca formula e orientativa si depinde de izolatie, numar de etaje, zona climatica. Pentru calcul exact → "Cere consultanta gratuita".

## Date

Extragem din termoshop.ro (via WebFetch) pentru fiecare model:
- Lista variantelor KW disponibile
- Imagine produs (hotlink direct catre `termoshop.ro/wp-content/uploads/...`)
- PDF manual (hotlink)
- Specs: eficienta, suprafata, combustibil

Incepem cu **Warmline Premium** ca test. Dupa ce validezi cum arata live, extindem la celelalte 4 modele.

## Stil

Refolosim complet clasele existente din `styles.css`:
- `catalog-card`, `catalog-card-image`, `catalog-card-title`, `catalog-card-specs` etc.
- `btn-primary`, `hero`, `navbar`, `footer`
- Culorile brand (verde #16a34a / #15803d din brand-guidelines.md)

Clase noi (minimale):
- `kw-selector` — caseta verde cu input + buton
- `variant-card.is-recommended` — varianta highlighted dupa calcul
- `variant-badge` — badge-ul "POTRIVIT PENTRU TINE"

## JavaScript

Selector KW → variant highlight:
- Event listener pe butonul "Calculeaza"
- Parseaza `data-kw` de pe fiecare `.variant-card`
- Gaseste prima varianta cu `kw >= ceil(m²/10)`
- Adauga `.is-recommended` pe ea, scroll into view (smooth)
- Daca nicio varianta nu acopera → alert friendly: "Pentru suprafete foarte mari recomandam o consultanta personalizata"

Vanilla JS, fara dependinte. ~30 linii total.

## Impact asupra paginilor existente

**`produse.html`:**
- Cardurile individuale Warmline (Premium 17 kW, Premium 27 kW etc.) se inlocuiesc cu **un singur card "Warmline"** care linkeaza catre `warmline.html`
- Pastram filtrele existente (Toate / Lemne / Peleti etc.)
- Cardul Warmline apare in filtrul "lemne" si "peleti"

**`navbar` pe toate paginile noi:**
- Link-ul "Produse" ramane activ cand esti pe orice pagina din ierarhie (`warmline.html`, `warmline-premium.html` etc.)

**Celelalte branduri** (TIS, Neus, Kronas, Almax, Burnit):
- Raman pe `produse.html` ca acum, neschimbate
- Cand primim mai multe date, le migram la acelasi pattern (`tis.html` + `tis-<model>.html`)

## Pasi de implementare

1. ✅ Design doc (acest fisier)
2. Extract date Warmline Premium de pe termoshop.ro (WebFetch)
3. Construieste `warmline.html` (pagina brand cu cele 5 carduri)
4. Construieste `warmline-premium.html` (model + selector KW interactiv)
5. Update `produse.html` → card unic Warmline catre `warmline.html`
6. Adauga CSS pentru `kw-selector` si `variant-card.is-recommended`
7. Test live in browser, verifica pe mobile
8. Confirmare cu Ovidiu → extindem la Uni, Eco, Black Pellet, Monogravity

## De discutat dupa prima iteratie

- Adaugam FAQ/comparatie intre modele pe `warmline.html`?
- Pre-completare formular contact cu modelul/KW-ul selectat?
- Versiune mobila a selectorului KW — slider in loc de input?
- Dupa Warmline: ne gandim si la structura brand hub pentru TIS/Neus?
