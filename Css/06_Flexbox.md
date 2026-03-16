# 06-Dars: Flexbox

## 📌 Flexbox nima?

**Flexbox (Flexible Box Layout)** — bir o'lchovli layout tizimi. Elementlarni qator yoki ustun bo'yicha joylashtirishga yordam beradi.

```css
/* Ota element (Flex Container) */
.konteyner { display: flex; }

/* Bola elementlar (Flex Items) */
.el { flex: 1; }
```

---

## 📌 Flex Container Xossalari

```css
.konteyner {
  display: flex;           /* Flexni yoqish */

  /* flex-direction — elementlar yo'nalishi */
  flex-direction: row;            /* → Gorizontal (default) */
  flex-direction: row-reverse;    /* ← */
  flex-direction: column;         /* ↓ Vertikal */
  flex-direction: column-reverse; /* ↑ */

  /* flex-wrap — qatorga sig'masa */
  flex-wrap: nowrap;   /* Sig'masa ham bitta qatorda (default) */
  flex-wrap: wrap;     /* Yangi qatorga tushadi */
  flex-wrap: wrap-reverse;

  /* justify-content — bosh o'q bo'yicha hizalash */
  justify-content: flex-start;    /* |●●●    | Chapga */
  justify-content: flex-end;      /* |    ●●●| O'ngga */
  justify-content: center;        /* |  ●●●  | Markazga */
  justify-content: space-between; /* |●  ●  ●| Ikki cheta */
  justify-content: space-around;  /* | ● ● ● | Atrofida */
  justify-content: space-evenly;  /* |●●●●●●●| Teng bo'sh */

  /* align-items — ko'ndalang o'q bo'yicha */
  align-items: stretch;     /* To'liq balandlik (default) */
  align-items: flex-start;  /* Yuqoriga */
  align-items: flex-end;    /* Pastga */
  align-items: center;      /* Markazga ← Eng ko'p ishlatiladi */
  align-items: baseline;    /* Matn chizig'i bo'yicha */

  /* gap */
  gap: 16px;            /* Har tomondan */
  gap: 12px 24px;       /* satr | ustun */
  row-gap: 12px;
  column-gap: 24px;
}
```

---

## 📌 Flex Item Xossalari

```css
.el {
  /* flex-grow — bo'sh joyni qancha olsin (0 = olmaydi) */
  flex-grow: 0;   /* Default — kengaymaydi */
  flex-grow: 1;   /* Bo'sh joyni oladi */
  flex-grow: 2;   /* 2 marta ko'p */

  /* flex-shrink — joy yetishmasa qanchaga qisqarsin */
  flex-shrink: 1;   /* Default — qisqaradi */
  flex-shrink: 0;   /* Qisqarmaslik */

  /* flex-basis — boshlang'ich kenglik */
  flex-basis: auto;   /* Kontent bo'yicha (default) */
  flex-basis: 200px;  /* Aniq */
  flex-basis: 30%;    /* Foiz */

  /* flex — shorthand (grow shrink basis) */
  flex: 0 1 auto;  /* Default */
  flex: 1;         /* flex: 1 1 0 */
  flex: auto;      /* flex: 1 1 auto */
  flex: none;      /* flex: 0 0 auto */

  /* align-self — faqat shu element uchun */
  align-self: auto;       /* Ota elementdan oladi */
  align-self: flex-start;
  align-self: flex-end;
  align-self: center;
  align-self: stretch;

  /* order — tartibni o'zgartirish */
  order: 0;   /* Default */
  order: -1;  /* Birinchiga */
  order: 1;   /* Keyingiga */
}
```

---

## 📌 Klassik Flexbox Patterns

```css
/* 1. Perfect centering — eng oson usul */
.markazlash {
  display: flex;
  justify-content: center;
  align-items: center;
}

/* 2. Space-between navbar */
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 20px;
}

/* 3. Equal-width columns */
.ustunlar {
  display: flex;
  gap: 20px;
}
.ustunlar .ustun { flex: 1; }

/* 4. Sidebar + content */
.layout {
  display: flex;
}
.sidebar { flex: 0 0 250px; }   /* Kenglik 250px, o'zgarmaydi */
.kontent { flex: 1; }            /* Qolgan joy */

/* 5. Holy Grail Layout */
body { display: flex; flex-direction: column; min-height: 100vh; }
main { display: flex; flex: 1; }
.kontent { flex: 1; }
.sidebar { flex: 0 0 200px; }
footer { margin-top: auto; }
```

---

## 🎯 10 ta Amaliy Vazifa

```html
<!DOCTYPE html>
<html lang="uz">
<head>
  <meta charset="UTF-8">
  <title>Flexbox</title>
  <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
  <link rel="stylesheet" href="flex.css">
</head>
<body>

<!-- Vazifa 1: Navbar -->
<nav class="navbar">
  <div class="navbar__logo">🎨 BrandLogo</div>
  <ul class="navbar__menu">
    <li><a href="#">Bosh sahifa</a></li>
    <li><a href="#">Xizmatlar</a></li>
    <li><a href="#">Haqida</a></li>
  </ul>
  <button class="navbar__btn">Bog'lanish</button>
</nav>

<!-- Vazifa 2: Hero (Markazlashtirish) -->
<section class="hero">
  <h1>CSS Flexbox</h1>
  <p>Saytlarni chiroyli joylashtirishning eng oson usuli</p>
  <div class="hero__tugmalar">
    <button class="btn btn--asosiy">Boshlash</button>
    <button class="btn btn--ikkilamchi">Ko'proq</button>
  </div>
</section>

<!-- Vazifa 3: Xizmatlar kartalar -->
<section class="xizmatlar">
  <h2>Xizmatlar</h2>
  <div class="xizmat-grid">
    <div class="xizmat-karta">
      <i class="fa-solid fa-code"></i>
      <h3>Frontend</h3>
      <p>HTML, CSS, JavaScript</p>
    </div>
    <div class="xizmat-karta">
      <i class="fa-solid fa-database"></i>
      <h3>Backend</h3>
      <p>Node.js, Python</p>
    </div>
    <div class="xizmat-karta">
      <i class="fa-solid fa-mobile-screen"></i>
      <h3>Mobile</h3>
      <p>React Native</p>
    </div>
    <div class="xizmat-karta">
      <i class="fa-solid fa-palette"></i>
      <h3>Dizayn</h3>
      <p>Figma, Adobe XD</p>
    </div>
  </div>
</section>

<!-- Vazifa 4: Sidebar layout -->
<div class="sidebar-layout">
  <aside class="sidebar">
    <h3>Kategoriyalar</h3>
    <ul>
      <li>HTML</li><li>CSS</li><li>JavaScript</li>
    </ul>
  </aside>
  <main class="kontent">
    <article>
      <h2>Maqola sarlavhasi</h2>
      <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
    </article>
  </main>
</div>

<!-- Vazifa 5: Oyoq qism -->
<footer class="footer">
  <p>&copy; 2024 BrandLogo</p>
  <div class="footer__links">
    <a href="#">Maxfiylik</a>
    <a href="#">Shartlar</a>
    <a href="#">Yordam</a>
  </div>
</footer>

</body>
</html>
```

```css
/* flex.css */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
body { font-family: "Inter", sans-serif; color: #1a1a2e; background: #f8f9fa; }

/* Vazifa 1: Navbar */
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 32px;
  height: 64px;
  background: #16213e;
  color: white;
  position: sticky;
  top: 0;
  z-index: 100;
}
.navbar__logo { font-size: 20px; font-weight: 700; }
.navbar__menu {
  display: flex;
  list-style: none;
  gap: 24px;
}
.navbar__menu a { color: rgba(255,255,255,0.8); text-decoration: none; transition: color 0.2s; }
.navbar__menu a:hover { color: white; }
.navbar__btn { background: royalblue; color: white; border: none; padding: 8px 20px;
               border-radius: 6px; cursor: pointer; font-weight: 600; }

/* Vazifa 2: Hero — perfect centering */
.hero {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
  min-height: 80vh;
  background: linear-gradient(135deg, #16213e, #0f3460);
  color: white;
  padding: 40px 20px;
}
.hero h1 { font-size: clamp(36px, 6vw, 72px); margin-bottom: 16px; }
.hero p { font-size: 18px; opacity: 0.8; max-width: 500px; margin-bottom: 32px; }
.hero__tugmalar { display: flex; gap: 12px; flex-wrap: wrap; justify-content: center; }

/* Vazifa 3: Xizmatlar grid */
.xizmatlar { padding: 60px 32px; max-width: 1100px; margin: 0 auto; }
.xizmatlar h2 { text-align: center; font-size: 32px; margin-bottom: 36px; }
.xizmat-grid {
  display: flex;
  gap: 20px;
  flex-wrap: wrap;
}
.xizmat-karta {
  flex: 1 1 200px;   /* min 200px, kengayadi */
  background: white;
  padding: 32px 24px;
  text-align: center;
  border-radius: 16px;
  box-shadow: 0 4px 20px rgba(0,0,0,0.06);
  transition: transform 0.3s;
}
.xizmat-karta:hover { transform: translateY(-6px); }
.xizmat-karta i { font-size: 40px; color: royalblue; margin-bottom: 16px; }
.xizmat-karta h3 { margin-bottom: 8px; }
.xizmat-karta p { color: #666; font-size: 14px; }

/* Vazifa 4: Sidebar layout */
.sidebar-layout {
  display: flex;
  gap: 24px;
  max-width: 1100px;
  margin: 0 auto;
  padding: 40px 32px;
}
.sidebar {
  flex: 0 0 240px;
  background: white;
  padding: 24px;
  border-radius: 12px;
  height: fit-content;
}
.sidebar h3 { margin-bottom: 12px; }
.sidebar ul { list-style: none; }
.sidebar li { padding: 8px 0; border-bottom: 1px solid #eee; cursor: pointer; }
.sidebar li:hover { color: royalblue; }
.kontent { flex: 1; background: white; padding: 32px; border-radius: 12px; }
.kontent h2 { margin-bottom: 12px; }

/* Vazifa 5: Footer */
.footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px 32px;
  background: #16213e;
  color: rgba(255,255,255,0.7);
}
.footer__links { display: flex; gap: 20px; }
.footer__links a { color: rgba(255,255,255,0.7); text-decoration: none; }
.footer__links a:hover { color: white; }

/* Umumiy tugmalar */
.btn { padding: 12px 28px; border: none; border-radius: 8px;
       font-size: 16px; font-weight: 600; cursor: pointer; }
.btn--asosiy { background: royalblue; color: white; }
.btn--ikkilamchi { background: rgba(255,255,255,0.15); color: white;
                   border: 1px solid rgba(255,255,255,0.3); backdrop-filter: blur(4px); }
```
