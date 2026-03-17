# 01-Dars: Kirish — Kompyuter, Editor, Browser

## 📌 Web Dasturlash nima?

**Web dasturlash** — brauzerda ko'rinadigan sahifalarni yaratish san'ati.

```
Web technologies uchburchagi:
├── HTML  → Tarkib (Struktura)
├── CSS   → Ko'rinish (Dizayn)
└── JS    → Xulq-atvor (Interaktivlik)
```

---

## 📌 Web umumiy ma'lumot

```
Brauzer qanday ishlaydi?
1. Foydalanuvchi URL kiritadi: https://google.com
2. DNS server — domen nomini IP manzilga aylantiradi
3. Brauzer serverga HTTP so'rov yuboradi
4. Server HTML, CSS, JS fayllarini qaytaradi
5. Brauzer fayllarni tahlil qilib sahifani ko'rsatadi

Client ←──── Server
  ↑              │
  │    HTML      │
  │    CSS       │
  └──── JS ──────┘
```

---

## 📌 HTML, CSS, JavaScript — Misollar

```html
<!-- HTML — Tarkib -->
<h1>Salom Dunyo!</h1>
<p>Bu birinchi veb sahifam.</p>
<button>Bosing</button>
```

```css
/* CSS — Ko'rinish */
h1 { color: royalblue; font-size: 48px; }
p  { color: #555; line-height: 1.6; }
button { background: royalblue; color: white; padding: 12px 24px; }
```

```javascript
// JavaScript — Interaktivlik
document.querySelector("button").addEventListener("click", () => {
  alert("Tugma bosildi!");
});
```

---

## 📌 Tag haqida umumiy ma'lumot

```html
<!-- Tag sintaksisi -->
<tagNomi atribut="qiymat">Kontent</tagNomi>

<!-- Misol -->
<a href="https://google.com" target="_blank">Google</a>

<!-- Anatomiya:
  <a          → Ochuvchi tag
  href="..."  → Atribut (ism="qiymat")
  target=...  → Ikkinchi atribut
  >           → Tag tugashi
  Google      → Kontent
  </a>        → Yopuvchi tag
-->
```

---

## 📌 Editor — VS Code o'rnatish va Sozlash

```
VS Code uchun zarur extensionlar:
├── Live Server      → Sahifani brauzerda ochish
├── Prettier         → Kodni chiroyli formatlash
├── Auto Rename Tag  → Tag nomini o'zgartirganda juftini ham
├── HTML CSS Support → CSS class autocomplete
├── GitLens          → Git tarixini ko'rish
└── Material Icon Theme → Chiroyli ikonkalar
```

```
Foydali VS Code Shortcutlar:
Ctrl + S        → Saqlash
Ctrl + Z        → Bekor qilish
Ctrl + Shift+P  → Command palette
Alt + Shift + F → Formatlash (Prettier)
! + Tab         → HTML boilerplate (Emmet)
Ctrl + /        → Izoh qo'shish/olib tashlash
Alt + ↑/↓       → Qatorni ko'chirish
Ctrl + D        → Keyingi mos so'zni tanlash
```

---

## 📌 W3School va MDN — Resurslar

```
Asosiy o'rganish resurslari:
├── https://developer.mozilla.org  → MDN (Eng to'liq)
├── https://www.w3schools.com      → W3Schools (Sodda)
├── https://css-tricks.com         → CSS maslahatlar
└── https://caniuse.com            → Brauzer muvofiqlik

Mashq qilish:
├── https://codepen.io             → Online kod muhit
├── https://jsfiddle.net           → JS sinov
└── https://developer.chrome.com  → Chrome DevTools
```

---

## 🎯 10 ta Amaliy Vazifa

### Vazifa 1: "Hello, World!" sahifasi
```html
<!DOCTYPE html>
<html lang="uz">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Salom Dunyo</title>
</head>
<body>
  <h1>Salom, Dunyo! 👋</h1>
  <p>Bu mening birinchi HTML sahifam.</p>
</body>
</html>
```

### Vazifa 2: Shaxsiy vizit karta
```html
<!DOCTYPE html>
<html lang="uz">
<head>
  <meta charset="UTF-8">
  <title>Vizit Karta</title>
  <style>
    body { font-family: Arial, sans-serif; max-width: 600px; margin: 40px auto; padding: 20px; }
    h1 { color: royalblue; }
    .info { background: #f0f4ff; padding: 20px; border-radius: 10px; }
  </style>
</head>
<body>
  <div class="info">
    <h1>Ali Valiev</h1>
    <p>📧 ali@mail.com</p>
    <p>📞 +998 90 123 45 67</p>
    <p>💼 Junior Frontend Developer</p>
    <p>🏠 Toshkent, O'zbekiston</p>
  </div>
</body>
</html>
```

### Vazifa 3: W3School dan o'rganing
```
1. https://www.w3schools.com/html/ sahifasini oching
2. "HTML Introduction" ni o'qing
3. "Try it Yourself" tugmasini bosib kod sinab ko'ring
4. "HTML Editors" bo'limini o'qing
```

### Vazifa 4: Wikipedia vazifa
```
1. https://en.wikipedia.org/wiki/Avicenna sahifasini oching
2. Sahifadagi: Sarlavha (h1), havolalar (a), rasmlar (img) larni toping
3. Brauzerda F12 (DevTools) ni oching
4. Elements panelida sahifa strukturasini ko'ring
```

### Vazifa 5: DevTools bilan tanishish
```
Chrome DevTools:
1. F12 → Elements paneli → HTML ni ko'ring
2. Console → "console.log('Salom!')" yozing
3. Network → Sahifani yangilang → Yuklanayotgan fayllarni ko'ring
4. Biror element ustida Right Click → Inspect
```

### Vazifa 6: VS Code sozlash
```
1. VS Code o'rnating (code.visualstudio.com)
2. Extensions (Ctrl+Shift+X):
   - "Live Server" o'rnating
   - "Prettier" o'rnating
3. Yangi fayl: index.html
4. ! + Tab bosing → Boilerplate yarating
5. Live Server bilan oching (Alt + L, Alt + O)
```

### Vazifa 7: Birinchi loyiha papkasi
```
Fayl tuzilmasi:
mening-saytim/
├── index.html     ← Bosh sahifa
├── haqida.html    ← Haqimda
├── aloqa.html     ← Aloqa
├── css/
│   └── style.css  ← Stilllar
└── images/        ← Rasmlar
```

### Vazifa 8: Sahifalar o'rtasida havolalar
```html
<!-- index.html -->
<nav>
  <a href="index.html">Bosh sahifa</a>
  <a href="haqida.html">Haqimda</a>
  <a href="aloqa.html">Aloqa</a>
</nav>
```

### Vazifa 9: Paragraph va Heading taglar
```html
<h1>Eng katta sarlavha</h1>
<h2>Ikkinchi darajali</h2>
<h3>Uchinchi darajali</h3>
<h4>To'rtinchi darajali</h4>
<h5>Beshinchi darajali</h5>
<h6>Oltinchi darajali</h6>

<p>Bu oddiy paragraf matni.</p>
<p>Bu ikkinchi paragraf. <br> Bu yangi qator.</p>
```

### Vazifa 10: HTML + CSS + JS birgalikda
```html
<!DOCTYPE html>
<html lang="uz">
<head>
  <meta charset="UTF-8">
  <title>Interaktiv Sahifa</title>
  <style>
    body { text-align: center; font-family: Arial; padding: 50px; }
    h1 { color: royalblue; }
    button {
      padding: 12px 28px; background: royalblue; color: white;
      border: none; border-radius: 8px; font-size: 16px; cursor: pointer;
    }
    button:hover { background: navy; }
    #natija { margin-top: 20px; font-size: 24px; }
  </style>
</head>
<body>
  <h1>Mening birinchi interaktiv sahifam</h1>
  <button onclick="salomlash()">Salom ayt!</button>
  <div id="natija"></div>

  <script>
    function salomlash() {
      const ism = prompt("Ismingiz nima?");
      document.getElementById("natija").textContent = `Salom, ${ism}! 🎉`;
    }
  </script>
</body>
</html>
```
