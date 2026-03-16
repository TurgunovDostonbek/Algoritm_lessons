# 19-Dars: Tailwind CSS va Bootstrap

## 📌 Tailwind CSS nima?

**Tailwind CSS** — utility-first CSS freymvorki. Har bir sinf bitta CSS xossaning qiymati.

```html
<!-- Bootstrap — Komponent asosida -->
<button class="btn btn-primary btn-lg">Bosing</button>

<!-- Tailwind — Utility asosida -->
<button class="px-6 py-3 bg-blue-600 text-white rounded-lg text-lg hover:bg-blue-700">
  Bosing
</button>
```

---

## 📌 Tailwind CSS — O'rnatish

```html
<!-- 1. CDN (darslar uchun, production emas) -->
<script src="https://cdn.tailwindcss.com"></script>

<!-- 2. NPM orqali (production uchun) -->
<!-- npm install -D tailwindcss -->
<!-- npx tailwindcss init -->
```

---

## 📌 Tailwind Asosiy Classlar

```html
<!-- Spacing (m=margin, p=padding, t=top, r=right, b=bottom, l=left, x=gorizontal, y=vertikal) -->
<div class="m-4 p-6 mx-auto mt-8 px-4 py-2"></div>
<!-- 1 birlik = 4px: m-1=4px, m-2=8px, m-4=16px, m-8=32px -->

<!-- Width va Height -->
<div class="w-full w-1/2 w-64 h-screen h-auto max-w-xl min-h-screen"></div>

<!-- Flexbox -->
<div class="flex items-center justify-between gap-4 flex-wrap flex-col"></div>

<!-- Grid -->
<div class="grid grid-cols-3 grid-cols-12 gap-6 col-span-4"></div>

<!-- Typography -->
<p class="text-sm text-base text-lg text-xl text-2xl text-4xl
          font-bold font-semibold font-normal italic
          text-center text-left uppercase tracking-wide
          leading-loose text-gray-700 text-blue-600"></p>

<!-- Colors (bg-RANG-KUCH) -->
<div class="bg-blue-500 bg-red-600 bg-green-400 bg-gray-100
            text-white text-gray-900 text-blue-700
            border border-gray-200 border-blue-500"></div>

<!-- Border -->
<div class="border border-2 border-dashed rounded rounded-lg rounded-full
            border-gray-300 border-blue-500"></div>

<!-- Shadows -->
<div class="shadow shadow-md shadow-lg shadow-xl shadow-none"></div>

<!-- Display -->
<div class="block inline inline-block flex grid hidden"></div>

<!-- Position -->
<div class="relative absolute fixed sticky top-0 left-0 right-0 bottom-0 z-10"></div>

<!-- Hover, Focus, Active -->
<button class="bg-blue-600 hover:bg-blue-700 focus:ring-2 active:scale-95"></button>

<!-- Responsive (sm: md: lg: xl: 2xl:) -->
<div class="text-sm md:text-base lg:text-lg xl:text-xl"></div>
<div class="grid-cols-1 md:grid-cols-2 lg:grid-cols-4"></div>
```

---

## 📌 Tailwind — Custom Qiymatlar

```html
<!-- Arbitrary values — kvadrat qavs ichida istalgan qiymat -->
<div class="w-[320px] h-[50vh] top-[72px]"></div>
<div class="text-[22px] text-[#ff6b6b] bg-[rgba(0,0,0,0.5)]"></div>
<div class="grid-cols-[1fr_2fr_1fr]"></div>
```

---

## 📌 Tailwind — @apply Direktivi

```css
/* style.css */
@tailwind base;
@tailwind components;
@tailwind utilities;

/* Komponent classlar yaratish */
@layer components {
  .btn-primary {
    @apply px-6 py-3 bg-blue-600 text-white rounded-lg font-semibold
           hover:bg-blue-700 transition-colors duration-200 cursor-pointer;
  }
  .karta {
    @apply bg-white rounded-xl shadow-md p-6 hover:shadow-lg transition-shadow;
  }
}
```

---

## 📌 Bootstrap nima?

**Bootstrap** — oldindan tayyor komponentlarga ega CSS freymvorki.

```html
<!-- Bootstrap CDN -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css">
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
```

---

## 📌 Bootstrap Grid Tizimi (12 ustun)

```html
<div class="container">          <!-- Markazga, max-width -->
  <div class="container-fluid">  <!-- To'liq kenglik -->
    <div class="row">            <!-- Qator -->
      <div class="col-12 col-md-6 col-lg-4">  <!-- Responsive ustun -->
        Kontent
      </div>
    </div>
  </div>
</div>

<!-- Breakpoints: xs(<576), sm(576+), md(768+), lg(992+), xl(1200+), xxl(1400+) -->
<!-- Ustunlar: col-1 dan col-12 gacha (12 ga teng bo'lishi kerak) -->
```

---

## 📌 Bootstrap Komponentlari

```html
<!-- Navbar -->
<nav class="navbar navbar-expand-lg navbar-dark bg-dark">
  <div class="container">
    <a class="navbar-brand" href="#">Brand</a>
    <button class="navbar-toggler" data-bs-toggle="collapse" data-bs-target="#navbarNav">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNav">
      <ul class="navbar-nav ms-auto">
        <li class="nav-item"><a class="nav-link" href="#">Bosh</a></li>
      </ul>
    </div>
  </div>
</nav>

<!-- Tugmalar -->
<button class="btn btn-primary">Asosiy</button>
<button class="btn btn-secondary btn-lg">Katta</button>
<button class="btn btn-outline-danger btn-sm">Kichik</button>

<!-- Kartalar -->
<div class="card" style="width: 18rem;">
  <img src="..." class="card-img-top" alt="...">
  <div class="card-body">
    <h5 class="card-title">Sarlavha</h5>
    <p class="card-text">Tavsif</p>
    <a href="#" class="btn btn-primary">Ko'rish</a>
  </div>
</div>

<!-- Modal -->
<button data-bs-toggle="modal" data-bs-target="#myModal">Modal</button>
<div class="modal fade" id="myModal" tabindex="-1">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title">Sarlavha</h5>
        <button class="btn-close" data-bs-dismiss="modal"></button>
      </div>
      <div class="modal-body">Kontent</div>
    </div>
  </div>
</div>

<!-- Alert -->
<div class="alert alert-success alert-dismissible fade show">
  Muvaffaqiyat! <button class="btn-close" data-bs-dismiss="alert"></button>
</div>
```

---

## 📌 Tailwind vs Bootstrap

| Jihat | Tailwind | Bootstrap |
|-------|----------|-----------|
| Yondashuv | Utility-first | Component-based |
| Fayl hajmi (unoptimized) | Katta | O'rtacha |
| Fayl hajmi (optimized) | Kichik (PurgeCSS) | O'rtacha |
| Flexibillik | ✅ Juda yuqori | ❌ Cheklangan |
| O'rganish egri | Tik | Tekis |
| Tayyor komponent | ❌ Yo'q | ✅ Ko'p |
| Dizayn mosligi | To'liq | Qisman |
| Bootstrap o'xshashligi | ❌ | ✅ O'xshash saytlar |

---

## 🎯 10 ta Amaliy Vazifa

```html
<!-- Tailwind bilan amaliyot (CDN) -->
<!DOCTYPE html>
<html lang="uz">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tailwind Amaliyot</title>
  <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-gray-50 font-sans">

  <!-- Vazifa 1: Tailwind Navbar -->
  <nav class="bg-slate-900 px-6 py-4 flex items-center justify-between sticky top-0 z-50">
    <span class="text-white text-xl font-bold">🎨 MyBrand</span>
    <div class="hidden md:flex gap-6">
      <a href="#" class="text-gray-300 hover:text-white transition-colors">Bosh</a>
      <a href="#" class="text-gray-300 hover:text-white transition-colors">Xizmat</a>
      <a href="#" class="text-gray-300 hover:text-white transition-colors">Aloqa</a>
    </div>
    <button class="bg-blue-600 text-white px-4 py-2 rounded-lg text-sm font-semibold hover:bg-blue-700 transition-colors">
      Boshlash
    </button>
  </nav>

  <!-- Vazifa 2: Hero sekciyasi -->
  <section class="min-h-[90vh] flex items-center justify-center bg-gradient-to-br from-slate-900 to-blue-900 text-white text-center px-6">
    <div>
      <span class="inline-block bg-blue-600/30 text-blue-300 px-4 py-1 rounded-full text-sm mb-6">
        🚀 Yangi versiya chiqdi!
      </span>
      <h1 class="text-5xl md:text-7xl font-bold mb-6 leading-tight">
        Zamonaviy <span class="text-blue-400">Veb</span> Dizayn
      </h1>
      <p class="text-gray-300 text-lg md:text-xl max-w-2xl mx-auto mb-8">
        Tailwind CSS bilan tez va chiroyli interfeys yarating
      </p>
      <div class="flex gap-4 justify-center flex-wrap">
        <button class="bg-blue-600 px-8 py-4 rounded-xl font-semibold text-lg hover:bg-blue-700 transition-all hover:scale-105 active:scale-95">
          Boshlash →
        </button>
        <button class="border border-white/30 px-8 py-4 rounded-xl font-semibold text-lg hover:bg-white/10 transition-all">
          Namunalar
        </button>
      </div>
    </div>
  </section>

  <!-- Vazifa 3: Xizmatlar grid -->
  <section class="py-24 px-6 max-w-6xl mx-auto">
    <h2 class="text-4xl font-bold text-center mb-4">Xizmatlar</h2>
    <p class="text-gray-500 text-center mb-12 max-w-xl mx-auto">Biz taqdim etadigan asosiy xizmatlar</p>
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
      <div class="bg-white p-8 rounded-2xl shadow-sm hover:shadow-lg transition-shadow group">
        <div class="w-12 h-12 bg-blue-100 rounded-xl flex items-center justify-center mb-4 group-hover:bg-blue-600 transition-colors">
          <span class="text-2xl group-hover:scale-110 transition-transform inline-block">💻</span>
        </div>
        <h3 class="text-xl font-bold mb-2">Frontend</h3>
        <p class="text-gray-500 text-sm leading-relaxed">HTML, CSS va JavaScript bilan zamonaviy interfeys</p>
      </div>
      <div class="bg-white p-8 rounded-2xl shadow-sm hover:shadow-lg transition-shadow group">
        <div class="w-12 h-12 bg-purple-100 rounded-xl flex items-center justify-center mb-4 group-hover:bg-purple-600 transition-colors">
          <span class="text-2xl">🎨</span>
        </div>
        <h3 class="text-xl font-bold mb-2">UI/UX Dizayn</h3>
        <p class="text-gray-500 text-sm leading-relaxed">Figma va zamonaviy dizayn trendlari</p>
      </div>
      <div class="bg-white p-8 rounded-2xl shadow-sm hover:shadow-lg transition-shadow group">
        <div class="w-12 h-12 bg-green-100 rounded-xl flex items-center justify-center mb-4 group-hover:bg-green-600 transition-colors">
          <span class="text-2xl">📱</span>
        </div>
        <h3 class="text-xl font-bold mb-2">Responsive</h3>
        <p class="text-gray-500 text-sm leading-relaxed">Barcha qurilmalarda mukammal ko'rinish</p>
      </div>
    </div>
  </section>

  <!-- Vazifa 4: Narx kartalar -->
  <section class="py-24 bg-slate-900 px-6">
    <h2 class="text-4xl font-bold text-center text-white mb-12">Narxlar</h2>
    <div class="grid grid-cols-1 md:grid-cols-3 gap-8 max-w-5xl mx-auto">
      <!-- Oddiy -->
      <div class="bg-slate-800 text-white p-8 rounded-2xl">
        <h3 class="text-lg font-semibold text-gray-400 mb-2">Starter</h3>
        <div class="text-4xl font-bold mb-6">$0 <span class="text-base font-normal text-gray-400">/oy</span></div>
        <ul class="space-y-3 text-sm text-gray-300 mb-8">
          <li class="flex items-center gap-2"><span class="text-green-400">✓</span> 1 ta loyiha</li>
          <li class="flex items-center gap-2"><span class="text-green-400">✓</span> Asosiy funksiyalar</li>
          <li class="flex items-center gap-2 opacity-50"><span>✗</span> Kengaytirilgan</li>
        </ul>
        <button class="w-full py-3 border border-gray-600 rounded-xl hover:bg-slate-700 transition-colors">Boshlash</button>
      </div>
      <!-- Featured -->
      <div class="bg-blue-600 text-white p-8 rounded-2xl scale-105 shadow-2xl shadow-blue-500/30 relative">
        <span class="absolute -top-3 left-1/2 -translate-x-1/2 bg-yellow-400 text-black text-xs font-bold px-3 py-1 rounded-full">MASHHUR</span>
        <h3 class="text-lg font-semibold text-blue-200 mb-2">Pro</h3>
        <div class="text-4xl font-bold mb-6">$29 <span class="text-base font-normal text-blue-200">/oy</span></div>
        <ul class="space-y-3 text-sm mb-8">
          <li class="flex items-center gap-2"><span>✓</span> 10 ta loyiha</li>
          <li class="flex items-center gap-2"><span>✓</span> Barcha funksiyalar</li>
          <li class="flex items-center gap-2"><span>✓</span> 24/7 yordam</li>
        </ul>
        <button class="w-full py-3 bg-white text-blue-600 rounded-xl font-bold hover:bg-blue-50 transition-colors">Sotib olish</button>
      </div>
      <!-- Enterprise -->
      <div class="bg-slate-800 text-white p-8 rounded-2xl">
        <h3 class="text-lg font-semibold text-gray-400 mb-2">Enterprise</h3>
        <div class="text-4xl font-bold mb-6">$99 <span class="text-base font-normal text-gray-400">/oy</span></div>
        <ul class="space-y-3 text-sm text-gray-300 mb-8">
          <li class="flex items-center gap-2"><span class="text-green-400">✓</span> Cheksiz loyiha</li>
          <li class="flex items-center gap-2"><span class="text-green-400">✓</span> VIP yordam</li>
          <li class="flex items-center gap-2"><span class="text-green-400">✓</span> Custom domain</li>
        </ul>
        <button class="w-full py-3 border border-gray-600 rounded-xl hover:bg-slate-700 transition-colors">Murojaat</button>
      </div>
    </div>
  </section>

  <!-- Vazifa 5-10: Bootstrap bilan amaliyot -->
  <!-- Bu qismni Bootstrap CDN bilan alohida faylda sinab ko'ring -->

  <!-- Vazifa 5: Bootstrap Navbar -->
  <!-- Vazifa 6: Bootstrap Grid (12 ustun tizimi) -->
  <!-- Vazifa 7: Bootstrap Tugmalar va Formalar -->
  <!-- Vazifa 8: Bootstrap Modal -->
  <!-- Vazifa 9: Bootstrap Alert va Badge -->
  <!-- Vazifa 10: Bootstrap + Custom CSS birlashtirish -->

  <!-- Bootstrap namunasi: -->
  <!--
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css">
  <div class="container">
    <div class="row g-4">
      <div class="col-12 col-md-6 col-lg-4">
        <div class="card h-100">
          <img src="..." class="card-img-top" alt="...">
          <div class="card-body">
            <h5 class="card-title">Karta sarlavhasi</h5>
            <p class="card-text text-muted">Tavsif matni</p>
            <a href="#" class="btn btn-primary">Ko'rish</a>
          </div>
        </div>
      </div>
    </div>
  </div>
  -->

</body>
</html>
```
