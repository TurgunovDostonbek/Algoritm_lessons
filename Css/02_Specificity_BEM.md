# 02-Dars: Specificity (O'ziga Xoslik) va Meros

## 📌 Specificity nima?

Bir elementga bir nechta CSS qoidalari tegishli bo'lsa, qaysi biri g'alaba qilishini specificity hal qiladi.

```
Specificity hisobi (0, 0, 0, 0):
├── [1,0,0,0] — !important  (eng kuchli)
├── [0,1,0,0] — Inline style (style="...")
├── [0,0,1,0] — ID (#id)
├── [0,0,1,0] — Pseudo-element (::before)
├── [0,0,0,1] — Class (.class), Pseudo-class (:hover), Atribut ([type])
├── [0,0,0,1] — Element/Tag (p, div, span)
└── [0,0,0,0] — Universal (*), Kombinator (>, +, ~, " ")
```

---

## 📌 Specificity Hisoblash

```css
/* Specificity: 0-0-0-1 (1 tag) */
p { color: black; }

/* Specificity: 0-0-1-0 (1 class) */
.matn { color: blue; }

/* Specificity: 0-1-0-0 (1 ID) */
#sarlavha { color: red; }

/* Specificity: 0-0-1-1 (1 class + 1 tag) */
p.matn { color: green; }

/* Specificity: 0-1-1-0 (1 ID + 1 class) */
#sarlavha.asosiy { color: purple; }

/* Specificity: 0-1-0-1 (1 ID + 1 tag) */
div#container { color: orange; }

/* Qaysi kuchli? */
/* 0-1-1-0 > 0-1-0-1 > 0-1-0-0 > 0-0-1-1 > 0-0-1-0 > 0-0-0-1 */
```

---

## 📌 !important — Eng kuchli

```css
/* !important — BARCHA specificity dan kuchli */
p { color: red !important; }  /* Bu har doim ishlaydi */

/* ⚠️ !important dan iloji boricha foydalanmang! */
/* Faqat tashqi kutubxonani override qilishda */
```

---

## 📌 Specificity Misollar

```html
<p id="birinchi" class="matn" style="color: pink;">Bu matn</p>
```

```css
p            { color: black; }    /* 0,0,0,1 */
.matn        { color: blue; }     /* 0,0,1,0 */
#birinchi    { color: red; }      /* 0,1,0,0 */
/* style="..." → */               /* 1,0,0,0 → PINK yutadi */
```

---

## 📌 Inheritance (Meros Olish)

Ba'zi CSS xossalar ota elementdan bolaga o'tadi (meros), ba'zilari o'tmaydi.

```css
/* ✅ Meros oluvchi xossalar */
color, font-family, font-size, font-weight, font-style,
text-align, line-height, letter-spacing, word-spacing,
visibility, cursor, list-style, quotes

/* ❌ Meros olmaydigan xosslar */
margin, padding, border, background, width, height,
display, position, top, left, overflow, box-shadow
```

```html
<div style="color: blue; font-family: Arial; border: 2px solid red;">
  <p>Bu paragraf meros oladi:</p>
  <!--   color: blue ✅ (meros)
         font-family ✅ (meros)
         border ❌ (meros emas) -->
</div>
```

---

## 📌 `inherit`, `initial`, `unset`, `revert`

```css
.bola {
  /* inherit — ota elementdan olish (majburiy) */
  color: inherit;
  
  /* initial — brauzer boshlang'ich qiymatiga qaytish */
  display: initial;  /* inline bo'ladi */
  
  /* unset — meros bo'lsa inherit, aks holda initial */
  margin: unset;
  
  /* revert — brauzer stillari ga qaytish */
  font-size: revert;
}

/* all xossasi — barchasini reset qilish */
.reset { all: unset; }
```

---

## 📌 Comments (Izohlar)

```css
/* Bu bir qatorli izoh */

/*
  Bu ko'p
  qatorli
  izoh
*/

/* === HEADER SECTION === */
header { ... }

/* TODO: Responsive qo'shish */
/* FIXME: Bu qism safari da ishlamayapti */
```

---

## 📌 BEM (Block Element Modifier)

```
block__element--modifier
```

```html
<!-- BEM namunasi: KARTA komponenti -->
<div class="karta">
  <div class="karta__rasm">
    <img src="..." alt="">
  </div>
  <div class="karta__matn">
    <h2 class="karta__sarlavha">Sarlavha</h2>
    <p class="karta__tavsif">Tavsif</p>
  </div>
  <div class="karta__tugmalar">
    <button class="karta__tugma">Ko'rish</button>
    <button class="karta__tugma karta__tugma--asosiy">Sotib olish</button>
    <button class="karta__tugma karta__tugma--xavfli">O'chirish</button>
  </div>
</div>
```

```css
/* Block */
.karta { border: 1px solid #ddd; border-radius: 12px; overflow: hidden; }

/* Elements */
.karta__rasm { width: 100%; }
.karta__rasm img { width: 100%; height: 200px; object-fit: cover; }
.karta__matn { padding: 16px; }
.karta__sarlavha { font-size: 20px; margin-bottom: 8px; }
.karta__tavsif { color: #666; line-height: 1.5; }
.karta__tugmalar { display: flex; gap: 8px; padding: 16px; border-top: 1px solid #eee; }

/* Modifiers */
.karta__tugma { padding: 8px 16px; border: none; border-radius: 6px; cursor: pointer; }
.karta__tugma--asosiy { background: royalblue; color: white; }
.karta__tugma--xavfli { background: #ff6b6b; color: white; }
```

---

## 🎯 10 ta Amaliy Vazifa

```html
<!DOCTYPE html>
<html lang="uz">
<head><meta charset="UTF-8"><title>Specificity Amaliyot</title>
<link rel="stylesheet" href="specificity.css"></head>
<body>
  <h1 id="bosh-sarlavha" class="sarlavha katta-sarlavha" style="font-style: italic;">
    Sarlavha
  </h1>
  <p class="matn">Oddiy matn</p>
  <p class="matn muhim-matn">Muhim matn</p>

  <!-- BEM — Karta komponenti -->
  <div class="karta">
    <img class="karta__rasm" src="https://picsum.photos/300/200" alt="Rasm">
    <div class="karta__tana">
      <h2 class="karta__sarlavha">Produkt Nomi</h2>
      <p class="karta__narx">150,000 so'm</p>
      <div class="karta__tugmalar">
        <button class="btn btn--asosiy">Sotib olish</button>
        <button class="btn btn--ikkilamchi">Saqlash</button>
        <button class="btn btn--xavfli">O'chirish</button>
      </div>
    </div>
  </div>
</body>
</html>
```

```css
/* specificity.css */

/* Vazifa 1: Tag selektori */
h1 { color: black; }

/* Vazifa 2: Class selektori — .sarlavha */
.sarlavha { color: royalblue; }

/* Vazifa 3: Ko'p class — qaysi g'alaba qiladi? (.katta-sarlavha kuchli!) */
.katta-sarlavha { font-size: 42px; }

/* Vazifa 4: ID selektori — #bosh-sarlavha (bu g'alaba qiladi!) */
#bosh-sarlavha { color: darkgreen; text-align: center; }
/* Lekin style="" font-style: italic ni qo'llaydi (1,0,0,0) */

/* Vazifa 5: Meros — matn rangini ota elementdan olish */
body { color: #333; font-family: "Segoe UI", sans-serif; }

/* Vazifa 6: Specificity taqqoslash */
p { color: gray; }              /* 0,0,0,1 */
.matn { color: navy; }          /* 0,0,1,0 — yutadi */
.muhim-matn { color: crimson; } /* 0,0,1,0 — KEYIN yozilgani yutadi */

/* Vazifa 7: !important */
.matn { font-size: 14px !important; }
#bosh-sarlavha { font-size: 48px; } /* bu ham !important dan zaif */

/* Vazifa 8: BEM Block */
.karta {
  max-width: 300px;
  border: 1px solid #e0e0e0;
  border-radius: 12px;
  overflow: hidden;
  box-shadow: 0 4px 12px rgba(0,0,0,0.08);
  margin: 20px auto;
}

/* Vazifa 9: BEM Elements */
.karta__rasm { width: 100%; height: 200px; object-fit: cover; display: block; }
.karta__tana { padding: 16px; }
.karta__sarlavha { font-size: 18px; font-weight: bold; margin-bottom: 8px; }
.karta__narx { color: crimson; font-size: 20px; font-weight: bold; margin-bottom: 16px; }
.karta__tugmalar { display: flex; gap: 8px; flex-wrap: wrap; }

/* Vazifa 10: BEM Modifiers */
.btn { padding: 8px 16px; border: none; border-radius: 6px; cursor: pointer;
       font-size: 14px; font-weight: 600; transition: opacity 0.2s; }
.btn:hover { opacity: 0.85; }
.btn--asosiy   { background: royalblue; color: white; }
.btn--ikkilamchi { background: #e0e0e0; color: #333; }
.btn--xavfli   { background: #ff6b6b; color: white; }
```
