# 04-Dars: HTMLdagi Strukturaviy Elementlar

## 📌 Block va Inline Elementlar

```
Block Elementlar:
├── Yangi qatordan boshlanadi
├── To'liq kenglikni egallaydi (default: 100%)
├── Width, Height, Margin, Padding ISHLAYDI
└── Misol: div, p, h1-h6, ul, ol, li, table, form, header, main, footer

Inline Elementlar:
├── Qator ichida joylashadi
├── Faqat kontent kengligi
├── Width va Height ISHLAMAYDI
├── Vertikal margin ISHLAMAYDI
└── Misol: span, a, img, strong, em, code, br, input, button
```

---

## 📌 `<div>` — Bo'linma (Block)

```html
<!-- div — hech qanday semantik ma'nosi yo'q, faqat guruh -->
<div class="konteyner">
  <div class="qator">
    <div class="ustun">Kontent 1</div>
    <div class="ustun">Kontent 2</div>
  </div>
</div>

<!-- Qachon div ishlatiladi? -->
<!-- - Bir nechta elementlarni guruhlash -->
<!-- - CSS bilan stil berish -->
<!-- - JavaScript bilan boshqarish -->
<!-- - Layout yaratish -->
```

---

## 📌 `<span>` — Inline Guruh

```html
<!-- span — inline, semantik ma'nosi yo'q -->
<p>Mening sevimli rangim <span style="color: royalblue; font-weight: bold;">ko'k</span>.</p>

<p>
  Telefon: <span class="telefon">+998 90 123 45 67</span> |
  Email: <span class="email">ali@mail.com</span>
</p>

<!-- JavaScript uchun -->
<p>Xush kelibsiz, <span id="ism-joy">Mehmon</span>!</p>
<script>
  document.getElementById("ism-joy").textContent = "Ali";
</script>
```

---

## 📌 Semantik HTML5 Elementlar

```html
<!-- Semantik elementlar ma'noga ega -->
<body>

  <!-- Sahifa sarlavhasi / logo va nav uchun -->
  <header>
    <nav>...</nav>
  </header>

  <!-- Asosiy navigatsiya -->
  <nav>
    <ul>
      <li><a href="/">Bosh</a></li>
      <li><a href="/haqida">Haqida</a></li>
    </ul>
  </nav>

  <!-- Sahifaning asosiy yagona kontent qismi -->
  <main>

    <!-- Mustaqil kontent (maqola, yangilik) -->
    <article>
      <h1>Maqola sarlavhasi</h1>
      <p>Maqola matni...</p>
    </article>

    <!-- Tematik guruh -->
    <section>
      <h2>Bo'lim sarlavhasi</h2>
      <p>Bo'lim matni...</p>
    </section>

  </main>

  <!-- Yon panel — qo'shimcha kontent -->
  <aside>
    <h3>So'nggi yangiliklar</h3>
  </aside>

  <!-- Sahifa pastki qismi -->
  <footer>
    <p>© 2024 MyApp</p>
  </footer>

</body>
```

---

## 📌 Div vs Semantik Elementlar

```html
<!-- ❌ YOMON — div soup (div to'pi) -->
<div class="header">
  <div class="nav">
    <div class="nav-item">Bosh</div>
  </div>
</div>
<div class="main">
  <div class="article">...</div>
</div>
<div class="footer">...</div>

<!-- ✅ YAXSHI — Semantik HTML -->
<header>
  <nav>
    <a href="/">Bosh</a>
  </nav>
</header>
<main>
  <article>...</article>
</main>
<footer>...</footer>
```

---

## 📌 Boshqa Semantik Elementlar

```html
<!-- figure — rasm + izoh -->
<figure>
  <img src="ibn-sino.jpg" alt="Ibn Sino portreti">
  <figcaption>Ibn Sino (980–1037) — buyuk alloma</figcaption>
</figure>

<!-- time — vaqt va sana -->
<time datetime="2024-01-15">15 yanvar 2024</time>
<time datetime="2024-01-15T13:30">2024 yil 15 yanvar, soat 13:30</time>

<!-- address — manzil ma'lumoti -->
<address>
  <strong>Ali Valiev</strong><br>
  Toshkent, O'zbekiston<br>
  <a href="tel:+998901234567">+998 90 123 45 67</a><br>
  <a href="mailto:ali@mail.com">ali@mail.com</a>
</address>

<!-- details va summary — yashirin kontent -->
<details>
  <summary>Ko'proq o'qish ▼</summary>
  <p>Bu yashirin kontent. Summary ga bosganda ochiladi.</p>
</details>

<!-- dialog — modal oyna -->
<dialog id="modal">
  <p>Bu modal oyna!</p>
  <button onclick="document.getElementById('modal').close()">Yopish</button>
</dialog>
<button onclick="document.getElementById('modal').showModal()">Ochish</button>
```

---

## 📌 display Xossasi bilan O'zgartirish

```html
<style>
  /* Block → Inline-block */
  .block-el { display: inline-block; }

  /* Inline → Block */
  .inline-el { display: block; }

  /* Hamma narsani flex qilish */
  .flex-konteyner { display: flex; gap: 16px; }
</style>
```

---

## 🎯 10 ta Amaliy Vazifa

### Vazifa 1: Block va Inline farqini ko'rish
```html
<!DOCTYPE html>
<html lang="uz">
<head>
  <meta charset="UTF-8">
  <title>Block va Inline</title>
  <style>
    .block-demo div   { background: #dbeafe; margin: 4px; padding: 8px; }
    .inline-demo span { background: #dcfce7; margin: 4px; padding: 8px; }
  </style>
</head>
<body>
  <h2>Block elementlar (har biri yangi qatordan)</h2>
  <div class="block-demo">
    <div>Block 1</div>
    <div>Block 2</div>
    <div>Block 3</div>
  </div>

  <h2>Inline elementlar (qatorda joylashadi)</h2>
  <div class="inline-demo">
    <span>Inline 1</span>
    <span>Inline 2</span>
    <span>Inline 3</span>
  </div>
</body>
</html>
```

### Vazifa 2: Oddiy Blog sahifasini yaratish
```html
<!DOCTYPE html>
<html lang="uz">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Mening Blogim</title>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body { font-family: "Segoe UI", sans-serif; background: #f8f9fa; color: #1a1a2e; }
    header { background: #16213e; color: white; padding: 20px 40px; }
    header h1 { font-size: 28px; }
    nav { background: #0f3460; padding: 12px 40px; }
    nav a { color: rgba(255,255,255,0.8); text-decoration: none; margin-right: 20px; }
    nav a:hover { color: white; }
    .wrapper { display: flex; max-width: 1100px; margin: 30px auto; gap: 24px; padding: 0 20px; }
    main { flex: 1; }
    aside { width: 280px; }
    article { background: white; padding: 28px; border-radius: 12px; margin-bottom: 20px; box-shadow: 0 2px 12px rgba(0,0,0,0.06); }
    article h2 { margin-bottom: 12px; }
    .sidebar-blok { background: white; padding: 20px; border-radius: 12px; margin-bottom: 16px; }
    .sidebar-blok h3 { margin-bottom: 12px; font-size: 16px; }
    footer { background: #16213e; color: rgba(255,255,255,0.7); text-align: center; padding: 20px; margin-top: 40px; }
  </style>
</head>
<body>
  <header>
    <h1>📝 Mening Blogim</h1>
    <p>HTML, CSS va JavaScript haqida</p>
  </header>

  <nav>
    <a href="#">🏠 Bosh</a>
    <a href="#">📖 Maqolalar</a>
    <a href="#">👤 Haqimda</a>
    <a href="#">📬 Aloqa</a>
  </nav>

  <div class="wrapper">
    <main>
      <article>
        <h2>HTML5 da Semantik Elementlar</h2>
        <time datetime="2024-01-15" style="color: #888; font-size: 13px;">15 Yanvar 2024</time>
        <p style="margin-top: 12px; line-height: 1.7;">
          HTML5 da <strong>semantik elementlar</strong> joriy etildi.
          Bu elementlar sahifaning tuzilmasini <em>aniqroq</em> ifodalaydi.
        </p>
        <p style="margin-top: 12px;">
          Misol uchun, <code>&lt;header&gt;</code>, <code>&lt;main&gt;</code>,
          <code>&lt;footer&gt;</code> elementlari.
        </p>
      </article>

      <article>
        <h2>CSS Grid vs Flexbox</h2>
        <time datetime="2024-01-10" style="color: #888; font-size: 13px;">10 Yanvar 2024</time>
        <p style="margin-top: 12px; line-height: 1.7;">
          <mark>Grid</mark> ikki o'lchovli, <mark>Flexbox</mark> bir o'lchovli layout uchun.
        </p>
      </article>
    </main>

    <aside>
      <div class="sidebar-blok">
        <h3>📌 Kategoriyalar</h3>
        <ul>
          <li>HTML (5)</li>
          <li>CSS (8)</li>
          <li>JavaScript (12)</li>
        </ul>
      </div>
      <div class="sidebar-blok">
        <h3>🔥 Mashhur Maqolalar</h3>
        <p><a href="#">Flexbox to'liq qo'llanma</a></p>
        <p><a href="#">JavaScript asoslari</a></p>
      </div>
    </aside>
  </div>

  <footer>
    <p>© 2024 Mening Blogim | Barcha huquqlar himoyalangan</p>
  </footer>
</body>
</html>
```

### Vazifa 3: Card (Karta) yaratish
```html
<!DOCTYPE html>
<html lang="uz">
<head>
  <meta charset="UTF-8">
  <title>Karta Komponenti</title>
  <style>
    body { display: flex; gap: 20px; flex-wrap: wrap; justify-content: center; padding: 40px; background: #f0f2f5; }
    .karta {
      background: white; border-radius: 16px; overflow: hidden;
      width: 300px; box-shadow: 0 4px 20px rgba(0,0,0,0.08);
    }
    .karta img { width: 100%; height: 200px; object-fit: cover; display: block; }
    .karta-tanasi { padding: 20px; }
    .karta-tanasi h3 { margin-bottom: 8px; }
    .karta-tanasi p { color: #666; font-size: 14px; line-height: 1.6; margin-bottom: 16px; }
    .karta-oyoq { display: flex; justify-content: space-between; align-items: center; }
    .tugma { background: royalblue; color: white; padding: 8px 16px; border: none; border-radius: 6px; cursor: pointer; }
    .teg { background: #f0f4ff; color: royalblue; padding: 4px 10px; border-radius: 20px; font-size: 12px; }
  </style>
</head>
<body>
  <div class="karta">
    <img src="https://picsum.photos/300/200?random=1" alt="Maqola rasmi">
    <div class="karta-tanasi">
      <span class="teg">HTML</span>
      <h3 style="margin-top: 8px;">Semantik HTML5</h3>
      <p>HTML5 ning semantik elementlari veb sahifalarni aniqroq tashkil etishga yordam beradi.</p>
      <div class="karta-oyoq">
        <button class="tugma">O'qish →</button>
        <time style="color: #888; font-size: 13px;">15 Jan 2024</time>
      </div>
    </div>
  </div>

  <div class="karta">
    <img src="https://picsum.photos/300/200?random=2" alt="Maqola rasmi">
    <div class="karta-tanasi">
      <span class="teg">CSS</span>
      <h3 style="margin-top: 8px;">CSS Grid Layout</h3>
      <p>CSS Grid — 2 o'lchovli layout yaratishning eng qulay usullaridan biri.</p>
      <div class="karta-oyoq">
        <button class="tugma">O'qish →</button>
        <time style="color: #888; font-size: 13px;">10 Jan 2024</time>
      </div>
    </div>
  </div>
</body>
</html>
```

### Vazifa 4: details va summary
```html
<div style="max-width: 600px; margin: 40px auto; font-family: Arial;">
  <h2>Ko'p beriladigan savollar (FAQ)</h2>

  <details style="border: 1px solid #ddd; border-radius: 8px; padding: 12px; margin: 8px 0;">
    <summary style="cursor: pointer; font-weight: bold;">HTML nima?</summary>
    <p style="margin-top: 12px; color: #555;">HTML — HyperText Markup Language. Veb sahifalar tarkibini belgilash tili.</p>
  </details>

  <details style="border: 1px solid #ddd; border-radius: 8px; padding: 12px; margin: 8px 0;">
    <summary style="cursor: pointer; font-weight: bold;">CSS nima?</summary>
    <p style="margin-top: 12px; color: #555;">CSS — Cascading Style Sheets. Sahifaning ko'rinishini boshqarish tili.</p>
  </details>

  <details style="border: 1px solid #ddd; border-radius: 8px; padding: 12px; margin: 8px 0;">
    <summary style="cursor: pointer; font-weight: bold;">JavaScript nima?</summary>
    <p style="margin-top: 12px; color: #555;">JavaScript — brauzerda amalga oshiriladigan dasturlash tili.</p>
  </details>
</div>
```

### Vazifa 5-10: Qo'shimcha topshiriqlar
```
Vazifa 5: Figma dan loyiha klonlash
  - Figma da oddiy blog dizayni ko'rib HTML bilan yarating

Vazifa 6: figure va figcaption bilan rasmli maqola

Vazifa 7: address tegi bilan aloqa sahifasi

Vazifa 8: time tegi bilan voqealar jadvali

Vazifa 9: dialog (modal) tegi bilan popup

Vazifa 10: To'liq portfolio bosh sahifasi:
  - header (logo + nav)
  - main (hero + kartalar)
  - aside (ijtimoiy havolalar)
  - footer (copyright)
```
