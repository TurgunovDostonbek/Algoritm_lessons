# 05-Dars: Text, Font va Pseudo-elementlar

## 📌 Text Xossalari

```css
/* text-align — gorizontal hizalash */
p {
  text-align: left;     /* Chapga (default) */
  text-align: right;    /* O'ngga */
  text-align: center;   /* Markazga */
  text-align: justify;  /* Ikki tomonga tekislash */
}

/* text-decoration */
a {
  text-decoration: none;         /* Chiziqsiz */
  text-decoration: underline;    /* Tagiga chiziq */
  text-decoration: line-through; /* Ustiga chiziq */
  text-decoration: overline;     /* Ustiga chiziq */
  text-decoration: underline dotted red 2px; /* Murakkab */
}

/* text-transform */
.el {
  text-transform: uppercase;   /* HAMMASINI KATTA */
  text-transform: lowercase;   /* hammasini kichik */
  text-transform: capitalize;  /* Har So'z Bosh Harf */
  text-transform: none;        /* O'zgartirmaslik */
}

/* letter-spacing va word-spacing */
.el {
  letter-spacing: 2px;  /* Harflar orasidagi bo'shliq */
  word-spacing: 5px;    /* So'zlar orasidagi bo'shliq */
}

/* line-height */
p {
  line-height: 1.6;     /* em bilan (tavsiya) */
  line-height: 24px;    /* px bilan */
  line-height: 160%;    /* Foiz bilan */
}

/* text-shadow */
h1 {
  text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
  /* offset-x | offset-y | blur | color */
  text-shadow: 1px 1px 0 red, 2px 2px 0 navy; /* Ko'p soya */
}

/* text-indent */
p { text-indent: 2em; }  /* Birinchi qator boshlanishi */

/* white-space */
.el {
  white-space: normal;   /* Qatorga tushiradi (default) */
  white-space: nowrap;   /* Qator o'tkazmaslik */
  white-space: pre;      /* Bo'sh joylarni saqlash */
  white-space: pre-wrap; /* Bo'sh joylarni saqlash + qator o'tkazish */
}
```

---

## 📌 Vertical Align

```css
/* Inline va inline-block elementlar uchun */
span, img, td {
  vertical-align: baseline;  /* Default */
  vertical-align: top;
  vertical-align: middle;
  vertical-align: bottom;
  vertical-align: text-top;
  vertical-align: text-bottom;
  vertical-align: 10px;   /* Custom */
}

/* ⚠️ vertical-align faqat inline/td da ishlaydi! */
/* Block uchun — flexbox ishlating */
```

---

## 📌 Float

```css
/* Float — elementni chap yoki o'ngga "suzishi" */
img {
  float: left;    /* Chap tomonga */
  float: right;   /* O'ng tomonga */
  float: none;    /* Default */
  margin: 0 16px 16px 0; /* Matndan ajratish */
}

/* clearfix — float dan keyin tozalash */
.clearfix::after {
  content: "";
  display: block;
  clear: both;
}

/* yoki */
.ota { overflow: hidden; } /* Float ni "tutib" oladi */
```

---

## 📌 Font Xossalari

```css
/* font-family */
body {
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  /* Zaxira (fallback) fontlar ketma-ket yoziladi */
}

/* font-size */
p {
  font-size: 16px;   /* px — aniq */
  font-size: 1rem;   /* root element ga nisbatan */
  font-size: 1.2em;  /* Joriy element ga nisbatan */
  font-size: 80%;    /* Ota elementga nisbatan */
}

/* font-weight */
p {
  font-weight: normal;   /* 400 */
  font-weight: bold;     /* 700 */
  font-weight: 100;      /* Eng ingichka */
  font-weight: 900;      /* Eng qalin */
}

/* font-style */
p {
  font-style: normal;
  font-style: italic;
  font-style: oblique;
}

/* Shorthand */
p {
  font: italic bold 18px/1.6 "Segoe UI", sans-serif;
  /* style | weight | size/line-height | family */
}
```

---

## 📌 Font Ulash Usullari (3 xil)

```html
<!-- 1. Google Fonts (CDN) — Eng oson -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap">
```

```css
/* 2. @import (CSS ichida) */
@import url("https://fonts.googleapis.com/css2?family=Inter&display=swap");

/* 3. @font-face (Lokal fayl) */
@font-face {
  font-family: "MeningSrijam";
  src: url("fonts/mening-srijanim.woff2") format("woff2"),
       url("fonts/mening-srijanim.woff")  format("woff");
  font-weight: 400;
  font-style: normal;
  font-display: swap; /* ← Yuklanish vaqtida zaxirani ko'rsatsin */
}

body { font-family: "MeningSrijam", sans-serif; }
```

---

## 📌 Font Awesome va SVG Icons

```html
<!-- Font Awesome (CDN) -->
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">

<!-- Ishlatish -->
<i class="fa-solid fa-heart"></i>       <!-- To'ldirilgan yurak -->
<i class="fa-regular fa-star"></i>      <!-- Bo'sh yulduz -->
<i class="fa-brands fa-github"></i>     <!-- GitHub logo -->
```

```css
/* Font Awesome o'lchamlari */
.icon { font-size: 24px; }
.icon-lg { font-size: 2em; }
.icon-spin { animation: fa-spin 2s infinite linear; }
```

```html
<!-- SVG inline -->
<svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
  <path d="M12 2L2 7l10 5 10-5-10-5z" stroke="currentColor" stroke-width="2"/>
</svg>

<!-- SVG img sifatida -->
<img src="icon.svg" alt="Icon" width="24" height="24">
```

```css
/* SVG ni CSS bilan boshqarish */
svg { fill: royalblue; }
svg path { stroke: red; }
.icon svg:hover { fill: navy; transition: fill 0.3s; }
```

---

## 🎯 10 ta Amaliy Vazifa

```html
<!DOCTYPE html>
<html lang="uz">
<head>
  <meta charset="UTF-8">
  <title>Text va Font</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&family=Playfair+Display:wght@700&display=swap">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
  <link rel="stylesheet" href="text-fonts.css">
</head>
<body>
  <main class="konteyner">
    <!-- Vazifa 1: Sarlavha -->
    <h1 class="bosh-sarlavha">Mening Blogim</h1>

    <!-- Vazifa 2: Maqola -->
    <article class="maqola">
      <h2>CSS bilan ajoyib dizayn</h2>
      <p class="kirish-para">CSS (Cascading Style Sheets) — veb sahifalarni bezatish uchun...</p>
      <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore.</p>
    </article>

    <!-- Vazifa 3: Rasm + float -->
    <div class="float-demo clearfix">
      <img src="https://picsum.photos/200/150" alt="Float rasm" class="float-rasm">
      <p>Bu matn rasmning o'ng tomonida joylashyapti. Float CSS xossasi yordamida shu effektga erishildi. 
         Float — elementni chap yoki o'ng tomonga "suzishga" majbur qiladi, qolgan elementlar esa uning atrofida joylashadi.</p>
    </div>

    <!-- Vazifa 4-5: Tugmalar va iconlar -->
    <div class="tugmalar-row">
      <button class="tugma tugma--asosiy">
        <i class="fa-solid fa-download"></i> Yuklab olish
      </button>
      <button class="tugma tugma--ikkilamchi">
        <i class="fa-solid fa-share-nodes"></i> Ulashish
      </button>
      <button class="tugma tugma--xavfli">
        <i class="fa-solid fa-trash"></i> O'chirish
      </button>
    </div>

    <!-- Vazifa 6: Social links -->
    <div class="social-links">
      <a href="#" class="social-link github"><i class="fa-brands fa-github"></i></a>
      <a href="#" class="social-link linkedin"><i class="fa-brands fa-linkedin"></i></a>
      <a href="#" class="social-link twitter"><i class="fa-brands fa-x-twitter"></i></a>
      <a href="#" class="social-link youtube"><i class="fa-brands fa-youtube"></i></a>
    </div>

    <!-- Vazifa 7: Qo'tichot (blockquote) -->
    <blockquote class="iqtibos">
      <p>"Dizayn nafaqat ko'rish, balki ishlash haqida"</p>
      <cite>— Steve Jobs</cite>
    </blockquote>

    <!-- Vazifa 8-10: Typography jadval -->
    <div class="tipografiya">
      <h1>Sarlavha 1 — 48px</h1>
      <h2>Sarlavha 2 — 36px</h2>
      <h3>Sarlavha 3 — 28px</h3>
      <p class="katta">Katta paragraf — 20px</p>
      <p>Oddiy paragraf — 16px</p>
      <p class="kichik">Izoh matni — 13px</p>
      <p class="uppercase-text">katta harfga o'girilgan</p>
      <p class="shadowed">Matn soyasi bilan</p>
    </div>
  </main>
</body>
</html>
```

```css
/* text-fonts.css */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

body {
  font-family: "Inter", system-ui, sans-serif;
  font-size: 16px;
  line-height: 1.6;
  color: #1a1a2e;
  background: #f8f9fa;
}

.konteyner { max-width: 860px; margin: 0 auto; padding: 40px 20px; }

/* Vazifa 1: Sarlavha tipografiyasi */
.bosh-sarlavha {
  font-family: "Playfair Display", Georgia, serif;
  font-size: clamp(32px, 6vw, 64px);
  font-weight: 700;
  text-align: center;
  letter-spacing: -1px;
  color: #16213e;
  margin-bottom: 40px;
  text-shadow: 2px 2px 0 rgba(0,0,0,0.05);
}

/* Vazifa 2: Maqola */
.maqola { margin-bottom: 32px; }
.maqola h2 { font-size: 28px; margin-bottom: 12px; }
.kirish-para {
  font-size: 18px;
  color: #444;
  font-style: italic;
  border-left: 4px solid royalblue;
  padding-left: 16px;
  margin-bottom: 16px;
}
.kirish-para::first-letter {
  font-size: 3em;
  font-weight: 700;
  color: royalblue;
  float: left;
  margin: 4px 8px -4px 0;
  font-family: "Playfair Display", serif;
}

/* Vazifa 3: Float */
.float-demo { margin-bottom: 32px; }
.float-rasm {
  float: left;
  margin: 0 20px 12px 0;
  border-radius: 8px;
}
.clearfix::after { content: ""; display: block; clear: both; }

/* Vazifa 4-5: Tugmalar iconlar bilan */
.tugmalar-row { display: flex; gap: 12px; flex-wrap: wrap; margin-bottom: 32px; }
.tugma {
  display: inline-flex; align-items: center; gap: 8px;
  padding: 10px 20px; border: none; border-radius: 8px;
  font-size: 15px; font-weight: 600; cursor: pointer;
  transition: transform 0.2s, box-shadow 0.2s;
}
.tugma:hover { transform: translateY(-2px); box-shadow: 0 4px 12px rgba(0,0,0,0.15); }
.tugma--asosiy   { background: royalblue;  color: white; }
.tugma--ikkilamchi { background: #e2e8f0; color: #2d3748; }
.tugma--xavfli   { background: #fc5c65;   color: white; }

/* Vazifa 6: Social links */
.social-links { display: flex; gap: 12px; margin-bottom: 32px; }
.social-link {
  width: 44px; height: 44px;
  display: inline-flex; align-items: center; justify-content: center;
  border-radius: 50%; font-size: 18px; color: white;
  text-decoration: none; transition: transform 0.3s;
}
.social-link:hover { transform: scale(1.2); }
.social-link.github   { background: #333; }
.social-link.linkedin { background: #0a66c2; }
.social-link.twitter  { background: #000; }
.social-link.youtube  { background: #ff0000; }

/* Vazifa 7: Iqtibos */
.iqtibos {
  margin: 32px 0;
  padding: 24px 32px;
  background: #eef2ff;
  border-left: 5px solid royalblue;
  border-radius: 0 12px 12px 0;
  font-size: 20px;
  font-style: italic;
}
.iqtibos cite {
  display: block;
  font-size: 14px;
  font-style: normal;
  color: #666;
  margin-top: 12px;
}

/* Vazifa 8-10: Tipografiya */
.tipografiya h1 { font-size: 48px; margin-bottom: 8px; }
.tipografiya h2 { font-size: 36px; margin-bottom: 8px; }
.tipografiya h3 { font-size: 28px; margin-bottom: 8px; }
.katta   { font-size: 20px; margin-bottom: 8px; }
.kichik  { font-size: 13px; color: #888; margin-bottom: 8px; }
.uppercase-text { text-transform: uppercase; letter-spacing: 3px; font-size: 13px; color: royalblue; margin-bottom: 8px; }
.shadowed { font-size: 32px; font-weight: 700; text-shadow: 3px 3px 0 royalblue, 6px 6px 0 navy; }
```
