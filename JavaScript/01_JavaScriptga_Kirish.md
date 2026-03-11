# 1-Dars: JavaScriptga Kirish

## 📌 JavaScript nima?

**JavaScript** — bu veb-sahifalarni interaktiv qilish uchun ishlatiladigan dasturlash tili. U brauzer ichida ishlaydi va HTML hamda CSS bilan birga veb-ilovalar yaratishda asosiy vosita hisoblanadi.

- **HTML** → Tuzilma (Struktura)
- **CSS** → Ko'rinish (Dizayn)
- **JavaScript** → Xatti-harakat (Interaktivlik)

```html
<!-- Misol: Tugma bosilganda alert chiqarish -->
<button onclick="alert('Salom, Dunyo!')">Bosing</button>
```

---

## 📌 JavaScript tarixi va ECMAScript versiyalari

| Yil  | Versiya         | Muhim yangiliklar                            |
|------|-----------------|----------------------------------------------|
| 1995 | JavaScript 1.0  | Brendan Eich tomonidan 10 kunda yaratildi     |
| 1997 | ES1 (ECMAScript)| Standartlashtirildi                          |
| 2009 | ES5             | `strict mode`, `JSON`, `Array` metodlari     |
| 2015 | ES6 / ES2015    | `let`, `const`, arrow functions, class, `...`|
| 2016+| ES7, ES8...     | `async/await`, optional chaining va boshqalar|

> **ECMAScript** — bu JavaScriptning rasmiy standarti. JavaScript ECMAScript ning eng mashhur implementatsiyasi hisoblanadi.

---

## 📌 JavaScript qanday ishlaydi?

### Bajarilish Konteksti (Execution Context)

JavaScript kodi ishlaganda **Execution Context** yaratiladi. Uning 2 turi bor:

1. **Global Execution Context (GEC)** — dastur boshlanganda yaratiladi
2. **Function Execution Context (FEC)** — har bir funksiya chaqirilganda yaratiladi

```
Global Execution Context
├── Memory Phase (Creation Phase)  → o'zgaruvchilar xotiraga olinadi
└── Execution Phase                → kod qator-qator bajariladi
```

### Chaqiruv Steki (Call Stack)

**Call Stack** — bu JavaScript qaysi funksiya bajarilayotganini kuzatib boruvchi mexanizm.

```javascript
function birinchi() {
  ikkinchi();
}

function ikkinchi() {
  console.log("Salom!");
}

birinchi();

// Call Stack:
// 1. birinchi() → stack ga qo'shiladi
// 2. ikkinchi() → stack ga qo'shiladi
// 3. ikkinchi() tugaydi → stack dan chiqariladi
// 4. birinchi() tugaydi → stack dan chiqariladi
```

---

## 📌 HTML ichida JavaScript yozish

### 1. `<script>` tegi orqali (Inline)

```html
<!DOCTYPE html>
<html>
<head>
  <title>JS Misol</title>
</head>
<body>
  <h1>Salom!</h1>

  <script>
    console.log("Bu inline JavaScript!");
  </script>
</body>
</html>
```

### 2. Tashqi fayl orqali (External)

```html
<!-- index.html -->
<script src="script.js"></script>
```

```javascript
// script.js
console.log("Bu tashqi JavaScript fayli!");
```

> ✅ **Tavsiya:** JavaScript faylini `<body>` ning oxiriga yozing — sahifa tezroq yuklansun.

---

## 📌 Variable (O'zgaruvchi) lar bilan tanishuv

O'zgaruvchi — ma'lumotni saqlash uchun ishlatiladigan "quti".

### E'lon qilish usullari

| Kalit so'z | Qayta belgilash | Qayta e'lon | Scope    |
|------------|-----------------|-------------|----------|
| `var`      | ✅ Ha           | ✅ Ha       | Function |
| `let`      | ✅ Ha           | ❌ Yo'q     | Block    |
| `const`    | ❌ Yo'q         | ❌ Yo'q     | Block    |

```javascript
// var - eski usul (ishlatmaslik tavsiya etiladi)
var ism = "Ali";
var ism = "Vali"; // xato yo'q, lekin muammo!

// let - o'zgaruvchi uchun
let yosh = 20;
yosh = 25; // OK ✅

// const - o'zgarmaydigan qiymat uchun
const PI = 3.14;
// PI = 3.15; // ❌ Xato!
```

### Nomlash qoidalari

```javascript
// ✅ To'g'ri nomlar
let userName = "Ali";
let _count = 0;
let $price = 100;

// ❌ Noto'g'ri nomlar
// let 1name = "Ali";   → raqam bilan boshlanmaydi
// let user-name = "";  → defis ishlatilmaydi
// let let = "kalit";  → kalit so'z ishlatilmaydi
```

---

## 🎯 Amaliy Vazifa

1. W3School.com da JavaScript bo'limini o'qib chiqing
2. Quyidagi 20 ta o'zgaruvchini e'lon qilib, misollar yozing:

```javascript
// Shaxsiy ma'lumotlar
const firstName = "Sizning ismingiz";
const lastName = "Familiyangiz";
let age = 20;
const birthYear = 2004;
let city = "Toshkent";

// Sonlar
let temperature = 36.6;
const maxScore = 100;
let currentScore = 85;

// Mantiqiy
let isStudent = true;
let isWorking = false;

// Satrlar
let greeting = "Assalomu alaykum";
let message = `Mening ismim ${firstName}`;

// va hokazo...
console.log(firstName, lastName, age);
```

---

> 📝 **Eslatma:** Har doim `let` va `const` ishlating. `var` dan foydalanmang!
