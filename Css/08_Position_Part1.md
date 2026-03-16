# 08-Dars: Position — 1-qism

## 📌 Position nima?

`position` xossasi elementning hujjatdagi joylashishini boshqaradi.

---
  
## 📌 position: static (Default)

```css
/* Barcha elementlar default holatda static */
.el {
  position: static;
  /* top, right, bottom, left ISHLAMAYDI! */
}
```

---

## 📌 position: relative

```css
/* O'zining normal joyiga nisbatan siljiydi */
.el {
  position: relative;
  top: 20px;    /* Pastga 20px */
  left: 10px;   /* O'ngga 10px */
  /* Eski joyi hali ham joy egollaydi! */
  /* z-index ISHLAYDI */
}
```

---

## 📌 position: absolute

```css
/* Eng yaqin positioned (non-static) ota elementiga nisbatan */
.ota {
  position: relative; /* ← Absolute uchun anchor */
}
.bola {
  position: absolute;
  top: 0;
  right: 0;
  /* Normal document flow dan chiqadi! */
  /* Positioned ota yo'q bo'lsa — viewport ga nisbatan */
}

/* Klassik pattern: Markazga joylashtirish */
.overlay {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
```

---

## 📌 position: fixed

```css
/* Viewport ga nisbatan, scroll da ham o'rnida turadi */
.yopishgan-navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;   /* yoki width: 100% */
  z-index: 1000;
}

.qaytish-tugmasi {
  position: fixed;
  bottom: 30px;
  right: 30px;
}

.cookie-bildirishnoma {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
}
```

---

## 📌 position: sticky

```css
/* Scroll qilganda ma'lum joyda "yopishib" qoladi */
.yopishgan-sarlavha {
  position: sticky;
  top: 0;    /* 0px dan past bo'lganda yopishadi */
  background: white;
  z-index: 10;
}

/* Table header uchun klassik ishlatilish */
th {
  position: sticky;
  top: 0;
  background: #f5f5f5;
}
```

---

## 📌 top, right, bottom, left

```css
/* Bu xossalar faqat positioned (non-static) elementlarda ishlaydi */
.el {
  position: absolute;
  top: 20px;     /* Yuqori chegara dan 20px uzoqlik */
  right: 0;      /* O'ng chegaraga yopishtirilgan */
  bottom: auto;  /* Avtomatik */
  left: 50%;     /* Chap chegaradan 50% */
}

/* inset — shorthand (top right bottom left) */
.el {
  inset: 0;                /* Hamma tomondan 0 */
  inset: 10px 20px;        /* T/B | L/R */
  inset: 10px 20px 30px 40px; /* T R B L */
}
```

---

## 🎯 10 ta Amaliy Vazifa — CSS Battle

```html
<!DOCTYPE html>
<html lang="uz">
<head>
  <meta charset="UTF-8">
  <title>Position</title>
  <link rel="stylesheet" href="position.css">
</head>
<body>

  <!-- Vazifa 1: Yopishgan navbar -->
  <header class="navbar-fixed">
    <span>🎨 Logo</span>
    <nav><a href="#">Bosh</a><a href="#">Xizmat</a><a href="#">Haqida</a></nav>
  </header>

  <div class="content">

    <!-- Vazifa 2: Relative + Absolute — badge (yorliq) bilan karta -->
    <div class="karta-badge">
      <img src="https://picsum.photos/300/200" alt="Rasm">
      <span class="badge badge--yangi">Yangi</span>
      <span class="badge badge--chegirma">-30%</span>
    </div>

    <!-- Vazifa 3: Absolute overlay — hover da ko'rinadigan -->
    <div class="hover-karta">
      <img src="https://picsum.photos/300/200?random=2" alt="Rasm">
      <div class="hover-karta__overlay">
        <h3>Mahsulot nomi</h3>
        <button>Ko'rish</button>
      </div>
    </div>

    <!-- Vazifa 4: Absolute bilan markazga joylash -->
    <div class="nisbiy-quti">
      <div class="markaz">Markazda!</div>
    </div>

    <!-- Vazifa 5: Sticky jadval sarlavhasi -->
    <div class="jadval-wrapper">
      <table>
        <thead>
          <tr><th>ID</th><th>Ism</th><th>Ball</th></tr>
        </thead>
        <tbody>
          <tr><td>1</td><td>Ali</td><td>95</td></tr>
          <tr><td>2</td><td>Vali</td><td>88</td></tr>
          <tr><td>3</td><td>Gani</td><td>76</td></tr>
          <tr><td>4</td><td>Sani</td><td>91</td></tr>
          <tr><td>5</td><td>Beka</td><td>84</td></tr>
        </tbody>
      </table>
    </div>

    <!-- Vazifa 6-8: Progress bar (relative + absolute) -->
    <div class="progress-bar">
      <div class="progress-bar__to'ldirish" style="width: 72%;">
        <span class="progress-bar__label">72%</span>
      </div>
    </div>

    <!-- Vazifa 9: Tooltip -->
    <div class="tooltip-wrapper">
      <button class="tooltip-trigger">
        Ustiga suring ℹ️
        <span class="tooltip">Bu maxsus ma'lumot!</span>
      </button>
    </div>

  </div>

  <!-- Vazifa 10: Fixed scroll-to-top tugmasi -->
  <button class="ortga-tugma" onclick="window.scrollTo({top:0,behavior:'smooth'})">↑</button>

</body>
</html>
```

```css
/* position.css */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
body { font-family: "Segoe UI", sans-serif; background: #f5f5f5; }

/* Vazifa 1: Fixed navbar */
.navbar-fixed {
  position: fixed;
  top: 0; left: 0; right: 0;
  height: 60px;
  background: #16213e;
  color: white;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 32px;
  z-index: 1000;
  box-shadow: 0 2px 12px rgba(0,0,0,0.2);
}
.navbar-fixed nav { display: flex; gap: 20px; }
.navbar-fixed a { color: rgba(255,255,255,0.8); text-decoration: none; }

.content {
  max-width: 900px;
  margin: 80px auto 0;
  padding: 24px;
  display: flex;
  flex-wrap: wrap;
  gap: 24px;
  align-items: flex-start;
}

/* Vazifa 2: Badge bilan karta */
.karta-badge {
  position: relative;  /* ← anchor */
  width: 300px;
  border-radius: 12px;
  overflow: hidden;
  box-shadow: 0 4px 20px rgba(0,0,0,0.1);
}
.karta-badge img { width: 100%; display: block; }
.badge {
  position: absolute;
  padding: 6px 12px;
  border-radius: 20px;
  font-size: 12px;
  font-weight: 700;
  color: white;
}
.badge--yangi  { top: 12px; left: 12px; background: royalblue; }
.badge--chegirma { top: 12px; right: 12px; background: #fc5c65; }

/* Vazifa 3: Hover overlay */
.hover-karta {
  position: relative;
  width: 300px;
  border-radius: 12px;
  overflow: hidden;
}
.hover-karta img { width: 100%; display: block; }
.hover-karta__overlay {
  position: absolute;
  inset: 0;
  background: rgba(22, 33, 62, 0.85);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 12px;
  color: white;
  opacity: 0;
  transition: opacity 0.3s;
}
.hover-karta:hover .hover-karta__overlay { opacity: 1; }
.hover-karta__overlay button {
  padding: 8px 20px; background: royalblue;
  border: none; color: white; border-radius: 6px; cursor: pointer;
}

/* Vazifa 4: Markazlash (relative + absolute + transform) */
.nisbiy-quti {
  position: relative;
  width: 300px;
  height: 200px;
  background: white;
  border-radius: 12px;
  box-shadow: 0 4px 20px rgba(0,0,0,0.08);
}
.markaz {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background: royalblue;
  color: white;
  padding: 12px 24px;
  border-radius: 8px;
  white-space: nowrap;
}

/* Vazifa 5: Sticky table header */
.jadval-wrapper {
  width: 100%;
  max-height: 200px;
  overflow-y: auto;
  border-radius: 12px;
  box-shadow: 0 4px 20px rgba(0,0,0,0.08);
}
table { width: 100%; border-collapse: collapse; background: white; }
th {
  position: sticky;
  top: 0;
  background: #16213e;
  color: white;
  padding: 12px;
  text-align: left;
}
td { padding: 12px; border-bottom: 1px solid #f0f0f0; }

/* Vazifa 6-8: Progress bar */
.progress-bar {
  width: 100%;
  height: 32px;
  background: #e0e0e0;
  border-radius: 16px;
  overflow: hidden;
  position: relative;
}
.progress-bar__to'ldirish {
  position: relative;
  height: 100%;
  background: linear-gradient(90deg, royalblue, #6a93ff);
  border-radius: 16px;
  transition: width 0.5s ease;
}
.progress-bar__label {
  position: absolute;
  right: 12px;
  top: 50%;
  transform: translateY(-50%);
  color: white;
  font-size: 13px;
  font-weight: 700;
}

/* Vazifa 9: Tooltip */
.tooltip-wrapper { position: relative; display: inline-block; }
.tooltip-trigger {
  padding: 10px 20px; background: #f0f0ff;
  border: 1px solid #c0c0ff; border-radius: 8px; cursor: pointer;
  position: relative;
}
.tooltip {
  position: absolute;
  bottom: calc(100% + 8px);
  left: 50%;
  transform: translateX(-50%);
  background: #16213e;
  color: white;
  padding: 8px 14px;
  border-radius: 6px;
  font-size: 13px;
  white-space: nowrap;
  opacity: 0;
  pointer-events: none;
  transition: opacity 0.2s;
}
.tooltip::after {
  content: "";
  position: absolute;
  top: 100%; left: 50%;
  transform: translateX(-50%);
  border: 6px solid transparent;
  border-top-color: #16213e;
}
.tooltip-trigger:hover .tooltip { opacity: 1; }

/* Vazifa 10: Fixed scroll-to-top */
.ortga-tugma {
  position: fixed;
  bottom: 30px; right: 30px;
  width: 50px; height: 50px;
  border-radius: 50%;
  background: royalblue;
  color: white;
  border: none;
  font-size: 20px;
  cursor: pointer;
  box-shadow: 0 4px 16px rgba(65,105,225,0.4);
  transition: transform 0.2s;
}
.ortga-tugma:hover { transform: scale(1.1) translateY(-2px); }
```
