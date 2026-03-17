# 11-Dars: HTML Best Practices va SEO

## 📌 Meta Teglar va SEO

```html
<head>
  <!-- 1. Kodlash — BOU BIRINCHI bo'lishi SHART -->
  <meta charset="UTF-8">

  <!-- 2. Viewport -->
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <!-- 3. Sahifa sarlavhasi — 50-60 belgi -->
  <title>HTML Kursi | Frontend Academy — Toshkent</title>

  <!-- 4. Tavsif — 150-160 belgi -->
  <meta name="description" content="HTML, CSS va JavaScript kurslarini online o'rganing. 3 oyda professional frontend developer bo'ling!">

  <!-- 5. Kalit so'zlar -->
  <meta name="keywords" content="html kurs, css dars, javascript uzbekcha, frontend uzbekistan">

  <!-- 6. Muallif -->
  <meta name="author" content="Ali Valiev">

  <!-- 7. Robots -->
  <meta name="robots" content="index, follow">      <!-- Indekslasin, havolalarni kuzatsin -->
  <meta name="robots" content="noindex, nofollow">  <!-- Indekslamasin -->

  <!-- 8. Open Graph (Facebook, Telegram) -->
  <meta property="og:title" content="Frontend Academy | Online Kurslar">
  <meta property="og:description" content="HTML, CSS va JavaScript o'rganing!">
  <meta property="og:image" content="https://mysite.com/og-image.jpg">
  <meta property="og:url" content="https://mysite.com">
  <meta property="og:type" content="website">
  <meta property="og:locale" content="uz_UZ">
  <meta property="og:site_name" content="Frontend Academy">

  <!-- 9. Twitter Card -->
  <meta name="twitter:card" content="summary_large_image">
  <meta name="twitter:title" content="Frontend Academy">
  <meta name="twitter:description" content="HTML, CSS va JavaScript o'rganing!">
  <meta name="twitter:image" content="https://mysite.com/twitter-image.jpg">

  <!-- 10. Canonical URL (takroriy kontent muammosini hal qilish) -->
  <link rel="canonical" href="https://mysite.com/html-kurs">

  <!-- 11. Favicon -->
  <link rel="icon" type="image/png" href="/favicon-32.png" sizes="32x32">
  <link rel="apple-touch-icon" href="/apple-touch-icon.png">

  <!-- 12. Tezlashtirish -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preload" href="style.css" as="style">
  <link rel="preload" href="hero.jpg" as="image">
</head>
```

---

## 📌 Semantik HTML va SEO

```html
<!-- ✅ SEO uchun to'g'ri tuzilma -->
<body>
  <header>
    <!-- Har sahifada faqat BITTA h1 -->
    <h1>Frontend Dasturlash Kursi</h1>
    <nav aria-label="Asosiy navigatsiya">
      <ul>
        <li><a href="/">Bosh</a></li>
        <li><a href="/kurslar">Kurslar</a></li>
      </ul>
    </nav>
  </header>

  <main>
    <article>
      <h2>HTML Asoslari</h2>           <!-- h2 — bo'lim sarlavhasi -->
      <p>Matn...</p>
      <h3>Teglar nima?</h3>            <!-- h3 — pastki bo'lim -->
      <p>Matn...</p>
    </article>
  </main>

  <footer>
    <address>
      📍 Toshkent, O'zbekiston
    </address>
  </footer>
</body>

<!-- ❌ YOMON — div to'pi, sarlavhalar tartibsiz -->
<div class="header">
  <h3>Kurs</h3>          <!-- h1 yo'q, h3 dan boshlanmoqda -->
</div>
<div>
  <h1>HTML</h1>          <!-- Ikkinchi h1! -->
</div>
```

---

## 📌 Rasm SEO va Performance

```html
<!-- ✅ To'g'ri -->
<img
  src="html-kurs-toshkent.webp"    <!-- SEO uchun ma'noli fayl nomi -->
  alt="Toshkentdagi HTML kursi o'quvchilari"  <!-- Tavsifli alt matn -->
  width="800"                       <!-- CLS (layout shift) oldini olish -->
  height="450"
  loading="lazy"                    <!-- Performance -->
  decoding="async"
>

<!-- ❌ YOMON -->
<img src="img123.jpg" alt="">       <!-- Alt bo'sh, fayl nomi ma'nosiz -->
<img src="photo.png">               <!-- Alt yo'q! -->

<!-- WebP format (kichik hajm, sifat saqlanadi) -->
<picture>
  <source type="image/webp" srcset="hero.webp">
  <img src="hero.jpg" alt="Hero banner" width="1200" height="600">
</picture>
```

---

## 📌 Strukturali Ma'lumotlar (Schema.org)

```html
<!-- JSON-LD — Google ko'rishi uchun -->
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Course",
  "name": "HTML va CSS Asoslari Kursi",
  "description": "Boshlang'ichlar uchun HTML va CSS kursi",
  "provider": {
    "@type": "Organization",
    "name": "Frontend Academy",
    "url": "https://frontend-academy.uz"
  },
  "inLanguage": "uz",
  "offers": {
    "@type": "Offer",
    "price": "499000",
    "priceCurrency": "UZS"
  }
}
</script>

<!-- Mahsulot uchun -->
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Product",
  "name": "Dell XPS 15",
  "aggregateRating": {
    "@type": "AggregateRating",
    "ratingValue": "4.8",
    "reviewCount": "342"
  }
}
</script>
```

---

## 📌 Accessibility (A11y) Best Practices

```html
<!-- 1. Alt matni -->
<img src="logo.svg" alt="Frontend Academy logotipi">
<img src="bezak.svg" alt="">   <!-- Bezak — bo'sh alt -->

<!-- 2. Skip link -->
<a href="#asosiy" class="skip-link">Asosiy kontentga o'tish</a>

<!-- 3. Aria atributlar -->
<button aria-label="Menyuni yopish">×</button>
<nav aria-label="Asosiy navigatsiya">...</nav>
<div role="alert">Xato yuz berdi!</div>
<div aria-live="polite" aria-atomic="true">Yuklanmoqda...</div>

<!-- 4. Form label -->
<label for="email">Email manzilingiz</label>
<input type="email" id="email" name="email">

<!-- 5. Focus ko'rinadigan bo'lsin -->
<style>
  :focus-visible { outline: 3px solid royalblue; outline-offset: 2px; }
</style>

<!-- 6. Kontrast: kamida 4.5:1 -->
<!-- Yaxshi: qora matn (#000) oq fon (#fff) = 21:1 -->
<!-- Yomon: och kulrang (#ccc) oq fon (#fff) = 1.6:1 -->
```

---

## 🎯 10 ta Amaliy Vazifa — SEO Optimallashtirilgan Sahifa

```html
<!DOCTYPE html>
<html lang="uz">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <!-- Vazifa 1: SEO meta teglar -->
  <title>Frontend Academy | HTML va CSS Kurslari — Toshkent</title>
  <meta name="description" content="Toshkentda eng yaxshi HTML, CSS va JavaScript kurslari. 3 oyda professional frontend developer bo'ling. Hozir ro'yxatdan o'ting!">
  <meta name="keywords" content="html kurs toshkent, css dars, javascript uzbekcha, frontend dasturlash">
  <meta name="author" content="Frontend Academy">
  <meta name="robots" content="index, follow">

  <!-- Vazifa 2: Open Graph -->
  <meta property="og:title" content="Frontend Academy | Dasturlash Kurslari">
  <meta property="og:description" content="HTML, CSS va JavaScript o'rganing!">
  <meta property="og:image" content="https://mysite.uz/og-image.jpg">
  <meta property="og:url" content="https://mysite.uz">
  <meta property="og:type" content="website">
  <meta property="og:locale" content="uz_UZ">

  <!-- Canonical -->
  <link rel="canonical" href="https://frontend-academy.uz">

  <!-- Favicon -->
  <link rel="icon" type="image/png" href="favicon.png">

  <!-- Schema.org JSON-LD -->
  <script type="application/ld+json">
  {
    "@context": "https://schema.org",
    "@type": "EducationalOrganization",
    "name": "Frontend Academy",
    "url": "https://frontend-academy.uz",
    "address": { "@type": "PostalAddress", "addressLocality": "Toshkent", "addressCountry": "UZ" }
  }
  </script>

  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    html { scroll-behavior: smooth; }
    body { font-family: "Segoe UI", sans-serif; color: #1a1a2e; line-height: 1.6; }

    /* Vazifa 3: Skip link */
    .skip-link {
      position: absolute; top: -100%; left: 8px;
      background: royalblue; color: white; padding: 8px 16px;
      border-radius: 0 0 8px 8px; z-index: 9999; text-decoration: none; font-weight: 600;
    }
    .skip-link:focus { top: 0; }

    /* Focus */
    :focus-visible { outline: 3px solid royalblue; outline-offset: 2px; border-radius: 4px; }

    /* Vazifa 4: Semantic header */
    header { background: #16213e; color: white; padding: 16px 40px; }
    header .bosh { display: flex; align-items: center; justify-content: space-between; }
    header .logo { font-size: 22px; font-weight: 700; color: white; text-decoration: none; }
    header .logo span { color: royalblue; }

    nav ul { list-style: none; display: flex; gap: 20px; }
    nav a { color: rgba(255,255,255,0.8); text-decoration: none; transition: color 0.2s; }
    nav a:hover, nav a[aria-current] { color: white; }

    /* Vazifa 5: Hero h1 */
    .hero {
      min-height: 85vh; display: flex; align-items: center; justify-content: center;
      background: linear-gradient(135deg, #1a1a2e, #16213e);
      color: white; text-align: center; padding: 40px 20px;
    }
    .hero__tarkib { max-width: 700px; }
    .hero__teg { display: inline-block; background: rgba(65,105,225,0.2); color: #93c5fd;
                 padding: 6px 14px; border-radius: 20px; font-size: 13px; margin-bottom: 16px; }
    .hero h1 { font-size: clamp(32px, 6vw, 60px); font-weight: 800; margin-bottom: 16px; }
    .hero p  { font-size: 18px; opacity: 0.8; margin-bottom: 28px; }
    .hero-tugmalar { display: flex; gap: 12px; justify-content: center; flex-wrap: wrap; }
    .btn { padding: 12px 28px; border-radius: 10px; font-weight: 700; font-size: 15px;
           text-decoration: none; border: none; cursor: pointer; transition: all 0.2s; }
    .btn-asosiy { background: royalblue; color: white; }
    .btn-asosiy:hover { background: #2c5282; transform: translateY(-2px); }
    .btn-ochiq { background: rgba(255,255,255,0.1); color: white; border: 1px solid rgba(255,255,255,0.3); }

    /* Vazifa 6: Article tuzilmasi */
    main { max-width: 1100px; margin: 0 auto; padding: 60px 20px; }

    .kurs-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(300px, 1fr)); gap: 24px; margin-bottom: 60px; }
    article.kurs-karta { background: white; border-radius: 16px; overflow: hidden; box-shadow: 0 4px 20px rgba(0,0,0,0.07); }
    article.kurs-karta img { width: 100%; height: 180px; object-fit: cover; display: block; }
    .karta-tana { padding: 20px; }
    .karta-tana h2 { font-size: 18px; margin: 8px 0; }     /* h2 — bo'lim sarlavhasi */
    .karta-tana p  { color: #666; font-size: 14px; margin-bottom: 14px; }
    .karta-oyoq { display: flex; justify-content: space-between; align-items: center; }
    .kurs-teg { background: #f0f4ff; color: royalblue; padding: 4px 10px; border-radius: 20px; font-size: 12px; font-weight: 600; }
    .narx { font-weight: 700; color: royalblue; }

    /* Vazifa 7: Breadcrumb */
    .breadcrumb { display: flex; gap: 8px; align-items: center; font-size: 13px; color: #888; margin-bottom: 32px; }
    .breadcrumb a { color: royalblue; text-decoration: none; }
    .breadcrumb a:hover { text-decoration: underline; }
    .breadcrumb [aria-current] { color: #1a1a2e; font-weight: 600; }

    /* Vazifa 8: FAQ bo'limi */
    .faq h2 { font-size: 28px; text-align: center; margin-bottom: 32px; }
    .faq details { border: 1px solid #e5e7eb; border-radius: 12px; margin-bottom: 8px; }
    .faq summary { padding: 16px 20px; cursor: pointer; font-weight: 600; display: flex; justify-content: space-between; }
    .faq summary::after { content: "+"; font-size: 20px; }
    .faq details[open] summary::after { content: "−"; }
    .faq details p { padding: 0 20px 16px; color: #555; }

    /* Vazifa 9: Address va footer */
    footer { background: #16213e; color: rgba(255,255,255,0.7); padding: 40px; }
    .footer-grid { max-width: 1100px; margin: 0 auto; display: grid; grid-template-columns: 1.5fr 1fr 1fr; gap: 40px; }
    .footer-grid h3 { color: white; margin-bottom: 14px; font-size: 15px; }
    .footer-grid ul { list-style: none; }
    .footer-grid ul li { margin-bottom: 8px; }
    .footer-grid a { color: rgba(255,255,255,0.65); text-decoration: none; font-size: 14px; }
    .footer-grid a:hover { color: white; }
    address { font-style: normal; font-size: 14px; }
    address p { margin-bottom: 6px; display: flex; align-items: center; gap: 8px; }
    .footer-pastki { max-width: 1100px; margin: 24px auto 0; padding-top: 20px; border-top: 1px solid rgba(255,255,255,0.1);
                     display: flex; justify-content: space-between; align-items: center; font-size: 13px; }
  </style>
</head>
<body>

  <!-- Vazifa 3: Skip link -->
  <a href="#asosiy-kontent" class="skip-link">Asosiy kontentga o'tish</a>

  <!-- Vazifa 4: Semantic header -->
  <header role="banner">
    <div class="bosh">
      <a href="/" class="logo">Frontend <span>Academy</span></a>
      <nav aria-label="Asosiy navigatsiya">
        <ul>
          <li><a href="/" aria-current="page">Bosh</a></li>
          <li><a href="/kurslar">Kurslar</a></li>
          <li><a href="/haqida">Haqida</a></li>
          <li><a href="/aloqa">Aloqa</a></li>
        </ul>
      </nav>
    </div>
  </header>

  <!-- Vazifa 5: Hero section (bir sahifada faqat bitta h1!) -->
  <section class="hero" aria-label="Asosiy Banner">
    <div class="hero__tarkib">
      <span class="hero__teg">🚀 2024 yangi kurs!</span>
      <h1>Frontend Dasturlashni O'rganing</h1>
      <p>HTML, CSS va JavaScript bilan zamonaviy veb saytlar yaring. 3 oyda ishga tayyorlanamiz!</p>
      <div class="hero-tugmalar">
        <a href="/royhxatdan-otish" class="btn btn-asosiy">Hozir Boshlang</a>
        <a href="#kurslar" class="btn btn-ochiq">Kurslarni ko'rish</a>
      </div>
    </div>
  </section>

  <!-- Asosiy kontent -->
  <main id="asosiy-kontent" role="main">

    <!-- Vazifa 7: Breadcrumb -->
    <nav class="breadcrumb" aria-label="Breadcrumb">
      <a href="/">🏠 Bosh</a> <span aria-hidden="true">›</span>
      <span aria-current="page">Kurslar</span>
    </nav>

    <!-- Vazifa 6: Article tuzilmasi -->
    <section id="kurslar" aria-labelledby="kurslar-sarlavha">
      <h2 id="kurslar-sarlavha" style="font-size:28px;margin-bottom:24px">Kurslarmiz</h2>
      <div class="kurs-grid">
        <article class="kurs-karta" aria-label="HTML va CSS kursi">
          <img src="https://picsum.photos/400/200?random=1" alt="HTML va CSS amaliy darslar ekran ko'rinishi" loading="lazy" width="400" height="200">
          <div class="karta-tana">
            <span class="kurs-teg">Boshlang'ich</span>
            <h2>HTML va CSS Asoslari</h2>
            <p>Teglar, selektorlar, Flexbox, Grid — 4 hafta.</p>
            <div class="karta-oyoq">
              <span class="narx">199,000 so'm</span>
              <a href="/kurs/html-css" class="btn btn-asosiy" style="font-size:13px;padding:8px 16px">Batafsil →</a>
            </div>
          </div>
        </article>

        <article class="kurs-karta" aria-label="JavaScript kursi">
          <img src="https://picsum.photos/400/200?random=2" alt="JavaScript dars video" loading="lazy" width="400" height="200">
          <div class="karta-tana">
            <span class="kurs-teg">O'rta</span>
            <h2>JavaScript to'liq kurs</h2>
            <p>DOM, ES6+, Fetch API, async/await — 8 hafta.</p>
            <div class="karta-oyoq">
              <span class="narx">349,000 so'm</span>
              <a href="/kurs/javascript" class="btn btn-asosiy" style="font-size:13px;padding:8px 16px">Batafsil →</a>
            </div>
          </div>
        </article>

        <article class="kurs-karta" aria-label="React kursi">
          <img src="https://picsum.photos/400/200?random=3" alt="React kurs materiallari" loading="lazy" width="400" height="200">
          <div class="karta-tana">
            <span class="kurs-teg">Ilg'or</span>
            <h2>React.js Professional</h2>
            <p>Hooks, Redux, Next.js — 10 hafta.</p>
            <div class="karta-oyoq">
              <span class="narx">599,000 so'm</span>
              <a href="/kurs/react" class="btn btn-asosiy" style="font-size:13px;padding:8px 16px">Batafsil →</a>
            </div>
          </div>
        </article>
      </div>
    </section>

    <!-- Vazifa 8: FAQ -->
    <section class="faq" aria-labelledby="faq-sarlavha">
      <h2 id="faq-sarlavha">Ko'p Beriladigan Savollar</h2>
      <details>
        <summary>Kurslar qancha davom etadi?</summary>
        <p>Kursimiz 3 oy davom etadi. Har hafta 3 dars, jami 36 ta dars bor.</p>
      </details>
      <details>
        <summary>Online yoki offline?</summary>
        <p>Ikki formatda ham mavjud. Online — Telegram orqali, offline — Toshkent markazida.</p>
      </details>
      <details>
        <summary>Ish topishga yordam berasizmi?</summary>
        <p>Ha! Kurs tugagach, portfolio yaratamiz va ish topishda yordam beramiz.</p>
      </details>
    </section>

  </main>

  <!-- Vazifa 9: Semantic footer va address -->
  <footer role="contentinfo">
    <div class="footer-grid">
      <div>
        <h3>Frontend Academy</h3>
        <address>
          <p>📍 Toshkent, Chilonzor tumani</p>
          <p>📞 <a href="tel:+998901234567">+998 90 123 45 67</a></p>
          <p>📧 <a href="mailto:info@frontend-academy.uz">info@frontend-academy.uz</a></p>
        </address>
      </div>
      <div>
        <h3>Kurslar</h3>
        <ul>
          <li><a href="/kurs/html">HTML va CSS</a></li>
          <li><a href="/kurs/js">JavaScript</a></li>
          <li><a href="/kurs/react">React.js</a></li>
        </ul>
      </div>
      <div>
        <h3>Ijtimoiy Tarmoqlar</h3>
        <ul>
          <li><a href="https://t.me/frontend_academy_uz" target="_blank" rel="noopener">Telegram</a></li>
          <li><a href="https://youtube.com/@frontend_academy" target="_blank" rel="noopener">YouTube</a></li>
          <li><a href="https://github.com/frontend-academy" target="_blank" rel="noopener noreferrer">GitHub</a></li>
        </ul>
      </div>
    </div>
    <!-- Vazifa 10: Copyright -->
    <div class="footer-pastki">
      <p>© <time datetime="2024">2024</time> Frontend Academy. Barcha huquqlar himoyalangan.</p>
      <nav aria-label="Footer navigatsiya">
        <a href="/maxfiylik">Maxfiylik</a> · <a href="/shartlar">Shartlar</a>
      </nav>
    </div>
  </footer>

</body>
</html>
```
