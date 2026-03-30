# TermoShop — Brand Guidelines

**Brand:** TermoShop
**Tagline:** "Experți în încălzire și climatizare lângă tine"
**Domeniu:** Intermediere produse de încălzire și climatizare
**Ton:** Cald, prietenos, accesibil, de încredere, specialist dar nu tehnic

---

## 1. Paleta de Culori

### Culori Principale
| Culoare | Hex | Unde se folosește |
|---------|-----|-------------------|
| **Portocaliu principal** | `#E8732A` | Butoane CTA, accente, linkuri active, iconuri importante |
| **Portocaliu închis** | `#D4611F` | Hover pe butoane, accente secundare |
| **Crem deschis** | `#FFF8F0` | Fundal pagină principal |
| **Crem mediu** | `#F5E6D3` | Carduri, secțiuni alternate, fundal formular |

### Culori Text
| Culoare | Hex | Unde se folosește |
|---------|-----|-------------------|
| **Gri închis** | `#2D3436` | Text principal (titluri, paragrafe) |
| **Gri mediu** | `#636E72` | Text secundar (subtitluri, caption, placeholder) |
| **Alb** | `#FFFFFF` | Text pe fundal portocaliu (butoane, hero overlay) |

### Culori Funcționale
| Culoare | Hex | Unde se folosește |
|---------|-----|-------------------|
| **Verde succes** | `#27AE60` | Confirmări, checkmarks, mesaje succes |
| **Roșu eroare** | `#E74C3C` | Erori formular, mesaje eroare |
| **Galben atenție** | `#F39C12` | Avertismente, note importante |

---

## 2. Tipografie

### Font: Poppins (Google Fonts)

**Import:**
```css
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap');
```

### Ierarhie Fonturi
| Element | Mărime | Greutate | Culoare |
|---------|--------|----------|---------|
| **H1** (titlu hero) | 42px / 2.625rem | 700 (Bold) | `#2D3436` |
| **H2** (titlu secțiune) | 32px / 2rem | 600 (Semibold) | `#2D3436` |
| **H3** (titlu card) | 22px / 1.375rem | 600 (Semibold) | `#2D3436` |
| **Body** (text normal) | 16px / 1rem | 400 (Regular) | `#2D3436` |
| **Body large** (subtitlu) | 18px / 1.125rem | 400 (Regular) | `#636E72` |
| **Small / Caption** | 14px / 0.875rem | 400 (Regular) | `#636E72` |
| **Button text** | 16px / 1rem | 600 (Semibold) | `#FFFFFF` |

### Line Height
- Titluri: 1.2
- Body text: 1.6
- Butoane: 1.0

---

## 3. Butoane

### Buton Principal (CTA)
```css
.btn-primary {
    background-color: #E8732A;
    color: #FFFFFF;
    border: none;
    border-radius: 12px;
    padding: 14px 32px;
    font-family: 'Poppins', sans-serif;
    font-size: 16px;
    font-weight: 600;
    cursor: pointer;
    transition: background-color 0.3s ease, transform 0.2s ease;
}

.btn-primary:hover {
    background-color: #D4611F;
    transform: translateY(-2px);
}
```

### Buton Secundar (Ghost)
```css
.btn-secondary {
    background-color: transparent;
    color: #E8732A;
    border: 2px solid #E8732A;
    border-radius: 12px;
    padding: 12px 28px;
    font-family: 'Poppins', sans-serif;
    font-size: 16px;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.3s ease;
}

.btn-secondary:hover {
    background-color: #E8732A;
    color: #FFFFFF;
}
```

---

## 4. Carduri

```css
.card {
    background-color: #FFFFFF;
    border-radius: 16px;
    padding: 32px 24px;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
    transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.card:hover {
    transform: translateY(-4px);
    box-shadow: 0 8px 24px rgba(0, 0, 0, 0.12);
}
```

---

## 5. Formulare

```css
input, select, textarea {
    background-color: #FFFFFF;
    border: 2px solid #F5E6D3;
    border-radius: 8px;
    padding: 12px 16px;
    font-family: 'Poppins', sans-serif;
    font-size: 16px;
    color: #2D3436;
    transition: border-color 0.3s ease;
}

input:focus, select:focus, textarea:focus {
    border-color: #E8732A;
    outline: none;
    box-shadow: 0 0 0 3px rgba(232, 115, 42, 0.15);
}

label {
    font-family: 'Poppins', sans-serif;
    font-size: 14px;
    font-weight: 500;
    color: #2D3436;
    margin-bottom: 6px;
}

::placeholder {
    color: #636E72;
    font-weight: 300;
}
```

---

## 6. Layout

### Secțiuni
```css
section {
    padding: 80px 20px;
    max-width: 1200px;
    margin: 0 auto;
}

/* Secțiuni alternate */
section:nth-child(even) {
    background-color: #FFF8F0;
}

section:nth-child(odd) {
    background-color: #FFFFFF;
}
```

### Header
```css
header {
    background-color: #2D3436;
    color: #FFFFFF;
    padding: 20px;
}
```

### Footer
```css
footer {
    background-color: #2D3436;
    color: #FFFFFF;
    padding: 40px 20px;
}
```

---

## 7. Iconuri

- Stil: Iconuri linie (outline), nu pline
- Librărie recomandată: Lucide Icons sau Heroicons (gratuite)
- Culoare iconuri: `#E8732A` (portocaliu) sau `#636E72` (gri)
- Mărime iconuri carduri: 48px
- Mărime iconuri inline: 20px

---

## 8. Tonul Comunicării

### Cum vorbim:
- **Accesibil:** "Te ajutăm să alegi" (nu "Oferim servicii de consultanță HVAC")
- **Personal:** "Sună-ne" (nu "Contactați departamentul de vânzări")
- **Încrezător:** "Găsim soluția potrivită" (nu "Sperăm să te putem ajuta")
- **Concret:** "Răspundem în maxim 2 ore" (nu "Răspundem prompt")

### Reguli:
- Fără jargon tehnic (nu HVAC, BTU, randament termic — decât în ghidul educativ)
- Tutui-m clientul ("tu", nu "dumneavoastră")
- Propoziții scurte, clare
- Folosim "noi" și "echipa noastră" (chiar dacă ești singur — sună profesional)

### Exemple mesaje:
| Context | Da ✅ | Nu ❌ |
|---------|------|------|
| Hero | "Experți în încălzire și climatizare lângă tine" | "Servicii profesionale HVAC la standarde europene" |
| CTA | "Vreau consultanță gratuită" | "Solicitați o ofertă" |
| Beneficiu | "Nu știi ce centrală ți se potrivește? Te ajutăm noi." | "Oferim asistență în selectarea echipamentelor termice." |
| Confirmare | "Gata! Te contactăm în maxim 2 ore." | "Cererea dumneavoastră a fost înregistrată cu succes." |

---

## 9. Spațiere

| Element | Valoare |
|---------|---------|
| Spațiu între secțiuni | 80px |
| Spațiu între titlu și conținut | 24px |
| Spațiu între carduri | 24px |
| Padding carduri | 32px 24px |
| Padding butoane | 14px 32px |
| Border radius carduri | 16px |
| Border radius butoane | 12px |
| Border radius inputuri | 8px |

---

## 10. Responsive Breakpoints

| Breakpoint | Dispozitiv | Lățime max |
|-----------|------------|------------|
| Mobile | Telefon | 768px |
| Tablet | Tabletă | 1024px |
| Desktop | Computer | 1200px |

### Reguli mobile:
- H1 scade la 28px
- H2 scade la 24px
- Carduri pe o singură coloană
- Padding secțiuni: 40px 16px
- Butoane: full-width pe mobile
