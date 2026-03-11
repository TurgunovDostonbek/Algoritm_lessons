# 4-Dars: Conditional Statements (Shartli Operatorlar)

## 📌 Conditional Statements nima?

**Shartli operatorlar** — ma'lum bir shart bajarilganida yoki bajarilmaganida turli kod bloklarini ishlatish imkonini beradi.

```
Shartli Operatorlar
├── if
├── if-else
├── if-else if-else
├── switch-case
└── Ternary Operator (? :)
```

---

## 📌 Truthy va Falsy Qiymatlar

JavaScript da har qanday qiymat `if` shart ichida `true` yoki `false` ga aylanadi.

### Falsy qiymatlar (false ga aylanadi):

```javascript
if (false)     console.log("bajarilmaydi");
if (0)         console.log("bajarilmaydi");
if (-0)        console.log("bajarilmaydi");
if ("")        console.log("bajarilmaydi");
if (null)      console.log("bajarilmaydi");
if (undefined) console.log("bajarilmaydi");
if (NaN)       console.log("bajarilmaydi");
```

### Truthy qiymatlar (true ga aylanadi):

```javascript
if (true)      console.log("bajariladi");
if (1)         console.log("bajariladi");
if (-1)        console.log("bajariladi");
if ("salom")   console.log("bajariladi");
if ("0")       console.log("bajariladi"); // "0" string — truthy!
if ([])        console.log("bajariladi"); // bo'sh massiv — truthy!
if ({})        console.log("bajariladi"); // bo'sh ob'ekt — truthy!
```

---

## 📌 if Operatori

Shart bajarilsa (`true`), blok ichidagi kod ishlaydi.

```javascript
let yosh = 20;

if (yosh >= 18) {
  console.log("Siz voyaga yetgansiz"); // ✅ bajariladi
}
```

---

## 📌 if-else Operatori

Shart `true` bo'lsa birinchi blok, `false` bo'lsa ikkinchi blok ishlaydi.

```javascript
let yosh = 15;

if (yosh >= 18) {
  console.log("Siz voyaga yetgansiz");
} else {
  console.log("Siz voyaga yetmagansiz"); // ✅ bu bajariladi
}
```

**Amaliy misollar:**

```javascript
// Toq/Juft tekshirish
let son = 7;

if (son % 2 === 0) {
  console.log(`${son} juft son`);
} else {
  console.log(`${son} toq son`); // ✅
}

// Login tekshirish
let foydalanuvchi = "admin";
let parol = "1234";

if (foydalanuvchi === "admin" && parol === "1234") {
  console.log("Xush kelibsiz!"); // ✅
} else {
  console.log("Login yoki parol noto'g'ri");
}
```

---

## 📌 if-else if-else Operatori

Bir nechta shartni ketma-ket tekshirish uchun.

```javascript
let ball = 75;

if (ball >= 90) {
  console.log("A'lo (5)");
} else if (ball >= 70) {
  console.log("Yaxshi (4)");    // ✅ bu bajariladi
} else if (ball >= 55) {
  console.log("Qoniqarli (3)");
} else {
  console.log("Qoniqarsiz (2)");
}
```

**Fasl aniqlash:**

```javascript
let oy = 7;
let fasl;

if (oy >= 3 && oy <= 5) {
  fasl = "Bahor";
} else if (oy >= 6 && oy <= 8) {
  fasl = "Yoz";          // ✅
} else if (oy >= 9 && oy <= 11) {
  fasl = "Kuz";
} else {
  fasl = "Qish";
}

console.log(`Joriy fasl: ${fasl}`); // "Joriy fasl: Yoz"
```

---

## 📌 switch-case Operatori

Bir o'zgaruvchini bir nechta aniq qiymat bilan solishtirish uchun qulay.

### Sintaksis:

```javascript
switch (ifoda) {
  case qiymat1:
    // kod
    break;
  case qiymat2:
    // kod
    break;
  default:
    // hech bir case mos kelmasa
}
```

**Misol — Haftaning kuni:**

```javascript
let kun = 3;
let kunNomi;

switch (kun) {
  case 1:
    kunNomi = "Dushanba";
    break;
  case 2:
    kunNomi = "Seshanba";
    break;
  case 3:
    kunNomi = "Chorshanba"; // ✅
    break;
  case 4:
    kunNomi = "Payshanba";
    break;
  case 5:
    kunNomi = "Juma";
    break;
  case 6:
    kunNomi = "Shanba";
    break;
  case 7:
    kunNomi = "Yakshanba";
    break;
  default:
    kunNomi = "Noto'g'ri kun";
}

console.log(kunNomi); // "Chorshanba"
```

> ⚠️ **Muhim:** `break` ni unutmang! `break` bo'lmasa quyidagi case lar ham bajariladi ("fall-through").

**Fall-through misoli (ba'zan foydali):**

```javascript
let daraja = "B";

switch (daraja) {
  case "A":
  case "B":
    console.log("Yaxshi natija"); // A yoki B bo'lsa bajariladi ✅
    break;
  case "C":
    console.log("O'rtacha natija");
    break;
  default:
    console.log("Yaxshilash kerak");
}
```

---

## 📌 Ternary Operator (Uchlik Operator)

`if-else` ning qisqa shakli. Oddiy shartlar uchun qulay.

### Sintaksis:

```javascript
shart ? qiymat_if_true : qiymat_if_false
```

**Misollar:**

```javascript
let yosh = 20;

// Oddiy if-else
let holat;
if (yosh >= 18) {
  holat = "Katta";
} else {
  holat = "Kichik";
}

// Ternary bilan (bir qatorda!)
let holat2 = yosh >= 18 ? "Katta" : "Kichik";

console.log(holat2); // "Katta" ✅
```

**Ko'proq misollar:**

```javascript
// Toq/Juft
let son = 14;
console.log(son % 2 === 0 ? "Juft" : "Toq"); // "Juft"

// Maksimal son
let a = 5, b = 10;
let max = a > b ? a : b;
console.log(max); // 10

// Login
let loggedIn = true;
let habar = loggedIn ? "Kabinet" : "Kirish sahifasi";
console.log(habar); // "Kabinet"
```

**Zanjirli ternary (ehtiyot bo'ling):**

```javascript
let ball = 75;
let daraja = ball >= 90 ? "A'lo" 
           : ball >= 70 ? "Yaxshi"
           : ball >= 55 ? "Qoniqarli"
           : "Qoniqarsiz";

console.log(daraja); // "Yaxshi"
```

---

## 📌 if vs switch vs Ternary — Qachon ishlatish?

| Holat                              | Tavsiya         |
|------------------------------------|-----------------|
| 1-2 ta shart                      | `if-else`       |
| Ko'p aniq qiymatlar taqqoslash     | `switch-case`   |
| Oddiy ikki tanlov, qiymat kerak    | `Ternary`       |
| Murakkab mantiq                    | `if-else if`    |

---

## 🎯 Amaliy Vazifa

```javascript
// 1. Sonni manfiy, nol yoki musbat ekanligini aniqlang
let son = -5;
// yechim...

// 2. switch-case bilan oyni faslga aylantiring
let oy = 4;
// 3-5 → Bahor, 6-8 → Yoz, 9-11 → Kuz, 12,1,2 → Qish

// 3. Ternary bilan eng katta sonni toping (3 ta son)
let x = 10, y = 25, z = 18;
// eng_katta = ?

// 4. Foydalanuvchi yoshiga qarab kategoriya aniqlang
// 0-12: Bola, 13-17: O'smir, 18-64: Kattalar, 65+: Keksa
let foydalanuvchi_yoshi = 35;
```

> 📝 **Eslatma:** `switch-case` da `===` (aniq taqqoslash) ishlatiladi, shuning uchun `switch("3")` va `case 3:` mos kelmaydi!
