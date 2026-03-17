# 12-Dars: Semantics va Umumiy Takrorlash (Imtihonga Tayyorgarlik)

---

## 📌 1. Semantik HTML nima?

**Semantik** — elementning o'z ma'nosiga ega bo'lishi. Brauzer, qidiruv tizimlari (Google) va dasturlar tegning nima ekanini tushunadi.

```html
<!-- ❌ NON-SEMANTIC — div va span ma'nosiz -->
<div class="header">
  <div class="nav">
    <div class="nav-item">Bosh sahifa</div>
  </div>
</div>
<div class="content">
  <div class="article">
    <div class="title">Maqola sarlavhasi</div>
    <div class="para">Matn...</div>
  </div>
</div>
<div class="footer">...</div>

<!-- ✅ SEMANTIC — teglar o'z ma'nosini bildiradi -->
<header>
  <nav>
    <a href="/">Bosh sahifa</a>
  </nav>
</header>
<main>
  <article>
    <h1>Maqola sarlavhasi</h1>
    <p>Matn...</p>
  </article>
</main>
<footer>...</footer>
```

---

## 📌 2. Barcha Semantik Elementlar

### 🏗 Sahifa Tuzilmasi

| Element | Ma'nosi | Qachon ishlatiladi |
|---------|---------|-------------------|
| `<header>` | Sarlavha qismi | Sayt yoki section sarlavhasi |
| `<nav>` | Navigatsiya | Havolalar ro'yxati |
| `<main>` | Asosiy kontent | Sahifada faqat **bir marta** |
| `<article>` | Mustaqil kontent | Maqola, yangilik, post |
| `<section>` | Tematik bo'lim | Guruhlashtirish uchun |
| `<aside>` | Yon panel | Qo'shimcha kontent, reklama |
| `<footer>` | Pastki qism | Kopyayt, aloqa |

```html
<!DOCTYPE html>
<html lang="uz">
<head>
  <meta charset="UTF-8">
  <title>Semantik Sahifa</title>
</head>
<body>

  <header>                          <!-- Sahifa sarlavhasi -->
    <h1>MyBlog</h1>
    <nav aria-label="Asosiy">
      <a href="/">Bosh</a>
      <a href="/blog">Blog</a>
      <a href="/aloqa">Aloqa</a>
    </nav>
  </header>

  <main>                            <!-- Asosiy kontent (1 ta!) -->

    <section aria-labelledby="yangiliklar">
      <h2 id="yangiliklar">So'nggi Maqolalar</h2>

      <article>                     <!-- Mustaqil maqola -->
        <header>
          <h3>HTML Semantics nima?</h3>
          <time datetime="2024-03-15">15 Mart, 2024</time>
        </header>
        <p>Semantik HTML deganda...</p>
        <footer>
          <address>Muallif: <a href="/ali">Ali Valiev</a></address>
        </footer>
      </article>

      <article>
        <header>
          <h3>CSS Grid to'liq qo'llanma</h3>
          <time datetime="2024-03-10">10 Mart, 2024</time>
        </header>
        <p>CSS Grid deganda...</p>
      </article>

    </section>

    <aside aria-label="Yon panel">  <!-- Qo'shimcha kontent -->
      <section>
        <h3>Mashhur Maqolalar</h3>
        <ul>
          <li><a href="#">HTML 5 yangiliklari</a></li>
          <li><a href="#">Flexbox vs Grid</a></li>
        </ul>
      </section>
    </aside>

  </main>

  <footer>                          <!-- Sahifa pastki qismi -->
    <p>© 2024 MyBlog</p>
    <address>
      <a href="mailto:info@myblog.uz">info@myblog.uz</a>
    </address>
  </footer>

</body>
</html>
```

---

### 📝 Matn Semantikasi

| Element | Ma'nosi | Misol |
|---------|---------|-------|
| `<h1>`–`<h6>` | Sarlavhalar (ierarxiya) | Faqat bitta `<h1>`! |
| `<p>` | Paragraf | Oddiy matn uchun |
| `<strong>` | **Muhim** matn (bold) | "Bu **muhim**!" |
| `<em>` | *Ta'kidlangan* matn (italic) | "*Diqqat* biling" |
| `<mark>` | ==Belgilangan== matn | Qidiruvda topilgan so'z |
| `<time>` | Sana/vaqt | `<time datetime="2024-01-01">` |
| `<address>` | Manzil/kontakt | Email, telefon, jismoniy manzil |
| `<cite>` | Manbaa | Kitob, film, maqola nomi |
| `<code>` | Kod | `const x = 5;` |
| `<pre>` | Formatlangan matn | Kod bloki |
| `<abbr>` | Qisqartma | `<abbr title="HyperText ML">HTML</abbr>` |
| `<blockquote>` | Katta iqtibos | Boshqa manbadan |
| `<q>` | Kichik iqtibos | Ichki qatorli |
| `<del>` | ~~O'chirilgan~~ matn | Narx chegirmasi |
| `<ins>` | Qo'shilgan matn | Yangilanma |
| `<sup>` | Yuqori indeks | x² |
| `<sub>` | Quyi indeks | H₂O |
| `<small>` | Kichik matn | Eslatma, huquqiy matn |
| `<hr>` | Mavzular orasidagi chiziq | Tematik ajratgich |
| `<br>` | Qator uzilishi | Manzil, she'r |
| `<wbr>` | Ixtiyoriy qator uzilishi | Uzun URL da |

```html
<article>
  <h1>Dasturlash Asoslari</h1>
  <p>
    <strong>Dasturlash</strong> — bu kompyuterga buyruqlar berishdir.
    <em>To'g'ri o'rganish</em> uchun amaliyot juda muhim.
  </p>

  <blockquote cite="https://en.wikipedia.org/wiki/Programming">
    "Programming is the process of writing instructions for computers."
    <cite>— Wikipedia</cite>
  </blockquote>

  <p>
    HTML ning to'liq nomi:
    <abbr title="HyperText Markup Language">HTML</abbr>
  </p>

  <p>
    Eskilarcha narxi: <del>150,000 so'm</del>
    Yangi narxi: <ins>99,000 so'm</ins>
  </p>

  <p>
    Kimyoviy formula: H<sub>2</sub>O
    Matematik: x<sup>2</sup> + y<sup>2</sup> = r<sup>2</sup>
  </p>

  <time datetime="2024-03-15T10:30:00+05:00">
    15 Mart 2024, 10:30
  </time>

  <address>
    Muallif: Ali Valiev<br>
    Email: <a href="mailto:ali@mail.com">ali@mail.com</a><br>
    📍 Toshkent, O'zbekiston
  </address>
</article>
```

---

### 🔢 Ro'yxatlar va Jadvallar

```html
<!-- Navigatsiya — ul (tartibsiz) -->
<nav>
  <ul>
    <li><a href="#">Bosh</a></li>
    <li><a href="#">Blog</a></li>
  </ul>
</nav>

<!-- Qadamlar — ol (tartibli) -->
<ol>
  <li>HTML o'rgan</li>
  <li>CSS o'rgan</li>
  <li>JavaScript o'rgan</li>
</ol>

<!-- Lug'at — dl (izolli) -->
<dl>
  <dt>HTML</dt>
  <dd>Sahifa tarkibini yaratish tili</dd>
</dl>

<!-- Jadval — semantik atributlar bilan -->
<table>
  <caption>O'quvchilar reytingi</caption>
  <thead>
    <tr>
      <th scope="col">Ism</th>
      <th scope="col">Ball</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Ali</td>
      <td>95</td>
    </tr>
  </tbody>
</table>
```

---

## 📌 3. Barcha HTML Elementlarni Takrorlash

### Guruhlab takrorlash:

```
📁 HTML elementlar
├── 🏗 Tuzilma (Structural)
│   ├── html, head, body
│   ├── header, nav, main, footer
│   ├── article, section, aside
│   └── div, span (non-semantic)
│
├── 📝 Matn (Text)
│   ├── h1-h6, p, br, hr
│   ├── strong, em, mark, small
│   ├── time, address, cite, abbr
│   ├── blockquote, q
│   ├── del, ins, sup, sub
│   └── code, pre, kbd, var, samp
│
├── 🔗 Havolalar (Links)
│   ├── a (href, target, rel, download)
│   └── base
│
├── 🖼 Media
│   ├── img (src, alt, loading, srcset)
│   ├── video (controls, autoplay, muted)
│   ├── audio (controls, loop)
│   ├── iframe, source
│   └── picture, figure, figcaption
│
├── 📋 Ro'yxatlar (Lists)
│   ├── ul, ol, li
│   └── dl, dt, dd
│
├── 📊 Jadvallar (Tables)
│   ├── table, caption
│   ├── thead, tbody, tfoot
│   ├── tr, th, td
│   └── colspan, rowspan
│
├── 📬 Forma (Forms)
│   ├── form (action, method)
│   ├── input (type, name, id, required...)
│   ├── label, textarea, select, option
│   ├── fieldset, legend
│   ├── button, datalist
│   └── output, meter, progress
│
└── 🔧 Meta/Head
    ├── meta (charset, viewport, description)
    ├── title, link, style, script
    └── noscript
```

---

## 📌 4. Muhim Farqlar (Imtihonga)

### `<div>` vs Semantic teglar

| Holat | Ishlatiladi |
|-------|------------|
| Sahifa sarlavhasi | `<header>` |
| Navigatsiya | `<nav>` |
| Asosiy kontent | `<main>` |
| Mustaqil kontent | `<article>` |
| Mavzu bo'limi | `<section>` |
| Yon panel | `<aside>` |
| Sahifa pastki | `<footer>` |
| **Faqat stil uchun** | `<div>` |

### `<strong>` vs `<b>` | `<em>` vs `<i>`

```html
<!-- strong — semantik (MUHIM degani) -->
<strong>Diqqat!</strong>

<!-- b — vizual (faqat qalin yozuv, ma'no yo'q) -->
<b>Qalin</b>

<!-- em — semantik (ta'kidlash, urg'u) -->
<em>Albatta kelmoqchi edim</em>

<!-- i — vizual (kursiv, ma'no yo'q) -->
<i>Kursiv matn</i>
```

### `<section>` vs `<article>` vs `<div>`

```html
<!-- section — tematik guruh, sarlavhasi bo'lishi kerak -->
<section>
  <h2>Kurslar</h2>
  <!-- ... -->
</section>

<!-- article — o'z-o'zicha ma'noli (maqola, post, blog) -->
<article>
  <h2>SEO nima?</h2>
  <!-- Bu maqolani boshqa saytga ko'chirsa ham ma'nosi bor -->
</article>

<!-- div — hech qanday semantika yo'q, faqat grup/stil -->
<div class="karta-grid">
  <!-- Faqat layout uchun -->
</div>
```

---

## 🎯 Imtihonga Tayyorgarlik + Semantikaga Oid Amaliy Vazifalar

### Vazifa 1-10: Portfolio Blog Sahifasi (To'liq Semantik)

```html
<!DOCTYPE html>
<html lang="uz">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="Ali Valiev — Frontend Developer blog. HTML, CSS, JavaScript bo'yicha maqolalar.">
  <meta property="og:title" content="Ali Dev — Blog">
  <meta property="og:description" content="Frontend development haqida uzbekcha maqolalar">
  <title>Ali Dev | Blog</title>
  <link rel="canonical" href="https://alidev.uz/blog">
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    html { scroll-behavior: smooth; font-size: 16px; }
    body { font-family: "Segoe UI", sans-serif; color: #1a1a2e; background: #fafbff; line-height: 1.7; }

    /* ===================== */
    /* VAZIFA 1: Skip Link    */
    /* ===================== */
    .skip-link {
      position: absolute; top: -100%; left: 8px;
      background: royalblue; color: white;
      padding: 10px 20px; border-radius: 0 0 8px 8px;
      z-index: 9999; text-decoration: none; font-weight: 700;
      transition: top 0.2s;
    }
    .skip-link:focus { top: 0; }
    :focus-visible { outline: 3px solid royalblue; outline-offset: 3px; }

    /* ===================== */
    /* VAZIFA 2: HEADER/NAV  */
    /* ===================== */
    .site-header {
      position: sticky; top: 0; z-index: 100;
      background: rgba(255,255,255,0.95); backdrop-filter: blur(12px);
      border-bottom: 1px solid #f0f0f0;
      padding: 0 clamp(16px, 5vw, 60px);
    }
    .site-header__inner {
      max-width: 1100px; margin: 0 auto;
      display: flex; align-items: center; justify-content: space-between;
      height: 64px;
    }
    .site-logo { font-size: 22px; font-weight: 800; color: #1a1a2e; text-decoration: none; }
    .site-logo span { color: royalblue; }

    .site-nav ul { list-style: none; display: flex; gap: 4px; }
    .site-nav a {
      text-decoration: none; color: #555; padding: 8px 14px;
      border-radius: 8px; font-size: 15px; transition: all 0.2s;
    }
    .site-nav a:hover, .site-nav a[aria-current="page"] {
      background: #f0f4ff; color: royalblue; font-weight: 600;
    }

    /* ===================== */
    /* VAZIFA 3: HERO         */
    /* ===================== */
    .hero {
      background: linear-gradient(135deg, #1a1a2e, #16213e);
      color: white; padding: clamp(60px, 12vw, 120px) clamp(16px, 5vw, 60px);
      text-align: center;
    }
    .hero__tag {
      display: inline-flex; align-items: center; gap: 6px;
      background: rgba(65,105,225,0.2); color: #93c5fd;
      padding: 6px 14px; border-radius: 20px; font-size: 13px;
      margin-bottom: 20px; border: 1px solid rgba(65,105,225,0.3);
    }
    .hero h1 { font-size: clamp(28px, 6vw, 54px); font-weight: 800; margin-bottom: 16px; }
    .hero p { font-size: clamp(15px, 2vw, 18px); opacity: 0.8; max-width: 520px; margin: 0 auto 28px; }
    .hero-actions { display: flex; gap: 12px; justify-content: center; flex-wrap: wrap; }
    .btn { display: inline-flex; align-items: center; gap: 8px;
           padding: 12px 24px; border-radius: 10px; font-weight: 700;
           font-size: 15px; text-decoration: none; transition: all 0.2s; border: none; cursor: pointer; }
    .btn-primary { background: royalblue; color: white; }
    .btn-primary:hover { background: #2c5282; transform: translateY(-2px); }
    .btn-outline { background: rgba(255,255,255,0.1); color: white; border: 1px solid rgba(255,255,255,0.25); }
    .btn-outline:hover { background: rgba(255,255,255,0.15); }

    /* ===================== */
    /* KONTEYNER              */
    /* ===================== */
    .container { max-width: 1100px; margin: 0 auto; padding: 60px clamp(16px, 5vw, 60px); }

    /* ===================== */
    /* VAZIFA 4-5: BLOG GRID */
    /* ===================== */
    .blog-layout { display: grid; grid-template-columns: 1fr 320px; gap: 40px; align-items: start; }
    @media (max-width: 768px) { .blog-layout { grid-template-columns: 1fr; } }

    .blog-grid { display: flex; flex-direction: column; gap: 24px; }

    /* Asosiy Post */
    .article-katta {
      background: white; border-radius: 20px; overflow: hidden;
      box-shadow: 0 4px 24px rgba(0,0,0,0.06); border: 1px solid #f0f0f0;
    }
    .article-katta img { width: 100%; height: 280px; object-fit: cover; display: block; }
    .article-katta__body { padding: 28px; }
    .article-meta { display: flex; align-items: center; gap: 12px; flex-wrap: wrap; margin-bottom: 12px; }
    .kategory-teg { padding: 4px 12px; border-radius: 20px; font-size: 12px; font-weight: 700; }
    .k-html  { background: #fff7ed; color: #c2410c; }
    .k-css   { background: #f0f4ff; color: royalblue; }
    .k-js    { background: #fefce8; color: #854d0e; }
    .k-git   { background: #fdf4ff; color: #7e22ce; }
    .article-time { color: #888; font-size: 13px; }
    .article-katta h2 { font-size: 22px; margin-bottom: 10px; line-height: 1.4; }
    .article-katta p  { color: #555; font-size: 15px; margin-bottom: 20px; }
    .article-oyoq { display: flex; justify-content: space-between; align-items: center; }
    .muallif { display: flex; align-items: center; gap: 10px; font-size: 13px; color: #555; }
    .muallif-avatar { width: 32px; height: 32px; border-radius: 50%; background: royalblue; color: white; display: flex; align-items: center; justify-content: center; font-weight: 700; font-size: 13px; }
    .o'qish-havolasi { color: royalblue; text-decoration: none; font-weight: 700; font-size: 14px; }
    .o'qish-havolasi:hover { text-decoration: underline; }

    /* Kichik postlar grid */
    .mini-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }
    .article-mini {
      background: white; border-radius: 14px; overflow: hidden;
      box-shadow: 0 2px 12px rgba(0,0,0,0.05); border: 1px solid #f0f0f0;
      transition: transform 0.2s, box-shadow 0.2s;
    }
    .article-mini:hover { transform: translateY(-4px); box-shadow: 0 8px 28px rgba(0,0,0,0.1); }
    .article-mini img { width: 100%; height: 140px; object-fit: cover; display: block; }
    .article-mini__body { padding: 14px; }
    .article-mini h3 { font-size: 14px; line-height: 1.4; margin: 6px 0; }
    .article-mini time{ color: #888; font-size: 12px; }

    /* ===================== */
    /* VAZIFA 6: ASIDE        */
    /* ===================== */
    aside.blog-aside { display: flex; flex-direction: column; gap: 20px; position: sticky; top: 80px; }
    .aside-kartа {
      background: white; border-radius: 16px; padding: 20px;
      box-shadow: 0 2px 12px rgba(0,0,0,0.05); border: 1px solid #f0f0f0;
    }
    .aside-kartа h3 { font-size: 15px; font-weight: 700; margin-bottom: 14px; padding-bottom: 10px; border-bottom: 1px solid #f0f0f0; }
    .kategoriya-royh { list-style: none; display: flex; flex-direction: column; gap: 8px; }
    .kategoriya-royh a {
      display: flex; justify-content: space-between; align-items: center;
      text-decoration: none; color: #444; font-size: 14px; padding: 8px 10px;
      border-radius: 8px; transition: all 0.2s;
    }
    .kategoriya-royh a:hover { background: #f0f4ff; color: royalblue; }
    .kategoriya-royh .son { background: #f0f0f0; border-radius: 20px; padding: 2px 8px; font-size: 12px; font-weight: 700; }

    .email-forma { display: flex; flex-direction: column; gap: 10px; }
    .email-forma input { padding: 10px 14px; border: 1px solid #e5e7eb; border-radius: 8px; font-size: 14px; outline: none; }
    .email-forma input:focus { border-color: royalblue; box-shadow: 0 0 0 3px rgba(65,105,225,0.1); }
    .email-forma button { background: royalblue; color: white; border: none; padding: 10px; border-radius: 8px; font-weight: 700; cursor: pointer; }

    /* ===================== */
    /* VAZIFA 7: MAQOLA      */
    /* ===================== */
    .maqola-tana { max-width: 720px; margin: 0 auto; padding: 60px 24px; }
    .maqola-tana h2 { font-size: 26px; margin: 28px 0 14px; }
    .maqola-tana h3 { font-size: 20px; margin: 22px 0 10px; color: royalblue; }
    .maqola-tana p  { color: #444; margin-bottom: 16px; }
    .maqola-tana ul, .maqola-tana ol { padding-left: 24px; margin-bottom: 16px; color: #444; }
    .maqola-tana li { margin-bottom: 6px; }
    .kod-blok { background: #16213e; color: #a8dadc; padding: 20px 24px; border-radius: 12px; margin: 20px 0; overflow-x: auto; }
    .kod-blok code { font-family: "Cascadia Code", "Courier New", monospace; font-size: 14px; }
    blockquote.iqtibos {
      border-left: 4px solid royalblue; background: #f0f4ff;
      padding: 16px 20px; border-radius: 0 12px 12px 0; margin: 20px 0;
      font-style: italic; color: #2c5282;
    }
    .belgilangan { background: #fef9c3; padding: 2px 4px; border-radius: 3px; }

    /* ===================== */
    /* VAZIFA 8: FAQ (details)*/
    /* ===================== */
    .faq-royhat { list-style: none; display: flex; flex-direction: column; gap: 8px; }
    .faq-royhat details {
      background: white; border: 1px solid #e5e7eb; border-radius: 12px; overflow: hidden;
    }
    .faq-royhat summary {
      padding: 16px 20px; cursor: pointer; font-weight: 600; font-size: 15px;
      display: flex; justify-content: space-between; align-items: center;
      user-select: none;
    }
    .faq-royhat summary::after { content: "+"; font-size: 22px; color: royalblue; line-height: 1; }
    .faq-royhat details[open] { border-color: royalblue; }
    .faq-royhat details[open] summary { color: royalblue; }
    .faq-royhat details[open] summary::after { content: "−"; }
    .faq-royhat details p { padding: 0 20px 18px; color: #555; line-height: 1.8; }

    /* ===================== */
    /* VAZIFA 9: FOOTER       */
    /* ===================== */
    .site-footer { background: #1a1a2e; color: rgba(255,255,255,0.7); padding: 60px clamp(16px, 5vw, 60px) 0; }
    .footer-grid { max-width: 1100px; margin: 0 auto; display: grid; grid-template-columns: 2fr 1fr 1fr 1fr; gap: 40px; padding-bottom: 48px; }
    @media (max-width: 640px) { .footer-grid { grid-template-columns: 1fr 1fr; } }
    .footer-brand .logo { font-size: 22px; font-weight: 800; color: white; text-decoration: none; }
    .footer-brand .logo span { color: royalblue; }
    .footer-brand p { margin: 12px 0 16px; font-size: 14px; max-width: 240px; line-height: 1.7; }
    .social-links { display: flex; gap: 10px; }
    .social-links a { width: 36px; height: 36px; border-radius: 8px; background: rgba(255,255,255,0.07); display: flex; align-items: center; justify-content: center; text-decoration: none; font-size: 16px; transition: background 0.2s; }
    .social-links a:hover { background: royalblue; }
    .footer-col h4 { color: white; font-size: 14px; margin-bottom: 14px; }
    .footer-col ul { list-style: none; display: flex; flex-direction: column; gap: 8px; }
    .footer-col a { color: rgba(255,255,255,0.6); text-decoration: none; font-size: 14px; transition: color 0.2s; }
    .footer-col a:hover { color: white; }
    .footer-bottom { max-width: 1100px; margin: 0 auto; padding: 20px 0; border-top: 1px solid rgba(255,255,255,0.08); display: flex; justify-content: space-between; align-items: center; font-size: 13px; flex-wrap: wrap; gap: 12px; }
    .footer-bottom a { color: rgba(255,255,255,0.5); text-decoration: none; }

    /* Breadcrumb */
    .breadcrumb { display: flex; gap: 8px; align-items: center; font-size: 13px; color: #888; margin-bottom: 32px; }
    .breadcrumb a { color: royalblue; text-decoration: none; }
    .breadcrumb a:hover { text-decoration: underline; }
  </style>
</head>
<body>

  <!-- Vazifa 1: Skip Link (Accessibility) -->
  <a href="#asosiy" class="skip-link">Asosiy kontentga o'tish</a>

  <!-- Vazifa 2: Semantic Header + Nav -->
  <header class="site-header" role="banner">
    <div class="site-header__inner">
      <a href="/" class="site-logo">Ali <span>Dev</span></a>
      <nav class="site-nav" aria-label="Asosiy navigatsiya">
        <ul>
          <li><a href="/">Bosh</a></li>
          <li><a href="/blog" aria-current="page">Blog</a></li>
          <li><a href="/loyihalar">Loyihalar</a></li>
          <li><a href="/haqida">Haqimda</a></li>
          <li><a href="/aloqa" class="btn btn-primary" style="padding:8px 16px;font-size:14px">Aloqa</a></li>
        </ul>
      </nav>
    </div>
  </header>

  <!-- Vazifa 3: Semantic Hero (BITTA h1!) -->
  <section class="hero" aria-labelledby="hero-sarlavha">
    <div class="hero__tag">📝 135+ ta maqola</div>
    <h1 id="hero-sarlavha">Frontend Blog</h1>
    <p>HTML, CSS va JavaScript bo'yicha amaliy maqolalar. Har hafta yangi kontent!</p>
    <div class="hero-actions">
      <a href="#maqolalar" class="btn btn-primary">Maqolalarni ko'rish ↓</a>
      <a href="/email" class="btn btn-outline">Obuna bo'lish 📧</a>
    </div>
  </section>

  <!-- Asosiy Kontent -->
  <main id="asosiy" role="main">
    <div class="container">

      <!-- Vazifa 7: Breadcrumb navigatsiya -->
      <nav class="breadcrumb" aria-label="Sahifa yo'li">
        <a href="/">🏠 Bosh</a>
        <span aria-hidden="true">›</span>
        <span aria-current="page">Blog</span>
      </nav>

      <!-- Vazifa 4-5: Article + Aside layout -->
      <div class="blog-layout" id="maqolalar">

        <!-- Asosiy blog maqolalari -->
        <section aria-labelledby="maqolalar-sarlavha">
          <h2 id="maqolalar-sarlavha" style="font-size:22px;margin-bottom:20px">
            So'nggi Maqolalar
          </h2>

          <div class="blog-grid">

            <!-- Asosiy katta maqola (article — mustaqil kontent) -->
            <article class="article-katta">
              <img src="https://picsum.photos/800/400?random=10"
                   alt="HTML Semantics tushuntirilagan amaliy misol"
                   loading="eager" width="800" height="280">
              <div class="article-katta__body">
                <div class="article-meta">
                  <span class="kategory-teg k-html">HTML</span>
                  <time datetime="2024-03-15" class="article-time">15 Mart, 2024</time>
                </div>
                <h2>Semantik HTML — Nimaga Kerak va Qanday Ishlatiladi?</h2>
                <p>
                  Ko'pchilik dasturchilar hamma narsa uchun
                  <code>&lt;div&gt;</code> ishlatadi. Lekin semantik HTML teglar
                  <mark>SEO, Accessibility va kodni o'qish</mark> uchun juda muhim...
                </p>
                <div class="article-oyoq">
                  <div class="muallif">
                    <div class="muallif-avatar" aria-hidden="true">A</div>
                    <span>Ali Valiev</span>
                  </div>
                  <a href="/blog/semantik-html" class="o'qish-havolasi" aria-label="Semantik HTML maqolasini o'qish">
                    Batafsil o'qish →
                  </a>
                </div>
              </div>
            </article>

            <!-- Kichik maqolalar grid -->
            <div class="mini-grid">
              <article class="article-mini">
                <img src="https://picsum.photos/400/240?random=11" alt="CSS Flexbox vizual tushuntirish" loading="lazy" width="400" height="140">
                <div class="article-mini__body">
                  <span class="kategory-teg k-css" style="font-size:11px">CSS</span>
                  <h3>Flexbox — 2024 da To'liq Qo'llanma</h3>
                  <time datetime="2024-03-12">12 Mart 2024</time>
                </div>
              </article>

              <article class="article-mini">
                <img src="https://picsum.photos/400/240?random=12" alt="JavaScript async await misollar" loading="lazy" width="400" height="140">
                <div class="article-mini__body">
                  <span class="kategory-teg k-js" style="font-size:11px">JS</span>
                  <h3>Async/Await — Real Loyihada Ishlatish</h3>
                  <time datetime="2024-03-08">8 Mart 2024</time>
                </div>
              </article>

              <article class="article-mini">
                <img src="https://picsum.photos/400/240?random=13" alt="Git komandalar" loading="lazy" width="400" height="140">
                <div class="article-mini__body">
                  <span class="kategory-teg k-git" style="font-size:11px">Git</span>
                  <h3>Git Komandalar — Har Kuni Ishlatiladiganlar</h3>
                  <time datetime="2024-03-05">5 Mart 2024</time>
                </div>
              </article>

              <article class="article-mini">
                <img src="https://picsum.photos/400/240?random=14" alt="CSS Grid layout" loading="lazy" width="400" height="140">
                <div class="article-mini__body">
                  <span class="kategory-teg k-css" style="font-size:11px">CSS</span>
                  <h3>CSS Grid vs Flexbox — Qachon Nima Ishlatish</h3>
                  <time datetime="2024-03-01">1 Mart 2024</time>
                </div>
              </article>
            </div>

          </div><!-- /blog-grid -->
        </section>

        <!-- Vazifa 6: Semantic Aside -->
        <aside class="blog-aside" aria-label="Qo'shimcha kontent">

          <!-- Kategoriyalar -->
          <div class="aside-kartа">
            <h3>📁 Kategoriyalar</h3>
            <ul class="kategoriya-royh" role="list">
              <li><a href="/blog?cat=html">🌐 HTML <span class="son">18</span></a></li>
              <li><a href="/blog?cat=css">🎨 CSS <span class="son">24</span></a></li>
              <li><a href="/blog?cat=js"><span>⚡</span> JavaScript <span class="son">41</span></a></li>
              <li><a href="/blog?cat=react">⚛️ React <span class="son">29</span></a></li>
              <li><a href="/blog?cat=git">🐙 Git <span class="son">12</span></a></li>
            </ul>
          </div>

          <!-- Email obuna -->
          <div class="aside-kartа">
            <h3>📧 Yangilandi xabarlari</h3>
            <p style="font-size:13px;color:#666;margin-bottom:12px">
              Har hafta yangi maqolalar emailingizga!
            </p>
            <form class="email-forma" aria-label="Email obuna formasi">
              <label for="obuna-email" class="sr-only">Email manzilingiz</label>
              <input type="email" id="obuna-email" placeholder="email@mail.com" required autocomplete="email">
              <button type="submit">Obuna bo'lish ✉️</button>
            </form>
          </div>

        </aside>
      </div><!-- /blog-layout -->

      <!-- Vazifa 8: FAQ — details/summary (semantik!) -->
      <section style="margin-top: 60px" aria-labelledby="faq-sarlavha">
        <h2 id="faq-sarlavha" style="font-size:26px;margin-bottom:24px">❓ Ko'p Beriladigan Savollar</h2>
        <ul class="faq-royhat" role="list">
          <li>
            <details>
              <summary>Semantik HTML nima uchun muhim?</summary>
              <p>
                Semantik HTML <strong>qidiruv tizimlari</strong> (Google),
                <strong>ekran o'quvchi</strong> qurilmalar va
                <strong>boshqa dasturchilar</strong> uchun kodni tushunishni osonlashtiradi.
                Bu <em>SEO</em>, <em>Accessibility</em> va kodni saqlash samaradorligini oshiradi.
              </p>
            </details>
          </li>
          <li>
            <details>
              <summary>div va section qanday farq qiladi?</summary>
              <p>
                <code>&lt;section&gt;</code> — tematik guruh, sarlavhasi bo'lishi kerak. Semantik ma'nosi bor.<br>
                <code>&lt;div&gt;</code> — faqat vizual guruh, hech qanday ma'nosi yo'q.
                Faqat CSS layout uchun ishlatiladi.
              </p>
            </details>
          </li>
          <li>
            <details>
              <summary>article va section — farqi nima?</summary>
              <p>
                <code>&lt;article&gt;</code> — o'z-o'zicha ma'noli. Masalan, blog maqolasini
                boshqa saytga ko'chirsangiz ham ma'nosi saqlanadi.<br>
                <code>&lt;section&gt;</code> — kontekstga bog'liq. Faqat o'sha sahifada ma'nosi bor.
              </p>
            </details>
          </li>
          <li>
            <details>
              <summary>strong va b ning farqi nima?</summary>
              <p>
                <code>&lt;strong&gt;</code> — semantik, "bu matn muhim" degan ma'noni bildiradi.
                Screen reader ovozini balandlashtiradi.<br>
                <code>&lt;b&gt;</code> — faqat vizual, qalin yozuv. Hech qanday semantik ma'nosi yo'q.
              </p>
            </details>
          </li>
          <li>
            <details>
              <summary>Sahifada nechta h1 bo'lishi mumkin?</summary>
              <p>
                Faqat <strong>bitta</strong> <code>&lt;h1&gt;</code>! U sahifaning asosiy mavzusini bildiradi.
                Google ham birinchi navbatda h1 ga qaraydi. h2–h6 esa ierarxik tarzda ishlatiladi.
              </p>
            </details>
          </li>
        </ul>
      </section>

    </div><!-- /container -->
  </main>

  <!-- Vazifa 9-10: Semantic Footer + address -->
  <footer class="site-footer" role="contentinfo">
    <div class="footer-grid">
      <div class="footer-brand">
        <a href="/" class="logo">Ali <span>Dev</span></a>
        <p>Frontend dasturlash bo'yicha uzbekcha qo'llanmalar. HTML, CSS, JS va React.</p>
        <nav aria-label="Ijtimoiy tarmoqlar">
          <div class="social-links">
            <a href="https://t.me/alidev" target="_blank" rel="noopener noreferrer" aria-label="Telegram">💬</a>
            <a href="https://github.com/alidev" target="_blank" rel="noopener noreferrer" aria-label="GitHub">🐙</a>
            <a href="https://youtube.com/@alidev" target="_blank" rel="noopener noreferrer" aria-label="YouTube">▶</a>
            <a href="https://linkedin.com/in/alidev" target="_blank" rel="noopener noreferrer" aria-label="LinkedIn">💼</a>
          </div>
        </nav>
      </div>

      <nav class="footer-col" aria-label="Kurslar">
        <h4>Kurslar</h4>
        <ul>
          <li><a href="/kurs/html">HTML va CSS</a></li>
          <li><a href="/kurs/js">JavaScript</a></li>
          <li><a href="/kurs/react">React.js</a></li>
          <li><a href="/kurs/git">Git</a></li>
        </ul>
      </nav>

      <nav class="footer-col" aria-label="Sayt bo'limlari">
        <h4>Sayt</h4>
        <ul>
          <li><a href="/haqida">Haqimda</a></li>
          <li><a href="/blog">Blog</a></li>
          <li><a href="/loyihalar">Loyihalar</a></li>
          <li><a href="/aloqa">Aloqa</a></li>
        </ul>
      </nav>

      <div class="footer-col">
        <h4>Aloqa</h4>
        <!-- address — semantik kontakt ma'lumotlari -->
        <address>
          <ul style="list-style:none">
            <li><a href="mailto:ali@alidev.uz">📧 ali@alidev.uz</a></li>
            <li><a href="tel:+998901234567">📞 +998 90 123 45 67</a></li>
            <li><a href="https://t.me/alidev">💬 @alidev</a></li>
          </ul>
        </address>
      </div>
    </div>

    <!-- Vazifa 10: Copyright bilan footer pastki -->
    <div class="footer-bottom">
      <p>© <time datetime="2024">2024</time> Ali Dev. Barcha huquqlar himoyalangan.</p>
      <nav aria-label="Huquqiy havolalar">
        <a href="/maxfiylik">Maxfiylik</a> ·
        <a href="/shartlar">Foydalanish shartlari</a> ·
        <a href="#bosh" aria-label="Sahifa tepasiga qaytish">Tepaga ↑</a>
      </nav>
    </div>
  </footer>

</body>
</html>
```

---

## 📝 Imtihon Savollari — O'z-O'zini Tekshirish

1. `<article>` va `<section>` orasidagi farq nima?
2. Sahifada nechta `<h1>` bo'lishi kerak?
3. `<strong>` va `<b>` — qaysi biri semantik?
4. `<time datetime="2024-03-15">` — datetime nima uchun kerak?
5. `<address>` tegi nima uchun ishlatiladi?
6. `loading="lazy"` — rasmda nima vazifani bajaradi?
7. `rel="noopener noreferrer"` — nima uchun kerak?
8. `aria-label` atributi qaysi holatlarda ishlatiladi?
9. `<main>` tegi sahifada necha marta ishlatilishi mumkin?
10. `<nav>` ichida `<ul>` ishlatish majburiymi?
