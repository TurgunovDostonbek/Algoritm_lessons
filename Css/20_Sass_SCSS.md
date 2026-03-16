# 20-Dars: Sass / SCSS — CSS Preprocessor

## 📌 Sass nima? CSS Preprocessor farqlari

```
CSS Preprocessorlar:
├── Sass/SCSS  — Eng mashhur (Ruby/Dart)
├── Less       — JavaScript asosida
└── Stylus     — Minimalist sintaksis
```

| Jihat | CSS | SCSS | Less |
|-------|-----|------|------|
| O'zgaruvchilar | `var(--rang)` | `$rang` | `@rang` |
| Nested | ❌ | ✅ | ✅ |
| Mixin | ❌ | ✅ | ✅ |
| Extend | ❌ | ✅ | ✅ |
| Math | `calc()` | `+, -, *, /` | ✅ |
| Kompilyatsiya | ❌ | Kerak | Kerak |

---

## 📌 Sass va SCSS farqi

```scss
/* SCSS — CSS ga o'xshash sintaksis (tavsiya) */
.navbar {
  background: $asosiy-rang;
  
  &:hover { color: white; }
  
  .logo { font-size: 24px; }
}

/* Sass — qavssiz sintaksis (eskirgan) */
.navbar
  background: $asosiy-rang
  
  &:hover
    color: white
  
  .logo
    font-size: 24px
```

---

## 📌 O'rnatish va Kompilyatsiya

```bash
# 1. NPM orqali
npm install -g sass

# 2. Kompilyatsiya
sass style.scss style.css
sass --watch style.scss style.css   # O'zgarishlarni kuzatib
sass --watch scss/:css/             # Papka kuzatish

# 3. VS Code — Live Sass Compiler extension
# .scss faylni saqlaganda avtomatik .css yaratadi
```

---

## 📌 `$` — O'zgaruvchilar

```scss
// O'zgaruvchilar — qayta foydalanish uchun
$asosiy-rang:    royalblue;
$ikkilamchi:     #764ba2;
$xavfli:         #ff6b6b;
$matn-rangi:     #1a1a2e;
$fon-rangi:      #f8f9fa;

$shrift:         "Inter", system-ui, sans-serif;
$shrift-katta:   2rem;
$shrift-asosiy:  1rem;
$shrift-kichik:  0.875rem;

$chegara:        1px solid #e0e0e0;
$radius:         12px;
$soya:           0 4px 20px rgba(0, 0, 0, 0.1);
$o_tish:         all 0.3s ease;

// Ishlatish
.btn {
  background: $asosiy-rang;
  font-family: $shrift;
  box-shadow: $soya;
  transition: $o_tish;
  border-radius: $radius;
}
```

---

## 📌 Nested (Ichki) Qoidalar va `&`

```scss
// & — ota selectorni bildiradi
.navbar {
  background: $asosiy-rang;
  padding: 0 24px;
  
  // .navbar .logo
  .logo {
    font-size: 24px;
    font-weight: 700;
  }
  
  // .navbar .menu
  .menu {
    display: flex;
    gap: 20px;
    
    // .navbar .menu a
    a {
      color: white;
      text-decoration: none;
      
      // .navbar .menu a:hover
      &:hover {
        opacity: 0.8;
      }
      
      // .navbar .menu a.faol
      &.faol {
        font-weight: bold;
        border-bottom: 2px solid white;
      }
    }
  }
  
  // .navbar--qorongu (Modifier)
  &--qorongu {
    background: #1a1a2e;
  }
  
  // Pseudo-element
  &::after {
    content: "";
    display: block;
  }
}
```

---

## 📌 `#{}` — Interpolatsiya (String ichiga o'zgaruvchi)

```scss
$tomonlar: top, right, bottom, left;
$propertiylar: width, height;
$prefiklar: webkit, moz, ms;

// Dinamik property nomi
@each $tomon in $tomonlar {
  .m-#{$tomon} { margin-#{$tomon}: 8px; }
}
// Natija: .m-top, .m-right, .m-bottom, .m-left
```

---

## 📌 `@mixin` va `@include`

```scss
// Mixin — qayta ishlatiladigan kod bloklari

// 1. Parametrsiz mixin
@mixin flex-markaz {
  display: flex;
  align-items: center;
  justify-content: center;
}

// 2. Parametrli mixin
@mixin tugma($fon, $matn: white, $radius: 8px) {
  padding: 12px 24px;
  background: $fon;
  color: $matn;
  border: none;
  border-radius: $radius;
  cursor: pointer;
  font-weight: 600;
  transition: all 0.2s;
  
  &:hover { opacity: 0.85; transform: translateY(-2px); }
  &:active { transform: translateY(0); }
}

// 3. @content — mixin ichiga kod uzatish
@mixin media($breakpoint) {
  @if $breakpoint == sm { @media (min-width: 576px) { @content; } }
  @else if $breakpoint == md { @media (min-width: 768px) { @content; } }
  @else if $breakpoint == lg { @media (min-width: 992px) { @content; } }
  @else if $breakpoint == xl { @media (min-width: 1200px) { @content; } }
}

// Ishlatish
.element {
  @include flex-markaz;
}
.btn-asosiy {
  @include tugma(royalblue);
}
.btn-xavfli {
  @include tugma(#ff6b6b, white, 4px);
}

// Media mixin ishlatish
.karta {
  width: 100%;
  @include media(md) { width: 50%; }
  @include media(lg) { width: 33.33%; }
}
```

---

## 📌 `@extend` — Kengaytirish

```scss
// Asosiy klass
%tugma-asosi {
  padding: 12px 24px;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  font-weight: 600;
  transition: all 0.2s;
}

// Kengaytirish
.btn-asosiy {
  @extend %tugma-asosi;
  background: royalblue;
  color: white;
}
.btn-ikkilamchi {
  @extend %tugma-asosi;
  background: #e2e8f0;
  color: #1a1a2e;
}
.btn-xavfli {
  @extend %tugma-asosi;
  background: #ff6b6b;
  color: white;
}
```

---

## 📌 `@if`, `@each`, `@for`, `@while`

```scss
// @if - Shart
@mixin rang-tema($tema) {
  @if $tema == "yorug" {
    background: white;
    color: #1a1a2e;
  } @else if $tema == "qorongu" {
    background: #1a1a2e;
    color: white;
  } @else {
    background: gray;
  }
}

// @each — Ro'yxat bo'yicha
$ranglar: (asosiy: royalblue, xavfli: #ff6b6b, muvaffaq: #51cf66, ogohlantirish: #fcc419);

@each $nom, $rang in $ranglar {
  .text-#{$nom}  { color: $rang; }
  .bg-#{$nom}    { background: $rang; }
  .btn-#{$nom}   { background: $rang; color: white; }
}

// @for — Raqamli tsikl
@for $i from 1 through 6 {
  .grid-cols-#{$i} { grid-template-columns: repeat(#{$i}, 1fr); }
}
// Natija: .grid-cols-1, .grid-cols-2, ..., .grid-cols-6

// Spacing utilities
$spacings: 0, 4, 8, 12, 16, 20, 24, 32, 40, 48;
@each $s in $spacings {
  .m-#{$s}  { margin: #{$s}px; }
  .p-#{$s}  { padding: #{$s}px; }
  .mt-#{$s} { margin-top: #{$s}px; }
  .mb-#{$s} { margin-bottom: #{$s}px; }
}
```

---

## 📌 `@use` va `@forward` — Modullar

```scss
// _o'zgaruvchilar.scss (prefiks _ = partial)
$asosiy: royalblue;
$radius: 12px;

// _mixinlar.scss
@use "o'zgaruvchilar" as v;
@mixin karta-stil {
  border-radius: v.$radius;
  box-shadow: 0 4px 20px rgba(0,0,0,0.1);
}

// style.scss — asosiy fayl
@use "o'zgaruvchilar" as v;
@use "mixinlar" as m;

body { color: v.$asosiy; }
.karta { @include m.karta-stil; }
```

---

## 🎯 10 ta Amaliy Vazifa

```scss
/* ======= _variables.scss ======= */
// Ranglar
$rang-asosiy:      #4361ee;
$rang-ikkilamchi:  #7209b7;
$rang-muvaffaq:    #4cc9f0;
$rang-xavfli:      #f72585;
$rang-ogohlantirish: #f8961e;

// Tipografiya
$font-asosiy:  "Inter", system-ui, sans-serif;
$font-sarlavha: "Playfair Display", Georgia, serif;
$font-kichik:  0.875rem;
$font-asosiy-o'lchami: 1rem;
$font-katta:   1.125rem;

// O'lcham
$radius-sm:   6px;
$radius-md:   12px;
$radius-lg:   20px;
$radius-doira: 50%;

// Soya
$soya-sm: 0 2px 8px rgba(0,0,0,0.06);
$soya-md: 0 4px 20px rgba(0,0,0,0.08);
$soya-lg: 0 8px 32px rgba(0,0,0,0.12);

// Breakpoints
$sm: 576px; $md: 768px; $lg: 992px; $xl: 1200px;

/* ======= _mixins.scss ======= */
@use "variables" as *;

// Vazifa 1: Flex markaz mixin
@mixin flex-markaz($yo'nalish: row) {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: $yo'nalish;
}

// Vazifa 2: Responsive mixin
@mixin bp($breakpoint) {
  @if $breakpoint == sm { @media (min-width: $sm) { @content; } }
  @else if $breakpoint == md { @media (min-width: $md) { @content; } }
  @else if $breakpoint == lg { @media (min-width: $lg) { @content; } }
  @else if $breakpoint == xl { @media (min-width: $xl) { @content; } }
}

// Vazifa 3: Gradient mixin
@mixin gradient($boshlanish, $tugash, $burchak: 135deg) {
  background: linear-gradient($burchak, $boshlanish, $tugash);
}

// Vazifa 4: Truncate (matn qisqartirish)
@mixin qisqartir($qatorlar: 1) {
  @if $qatorlar == 1 {
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
  } @else {
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-line-clamp: $qatorlar;
    overflow: hidden;
  }
}

/* ======= _components.scss ======= */
@use "variables" as *;
@use "mixins" as *;

// Vazifa 5: Tugmalar @each bilan
$tugma-ranglar: (
  asosiy: ($rang-asosiy, white),
  ikkilamchi: (#e2e8f0, #1a1a2e),
  xavfli: ($rang-xavfli, white),
  muvaffaq: ($rang-muvaffaq, #1a1a2e)
);

%tugma-baza {
  padding: 10px 22px;
  border: none;
  border-radius: $radius-md;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.2s;
  &:hover { transform: translateY(-2px); filter: brightness(1.1); }
  &:active { transform: translateY(0); }
}

@each $nom, $qiymatlar in $tugma-ranglar {
  $fon: nth($qiymatlar, 1);
  $matn: nth($qiymatlar, 2);
  .btn-#{$nom} {
    @extend %tugma-baza;
    background: $fon;
    color: $matn;
  }
}

// Vazifa 6: Karta komponenti
.karta {
  background: white;
  border-radius: $radius-lg;
  box-shadow: $soya-md;
  overflow: hidden;
  transition: transform 0.3s, box-shadow 0.3s;
  
  &:hover {
    transform: translateY(-6px);
    box-shadow: $soya-lg;
  }
  
  &__rasm {
    width: 100%;
    height: 220px;
    object-fit: cover;
    display: block;
  }
  
  &__tana { padding: 24px; }
  
  &__sarlavha {
    font-family: $font-sarlavha;
    font-size: 1.25rem;
    margin-bottom: 8px;
    @include qisqartir(2);
  }
  
  &__tavsif {
    color: #666;
    font-size: $font-kichik;
    line-height: 1.6;
    @include qisqartir(3);
  }
  
  // Sizes
  &--kichik { .karta__rasm { height: 160px; } }
  &--katta   { .karta__rasm { height: 300px; } }
  
  // Themes
  &--qorongu {
    background: #16213e;
    color: white;
    .karta__tavsif { color: rgba(255,255,255,0.7); }
  }
}

// Vazifa 7-10: Grid va Responsive
.grid-sistema {
  display: grid;
  grid-template-columns: 1fr;
  gap: 20px;
  
  @include bp(sm) { grid-template-columns: repeat(2, 1fr); }
  @include bp(lg) { grid-template-columns: repeat(3, 1fr); }
  @include bp(xl) { grid-template-columns: repeat(4, 1fr); }
}

/* ======= style.scss (asosiy) ======= */
@use "variables" as *;
@use "mixins" as *;
@use "components";

*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
body { font-family: $font-asosiy; color: #1a1a2e; background: #f0f2f5; }

.sahifa { max-width: 1200px; margin: 0 auto; padding: 40px 20px; }

// Spacing utilities (Vazifa 9)
@for $i from 1 through 10 {
  .mt-#{$i} { margin-top: #{$i * 8}px; }
  .mb-#{$i} { margin-bottom: #{$i * 8}px; }
  .p-#{$i}  { padding: #{$i * 8}px; }
}

// Rang utilities (Vazifa 10)
$rang-lar: (asosiy: $rang-asosiy, ikkilamchi: $rang-ikkilamchi,
            xavfli: $rang-xavfli, muvaffaq: $rang-muvaffaq);
@each $nom, $rang in $rang-lar {
  .text-#{$nom} { color: $rang; }
  .bg-#{$nom} { background: $rang; }
}
```
