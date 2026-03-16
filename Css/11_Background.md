# 11-Dars: Background (Fon)

## 📌 background-color

```css
.el {
  background-color: royalblue;
  background-color: #4169e1;
  background-color: rgb(65, 105, 225);
  background-color: rgba(65, 105, 225, 0.8);  /* Alpha (shaffoflik) */
  background-color: hsl(225, 73%, 57%);
  background-color: transparent;               /* Shaffof */
}
```

---

## 📌 background-image va Styling Images

```css
.el {
  /* Rasm */
  background-image: url("rasm.jpg");
  background-image: url("https://picsum.photos/800/400");

  /* background-repeat */
  background-repeat: no-repeat;  /* Takrorlanmaydi */
  background-repeat: repeat;     /* Takrorlanadi (default) */
  background-repeat: repeat-x;   /* Faqat gorizontal */
  background-repeat: repeat-y;   /* Faqat vertikal */
  background-repeat: space;      /* Bo'sh joylar bilan */

  /* background-position */
  background-position: center;        /* Markazda */
  background-position: top right;     /* Yuqori o'ng */
  background-position: 50% 50%;       /* Foiz */
  background-position: 20px 40px;     /* px */

  /* background-size */
  background-size: cover;    /* Elementni to'liq qoplaydi (kesilishi mumkin) */
  background-size: contain;  /* Elementga sig'adi (bo'sh joy qolishi mumkin) */
  background-size: 300px 200px;  /* Aniq o'lcham */
  background-size: 50% auto;     /* Kenglik 50%, balandlik auto */
  background-size: 100%;

  /* background-attachment */
  background-attachment: scroll;    /* Element bilan birga aylanadi (default) */
  background-attachment: fixed;     /* Viewport ga oid — parallax effekti */
  background-attachment: local;
}
```

---

## 📌 Gradient — CSS Gradient

```css
/* linear-gradient — chiziqli */
.el {
  background: linear-gradient(to right, royalblue, purple);
  background: linear-gradient(45deg, #ff6b6b, #feca57);    /* Burchak */
  background: linear-gradient(to bottom, red, orange, yellow, green, blue);
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  
  /* Aniq nuqtalar bilan */
  background: linear-gradient(to right, red 0%, red 50%, blue 50%, blue 100%);
}

/* radial-gradient — doiraviy */
.el {
  background: radial-gradient(circle, royalblue, purple);
  background: radial-gradient(ellipse at center, #f5f7fa, #c3cfe2);
  background: radial-gradient(circle at top left, #ff9a9e, #fad0c4);
}

/* conic-gradient — konus */
.el {
  background: conic-gradient(red, yellow, green, blue, red);
  background: conic-gradient(from 0deg, #ff9a9e, #fecfef, #ff9a9e);
}

/* Repeating gradient */
.el {
  background: repeating-linear-gradient(
    45deg,
    #606dbc,
    #606dbc 10px,
    #465298 10px,
    #465298 20px
  );
}
```

---

## 📌 Multiple Backgrounds

```css
.el {
  background:
    url("ust-rasm.png") no-repeat center,  /* Birinchi — ustida */
    url("past-rasm.jpg") cover;             /* Ikkinchi — pastida */
  
  /* Gradient + rasm */
  background:
    linear-gradient(rgba(0,0,0,0.5), rgba(0,0,0,0.5)),
    url("rasm.jpg") no-repeat center/cover;
}
```

---

## 📌 background shorthand

```css
.el {
  background: rangi url("rasm") takrorlash pozitsiya/o'lcham biriktirilish;
  
  /* Misol */
  background: #fff url("logo.png") no-repeat center top / 80px auto scroll;
  
  /* Faqat rang */
  background: royalblue;
  
  /* Faqat gradient */
  background: linear-gradient(135deg, #667eea, #764ba2);
}
```

---

## 📌 CSS Filter

```css
.el {
  filter: none;                    /* Default */
  filter: blur(5px);               /* Xiralash */
  filter: brightness(0.8);        /* Yorqinlik (0–1 qoraytiradi) */
  filter: brightness(1.5);        /* Yorqinlik (>1 yorqinlashtiradi) */
  filter: contrast(200%);         /* Kontrast */
  filter: grayscale(100%);        /* Kulrang */
  filter: hue-rotate(90deg);      /* Rang aylantirish */
  filter: invert(100%);           /* Inverti */
  filter: opacity(50%);           /* Shaffoflik */
  filter: saturate(200%);         /* To'yinganlik */
  filter: sepia(100%);            /* Sepia */
  filter: drop-shadow(3px 3px 5px rgba(0,0,0,0.3)); /* Soya */

  /* Bir nechta */
  filter: brightness(1.2) contrast(110%) saturate(130%);
}

/* backdrop-filter — ortidagi elementga */
.frosted-glass {
  backdrop-filter: blur(10px);
  background: rgba(255,255,255,0.2);
}
```

---

## 📌 object-fit va object-position (Rasm uchun)

```css
/* img yoki video uchun */
img {
  width: 300px;
  height: 200px;

  object-fit: fill;      /* Default — cho'ziladi */
  object-fit: contain;   /* Sig'adi, nisbatni saqlaydi */
  object-fit: cover;     /* Qoplaydi, nisbatni saqlaydi (kesiladi) */
  object-fit: none;      /* O'z o'lchamida */
  object-fit: scale-down;/* contain yoki none, kichigi */

  object-position: center;     /* Qaysi qismini ko'rsatish */
  object-position: top;
  object-position: 20% 80%;
}
```

---

## 🎯 10 ta Amaliy Vazifa

```html
<!DOCTYPE html>
<html lang="uz">
<head>
  <meta charset="UTF-8">
  <title>Background Amaliyot</title>
  <link rel="stylesheet" href="background.css">
</head>
<body>

  <!-- Vazifa 1: Gradient hero -->
  <section class="hero">
    <h1>Gradient Fon</h1>
    <p>Linear gradient bilan yaratilgan</p>
  </section>

  <!-- Vazifa 2: Rasm fon -->
  <section class="rasm-fon">
    <div class="rasm-fon__kontent">
      <h2>Rasm Fon</h2>
      <p>Background image + overlay bilan</p>
    </div>
  </section>

  <!-- Vazifa 3: Kartalar grid -->
  <section class="kartalar-sektsiya">
    <div class="gradient-karta gradient-karta--atirgul">
      <h3>Atirgul</h3>
      <p>Linear gradient</p>
    </div>
    <div class="gradient-karta gradient-karta--okean">
      <h3>Okean</h3>
      <p>Radial gradient</p>
    </div>
    <div class="gradient-karta gradient-karta--quyosh">
      <h3>Quyosh</h3>
      <p>Conic gradient</p>
    </div>
    <div class="gradient-karta gradient-karta--o_rmon">
      <h3>O'rmon</h3>
      <p>Ko'p rang gradient</p>
    </div>
  </section>

  <!-- Vazifa 4: Rasmlar va object-fit -->
  <section class="rasmlar-sektsiya">
    <h2>object-fit Farqlari</h2>
    <div class="rasmlar-grid">
      <div class="rasm-quti">
        <img src="https://picsum.photos/600/400?random=1" alt="Cover" class="img-cover">
        <span>cover</span>
      </div>
      <div class="rasm-quti">
        <img src="https://picsum.photos/600/400?random=1" alt="Contain" class="img-contain">
        <span>contain</span>
      </div>
      <div class="rasm-quti">
        <img src="https://picsum.photos/600/400?random=1" alt="Fill" class="img-fill">
        <span>fill</span>
      </div>
    </div>
  </section>

  <!-- Vazifa 5-6: Filter effektlar galereya -->
  <section class="galereya-sektsiya">
    <h2>CSS Filter Effektlar</h2>
    <div class="galereya">
      <div class="galereya__element"><img src="https://picsum.photos/300/200?random=2" alt="">
        <span>Normal</span></div>
      <div class="galereya__element"><img src="https://picsum.photos/300/200?random=2" alt="" class="f-grayscale">
        <span>Grayscale</span></div>
      <div class="galereya__element"><img src="https://picsum.photos/300/200?random=2" alt="" class="f-blur">
        <span>Blur</span></div>
      <div class="galereya__element"><img src="https://picsum.photos/300/200?random=2" alt="" class="f-brightness">
        <span>Brightness</span></div>
      <div class="galereya__element"><img src="https://picsum.photos/300/200?random=2" alt="" class="f-sepia">
        <span>Sepia</span></div>
      <div class="galereya__element"><img src="https://picsum.photos/300/200?random=2" alt="" class="f-invert">
        <span>Invert</span></div>
    </div>
  </section>

  <!-- Vazifa 7: Parallax -->
  <section class="parallax">
    <div class="parallax__kontent">
      <h2>Parallax Effekti</h2>
      <p>background-attachment: fixed</p>
    </div>
  </section>

  <!-- Vazifa 8: Frosted glass -->
  <section class="glass-sektsiya">
    <div class="glass-karta">
      <h3>Frosted Glass</h3>
      <p>backdrop-filter: blur() effekti</p>
    </div>
  </section>

  <!-- Vazifa 9-10: Pattern backgrounds -->
  <section class="pattern-sektsiya">
    <div class="pattern-1"><h3>Pattern 1</h3></div>
    <div class="pattern-2"><h3>Pattern 2</h3></div>
  </section>

</body>
</html>
```

```css
/* background.css */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
body { font-family: "Segoe UI", sans-serif; }
section { padding: 80px 40px; }
h2 { font-size: 32px; margin-bottom: 32px; text-align: center; }
h3 { margin-bottom: 8px; }

/* Vazifa 1: Gradient hero */
.hero {
  min-height: 100vh; display: flex; flex-direction: column;
  align-items: center; justify-content: center; text-align: center;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
}
.hero h1 { font-size: clamp(40px, 8vw, 80px); margin-bottom: 16px; }
.hero p  { font-size: 20px; opacity: 0.9; }

/* Vazifa 2: Rasm fon + overlay */
.rasm-fon {
  min-height: 70vh; display: flex; align-items: center; justify-content: center;
  background: linear-gradient(rgba(0,0,0,0.6), rgba(0,0,0,0.6)),
              url("https://picsum.photos/1600/900?random=10") no-repeat center/cover;
  color: white; text-align: center;
}
.rasm-fon__kontent h2 { font-size: 48px; margin-bottom: 12px; }

/* Vazifa 3: Gradient kartalar */
.kartalar-sektsiya { background: #f8f9fa; display: flex; flex-wrap: wrap;
                     gap: 24px; justify-content: center; }
.gradient-karta {
  width: 280px; height: 180px; border-radius: 20px; display: flex;
  flex-direction: column; align-items: center; justify-content: center;
  color: white; font-size: 20px; cursor: pointer;
  transition: transform 0.3s; box-shadow: 0 8px 32px rgba(0,0,0,0.15);
}
.gradient-karta:hover { transform: scale(1.05) translateY(-4px); }
.gradient-karta--atirgul { background: linear-gradient(135deg, #f093fb, #f5576c); }
.gradient-karta--okean { background: radial-gradient(circle, #4facfe, #00f2fe); }
.gradient-karta--quyosh { background: conic-gradient(from 45deg, #fc5c7d, #6a82fb, #fc5c7d); }
.gradient-karta--o_rmon { background: linear-gradient(135deg, #43e97b 0%, #38f9d7 100%); }

/* Vazifa 4: object-fit */
.rasmlar-sektsiya { background: white; }
.rasmlar-grid { display: flex; gap: 24px; flex-wrap: wrap; justify-content: center; }
.rasm-quti { text-align: center; }
.rasm-quti img { width: 250px; height: 180px; border: 2px solid #ddd; border-radius: 8px; display: block; }
.rasm-quti span { font-size: 13px; color: #666; display: block; margin-top: 6px; font-family: monospace; }
.img-cover { object-fit: cover; }
.img-contain { object-fit: contain; background: #f0f0f0; }
.img-fill { object-fit: fill; }

/* Vazifa 5-6: Galereya filterlari */
.galereya-sektsiya { background: #1a1a2e; }
.galereya-sektsiya h2 { color: white; }
.galereya { display: grid; grid-template-columns: repeat(auto-fit, minmax(160px, 1fr)); gap: 16px; }
.galereya__element { text-align: center; }
.galereya__element img { width: 100%; height: 120px; object-fit: cover; border-radius: 8px; display: block; }
.galereya__element span { color: #aaa; font-size: 12px; display: block; margin-top: 6px; }
.f-grayscale  { filter: grayscale(100%); }
.f-blur       { filter: blur(3px); }
.f-brightness { filter: brightness(1.8) saturate(1.5); }
.f-sepia      { filter: sepia(100%); }
.f-invert     { filter: invert(100%); }

/* Vazifa 7: Parallax */
.parallax {
  min-height: 60vh; display: flex; align-items: center; justify-content: center;
  background: url("https://picsum.photos/1600/900?random=20") no-repeat center/cover;
  background-attachment: fixed;  /* ← Parallax effekti */
  color: white; text-align: center;
}
.parallax__kontent { background: rgba(0,0,0,0.5); padding: 40px 60px; border-radius: 16px; }
.parallax__kontent h2 { font-size: 40px; margin-bottom: 8px; }

/* Vazifa 8: Frosted glass */
.glass-sektsiya {
  display: flex; align-items: center; justify-content: center;
  background: linear-gradient(135deg, #667eea, #764ba2, #f093fb);
  min-height: 50vh;
}
.glass-karta {
  background: rgba(255,255,255,0.15);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  border: 1px solid rgba(255,255,255,0.3);
  border-radius: 20px; padding: 40px; color: white; text-align: center;
  box-shadow: 0 8px 32px rgba(31,38,135,0.37);
}

/* Vazifa 9-10: Pattern backgrounds */
.pattern-sektsiya { display: flex; gap: 0; padding: 0; }
.pattern-1, .pattern-2 {
  flex: 1; height: 300px; display: flex; align-items: center; justify-content: center;
}
.pattern-1 h3, .pattern-2 h3 { color: white; font-size: 24px; text-shadow: 1px 1px 4px rgba(0,0,0,0.5); }
.pattern-1 {
  background-color: #4facfe;
  background-image: repeating-linear-gradient(
    45deg, rgba(255,255,255,0.1) 0, rgba(255,255,255,0.1) 1px,
    transparent 0, transparent 50%
  );
  background-size: 20px 20px;
}
.pattern-2 {
  background-color: #764ba2;
  background-image: radial-gradient(circle, rgba(255,255,255,0.2) 1px, transparent 1px);
  background-size: 24px 24px;
}
```
