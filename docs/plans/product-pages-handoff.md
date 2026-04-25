# Product Pages Handoff — Continuare sesiune

**Data:** 2026-04-16
**Scop:** Acest fisier e ghidul complet pentru continuarea muncii pe paginile de produse. Citeste-l la inceputul fiecarei sesiuni noi.

## Stare curenta

### GATA (nu modifica)
| Fisier | Ce contine | Status |
|--------|-----------|--------|
| `warmline.html` | Brand hub — 5 carduri (Premium, Uni, Eco, Black Pellet, Monogravity) | COMPLET |
| `warmline-premium.html` | 10 variante KW (17-200), calculator, preturi | COMPLET |
| `warmline-uni.html` | 5 variante KW + calculator | COMPLET |
| `warmline-eco.html` | 5 variante KW + calculator | COMPLET |
| `warmline-black-pellet.html` | 5 variante KW + calculator | COMPLET |
| `warmline-monogravity.html` | 3 variante KW + calculator | COMPLET |
| `tis.html` | Brand hub — 3 carduri (Uni, Pro, Pellet) | COMPLET |
| `tis-uni.html` | 10 variante KW (15-95), calculator, preturi | COMPLET |

### DE FACUT — in ordinea asta

#### Sesiune 1: TIS (restul)
1. **`tis-pro.html`** — Fetch date de pe termoshop.ro, creeaza pagina model cu variante KW + calculator
   - URL-uri termoshop.ro: cauta `tis pro` pe termoshop.ro (4 variante: 15-30 kW conform tis.html)
   - Template de referinta: `tis-uni.html` (copiaza structura exacta)
2. **`tis-pellet.html`** — La fel, fetch + creeaza
   - Probabil mai multe sub-modele (Pellet Combi, New Pellet etc.)
   - Daca sunt sub-modele diferite, creeaza pagini separate: `tis-pellet-combi.html`, `tis-new-pellet.html` si actualizeaza linkul din `tis.html`
3. **Update `produse.html`**: inlocuieste cardurile individuale TIS (Pro 25kW, Uni N 20kW, New Pellet 30kW - liniile 74-129) cu UN SINGUR card brand "Gama TIS" care trimite la `tis.html` (exact cum e cardul Warmline de pe liniile 55-72)

#### Sesiune 2: Neus
1. **`neus.html`** — Brand hub (fetch toate modelele Neus de pe termoshop.ro)
   - Modele cunoscute deja pe produse.html: Turbo (25kW, 35kW), Praktik (30kW), Compact (24-50kW)
   - Fa search pe termoshop.ro: `neus` pentru lista completa
2. **`neus-turbo.html`**, **`neus-praktik.html`**, **`neus-compact.html`** etc. — cate o pagina per model cu variantele KW
3. **Update `produse.html`**: inlocuieste cardurile individuale Neus (liniile 132-186) cu un card brand

#### Sesiune 3: Kronas
1. **`kronas.html`** — Brand hub
   - Modele pe produse.html: Eko 24kW, Standart 26kW
   - Search termoshop.ro: `kronas` pentru toate
2. **`kronas-eko.html`**, **`kronas-standart.html`** etc.
3. **Update `produse.html`**: card brand Kronas

#### Sesiune 4: Almax
1. **`almax.html`** — Brand hub
   - Modele pe produse.html: Class D 25kW, Class B (16/21/28/33 kW)
   - Search termoshop.ro: `almax`
2. **`almax-class-d.html`**, **`almax-class-b.html`** etc.
3. **Update `produse.html`**: card brand Almax

#### Sesiune 5: Burnit
1. **`burnit.html`** — Brand hub
   - Modele pe produse.html: NWB 25kW, NWB 30kW
   - Din terminal output sesiunea anterioara: NWB Prime (50, 70, 90, 110 kW) — deja fetched
   - Search termoshop.ro: `burnit` pentru toate
2. **`burnit-nwb.html`**, **`burnit-nwb-prime.html`** etc.
3. **Update `produse.html`**: card brand Burnit

## Pattern de creare pagina model (template)

Fiecare pagina de model (ex: `tis-pro.html`) urmeaza **exact** structura din `tis-uni.html`:

1. **`<head>`**: meta title/description, link styles.css, `<style>` bloc cu clasele: breadcrumb, kw-selector, kw-form, kw-result, variant-card.is-recommended, price-box, info-note
2. **Navbar**: identic pe toate paginile, cu `class="active"` pe Produse
3. **Hero** cu breadcrumb: `Produse / [Brand] / [Model]`
4. **KW Selector** (caseta portocalie): input suprafata + buton Calculeaza
5. **Catalog grid** cu variant-card-uri: fiecare card are `data-kw="X"`, poza, specs (putere, suprafata, eficienta, combustibil, otel), price-box (RON + EUR), Manual PDF link, CTA "Cere oferta" cu `?produs=...`
6. **Info note**: 3-4 paragrafe descriptive
7. **CTA section** + **Footer** (identice)
8. **`<script>`**: functia `calculateKW()` identica, doar se schimba numele modelului in mesajul de rezultat

## Pattern de creare brand hub (template)

Fiecare brand hub (ex: `neus.html`) urmeaza structura din `tis.html`:

1. Navbar cu Produse activ
2. Hero cu breadcrumb simplu: `Produse / [Brand]`
3. Sectiune intro cu titlu si descriere
4. Catalog grid cu cate un card per model (tagline, specs sumarizate, CTA "Vezi variantele")
5. CTA section + Footer

## Reguli importante

- **Hotlink imagini** direct de pe termoshop.ro/wp-content/uploads/... (nu downloada)
- **Hotlink PDF-uri** de pe termoshop.ro
- **Preturi in RON** cu conversie estimata EUR (1 EUR ≈ 5 RON)
- **Formula KW**: `suprafata_m2 / 10`
- **CTA link**: `contact.html?produs=[Brand]+[Model]+[X]kW`
- **Stil CSS**: refolosim clasele din styles.css (catalog-card, btn-primary etc.)
- **data-cat pe produse.html**: `lemne` sau `peleti` dupa combustibilul principal
- **Comanda user**: cand Ovidiu spune "continua cu [brand]", citeste acest fisier, fetch de pe termoshop.ro, si creeaza paginile

## Preturi Warmline — COMPLET (2026-04-16)

Toate preturile au fost adaugate in cele 5 fisiere Warmline. CSS `.price-box` adaugat in fiecare `<style>` bloc. HTML `<div class="price-box">` inserat inainte de `<div class="catalog-card-footer">` in fiecare card.

**Premium**: 17→8.918, 21→9.486, 27→10.449, 33→11.702, 42→12.943, 55→15.484, 75→27.132, 98→36.552, 150→44.754, 200→52.842 lei
**Uni**: 16→7.330, 21→8.124, 27→8.895, 33→9.672, 42→10.636 lei
**Eco**: 16→6.288, 20→6.219, 25→6.996, 30→7.756, 40→8.742 lei
**Black Pellet**: 15→15.660, 20→16.156, 25→16.800, 30→17.400, 40→20.070 lei
**Monogravity**: 20→11.610, 25→12.510, 30→13.410 lei

## Sesiunea 2026-04-16 — CE S-A FACUT (COMPLET)

### Pompe de caldura — COMPLET
- [x] `sunsystem.html` — brand hub (2 carduri: Mono Plus, Split Plus)
- [x] `sunsystem-mono-plus.html` — 4 variante: 6kW/10.700, 9kW/12.400, 13kW/13.400, **16kW/19.900 lei (380V)**
- [x] `sunsystem-split-plus.html` — 5 variante: 6/13.734, 9/15.984, 13/17.550, 18.5/22.410, 20/23.310 lei
- [x] `termoshop-r290.html` — 3 variante: 6kW/12.255, 9kW/14.155, 20kW/23.085 lei (R290, A+++)
- [x] `produse.html` — placeholder pompe inlocuit cu carduri reale: Sunsystem + Termoshop R290
- [x] `produse.html` — filter JS actualizat pentru data-cat cu spatii (lemne peleti)

### Climatizare — PARTIAL (hub gata, pagini modele DE FACUT)
- [x] `rotenso.html` — brand hub cu 12 modele grupate (8 split perete + 4 tipuri speciale)
- [x] `produse.html` — placeholder climatizare inlocuit cu card Rotenso real

---

## URMATOAREA SESIUNE: Rotenso — pagini modele individuale

### Date colectate (nu mai trebuie fetch)

**Calculator BTU pentru AC:** `needed_btu = suprafata_m2 * 250`
Ghid orientativ afisabil pe pagina: 9k BTU ≤ 35 m² | 12k BTU 35-50 m² | 18k BTU 50-70 m² | 24k BTU 70-90 m²

**Template pagina model AC** = identic cu cazanele (sunsystem-mono-plus.html), cu 2 diferente:
1. `data-btu="9000"` in loc de `data-kw="6"` pe fiecare variant-card
2. Formula calculator: `var needed = suprafata * 250;` si compara cu `parseInt(c.dataset.btu, 10)`
3. Afiseaza BTU pe card, nu kW (sau ambele: "9.000 BTU / ~2,6 kW")

**URL-uri termoshop.ro pentru fetch date (nu au fost accesate inca):**
- Roni: `termoshop.ro/produs/aparat-de-aer-conditionat-rotenso-roni/`
- Ukura non-X: `termoshop.ro/produs/aparat-de-aer-conditionat-rotenso-ukura-2/`
- Ukura X: `termoshop.ro/produs/aparat-de-aer-conditionat-rotenso-ukura/`
- Elis X: `termoshop.ro/produs/aparatul-de-aer-conditionat-rotenso-elis-x-silver-black/`
- Imoto X: `termoshop.ro/produs/aparat-de-aer-conditionat-rotenso-imoto-x/`
- Versu: `termoshop.ro/produs/aparat-de-aer-conditionat-rotenso-versu/`
- Revio X: `termoshop.ro/produs/aparat-de-aer-conditionat-rotenso-revio-x/`
- Mirai X Multi: `termoshop.ro/produs/aparat-de-aer-conditionat-rotenso-mirai-x/`
- Aneru X: `termoshop.ro/produs/aparat-de-aer-conditionat-tip-consola-rotenso-aneru-x/`
- Jato: `termoshop.ro/produs/aparat-de-aer-conditionat-rotenso-jato-x/`
- Tenji caseta: `termoshop.ro/produs/aparat-de-aer-conditionat-caseta-rotenso-tenji/`
- Nevo canal: `termoshop.ro/produs/aparat-de-aer-conditionat-canal-rotenso-nevo-x/`

**Date deja colectate (nu mai fetch):**
| Model | BTU | Pret de la | Clase | SEER | SCOP | Note |
|-------|-----|-----------|-------|------|------|------|
| Roni X | 9k-24k | 1.366 lei | A++/A+ | 6,1 | 4,0 | -20°C, filtru 3-in-1, Wi-Fi |
| Elis X | 9k-24k | 1.658 lei | A++/A+ | 6,1 | 4,0 | Silver/Black, -20°C |
| Imoto X | 9k-24k | 1.717 lei | A+++/A++ | 9,3 | 4,6 | sticla acrilica, -22°C |
| Ukura X | 9k-24k | 1.785 lei | A++/A+ | 6,1-7,2 | 4,0-4,1 | 4D airflow, -20°C |
| Versu | 9k-18k | 2.475 lei | A+++/A++ | pana la 8,8 | 4,6 | 19dB, White/Mirror/Silver/Gold, -22°C |
| Revio X | 9k-24k | 2.772 lei | A+++/A++ | 8,5-8,6 | 4,2-4,6 | **-25°C**, ionizare |
| Jato X | 18k-60k | 4.654 lei | A++/A+ | 6,1-6,3 | 4,0-4,1 | tavan/podea |
| Mirai X | 9k-12k | 3.958 lei | - | - | - | multi-split, fetch complet |
| Aneru X | 9k-18k | 3.961 lei | - | - | - | consola, fetch complet |
| Tenji CC X | BTU n/a | 4.296 lei | - | - | - | caseta 360°, fetch complet |
| Nevo X | 12k-60k | 4.378 lei | - | - | - | canal tubulatura, fetch complet |
| Ukura | 9k-24k | 1.495 lei | - | - | - | versiunea mai simpla, fetch complet |

**IMAGINI:** Toate imaginile sunt placeholder (termoshop.ro le incarca prin JS). Ovidiu trebuie sa dea URL-urile manual din browser (click dreapta → copie adresa imagine) sau sa le puna in IMAGES/.

### Pagini de creat in urmatoarea sesiune (in ordine)

Prioritate 1 — cele mai populare (split perete entry/mid):
1. ~~`rotenso-roni.html`~~ — **COMPLET** (2026-04-16)
2. ~~`rotenso-elis-x.html`~~ — **COMPLET** (2026-04-16)
3. ~~`rotenso-imoto-x.html`~~ — **COMPLET** (2026-04-16)
4. ~~`rotenso-revio-x.html`~~ — **COMPLET** (2026-04-16)

Prioritate 2 — mid-range:
5. ~~`rotenso-ukura.html`~~ — **COMPLET** (2026-04-17) — 4 variante: 9k/1.495, 12k/1.785, 18k/2.500, 24k/3.100 lei
6. ~~`rotenso-ukura-x.html`~~ — **COMPLET** (2026-04-17) — 4 variante: 9k/1.785, 12k/1.785, 18k/3.130, 24k/4.146 lei
7. ~~`rotenso-versu.html`~~ — **COMPLET** (2026-04-17) — 3 variante: 9k/2.475, 12k/2.870, 18k/3.500 lei (estimat); 4 culori

Prioritate 3 — tipuri speciale:
8. ~~`rotenso-aneru-x.html`~~ — **COMPLET** (2026-04-17) — 3 variante: 9k/3.961, 12k/4.539, 18k/5.117 lei
9. ~~`rotenso-jato.html`~~ — **COMPLET** (2026-04-17) — 5 variante: 18k/4.654, 24k/6.280, 36k/8.906, 48k/10.627, 60k/12.347 lei
10. ~~`rotenso-tenji.html`~~ — **COMPLET** (2026-04-17) — 8 variante: 12k/4.296...60k/12.900 lei
11. ~~`rotenso-nevo.html`~~ — **COMPLET** (2026-04-17) — 8 variante: 12k/4.378...60k/12.530 lei
12. ~~`rotenso-mirai-x.html`~~ — **COMPLET** (2026-04-17) — 2 variante: 9k/3.958, 12k/4.176 lei (A+++, SEER 9.3)

---

## Sesiunea 2026-04-17 — CE S-A FACUT (COMPLET)

### Rotenso — toate paginile modele COMPLETE
- [x] `rotenso-ukura.html` — 4 variante: 9k/1.495, 12k/1.785, 18k/2.500, 24k/3.100 lei (A++, SEER 6.5-7.2)
- [x] `rotenso-ukura-x.html` — 4 variante: 9k/1.785, 12k/1.785, 18k/3.130, 24k/4.146 lei (A++, Super Ionizer)
- [x] `rotenso-versu.html` — 3 variante: 9k/2.475, 12k/2.870, 18k/3.500 lei; 4 culori; A+++, SEER 8.8, 19 dB, -22°C
- [x] `rotenso-aneru-x.html` — 3 variante consola: 9k/3.961, 12k/4.539, 18k/5.117 lei (A++, SEER 6.7-7.4)
- [x] `rotenso-jato.html` — 5 variante tavan/podea: 18k/4.654...60k/12.347 lei (A++, Eurovent)
- [x] `rotenso-tenji.html` — 8 variante caseta 360°: 12k/4.296...60k/12.900 lei (A++, pompa condensat)
- [x] `rotenso-nevo.html` — 8 variante canal: 12k/4.378...60k/12.530 lei (A++, 160 Pa, pompa condensat)
- [x] `rotenso-mirai-x.html` — 2 variante multi-split: 9k/3.958, 12k/4.176 lei (A+++, SEER 9.3, SCOP 5.3)
- [x] `rotenso.html` — hub-ul era deja pregatit cu toate linkurile corecte

**STATUS ROTENSO: 100% COMPLET** — toate 12 modele au pagini individuale

---

## Sesiunea 2026-04-17 (tarziu) — CE S-A FACUT

### UX produse.html — COMPLET
- [x] Tab Climatizare: split in 2 taburi noi — "AC Split Perete" (`ac-split`) + "AC Tipuri Speciale" (`ac-speciale`)
- [x] rotenso.html: 2 sectiuni cu `id="section-split"` si `id="section-speciale"`, JS ascunde sectiunea gresita la `?section=split` / `?section=speciale`
- [x] Carduri produse.html: "AC Split de Perete" → `rotenso.html?section=split`, "AC Tipuri Speciale" → `rotenso.html?section=speciale`
- [x] Mirai X mutat din sectiunea Split Perete → Tipuri Speciale in rotenso.html
- [x] Tipuri Speciale reordonate dupa pret: Mirai X (3.958) → Aneru X (3.961) → Tenji (4.296) → Nevo (4.378) → Jato (4.654)
- [x] Breadcrumb `?cat=` adaugat pe toate paginile produs (~35 fisiere) — parametrul restaureaza tabul activ pe produse.html
- [x] produse.html: JS IIFE adaugat — citeste `?cat=` din URL si activeaza filtrul corespunzator

### Boilere Termoelectrice — PARTIAL
- [x] `sunsystem-boilere.html` — creat cu 3 variante MB-L: 80L/880lei, 100L/946lei, 120L/1.150lei + selector persoane
- [x] `produse.html` — tab redenumit + restructurat: "Boilere & Puffere" (data-cat=boilere) + "Calorifere" (data-cat=calorifere) separate
- [x] Carduri noi: Boilere Termoelectrice (real, link sunsystem-boilere.html), Calorifere (placeholder), Puffere (placeholder)

### PAGINA BOILERE — DE COMPLETAT IN SESIUNEA URMATOARE
Pagina curenta `sunsystem-boilere.html` are DOAR Sunsystem MB-L (3 modele). Trebuie extinsa cu:

**Sunsystem — Boilere ACM rezidentiale:**
| Serie | 80L | 100L | 120L |
|-------|-----|------|------|
| MB-L | 880 lei | 946 lei | 1.150 lei |
| MB S1 (premium, 8 bar) | ? lei | ? lei | 1.650 lei |

**Ferroli — Boilere ACM:**
| Capacitate | Pret |
|-----------|------|
| 80L | 888 lei |
| 100L | 954 lei |
| 120L | 1.160 lei |
| 150L | 1.290 lei |
| (5th model ?) | ? |

**Sunsystem — Puffere (sesiune separata, data-cat=boilere):**
- SWPN 1S: 150L (2.635 lei), 200L, 400L, 500L — serpentina pardosea + solar
- SON 2S: 150→1500L — puffere cu doua serpentine
- SN: 150→1500L — puffere cu o serpentina
- BB NL2 150: boiler cu doua serpentine

**Diferenta MB-L vs MB S1:**
- MB-L: 6 bar, standard
- MB S1: 8 bar / 95°C, premium (mai scump ~40%)

**URL-uri pentru fetch preturile lipsa:**
- MB S1 80L: `termoshop.ro/produs/boiler-termoelectric-sunsystem-mb-s1-80-l/` (timeout — reincearca)
- MB S1 100L: `termoshop.ro/produs/boiler-termoelectric-sunsystem-mb-s1-100-l/` (404 — cauta alt slug)
- Ferroli al 5-lea model: cauta `?s=ferroli+boiler` pe pagina 2

---

## Sesiunea 2026-04-18 — CE S-A FACUT (COMPLET)

### Formulare functionale — Formspree integrat
- [x] `contact.html` — submit trimite toate datele la `https://formspree.io/f/meevgbzl` via fetch AJAX
  - Payload include: cod_lead (TS-YYYY-MMDD-XXXX), nume, telefon, email, produse_dorite, suprafata, camere, izolatie, montaj, detalii
  - Buton dezactivat pe durata submitului, mesaj de eroare daca esueaza
  - Success UI (cod TS) afisat dupa confirmare server
- [x] `ghid.html` — submit trimite raspunsurile wizardului la acelasi endpoint Formspree
  - Payload include: cod_lead, sursa (Ghid interactiv), categorie, nume, telefon, email, detalii, raspunsuri_wizard
  - Raspunsuri wizard formatate ca text lizibil cu emoji (nu JSON brut) si fara diacritice
  - Functie `removeDiacritics()` + mapping `KEY_LABELS` cu emoji per camp
- [x] Formspree account: ovidiu_cristian29@yahoo.com, notificari si pe ovidiucristiand@gmail.com
- [x] Testat si confirmat functional — emailuri primite cu toate datele

### Urmatoare etape formulare (roadmap)
- [ ] **Etapa 2**: Formspree → Slack (notificari instant, built-in Formspree, ~10 min)
- [ ] **Etapa 3**: N8N webhook — inlocuieste Formspree, control total, email automat catre client
- [ ] **Etapa 4**: N8N flows avansate — CRM, dashboard leads, etc.

---

## URMATOAREA SESIUNE: Boilere complete + Puffere SAU Slack/N8N

---

---

## Sesiunea 2026-04-25 — Homepage redesign sesiunea 1 (COMPLET)

### Ce s-a facut
- [x] **Hero rescris cu Calculator cost lunar** in `index.html`:
  - 2 inputuri: Suprafata (m²) + Izolatie (slaba/medie/buna)
  - Live update — rezultat se recalculeaza la fiecare modificare
  - 4 randuri output: Lemne / Peleti / Mixt / Pompa caldura, fiecare cu cost lunar + putere kW + badge
  - 2 CTA: "Vreau oferta personalizata" (→ contact.html cu params) + "Vezi catalog" (→ produse.html?cat=<sursa_ieftina>)
  - Formule: necesar = suprafata × 100 × factor_izolatie {slaba:1.4, medie:1.0, buna:0.7}; cost_lunar = (necesar/6) × pret_kWh / eficienta. Sezon de incalzire 6 luni.
- [x] **Sectiune Quiz teaser** sub hero in `index.html`:
  - 2 intrebari: Categorie (5 optiuni) + Locuinta (Apartament/Casa/Vila)
  - Buton "Continua spre recomandare" → redirect `ghid.html?cat=<id>&locuinta=<value>`
- [x] **Sticky CTA mobil** in `index.html` (doar @media max-width:768px):
  - 2 butoane jumate-jumate: Suna (portocaliu brand) + WhatsApp (verde WA)
  - `body { padding-bottom: 64px }` pe mobil pentru a nu acoperi footerul
- [x] **`styles.css`**: adaugate ~430 linii noi (calculator, quiz, sticky bar + responsive)
- [x] **`ghid.html`**: parser URL params — daca prezent `?cat=` deschide categoria; daca prezent si `?locuinta=` si categoria are "Tip locuinta" ca step 0 (centrale/cazane), pre-populeaza si avanseaza la step 1
- [x] **`contact.html`**: parser URL params — pre-populeaza Suprafata, Izolatie (mapare label→value), si bifeaza checkbox-ul Produs corespunzator sursei (Lemne/Peleti/Mixt → cazane-sobe; Pompa caldura → pompe-caldura)

### Document design salvat
`docs/plans/2026-04-25-homepage-redesign-design.md` — contine UX, formule complete, edge cases.

### Sesiunea 2 — Homepage (URMATOAREA)
**STATUS:** PARTIAL COMPLET (FAQ + video) — cleanup vizual amanat

1. ~~**FAQ accordion** pe homepage~~ — **COMPLET (2026-04-25 sesiunea 2)**
   - 8 intrebari adaugate inainte de CTA Final: consultanta gratuita, intermediar/producator, livrare, timp oferta, montaj, garantie, plata in rate, vizionare fizica showroom Iasi
   - Refoloseste stilul `.faq-item`/`.faq-question`/`.faq-answer` din contact.html (deja in styles.css)
   - Bumped `.faq-item.open .faq-answer { max-height: 200px → 600px }` pentru raspunsuri mai lungi
2. **Cleanup vizual sectiuni "De ce CrisTermo?" si "Branduri"** — **AMANAT pentru sesiunea urmatoare**
   - Ovidiu a mentionat ca arata fad/fara impact
   - Idei: schimbat icoanele cu SVG-uri proprii sau imagini, branduri cu logo-uri reale (nu doar text), eventual hover effects mai puternice, eventual sectiune unica "De ce noi" cu numere/statistici (X clienti, Y ani experienta TermoShop, Z branduri exclusive)
3. ~~**Sectiune video carusel**~~ — **COMPLET (2026-04-25 sesiunea 2 — revizuit)**
   - Implementat ca **carusel rotativ cu 3 Reels**: 1 mare in centru + 2 mici lateral + sageti stanga/dreapta + dots indicator
   - Reel-uri: `4227054024202116` + `1194774799260913` + `2406229736535735`
   - Pozitionare absoluta cu CSS transform (scale 0.7 pe lateralele); tranzitie 0.5s
   - Navigare: sageti, click pe slide lateral (il aduce in centru), dots, tastatura ←/→ (cand e in viewport)
   - **Stop video automat la navigare**: `stopSlideVideo()` reseteaza `iframe.src` pe slide-ul vechi → reload iframe → video-ul se opreste. Previne situatia in care 2-3 video-uri ruleaza simultan.
   - Iframe-urile au `loading="lazy"`; raman montate intre rotiri (doar slide-ul vechi se reincarca la nav)
   - Overlay portocaliu cu numarul de telefon pe toate 3
   - Mobil (≤900px): doar slide-ul central vizibil, lateralele ascunse cu opacity 0; sagetile + dots raman functionale
   - Selectoare CSS: `.reels-carousel`, `.reels-stage`, `.reel-slide.pos-{center,left,right}`, `.reels-arrow`, `.reels-dots`

4. ~~**Eliminat sectiunea "Branduri de incredere"**~~ — **COMPLET (2026-04-25 sesiunea 2)**
   - Brandurile sunt deja mentionate in cardul "Produse exclusive" din "De ce sa alegi CrisTermo?" — sectiunea era duplicata
   - Sters HTML-ul `.social-proof` din index.html + CSS-ul aferent (`.social-proof`, `.brands-grid`, `.brand-item`) din styles.css

### Sesiunea 3 — Cand exista trafic real (>20-30 leaduri)
1. **Banda live cu lead-uri** (anonimizate: "Mihai din Iasi a cerut oferta acum 12 minute")
2. **Harta interventii** SVG cu pin-uri pe orase + contor "X clienti / Y orase"

### Note importante pentru sesiunea 2
- Index-ul actual mai contine sectiunea "De ce CrisTermo?" (cards cu emoji-uri 💬💰🔧⭐) si "Branduri de incredere" (badge-uri text). Astea sunt sectiunile pe care Ovidiu vrea sa le punem la zi vizual.
- Pe mobil, body are padding-bottom 64px — daca adaugi sectiuni noi nu uita.
- Styles.css are deja stilurile necesare pentru `.faq-item`, `.faq-question` (folosite in contact.html si ghid.html) — pot fi refolosite.

---

## Dupa fiecare sesiune

**IMPORTANT:** La finalul fiecarei sesiuni, bifeaza ce ai completat:
- [x] TIS Pro → `tis-pro.html` (4 variante: 15-30 kW, preturi reale)
- [x] TIS Pellet → `tis-pellet.html` (hub) + `tis-pellet-combi.html` (15, 25 kW) + `tis-new-pellet.html` (40-95 kW)
- [x] produse.html update TIS → card unic brand → tis.html
- [x] Neus hub → `neus.html` (6 modele: Compact, Praktik, Duo Uni, Trio Uni, Turbo, Cu Plita)
- [x] `neus-compact.html` (6 variante: 24, 36, 42, 50, 75, 95 kW)
- [x] `neus-praktik.html` (5 variante: 12, 15, 20, 25, 30 kW)
- [x] `neus-duo-uni.html` (8 variante: 21-95 kW)
- [x] `neus-trio-uni.html` (5 variante: 14, 20, 30, 40, 50 kW)
- [x] `neus-turbo.html` (4 variante: 15, 25, 35, 50 kW — tip lumanare)
- [x] `neus-plita.html` (DOAR 20 kW — confirmat Eusebiu)
- [x] produse.html update Neus → card unic brand → neus.html
- [x] Kronas hub → `kronas.html` (2 modele: Standard, Eco)
- [x] `kronas-standart.html` (3 variante: 18 kW/4.716 lei, 22 kW/5.640 lei, 26 kW/6.029 lei)
- [x] `kronas-eco.html` (1 varianta: 24 kW, pret la cerere — pretul standalone necunoscut)
- [x] produse.html update Kronas → card unic brand → kronas.html
- [x] Almax hub → `almax.html` (3 modele: Class D, Class B, cu Plita VP)
- [x] `almax-class-d.html` (3 variante: 20 kW/7.749 lei, 25 kW/8.495 lei, 30 kW/8.977 lei)
- [x] `almax-class-b.html` (2 variante: 20 kW/4.819 lei, 24 kW/5.103 lei)
- [x] `almax-plita.html` (1 varianta: VP 18 kW, pret la cerere — standalone necunoscut)
- [x] produse.html update Almax → card unic brand → almax.html
- [x] Burnit hub → `burnit.html` (2 serii: NWB, NWB Prime)
- [x] `burnit-nwb.html` (1 varianta: 25 kW/4.690 lei, EN 303-5, otel 6mm)
- [x] `burnit-nwb-prime.html` (7 variante: 25/6.640, 30/6.990, 40/7.690, 50/8.239, 70/9.690, 90/10.600, 110/11.430 lei)
- [x] produse.html update Burnit → card unic brand → burnit.html
