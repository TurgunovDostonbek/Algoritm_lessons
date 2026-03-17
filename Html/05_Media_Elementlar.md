# 05-Dars: Media Elementlari va Multimedia Content

## 📌 `<img>` — Rasm Tegi

```html
<!-- Asosiy sintaksis -->
<img src="rasm.jpg" alt="Rasmning tavsifi">

<!-- src — rasm manzili (relative yoki absolute) -->
<img src="images/avatar.jpg" alt="Profil rasmi">       <!-- Lokal fayl -->
<img src="../images/logo.png" alt="Logo">               <!-- Yuqori papka -->
<img src="https://picsum.photos/400/300" alt="Rasm">   <!-- URL -->
<img src="data:image/png;base64,..." alt="Base64 rasm"> <!-- Base64 -->

<!-- alt — MAJBURIY! -->
<img src="rasm.jpg" alt="Ibn Sino portreti">  <!-- Matnli tavsif -->
<img src="bezak.svg" alt="">                  <!-- Bezak rasm — bo'sh alt -->

<!-- width va height — Safari uchun performance -->
<img src="rasm.jpg" alt="Tavsif" width="800" height="600">

<!-- loading — lazy loading (performance) -->
<img src="rasm.jpg" alt="Tavsif" loading="lazy">   <!-- Viewport da ko'ringanda yuklaydi -->
<img src="hero.jpg" alt="Hero" loading="eager">     <!-- Darhol yuklaydi (default) -->

<!-- decoding -->
<img src="rasm.jpg" alt="Tavsif" decoding="async"> <!-- Yuklashni async qiladi -->
```

---

## 📌 `<img>` Atributlari

```html
<img
  src="rasm.jpg"           <!-- Manba (required) -->
  alt="Tavsif"             <!-- Alt matn (required) -->
  width="400"              <!-- Kenglik (px, %, raqam) -->
  height="300"             <!-- Balandlik -->
  title="Tooltip matni"   <!-- Hover tooltip -->
  loading="lazy"           <!-- Lazy loading -->
  decoding="async"         <!-- Asinxron dekod -->
  class="hero-rasm"        <!-- CSS sinf -->
  id="bosh-rasm"           <!-- ID -->
  style="border-radius: 8px"  <!-- Inline style -->

  <!-- Srcset — Responsive rasmlar -->
  srcset="
    rasm-400.jpg 400w,
    rasm-800.jpg 800w,
    rasm-1200.jpg 1200w
  "
  sizes="(max-width: 600px) 400px, (max-width: 1000px) 800px, 1200px"
>
```

---

## 📌 `<video>` — Video Tegi

```html
<!-- Asosiy -->
<video src="video.mp4" controls></video>

<!-- Atributlar bilan -->
<video
  src="video.mp4"
  controls           <!-- Boshqaruv paneli -->
  autoplay           <!-- Avtomatik boshlanish -->
  muted              <!-- Ovossiz (autoplay uchun kerak!) -->
  loop               <!-- Qayta boshlash -->
  preload="auto"     <!-- Oldindan yuklash (auto|metadata|none) -->
  poster="preview.jpg"  <!-- Yuklanmasdan oldin ko'rinadigan rasm -->
  width="800"
  height="450"
>
</video>

<!-- Bir nechta format (brauzer muvofiq topadi) -->
<video controls>
  <source src="video.mp4" type="video/mp4">
  <source src="video.webm" type="video/webm">
  <source src="video.ogg" type="video/ogg">
  <p>Brauzeringiz videoyi qo'llab-quvvatlamaydi.</p>
</video>

<!-- YouTube embedi (iframe) -->
<iframe
  width="560" height="315"
  src="https://www.youtube.com/embed/VIDEO_ID"
  title="Video nomi"
  frameborder="0"
  allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
  allowfullscreen>
</iframe>
```

---

## 📌 `<audio>` — Audio Tegi

```html
<!-- Asosiy -->
<audio src="musiqa.mp3" controls></audio>

<!-- Bir nechta format -->
<audio controls>
  <source src="musiqa.mp3" type="audio/mpeg">
  <source src="musiqa.ogg" type="audio/ogg">
  <source src="musiqa.wav" type="audio/wav">
  <p>Brauzeringiz audioyi qo'llab-quvvatlamaydi.</p>
</audio>

<!-- Atributlar -->
<audio
  src="musiqa.mp3"
  controls
  autoplay
  loop
  muted
  preload="none"
>
</audio>
```

---

## 📌 `<iframe>` — Tashqi Resurslar

```html
<!-- iframe — sahifa ichida boshqa sahifa -->

<!-- YouTube -->
<iframe
  src="https://www.youtube.com/embed/dQw4w9WgXcQ"
  width="560" height="315"
  title="YouTube video"
  allowfullscreen>
</iframe>

<!-- Google Maps -->
<iframe
  src="https://www.google.com/maps/embed?pb=!1m18!..."
  width="600" height="450"
  style="border:0;"
  allowfullscreen
  loading="lazy"
  referrerpolicy="no-referrer-when-downgrade">
</iframe>

<!-- Boshqa sayt -->
<iframe
  src="https://example.com"
  width="100%"
  height="500"
  title="Tashqi sahifa">
</iframe>

<!-- Sandbox — xavfsizlik -->
<iframe
  src="sandbox.html"
  sandbox="allow-scripts allow-same-origin"
  title="Sandbox sahifa">
</iframe>
```

---

## 📌 `<picture>` — Responsive Rasm

```html
<!-- picture — turli ekranlar uchun turli rasmlar -->
<picture>
  <!-- Katta ekran -->
  <source media="(min-width: 1200px)" srcset="rasm-katta.jpg">
  <!-- O'rta ekran -->
  <source media="(min-width: 768px)"  srcset="rasm-orta.jpg">
  <!-- WebP format (agar qo'llab-quvvatlansa) -->
  <source type="image/webp" srcset="rasm.webp">
  <!-- Fallback (default) -->
  <img src="rasm.jpg" alt="Tavsif" loading="lazy">
</picture>
```

---

## 🎯 10 ta Amaliy Vazifa

### Vazifa 1-5: YouTube sahifasidan misol yaratib kelish (5tadan)
```html
<!DOCTYPE html>
<html lang="uz">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Media — YouTube Klonı</title>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body { background: #0f0f0f; color: white; font-family: "Segoe UI", sans-serif; }
    .navbar { display: flex; align-items: center; justify-content: space-between;
              padding: 14px 24px; background: #0f0f0f; position: sticky; top: 0; }
    .logo { font-size: 22px; font-weight: 700; color: white; }
    .logo span { color: #ff0000; }
    .qidiruv { display: flex; gap: 8px; }
    .qidiruv input { padding: 8px 16px; border: 1px solid #444; background: #1a1a1a;
                     color: white; border-radius: 20px 0 0 20px; width: 300px; outline: none; }
    .qidiruv button { padding: 8px 16px; background: #333; color: white; border: 1px solid #444; border-radius: 0 20px 20px 0; cursor: pointer; }

    .video-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
                  gap: 20px; padding: 20px; }
    .video-karta { cursor: pointer; }
    .thumbnail { position: relative; border-radius: 10px; overflow: hidden; }
    .thumbnail img { width: 100%; height: 170px; object-fit: cover; display: block;
                     transition: transform 0.3s; }
    .video-karta:hover .thumbnail img { transform: scale(1.02); }
    .muddat { position: absolute; bottom: 6px; right: 6px; background: rgba(0,0,0,0.8);
              padding: 2px 6px; border-radius: 4px; font-size: 12px; }
    .meta { display: flex; gap: 12px; padding: 10px 0; }
    .avatar { width: 36px; height: 36px; border-radius: 50%; background: royalblue;
              display: flex; align-items: center; justify-content: center; flex-shrink: 0; font-weight: bold; }
    .info h3 { font-size: 14px; margin-bottom: 4px; line-height: 1.4; }
    .info .kanal { color: #aaa; font-size: 12px; }
    .info .statistika { color: #aaa; font-size: 12px; }
  </style>
</head>
<body>

  <nav class="navbar">
    <div class="logo">📺 <span>You</span>Tube</div>
    <div class="qidiruv">
      <input type="search" placeholder="Qidirish">
      <button>🔍</button>
    </div>
    <div>👤</div>
  </nav>

  <div class="video-grid">
    <!-- Vazifa 1 -->
    <div class="video-karta">
      <div class="thumbnail">
        <img src="https://picsum.photos/400/225?random=1" alt="CSS Flexbox" loading="lazy">
        <span class="muddat">12:34</span>
      </div>
      <div class="meta">
        <div class="avatar">A</div>
        <div class="info">
          <h3>CSS Flexbox to'liq qo'llanma — Boshlang'ichlar uchun</h3>
          <div class="kanal">Web Dev Academy</div>
          <div class="statistika">125K ko'rish • 3 kun oldin</div>
        </div>
      </div>
    </div>

    <!-- Vazifa 2 -->
    <div class="video-karta">
      <div class="thumbnail">
        <img src="https://picsum.photos/400/225?random=2" alt="JavaScript" loading="lazy">
        <span class="muddat">25:18</span>
      </div>
      <div class="meta">
        <div class="avatar" style="background: #e63946;">J</div>
        <div class="info">
          <h3>JavaScript Async/Await — Batafsil tushuntirish</h3>
          <div class="kanal">JS Master</div>
          <div class="statistika">89K ko'rish • 1 hafta oldin</div>
        </div>
      </div>
    </div>

    <!-- Vazifa 3 -->
    <div class="video-karta">
      <div class="thumbnail">
        <img src="https://picsum.photos/400/225?random=3" alt="React" loading="lazy">
        <span class="muddat">45:02</span>
      </div>
      <div class="meta">
        <div class="avatar" style="background: #2196f3;">R</div>
        <div class="info">
          <h3>React.js 2024 — To'liq kurs boshlang'ichlar uchun</h3>
          <div class="kanal">React Dars</div>
          <div class="statistika">340K ko'rish • 2 oy oldin</div>
        </div>
      </div>
    </div>

    <!-- Vazifa 4 -->
    <div class="video-karta">
      <div class="thumbnail">
        <img src="https://picsum.photos/400/225?random=4" alt="HTML" loading="lazy">
        <span class="muddat">8:45</span>
      </div>
      <div class="meta">
        <div class="avatar" style="background: #ff9800;">H</div>
        <div class="info">
          <h3>HTML5 Semantik Elementlar — 2024</h3>
          <div class="kanal">HTML Asoslari</div>
          <div class="statistika">45K ko'rish • 5 kun oldin</div>
        </div>
      </div>
    </div>

    <!-- Vazifa 5 -->
    <div class="video-karta">
      <div class="thumbnail">
        <img src="https://picsum.photos/400/225?random=5" alt="Git" loading="lazy">
        <span class="muddat">31:20</span>
      </div>
      <div class="meta">
        <div class="avatar" style="background: #4caf50;">G</div>
        <div class="info">
          <h3>Git va GitHub — Boshlang'ichlar uchun to'liq qo'llanma</h3>
          <div class="kanal">DevOps Life</div>
          <div class="statistika">210K ko'rish • 3 oy oldin</div>
        </div>
      </div>
    </div>
  </div>

</body>
</html>
```

### Vazifa 6: Audio player
```html
<div style="background: #1a1a2e; padding: 40px; max-width: 400px; margin: 40px auto; border-radius: 20px; color: white; text-align: center;">
  <div style="font-size: 80px; margin-bottom: 16px;">🎵</div>
  <h2>Mening Qo'shig'im</h2>
  <p style="color: #aaa; font-size: 14px; margin-bottom: 20px;">Artist nomi</p>
  <audio controls style="width: 100%;">
    <source src="https://www.w3schools.com/html/horse.mp3" type="audio/mpeg">
    Brauzeringiz audio qo'llab-quvvatlamaydi.
  </audio>
</div>
```

### Vazifa 7: Responsive rasm
```html
<picture>
  <source media="(min-width: 800px)" srcset="https://picsum.photos/1200/400?random=10">
  <source media="(min-width: 500px)" srcset="https://picsum.photos/800/400?random=10">
  <img src="https://picsum.photos/400/300?random=10" alt="Responsive rasm" style="width: 100%;">
</picture>
```

### Vazifa 8-10: iframe va video
```html
<!-- Vazifa 8: YouTube embed -->
<iframe width="100%" height="400"
  src="https://www.youtube.com/embed/qz0aGYrrlhU"
  title="HTML Tutorial" allowfullscreen
  style="border:0; border-radius: 12px;">
</iframe>

<!-- Vazifa 9: Video player -->
<video controls width="100%" poster="https://picsum.photos/800/450?random=20"
  style="border-radius: 12px;">
  <source src="https://www.w3schools.com/html/mov_bbb.mp4" type="video/mp4">
</video>

<!-- Vazifa 10: Figure va Figcaption -->
<figure style="text-align: center; max-width: 600px; margin: 0 auto;">
  <img src="https://picsum.photos/600/400?random=30" alt="Ibn Sino"
    style="width: 100%; border-radius: 12px;">
  <figcaption style="color: #666; font-size: 14px; margin-top: 8px;">
    <em>Ibn Sino portreti — 980-1037 yillar</em>
  </figcaption>
</figure>
```
