# Design: Pagina Ghid — Redesign complet + Restructurare Contact

**Status:** VALIDAT — pregătit pentru implementare
**Data:** 2026-03-29

---

## Viziune

Pagina Ghid devine principalul instrument de **calificare a lead-urilor** și **educație a clientului**. Clientul răspunde la câteva întrebări simple, primește o recomandare personalizată, și completează un formular direct pe pagină. La contactul ulterior, noi știm deja ce are nevoie — totul merge mai smooth spre oferta finală.

**Obiectiv dual:**
- Pentru client: învață ce i se potrivește, fără jargon tehnic
- Pentru noi: colectăm datele necesare pentru o ofertă precisă

---

## Structura paginii

### 1. HERO
- **Titlu:** "Găsește soluția potrivită pentru casa ta"
- **Subtitlu:** "Răspunde la câteva întrebări și primești o recomandare + ofertă personalizată"

### 2. HUB CATEGORII — 6 carduri mari
Fiecare card: titlu + descriere simplă în limbaj nespecialist + iconiță.

| Card | Descriere |
|------|-----------|
| 🔥 Centrale termice | Soluția principală de încălzire — pe gaz, electric sau cu pompă |
| 🪵 Cazane & Sobe | Lemne, peleți, seminee — ideal dacă ai acces la combustibil solid |
| ❄️ Climatizare | Aer condiționat, răcire, încălzire prin split |
| 🌡️ Încălzire în pardoseală | Confort uniform în toată casa |
| ☀️ Panouri solare | Apă caldă gratuită de la soare |
| ♨️ Pompe de căldură | Eficiență maximă, economie pe termen lung |

**Comportament:** Click pe card → scroll smooth la secțiunea categoriei → wizard-ul se deschide automat.

### 3. SECȚIUNI PER CATEGORIE (×6)
Fiecare secțiune conține:
1. Titlu categorie + introducere educativă (3-4 rânduri simple)
2. Wizard specific (3-5 întrebări adaptate)
3. Rezultat wizard cu sumar vizual al răspunsurilor
4. Scroll automat la formularul comun

### 4. FORMULAR UNIC (jos pe pagină)
Un singur formular care agregă toate categoriile completate.

```
Categorii completate:
  ✅ Centrale termice (24 kW, gaz, apartament 125 m²)
  ✅ Climatizare (2 camere, răcire + încălzire)

Nume *          [_______________]
Telefon *       [_______________]  ← doar cifre
Email           [_______________]
Detalii         [_______________]  ← câmp liber, GOL (nu pre-completat)

[ Trimite cererea ]
```

**Câmpul Categoria:** pre-selectat dar EDITABIL (dropdown) — clientul poate corecta.
**Câmpul Detalii:** rămâne GOL — pentru mesaj liber. Sumarul răspunsurilor se afișează vizual deasupra formularului, separat.
**Validare:** Nume = doar litere + diacritice. Telefon = doar cifre.

### 5. CONFIRMARE + CROSS-LINKING
După trimiterea formularului:

```
✅ Cererea ta a fost trimisă!
Cod referință: TS-2026-0329-XXXX
Te contactăm în maxim 2 ore.

Mai ai nevoie și de...?
[ + Climatizare ]  [ + Panouri solare ]  [ + Descrie singur ]
```

Cross-linking-ul apare DUPĂ captarea lead-ului, nu înainte.

---

## Wizard-uri per categorie

### Centrale termice (5 pași)
1. Ce tip de locuință ai? → Apartament / Casă / Vilă
2. Care e suprafața? → Sub 50 / 50-100 / 100-150 / Peste 150 m²
3. Ai racord la gaz? → Da / Nu / Nu știu
4. Ce tip de izolație are casa? → Bună / Medie / Fără / Nu știu
5. Ai nevoie și de apă caldă de la centrală? → Da / Nu / Nu știu

### Cazane & Sobe (4 pași)
1. Tip locuință + suprafață → Apartament/Casă + suprafață
2. Ce combustibil ai acces ușor? → Lemne / Peleți / Ambele
3. Vrei alimentare automată sau manuală? → Automată / Manuală / Nu știu
4. Ai nevoie și de apă caldă? → Da / Nu / Nu știu

### Climatizare (4 pași)
1. Ce vrei să faci? → Răcire vara / Încălzire iarna / Ambele
2. Câte camere vrei să climatizezi? → 1 / 2-3 / 4+ / Spațiu comercial
3. Tip clădire → Apartament / Casă / Spațiu comercial
4. Ai mai avut aer condiționat? → Da / Nu

### Încălzire în pardoseală (3 pași)
1. Construcție nouă sau renovare? → Nouă / Renovare
2. Ce suprafață vrei să acoperi? → Sub 50 / 50-100 / 100-150 / Peste 150 m²
3. Ai deja o sursă de căldură? → Da / Nu / Urmează să cumpăr

### Panouri solare (3 pași)
1. Ce vrei să obții? → Apă caldă / Contribuție la încălzire / Ambele
2. Tip acoperiș → Terasă / Înclinat / Nu știu
3. Câte persoane locuiesc în casă? → 1-2 / 3-4 / 5+

### Pompe de căldură (3 pași)
1. Ce vrei să faci? → Înlocuiesc centrala veche / Instalație nouă
2. Care e suprafața locuinței? → Sub 50 / 50-100 / 100-150 / Peste 150 m²
3. Ai spațiu exterior (curte/grădină)? → Da / Nu

---

## Persistarea stării

- Răspunsurile wizard-urilor se păstrează în sesiune (JavaScript)
- Dacă clientul se întoarce la un wizard completat, vede răspunsurile salvate
- Formularul comun agregă automat toate categoriile completate
- La trimitere, se generează cod unic TS-YYYY-MMDD-XXXX

---

## Restructurare Contact — "Ce produs te interesează?"

Înlocuim lista tehnică cu subcategorii (pe care clientul nu o înțelege) cu 7 carduri simple:

| Card | Comportament |
|------|-------------|
| 🔥 Centrale termice | Toggle selectat/deselectat |
| 🪵 Cazane & Sobe | Toggle selectat/deselectat |
| ❄️ Climatizare | Toggle selectat/deselectat |
| 🌡️ Încălzire pardoseală | Toggle selectat/deselectat |
| ☀️ Panouri solare | Toggle selectat/deselectat |
| ♨️ Pompe de căldură | Toggle selectat/deselectat |
| ✏️ Nu știu / Vreau sfat | Toggle — pentru cine nu se încadrează |

- Click = selectat/deselectat, pot alege mai multe
- Vizual identice cu cardurile din Ghid (consistență)
- Fără subcategorii tehnice

---

## Decizii de design

1. **Un singur formular per pagină Ghid** — o singură trimitere, un singur lead
2. **Cross-linking DUPĂ trimitere** — nu distragem de la conversie
3. **Categoria pre-selectată dar editabilă** — clientul poate corecta
4. **Detalii GOL** — sumarul wizard-ului se afișează vizual separat, nu în câmpul de text
5. **"Nu știu / Vreau sfat"** adăugat la Contact — pentru cine nu știe ce categorie vrea
6. **Fără buget** — nu întrebăm prețuri, scopul e calificare + educație
7. **Fără subcategorii tehnice** la Contact — clientul alege doar categoria mare
