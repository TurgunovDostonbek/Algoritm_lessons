# 17-Dars: Responsive Web Design va Media Queries

## 📌 Responsive Web Design (RWD) nima?

**RWD** — sayt barcha qurilmalarda (telefon, planshet, noutbuk, katta monitor) to'g'ri ko'rinishi.

```
Qurilmalar:
├── Mobile phone  → < 576px
├── Tablet        → 576px – 992px
├── Laptop        → 992px – 1200px
└── Desktop       → > 1200px
```

---

## 📌 Viewport Meta Tegi

```html
<!-- Bu MAJBURIY! Responsivlik ishlashi uchun -->
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

---

## 📌 Media Queries Sintaksisi

```css
/* @media qoidasi */
@media (shartlar) {
  /* Bu yergi stilllar faqat shart bajarilganda qo'llanadi */
}

/* Breakpointlar (Bootstrap standartlari) */
/* Default (Mobile First) — hamma uchun */
.el { font-size: 14px; }

/* Tablet va undan katta */
@media (min-width: 576px) { .el { font-size: 15px; } }

/* Kichik noutbuk */
@media (min-width: 768px) { .el { font-size: 16px; } }

/* Katta noutbuk */
@media (min-width: 992px) { .el { font-size: 17px; } }

/* Desktop */
@media (min-width: 1200px) { .el { font-size: 18px; } }

/* XL Desktop */
@media (min-width: 1400px) { .el { font-size: 20px; } }
```

---

## 📌 min-width va max-width

```css
/* Mobile First (tavsiya!) — kichikdan kattaga */
.el { display: block; }  /* Default: mobil */
@media (min-width: 768px) { .el { display: flex; } }  /* Tabletdan katta */

/* Desktop First (eskirgan) — kattadan kichikka */
.el { display: flex; }  /* Default: katta */
@media (max-width: 767px) { .el { display: block; } }  /* Mobilgacha */

/* Aniq oraliq */
@media (min-width: 576px) and (max-width: 991px) {
  /* Faqat tablet */
}
```

---

## 📌 Media Query Turlari

```css
/* screen — ekran */
@media screen and (min-width: 768px) { }  

/* print — chop etish */
@media print {
  .navbar, .footer, .reklama { display: none; }
  body { font-size: 12pt; }
}

/* Orientatsiya */
@media (orientation: portrait)  { /* Vertikal (telefon) */ }
@media (orientation: landscape) { /* Gorizontal */ }

/* Dark mode */
@media (prefers-color-scheme: dark) {
  body { background: #1a1a2e; color: white; }
}

/* Reduced motion — animatsiyalarga sezgir foydalanuvchilar */
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after { animation-duration: 0.01ms !important; }
}

/* Hover imkoniyati bor qurilmalar (mouse) */
@media (hover: hover) {
  .btn:hover { background: darkblue; }
}
```

---

## 📌 Responsive Patterns

```css
/* 1. Responsive navbar — hamburger */
.nav-menu { display: none; } /* Mobilda yashirilgan */
.hamburger { display: block; }

@media (min-width: 768px) {
  .nav-menu { display: flex; }
  .hamburger { display: none; }
}

/* 2. Responsive grid */
.grid {
  display: grid;
  grid-template-columns: 1fr; /* Mobilda 1 ustun */
  gap: 16px;
}
@media (min-width: 576px) {
  .grid { grid-template-columns: repeat(2, 1fr); }
}
@media (min-width: 992px) {
  .grid { grid-template-columns: repeat(4, 1fr); }
}

/* 3. Responsive typography (zamonaviy — clamp) */
h1 { font-size: clamp(1.5rem, 5vw, 3rem); } /* Media query kerak emas! */
p  { font-size: clamp(0.875rem, 2vw, 1.125rem); }

/* 4. Responsive rasm */
img { width: 100%; height: auto; max-width: 100%; }

/* 5. Container query (yangi CSS) */
@container (min-width: 600px) {
  .karta { display: flex; }
}
```

---

## 🎯 10 ta Amaliy Vazifa — Portfolio Website (Responsive)

```html
<!DOCTYPE html>
<html lang="uz">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Portfolio — Responsive</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
  <link rel="stylesheet" href="responsive.css">
</head>
<body>

  <!-- Vazifa 1: Responsive Navbar -->
  <header class="navbar">
    <div class="navbar__logo">👨‍💻 Ali.dev</div>
    <button class="hamburger" id="hamburger-btn" aria-label="Menu">
      <i class="fa-solid fa-bars"></i>
    </button>
    <nav class="nav-menu" id="nav-menu">
      <a href="#bosh">Bosh</a>
      <a href="#haqida">Haqida</a>
      <a href="#loyihalar">Loyihalar</a>
      <a href="#aloqa">Aloqa</a>
    </nav>
  </header>

  <!-- Vazifa 2: Hero -->
  <section class="hero" id="bosh">
    <div class="hero__kontent">
      <p class="hero__salomlash">Assalomu Alaykum! 👋</p>
      <h1 class="hero__sarlavha">Men Ali Valiev</h1>
      <p class="hero__mansab">Frontend Developer & UI Designer</p>
      <div class="hero__tugmalar">
        <a href="#loyihalar" class="btn btn--asosiy">Loyihalar</a>
        <a href="#aloqa" class="btn btn--ikkilamchi">Bog'lanish</a>
      </div>
    </div>
    <div class="hero__rasm">
      <div class="avatar-doira"></div>
    </div>
  </section>

  <!-- Vazifa 3: Statistika -->
  <section class="stat-sektsiya">
    <div class="stat-grid">
      <div class="stat"><strong>42+</strong><span>Loyiha</span></div>
      <div class="stat"><strong>3+</strong><span>Yil tajriba</span></div>
      <div class="stat"><strong>28</strong><span>Mijoz</span></div>
      <div class="stat"><strong>5⭐</strong><span>Reyting</span></div>
    </div>
  </section>

  <!-- Vazifa 4: Haqida -->
  <section class="haqida-sektsiya" id="haqida">
    <div class="haqida-kontent">
      <h2>Men Haqimda</h2>
      <p>Men 3 yillik tajribaga ega Frontend Developer. HTML, CSS, JavaScript va React da loyihalar yarataman.</p>
      <div class="konikma-grid">
        <div class="konikma-element"><i class="fa-brands fa-html5"></i> HTML5</div>
        <div class="konikma-element"><i class="fa-brands fa-css3-alt"></i> CSS3</div>
        <div class="konikma-element"><i class="fa-brands fa-js"></i> JavaScript</div>
        <div class="konikma-element"><i class="fa-brands fa-react"></i> React</div>
        <div class="konikma-element"><i class="fa-brands fa-git-alt"></i> Git</div>
        <div class="konikma-element"><i class="fa-brands fa-figma"></i> Figma</div>
      </div>
    </div>
  </section>

  <!-- Vazifa 5: Loyihalar kartalar -->
  <section class="loyihalar-sektsiya" id="loyihalar">
    <h2>Loyihalar</h2>
    <div class="loyiha-grid">
      <div class="loyiha-karta">
        <img src="https://picsum.photos/400/250?random=1" alt="Loyiha 1">
        <div class="loyiha-info">
          <h3>E-Commerce</h3>
          <p>React + CSS bilan online do'kon</p>
          <div class="loyiha-teglar">
            <span>React</span><span>CSS</span><span>API</span>
          </div>
        </div>
      </div>
      <div class="loyiha-karta">
        <img src="https://picsum.photos/400/250?random=2" alt="Loyiha 2">
        <div class="loyiha-info">
          <h3>Portfolio</h3>
          <p>Shaxsiy portfolio sayt</p>
          <div class="loyiha-teglar">
            <span>HTML</span><span>CSS</span><span>JS</span>
          </div>
        </div>
      </div>
      <div class="loyiha-karta">
        <img src="https://picsum.photos/400/250?random=3" alt="Loyiha 3">
        <div class="loyiha-info">
          <h3>Dashboard</h3>
          <p>Admin panel Grid bilan</p>
          <div class="loyiha-teglar">
            <span>Grid</span><span>Chart.js</span>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- Vazifa 6-7: Aloqa formasi -->
  <section class="aloqa-sektsiya" id="aloqa">
    <h2>Bog'lanish</h2>
    <div class="aloqa-grid">
      <div class="aloqa-info">
        <div class="aloqa-element">
          <i class="fa-solid fa-envelope"></i>
          <div><strong>Email</strong><p>ali@mail.com</p></div>
        </div>
        <div class="aloqa-element">
          <i class="fa-solid fa-phone"></i>
          <div><strong>Telefon</strong><p>+998 90 123 45 67</p></div>
        </div>
        <div class="aloqa-element">
          <i class="fa-solid fa-location-dot"></i>
          <div><strong>Manzil</strong><p>Toshkent, O'zbekiston</p></div>
        </div>
      </div>
      <form class="aloqa-forma">
        <input type="text" placeholder="Ismingiz" required>
        <input type="email" placeholder="Email" required>
        <textarea placeholder="Xabar" rows="4" required></textarea>
        <button type="submit" class="btn btn--asosiy">Yuborish</button>
      </form>
    </div>
  </section>

  <!-- Vazifa 8-10: Footer -->
  <footer class="footer">
    <div class="footer__kontent">
      <p>© 2024 Ali.dev — Barcha huquqlar himoyalangan</p>
      <div class="footer__social">
        <a href="#"><i class="fa-brands fa-github"></i></a>
        <a href="#"><i class="fa-brands fa-linkedin"></i></a>
        <a href="#"><i class="fa-brands fa-telegram"></i></a>
      </div>
    </div>
  </footer>

  <script>
    document.getElementById("hamburger-btn").addEventListener("click", () => {
      document.getElementById("nav-menu").classList.toggle("faol");
    });
  </script>
</body>
</html>
```

```css
/* responsive.css — MOBILE FIRST yondashuvi */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
html { scroll-behavior: smooth; font-size: 16px; }
body { font-family: "Segoe UI", system-ui, sans-serif; color: #1a1a2e; line-height: 1.6; }
section { padding: 60px 20px; }
h2 { font-size: clamp(24px, 5vw, 36px); margin-bottom: 32px; text-align: center; }

/* === NAVBAR === */
/* Vazifa 1: Mobile first navbar */
.navbar {
  position: fixed; top: 0; left: 0; right: 0; z-index: 100;
  height: 60px; display: flex; align-items: center; justify-content: space-between;
  padding: 0 20px; background: rgba(22,33,62,0.97);
  backdrop-filter: blur(8px);
}
.navbar__logo { color: white; font-size: 18px; font-weight: 700; }
.hamburger {
  display: flex; align-items: center; justify-content: center;
  background: none; border: none; color: white; font-size: 20px; cursor: pointer;
}
.nav-menu {
  display: none; flex-direction: column; position: fixed;
  top: 60px; left: 0; right: 0; background: #16213e;
  padding: 20px;
}
.nav-menu.faol { display: flex; }
.nav-menu a { color: rgba(255,255,255,0.8); text-decoration: none; padding: 12px 0;
              border-bottom: 1px solid rgba(255,255,255,0.1); }

/* Tablet+ */
@media (min-width: 768px) {
  .hamburger { display: none; }
  .nav-menu {
    display: flex !important; flex-direction: row; position: static;
    background: none; padding: 0; gap: 28px;
  }
  .nav-menu a { padding: 0; border: none; }
  .nav-menu a:hover { color: white; }
}

/* === HERO === */
/* Vazifa 2: Responsive hero */
.hero {
  min-height: 100vh; padding-top: 80px;
  display: flex; flex-direction: column; align-items: center; justify-content: center;
  text-align: center; gap: 32px;
  background: linear-gradient(135deg, #16213e 0%, #0f3460 100%);
  color: white;
}
.hero__salomlash { font-size: 16px; opacity: 0.8; letter-spacing: 2px; }
.hero__sarlavha  { font-size: clamp(28px, 7vw, 64px); font-weight: 700; margin: 8px 0; }
.hero__mansab    { font-size: clamp(14px, 3vw, 20px); opacity: 0.7; margin-bottom: 24px; }
.hero__tugmalar  { display: flex; gap: 12px; flex-wrap: wrap; justify-content: center; }
.avatar-doira {
  width: clamp(150px, 30vw, 280px); height: clamp(150px, 30vw, 280px);
  border-radius: 50%;
  background: linear-gradient(135deg, royalblue, #764ba2);
  border: 4px solid rgba(255,255,255,0.2);
}
@media (min-width: 768px) {
  .hero { flex-direction: row; text-align: left; padding: 80px 60px 40px; }
  .hero__kontent { flex: 1; }
  .hero__tugmalar { justify-content: flex-start; }
}

/* === STATISTIKA === */
.stat-sektsiya { background: #f8f9fa; padding: 40px 20px; }
.stat-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 16px; max-width: 800px; margin: 0 auto; }
.stat { background: white; padding: 24px; border-radius: 12px; text-align: center;
        box-shadow: 0 4px 16px rgba(0,0,0,0.06); }
.stat strong { display: block; font-size: 32px; color: royalblue; font-weight: 700; }
.stat span   { font-size: 13px; color: #888; }
@media (min-width: 576px) { .stat-grid { grid-template-columns: repeat(4, 1fr); } }

/* === HAQIDA === */
.haqida-sektsiya { background: white; }
.haqida-kontent { max-width: 800px; margin: 0 auto; }
.haqida-kontent h2 { text-align: left; }
.haqida-kontent > p { color: #555; margin-bottom: 24px; font-size: 16px; }
.konikma-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 12px; }
.konikma-element {
  padding: 14px; background: #f0f4ff; border-radius: 10px;
  display: flex; align-items: center; gap: 10px; font-weight: 600; font-size: 14px;
}
.konikma-element i { color: royalblue; font-size: 20px; }
@media (min-width: 576px) { .konikma-grid { grid-template-columns: repeat(3, 1fr); } }

/* === LOYIHALAR === */
.loyihalar-sektsiya { background: #f8f9fa; }
.loyiha-grid {
  display: grid; grid-template-columns: 1fr; gap: 24px;
  max-width: 1100px; margin: 0 auto;
}
@media (min-width: 576px) { .loyiha-grid { grid-template-columns: repeat(2, 1fr); } }
@media (min-width: 992px) { .loyiha-grid { grid-template-columns: repeat(3, 1fr); } }
.loyiha-karta { background: white; border-radius: 16px; overflow: hidden;
                box-shadow: 0 4px 20px rgba(0,0,0,0.06); transition: transform 0.3s; }
.loyiha-karta:hover { transform: translateY(-6px); }
.loyiha-karta img { width: 100%; height: 200px; object-fit: cover; display: block; }
.loyiha-info { padding: 20px; }
.loyiha-info h3 { margin-bottom: 6px; }
.loyiha-info p  { color: #666; font-size: 13px; margin-bottom: 12px; }
.loyiha-teglar { display: flex; gap: 8px; flex-wrap: wrap; }
.loyiha-teglar span {
  padding: 4px 10px; background: #eef2ff; color: royalblue;
  border-radius: 20px; font-size: 11px; font-weight: 600;
}

/* === ALOQA === */
.aloqa-sektsiya { background: white; }
.aloqa-grid { display: grid; grid-template-columns: 1fr; gap: 32px; max-width: 900px; margin: 0 auto; }
@media (min-width: 768px) { .aloqa-grid { grid-template-columns: 1fr 1.5fr; } }
.aloqa-element { display: flex; align-items: flex-start; gap: 14px; margin-bottom: 24px; }
.aloqa-element i { font-size: 22px; color: royalblue; margin-top: 2px; }
.aloqa-element strong { display: block; margin-bottom: 2px; }
.aloqa-element p { color: #666; font-size: 14px; }
.aloqa-forma { display: flex; flex-direction: column; gap: 12px; }
.aloqa-forma input, .aloqa-forma textarea {
  padding: 12px 16px; border: 1px solid #e0e0e0; border-radius: 8px;
  font-size: 15px; font-family: inherit; outline: none; transition: border-color 0.2s;
}
.aloqa-forma input:focus, .aloqa-forma textarea:focus { border-color: royalblue; }
.aloqa-forma textarea { resize: vertical; }

/* === FOOTER === */
.footer { background: #16213e; color: rgba(255,255,255,0.7); padding: 24px 20px; }
.footer__kontent {
  max-width: 900px; margin: 0 auto;
  display: flex; flex-direction: column; align-items: center; gap: 12px;
}
@media (min-width: 576px) {
  .footer__kontent { flex-direction: row; justify-content: space-between; }
}
.footer__social { display: flex; gap: 16px; }
.footer__social a { color: rgba(255,255,255,0.7); font-size: 20px; text-decoration: none;
                    transition: color 0.2s; }
.footer__social a:hover { color: white; }

/* Umumiy tugmalar */
.btn { display: inline-block; padding: 12px 28px; border-radius: 8px; font-size: 15px;
       font-weight: 600; cursor: pointer; text-decoration: none; border: none; }
.btn--asosiy    { background: royalblue; color: white; }
.btn--ikkilamchi { background: rgba(255,255,255,0.15); color: white;
                   border: 1px solid rgba(255,255,255,0.4); }
```
