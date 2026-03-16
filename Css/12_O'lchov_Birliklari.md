# 12-Dars: O'lchov Birliklari (Units)

## 📌 Absolyut Birliklar

```css
/* Ekran uchun faqat px ishlatilad */
.el {
  width: 300px;     /* Piksel — aniq, o'zgarmaydi */
  font-size: 16px;
  
  /* Kamdan-kam ishlatiladigan */
  width: 3cm;       /* Santimetr */
  width: 30mm;      /* Millimetr */
  width: 1in;       /* Dyuym = 96px */
  width: 12pt;      /* Point = 1/72 dyuym */
  width: 1pc;       /* Pica = 16px */
}
```

---

## 📌 Nisbiy Birliklar — em

```css
/* em — joriy elementning font-size ga nisbatan */
.ota {
  font-size: 20px;
}

.bola {
  font-size: 1.5em;   /* 1.5 × 20px = 30px */
  padding: 1em;       /* 1 × 30px = 30px (o'zning font-size) */
  margin: 0.5em;      /* 0.5 × 30px = 15px */
}

.nabira {
  font-size: 1.5em;   /* 1.5 × 30px = 45px — Kompound effekt! */
}

/* ⚠️ em murakkab — ichkilashganda qiymati o'zgarib ketadi */
```

---

## 📌 Nisbiy Birliklar — rem

```css
/* rem — ROOT element (html) font-size ga nisbatan */
html { font-size: 16px; } /* Default brauzer */

.el {
  font-size: 1rem;    /* 1 × 16px = 16px */
  font-size: 1.5rem;  /* 1.5 × 16px = 24px */
  font-size: 2rem;    /* 2 × 16px = 32px */
  padding: 1rem;      /* 16px — hamma joyda bir xil! */
}

/* rem vs em */
/* rem — global uchun, oldindan aytib bo'ladi */
/* em  — lokal uchun, ota elementga bog'liq */

/* Masshtab o'zgartirish — faqat html font-size ni o'zgartirish kerak */
html {
  font-size: 62.5%; /* 1rem = 10px (hisoblash oson!) */
}
.el {
  font-size: 1.6rem; /* = 16px */
  padding: 2.4rem;   /* = 24px */
}
```

---

## 📌 Foiz (%) Birligi

```css
/* % — ota elementga nisbatan */
.ota {
  width: 600px;
  height: 400px;
}

.bola {
  width: 50%;      /* 300px — ota kengligiga nisbatan */
  height: 50%;     /* 200px — ota balandligiga nisbatan */
  
  /* font-size — ota font-size ga nisbatan */
  font-size: 120%; /* Ota font-size × 1.2 */
  
  /* margin/padding — KENGLIKKA nisbatan (balandlik emas!) */
  padding-top: 50%;  /* Kenglikka nisbatan! */
}
```

---

## 📌 Viewport Birliklari

```css
.el {
  /* vw — viewport kengligining % i */
  width: 100vw;    /* To'liq kenglik */
  width: 50vw;     /* Yarmi */

  /* vh — viewport balandligining % i */
  height: 100vh;   /* To'liq balandlik */
  height: 50vh;    /* Yarmi */

  /* vmin — ikkisining kichigi */
  font-size: 5vmin;  /* Portrait: vw, Landscape: vh */

  /* vmax — ikkisining katasi */
  font-size: 5vmax;
}

/* dvh, svh, lvh — Yangi birliklar (mobil uchun) */
.hero {
  height: 100dvh;  /* Dynamic viewport height (mobile bar hisobga olinadi) */
  height: 100svh;  /* Small viewport height */
  height: 100lvh;  /* Large viewport height */
}
```

---

## 📌 Boshqa Birliklar

```css
/* ch — "0" belgisining kengligi */
.matn { max-width: 60ch; } /* Matni o'qish uchun qulay kenglik */

/* ex — "x" harfining balandligi (kamdan-kem) */

/* lh — line-height birligi */
.el { margin-bottom: 1lh; } /* Bir qator balandligi */

/* fr — Grid uchun kasr */
.grid { grid-template-columns: 1fr 2fr 1fr; }

/* Hisoblash — calc() */
.el {
  width: calc(100% - 32px);           /* Dinamik hisoblash */
  height: calc(100vh - 64px);         /* Navbar balandligini olib tashla */
  padding: calc(1rem + 5px);
  font-size: calc(16px + 0.5vw);      /* Fluid typography */
}

/* clamp() — minimal, ideal, maksimal */
.el {
  font-size: clamp(14px, 4vw, 24px);  /* Min 14px, Max 24px, Ideal 4vw */
  width: clamp(300px, 50%, 800px);
}

/* min() va max() */
.el {
  width: min(500px, 80%);   /* Kichigini tanlaydi */
  width: max(300px, 50%);   /* Kattasini tanlaydi */
}
```

---

## 📌 Qachon Nimani Ishlatish?

| Xossa        | Tavsiya etilgan birlik |
|-------------|------------------------|
| Font        | `rem`                  |
| Padding/Margin | `rem` yoki `em`    |
| Kenglik     | `%`, `vw`, `ch`        |
| Balandlik   | `vh`, `dvh`            |
| Border      | `px`                   |
| Shadow      | `px`                   |
| Grid/Flex gap | `rem`               |

---

## 🎯 10 ta Amaliy Vazifa

```html
<!DOCTYPE html>
<html lang="uz">
<head>
  <meta charset="UTF-8">
  <title>O'lchov Birliklari</title>
  <link rel="stylesheet" href="units.css">
</head>
<body>
  <!-- Vazifa 1-2: rem asosida tipografiya tizimi -->
  <div class="tipa-jadval">
    <h1 class="h1">Sarlavha 1 — 3rem</h1>
    <h2 class="h2">Sarlavha 2 — 2.25rem</h2>
    <h3 class="h3">Sarlavha 3 — 1.75rem</h3>
    <p class="katta-p">Katta paragraf — 1.25rem</p>
    <p class="normal-p">Oddiy paragraf — 1rem</p>
    <p class="kichik-p">Izoh — 0.875rem</p>
  </div>

  <!-- Vazifa 3: em bilan komponent -->
  <div class="em-komponent">
    <div class="em-karta em-karta--kichik">Kichik karta</div>
    <div class="em-karta em-karta--o_rta">O'rta karta</div>
    <div class="em-karta em-karta--katta">Katta karta</div>
  </div>

  <!-- Vazifa 4: Viewport birliklar -->
  <section class="vh-hero">
    <h2>100vh balandlik</h2>
    <p>Har doim ekranni to'ldiradi</p>
  </section>

  <!-- Vazifa 5: Fluid typography (clamp) -->
  <div class="fluid-tipa">
    <h2 class="fluid-sarlavha">Bu zamonaviy fluid sarlavha</h2>
    <p class="fluid-p">Bu fluid paragraf ekran kengligiga qarab moslashadi.</p>
  </div>

  <!-- Vazifa 6: ch birligi bilan matn -->
  <article class="ch-matn">
    <h3>Optimal qatorli matn</h3>
    <p>Bu matn 65ch kenglikda joylashgan. O'qish uchun qulay kenglik 45–75 belgidan iborat deb hisoblanadi. Shuning uchun ch birligi matn kengligi uchun juda foydali.</p>
  </article>

  <!-- Vazifa 7: calc() bilan layout -->
  <div class="calc-layout">
    <div class="calc-sidebar">Sidebar (280px)</div>
    <div class="calc-kontent">Kontent (calc(100% - 280px - 24px))</div>
  </div>

  <!-- Vazifa 8: Responsive grid (fr) -->
  <div class="fr-grid">
    <div class="fr-el">1fr</div>
    <div class="fr-el">2fr</div>
    <div class="fr-el">1fr</div>
  </div>

  <!-- Vazifa 9-10: min/max/clamp -->
  <div class="responsive-quti">
    <p>width: clamp(300px, 60%, 900px)</p>
  </div>
</body>
</html>
```

```css
/* units.css */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

/* Vazifa 1: rem asosini belgilash */
html { font-size: 16px; }   /* 1rem = 16px */
body { font-family: "Segoe UI", sans-serif; color: #1a1a2e; background: #f8f9fa; }

/* Vazifa 2: Tipografiya tizimi (rem) */
.tipa-jadval { max-width: 800px; margin: 0 auto; padding: 3rem 2rem; }
.h1 { font-size: 3rem;      margin-bottom: 1rem; }   /* 48px */
.h2 { font-size: 2.25rem;   margin-bottom: 0.875rem; } /* 36px */
.h3 { font-size: 1.75rem;   margin-bottom: 0.75rem; }  /* 28px */
.katta-p { font-size: 1.25rem;  margin-bottom: 0.625rem; } /* 20px */
.normal-p { font-size: 1rem;    margin-bottom: 0.5rem; }    /* 16px */
.kichik-p { font-size: 0.875rem; color: #666; }             /* 14px */

/* Vazifa 3: em bilan komponentlar */
.em-komponent {
  display: flex; gap: 1rem; flex-wrap: wrap;
  padding: 2rem; background: white; margin: 2rem;
}
.em-karta {
  background: royalblue; color: white; border-radius: 0.5em;
  /* padding va border-radius EM — font-size ga nisbatan */
}
.em-karta--kichik { font-size: 12px;  padding: 0.75em 1.5em; }
.em-karta--o_rta  { font-size: 16px;  padding: 0.75em 1.5em; }
.em-karta--katta  { font-size: 24px;  padding: 0.75em 1.5em; }

/* Vazifa 4: Viewport */
.vh-hero {
  height: 100vh; display: flex; flex-direction: column;
  align-items: center; justify-content: center; text-align: center;
  background: linear-gradient(135deg, #667eea, #764ba2); color: white;
}
.vh-hero h2 { font-size: 3rem; margin-bottom: 1rem; }

/* Vazifa 5: Fluid typography */
.fluid-tipa { padding: 4rem 2rem; background: white; margin: 2rem; border-radius: 1rem; }
.fluid-sarlavha {
  font-size: clamp(1.5rem, 5vw, 3.5rem); /* Min 24px, Max 56px */
  margin-bottom: 1rem; line-height: 1.2;
}
.fluid-p {
  font-size: clamp(0.875rem, 2vw, 1.25rem);
  line-height: 1.7; color: #555;
}

/* Vazifa 6: ch birligi */
.ch-matn {
  max-width: 65ch;   /* O'qish uchun qulay kenglik */
  margin: 2rem auto; padding: 2rem;
  background: white; border-radius: 0.5rem;
  line-height: 1.7;
}
.ch-matn h3 { margin-bottom: 0.75rem; font-size: 1.25rem; }

/* Vazifa 7: calc() */
.calc-layout { display: flex; gap: 24px; padding: 2rem; }
.calc-sidebar {
  width: 280px; min-height: 200px; background: #16213e; color: white;
  padding: 1.5rem; border-radius: 0.75rem; flex-shrink: 0;
}
.calc-kontent {
  width: calc(100% - 280px - 24px);  /* calc bilan aniq hisoblash */
  background: white; padding: 1.5rem; border-radius: 0.75rem;
}

/* Vazifa 8: fr birlik (Grid) */
.fr-grid {
  display: grid;
  grid-template-columns: 1fr 2fr 1fr;  /* fr birlik */
  gap: 16px; padding: 2rem;
}
.fr-el {
  background: royalblue; color: white; padding: 1.5rem;
  text-align: center; border-radius: 0.5rem; font-size: 0.9rem;
}

/* Vazifa 9-10: min/max/clamp bilan responsiv */
.responsive-quti {
  width: clamp(300px, 60%, 900px);
  margin: 2rem auto;
  padding: 2rem;
  background: linear-gradient(135deg, #f5f7fa, #c3cfe2);
  border-radius: 1rem; text-align: center;
  font-size: clamp(0.875rem, 2vw, 1.1rem);
}
```
