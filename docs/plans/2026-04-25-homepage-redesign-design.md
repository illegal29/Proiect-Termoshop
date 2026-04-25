# Homepage Redesign — Design Document

**Data:** 2026-04-25
**Sesiunea:** 1 din 3 (vezi handoff la final)
**Scop:** Transforma index.html dintr-o vitrina statica intr-un homepage interactiv care diferentiaza CrisTermo de competitia (termoshop.ro, climaprod.ro, climastar.ro, eMAG).

## Strategie

Homepage-ul actual e profesional dar interschimbabil cu competitorii. Concluzia analizei competitiei (`docs/plans/2026-03-28-cercetare-competitie.md`): nimeni in piata romaneasca HVAC nu ofera **calculator interactiv de cost lunar** + **quiz de orientare** + **acces rapid la consultanta pe mobil**. Sesiunea 1 implementeaza aceste 3 diferentiatori in primele 2 ecrane (hero + sectiunea imediat sub).

## Sesiune 1 — Scope

1. **Calculator cost lunar** in hero (peste fold)
2. **Quiz teaser** sub hero (categorie + locuinta → redirect spre ghid.html)
3. **Sticky CTA mobil** (Suna + WhatsApp, doar pe mobil, fix bottom)

Sectiunile existente (Beneficii, Cum lucram, Branduri, Video Reel, CTA final, Footer) raman neschimbate aceasta sesiune.

## 1. Calculator cost lunar

### UX
- 2 inputuri: **Suprafata (m²)** + **Izolatie (slaba/medie/buna)**
- **Live update** — rezultatul se recalculeaza pe masura ce se modifica inputurile (fara buton "Calculeaza")
- Output: tabel cu 4 randuri (Lemne / Peleti / Mixt / Pompa caldura), fiecare cu cost lunar + putere kW + badge punct forte
- 2 CTA-uri sub rezultat: **Vreau oferta personalizata** (→ contact.html cu valori pre-completate via query string) + **Vezi catalog** (→ produse.html)

### Formule

**Necesar termic anual:**
```
necesar_kWh_an = suprafata × 100 × factor_izolatie
factor_izolatie = { slaba: 1.4, medie: 1.0, buna: 0.7 }
```

**Cost lunar (sezon de incalzire = 6 luni, oct-mar):**
```
cost_lunar(sursa) = (necesar_kWh_an / 6) × pret_kWh(sursa) / eficienta(sursa)
```

| Sursa | Pret combustibil/kWh | Eficienta | Note |
|-------|---------------------|-----------|------|
| Lemne | 0.24 lei | 0.85 | 450 lei/mc, 1900 kWh/mc |
| Peleti | 0.39 lei | 0.92 | 1700 lei/tona, 4400 kWh/tona |
| Mixt | media (0.315) | 0.88 | medie lemne+peleti, eficienta echipament mixt |
| Pompa caldura | 1.30 lei | 3.5 (COP) | electricitate / coeficient performanta |

**Putere recomandata kW:**
- Lemne / Peleti / Mixt: `suprafata / 10`, rotunjit la cea mai apropiata varianta de catalog
- Pompa caldura: `suprafata / 14` (mai eficienta termic)

### Badges
| Sursa | Badge |
|-------|-------|
| Lemne | "Cel mai ieftin" |
| Peleti | "Automat" |
| Mixt | "Flexibil" |
| Pompa caldura | "Verde + eficient" |

### Edge cases
- Suprafata invalida (gol / 0 / negativ / >1000) → ascunde rezultatul, nu afisa erori (UX prietenos)
- Default la load: 100 m² + Medie (sa apara un rezultat exemplu imediat)
- Min: 20 m², Max: 1000 m². Cifrele de afisare se rotunjesc la 10 lei (ex: ~340 lei, nu 342.7 lei)
- "Mixt" e doar pentru centrale care accepta lemne SAU peleti — costul e media celor doua + eficienta usor mai mica

### CTA query string
```
contact.html?suprafata=120&izolatie=Medie&sursa_recomandata=Lemne
```
Pre-populeaza formularul in contact.html. (Contact.html are deja parsing pentru `?produs=` — adaugam si parametrii noi.)

## 2. Quiz teaser

### UX
Sectiune noua intre hero si "De ce CrisTermo?". Fundal usor diferit ca sa se distinga.

**Step 1:** "Ce te intereseaza?"
- 5 carduri-buton: Centrale termice / Cazane & Sobe / Climatizare / Pardoseala / Pompe caldura
- Click pe un card → trece la step 2

**Step 2:** "Tip locuinta?"
- 3 carduri: Apartament / Casa / Vila
- Click pe un card → buton **"Continua spre recomandare →"** apare

**Click final:** redirect catre `ghid.html?cat=<catId>&locuinta=<value>`

### Integrare ghid.html
Adaugam in `ghid.html` JS care, la load, citeste `?cat=` si `?locuinta=` din URL. Daca prezent:
1. Pre-populeaza `wizardState[catId].answers.locuinta = value`
2. `wizardState[catId].currentStep = 1`
3. Apeleaza `openCategory(catId)`

### Edge cases
- User da click pe categoria gresita → step 1 ramane revertibil cu buton "Inapoi"
- Daca skip step 2 si redirect direct (doar cu cat) → ghid.html porneste de la step 0 normal

## 3. Sticky CTA mobil

### UX
- Bara fixa la bottom, **doar pe mobile** (`@media (max-width: 768px)`)
- 2 butoane jumate-jumate:
  - **Suna** (icon telefon, `tel:+40775175897`)
  - **WhatsApp** (icon WA, `https://wa.me/40775175897`)
- Inaltime ~56px
- Body capata `padding-bottom: 56px` pe mobil pentru a nu acoperi footerul

### Edge cases
- Nu apare deloc pe desktop (numarul e in navbar/footer)
- Z-index: deasupra continutului dar sub navbar (in caz ca scrollam in jos cu navbar sticky)
- Culori: Suna = portocaliu brand (#E8732A), WhatsApp = verde WA (#25D366) sau pastram brand pe ambele cu icon distinctiv

## Fisiere modificate

| Fisier | Modificare |
|--------|-----------|
| `index.html` | Hero rescris cu calculator + sectiune quiz noua + sticky bar HTML |
| `styles.css` | Stiluri pentru `.calc-*`, `.quiz-teaser-*`, `.sticky-cta-mobile` (+ media query) |
| `ghid.html` | JS la load: parse `?cat=` si `?locuinta=` → pre-populare wizardState |

## Sesiunile urmatoare (handoff)

### Sesiunea 2 — FAQ accordion + Video curatat
- FAQ cu 6-8 intrebari (TVA inclus? Cat dureaza livrarea? Ce judete acoperim? Garantie? Modalitati plata? etc.)
- Sectiune video: trec de la 1 Reel singular la layout 2-3 Reels (un mare central + 2 mici, sau carusel)
- Buton "Vezi toate videoclipurile" pentru un viitor /videoclipuri
- Cleanup pe sectiunile "De ce CrisTermo" + "Branduri" — Ovidiu a mentionat ca arata fad vizual

### Sesiunea 3 — Cand exista trafic real
- Banda live cu lead-uri reale (anonimizate)
- Harta interventii / orase acoperite (cand exista 30+ leaduri)

## Concepte excluse din sesiunea 1 (deliberat)

- **Tier-uri de pret in calculator** (entry/mid/premium per sursa) — confuza, 9 randuri prea mult. Tier-urile raman in pagina produs.
- **Centrale pe gaz** in calculator — Ovidiu nu vinde centrale pe gaz, scoasa din comparatie.
- **Lista detaliata de calificare** (camera tehnica, accesorii, boiler, puffer) — apartine de ghid.html, va fi imbogatit intr-o sesiune separata.
