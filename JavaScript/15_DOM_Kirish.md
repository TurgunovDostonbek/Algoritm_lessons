# 15-Dars: DOM ga Kirish

## 📌 DOM nima?

**DOM (Document Object Model)** — HTML hujjatining dasturlash interfeysi. Brauzer HTML ni o'qib, uni JavaScript orqali boshqarish mumkin bo'lgan daraxtsimon tuzilmaga aylantiradi.

```
window
└── document
    └── html
        ├── head
        │   └── title
        └── body
            ├── h1 ("Salom")
            ├── p ("Paragraf")
            └── div#app
                └── ul
                    ├── li ("1-element")
                    └── li ("2-element")
```

---

## 📌 Element Tanlash Metodlari

### `document.querySelector()` — CSS selektor bilan

```javascript
// Birinchi mos elementni qaytaradi
let sarlavha = document.querySelector("h1");
let tugma = document.querySelector("#submit-btn"); // ID bo'yicha
let klass = document.querySelector(".menu-item"); // Klass bo'yicha
let ichki = document.querySelector("ul li:first-child"); // Ichki selektor

// Topilmasa — null
let yoq = document.querySelector(".mavjud-emas"); // null
if (yoq) { /* foydalaning */ }
```

### `document.querySelectorAll()` — Barcha mos elementlar

```javascript
// NodeList qaytaradi (massivga o'xshash)
let barcha_li = document.querySelectorAll("li");
let barcha_tugmalar = document.querySelectorAll(".btn");

// NodeList ustida aylanish
barcha_li.forEach(li => {
  console.log(li.textContent);
});

// Massivga aylantirish
let massiv = Array.from(barcha_li);
// yoki [...barcha_li]
```

### `document.getElementById()` — ID bo'yicha

```javascript
let el = document.getElementById("app"); // "#" kerak emas!
let el2 = document.getElementById("submit-btn");

// querySelector dan farqi: faqat ID qidiradi, tezroq
```

### `document.getElementsByClassName()` — Klass bo'yicha

```javascript
let elementlar = document.getElementsByClassName("menu-item");
// HTMLCollection qaytaradi — LIVE (o'zgarib turadi!)

// getElementsByTagName
let barcha_p = document.getElementsByTagName("p");
```

---

## 📌 Element Xususiyatlari

### `textContent` va `innerHTML`

```javascript
let div = document.querySelector("#app");

// textContent — faqat matn (xavfsiz)
console.log(div.textContent); // "Matn"
div.textContent = "<b>Yangi matn</b>"; // HTML ko'rsatilmaydi, matn sifatida

// innerHTML — HTML bilan birga (XSS xavfi bor!)
console.log(div.innerHTML); // "<p>Matn</p>"
div.innerHTML = "<strong>Yangi HTML</strong>"; // HTML ishlaydi

// innerText — ko'rinuvchi matn (CSS ga bog'liq)
console.log(div.innerText);
```

### `style` — Stil o'zgartirish

```javascript
let el = document.querySelector("p");

// Inline style orqali
el.style.color = "red";
el.style.fontSize = "20px";       // camelCase!
el.style.backgroundColor = "yellow";
el.style.display = "none";        // yashirish

// Qaytarish
el.style.display = "";            // Inline stili olib tashlash
```

### `classList` — Class boshqarish

```javascript
let el = document.querySelector(".box");

el.classList.add("active");      // klass qo'shish
el.classList.remove("hidden");   // klass olib tashlash
el.classList.toggle("dark");     // bor bo'lsa o'chir, yo'q bo'lsa qo'sh
el.classList.contains("active"); // true/false
el.classList.replace("old", "new"); // almashtirish

console.log(el.classList);       // DOMTokenList
```

### Atributlar

```javascript
let img = document.querySelector("img");

// Olish
img.getAttribute("src");   // "/images/rasm.jpg"
img.getAttribute("alt");   // "Rasm tavsifi"

// O'rnatish
img.setAttribute("src", "/new-rasm.jpg");
img.setAttribute("alt", "Yangi rasm");

// O'chirish
img.removeAttribute("title");

// Tekshirish
img.hasAttribute("src"); // true

// data-* atributlar
let div = document.querySelector("[data-id]");
console.log(div.dataset.id);      // data-id qiymati
console.log(div.dataset.userId);  // data-user-id qiymati
```

---

## 📌 Element Yaratish va DOM ga Qo'shish

```javascript
// Yangi element yaratish
let yangiP = document.createElement("p");
yangiP.textContent = "Bu yangi paragraf!";
yangiP.classList.add("highlight");

let container = document.querySelector("#container");

// Qo'shish usullari
container.appendChild(yangiP);              // Oxiriga qo'shish
container.prepend(yangiP);                  // Boshiga qo'shish
container.insertAdjacentElement("beforeend", yangiP); // Aniq joy
container.insertAdjacentHTML("beforeend", "<p>HTML string</p>"); // HTML dan
```

---

## 📌 Element O'chirish va Almashtirish

```javascript
let container = document.querySelector("#list");
let element = document.querySelector("#item-2");

// O'chirish
element.remove();                          // Zamonaviy
// container.removeChild(element);         // Eski usul

// Almashtirish
let yangi = document.createElement("li");
yangi.textContent = "Yangi element";
// container.replaceChild(yangi, element); // Eski
element.replaceWith(yangi);               // Zamonaviy
```

---

## 📌 DOM Traversal (Harakatlanish)

```javascript
let el = document.querySelector(".target");

// Ota (Parent)
console.log(el.parentElement);
console.log(el.parentNode);

// Bolalar (Children)
console.log(el.children);          // HTMLCollection (faqat elementlar)
console.log(el.childNodes);        // NodeList (matn tugunlari ham)
console.log(el.firstElementChild); // Birinchi bola element
console.log(el.lastElementChild);  // Oxirgi bola element

// Qo'shni (Siblings)
console.log(el.nextElementSibling);
console.log(el.previousElementSibling);
```

---

## 📌 `querySelector` vs `getElementById` — Qachon nimani ishlatish?

| Metod                      | Tezlik    | Moslashuvchanlik | Qaytarish  |
|----------------------------|-----------|------------------|------------|
| `getElementById`           | ⚡ Tez    | Faqat ID         | Element    |
| `querySelector`            | 🐢 Sekin  | Har qanday CSS   | Element    |
| `querySelectorAll`         | 🐢 Sekin  | Har qanday CSS   | NodeList   |
| `getElementsByClassName`  | ⚡ Tez    | Klass            | HTMLCollection |

---

## 🎯 10 ta Amaliy Vazifa

```html
<!-- HTML tuzilma (asos) -->
<!DOCTYPE html>
<html>
<head>
  <title>DOM Amaliyot</title>
  <style>
    .highlight { background: yellow; }
    .hidden { display: none; }
    .active { color: red; font-weight: bold; }
  </style>
</head>
<body>
  <h1 id="sarlavha">Salom DOM!</h1>
  <p class="tavsif">Bu asosiy paragraf.</p>
  <ul id="royxat">
    <li>Birinchi</li>
    <li>Ikkinchi</li>
    <li>Uchinchi</li>
  </ul>
  <button id="tugma">Bosing</button>
  <img src="rasm.jpg" alt="Rasm" id="img">
  <div id="container"></div>

  <script>
  // 1. h1 matnini o'zgartiring
  document.getElementById("sarlavha").textContent = "Yangi Sarlavha!";

  // 2. .tavsif paragrafiga "highlight" klassini qo'shing
  document.querySelector(".tavsif").classList.add("highlight");

  // 3. Ro'yxatning barcha li larini aylanib, matnlarini katta harfga
  document.querySelectorAll("#royxat li").forEach(li => {
    li.textContent = li.textContent.toUpperCase();
  });

  // 4. Yangi li element yaratib ro'yxatga qo'shing
  let yangiLi = document.createElement("li");
  yangiLi.textContent = "To'rtinchi";
  document.getElementById("royxat").appendChild(yangiLi);

  // 5. img ning src va alt atributlarini o'zgartiring
  let img = document.getElementById("img");
  img.setAttribute("src", "yangi-rasm.jpg");
  img.setAttribute("alt", "Yangi rasm tavsifi");

  // 6. Tugma bosilganda p ni yashiring/ko'rsating (toggle)
  document.getElementById("tugma").addEventListener("click", function() {
    document.querySelector(".tavsif").classList.toggle("hidden");
  });

  // 7. container ga 5 ta div yarating (1-5 raqamlar bilan)
  let konteyner = document.getElementById("container");
  for (let i = 1; i <= 5; i++) {
    let div = document.createElement("div");
    div.textContent = i;
    div.style.padding = "10px";
    div.style.margin = "5px";
    div.style.background = `hsl(${i * 60}, 70%, 80%)`;
    konteyner.appendChild(div);
  }

  // 8. Ro'yxatning oxirgi elementini o'chiring
  let royxat = document.getElementById("royxat");
  royxat.lastElementChild.remove();

  // 9. Barcha li larga click event qo'shing — bosilganda "active" klass
  document.querySelectorAll("#royxat li").forEach(li => {
    li.addEventListener("click", function() {
      // Avvalgi active ni olib tashlash
      document.querySelectorAll("#royxat li").forEach(l => l.classList.remove("active"));
      // Yangi qo'shish
      this.classList.add("active");
    });
  });

  // 10. p ning ota elementini va qo'shni elementini toping
  let p = document.querySelector(".tavsif");
  console.log("Ota:", p.parentElement.tagName);
  console.log("Oldingi:", p.previousElementSibling?.tagName);
  console.log("Keyingi:", p.nextElementSibling?.tagName);
  </script>
</body>
</html>
```
