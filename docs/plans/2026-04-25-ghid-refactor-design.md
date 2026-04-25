# Ghid.html Refactor — Design Document (sesiune dedicata)

**Data design:** 2026-04-25
**Sesiune planificata:** urmatoarea (estimat 2-3 ore)
**Scop:** Restructurare completa ghid.html cu un set de intrebari coerent, branching logic real si UX nou (re-edit la orice pas).

## 1. Arhitectura — DECIS: Optiunea B

5 wizard-uri reduse la **3 wizard-uri verticale + 1 holistic**:

```
HUB (5 carduri)
├─ 🔥 Centrale (wizard)
├─ ❄️ Climatizare (wizard)
├─ 🌡️ Incalzire pardoseala (wizard)
├─ ♨️ Pompe de caldura  ← DE CLARIFICAT (vezi sectiunea 5)
└─ 🏠 Configurez tot pentru o casa (wizard holistic NOU)
```

### Eliminate fata de structura curenta
- **Categoria "Cazane & Sobe"** se contopeste cu Centrale (lemnele, peletii, mixtele sunt cazane termice)
- Wizardul izolat pentru **Boilere/Puffere** si **Calorifere** dispar din ghid.html — devin **intrebari opt in wizardul Centrale** (vezi sectiunea 3)

### Sub-tipuri pe categorie
- **Centrale:** Lemne / Peleti / Mixte (+ posibil Pompa caldura aer-apa — DE DECIS)
- **Climatizare:** Split (perete) / Speciale (canal, caseta, consola, multi-split)
- **Pardoseala:** flux unic
- **Holistic:** flux unic mai lung, atinge toate elementele unei case

## 2. Set de intrebari (lista finala)

### Intrebari de baza (confirmate de Ovidiu)
1. **Locatie** (judet) → zona climatica + acoperire livrare
2. **Suprafata** m² locuinta
3. **Sursa principala incalzire**: Lemne / Peleti / Mixta / Pompa caldura / AC (+ cate camere daca AC)
4. **Vrei accesorii aferente?** (depinde de raspuns 3)
5. **Distributie caldura**: Calorifere / Pardoseala / Am deja una / Mix
6. **Boiler ACM**: Am deja / Vreau termoelectric / Vreau cu serpentina (+ Cate persoane locuiesc in casa?)
7. **Puffer**: Vrei?
   - **Regula:** la `peleti` ascunde intrebarea (nota: "Centralele pe peleti nu necesita puffer")
   - **Regula:** la `lemne / mixt` arata intrebarea cu nota: "Recomandat, dar nu obligatoriu"
8. **Camera tehnica** m²
   - **Daca DA:** mergem mai departe normal
   - **Daca NU:** intrebare libera "Unde vrei sa montezi?" (text + presugestii: hol / bucatarie / living) → recomandari speciale (centrala cu plita, monobloc peleti, termosemineu — nu polueaza interiorul)

### Intrebari suplimentare (sugestii integrate)
9. **Casa noua sau renovare?** — afecteaza ce poti instala (pardoseala mult mai usor in casa noua/renovare totala)
10. ~~Buget orientativ~~ — **EXCLUS** (decizie Ovidiu — sensitive, scade conversia)
11. **Cand vrei sa instalezi?** — ASAP / 1-3 luni / >6 luni (pentru prioritizare leaduri ASAP = hot lead)
12. **Acces gaz natural?** — desi nu vinde gaz, e relevant pentru a sti concurenta + a recomanda solutii hibride
13. **Solar fotovoltaic existent?** — schimba rentabilitatea pompei caldura (PV + PC = combo killer pe rentabilitate)
14. **Cos de fum existent?** — pentru lemne/peleti, daca nu au cos = costuri extra mentionate in oferta
15. ~~Numar copii~~ — deja partial in #6 (persoane in casa)

### Total intrebari per wizard
- **Centrale:** ~10-12 intrebari (cu skip-uri)
- **Climatizare:** ~6-8 intrebari
- **Pardoseala:** ~5-6 intrebari
- **Holistic:** ~14-16 intrebari (acopera tot)

## 3. Reguli de logica (branching + recomandari)

### Skip-uri / arata-ascunde
| Conditie | Comportament |
|----------|-------------|
| `sursa = peleti` | Ascunde intrebarea Puffer; cu nota explicativa |
| `sursa = lemne / mixt` | Arata Puffer cu nota "Recomandat" |
| `camera_tehnica = nu` | Forteaza branch "fara fum interior": centrala plita / monobloc peleti / termosemineu |
| `casa = renovare` & `pardoseala = vreau` | Avertisment "Necesita ridicare sapa, recomandat doar pe parter sau in renovare totala" |
| `cos_fum = nu` & `sursa in [lemne/peleti/mixt]` | Mentiune in oferta: "Necesita instalare cos de fum (~3.000-5.000 lei extra)" |
| `acces_gaz = da` | Nota informativa "Daca ai gaz, costul lunar pe gaz e ~720 lei vs lemne ~340 lei — diferenta justifica investitia in cazan lemne dupa ~3 ani" |
| `pv = da` & `sursa = pompa caldura` | Boost recomandare: "PC + PV = combinatia ideala, costul lunar poate fi aproape 0 in sezon insorit" |

### Recomandari produs (mapare raspuns → produse din catalog)
| Raspunsuri cheie | Produse recomandate |
|------------------|---------------------|
| Lemne, suprafata 50-100m², izolatie buna | Warmline Eco / TIS Uni / Neus Compact 24kW |
| Lemne, suprafata 100-200m² | Warmline Premium / TIS Pro / Burnit NWB Prime 30-50kW |
| Lemne, suprafata 200m²+, vila | Warmline Premium 75-200kW / Neus Compact 75-95kW |
| Peleti automate, mediu | Warmline Black Pellet / TIS Pellet / Burnit Pellet |
| Peleti monobloc (fara camera tehnica) | Warmline Monogravity (3 variante 20/25/30kW) |
| Mixt, peleti+lemne | Warmline Premium (poate functiona pe ambele) / Burnit NWB Prime |
| Pompa aer-apa, casa noua, izolatie buna | Sunsystem Mono Plus / Sunsystem Split Plus / Termoshop R290 |
| AC Split, 1 camera 25-35m² | Rotenso Roni / Elis X / Imoto X (9k BTU) |
| AC Special, multi camere | Rotenso Mirai X (multi-split) |
| Boiler termoelectric, 2-3 persoane | Sunsystem MB-L 80L sau MB S1 80L |
| Boiler termoelectric, 4+ persoane | Sunsystem MB-L 100L / 120L / Ferroli 120L+ |
| Puffer, lemne, suprafata medie | Sunsystem SN sau SON 2S 200-400L |
| Puffer + solar | Sunsystem SWPN 1S (cu serpentina solar) |

## 4. UX nou — Summary clickabil pentru re-edit

### Cerinta Ovidiu
> "sa poata selecta intrebarea 3-7-9 .... care e marcata scurt ex: intrebarea 3: 'Boiler' apasam click: Boiler - revine la intrebarea 3"

### Implementare
**Sub bara de progress, afisam un sir de pills cu raspunsurile date pana acum**:

```
[1. Iasi ✓]  [2. 120m² ✓]  [3. Lemne ✓]  [4. ... ]  [5 → in progres]
              ↑ click oriunde se editeaza acel pas
```

- Fiecare pill arata: numar intrebare + raspuns sumarizat (max 12 caractere) + bifa
- Click pe orice pill → wizard se intoarce la acel step, raspunsul ramane preselectat (poate fi schimbat)
- Pill-urile dupa step-ul curent sunt gri/dezactivate (nu poti sari inainte fara sa raspunzi)
- Bifa pe verde la cele completate, gri la cele necompletate

### Alte UX
- "Nu stiu" ca optiune valida la fiecare intrebare (parte deja existenta)
- Bara progres reala (ex: "Intrebarea 7 din 14")
- Buton "Sari peste" pentru intrebari optionale (Casa noua/renovare, Solar, etc.)
- **Pre-completare din homepage quiz** — deja functional (`?cat=X&locuinta=Y`)
- **Salvare state in localStorage** — daca user inchide tab-ul, revine la unde a ramas
- Ordine UX intrebari: incepe cu cele de baza (locatie, suprafata) → apoi specifice (sursa, accesorii) → la final cele optionale (gaz, solar, cos fum)

## 5. DE CLARIFICAT in sesiunea urmatoare

1. **Pompele de caldura aer-apa (Sunsystem, Termoshop R290)** — unde le punem?
   - **Opt A:** Sub-tip in Centrale (Lemne / Peleti / Mixte / **Pompa caldura aer-apa**)
   - **Opt B:** Categorie separata in hub (cum e acum)
   - **Opt C:** Doar in wizardul Holistic, nu si stand-alone
2. **Wizardul Holistic vs Centrale** — exista risc de overlap mare. Diferentiere clara: Holistic = "construiesc casa de la 0", Centrale = "vreau o centrala specifica si stiu deja ce".
3. **Configurator AC** — pentru AC, formula `BTU = suprafata * 250` (deja in handoff). Vrem sa adaugam si configurator BTU in wizardul Climatizare?
4. **Localitate vs Judet** — input liber (text) sau dropdown cu cele 41 judete + Bucuresti?

## 6. Plan de executie sesiune urmatoare

| Pas | Effort | Activitate |
|-----|--------|-----------|
| 1 | 5 min | Raspuns la cele 4 intrebari de clarificat din sectiunea 5 |
| 2 | 20 min | Brainstorming detaliat ordine intrebari + branch tree (skill `brainstorming` + AskUserQuestion) |
| 3 | 15 min | Build matrice produs ↔ raspuns (folosesc paginile produs deja existente) |
| 4 | 60 min | Refactor HTML: 3 wizards (Centrale/Climatizare/Pardoseala) + 1 nou (Holistic) |
| 5 | 40 min | Refactor JS: branching logic + summary clickabil + getRecommendation actualizat |
| 6 | 15 min | CSS pt summary pills + skip button + indicator step |
| 7 | 10 min | Test manual + handoff doc + commit |
| **Total** | **~2-3 ore** | Sesiune dedicata |

## 7. Ce trebuie pastrat din ghid.html actual (nu rescriem de la 0)

- Layout HUB cu carduri (am adaugat doar holistic la final)
- Stilurile CSS `.wizard-container`, `.wizard-step`, `.wizard-option`, `.wizard-progress` (in styles.css)
- Functia de submit form catre Formspree (ramane neschimbata, doar payload-ul se imbogateste cu noile raspunsuri)
- Cod-ul TS-YYYY-MMDD-XXXX (lead tracking)
- URL params parser `?cat=X&locuinta=Y` (deja functional, integrare cu homepage quiz)
- Stilizare diacritice removal pentru email payload

## 8. Cum porneste sesiunea urmatoare

User-ul va spune: *"Citeste 2026-04-25-ghid-refactor-design.md si continua cu refactor-ul ghid.html"*

Pasi:
1. Read design doc + product-pages-handoff.md (pt context produs)
2. Raspund la 4 intrebari de clarificat din sectiunea 5
3. Brainstorming detaliat → confirmare cu Ovidiu
4. Implementare iterativa cu commit-uri pe etape
