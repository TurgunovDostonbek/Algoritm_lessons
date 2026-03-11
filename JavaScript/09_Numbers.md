# 9-Dars: Numbers (Sonlar)

## 📌 Number nima?

JavaScript da barcha sonlar (butun va kasr) bitta `Number` turida saqlanadi. JavaScript **IEEE 754** double-precision 64-bit floating point standartidan foydalanadi.

```javascript
let butun = 42;
let kasr = 3.14;
let manfiy = -10;
let ilmiy = 1.5e6;  // 1,500,000

console.log(typeof butun); // "number"
console.log(typeof kasr);  // "number"
```

---

## 📌 Number Constructor (Number() funksiyasi)

```javascript
// Konstruktor sifatida — yangi Number ob'ekti (ishlatilmaydi)
let n = new Number(42);
console.log(typeof n); // "object" — oddiy number emas!

// Konversiya funksiyasi sifatida (to'g'ri usul)
console.log(Number("42"));       // 42
console.log(Number("3.14"));     // 3.14
console.log(Number(""));         // 0
console.log(Number(true));       // 1
console.log(Number(false));      // 0
console.log(Number(null));       // 0
console.log(Number(undefined));  // NaN
console.log(Number("abc"));      // NaN
```

---

## 📌 Maxsus Number Qiymatlari

```javascript
// Cheksizlik
console.log(Infinity);   // Infinity
console.log(-Infinity);  // -Infinity
console.log(1 / 0);      // Infinity
console.log(-1 / 0);     // -Infinity

// NaN — Not a Number (Son emas)
console.log(NaN);              // NaN
console.log("abc" * 2);        // NaN
console.log(Math.sqrt(-1));    // NaN
console.log(NaN === NaN);      // false! (NaN o'ziga teng emas)
console.log(isNaN(NaN));       // true
console.log(Number.isNaN(NaN)); // true (aniqroq usul)

// Eng katta va kichik sonlar
console.log(Number.MAX_VALUE);       // 1.7976931348623157e+308
console.log(Number.MIN_VALUE);       // 5e-324 (eng kichik musbat)
console.log(Number.MAX_SAFE_INTEGER); // 9007199254740991 (2^53 - 1)
console.log(Number.MIN_SAFE_INTEGER); // -9007199254740991
```

---

## 📌 Sonlarni Tahlil Qilish (Parsing)

### `parseInt()` — Butun songa aylantirish

```javascript
console.log(parseInt("42"));       // 42
console.log(parseInt("42.9"));     // 42 — kasrni kesib tashlaydi
console.log(parseInt("42px"));     // 42 — boshidan sonni oladi
console.log(parseInt("px42"));     // NaN — son boshida emas
console.log(parseInt("0xFF", 16)); // 255 — 16-lik tizimdan
console.log(parseInt("1010", 2));  // 10  — ikkilik tizimdan
console.log(parseInt("52", 8));    // 42  — sakkizlik tizimdan

// Amaliy: CSS dan piksel qiymatini olish
let margin = "16px";
console.log(parseInt(margin) + 10); // 26
```

### `parseFloat()` — Kasr songa aylantirish

```javascript
console.log(parseFloat("3.14"));      // 3.14
console.log(parseFloat("3.14abc"));   // 3.14 (boshidan oladi)
console.log(parseFloat("3.14.99"));   // 3.14 (birinchi nuqtagacha)
console.log(parseFloat(".5"));        // 0.5
console.log(parseFloat("abc"));       // NaN
```

---

## 📌 Butun va Kasr Sonlar

```javascript
// Butun sonlar (Integer)
let yosh = 25;
let aholi = 35_000_000; // _ ajratuvchi (ES2021) — o'qishni osonlashtiradi

// Kasr sonlar (Float)
let narx = 19.99;
let foiz = 0.05;

// Floating point muammosi!
console.log(0.1 + 0.2); // 0.30000000000000004 ← !!!
console.log(0.1 + 0.2 === 0.3); // false!

// Yechim 1: toFixed
console.log((0.1 + 0.2).toFixed(2)); // "0.30" (string!)
console.log(+((0.1 + 0.2).toFixed(2))); // 0.3 (number)

// Yechim 2: Math.round + ko'paytirish
console.log(Math.round((0.1 + 0.2) * 10) / 10); // 0.3
```

---

## 📌 Ikkilik, Sakkizlik va O'n Oltilik Sonlar

```javascript
// Ikkilik (Binary) — 0b prefiksi
let ikkilik = 0b1010;    // = 10 (o'nlik)
console.log(ikkilik);    // 10
console.log(0b11111111); // 255

// Sakkizlik (Octal) — 0o prefiksi
let sakkizlik = 0o17;    // = 15 (o'nlik)
console.log(sakkizlik);  // 15

// O'n oltilik (Hexadecimal) — 0x prefiksi
let hex = 0xFF;          // = 255 (o'nlik)
console.log(hex);        // 255
console.log(0x1A);       // 26

// O'nlikdan boshqa tizimlarga o'tkazish
let son = 255;
console.log(son.toString(2));  // "11111111" (ikkilik)
console.log(son.toString(8));  // "377" (sakkizlik)
console.log(son.toString(16)); // "ff" (o'n oltilik)
```

---

## 📌 Number Metodlari

### `.toFixed(raqamlar)` — Kasr o'rinlar (String qaytaradi!)

```javascript
let pi = 3.14159265;

console.log(pi.toFixed(0));  // "3"
console.log(pi.toFixed(2));  // "3.14"
console.log(pi.toFixed(5));  // "3.14159"

// Moliyaviy hisoblash
let narx = 19.999;
console.log(narx.toFixed(2)); // "20.00"

// Numberga aylantirish
let son = +narx.toFixed(2);
console.log(son, typeof son); // 20 "number"
```

### `.toPrecision(umumiy)` — Umumiy raqamlar soni

```javascript
let son = 123.456;
console.log(son.toPrecision(2)); // "1.2e+2"
console.log(son.toPrecision(4)); // "123.5"
console.log(son.toPrecision(7)); // "123.4560"
```

### `.toExponential()` — Ilmiy yozuv

```javascript
let son = 123456789;
console.log(son.toExponential(2)); // "1.23e+8"
console.log(son.toExponential(4)); // "1.2346e+8"
```

---

## 📌 Number Statik Metodlari

```javascript
// isNaN — NaN mi?
console.log(Number.isNaN(NaN));     // true
console.log(Number.isNaN("abc"));   // false! (global isNaN dan farqli)
console.log(isNaN("abc"));          // true (global — avval number ga o'tkazadi)

// isFinite — chekli mi?
console.log(Number.isFinite(42));       // true
console.log(Number.isFinite(Infinity)); // false
console.log(Number.isFinite(NaN));      // false

// isInteger — butun sonmi?
console.log(Number.isInteger(42));    // true
console.log(Number.isInteger(42.0));  // true (42.0 === 42)
console.log(Number.isInteger(42.5));  // false

// isSafeInteger — xavfsiz butun sonmi?
console.log(Number.isSafeInteger(42));                    // true
console.log(Number.isSafeInteger(9007199254740992));       // false (MAX+1)
```

---

## 📌 `Object.is()` — Aniq taqqoslash

```javascript
// === muammolari
console.log(NaN === NaN); // false (noto'g'ri!)
console.log(+0 === -0);   // true (aslida farqli!)

// Object.is — to'g'ri taqqoslaydi
console.log(Object.is(NaN, NaN)); // true ✅
console.log(Object.is(+0, -0));   // false ✅
console.log(Object.is(1, 1));     // true
```

---

## 📌 Strange JS — G'alati Hollar

```javascript
console.log(0.1 + 0.2);     // 0.30000000000000004
console.log(typeof NaN);    // "number" (NaN — son emas, turi son!)
console.log(NaN === NaN);   // false
console.log(null + 1);      // 1 (null → 0)
console.log(undefined + 1); // NaN
console.log("5" - 3);       // 2 (string → number)
console.log("5" + 3);       // "53" (number → string)
console.log([] + []);       // "" (bo'sh string)
console.log([] + {});       // "[object Object]"
console.log({} + []);       // 0 (JS {} ni blok deb o'ylaydi)
```

---

## 🎯 Amaliy Vazifalar

```javascript
// 1. Ikkita sonni bo'lib, ikki o'rinli kasr qilib chiqaring
function bo_lish(a, b) {
  if (b === 0) return "Nolga bo'lib bo'lmaydi!";
  return +(a / b).toFixed(2);
}
console.log(bo_lish(10, 3)); // 3.33

// 2. Sonning ikkilik, sakkizlik, o'n oltilik ko'rinishini chiqaring
function sonTizimlar(n) {
  return {
    ikkilik: n.toString(2),
    sakkizlik: n.toString(8),
    hex: n.toString(16).toUpperCase()
  };
}
console.log(sonTizimlar(255)); // { ikkilik: "11111111", sakkizlik: "377", hex: "FF" }

// 3. Sonning xavfsiz integer ekanligini tekshiring
function xavfsizMi(n) {
  return Number.isSafeInteger(n) ? "Xavfsiz" : "Xavfli!";
}

// 4. Tanga tashlash simulyatsiyasi (50% ehtimолlik)
function tanga() {
  return Math.random() < 0.5 ? "Tura" : "Yozuv";
}

// 5. Bankir yaxlitlash — 5 ta foydalanib pul operatsiyasi biling
function pulFormati(miqdor) {
  return new Intl.NumberFormat("uz-UZ", {
    style: "currency",
    currency: "UZS"
  }).format(miqdor);
}
```

---

## ❓ 20 ta Savol-Javob

### Boshlang'ich Savolar

**1. JavaScript da nechta son turi bor?**
> Bitta — `Number` (va ES2020 dan `BigInt`). Butun va kasr uchun alohida tur yo'q.

**2. `NaN` nima?**
> Not a Number — son bo'lmagan arifmetik amalning natijasi (masalan, `"abc" * 2`).

**3. `NaN === NaN` nima qaytaradi?**
> `false`. NaN hech narsaga, hatto o'ziga ham teng emas. Tekshirish uchun `Number.isNaN()` ishlatiladi.

**4. `parseInt()` va `parseFloat()` farqi nima?**
> `parseInt` butun sonni, `parseFloat` kasr sonni oladi. Ikkalasi ham boshidagi sonni oladi.

**5. `0.1 + 0.2 === 0.3` nima qaytaradi?**
> `false`. Floating point xatosi: `0.1 + 0.2 = 0.30000000000000004`.

**6. `.toFixed()` qanday tur qaytaradi?**
> String qaytaradi! Son uchun `+num.toFixed(2)` yoki `Number(...)` kerak.

**7. Sonning ikkilik ko'rinishini qanday olamiz?**
> `son.toString(2)` — `255..toString(2)` → `"11111111"`.

**8. `Infinity` nima?**
> Cheksiz katta son. `1/0 === Infinity` → `true`.

**9. `Number.isNaN()` va global `isNaN()` farqi nima?**
> Global `isNaN` avval `Number()` bilan o'giradi: `isNaN("abc")` → `true`. `Number.isNaN` faqat haqiqiy NaN uchun `true`: `Number.isNaN("abc")` → `false`.

**10. `parseInt("0xFF", 16)` nima qaytaradi?**
> `255`.

---

### O'rta Savolar

**11. JavaScript dagi eng katta xavfsiz integer nima?**
> `Number.MAX_SAFE_INTEGER = 9007199254740991 (2^53 - 1)`.

**12. Nima uchun katta sonlar uchun `BigInt` kerak?**
> `Number` `MAX_SAFE_INTEGER` dan katta sonlarda aniqlik yo'qotadi. `BigInt` cheksiz katta sonlarni aniq saqlaydi.

**13. `Object.is(+0, -0)` nima qaytaradi?**
> `false`. `+0 === -0` `true` qaytaradi, lekin `Object.is` aniqroq.

**14. `Number._` nima uchun ishlatiladi?**
> Sonlarni o'qishni osonlashtirish uchun: `1_000_000` = `1000000`. ES2021 dan.

**15. `parseInt("10", 2)` nima qaytaradi?**
> `2`. Ikkilik `10` = o'nlik `2`.

**16. Floating point muammosini qanday hal qilamiz?**
> `.toFixed()`, `Math.round()`, yoki butun sonlarga ko'paytirish: `(0.1*10 + 0.2*10) / 10`.

**17. `Number.isFinite(Infinity)` nima qaytaradi?**
> `false`.

**18. `parseFloat("3.14.99")` nima qaytaradi?**
> `3.14` — birinchi nuqtagacha oladi.

**19. Songa string qo'shilsa nima bo'ladi?**
> String bo'ladi: `5 + "0"` → `"50"`.

**20. `typeof Infinity` nima?**
> `"number"`.

---

