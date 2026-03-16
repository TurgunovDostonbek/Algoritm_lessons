# 15-Dars: CSS Grid

## 📌 CSS Grid nima?

**CSS Grid** — ikki o'lchovli layout tizimi (qator + ustun). Flexbox bir o'lchovli bo'lsa, Grid ikki o'lchovli.

```css
.konteyner {
  display: grid;        /* Gridni yoqish */
  display: inline-grid; /* Inline versiyasi */
}
```

---

## 📌 grid-template-columns va grid-template-rows

```css
.grid {
  display: grid;

  /* Ustunlar */
  grid-template-columns: 200px 300px 200px;    /* 3 ustun (px) */
  grid-template-columns: 1fr 2fr 1fr;           /* Kasr birlik */
  grid-template-columns: 33.33% 33.33% 33.33%;  /* Foiz */
  grid-template-columns: repeat(3, 1fr);         /* 3 teng ustun */
  grid-template-columns: repeat(4, 200px);       /* 4 × 200px */
  grid-template-columns: auto 1fr auto;          /* Avtomatik */
  grid-template-columns: minmax(150px, 1fr) 2fr; /* Min-Max */
  
  /* Auto-fill va auto-fit */
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));  /* Toldiradi */
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));   /* Kengaytiradi */

  /* Qatorlar */
  grid-template-rows: 100px 200px auto;
  grid-template-rows: repeat(3, 1fr);

  /* Bo'shliqlar */
  gap: 16px;
  row-gap: 12px;
  column-gap: 24px;
}
```

---

## 📌 Grid Lines — Element Joylashtirish

```css
.el {
  /* grid-column: boshlanish / tugash */
  grid-column: 1 / 3;       /* 1-chiziiqdan 3-chiziqqa = 2 ustun */
  grid-column: 1 / -1;      /* Birinchidan oxirigacha */
  grid-column: 2 / span 2;  /* 2-dan boshlab 2 ustun */

  /* grid-row: boshlanish / tugash */
  grid-row: 1 / 3;          /* 2 qator egallaydi */
  grid-row: auto;            /* Avtomatik */
}

/* Shorthand */
.el {
  grid-area: qator-boshlash / ustun-boshlash / qator-tugash / ustun-tugash;
  grid-area: 1 / 1 / 3 / 3; /* 2×2 joy egallaydi */
}
```

---

## 📌 grid-template-areas — Mintaqalar

```css
.layout {
  display: grid;
  grid-template-areas:
    "header header header"
    "sidebar kontent kontent"
    "footer footer footer";
  grid-template-columns: 200px 1fr 1fr;
  grid-template-rows: 80px 1fr 60px;
  min-height: 100vh;
}

header  { grid-area: header; }
.sidebar { grid-area: sidebar; }
main    { grid-area: kontent; }
footer  { grid-area: footer; }

/* Yopiq joy */
.el {
  grid-template-areas:
    "h h h"
    ". m m"   /* . = bo'sh */
    "f f f";
}
```

---

## 📌 align va justify (Grid uchun)

```css
/* Konteyner */
.grid {
  justify-items: start | end | center | stretch; /* Gorizontal (default: stretch) */
  align-items:   start | end | center | stretch; /* Vertikal   */
  place-items: center center; /* Ikkalasi */

  justify-content: start | end | center | stretch |
                   space-between | space-around | space-evenly;
  align-content: ...;
  place-content: center space-between;
}

/* Alohida element */
.el {
  justify-self: start | end | center | stretch;
  align-self:   start | end | center | stretch;
  place-self:   center end;
}
```

---

## 📌 Grid vs Flexbox

| Holat | Grid | Flexbox |
|-------|------|---------|
| 2 o'lchovli layoutlar | ✅ | ❌ |
| 1 o'lchovli (qator/ustun) | ❌ | ✅ |
| Kontent asosida | ❌ | ✅ |
| Layout asosida | ✅ | ❌ |
| Sahifa tuzilmasi | ✅ | ❌ |
| Navigatsiya, toolbar | ❌ | ✅ |

---

## 🎯 10 ta Amaliy Vazifa — Web Site Layouti

```html
<!DOCTYPE html>
<html lang="uz">
<head>
  <meta charset="UTF-8">
  <title>CSS Grid</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
  <link rel="stylesheet" href="grid.css">
</head>
<body>

<!-- Vazifa 1: Holy Grail Layout (grid-template-areas) -->
<div class="bosh-layout">
  <header class="layout-header">
    <h1>🎨 WebSite</h1>
    <nav><a href="#">Bosh</a><a href="#">Haqida</a><a href="#">Aloqa</a></nav>
  </header>
  <aside class="layout-sidebar">
    <h3>Kategoriyalar</h3>
    <ul>
      <li>HTML</li><li>CSS</li><li>JavaScript</li>
    </ul>
  </aside>
  <main class="layout-kontent">
    <h2>Asosiy Kontent</h2>

    <!-- Vazifa 2: Mahsulotlar grid -->
    <div class="mahsulot-grid">
      <div class="mahsulot-karta">
        <img src="https://picsum.photos/300/200?random=1" alt="">
        <div class="mahsulot-info">
          <h3>Mahsulot 1</h3><p>85,000 so'm</p>
        </div>
      </div>
      <div class="mahsulot-karta mahsulot-karta--featured">
        <img src="https://picsum.photos/300/200?random=2" alt="">
        <div class="mahsulot-info"><h3>Featured ★</h3><p>195,000 so'm</p></div>
      </div>
      <div class="mahsulot-karta">
        <img src="https://picsum.photos/300/200?random=3" alt="">
        <div class="mahsulot-info"><h3>Mahsulot 3</h3><p>65,000 so'm</p></div>
      </div>
      <div class="mahsulot-karta">
        <img src="https://picsum.photos/300/200?random=4" alt="">
        <div class="mahsulot-info"><h3>Mahsulot 4</h3><p>120,000 so'm</p></div>
      </div>
      <div class="mahsulot-karta">
        <img src="https://picsum.photos/300/200?random=5" alt="">
        <div class="mahsulot-info"><h3>Mahsulot 5</h3><p>48,000 so'm</p></div>
      </div>
    </div>

    <!-- Vazifa 3: Rasm galereya (masonry-like) -->
    <h2 style="margin:32px 0 16px">Galereya</h2>
    <div class="galereya-grid">
      <img src="https://picsum.photos/400/300?random=11" alt="">
      <img src="https://picsum.photos/400/300?random=12" alt="" class="katta">
      <img src="https://picsum.photos/400/300?random=13" alt="">
      <img src="https://picsum.photos/400/300?random=14" alt="">
      <img src="https://picsum.photos/400/300?random=15" alt="" class="keng">
    </div>

    <!-- Vazifa 4: Statistika grid -->
    <div class="statistika-grid">
      <div class="stat-kartа">
        <i class="fa-solid fa-users"></i>
        <strong>12,486</strong><span>Foydalanuvchilar</span>
      </div>
      <div class="stat-kartа">
        <i class="fa-solid fa-file"></i>
        <strong>3,842</strong><span>Maqolalar</span>
      </div>
      <div class="stat-kartа">
        <i class="fa-solid fa-star"></i>
        <strong>4.9</strong><span>Reyting</span>
      </div>
      <div class="stat-kartа">
        <i class="fa-solid fa-globe"></i>
        <strong>62</strong><span>Mamlakatlar</span>
      </div>
    </div>
  </main>
  <footer class="layout-footer">
    <p>&copy; 2024 WebSite. Barcha huquqlar himoyalangan.</p>
  </footer>
</div>

</body>
</html>
```

```css
/* grid.css */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
body { font-family: "Segoe UI", sans-serif; color: #1a1a2e; background: #f0f2f5; }

/* Vazifa 1: Holy Grail Grid Layout */
.bosh-layout {
  display: grid;
  grid-template-areas:
    "header  header  header"
    "sidebar kontent kontent"
    "footer  footer  footer";
  grid-template-columns: 220px 1fr;
  grid-template-rows: 64px 1fr 52px;
  min-height: 100vh;
}

.layout-header {
  grid-area: header;
  background: #16213e; color: white;
  display: flex; align-items: center; justify-content: space-between;
  padding: 0 32px; position: sticky; top: 0; z-index: 10;
  box-shadow: 0 2px 12px rgba(0,0,0,0.2);
}
.layout-header h1 { font-size: 20px; }
.layout-header nav { display: flex; gap: 24px; }
.layout-header a   { color: rgba(255,255,255,0.8); text-decoration: none; }
.layout-header a:hover { color: white; }

.layout-sidebar {
  grid-area: sidebar;
  background: white; padding: 24px;
  border-right: 1px solid #e0e0e0;
  position: sticky; top: 64px; height: calc(100vh - 64px);
  overflow-y: auto;
}
.layout-sidebar h3 { margin-bottom: 16px; font-size: 14px; text-transform: uppercase;
                     letter-spacing: 1px; color: #888; }
.layout-sidebar ul { list-style: none; }
.layout-sidebar li { padding: 10px 0; border-bottom: 1px solid #f5f5f5;
                     cursor: pointer; transition: color 0.2s; }
.layout-sidebar li:hover { color: royalblue; }

.layout-kontent { grid-area: kontent; padding: 32px; }
.layout-kontent > h2 { font-size: 24px; margin-bottom: 20px; }

.layout-footer {
  grid-area: footer;
  background: #16213e; color: rgba(255,255,255,0.7);
  display: flex; align-items: center; justify-content: center;
  font-size: 14px;
}

/* Vazifa 2: Mahsulotlar auto-fit grid */
.mahsulot-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 16px;
  margin-bottom: 40px;
}
.mahsulot-karta { background: white; border-radius: 12px; overflow: hidden;
                  transition: transform 0.3s; box-shadow: 0 4px 16px rgba(0,0,0,0.06); }
.mahsulot-karta:hover { transform: translateY(-4px); }
.mahsulot-karta--featured {
  grid-column: span 2;   /* 2 ustun egallaydi */
  background: linear-gradient(135deg, #16213e, #0f3460);
}
.mahsulot-karta--featured .mahsulot-info { color: white; }
.mahsulot-karta img { width: 100%; height: 160px; object-fit: cover; display: block; }
.mahsulot-karta--featured img { height: 200px; }
.mahsulot-info { padding: 14px; }
.mahsulot-info h3 { margin-bottom: 4px; font-size: 15px; }
.mahsulot-info p  { color: royalblue; font-weight: 700; }

/* Vazifa 3: Galereya (rasmlar turli o'lchamda) */
.galereya-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-auto-rows: 200px;
  gap: 12px;
  margin-bottom: 40px;
}
.galereya-grid img { width: 100%; height: 100%; object-fit: cover; border-radius: 10px;
                     transition: transform 0.3s; cursor: pointer; }
.galereya-grid img:hover { transform: scale(1.02); }
.galereya-grid .katta  { grid-row: span 2; }  /* 2 qator balandligi */
.galereya-grid .keng   { grid-column: span 2; } /* 2 ustun kengligi */

/* Vazifa 4: Statistika grid */
.statistika-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 16px;
}
.stat-kartа {
  background: white; padding: 24px; border-radius: 12px; text-align: center;
  box-shadow: 0 4px 16px rgba(0,0,0,0.06);
  display: flex; flex-direction: column; align-items: center; gap: 8px;
}
.stat-kartа i    { font-size: 28px; color: royalblue; }
.stat-kartа strong { font-size: 28px; font-weight: 700; }
.stat-kartа span { font-size: 13px; color: #888; }

/* Responsive */
@media (max-width: 768px) {
  .bosh-layout {
    grid-template-areas:
      "header"
      "kontent"
      "footer";
    grid-template-columns: 1fr;
  }
  .layout-sidebar { display: none; }
  .statistika-grid { grid-template-columns: repeat(2, 1fr); }
  .galereya-grid { grid-template-columns: repeat(2, 1fr); }
  .mahsulot-karta--featured { grid-column: span 1; }
}
```
