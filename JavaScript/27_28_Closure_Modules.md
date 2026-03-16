# 27-Dars: Scope, Hoisting, Closure

## 📌 Hoisting (Ko'tarish)

JavaScript kodni bajarishdan avval o'zgaruvchilar va funksiyalar e'lonlarini fayl tepasiga "ko'taradi".

```javascript
// ===== var HOISTING =====
console.log(x); // undefined (xato emas!)
var x = 5;
console.log(x); // 5

// JavaScript buni shunday ko'radi:
var x;           // E'lon ko'tariladi
console.log(x); // undefined
x = 5;           // Qiymat ko'tarilmaydi
console.log(x); // 5

// ===== let/const HOISTING (TDZ) =====
// console.log(y); // ❌ ReferenceError — Temporal Dead Zone!
let y = 10;
console.log(y);  // 10

// ===== FUNCTION DECLARATION HOISTING =====
salom(); // ✅ "Salom!" — to'liq ko'tariladi!
function salom() { console.log("Salom!"); }

// ===== FUNCTION EXPRESSION HOISTING =====
// xayir(); // ❌ TypeError — undefined chaqirib bo'lmaydi
var xayir = function() { console.log("Xayr!"); };
// const xayir bilan ReferenceError bo'lardi
```

---

## 📌 Hoisting — Ustuvorlik Tartibi

```javascript
var x = "var";
function x() {}

console.log(x); // "var" — funksiya e'loni avval, lekin var qiymati ustun!

// Aslida JS buni shunday ko'radi:
// 1. function x() {} — ko'tariladi
// 2. var x;          — e'lon ko'tariladi (lekin funksiya allaqachon x ni egallagan)
// 3. x = "var";     — qiymat beriladi
```

---

## 📌 Lexical Scope va Scope Chain

```javascript
let global = "global";

function tashqi() {
  let tashqiO_zg = "tashqi";
  
  function o_rta() {
    let o_rtaO_zg = "o'rta";
    
    function ichki() {
      let ichkiO_zg = "ichki";
      
      // Scope chain: ichki → o'rta → tashqi → global
      console.log(global);     // ✅ "global"
      console.log(tashqiO_zg); // ✅ "tashqi"
      console.log(o'rtaO_zg);  // ✅ "o'rta"
      console.log(ichkiO_zg);  // ✅ "ichki"
    }
    ichki();
    // console.log(ichkiO_zg); // ❌ Shu darajada ko'rinmaydi
  }
  o'rta();
}
tashqi();
```

---

## 📌 Closure — Yopiq Qamrov

**Closure** — ichki funksiya tashqi funksiyaning o'zgaruvchilarini eslab qoladi — tashqi funksiya tugagandan keyin ham.

```javascript
function tashqi() {
  let maxfiy = "Bu maxfiy!";
  
  return function() { // Closure — maxfiy ni eslaydi
    console.log(maxfiy);
  };
}

let ichkiFn = tashqi(); // tashqi() tugadi
ichkiFn(); // "Bu maxfiy!" — lekin maxfiy hali ham mavjud! 🔐

// Hisoblagich (closure klassik misoli)
function hisoblagich(boshlangich = 0) {
  let hisob = boshlangich;
  
  return {
    oshir: () => ++hisob,
    kamayt: () => --hisob,
    olish: () => hisob,
    sfir: () => { hisob = boshlangich; }
  };
}

let c1 = hisoblagich(10);
let c2 = hisoblagich(0); // Alohida closure!

c1.oshir(); c1.oshir();
console.log(c1.olish()); // 12
console.log(c2.olish()); // 0 — c1 dan mustaqil
```

---

## 📌 Closure bilan Amaliy Patterns

```javascript
// 1. Module Pattern — maxfiy ma'lumotlar
function bankHisobi(egasi, boshlangichBalans) {
  let balans = boshlangichBalans; // Tashqaridan ko'rinmaydi!
  let tarix = [];
  
  return {
    kirim(miqdor) {
      balans += miqdor;
      tarix.push(`+${miqdor}`);
    },
    chiqim(miqdor) {
      if (miqdor > balans) throw new Error("Balans yetarli emas!");
      balans -= miqdor;
      tarix.push(`-${miqdor}`);
    },
    balansKo_rish: () => `${egasi} balansi: ${balans}`,
    tarixKo_rish: () => tarix
  };
}

let hisob = bankHisobi("Ali", 1000000);
hisob.kirim(500000);
hisob.chiqim(200000);
console.log(hisob.balansKo_rish()); // "Ali balansi: 1300000"
// hisob.balans — undefined (maxfiy!) ✅

// 2. Memoization (closure bilan kesh)
function memoize(fn) {
  let kesh = new Map();
  return function(...args) {
    let kalit = JSON.stringify(args);
    if (kesh.has(kalit)) {
      console.log("Keshdan!");
      return kesh.get(kalit);
    }
    let natija = fn.apply(this, args);
    kesh.set(kalit, natija);
    return natija;
  };
}

const asta_fibonacci = n => n <= 1 ? n : asta_fibonacci(n-1) + asta_fibonacci(n-2);
const tez_fibonacci = memoize(function(n) {
  return n <= 1 ? n : tez_fibonacci(n-1) + tez_fibonacci(n-2);
});

// 3. Event listener closure muammosi (va yechimi)
// Muammo: var bilan loop
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 100); // 3 3 3 ❌
}

// Yechim 1: let
for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 100); // 0 1 2 ✅
}

// Yechim 2: IIFE closure
for (var i = 0; i < 3; i++) {
  (function(j) {
    setTimeout(() => console.log(j), 100); // 0 1 2 ✅
  })(i);
}
```

---

## 🎯 10 ta Amaliy Vazifa

```javascript
// 1. Hoisting natijasini taxmin qiling
console.log(a); // ?
var a = 1;
console.log(a); // ?
function a() {} // ?
// Javob: function a(){}, 1

// 2. Closure bilan "once" funksiya (faqat bir marta bajariladi)
function bir_marta(fn) {
  let bajarildi = false, natija;
  return function(...args) {
    if (!bajarildi) {
      natija = fn.apply(this, args);
      bajarildi = true;
    }
    return natija;
  };
}
const bir_marta_log = bir_marta(() => console.log("Bir marta!"));
bir_marta_log(); // "Bir marta!"
bir_marta_log(); // Hech narsa

// 3. Private kaounter sinfi (closure bilan)
function privatHisoblagich() {
  let _hisob = 0;
  return {
    oshir() { return ++_hisob; },
    kamayt() { return --_hisob; },
    get hisob() { return _hisob; }
  };
}
let h = privatHisoblagich();
h.oshir(); h.oshir();
console.log(h.hisob); // 2
// h._hisob — undefined (maxfiy)

// 4. Debounce closure bilan
function debounce(fn, ms) {
  let taymer;
  return function(...args) {
    clearTimeout(taymer);
    taymer = setTimeout(() => fn.apply(this, args), ms);
  };
}

// 5. Throttle closure bilan
function throttle(fn, ms) {
  let oxirgi = 0;
  return function(...args) {
    let hozir = Date.now();
    if (hozir - oxirgi >= ms) {
      fn.apply(this, args);
      oxirgi = hozir;
    }
  };
}

// 6. Compose — funksiyalar zanjirlash
function compose(...fnlar) {
  return function(qiymat) {
    return fnlar.reduceRight((acc, fn) => fn(acc), qiymat);
  };
}
const pipe = (...fnlar) => qiymat => fnlar.reduce((acc, fn) => fn(acc), qiymat);

const transformatsiya = compose(
  x => x * 2,
  x => x + 10,
  x => x ** 2
);
console.log(transformatsiya(3)); // ((9+10)*2) = 38

// 7. Generator (closure ga o'xshash)
function idGenerator(boshlanish = 1) {
  let id = boshlanish;
  return { keyingisi: () => id++ };
}
let gen = idGenerator(100);
console.log(gen.keyingisi()); // 100
console.log(gen.keyingisi()); // 101

// 8. TDZ (Temporal Dead Zone) misoli
function tdz_test() {
  // console.log(x); // ReferenceError — TDZ!
  let x = 10;
  console.log(x); // 10
}
tdz_test();

// 9. Closure bilan konfiguratsiya
function sozlash(maxSon, minSon) {
  return function hisoblash(son) {
    if (son > maxSon) return `${son} juda katta (max: ${maxSon})`;
    if (son < minSon) return `${son} juda kichik (min: ${minSon})`;
    return `${son} - qabul qilindi`;
  };
}
let tekshir = sozlash(100, 0);
console.log(tekshir(50));  // "50 - qabul qilindi"
console.log(tekshir(150)); // "150 juda katta (max: 100)"

// 10. Scope muammo va yechim
let ob_ektlar = [];
for (let i = 0; i < 5; i++) {
  ob_ektlar.push({ id: i, harakat: () => console.log(i) });
}
ob_ektlar[0].harakat(); // 0 ✅ (let tufayli)
ob_ektlar[3].harakat(); // 3 ✅
```

---

# 28-Dars: Export & Import — ES6 Modules

## 📌 Modullar nima?

**Modullar** — kodni alohida fayllarga ajratish va ular orasida almashish mexanizmi.

---

## 📌 Named Export/Import

```javascript
// math.js — Named export
export const PI = 3.14159;
export function qo_sh(a, b) { return a + b; }
export function ayir(a, b) { return a - b; }
export class Doira {
  constructor(r) { this.r = r; }
  maydon() { return PI * this.r ** 2; }
}

// main.js — Named import
import { PI, qo_sh, ayir, Doira } from "./math.js";
console.log(PI);          // 3.14159
console.log(qo_sh(2, 3)); // 5
let d = new Doira(5);
console.log(d.maydon().toFixed(2)); // "78.54"

// Alias (nom o'zgartirish)
import { qo_sh as plus, ayir as minus } from "./math.js";
console.log(plus(10, 5));  // 15
console.log(minus(10, 5)); // 5

// Hamma narsani bitta ob'ektga
import * as Math from "./math.js";
console.log(Math.PI);    // 3.14159
console.log(Math.qo_sh(1, 2)); // 3
```

---

## 📌 Default Export/Import

```javascript
// foydalanuvchi.js — Default export (faqat bitta bo'ladi)
export default class Foydalanuvchi {
  constructor(ism, email) {
    this.ism = ism;
    this.email = email;
  }
  tavsif() { return `${this.ism} <${this.email}>`; }
}

// Yoki funksiya
export default function salomlash(ism) {
  return `Salom, ${ism}!`;
}

// main.js — Default import (istalgan nom)
import Foydalanuvchi from "./foydalanuvchi.js";
// import MeningFoydalanuvchim from "./foydalanuvchi.js"; // Bu ham ishlaydi!

let f = new Foydalanuvchi("Ali", "ali@mail.com");
console.log(f.tavsif());
```

---

## 📌 Mixed Export/Import

```javascript
// utils.js
export default function asosiy() { return "Asosiy funksiya"; }
export const VERSION = "1.0.0";
export function yordamchi() { return "Yordamchi funksiya"; }

// main.js
import asosiy, { VERSION, yordamchi } from "./utils.js";
```

---

## 📌 Re-export (qayta eksport)

```javascript
// index.js — barcha modullarni birlashtirish
export { qo'sh, ayir } from "./math.js";
export { default as Foydalanuvchi } from "./foydalanuvchi.js";
export * from "./utils.js";
```

---

## 📌 Dynamic Import (Dinamik)

```javascript
// Faqat kerak bo'lganda yuklash
async function funksiyaYukla() {
  let { qo_sh } = await import("./math.js");
  console.log(qo_sh(1, 2)); // 3
}

// Lazy loading
button.addEventListener("click", async () => {
  let { default: Modal } = await import("./modal.js");
  new Modal().ko_rsat();
});
```

---

## 🎯 10 ta Amaliy Vazifa

```javascript
// Fayl tuzilmasi:
// src/
//   utils/
//     math.js
//     string.js
//     array.js
//   models/
//     user.js
//   index.js

// === math.js ===
export const qo_sh = (a, b) => a + b;
export const ayir = (a, b) => a - b;
export const ko_paytir = (a, b) => a * b;
export const bo_l = (a, b) => b !== 0 ? a / b : null;
export default Math; // default — Math ob'ektini re-export

// === string.js ===
export const kattaHarf = s => s.toUpperCase();
export const kichikHarf = s => s.toLowerCase();
export const qisqartir = (s, n) => s.length > n ? s.slice(0,n) + "..." : s;
export const palindromMi = s => s === [...s].reverse().join("");

// === array.js ===
export const noyob = arr => [...new Set(arr)];
export const birinchiN = (arr, n) => arr.slice(0, n);
export const saralash = arr => [...arr].sort((a,b) => a - b);

// === user.js ===
export default class User {
  #balans = 0; // Private field

  constructor(ism, email) {
    this.ism = ism;
    this.email = email;
    this.id = Date.now();
  }
  kirim(miqdor) { this.#balans += miqdor; }
  chiqim(miqdor) {
    if (miqdor > this.#balans) throw new Error("Balans yetarli emas");
    this.#balans -= miqdor;
  }
  get balans() { return this.#balans; }
  toJSON() { return { id: this.id, ism: this.ism, email: this.email }; }
}

// === index.js — Barcha modullarni birlashtirish ===
export * from "./utils/math.js";
export * from "./utils/string.js";
export * from "./utils/array.js";
export { default as User } from "./models/user.js";

// Dinamik import
async function modulYukla(modulNomi) {
  try {
    let modul = await import(`./utils/${modulNomi}.js`);
    return modul;
  } catch (e) {
    console.error("Modul topilmadi:", e.message);
    return null;
  }
}
```
