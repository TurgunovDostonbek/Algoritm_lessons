# 14-Dars: CSS Animation (Animatsiyalar)

## 📌 @keyframes — Animatsiya Kadrlari

```css
/* Sintaksis */
@keyframes animatsiya_nomi {
  from { /* Boshlang'ich holat */ }
  to   { /* Oxirgi holat */ }
}

/* Yoki foizlar bilan */
@keyframes animatsiya_nomi {
  0%   { /* Boshlanishi */ }
  50%  { /* Yarim yo'lda */ }
  100% { /* Tugashi */ }
}

/* Misol */
@keyframes siljish {
  from { transform: translateX(0); }
  to   { transform: translateX(200px); }
}

@keyframes rang_o'zgarish {
  0%   { background: red; }
  33%  { background: green; }
  66%  { background: blue; }
  100% { background: red; }
}
```

---

## 📌 animation Xossalari

```css
.el {
  /* animation-name */
  animation-name: siljish;

  /* animation-duration */
  animation-duration: 2s;
  animation-duration: 500ms;

  /* animation-timing-function */
  animation-timing-function: linear;
  animation-timing-function: ease;
  animation-timing-function: ease-in;
  animation-timing-function: ease-out;
  animation-timing-function: ease-in-out;
  animation-timing-function: steps(5);         /* Bosqichma-bosqich */
  animation-timing-function: cubic-bezier(0.68, -0.55, 0.265, 1.55);

  /* animation-delay */
  animation-delay: 1s;      /* 1 soniyadan keyin boshlanadi */
  animation-delay: -1s;     /* 1 soniya oldin boshlangandek */

  /* animation-iteration-count */
  animation-iteration-count: 1;         /* Bir marta */
  animation-iteration-count: 3;         /* 3 marta */
  animation-iteration-count: infinite;  /* Cheksiz */

  /* animation-direction */
  animation-direction: normal;           /* → Default */
  animation-direction: reverse;          /* ← Teskari */
  animation-direction: alternate;        /* → ← Alo-nav */
  animation-direction: alternate-reverse;/* ← → Teskari alo-nav */

  /* animation-fill-mode */
  animation-fill-mode: none;        /* Default — qaytib ketadi */
  animation-fill-mode: forwards;    /* Oxirgi holatda qoladi */
  animation-fill-mode: backwards;   /* Boshlang'ich holatdan boshlanadi */
  animation-fill-mode: both;        /* Ikkisi ham */

  /* animation-play-state */
  animation-play-state: running; /* Ishlaydi */
  animation-play-state: paused;  /* To'xtaydi */
}

/* Shorthand */
.el {
  animation: nomi davomiylik timing takrorlash kechikish yo'nalish fill-mode;
  animation: siljish 2s ease infinite 0.5s alternate forwards;
}

/* Bir nechta animatsiya */
.el {
  animation: siljish 2s ease, rang 3s linear infinite;
}
```

---

## 📌 Klassik Animatsiyalar

```css
/* 1. Fade In */
@keyframes fadeIn {
  from { opacity: 0; }
  to   { opacity: 1; }
}
.fade-in { animation: fadeIn 0.5s ease forwards; }

/* 2. Fade In Up */
@keyframes fadeInUp {
  from { opacity: 0; transform: translateY(30px); }
  to   { opacity: 1; transform: translateY(0); }
}
.fade-in-up { animation: fadeInUp 0.6s ease forwards; }

/* 3. Pulse (yurak urishi) */
@keyframes pulse {
  0%, 100% { transform: scale(1); }
  50%       { transform: scale(1.08); }
}
.pulse { animation: pulse 1.5s ease-in-out infinite; }

/* 4. Spin (aylantirish) */
@keyframes spin {
  to { transform: rotate(360deg); }
}
.spinner { animation: spin 1s linear infinite; }

/* 5. Bounce */
@keyframes bounce {
  0%, 100% { transform: translateY(0); animation-timing-function: ease-out; }
  50%       { transform: translateY(-20px); animation-timing-function: ease-in; }
}
.bounce { animation: bounce 0.8s infinite; }

/* 6. Shimmer (yuklanish skelet) */
@keyframes shimmer {
  from { background-position: -200px 0; }
  to   { background-position: 200px 0; }
}
.skeleton {
  background: linear-gradient(90deg, #f0f0f0 25%, #e0e0e0 50%, #f0f0f0 75%);
  background-size: 400px 100%;
  animation: shimmer 1.5s infinite linear;
}
```

---

## 📌 animation-play-state bilan To'xtatish

```css
.animatsiya-qutisi {
  animation: spin 2s linear infinite;
}
.animatsiya-qutisi:hover {
  animation-play-state: paused; /* Hover da to'xtaydi */
}
```

---

## 🎯 10 ta Amaliy Vazifa — Loading sahifasi

```html
<!DOCTYPE html>
<html lang="uz">
<head>
  <meta charset="UTF-8">
  <title>CSS Animatsiya</title>
  <link rel="stylesheet" href="animation.css">
</head>
<body>

  <!-- Vazifa 1: Spinner yuklash animatsiyasi -->
  <div class="loader-wrapper">
    <div class="spinner"></div>
    <div class="spinner spinner--ikkilamchi"></div>
    <p class="loader-matn">Yuklanmoqda...</p>
  </div>

  <!-- Vazifa 2: Skeleton loading -->
  <div class="kontent-sahifa">
    <div class="skelet-karta">
      <div class="skelet-avatar"></div>
      <div class="skelet-matn">
        <div class="skelet-qator"></div>
        <div class="skelet-qator skelet-qator--qisqa"></div>
        <div class="skelet-qator"></div>
      </div>
    </div>

    <!-- Vazifa 3: Animatsiyali kartalar -->
    <div class="animatsion-kartalar">
      <div class="anim-karta" style="--kechikish: 0s">
        <span class="karta-emoji">🚀</span>
        <h3>Birinchi</h3>
      </div>
      <div class="anim-karta" style="--kechikish: 0.15s">
        <span class="karta-emoji">⚡</span>
        <h3>Ikkinchi</h3>
      </div>
      <div class="anim-karta" style="--kechikish: 0.3s">
        <span class="karta-emoji">🎨</span>
        <h3>Uchinchi</h3>
      </div>
    </div>

    <!-- Vazifa 4: Pulsating CTA -->
    <div class="cta-sektsiya">
      <button class="cta-tugma">
        <span class="cta-halqa"></span>
        Bosing!
      </button>
    </div>

    <!-- Vazifa 5-6: Progress bar animatsiya -->
    <div class="progress-sektsiya">
      <h3>Mening Ko'nikmalarim</h3>
      <div class="ko'nikma">
        <span>HTML</span>
        <div class="progress"><div class="progress__to'ldirish" style="--daraja: 95%"></div></div>
        <span>95%</span>
      </div>
      <div class="ko'nikma">
        <span>CSS</span>
        <div class="progress"><div class="progress__to'ldirish" style="--daraja: 88%"></div></div>
        <span>88%</span>
      </div>
      <div class="ko'nikma">
        <span>JS</span>
        <div class="progress"><div class="progress__to'ldirish" style="--daraja: 75%"></div></div>
        <span>75%</span>
      </div>
    </div>

    <!-- Vazifa 7: Bouncing dots -->
    <div class="typing-indikator">
      <div class="dot"></div>
      <div class="dot"></div>
      <div class="dot"></div>
    </div>

    <!-- Vazifa 8: Notification animatsiya -->
    <div class="notification">
      <span>✅</span> Muvaffaqiyatli yuborildi!
    </div>

    <!-- Vazifa 9-10: Gradient animatsiya -->
    <section class="gradient-anim-sektsiya">
      <h2>Gradient Animatsiya</h2>
      <p>background-size + animation bilan</p>
    </section>
  </div>

</body>
</html>
```

```css
/* animation.css */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
body { font-family: "Segoe UI", sans-serif; background: #f0f2f5; color: #1a1a2e; }

/* === KEYFRAMES === */
@keyframes spin           { to { transform: rotate(360deg); } }
@keyframes fadeInUp       { from { opacity: 0; transform: translateY(30px); } to { opacity: 1; transform: translateY(0); } }
@keyframes shimmer        { from { background-position: -400px 0; } to { background-position: 400px 0; } }
@keyframes pulse          { 0%,100% { transform: scale(1); } 50% { transform: scale(1.06); } }
@keyframes bounce         { 0%,80%,100% { transform: translateY(0); } 40% { transform: translateY(-10px); } }
@keyframes progressFill   { from { width: 0; } to { width: var(--daraja); } }
@keyframes slideIn        { from { opacity: 0; transform: translateX(100px); } to { opacity: 1; transform: translateX(0); } }
@keyframes gradientShift  {
  0%   { background-position: 0% 50%; }
  50%  { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}
@keyframes ringPulse { 0% { transform: scale(1); opacity: 0.7; } 100% { transform: scale(2); opacity: 0; } }

/* Vazifa 1: Spinner */
.loader-wrapper {
  display: flex; flex-direction: column; align-items: center;
  justify-content: center; gap: 16px; padding: 60px;
  position: relative;
}
.spinner {
  width: 60px; height: 60px; border-radius: 50%;
  border: 4px solid #e0e0e0;
  border-top-color: royalblue;
  animation: spin 0.8s linear infinite;
}
.spinner--ikkilamchi {
  width: 40px; height: 40px;
  border-top-color: #764ba2;
  animation-duration: 0.6s;
  animation-direction: reverse;
  position: absolute; top: 70px;
}
.loader-matn { color: #666; font-size: 14px; }

/* Vazifa 2: Skeleton */
.kontent-sahifa { max-width: 900px; margin: 0 auto; padding: 20px; }
.skelet-karta {
  display: flex; gap: 16px; background: white; padding: 24px;
  border-radius: 16px; margin-bottom: 24px;
  box-shadow: 0 4px 20px rgba(0,0,0,0.05);
}
.skeleton-bg {
  background: linear-gradient(90deg, #f0f0f0 25%, #e8e8e8 50%, #f0f0f0 75%);
  background-size: 800px 100%;
  animation: shimmer 1.5s infinite linear;
}
.skelet-avatar {
  width: 60px; height: 60px; border-radius: 50%; flex-shrink: 0;
  background: linear-gradient(90deg, #f0f0f0 25%, #e8e8e8 50%, #f0f0f0 75%);
  background-size: 800px 100%;
  animation: shimmer 1.5s infinite linear;
}
.skelet-matn { flex: 1; display: flex; flex-direction: column; gap: 10px; }
.skelet-qator {
  height: 16px; border-radius: 8px;
  background: linear-gradient(90deg, #f0f0f0 25%, #e8e8e8 50%, #f0f0f0 75%);
  background-size: 800px 100%;
  animation: shimmer 1.5s infinite linear;
}
.skelet-qator--qisqa { width: 50%; }

/* Vazifa 3: Animatsion kartalar (CSS custom property bilan kechikish) */
.animatsion-kartalar { display: flex; gap: 16px; margin-bottom: 32px; flex-wrap: wrap; }
.anim-karta {
  flex: 1; min-width: 160px; background: white; padding: 28px; border-radius: 16px;
  text-align: center; opacity: 0;
  animation: fadeInUp 0.6s ease var(--kechikish, 0s) forwards;
  box-shadow: 0 4px 20px rgba(0,0,0,0.06);
}
.karta-emoji { font-size: 40px; display: block; margin-bottom: 12px; }
.anim-karta:hover .karta-emoji { animation: bounce 0.6s ease; }

/* Vazifa 4: Pulsating button */
.cta-sektsiya { text-align: center; margin: 32px 0; }
.cta-tugma {
  position: relative; padding: 16px 40px; background: royalblue; color: white;
  border: none; border-radius: 50px; font-size: 18px; font-weight: 700; cursor: pointer;
}
.cta-halqa {
  position: absolute; inset: 0; border-radius: 50px;
  background: royalblue;
  animation: ringPulse 1.5s ease-out infinite;
}

/* Vazifa 5-6: Progress bars */
.progress-sektsiya { background: white; padding: 28px; border-radius: 16px; margin-bottom: 24px; }
.progress-sektsiya h3 { margin-bottom: 20px; }
.ko'nikma { display: flex; align-items: center; gap: 12px; margin-bottom: 14px; }
.ko'nikma span:first-child { min-width: 40px; font-weight: 600; font-size: 14px; }
.ko'nikma span:last-child  { min-width: 40px; font-size: 13px; color: #888; }
.progress { flex: 1; height: 10px; background: #f0f0f0; border-radius: 5px; overflow: hidden; }
.progress__to'ldirish {
  height: 100%; width: 0; border-radius: 5px;
  background: linear-gradient(90deg, royalblue, #764ba2);
  animation: progressFill 1.5s ease forwards 0.3s;
}

/* Vazifa 7: Typing dots */
.typing-indikator {
  display: inline-flex; gap: 6px; padding: 12px 20px;
  background: white; border-radius: 20px; margin-bottom: 24px;
  box-shadow: 0 2px 12px rgba(0,0,0,0.08);
}
.dot {
  width: 10px; height: 10px; border-radius: 50%; background: #aaa;
  animation: bounce 1.2s ease infinite;
}
.dot:nth-child(2) { animation-delay: 0.2s; }
.dot:nth-child(3) { animation-delay: 0.4s; }

/* Vazifa 8: Notification */
.notification {
  display: flex; align-items: center; gap: 10px; padding: 16px 24px;
  background: #d4edda; border: 1px solid #c3e6cb; border-radius: 10px;
  color: #155724; margin-bottom: 24px;
  animation: slideIn 0.5s cubic-bezier(0.34, 1.56, 0.64, 1) forwards;
}

/* Vazifa 9-10: Animatsion gradient */
.gradient-anim-sektsiya {
  min-height: 300px; display: flex; flex-direction: column;
  align-items: center; justify-content: center; text-align: center;
  border-radius: 20px; color: white;
  background: linear-gradient(-45deg, #ee7752, #e73c7e, #23a6d5, #23d5ab);
  background-size: 400% 400%;
  animation: gradientShift 8s ease infinite;
}
.gradient-anim-sektsiya h2 { font-size: 36px; margin-bottom: 12px; }
```
