# 3-Dars: Operatorlar & Type Conversion

## 📌 Operatorlar nima?

Operator — qiymatlar ustida amal bajaruvchi belgi yoki kalit so'z.

```
Operatorlar
├── Aritmetik operatorlar
├── Taqqoslash operatorlari
├── Mantiqiy operatorlar
├── Tayinlash operatorlari
├── Qisqa tutashuv operatorlari
└── Boshqa operatorlar
```

---

## 📌 Aritmetik Operatorlar

```javascript
let a = 10;
let b = 3;

console.log(a + b);  // 13  → qo'shish
console.log(a - b);  // 7   → ayirish
console.log(a * b);  // 30  → ko'paytirish
console.log(a / b);  // 3.333... → bo'lish
console.log(a % b);  // 1   → qoldiq (modulo)
console.log(a ** b); // 1000 → daraja (ES6)

// Increment va Decrement
let x = 5;
console.log(x++); // 5 — avval qaytaradi, keyin oshiradi
console.log(x);   // 6
console.log(++x); // 7 — avval oshiradi, keyin qaytaradi

let y = 5;
console.log(y--); // 5 — avval qaytaradi, keyin kamaytiradi
console.log(--y); // 3 — avval kamaytiradi, keyin qaytaradi
```

**String bilan "+" operatori:**

```javascript
console.log("Salom" + " " + "Dunyo"); // "Salom Dunyo" → birlashtirish
console.log("5" + 3);   // "53" → string bo'ladi!
console.log("5" - 3);   // 2   → number bo'ladi
console.log("5" * "3"); // 15  → number bo'ladi
```

---

## 📌 Taqqoslash Operatorlari

```javascript
let a = 5;
let b = "5";

// Qiymat bo'yicha taqqoslash (noaniq)
console.log(a == b);   // true  → faqat qiymat tekshiradi
console.log(a != b);   // false

// Qiymat VA tur bo'yicha taqqoslash (aniq)
console.log(a === b);  // false → qiymat VA tur tekshiradi
console.log(a !== b);  // true

// Katta-kichik taqqoslash
console.log(5 > 3);    // true
console.log(5 < 3);    // false
console.log(5 >= 5);   // true
console.log(5 <= 4);   // false
```

> ⚠️ **Tavsiya:** Har doim `===` va `!==` ishlating! `==` kutilmagan natijalar berishi mumkin.

---

## 📌 Mantiqiy Operatorlar

```javascript
// && (AND — VA) — ikkisi ham true bo'lsa true
console.log(true && true);   // true
console.log(true && false);  // false
console.log(false && true);  // false

// || (OR — YOKI) — biri true bo'lsa true
console.log(true || false);  // true
console.log(false || false); // false

// ! (NOT — EMAS) — teskarisini qaytaradi
console.log(!true);   // false
console.log(!false);  // true

// Amaliy misol
let yosh = 20;
let isStudent = true;

if (yosh >= 18 && isStudent) {
  console.log("Talaba va voyaga yetgan");
}
```

---

## 📌 Tayinlash Operatorlari

```javascript
let x = 10;

x += 5;   // x = x + 5  → 15
x -= 3;   // x = x - 3  → 12
x *= 2;   // x = x * 2  → 24
x /= 4;   // x = x / 4  → 6
x %= 4;   // x = x % 4  → 2
x **= 3;  // x = x ** 3 → 8

console.log(x); // 8
```

---

## 📌 Operatorlarning Ustuvorligi (Precedence)

Yuqoriroq ustuvorlik — avval bajariladi.

| Tartib | Operator                   | Misol          |
|--------|----------------------------|----------------|
| 1 (yuqori) | `()` — qavslar        | `(2 + 3) * 4`  |
| 2      | `**` — daraja             | `2 ** 3`       |
| 3      | `*`, `/`, `%`             | `6 / 2 * 3`    |
| 4      | `+`, `-`                  | `5 + 3 - 2`    |
| 5      | `<`, `>`, `<=`, `>=`      | `5 > 3`        |
| 6      | `==`, `!=`, `===`, `!==`  | `5 === 5`      |
| 7      | `&&`                      | `a && b`       |
| 8      | `\|\|`                    | `a \|\| b`     |
| 9 (past) | `=`, `+=`, `-=` ...     | `x = 5`        |

```javascript
// Ustuvorlik misoli
console.log(2 + 3 * 4);     // 14 (ko'paytirish avval)
console.log((2 + 3) * 4);   // 20 (qavslar avval)
console.log(2 ** 3 ** 2);   // 512 (o'ngdan chapga)
```

---

## 📌 Qisqa Tutashuv (Short-Circuit) Operatorlari

### `&&` — Birinchi yolg'on qiymatni qaytaradi

```javascript
console.log(1 && 2);        // 2   → ikkalasi ham true, oxirgisini qaytaradi
console.log(0 && "salom");  // 0   → 0 falsy, to'xtaydi
console.log(null && 5);     // null

// Amaliy foydalanish
let foydalanuvchi = { ism: "Ali" };
console.log(foydalanuvchi && foydalanuvchi.ism); // "Ali"
```

### `||` — Birinchi rost qiymatni qaytaradi

```javascript
console.log(0 || "zahira");     // "zahira" → 0 falsy, keyingisini qaytaradi
console.log("Ali" || "zahira"); // "Ali"    → "Ali" truthy, to'xtaydi
console.log(null || undefined); // undefined

// Standart qiymat berish
let ism = "";
let korinuvchi_ism = ism || "Mehmon";
console.log(korinuvchi_ism); // "Mehmon"
```

### `??` — Nullish Coalescing (ES2020)

```javascript
// Faqat null va undefined uchun zahira qiymat
console.log(null ?? "zahira");      // "zahira"
console.log(undefined ?? "zahira"); // "zahira"
console.log(0 ?? "zahira");         // 0 (0 falsy lekin null/undefined emas!)
console.log("" ?? "zahira");        // "" (bo'sh string null/undefined emas!)
```

---

## 📌 Tipni O'zgartirish (Type Conversion)

### Bilvosita (Implicit — Avtomatik)

```javascript
// String ga o'tish
console.log(1 + "2");    // "12" → number string ga aylanadi
console.log(true + ""); // "true"

// Number ga o'tish
console.log("5" - 2);  // 3   → string number ga aylanadi
console.log(true + 1); // 2   → true = 1
console.log(false + 1);// 1   → false = 0
console.log(null + 1); // 1   → null = 0

// Boolean ga o'tish (Falsy qiymatlar)
if (0) {} // bajarmaydi — 0 falsy
if ("") {} // bajarmaydi — bo'sh string falsy
```

### Aniq (Explicit — Qo'lda)

**String() — satrga aylantirish:**

```javascript
console.log(String(42));      // "42"
console.log(String(true));    // "true"
console.log(String(null));    // "null"
console.log(String(undefined)); // "undefined"

// Yoki toString() metodi
console.log((42).toString());  // "42"
console.log((255).toString(16)); // "ff" (16-lik)
```

**Number() — songa aylantirish:**

```javascript
console.log(Number("42"));     // 42
console.log(Number("3.14"));   // 3.14
console.log(Number(""));       // 0
console.log(Number(" "));      // 0
console.log(Number("salom"));  // NaN
console.log(Number(true));     // 1
console.log(Number(false));    // 0
console.log(Number(null));     // 0
console.log(Number(undefined));// NaN

// parseInt va parseFloat
console.log(parseInt("42px"));    // 42  → boshidan sonni oladi
console.log(parseFloat("3.14m")); // 3.14
console.log(parseInt("px42"));    // NaN → son yo'q
```

**Boolean() — mantiqiy turga aylantirish:**

```javascript
// Falsy qiymatlar → false
console.log(Boolean(0));         // false
console.log(Boolean(""));        // false
console.log(Boolean(null));      // false
console.log(Boolean(undefined)); // false
console.log(Boolean(NaN));       // false

// Truthy qiymatlar → true
console.log(Boolean(1));         // true
console.log(Boolean("salom"));   // true
console.log(Boolean([]));        // true (bo'sh massiv ham!)
console.log(Boolean({}));        // true (bo'sh ob'ekt ham!)
```

---

## 📌 Qiymat Tekshirish Jadvali

| Qiymat      | Boolean  | Number | String       |
|-------------|----------|--------|--------------|
| `0`         | `false`  | `0`    | `"0"`        |
| `""`        | `false`  | `0`    | `""`         |
| `null`      | `false`  | `0`    | `"null"`     |
| `undefined` | `false`  | `NaN`  | `"undefined"`|
| `NaN`       | `false`  | `NaN`  | `"NaN"`      |
| `1`         | `true`   | `1`    | `"1"`        |
| `"salom"`   | `true`   | `NaN`  | `"salom"`    |
| `[]`        | `true`   | `0`    | `""`         |
| `{}`        | `true`   | `NaN`  | `"[object Object]"` |

---

## 🎯 Amaliy Vazifa

Quyidagi misollarda natijani oldin taxmin qiling, so'ng tekshiring:

```javascript
// 1. Aritmetik
console.log(10 % 3);
console.log(2 ** 10);
console.log("10" - 5);
console.log("10" + 5);

// 2. Taqqoslash
console.log(null == undefined);
console.log(null === undefined);
console.log(NaN === NaN);

// 3. Mantiqiy
console.log(0 || 5);
console.log(1 && 0);
console.log(!!"salom");
console.log(!!0);

// 4. Type Conversion
console.log(Number(""));
console.log(Boolean([]));
console.log(String(null));
```
