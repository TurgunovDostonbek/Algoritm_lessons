# 01-Dars: CSS ga Kirish

## 📌 CSS nima?

**CSS (Cascading Style Sheets)** — HTML elementlarining ko'rinishini boshqarish tili.
- **Cascading** = Yuqoridan pastga tushish (kaskad qoidalar)
- CSS — dizayn, HTML — tarkib, JavaScript — xulq-atvor

---

## 📌 CSS Qo'shishning 3 Usuli

```html
<!-- 1. Inline (Bevosita elementga) ← Eng past ustuvorlik, foydalanmang -->
<p style="color: red; font-size: 20px;">Matn</p>

<!-- 2. Internal (HTML ichida <style> tegi) -->
<head>
  <style>
    p { color: blue; }
    h1 { font-size: 32px; }
  </style>
</head>

<!-- 3. External (Alohida .css fayl) ← Tavsiya etiladi! -->
<head>
  <link rel="stylesheet" href="style.css">
</head>
```

```css
/* style.css */
p { color: green; }
```

---

## 📌 CSS Selektorlar

### Asosiy Selektorlar

```css
/* Tag (element) selektori */
p { color: blue; }
h1, h2, h3 { font-weight: bold; }  /* Bir nechta */

/* Class selektori (.) */
.btn { background: royalblue; color: white; }
.btn.katta { font-size: 20px; }  /* Ikkala class bir vaqtda */

/* ID selektori (#) */
#sarlavha { font-size: 48px; }   /* Sahifada faqat bitta bo'lishi kerak */

/* Universal (*) */
* { box-sizing: border-box; margin: 0; }

/* Atribut selektori */
input[type="text"] { border: 2px solid blue; }
a[href^="https"] { color: green; }  /* href https bilan boshlanadigan */
a[href$=".pdf"] { color: red; }     /* href .pdf bilan tugaydigan */
a[href*="google"] { color: orange; } /* href ichida google bor */
```

---

## 📌 Kombinatorlar

```css
/* " " (bo'sh joy) — Avlod (barcha ichkilar) */
div p { color: red; }  /* div ichidagi barcha p lar */

/* > — To'g'ridan-to'g'ri bola */
ul > li { list-style: none; }  /* ul ning bevosita li lari */

/* + — Keyingi aka-uka (Adjacent) */
h1 + p { font-size: 18px; }  /* h1 dan keyin kelgan birinchi p */

/* ~ — Keyingi barcha aka-ukalar (General Sibling) */
h1 ~ p { color: gray; }  /* h1 dan keyingi barcha p lar */

/* , — Ro'yxat */
h1, h2, .sarlavha { font-family: Georgia; }
```

---

## 📌 Pseudo-class-lar

```css
/* Holat asosida */
a:hover      { color: red; }       /* Sichqoncha ustida */
a:active     { color: darkred; }   /* Bosilayotganda */
a:visited    { color: purple; }    /* Tashrif buyurilgan */
a:focus      { outline: 2px solid blue; }

/* Pozitsiya asosida */
li:first-child    { font-weight: bold; }
li:last-child     { color: red; }
li:nth-child(2)   { background: yellow; }   /* 2-element */
li:nth-child(odd) { background: #eee; }     /* Toq (1,3,5...) */
li:nth-child(even){ background: #fff; }     /* Juft (2,4,6...) */
li:nth-child(3n)  { color: blue; }          /* Har 3-chi */

/* Input holatlari */
input:required   { border-color: red; }
input:checked    { accent-color: green; }
input:disabled   { opacity: 0.5; }
input:placeholder { color: gray; }
```

---

## 📌 Pseudo-element-lar

```css
/* ::before va ::after — yangi content qo'shish */
.btn::before {
  content: "→ ";
  color: white;
}
.btn::after {
  content: " ←";
}

/* ::first-line va ::first-letter */
p::first-line   { font-weight: bold; }
p::first-letter { font-size: 2em; float: left; }

/* ::selection — tanlanganda */
::selection { background: navy; color: white; }

/* ::placeholder */
input::placeholder { color: #999; font-style: italic; }
```

---

## 📌 HTML ga CSS ulanish namunasi

```html
<!DOCTYPE html>
<html lang="uz">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>CSS Kirish</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <header id="bosh">
    <h1>Mening Saytim</h1>
    <nav>
      <a href="#" class="nav-link">Bosh sahifa</a>
      <a href="#" class="nav-link active">Haqida</a>
    </nav>
  </header>
  <main>
    <p class="kirish-para">Birinchi paragraf.</p>
    <p>Ikkinchi paragraf.</p>
  </main>
</body>
</html>
```

```css
/* style.css */
* { margin: 0; padding: 0; box-sizing: border-box; }

body { font-family: Arial, sans-serif; color: #333; background: #f5f5f5; }

#bosh { background: navy; color: white; padding: 20px; }
#bosh h1 { font-size: 28px; }

.nav-link { color: white; text-decoration: none; margin-right: 15px; }
.nav-link:hover { text-decoration: underline; }
.nav-link.active { font-weight: bold; border-bottom: 2px solid white; }

main { padding: 20px; max-width: 800px; margin: 0 auto; }
.kirish-para::first-letter { font-size: 2em; color: navy; }

/* Kombinatorlar */
main > p { margin-bottom: 16px; }
main p + p { border-top: 1px solid #eee; padding-top: 16px; }

/* Atribut selektori */
a[href^="http"] { color: green; }
a[href^="http"]::after { content: " ↗"; font-size: 12px; }
```

---

## 🎯 10 ta Amaliy Vazifa

```html
<!-- HTML (ikkala fayl uchun) -->
<!DOCTYPE html>
<html lang="uz">
<head><meta charset="UTF-8"><title>Amaliyot</title><link rel="stylesheet" href="vazifalar.css"></head>
<body>
  <h1 id="asosiy-sarlavha">Salom CSS!</h1>
  <p class="kirish">Bu birinchi paragraf.</p>
  <p>Bu ikkinchi paragraf.</p>
  <p>Bu uchinchi paragraf.</p>
  <ul id="royxat">
    <li>Birinchi</li>
    <li>Ikkinchi</li>
    <li>Uchinchi</li>
    <li>To'rtinchi</li>
    <li>Beshinchi</li>
  </ul>
  <a href="https://google.com">Google</a>
  <a href="http://example.com">Example</a>
  <a href="/haqida">Haqida</a>
  <input type="text" placeholder="Yozing...">
  <button class="btn">Bosing</button>
</body>
</html>
```

```css
/* vazifalar.css */

/* 1: ID selektori — asosiy sarlavhani yashil qiling */
#asosiy-sarlavha { color: green; font-size: 36px; text-align: center; }

/* 2: Class selektori — .kirish klassini qo'shing (katta, qo'ng'ir) */
.kirish { font-size: 20px; color: saddlebrown; font-weight: bold; }

/* 3: Tag selektori — barcha p larni 16px, 1.6 line-height */
p { font-size: 16px; line-height: 1.6; margin-bottom: 10px; }

/* 4: Avlod selektori — #royxat ichidagi li lar */
#royxat li { list-style: "➤ "; padding: 5px; color: navy; }

/* 5: :first-child va :last-child */
#royxat li:first-child { color: green; font-weight: bold; }
#royxat li:last-child  { color: red; }

/* 6: :nth-child — juft raqamli li larga kulrang fon */
#royxat li:nth-child(even) { background: #eee; }

/* 7: Atribut selektori — https bilan boshlanadigan link lar */
a[href^="https"] { color: green; font-weight: bold; }
a[href^="http"]:not([href^="https"]) { color: orange; }
a:not([href^="http"]) { color: royalblue; }

/* 8: :hover va :focus effektlari */
a:hover { text-decoration: none; opacity: 0.7; }
input:focus { outline: 3px solid royalblue; border-radius: 4px; }

/* 9: ::before va ::after */
.btn::before { content: "🚀 "; }
.btn::after  { content: " →"; }
.btn { background: royalblue; color: white; padding: 10px 20px; border: none;
       cursor: pointer; border-radius: 6px; font-size: 15px; }

/* 10: + kombinatori — h1 dan keyingi birinchi p */
h1 + p { border-left: 4px solid green; padding-left: 12px; background: #f0fff0; }
```
