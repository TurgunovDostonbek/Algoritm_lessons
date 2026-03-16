# 09-Dars: Position — 2-qism (Z-index va Overflow)

## 📌 Z-index — Qatlam Tartibi

`z-index` — elementlarning "chuqurlik" tartibini boshqaradi (qaysi ustida turishi).

```css
/* z-index faqat positioned elementlarda ishlaydi (non-static) */
.birinchi { position: relative; z-index: 1; }
.ikkinchi { position: relative; z-index: 2; } /* Ustida turadi */
.uchinchi { position: relative; z-index: 3; } /* Eng yuqorida */

/* Salbiy z-index — elementning orqasiga */
.fon { position: absolute; z-index: -1; }

/* Umumiy z-index qiymatlari */
.modal-fon     { z-index: 900; }
.modal         { z-index: 1000; }
.tooltip       { z-index: 1100; }
.navbar        { z-index: 100; }
.dropdown      { z-index: 200; }
.notification  { z-index: 9999; }
```

---

## 📌 Stacking Context (Qatlam Konteksti)

```css
/* Yangi stacking context yaratuvchi xossalar: */
.el {
  position: relative; z-index: 1;  /* z-index != auto va positioned */
  opacity: 0.99;                    /* opacity < 1 */
  transform: translateX(0);         /* istalgan transform */
  filter: blur(0);                  /* istalgan filter */
  isolation: isolate;               /* Maxsus */
  will-change: transform;           /* Brauzer optimizatsiyasi */
}
```

---

## 📌 Overflow

```css
.el {
  overflow: visible;  /* Default — tashqariga chiqadi */
  overflow: hidden;   /* Kesiladi (float clearing uchun ham) */
  overflow: scroll;   /* Har doim scrollbar ko'rsatadi */
  overflow: auto;     /* Zarur bo'lganda scrollbar ko'rsatadi */
  overflow: clip;     /* hidden ga o'xshash, lekin scroll bo'lmaydi */

  /* Alohida o'qlar */
  overflow-x: hidden; /* Gorizontal kesiladi */
  overflow-y: auto;   /* Vertikal zarur bo'lganda */
}

/* scroll-behavior — silliq aylanish */
html { scroll-behavior: smooth; }

/* Matnni kesilgan ko'rsatish (...) */
.qisqa-matn {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}

/* Ko'p qatorli matn truncation */
.ko_p-qator {
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 3;  /* 3 qatordan keyin ... */
  overflow: hidden;
}
```

---

## 📌 Position bilan Loyiha Dizayni

```css
/* Modal */
.modal-fon {
  position: fixed;
  inset: 0;
  background: rgba(0,0,0,0.6);
  z-index: 900;
  display: flex;
  align-items: center;
  justify-content: center;
}
.modal {
  position: relative;
  background: white;
  border-radius: 16px;
  padding: 32px;
  width: 90%;
  max-width: 500px;
  z-index: 1000;
}
.modal__yopish {
  position: absolute;
  top: 16px;
  right: 16px;
  background: none;
  border: none;
  font-size: 24px;
  cursor: pointer;
}

/* Sticky sidebar + viewport  */
.layout { display: flex; gap: 24px; }
.sticky-sidebar {
  position: sticky;
  top: 80px;          /* Navbar balandligi */
  height: fit-content;
  flex: 0 0 280px;
}
```

---

## 📌 CSS Transform bilan birga Position

```css
/* Markazlash patternlari */

/* 1. Transform bilan absolute centering */
.absolute-center {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

/* 2. inset: 0 + margin: auto */
.inset-center {
  position: absolute;
  inset: 0;
  margin: auto;
  width: 200px;  /* Aniq o'lcham kerak! */
  height: 100px;
}

/* 3. Flex (eng oson) */
.flex-center {
  display: flex;
  align-items: center;
  justify-content: center;
}
```

---

## 🎯 10 ta Amaliy Vazifa — Z-index va Overflow bilan Loyiha

```html
<!DOCTYPE html>
<html lang="uz">
<head>
  <meta charset="UTF-8">
  <title>Position Part 2</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
  <link rel="stylesheet" href="position2.css">
</head>
<body>

  <!-- Vazifa 1: Yopishgan navbar -->
  <header class="navbar">
    <div class="navbar__logo">🎨 WebCraft</div>
    <nav class="navbar__nav">
      <a href="#xizmatlar">Xizmatlar</a>
      <a href="#portfolio">Portfolio</a>
      <a href="#aloqa">Aloqa</a>
    </nav>
  </header>

  <!-- Vazifa 2: Hero sektsiya -->
  <section class="hero">
    <div class="hero__fon"></div>
    <div class="hero__kontent">
      <h1>Zamonaviy Web Dizayn</h1>
      <p>Position va Z-index bilan profesional layoutlar</p>
      <button class="btn" onclick="document.getElementById('modal-fon').classList.add('faol')">
        Modal Ochish
      </button>
    </div>
    <div class="hero__dekor">
      <div class="dekor-doira dekor-doira--1"></div>
      <div class="dekor-doira dekor-doira--2"></div>
      <div class="dekor-doira dekor-doira--3"></div>
    </div>
  </section>

  <!-- Vazifa 3: Kartalar (z-index hover effekti) -->
  <section id="xizmatlar" class="sektsiya">
    <h2 class="sektsiya__sarlavha">Xizmatlar</h2>
    <div class="kartalar">
      <div class="xizmat-karta">
        <i class="fa-solid fa-layer-group karta__icon"></i>
        <h3>Layerlar</h3>
        <p class="karta__matn">Z-index yordamida kompleks qatlam tizimi</p>
        <div class="karta__tooltip">Batafsil ma'lumot</div>
      </div>
      <div class="xizmat-karta xizmat-karta--featured">
        <div class="featured-yorliq">Mashhur</div>
        <i class="fa-solid fa-wand-magic-sparkles karta__icon"></i>
        <h3>Animatsiya</h3>
        <p class="karta__matn">Position + Transform bilan silliq animatsiyalar</p>
        <div class="karta__tooltip">Batafsil ma'lumot</div>
      </div>
      <div class="xizmat-karta">
        <i class="fa-solid fa-mobile-screen karta__icon"></i>
        <h3>Responsive</h3>
        <p class="karta__matn">Barcha qurilmalarda mukammal ko'rinish</p>
        <div class="karta__tooltip">Batafsil ma'lumot</div>
      </div>
    </div>
  </section>

  <!-- Vazifa 4: Overflow bilan kartalar silaydr -->
  <section class="overflow-sektsiya">
    <h2 class="sektsiya__sarlavha">Portfolio</h2>
    <div class="gorizontal-scroll" id="portfolio">
      <div class="scroll-karta">
        <img src="https://picsum.photos/300/200?random=1" alt="">
        <p class="scroll-karta__matn">Bu matn juda uzun bo'lishi mumkin, shuning uchun truncation ishlatamiz</p>
      </div>
      <div class="scroll-karta">
        <img src="https://picsum.photos/300/200?random=2" alt="">
        <p class="scroll-karta__matn">Lorem ipsum dolor sit amet consectetur adipisicing elit.</p>
      </div>
      <div class="scroll-karta">
        <img src="https://picsum.photos/300/200?random=3" alt="">
        <p class="scroll-karta__matn">Zamonaviy dizayn tendentsiyalari va CSS ilg'or usullari</p>
      </div>
      <div class="scroll-karta">
        <img src="https://picsum.photos/300/200?random=4" alt="">
        <p class="scroll-karta__matn">Grid va Flexbox bilan murakkab layoutlar yaratish</p>
      </div>
    </div>
  </section>

  <!-- Vazifa 5: Sticky sidebar layout -->
  <section id="aloqa" class="sticky-layout">
    <aside class="sticky-sidebar">
      <h3><i class="fa-solid fa-list"></i> Navigatsiya</h3>
      <ul>
        <li><a href="#xizmatlar">Xizmatlar</a></li>
        <li><a href="#portfolio">Portfolio</a></li>
        <li><a href="#aloqa">Aloqa</a></li>
      </ul>
    </aside>
    <main class="asosiy-kontent">
      <h2>Biz Haqimizda</h2>
      <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>
      <p style="margin-top:12px">Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.</p>
      <p style="margin-top:12px">Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.</p>
      <p style="margin-top:12px">Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</p>
      <p style="margin-top:12px">Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore.</p>
    </main>
  </section>

  <!-- Vazifa 6: Modal -->
  <div class="modal-fon" id="modal-fon">
    <div class="modal">
      <button class="modal__yopish" onclick="document.getElementById('modal-fon').classList.remove('faol')">
        <i class="fa-solid fa-xmark"></i>
      </button>
      <h2>Modal Oynasi</h2>
      <p>Bu position: fixed va z-index yordamida yaratilgan modal.</p>
      <div style="margin-top: 20px; display: flex; gap: 12px;">
        <button class="btn">Tasdiqlash</button>
        <button class="btn btn--ikkilamchi" onclick="document.getElementById('modal-fon').classList.remove('faol')">Bekor qilish</button>
      </div>
    </div>
  </div>

  <!-- Vazifa 7-10: Notification va Fixed tugmalar -->
  <div class="notification" id="notification">
    <i class="fa-solid fa-circle-check"></i> Muvaffaqiyatli saqlandi!
    <button onclick="this.parentElement.style.display='none'">✕</button>
  </div>
  <button class="scroll-top" onclick="window.scrollTo({top:0,behavior:'smooth'})">
    <i class="fa-solid fa-arrow-up"></i>
  </button>

</body>
</html>
```

```css
/* position2.css */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
html { scroll-behavior: smooth; }
body { font-family: "Segoe UI", sans-serif; color: #1a1a2e; background: #f8f9fa; }

/* Vazifa 1: Navbar (fixed + z-index) */
.navbar {
  position: fixed; top: 0; left: 0; right: 0;
  height: 64px; background: rgba(22,33,62,0.95); backdrop-filter: blur(8px);
  display: flex; align-items: center; justify-content: space-between;
  padding: 0 40px; z-index: 100;
}
.navbar__logo { color: white; font-size: 20px; font-weight: 700; }
.navbar__nav { display: flex; gap: 28px; }
.navbar__nav a { color: rgba(255,255,255,0.8); text-decoration: none; transition: color 0.2s; }
.navbar__nav a:hover { color: white; }

/* Vazifa 2: Hero (z-index layerlari) */
.hero {
  position: relative; min-height: 100vh;
  display: flex; align-items: center; justify-content: center;
  overflow: hidden; background: #16213e;
}
.hero__fon {
  position: absolute; inset: 0;
  background: linear-gradient(135deg, #0f3460 0%, #16213e 100%);
  z-index: 0;
}
.hero__dekor { position: absolute; inset: 0; z-index: 1; pointer-events: none; }
.dekor-doira {
  position: absolute; border-radius: 50%;
  border: 2px solid rgba(255,255,255,0.1);
}
.dekor-doira--1 { width: 400px; height: 400px; top: -100px; right: -100px; }
.dekor-doira--2 { width: 250px; height: 250px; bottom: -50px; left: 10%; background: rgba(65,105,225,0.1); }
.dekor-doira--3 { width: 150px; height: 150px; top: 30%; left: 5%; background: rgba(255,255,255,0.03); }
.hero__kontent { position: relative; z-index: 2; text-align: center; color: white; padding: 20px; }
.hero__kontent h1 { font-size: clamp(32px, 6vw, 72px); margin-bottom: 16px; }
.hero__kontent p { font-size: 18px; opacity: 0.8; margin-bottom: 32px; }

/* Vazifa 3: Kartalar va hover z-index */
.sektsiya { max-width: 1100px; margin: 0 auto; padding: 80px 32px; }
.sektsiya__sarlavha { font-size: 36px; text-align: center; margin-bottom: 48px; }
.kartalar { display: flex; gap: 24px; flex-wrap: wrap; justify-content: center; }
.xizmat-karta {
  position: relative; width: 300px; padding: 32px 24px; background: white;
  border-radius: 16px; text-align: center; transition: transform 0.3s, z-index 0s;
  box-shadow: 0 4px 20px rgba(0,0,0,0.06); z-index: 1;
}
.xizmat-karta:hover { transform: translateY(-8px) scale(1.02); z-index: 10; }
.xizmat-karta--featured { background: #16213e; color: white; }
.featured-yorliq {
  position: absolute; top: -12px; left: 50%; transform: translateX(-50%);
  background: royalblue; color: white; padding: 4px 16px;
  border-radius: 20px; font-size: 12px; font-weight: 700; white-space: nowrap;
}
.karta__icon { font-size: 40px; color: royalblue; margin-bottom: 16px; }
.xizmat-karta--featured .karta__icon { color: #6a93ff; }
.xizmat-karta h3 { margin-bottom: 12px; font-size: 20px; }
.karta__matn {
  font-size: 14px; color: #666; line-height: 1.6;
  display: -webkit-box; -webkit-box-orient: vertical;
  -webkit-line-clamp: 2; overflow: hidden;
}
.xizmat-karta--featured .karta__matn { color: rgba(255,255,255,0.7); }
.karta__tooltip {
  position: absolute; bottom: calc(100% + 8px); left: 50%; transform: translateX(-50%);
  background: #1a1a2e; color: white; padding: 6px 12px; border-radius: 6px;
  font-size: 12px; white-space: nowrap; opacity: 0; pointer-events: none; transition: opacity 0.2s;
}
.xizmat-karta:hover .karta__tooltip { opacity: 1; }

/* Vazifa 4: Gorizontal scroll (overflow-x) */
.overflow-sektsiya { padding: 60px 32px; }
.overflow-sektsiya .sektsiya__sarlavha { text-align: center; margin-bottom: 32px; }
.gorizontal-scroll {
  display: flex; gap: 20px; overflow-x: auto; padding: 16px 0;
  scrollbar-width: thin; scroll-snap-type: x mandatory;
}
.gorizontal-scroll::-webkit-scrollbar { height: 6px; }
.gorizontal-scroll::-webkit-scrollbar-track { background: #eee; border-radius: 3px; }
.gorizontal-scroll::-webkit-scrollbar-thumb { background: royalblue; border-radius: 3px; }
.scroll-karta {
  flex: 0 0 280px; background: white; border-radius: 12px;
  overflow: hidden; scroll-snap-align: start;
}
.scroll-karta img { width: 100%; height: 180px; object-fit: cover; display: block; }
.scroll-karta__matn {
  padding: 12px; font-size: 14px; color: #555;
  display: -webkit-box; -webkit-box-orient: vertical;
  -webkit-line-clamp: 2; overflow: hidden;
}

/* Vazifa 5: Sticky sidebar */
.sticky-layout { display: flex; gap: 32px; max-width: 1100px; margin: 0 auto; padding: 60px 32px; }
.sticky-sidebar {
  position: sticky; top: 84px; height: fit-content;
  flex: 0 0 220px; background: white; padding: 24px; border-radius: 12px;
  box-shadow: 0 4px 20px rgba(0,0,0,0.06);
}
.sticky-sidebar h3 { margin-bottom: 16px; display: flex; align-items: center; gap: 8px; }
.sticky-sidebar ul { list-style: none; }
.sticky-sidebar li { border-bottom: 1px solid #f0f0f0; }
.sticky-sidebar a { display: block; padding: 10px 0; color: #555; text-decoration: none; transition: color 0.2s; }
.sticky-sidebar a:hover { color: royalblue; }
.asosiy-kontent { flex: 1; background: white; padding: 32px; border-radius: 12px; }
.asosiy-kontent h2 { margin-bottom: 16px; }

/* Vazifa 6: Modal (fixed + z-index) */
.modal-fon {
  position: fixed; inset: 0;
  background: rgba(0,0,0,0.7); backdrop-filter: blur(4px);
  z-index: 900; display: flex; align-items: center; justify-content: center;
  opacity: 0; pointer-events: none; transition: opacity 0.3s;
}
.modal-fon.faol { opacity: 1; pointer-events: all; }
.modal {
  position: relative; background: white; border-radius: 20px;
  padding: 40px; width: 90%; max-width: 480px; z-index: 1000;
  transform: scale(0.9); transition: transform 0.3s;
}
.modal-fon.faol .modal { transform: scale(1); }
.modal h2 { margin-bottom: 12px; }
.modal__yopish {
  position: absolute; top: 16px; right: 16px;
  background: #f0f0f0; border: none; width: 36px; height: 36px;
  border-radius: 50%; cursor: pointer; font-size: 16px;
  display: flex; align-items: center; justify-content: center;
}
.modal__yopish:hover { background: #e0e0e0; }

/* Vazifa 7-8: Notification (fixed, top) */
.notification {
  position: fixed; top: 80px; right: 20px; z-index: 800;
  background: #51cf66; color: white; padding: 12px 20px;
  border-radius: 10px; display: flex; align-items: center; gap: 10px;
  box-shadow: 0 4px 20px rgba(81,207,102,0.3); font-weight: 600;
}
.notification button { background: none; border: none; color: white; cursor: pointer; font-size: 16px; }

/* Vazifa 9-10: Scroll to top */
.scroll-top {
  position: fixed; bottom: 30px; right: 30px; z-index: 50;
  width: 48px; height: 48px; border-radius: 50%;
  background: royalblue; color: white; border: none;
  font-size: 18px; cursor: pointer; transition: transform 0.2s, box-shadow 0.2s;
  box-shadow: 0 4px 16px rgba(65,105,225,0.4);
  display: flex; align-items: center; justify-content: center;
}
.scroll-top:hover { transform: translateY(-4px); box-shadow: 0 8px 24px rgba(65,105,225,0.5); }

/* Tugmalar */
.btn { padding: 12px 28px; background: royalblue; color: white; border: none;
       border-radius: 8px; cursor: pointer; font-size: 15px; font-weight: 600; }
.btn--ikkilamchi { background: #e2e8f0; color: #1a1a2e; }
```
