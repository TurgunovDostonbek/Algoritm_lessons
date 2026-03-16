# 04-Dars: Sizes va Display

## 📌 Width va Height

```css
/* Aniq o'lcham */
.el {
  width: 300px;
  height: 200px;
}

/* Foiz (ota elementga nisbatan) */
.el {
  width: 50%;     /* Ota elementning 50% i */
  height: 100%;   /* Ota elementning balandligi */
}

/* Auto */
.el {
  width: auto;    /* Default: to'liq kenglik (block uchun) */
  height: auto;   /* Default: kontent bo'yicha */
}

/* vh va vw (Viewport) */
.el {
  width: 100vw;   /* Viewport kengligining 100% */
  height: 100vh;  /* Viewport balandligining 100% */
  height: 50vh;   /* Viewport balandligining yarmi */
}

/* rem va em */
.el {
  font-size: 16px;    /* 1rem = 16px (default) */
  width: 10rem;       /* 10 × 16 = 160px */
  padding: 1em;       /* 1 × joriy element font-size */
}
```

---

## 📌 Min / Max o'lchamlar

```css
/* Min — eng kichik chegara */
.el {
  min-width: 200px;   /* 200px dan kichik bo'lmaydi */
  min-height: 100px;
}

/* Max — eng katta chegara */
.el {
  max-width: 800px;   /* 800px dan katta bo'lmaydi */
  max-height: 500px;
}

/* Responsivlik uchun klassik pattern */
.konteyner {
  width: 100%;        /* Kichik ekranda to'liq */
  max-width: 1200px;  /* Katta ekranda 1200px */
  margin: 0 auto;     /* Markazga */
}

/* Rasm responsiv */
img {
  width: 100%;
  max-width: 100%;
  height: auto;
}
```

---

## 📌 display Xossasi

```css
/* block — alohida qatordan, to'liq kenglikni egallaydi */
div, p, h1–h6, ul, li, section, article {
  display: block;
  /* → width, height, margin, padding ISHLAYDI */
}

/* inline — qator ichida, faqat kontent kengligi */
span, a, em, strong, img {
  display: inline;
  /* → width, height ISHLAMAYDI */
  /* → Vertikal margin ISHLAMAYDI */
}

/* inline-block — qator ichida, lekin width/height ISHLAYDI */
.tugma {
  display: inline-block;
  width: 120px;
  height: 40px;
  /* → width, height, margin, padding BARCHASI ISHLAYDI */
}

/* none — elementni to'liq yashirish */
.yashirin { display: none; }        /* Joy ham egollamaydi */
/* visibility: hidden → Joy egallaydi, lekin ko'rinmaydi */
.ko_rinmas { visibility: hidden; }

/* flex va grid */
.konteyner { display: flex; }
.grid-konteyner { display: grid; }
```

---

## 📌 Block vs Inline vs Inline-block

| Xususiyat     | `block`    | `inline`   | `inline-block` |
|---------------|------------|------------|----------------|
| Yangi qator   | ✅         | ❌         | ❌             |
| width/height  | ✅         | ❌         | ✅             |
| Yon margin    | ✅         | ✅         | ✅             |
| Vertikal margin| ✅        | ❌         | ✅             |
| Misollar      | div, p, h1 | span, a    | button, img    |

---

## 📌 Overflow

```css
.el {
  overflow: visible;  /* Default — tashqariga chiqadi */
  overflow: hidden;   /* Kesiladi */
  overflow: scroll;   /* Doim scrollbar */
  overflow: auto;     /* Kerak bo'lganda scrollbar */

  overflow-x: hidden; /* Gorizontal */
  overflow-y: auto;   /* Vertikal */
}

/* Matnni kesilgan ko'rsatish (...) */
.qisqa {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  max-width: 200px;
}
```

---

## 🎯 10 ta Amaliy Vazifa

```html
<!DOCTYPE html>
<html lang="uz">
<head><meta charset="UTF-8"><title>Sizes</title>
<link rel="stylesheet" href="sizes.css"></head>
<body>
  <div class="konteyner">
    <!-- Vazifa 1: Foiz width -->
    <div class="kenglik-demo">
      <div class="kenglik-50">50% kenglik</div>
      <div class="kenglik-100">100% kenglik</div>
    </div>

    <!-- Vazifa 2-4: Min/Max -->
    <div class="moslashuvchan">Moslashuvchan blok</div>

    <!-- Vazifa 5-6: Display turlari -->
    <div class="display-demo">
      <div class="block-el">Block</div>
      <span class="inline-el">Inline 1</span>
      <span class="inline-el">Inline 2</span>
      <span class="inline-block-el">Inline-block 1</span>
      <span class="inline-block-el">Inline-block 2</span>
    </div>

    <!-- Vazifa 7: Overflow -->
    <div class="overflow-demo">
      Bu juda uzun matn bo'lib, element ichiga sig'masligi mumkin agar element juda tor bo'lsa...
    </div>

    <!-- Vazifa 8: Viewport -->
    <section class="hero">
      <h1>Hero Sektsiya</h1>
      <p>100vh balandlik</p>
    </section>

    <!-- Vazifa 9-10: Responsive rasm grid -->
    <div class="rasm-grid">
      <img src="https://picsum.photos/300/200?random=1" alt="1">
      <img src="https://picsum.photos/300/200?random=2" alt="2">
      <img src="https://picsum.photos/300/200?random=3" alt="3">
    </div>
  </div>
</body>
</html>
```

```css
/* sizes.css */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
body { font-family: "Segoe UI", sans-serif; }

/* Vazifa 1: Konteyner max-width */
.konteyner {
  width: 100%;
  max-width: 1100px;
  margin: 0 auto;
  padding: 24px;
}

/* Vazifa 2: Foiz kengligi */
.kenglik-demo { margin-bottom: 20px; }
.kenglik-50 {
  width: 50%;
  background: royalblue;
  color: white;
  padding: 12px;
  text-align: center;
  border-radius: 6px;
  margin-bottom: 8px;
}
.kenglik-100 {
  width: 100%;
  background: navy;
  color: white;
  padding: 12px;
  text-align: center;
  border-radius: 6px;
}

/* Vazifa 3: Min-max */
.moslashuvchan {
  min-width: 200px;
  max-width: 600px;
  width: 60%;
  background: #f0f0ff;
  border: 2px solid royalblue;
  padding: 20px;
  border-radius: 8px;
  margin-bottom: 20px;
}

/* Vazifa 4: Display block */
.block-el {
  display: block;
  background: #ffe0e0;
  padding: 10px;
  margin-bottom: 4px;
}

/* Vazifa 5: Display inline */
.inline-el {
  display: inline;
  background: #e0ffe0;
  padding: 10px;  /* Vertikal padding vizual bor, lekin joy egollamaydi */
}

/* Vazifa 6: Display inline-block */
.inline-block-el {
  display: inline-block;
  width: 150px;
  height: 50px;
  background: #e0e0ff;
  text-align: center;
  line-height: 50px;
  margin: 4px;
  border-radius: 6px;
}

/* Vazifa 7: Overflow + ellipsis */
.overflow-demo {
  width: 300px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  background: #fff3cd;
  padding: 12px;
  border: 1px solid #ffc107;
  border-radius: 6px;
  margin: 16px 0;
}

/* Vazifa 8: Viewport units */
.hero {
  width: 100%;
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background: linear-gradient(135deg, royalblue, purple);
  color: white;
  text-align: center;
  margin: 20px 0;
}
.hero h1 { font-size: clamp(24px, 5vw, 64px); margin-bottom: 16px; }

/* Vazifa 9: Responsiv rasm grid */
.rasm-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 16px;
  margin-top: 20px;
}

/* Vazifa 10: Responsiv rasmlar */
.rasm-grid img {
  width: 100%;
  height: 200px;
  object-fit: cover;
  border-radius: 8px;
  transition: transform 0.3s;
}
.rasm-grid img:hover { transform: scale(1.03); }
```
