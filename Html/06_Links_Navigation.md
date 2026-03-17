# 06-Dars: Link lar va Navigation

## 📌 `<a>` — Havola Tegi

```html
<!-- Asosiy sintaksis -->
<a href="URL">Ko'rinadigan matn</a>

<!-- 1. Tashqi havola -->
<a href="https://google.com">Google</a>
<a href="https://developer.mozilla.org">MDN Docs</a>

<!-- 2. Ichki sahifalar -->
<a href="index.html">Bosh sahifa</a>
<a href="haqida.html">Haqimda</a>
<a href="css/style.css">CSS fayl</a>    <!-- Bu CSS faylni ochadi -->
<a href="../index.html">Yuqoriga</a>   <!-- Yuqori papkaga -->

<!-- 3. Anchor links (sahifa ichida) -->
<a href="#kirish">Kirish bo'limiga</a>
<a href="#aloqa">Aloqa</a>
<a href="#">Tepaga</a>               <!-- # = sahifa tepasiga -->

<!-- 4. Email -->
<a href="mailto:ali@mail.com">Email yuborish</a>
<a href="mailto:ali@mail.com?subject=Salom&body=Qanday halsiz?">
  Email (mavzu bilan)
</a>

<!-- 5. Telefon -->
<a href="tel:+998901234567">+998 90 123 45 67</a>

<!-- 6. Fayl yuklab olish -->
<a href="hujjat.pdf" download>PDF yuklab olish</a>
<a href="rasm.jpg" download="mening-rasmim.jpg">Rasm yuklab olish</a>
```

---

## 📌 target Atributi

```html
<!-- target — havola qayerda ochilsin -->
<a href="https://google.com" target="_blank">  <!-- Yangi tabda -->
  Google (yangi tabda)
</a>

<a href="sahifa.html" target="_self">          <!-- Hozirgi tabda (default) -->
  Hozirgi tabda
</a>

<a href="sahifa.html" target="_parent">        <!-- Ota freymda -->
  Ota freymda
</a>

<a href="sahifa.html" target="_top">           <!-- Asosiy oynada -->
  Asosiy oynada
</a>

<!-- ⚠️ _blank bilan rel="noopener noreferrer" qo'shing (xavfsizlik) -->
<a href="https://google.com" target="_blank" rel="noopener noreferrer">
  Xavfsiz tashqi havola
</a>
```

---

## 📌 rel Atributi

```html
<!-- rel — havola va maqsadli sahifa munosabati -->
<a href="https://google.com" rel="noopener noreferrer">Tashqi</a>
<a href="https://example.com" rel="nofollow">SEO ga ta'sir qilmasin</a>
<a href="haqida.html" rel="author">Muallif</a>
<a href="litsenziya.html" rel="license">Litsenziya</a>
<a href="keyingi.html" rel="next">Keyingi</a>
<a href="oldingi.html" rel="prev">Oldingi</a>
```

---

## 📌 Anchor Links — Sahifa ichida Navigatsiya

```html
<!-- Maqsadli joy (id bilan belgilanadi) -->
<section id="kirish">
  <h2>Kirish</h2>
  <p>...</p>
</section>

<section id="xizmatlar">
  <h2>Xizmatlar</h2>
  <p>...</p>
</section>

<section id="aloqa">
  <h2>Aloqa</h2>
  <p>...</p>
</section>

<!-- Anchor havolalar -->
<nav>
  <a href="#kirish">Kirish</a>
  <a href="#xizmatlar">Xizmatlar</a>
  <a href="#aloqa">Aloqa</a>
</nav>

<!-- Boshqa sahifadan anchor -->
<a href="index.html#xizmatlar">Xizmatlar (bosh sahifada)</a>
```

---

## 📌 Navigatsiya `<nav>` Bilan

```html
<!-- Navbar (gorizontal) -->
<header>
  <nav aria-label="Asosiy navigatsiya">
    <div class="nav-logo">
      <a href="index.html">🎨 MyBrand</a>
    </div>
    <ul class="nav-royhati">
      <li><a href="index.html" class="faol">Bosh sahifa</a></li>
      <li><a href="haqida.html">Haqimda</a></li>
      <li>
        <a href="xizmatlar.html">Xizmatlar ▾</a>
        <!-- Dropdown -->
        <ul class="dropdown">
          <li><a href="web.html">Web dizayn</a></li>
          <li><a href="mobil.html">Mobil</a></li>
        </ul>
      </li>
      <li><a href="aloqa.html">Aloqa</a></li>
    </ul>
    <button class="hamburger">☰</button>
  </nav>
</header>

<!-- Breadcrumb (Yo'l ko'rsatgich) -->
<nav aria-label="Breadcrumb">
  <ol class="breadcrumb">
    <li><a href="/">Bosh</a></li>
    <li><a href="/maqolalar">Maqolalar</a></li>
    <li aria-current="page">HTML Havolalar</li>
  </ol>
</nav>

<!-- Pagination (Sahifalash) -->
<nav aria-label="Sahifalash">
  <a href="?page=1" aria-label="Birinchi sahifa">«</a>
  <a href="?page=3" aria-label="Oldingi sahifa">‹</a>
  <a href="?page=4">4</a>
  <a href="?page=5" aria-current="page">5</a>
  <a href="?page=6">6</a>
  <a href="?page=7" aria-label="Keyingi sahifa">›</a>
  <a href="?page=20" aria-label="Oxirgi sahifa">»</a>
</nav>
```

---

## 🎯 10 ta Amaliy Vazifa — Contact Page

```html
<!DOCTYPE html>
<html lang="uz">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Aloqa | MyPortfolio</title>
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    html { scroll-behavior: smooth; }
    body { font-family: "Segoe UI", sans-serif; color: #1a1a2e; }

    /* === NAVBAR === */
    /* Vazifa 1: Sticky Navbar */
    .navbar {
      position: sticky; top: 0; z-index: 100;
      background: white; padding: 0 40px;
      display: flex; align-items: center; justify-content: space-between;
      height: 64px; box-shadow: 0 2px 12px rgba(0,0,0,0.06);
    }
    .navbar__logo { font-size: 22px; font-weight: 700; color: #1a1a2e; text-decoration: none; }
    .navbar__nav { display: flex; gap: 8px; list-style: none; }
    .navbar__nav a {
      text-decoration: none; color: #555; padding: 8px 14px;
      border-radius: 8px; transition: all 0.2s;
    }
    .navbar__nav a:hover, .navbar__nav a.faol { background: #f0f4ff; color: royalblue; }

    /* === HERO === */
    /* Vazifa 2: Anchor navigatsiya */
    .hero {
      min-height: 90vh; display: flex; align-items: center; justify-content: center;
      text-align: center; background: linear-gradient(135deg, #16213e, #0f3460);
      color: white; flex-direction: column; gap: 24px;
    }
    .hero h1 { font-size: clamp(32px, 6vw, 64px); }
    .hero p { font-size: 18px; opacity: 0.8; max-width: 500px; }
    .hero-havolalar { display: flex; gap: 12px; flex-wrap: wrap; justify-content: center; }
    .btn { padding: 12px 28px; border-radius: 8px; font-weight: 600; text-decoration: none; transition: all 0.2s; }
    .btn-asosiy { background: royalblue; color: white; }
    .btn-asosiy:hover { background: #2c5282; transform: translateY(-2px); }
    .btn-ikkilamchi { border: 2px solid rgba(255,255,255,0.4); color: white; }
    .btn-ikkilamchi:hover { background: rgba(255,255,255,0.1); }

    /* Vazifa 3: To'r havolalar */
    .social-tasma {
      display: flex; justify-content: center; gap: 16px;
      padding: 24px; background: #f8f9fa;
    }
    .social-havola {
      display: flex; align-items: center; gap: 8px;
      padding: 10px 20px; text-decoration: none; color: white;
      border-radius: 8px; font-weight: 600; transition: opacity 0.2s;
    }
    .social-havola:hover { opacity: 0.85; }
    .s-github   { background: #333; }
    .s-linkedin { background: #0a66c2; }
    .s-telegram { background: #2ca5e0; }
    .s-youtube  { background: #ff0000; }

    /* Konteneyner */
    .konteyner { max-width: 900px; margin: 0 auto; padding: 80px 24px; }

    /* Vazifa 4-6: Aloqa Bo'limi */
    .aloqa-grid {
      display: grid; grid-template-columns: 1fr 1fr; gap: 40px;
    }
    @media (max-width: 600px) { .aloqa-grid { grid-template-columns: 1fr; } }

    .aloqa-info h2 { font-size: 28px; margin-bottom: 16px; }
    .aloqa-info p  { color: #666; line-height: 1.7; margin-bottom: 24px; }

    .aloqa-havola-royhati { list-style: none; display: flex; flex-direction: column; gap: 12px; }
    .aloqa-havola-royhati li a {
      display: flex; align-items: center; gap: 12px;
      text-decoration: none; color: #1a1a2e; padding: 14px;
      background: #f8f9fa; border-radius: 10px; transition: all 0.2s;
    }
    .aloqa-havola-royhati li a:hover { background: #f0f4ff; color: royalblue; transform: translateX(4px); }
    .aloqa-icon { width: 36px; height: 36px; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 18px; }

    /* Vazifa 7: Download CV */
    .cv-quti {
      background: linear-gradient(135deg, royalblue, #764ba2); color: white;
      padding: 32px; border-radius: 16px; text-align: center; margin-top: 32px;
    }
    .cv-quti h3 { margin-bottom: 8px; }
    .cv-quti p  { opacity: 0.85; margin-bottom: 20px; font-size: 14px; }
    .cv-btn {
      display: inline-flex; align-items: center; gap: 8px;
      background: white; color: royalblue; padding: 12px 24px;
      border-radius: 8px; text-decoration: none; font-weight: 700;
      transition: transform 0.2s;
    }
    .cv-btn:hover { transform: scale(1.05); }

    /* Vazifa 8: Breadcrumb */
    .breadcrumb { display: flex; gap: 8px; align-items: center; font-size: 13px; color: #888; margin-bottom: 40px; }
    .breadcrumb a { color: royalblue; text-decoration: none; }
    .breadcrumb a:hover { text-decoration: underline; }

    /* Vazifa 9-10: Sahifa pastki qismi */
    footer { background: #16213e; color: rgba(255,255,255,0.7); padding: 40px; }
    .footer-grid { max-width: 900px; margin: 0 auto; display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; gap: 20px; }
    .footer-nav { display: flex; gap: 20px; }
    .footer-nav a { color: rgba(255,255,255,0.7); text-decoration: none; font-size: 14px; }
    .footer-nav a:hover { color: white; }
  </style>
</head>
<body>

  <!-- Vazifa 1: Sticky Navbar -->
  <header>
    <nav class="navbar" aria-label="Asosiy navigatsiya">
      <a href="index.html" class="navbar__logo">👨‍💻 Ali.dev</a>
      <ul class="navbar__nav">
        <li><a href="#bosh">Bosh</a></li>
        <li><a href="#haqida">Haqimda</a></li>
        <li><a href="#aloqa" class="faol">Aloqa</a></li>
      </ul>
    </nav>
  </header>

  <!-- Vazifa 2: Anchor havolalar -->
  <section class="hero" id="bosh">
    <h1>Bog'lanish 📬</h1>
    <p>Hamkorlik, loyiha yoki shunchaki salomlashish uchun yozing!</p>
    <div class="hero-havolalar">
      <a href="#aloqa" class="btn btn-asosiy">Xabar Yuborish →</a>
      <a href="#aloqa-info" class="btn btn-ikkilamchi">Aloqa Ma'lumotlari</a>
    </div>
  </section>

  <!-- Vazifa 3: Social havolalar -->
  <div class="social-tasma">
    <a href="https://github.com" target="_blank" rel="noopener noreferrer" class="social-havola s-github">
      GitHub
    </a>
    <a href="https://linkedin.com" target="_blank" rel="noopener noreferrer" class="social-havola s-linkedin">
      LinkedIn
    </a>
    <a href="https://t.me/username" target="_blank" rel="noopener noreferrer" class="social-havola s-telegram">
      Telegram
    </a>
    <a href="https://youtube.com" target="_blank" rel="noopener noreferrer" class="social-havola s-youtube">
      YouTube
    </a>
  </div>

  <!-- Vazifa 4-7: Asosiy aloqa qismi -->
  <section id="aloqa" class="konteyner">
    <!-- Vazifa 8: Breadcrumb -->
    <nav class="breadcrumb" aria-label="Breadcrumb">
      <a href="index.html">🏠 Bosh</a>
      <span>›</span>
      <span aria-current="page">Aloqa</span>
    </nav>

    <div class="aloqa-grid">
      <div class="aloqa-info" id="aloqa-info">
        <h2>Muloqotga tayyor!</h2>
        <p>Yangi loyiha, hamkorlik yoki shunchaki salomlashish uchun murojaat qiling.</p>

        <!-- Vazifa 5: Mailto havola -->
        <ul class="aloqa-havola-royhati">
          <li>
            <a href="mailto:ali@mail.com?subject=Loyiha haqida">
              <span class="aloqa-icon" style="background: #fee2e2;">📧</span>
              <div><strong>Email</strong><br><small>ali@mail.com</small></div>
            </a>
          </li>
          <!-- Vazifa 6: Tel havola -->
          <li>
            <a href="tel:+998901234567">
              <span class="aloqa-icon" style="background: #d1fae5;">📞</span>
              <div><strong>Telefon</strong><br><small>+998 90 123 45 67</small></div>
            </a>
          </li>
          <li>
            <a href="https://t.me/username" target="_blank" rel="noopener noreferrer">
              <span class="aloqa-icon" style="background: #dbeafe;">💬</span>
              <div><strong>Telegram</strong><br><small>@username</small></div>
            </a>
          </li>
          <li>
            <a href="https://github.com/username" target="_blank" rel="noopener noreferrer">
              <span class="aloqa-icon" style="background: #e5e7eb;">🐱</span>
              <div><strong>GitHub</strong><br><small>github.com/username</small></div>
            </a>
          </li>
        </ul>

        <!-- Vazifa 7: Download -->
        <div class="cv-quti">
          <h3>📄 CV Yuklab Olish</h3>
          <p>Frontend Developer sifatidagi tajribam haqida</p>
          <a href="cv.pdf" download="Ali_Valiev_CV.pdf" class="cv-btn">
            ⬇️ CV.pdf yuklab olish
          </a>
        </div>
      </div>

      <!-- Forma qismi -->
      <div>
        <h2>Xabar Yozing</h2>
        <br>
        <form style="display: flex; flex-direction: column; gap: 16px;">
          <input type="text" placeholder="Ismingiz" style="padding: 12px 16px; border: 1px solid #ddd; border-radius: 8px; font-size: 15px;">
          <input type="email" placeholder="Email" style="padding: 12px 16px; border: 1px solid #ddd; border-radius: 8px; font-size: 15px;">
          <textarea rows="5" placeholder="Xabaringiz..." style="padding: 12px 16px; border: 1px solid #ddd; border-radius: 8px; font-size: 15px; resize: vertical;"></textarea>
          <button type="submit" class="btn btn-asosiy" style="cursor: pointer; border: none;">Yuborish 🚀</button>
        </form>
      </div>
    </div>
  </section>

  <!-- Vazifa 9-10: Footer navigatsiya -->
  <footer>
    <div class="footer-grid">
      <p>© 2024 Ali.dev — Barcha huquqlar himoyalangan</p>
      <nav class="footer-nav" aria-label="Footer navigatsiya">
        <a href="index.html">Bosh</a>
        <a href="haqida.html">Haqimda</a>
        <a href="loyihalar.html">Loyihalar</a>
        <a href="#bosh">Tepaga ↑</a>
      </nav>
    </div>
  </footer>

</body>
</html>
```
