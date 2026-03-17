# 02-Dars: HTMLga Kirish va Asosiy Tuzilma

## 📌 HTML nima?

**HTML (HyperText Markup Language)** — veb sahifalarning tarkibini belgilaydigan markup tili.

- **HyperText** → Sahifalar o'rtasida havolalar
- **Markup** → Matnni maxsus teglar bilan belgilash
- **Language** → Brauzer tushunadigan til

---

## 📌 Dastlabki/Asosiy Struktura

```html
<!DOCTYPE html>
<html lang="uz">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="Sahifa tavsifi">
  <title>Sahifa Nomi</title>
  <link rel="stylesheet" href="style.css">
</head>

<body>
  <!-- Sahifa ko'rinadigan qismi bu yerda -->
  <h1>Salom!</h1>
  <p>Bu birinchi sahifam.</p>

  <script src="script.js"></script>
</body>

</html>
```

---

## 📌 `<!DOCTYPE html>` nima?

```html
<!DOCTYPE html>
<!-- Bu HTML5 ekanligini brauzerga bildiradi -->
<!-- MAJBURIY — har doim birinchi qatorda bo'lishi kerak -->
<!-- Tag emas, direktiva (buyruq) -->
```

---

## 📌 `<html>` — Ildiz Element

```html
<html lang="uz">
  <!-- lang — sahifa tilini bildiradi -->
  <!-- uz = Uzbek, en = English, ru = Russian, ar = Arabic -->
  <!-- Ekran o'quvchilar va SEO uchun muhim -->
</html>
```

---

## 📌 `<head>` — Meta Ma'lumotlar

```html
<head>
  <!-- 1. Kodlash tizimi — BIRINCHI bo'lishi kerak! -->
  <meta charset="UTF-8">
  <!-- UTF-8 = O'zbek, Rus, Xitoy harflari qo'llab-quvvatlanadi -->

  <!-- 2. Responsive uchun viewport -->
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <!-- 3. Sahifa sarlavhasi — Brauzer tabida ko'rinadi -->
  <title>Mening Saytim | Bosh Sahifa</title>

  <!-- 4. SEO meta teglari -->
  <meta name="description" content="Sayt tavsifi (150-160 belgi)">
  <meta name="keywords" content="html, css, javascript">
  <meta name="author" content="Ali Valiev">

  <!-- 5. CSS ulash -->
  <link rel="stylesheet" href="css/style.css">

  <!-- 6. Favicon (brauzer tab ikonkasi) -->
  <link rel="icon" type="image/x-icon" href="favicon.ico">
  <link rel="icon" type="image/png" href="icon-32.png" sizes="32x32">

  <!-- 7. Google Fonts -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Inter&display=swap">
</head>
```

---

## 📌 `<body>` — Ko'rinadigan Qism

```html
<body>
  <!-- Sarlavha -->
  <header>
    <nav>...</nav>
  </header>

  <!-- Asosiy kontent -->
  <main>
    <h1>Bosh sarlavha</h1>
    <p>Paragraf.</p>
  </main>

  <!-- Yon panel -->
  <aside>...</aside>

  <!-- Oyoq qism -->
  <footer>...</footer>

  <!-- JS — body oxirida (DOM tayyor bo'lishi uchun) -->
  <script src="js/main.js"></script>
</body>
```

---

## 📌 HTML Versiyalari

| Versiya | Yil | Muhim xususiyat |
|---------|-----|-----------------|
| HTML 1.0 | 1993 | Oddiy matn |
| HTML 4.01 | 1999 | Formalar, jadvallar |
| XHTML | 2000 | Qat'iy sintaksis |
| **HTML5** | **2014** | **Hozirgi standart** |

```html
<!-- HTML5 yangiliklari -->
<header>, <nav>, <main>, <section>, <article>, <aside>, <footer>
<video>, <audio>, <canvas>, <svg>
<input type="email">, <input type="date">, <input type="color">
```

---

## 📌 Coding Environment — VS Code

```
VS Code o'rnatish:
1. https://code.visualstudio.com/ dan yuklab oling
2. O'rnating
3. Quyidagi extension lar o'rnating:
   ✅ Live Server (ritwickdey.liveserver)
   ✅ Prettier (esbenp.prettier-vscode)
   ✅ Auto Rename Tag
   ✅ HTML CSS Support

Emmet (VS Code built-in):
! + Tab          → HTML boilerplate
h1 + Tab         → <h1></h1>
p*3 + Tab        → 3 ta paragraf
ul>li*5 + Tab    → ul ichida 5 li
div.klass + Tab  → <div class="klass"></div>
div#id + Tab     → <div id="id"></div>
```

---

## 🎯 10 ta Amaliy Vazifa

### Vazifa 1: Amaliyot: Oddiy "Hello World!" sahifasini yaratish
```html
<!DOCTYPE html>
<html lang="uz">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Hello World</title>
</head>
<body>
  <h1>Hello, World! 🌍</h1>
  <p>Bu mening birinchi HTML sahifam.</p>
</body>
</html>
```

### Vazifa 2: Lang atributini o'rganing
```html
<!-- Quyidagi sahifalarni yarating va har birida lang o'zgartiring -->
<html lang="uz">  <!-- O'zbekcha sahifa -->
<html lang="en">  <!-- Inglizcha sahifa -->
<html lang="ru">  <!-- Ruscha sahifa -->
<!-- DevTools → Accessibility → Language ni tekshiring -->
```

### Vazifa 3: Viewport meta tegi ahamiyati
```html
<!-- Telefonda Ko'rinish farqlarini sinab ko'ring -->

<!-- meta viewport BILAN -->
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<!-- meta viewport SIFATSIZ — telefonda kichik ko'rinadi! -->
<!-- Chrome DevTools → Ctrl+Shift+M → Mobil ko'rinish -->
```

### Vazifa 4: Favicon qo'shish
```html
<head>
  <link rel="icon" type="image/png" href="favicon.png">
  <!-- favicon.png faylini 32x32 piksel rasm sifatida yarating -->
  <!-- yoki https://favicon.io/ dan yuklab oling -->
</head>
```

### Vazifa 5: Google Fonts qo'shish
```html
<head>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap">
  <style>
    body { font-family: "Inter", sans-serif; }
  </style>
</head>
```

### Vazifa 6: To'liq sahifa tuzilmasi
```html
<!DOCTYPE html>
<html lang="uz">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="Ali Valevning shaxsiy portfolio sayti">
  <meta name="author" content="Ali Valiev">
  <title>Ali Valiev | Portfolio</title>
  <link rel="stylesheet" href="style.css">
  <link rel="icon" href="favicon.ico">
</head>
<body>
  <header>
    <nav>Navigatsiya</nav>
  </header>
  <main>
    <h1>Asosiy Kontent</h1>
  </main>
  <footer>
    <p>© 2024 Ali Valiev</p>
  </footer>
  <script src="main.js"></script>
</body>
</html>
```

### Vazifa 7: Wikipedia dan o'rganish
```
1. https://en.wikipedia.org/wiki/Avicenna oching
2. Sahifadagi head elementlarini ko'ring (View Source bilan)
3. Qanday meta teglar ishlatilganiga e'tibor bering
4. title tagi qanday yozilganini ko'ring
```

### Vazifa 8: W3School dan o'rganish
```
1. https://www.w3schools.com/html/html_head.asp oching
2. Barcha head elementlarini o'qing
3. "Try it Yourself" da sinab ko'ring
4. <base>, <style>, <script> elementlarini o'rganing
```

### Vazifa 9: Emmet bilan tez yozish
```
VS Code da quyidagi Emmet iboralarini sinab ko'ring:
! + Tab                          → To'liq boilerplate
html:5 + Tab                     → Alternativ usul
head>meta:utf + Tab              → meta charset
head>link:css + Tab              → CSS ulash
head>script:src + Tab            → Script ulash
meta:vp + Tab                    → Viewport meta
```

### Vazifa 10: Loyiha fayl strukturasi
```
Quyidagi strukturada loyiha yarating:

portfolio/
├── index.html
├── haqida.html
├── loyihalar.html
├── aloqa.html
├── css/
│   ├── style.css
│   └── responsive.css
├── js/
│   └── main.js
└── images/
    ├── avatar.jpg
    └── logo.png

Har bir HTML faylda to'g'ri `<title>` va `<meta>` teglarini yozing.
```
