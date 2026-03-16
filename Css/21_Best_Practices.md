# 21-Dars: CSS Best Practices va Accessibility

## 📌 Vendor Prefikslar (MOZ, WEB, Safari)

```css
/* Vendor prefikslar — brauzer muvofiqligini ta'minlash */
.el {
  /* -webkit-  → Chrome, Safari, yangi Edge */
  /* -moz-     → Firefox */
  /* -ms-      → Eski Internet Explorer */
  /* -o-       → Eski Opera */

  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none; /* ← Standart (har doim oxirida) */

  -webkit-backdrop-filter: blur(10px);
  backdrop-filter: blur(10px);

  -webkit-text-stroke: 1px black;
  text-stroke: 1px black;
}

/* Scrollbar stilini berish */
.scroll-quti {
  /* Firefox */
  scrollbar-width: thin;
  scrollbar-color: royalblue #f0f0f0;
  
  /* Chrome, Safari, Edge */
  &::-webkit-scrollbar { width: 8px; }
  &::-webkit-scrollbar-track { background: #f0f0f0; }
  &::-webkit-scrollbar-thumb { background: royalblue; border-radius: 4px; }
  &::-webkit-scrollbar-thumb:hover { background: navy; }
}
```

---

## 📌 Scrolling va Loading Effektlar

```css
/* Smooth scroll */
html { scroll-behavior: smooth; }

/* Scroll snap — Bir-birini yuzasidan o'tkazish */
.slider-konteyner {
  display: flex;
  overflow-x: auto;
  scroll-snap-type: x mandatory;
  gap: 16px;
}
.slide {
  flex: 0 0 100%;
  scroll-snap-align: start;
}

/* Overscroll — bounce effekti */
.modal { overscroll-behavior: contain; }
html { overscroll-behavior-y: none; }

/* Top loader (progress bar tepada) */
.top-loader {
  position: fixed;
  top: 0; left: 0;
  height: 3px;
  background: linear-gradient(90deg, royalblue, purple);
  z-index: 9999;
  animation: yuklash 1.5s ease infinite;
}
@keyframes yuklash {
  0% { width: 0; opacity: 1; }
  80% { width: 90%; opacity: 1; }
  100% { width: 100%; opacity: 0; }
}
```

---

## 📌 CSS Custom Properties (Variables) — Yangi Usul

```css
/* :root da global o'zgaruvchilar */
:root {
  --rang-asosiy: royalblue;
  --rang-fon: #f8f9fa;
  --rang-matn: #1a1a2e;

  --radius-sm: 6px;
  --radius-md: 12px;
  --radius-lg: 20px;

  --soya-sm: 0 2px 8px rgba(0,0,0,0.06);
  --soya-md: 0 4px 20px rgba(0,0,0,0.08);

  --o'tish: all 0.3s ease;

  --konteyner: 1200px;
  --padding: clamp(16px, 5vw, 40px);
}

/* Dark mode */
@media (prefers-color-scheme: dark) {
  :root {
    --rang-fon: #1a1a2e;
    --rang-matn: #f8f9fa;
  }
}

/* JavaScript bilan o'zgartirish */
.qorongu-tema { --rang-fon: #1a1a2e; --rang-matn: white; }

/* Ishlatish */
.el {
  background: var(--rang-fon, white);  /* Fallback qiymati */
  color: var(--rang-matn);
  border-radius: var(--radius-md);
  transition: var(--o'tish);
}
```

---

## 📌 Accessibility (Foydalanish imkoniyati)

```css
/* 1. Focus — klaviatura foydalanuvchilari uchun */
/* HECH QACHON faqat outline: none qilib qo'ymang! */
:focus-visible {
  outline: 3px solid royalblue;
  outline-offset: 2px;
}
/* :focus-visible — faqat klaviaturada navigatsiya qilganda ko'rinadi */

/* 2. Skip link — ekran o'quvchilar uchun */
.skip-link {
  position: absolute;
  top: -100%;
  left: 8px;
  background: royalblue;
  color: white;
  padding: 8px 16px;
  border-radius: 0 0 8px 8px;
  z-index: 9999;
}
.skip-link:focus { top: 0; }

/* 3. Screen reader faqat kontent */
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border: 0;
}

/* 4. Rang kontrastini kuzatish */
/* WCAG AA: 4.5:1 kontrast nisbati */
/* Yaxshi: Qora matn oq fonda = 21:1 */
/* Kichik matn: kamida 4.5:1 */
/* Katta matn (18px+): kamida 3:1 */

/* 5. Reduced motion */
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}
```

---

## 📌 CSS Performance va Optimallashtirish

```css
/* 1. will-change — animatsiya ilgari tayyorlanadi */
.animatsion-el {
  will-change: transform, opacity; /* GPU ga yuboradi */
}
/* ⚠️ Faqat haqiqatan kerakli elementlarda ishlating! */

/* 2. contain — render optimallashtirish */
.izolatsion-el {
  contain: layout style paint;
}

/* 3. content-visibility — Ko'rinmaydigan elementlarni skip qilish */
.uzun-maqola {
  content-visibility: auto;
  contain-intrinsic-size: 0 500px; /* Taxminiy balandlik */
}

/* 4. Loading atributi (HTML) */
/* <img loading="lazy" alt="..."> */
/* <iframe loading="lazy"> */

/* 5. Critical CSS inline qilish */
/* head ichida eng muhim CSS inline yuklanadi, qolganini defer */

/* 6. font-display */
@font-face {
  font-family: "MyFont";
  src: url("font.woff2");
  font-display: swap; /* Zaxira font ko'rsatadi, asosiy yuklanguncha */
}
```

---

## 📌 CSS Yozish Tartibi (Best Practice)

```css
/* Tavsiya etilgan CSS xossalar tartibi */
.el {
  /* 1. Positioning */
  position: relative;
  top: 0; right: 0; bottom: 0; left: 0;
  z-index: 10;

  /* 2. Box Model */
  display: flex;
  width: 300px;
  height: 200px;
  padding: 16px;
  margin: 20px auto;
  overflow: hidden;
  border: 1px solid #ddd;
  border-radius: 12px;

  /* 3. Visual */
  background: white;
  color: #1a1a2e;
  box-shadow: 0 4px 20px rgba(0,0,0,0.1);
  opacity: 1;
  visibility: visible;

  /* 4. Typography */
  font-family: "Inter", sans-serif;
  font-size: 16px;
  font-weight: 400;
  line-height: 1.6;
  text-align: left;

  /* 5. Transforms */
  transform: translateX(0);
  transition: all 0.3s ease;
}
```

---

## 🎯 10 ta Amaliy Vazifa

```html
<!DOCTYPE html>
<html lang="uz">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Best Practices</title>
  <link rel="stylesheet" href="best-practices.css">
</head>
<body>

  <!-- Accessibility: Skip link -->
  <a href="#asosiy-kontent" class="skip-link">Asosiy kontentga o'tish</a>

  <!-- Vazifa 1: Custom properties bilan Tema -->
  <div class="tema-demo">
    <button id="tema-almashtir" class="btn" aria-label="Temani almashtirish">🌙 Tema</button>
  </div>

  <header role="banner">
    <nav aria-label="Asosiy navigatsiya">
      <div class="navbar">
        <a href="#" class="logo" aria-label="Bosh sahifaga qaytish">🎨 MyApp</a>
        <ul role="list">
          <li><a href="#bosh">Bosh</a></li>
          <li><a href="#xizmatlar">Xizmatlar</a></li>
          <li><a href="#aloqa">Aloqa</a></li>
        </ul>
      </div>
    </nav>
  </header>

  <!-- Vazifa 2: Top Loader -->
  <div class="top-loader" id="top-loader" aria-hidden="true"></div>

  <main id="asosiy-kontent" role="main">

    <!-- Vazifa 3: Focus-visible -->
    <section class="qutiblar-sektsiya">
      <h2>Tugmalar (Tab bilan sinovdan o'tkazing)</h2>
      <div class="tugmalar-row">
        <button class="btn btn-asosiy">Asosiy tugma</button>
        <button class="btn btn-ikkilamchi">Ikkilamchi</button>
        <a href="#" class="btn btn-link">Link tugma</a>
      </div>
    </section>

    <!-- Vazifa 4: Scroll Snap -->
    <section class="slider-sektsiya" aria-label="Rasmlar silaydr">
      <h2>Scroll Snap Silaydr</h2>
      <div class="slider" role="list">
        <div class="slide" role="listitem" aria-label="Slayd 1">
          <img src="https://picsum.photos/800/400?random=1" alt="Birinchi slayd rasmi">
          <div class="slide__matn"><h3>Slayd 1</h3></div>
        </div>
        <div class="slide" role="listitem" aria-label="Slayd 2">
          <img src="https://picsum.photos/800/400?random=2" alt="Ikkinchi slayd rasmi">
          <div class="slide__matn"><h3>Slayd 2</h3></div>
        </div>
        <div class="slide" role="listitem" aria-label="Slayd 3">
          <img src="https://picsum.photos/800/400?random=3" alt="Uchinchi slayd rasmi">
          <div class="slide__matn"><h3>Slayd 3</h3></div>
        </div>
      </div>
    </section>

    <!-- Vazifa 5: Lazy loading rasmlar -->
    <section class="galereya-sektsiya">
      <h2>Lazy Loading Galereya</h2>
      <div class="galereya">
        <img loading="lazy" src="https://picsum.photos/400/300?random=11" alt="Galereya 1">
        <img loading="lazy" src="https://picsum.photos/400/300?random=12" alt="Galereya 2">
        <img loading="lazy" src="https://picsum.photos/400/300?random=13" alt="Galereya 3">
        <img loading="lazy" src="https://picsum.photos/400/300?random=14" alt="Galereya 4">
      </div>
    </section>

    <!-- Vazifa 6: Custom scrollbar -->
    <section class="scroll-sektsiya">
      <h2>Custom Scrollbar</h2>
      <div class="scroll-quti">
        <p>CSS Custom scrollbar bilan...</p>
        <p>Lorem ipsum dolor sit amet consectetur adipiscing elit.</p>
        <p>Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>
        <p>Ut enim ad minim veniam quis nostrud exercitation ullamco.</p>
        <p>Laboris nisi ut aliquip ex ea commodo consequat duis aute.</p>
        <p>Irure dolor in reprehenderit in voluptate velit esse cillum.</p>
      </div>
    </section>

    <!-- Vazifa 7: Accessible forma -->
    <section class="forma-sektsiya">
      <h2>Accessible Forma</h2>
      <form aria-label="Aloqa formasi">
        <div class="forma-guruh">
          <label for="ism-kiritish">Ism <span aria-hidden="true">*</span></label>
          <input type="text" id="ism-kiritish" name="ism" required
                 aria-required="true" autocomplete="name" placeholder="Ismingiz">
        </div>
        <div class="forma-guruh">
          <label for="email-kiritish">Email <span aria-hidden="true">*</span></label>
          <input type="email" id="email-kiritish" name="email" required
                 aria-required="true" autocomplete="email" placeholder="email@mail.com">
        </div>
        <button type="submit" class="btn btn-asosiy">Yuborish</button>
      </form>
    </section>

  </main>

  <!-- Vazifa 8: Screen reader faqat matn -->
  <div aria-live="polite" aria-atomic="true" class="sr-only" id="xabar-maydon"></div>

  <script>
    // Vazifa 9: Tema almashtirish
    const btn = document.getElementById("tema-almashtir");
    btn.addEventListener("click", () => {
      document.documentElement.classList.toggle("qorongu");
      btn.textContent = document.documentElement.classList.contains("qorongu") ? "☀️ Yorug'" : "🌙 Qorongu";
    });

    // Vazifa 10: Top loader simulyatsiya
    const loader = document.getElementById("top-loader");
    window.addEventListener("load", () => {
      loader.style.width = "100%";
      setTimeout(() => { loader.style.opacity = "0"; }, 500);
    });
  </script>

</body>
</html>
```

```css
/* best-practices.css */
/* === CUSTOM PROPERTIES === */
:root {
  --rang-asosiy: royalblue;
  --rang-fon: #f8f9fa;
  --rang-matn: #1a1a2e;
  --rang-chegara: #e0e0e0;
  --rang-karta: white;

  --radius-sm: 8px;
  --radius-md: 14px;
  --radius-lg: 20px;

  --soya: 0 4px 20px rgba(0,0,0,0.08);
  --o'tish: all 0.3s ease;
  --konteyner: 1000px;
}

/* Qorongu tema */
:root.qorongu {
  --rang-fon: #0f172a;
  --rang-matn: #e2e8f0;
  --rang-chegara: #334155;
  --rang-karta: #1e293b;
}

*,*::before,*::after { box-sizing: border-box; margin: 0; padding: 0; }

html { scroll-behavior: smooth; font-size: 16px; }
body {
  font-family: "Segoe UI", system-ui, sans-serif;
  background: var(--rang-fon);
  color: var(--rang-matn);
  transition: background 0.3s, color 0.3s;
  line-height: 1.6;
}

/* Skip link */
.skip-link {
  position: absolute; top: -100%; left: 8px;
  background: var(--rang-asosiy); color: white;
  padding: 8px 16px; border-radius: 0 0 8px 8px; z-index: 9999;
  transition: top 0.2s; text-decoration: none; font-weight: 600;
}
.skip-link:focus { top: 0; }
.sr-only {
  position: absolute; width: 1px; height: 1px;
  padding: 0; margin: -1px; overflow: hidden;
  clip: rect(0,0,0,0); white-space: nowrap; border: 0;
}

/* Vazifa 1: Tema tugmasi */
.tema-demo { position: fixed; bottom: 24px; right: 24px; z-index: 100; }

/* Navbar */
.navbar {
  display: flex; align-items: center; justify-content: space-between;
  padding: 16px 24px; background: var(--rang-karta);
  box-shadow: 0 1px 0 var(--rang-chegara); position: sticky; top: 0; z-index: 50;
}
.navbar .logo { font-weight: 700; font-size: 20px; color: var(--rang-matn); text-decoration: none; }
.navbar ul { list-style: none; display: flex; gap: 24px; }
.navbar a { color: var(--rang-matn); text-decoration: none; opacity: 0.75; }
.navbar a:hover { opacity: 1; }

/* Vazifa 2: Top loader */
.top-loader {
  position: fixed; top: 0; left: 0; height: 3px; z-index: 9999;
  width: 0; opacity: 1;
  background: linear-gradient(90deg, var(--rang-asosiy), purple);
  transition: width 2s cubic-bezier(0.1,0.5,0.5,1), opacity 0.5s;
}

main { max-width: var(--konteyner); margin: 0 auto; padding: 40px 24px; }
section { margin-bottom: 48px; }
h2 { font-size: 24px; margin-bottom: 20px; }

/* Vazifa 3: Focus visible */
:focus-visible {
  outline: 3px solid var(--rang-asosiy);
  outline-offset: 3px;
  border-radius: 4px;
}
.tugmalar-row { display: flex; gap: 12px; flex-wrap: wrap; }

/* Tugmalar */
.btn {
  padding: 10px 22px; border: none; border-radius: var(--radius-sm);
  font-size: 15px; font-weight: 600; cursor: pointer;
  transition: var(--o'tish); display: inline-flex; align-items: center; gap: 8px;
  text-decoration: none;
}
.btn:hover { transform: translateY(-2px); }
.btn:active { transform: translateY(0); }
.btn-asosiy { background: var(--rang-asosiy); color: white; }
.btn-ikkilamchi { background: var(--rang-chegara); color: var(--rang-matn); }
.btn-link { background: transparent; color: var(--rang-asosiy); text-decoration: underline; }

/* Vazifa 4: Scroll Snap */
.slider {
  display: flex; overflow-x: auto; gap: 16px;
  scroll-snap-type: x mandatory;
  scrollbar-width: none;
  -webkit-overflow-scrolling: touch;
}
.slider::-webkit-scrollbar { display: none; }
.slide {
  flex: 0 0 100%; scroll-snap-align: start;
  border-radius: var(--radius-md); overflow: hidden; position: relative;
}
.slide img { width: 100%; height: 300px; object-fit: cover; display: block; }
.slide__matn {
  position: absolute; bottom: 0; left: 0; right: 0; padding: 20px;
  background: linear-gradient(transparent, rgba(0,0,0,0.7)); color: white;
}

/* Vazifa 5: Galereya */
.galereya {
  display: grid; grid-template-columns: repeat(auto-fill, minmax(180px, 1fr)); gap: 12px;
}
.galereya img {
  width: 100%; height: 150px; object-fit: cover;
  border-radius: var(--radius-sm); display: block;
}

/* Vazifa 6: Custom scrollbar */
.scroll-quti {
  height: 160px; overflow-y: auto; padding: 16px;
  background: var(--rang-karta); border-radius: var(--radius-md);
  border: 1px solid var(--rang-chegara);

  scrollbar-width: thin;
  scrollbar-color: var(--rang-asosiy) var(--rang-fon);
}
.scroll-quti::-webkit-scrollbar { width: 6px; }
.scroll-quti::-webkit-scrollbar-track { background: var(--rang-fon); border-radius: 3px; }
.scroll-quti::-webkit-scrollbar-thumb { background: var(--rang-asosiy); border-radius: 3px; }
.scroll-quti p { margin-bottom: 12px; font-size: 14px; }

/* Vazifa 7: Accessible forma */
.forma-guruh { margin-bottom: 16px; display: flex; flex-direction: column; gap: 6px; }
.forma-guruh label { font-weight: 600; font-size: 14px; }
.forma-guruh span { color: #e63946; }
.forma-guruh input {
  padding: 10px 14px; border: 2px solid var(--rang-chegara);
  border-radius: var(--radius-sm); font-size: 15px; font-family: inherit;
  background: var(--rang-karta); color: var(--rang-matn);
  outline: none; transition: border-color 0.2s;
}
.forma-guruh input:focus { border-color: var(--rang-asosiy); }
.forma-guruh input:invalid:not(:placeholder-shown) { border-color: #e63946; }
```