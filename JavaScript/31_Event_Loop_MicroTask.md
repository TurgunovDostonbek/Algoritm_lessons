# 31-Dars: Event Loop va Micro Task

## 📌 JavaScript bir oqimli (Single-threaded)

JavaScript bir vaqtda bitta amalni bajaradi. Lekin asinxron amallarni qanday boshqaradi?

```
JavaScript Runtime
├── Call Stack      — Joriy bajarilayotgan funksiyalar
├── Web APIs        — setTimeout, fetch, DOM events (brauzer tomonidan)
├── Callback Queue  — Macro tasks (setTimeout, setInterval)
├── Microtask Queue — Promise, queueMicrotask, MutationObserver
└── Event Loop      — Stack bo'sh bo'lganda queue dan oladi
```

---

## 📌 Call Stack (Chaqiruv Steki)

```javascript
function c() { console.log("C"); }
function b() { c(); console.log("B"); }
function a() { b(); console.log("A"); }

a();

// Stack harakati:
// 1. a()  → Stack: [a]
// 2. b()  → Stack: [a, b]
// 3. c()  → Stack: [a, b, c]
// 4. "C"  → Stack: [a, b]  (c chiqdi)
// 5. "B"  → Stack: [a]     (b chiqdi)
// 6. "A"  → Stack: []      (a chiqdi)
```

---

## 📌 Event Loop Tartibi

```javascript
console.log("1 - Sinxron");

setTimeout(() => console.log("2 - setTimeout (macro)"), 0);

Promise.resolve().then(() => console.log("3 - Promise (micro)"));

console.log("4 - Sinxron");

// Chiqish tartibi:
// 1 - Sinxron
// 4 - Sinxron
// 3 - Promise (micro)    ← Microtask avval!
// 2 - setTimeout (macro) ← Macrotask keyin
```

---

## 📌 Macro Tasks vs Micro Tasks

```javascript
// Macro Tasks (Task Queue)
setTimeout(() => {}, 0);
setInterval(() => {}, 1000);
setImmediate(() => {}); // Node.js
// I/O operatsiyalar

// Micro Tasks (Microtask Queue)
Promise.resolve().then(() => {});
queueMicrotask(() => {});
// MutationObserver
// async/await (await dan keyingi kod)

// Tartib: Sinxron → Barcha Microtask → Bitta Macrotask → Barcha Microtask → ...
```

---

## 📌 Async/Await va Event Loop

```javascript
async function asinxron() {
  console.log("1 - async boshlandi");
  await Promise.resolve(); // Micro task!
  console.log("3 - await dan keyin"); // Microtask navbatida
  return "natija";
}

console.log("0 - boshlanish");
asinxron().then(n => console.log("4 -", n));
console.log("2 - asinxron dan keyin");

// Tartib: 0, 1, 2, 3, 4
```

---

## 📌 Murakkab Event Loop Misollari

```javascript
// Misol 1
console.log("start");                          // 1

setTimeout(() => console.log("setTimeout"), 0); // macro

Promise.resolve()
  .then(() => console.log("promise 1"))         // micro 1
  .then(() => console.log("promise 2"));        // micro 2

queueMicrotask(() => console.log("microtask")); // micro 3

console.log("end");                             // 2

// Chiqish: start → end → promise 1 → microtask → promise 2 → setTimeout

// Misol 2 — Chuqurroq
setTimeout(() => {
  console.log("setTimeout 1");
  Promise.resolve().then(() => console.log("promise in setTimeout"));
}, 0);

setTimeout(() => console.log("setTimeout 2"), 0);

Promise.resolve().then(() => console.log("promise 1"));

// Chiqish:
// promise 1
// setTimeout 1
// promise in setTimeout  ← setTimeout 2 dan oldin!
// setTimeout 2
```

---

## 📌 Stack Overflow

```javascript
// Rekursiv funksiya stekni to'ldiradi
function cheksiz() {
  return cheksiz(); // Maximum call stack size exceeded
}
// cheksiz(); // ❌ RangeError!

// Yechim — asinxron rekursiya
function xavfsizRekursiya(n) {
  if (n <= 0) return;
  console.log(n);
  setTimeout(() => xavfsizRekursiya(n - 1), 0); // Stekni bo'shatadi
}
// xavfsizRekursiya(10000); // ✅ Ishlaydi
```

---

## 📌 queueMicrotask()

```javascript
// Microtask navbatiga funksiya qo'shish
queueMicrotask(() => {
  console.log("Bu microtask navbatida!");
});

// Promise.resolve().then() bilan bir xil
Promise.resolve().then(() => {
  console.log("Bu ham microtask!");
});
```

---

## 📌 Performance — Event Loop ni bloklash

```javascript
// ❌ Event Loopni bloklash (YOMON)
function og_irHisoblash() {
  let sum = 0;
  for (let i = 0; i < 1000000000; i++) sum += i; // UI muzlaydi!
  return sum;
}

// ✅ Yechim 1 — Chunklarga bo'lish
function xavfsizHisoblash(n, chunk = 10000000) {
  let sum = 0, i = 0;
  
  function keyingiBatchni_hisoblash() {
    let tugash = Math.min(i + chunk, n);
    for (; i < tugash; i++) sum += i;
    
    if (i < n) {
      setTimeout(keyingiBatchni_hisoblash, 0); // UI ga nafas beradi
    } else {
      console.log("Natija:", sum);
    }
  }
  keyingiBatchni_hisoblash();
}

// ✅ Yechim 2 — Web Worker (alohida oqim)
// let worker = new Worker("worker.js");
```

---

## 🎯 10 ta Amaliy Vazifa

```javascript
// 1. Event Loop tartibini taxmin qiling
console.log("A");
setTimeout(() => console.log("B"), 0);
Promise.resolve().then(() => console.log("C"));
console.log("D");
// Javob: A → D → C → B

// 2. Micro va Macro farqini ko'rsating
function tartibniKo_rsat() {
  console.log("1: Sinxron");
  
  setTimeout(() => console.log("4: setTimeout"), 0);
  
  Promise.resolve()
    .then(() => console.log("3: Promise.then"))
    .then(() => console.log("3b: ikkinchi then"));
  
  queueMicrotask(() => console.log("3c: queueMicrotask"));
  
  console.log("2: Sinxron tugatildi");
}
tartibniKo_rsat();

// 3. Async funksiya tartibi
async function asyncTartib() {
  console.log("A");
  await null;
  console.log("C");
}
asyncTartib();
console.log("B");
// A → B → C

// 4. Asinxron navigatsiya simulyatsiyasi
class Router {
  #joriy = "/";
  
  async navigate(yo'l) {
    console.log(`${this.#joriy} → ${yo'l} ga o'tilmoqda`);
    await new Promise(r => setTimeout(r, 100)); // Server tekshiruvi
    this.#joriy = yo'l;
    console.log(`${yo'l} ga o'tildi`);
  }
  
  get joriyYol() { return this.#joriy; }
}
let router = new Router();
router.navigate("/bosh").then(() => router.navigate("/profil"));

// 5. Parallel amal bajarish va sinxronizatsiya
async function parallelAmallar() {
  let boshlanish = Date.now();
  
  let [natija1, natija2, natija3] = await Promise.all([
    new Promise(r => setTimeout(() => r("A"), 100)),
    new Promise(r => setTimeout(() => r("B"), 200)),
    new Promise(r => setTimeout(() => r("C"), 150))
  ]);
  
  console.log(natija1, natija2, natija3); // A B C
  console.log(`Jami: ${Date.now() - boshlanish}ms`); // ~200ms (parallel!)
}
parallelAmallar();

// 6. Event Loop bloklash va yechim
function bloklaydi() {
  let bosh = Date.now();
  while (Date.now() - bosh < 1000) {} // 1 soniya bloklaydi
  console.log("Tugadi");
}

// Yaxshisi async bilan:
function bloklaydiXavfsiz() {
  return new Promise(r => setTimeout(r, 1000)).then(() => console.log("Tugadi"));
}

// 7. Microtask navbati to'lib ketishi
function mikroTaskToshib_ketishi() {
  function recursiveMicro(n) {
    if (n <= 0) return;
    Promise.resolve().then(() => {
      console.log(n);
      recursiveMicro(n - 1); // Macro tasks heч qachon ishlamaydi!
    });
  }
  recursiveMicro(5);
  setTimeout(() => console.log("setTimeout - hech qachon?"), 0);
  // Micro tasks barcha tugamasa, setTimeout ishlamaydi!
}
// mikroTaskToshib_ketishi(); // Ehtiyot bo'ling!

// 8. Debounce (Event Loop bilan)
function debounce(fn, ms) {
  let taymer = null;
  return function(...args) {
    clearTimeout(taymer); // Avvalgi macro task ni bekor qil
    taymer = setTimeout(() => {
      fn.apply(this, args);
      taymer = null;
    }, ms);
  };
}
let saqlash = debounce(() => console.log("Saqlandi!"), 300);
saqlash(); saqlash(); saqlash(); // Faqat oxirgisi ishga tushadi

// 9. Race Condition simulyatsiyasi
let qiymat = 0;
async function incrementA() {
  let joriy = qiymat;     // O'qish
  await new Promise(r => setTimeout(r, 10)); // Kutish
  qiymat = joriy + 1;     // Yozish
}
await Promise.all([incrementA(), incrementA(), incrementA()]);
console.log(qiymat); // 1 (3 emas!) — Race condition!

// 10. requestAnimationFrame — UI da to'g'ri ishlash
function animatsiya(vaqt) {
  // Bu har kadrda chaqiriladi (~60fps)
  // Heavy hisoblash emas, faqat DOM yangilash
  requestAnimationFrame(animatsiya);
}
// requestAnimationFrame(animatsiya); // Brauzerda
```
