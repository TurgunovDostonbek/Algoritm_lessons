# 6-Dars: Functions & Scope (Funksiyalar va Qamrov)

## 📌 Funksiya nima?

**Funksiya** — muayyan vazifani bajaruvchi, qayta ishlatilishi mumkin bo'lgan kod bloki.

```javascript
// Funksiya e'lon qilish
function salom() {
  console.log("Salom, Dunyo!");
}

// Funksiyani chaqirish
salom(); // "Salom, Dunyo!"
```

---

## 📌 Function Declaration vs Function Expression

### Function Declaration (E'lon)

```javascript
// Hoisting tufayli yuqorida chaqirish mumkin!
salom(); // ✅ ishlaydi

function salom() {
  console.log("Salom!");
}
```

### Function Expression (Ifoda)

```javascript
// Hoisting yo'q — avval aniqlash kerak
// salom(); // ❌ ReferenceError!

const salom = function() {
  console.log("Salom!");
};

salom(); // ✅
```

### Farqlar jadvali

| Xususiyat         | Declaration       | Expression        |
|------------------|-------------------|-------------------|
| Hoisting         | ✅ Ha             | ❌ Yo'q           |
| Nom              | Majburiy          | Ixtiyoriy         |
| Ishlatish        | Har joyda         | E'londan keyin    |
| `typeof`         | `"function"`      | `"function"`      |

---

## 📌 Arrow Functions (O'q Funksiyalari) — ES6

```javascript
// Oddiy funksiya
function qo_sh(a, b) {
  return a + b;
}

// Arrow function — qisqaroq yozilish
const qo_sh2 = (a, b) => a + b;

// Bir parametr — qavssiz
const ikki_baravar = x => x * 2;

// Parametrsiz — bo'sh qavslar
const salom = () => "Salom!";

// Ko'p qatorli
const katta = (a, b) => {
  if (a > b) return a;
  return b;
};

console.log(qo_sh2(3, 4));     // 7
console.log(ikki_baravar(5));  // 10
console.log(salom());          // "Salom!"
```

### Arrow function vs Oddiy funksiya — `this` farqi

```javascript
// Oddiy funksiya — o'zining this ga ega
function Shaxs(ism) {
  this.ism = ism;
  
  setTimeout(function() {
    // Bu yerda this = window/global (Shaxs emas!)
    console.log(this.ism); // undefined
  }, 1000);
}

// Arrow function — tashqi this ni oladi
function Shaxs2(ism) {
  this.ism = ism;
  
  setTimeout(() => {
    // Bu yerda this = Shaxs2 ob'ekti ✅
    console.log(this.ism); // "Ali"
  }, 1000);
}

new Shaxs2("Ali");
```

---

## 📌 Parametrlar va Argumentlar

```javascript
// Parametr = funksiya ta'rifidagi o'zgaruvchi
// Argument = funksiya chaqirilgandagi qiymat

function kutib_ol(ism, shahar) {  // ism, shahar — parametrlar
  console.log(`Salom, ${ism} (${shahar})!`);
}

kutib_ol("Ali", "Toshkent"); // "Ali", "Toshkent" — argumentlar
```

### Default Parametrlar (ES6)

```javascript
function salom(ism = "Mehmon") {
  console.log(`Salom, ${ism}!`);
}

salom("Ali");   // "Salom, Ali!"
salom();        // "Salom, Mehmon!" — default ishlatildi
```

### Rest Parametrlar (`...`)

```javascript
function yig_indi(...sonlar) {
  return sonlar.reduce((jami, son) => jami + son, 0);
}

console.log(yig_indi(1, 2, 3));        // 6
console.log(yig_indi(1, 2, 3, 4, 5)); // 15
```

### arguments ob'ekti

```javascript
function hammasi() {
  console.log(arguments);        // ArrayLike ob'ekt
  console.log(arguments.length); // argumentlar soni
  
  for (let i = 0; i < arguments.length; i++) {
    console.log(arguments[i]);
  }
}

hammasi(1, "salom", true); // 1, "salom", true
```

---

## 📌 Return (Qaytarish)

```javascript
// Qiymat qaytaruvchi funksiya
function kvadrat(x) {
  return x * x;
}

let natija = kvadrat(5);
console.log(natija); // 25

// Biror narsani qaytarmaydigan funksiya → undefined qaytaradi
function chop_et(xabar) {
  console.log(xabar);
  // return yo'q → undefined
}

let res = chop_et("Salom");
console.log(res); // undefined

// Erta qaytish
function musbat_mi(son) {
  if (son <= 0) return false;  // erta chiqish
  return true;
}
```

---

## 📌 Scope (Qamrov)

**Scope** — o'zgaruvchi qayerda ko'rinadi va ishlatilishi mumkinligi.

### 1. Global Scope

```javascript
let globalO_zgaruvchi = "Men global!";

function test() {
  console.log(globalO_zgaruvchi); // ✅ Ko'rinadi
}

test();
console.log(globalO_zgaruvchi); // ✅ Ko'rinadi
```

### 2. Local (Function) Scope

```javascript
function test() {
  let localO_zgaruvchi = "Men lokal!";
  console.log(localO_zgaruvchi); // ✅ Ko'rinadi
}

test();
// console.log(localO_zgaruvchi); // ❌ ReferenceError!
```

### 3. Block Scope (ES6 — let/const)

```javascript
{
  let blockO_zgaruvchi = "Block ichida";
  const blockConst = "Men ham block ichida";
  var varO_zgaruvchi = "Men function scope!";
  
  console.log(blockO_zgaruvchi); // ✅
}

// console.log(blockO_zgaruvchi); // ❌ let — block scope
// console.log(blockConst);       // ❌ const — block scope
console.log(varO_zgaruvchi);      // ✅ var — function scope!
```

### Scope Zanjiri (Scope Chain)

```javascript
let global_o_zg = "global";

function tashqi() {
  let tashqi_o_zg = "tashqi";
  
  function ichki() {
    let ichki_o_zg = "ichki";
    
    // Ichki funksiya barcha tashqi o'zgaruvchilarni ko'radi
    console.log(ichki_o_zg);  // ✅ "ichki"
    console.log(tashqi_o_zg); // ✅ "tashqi"
    console.log(global_o_zg); // ✅ "global"
  }
  
  ichki();
  // console.log(ichki_o_zg); // ❌ ko'rinmaydi
}

tashqi();
```

---

## 📌 Hoisting (Ko'tarish)

JavaScript kodni bajarishdan oldin e'lonlarni fayl/funksiya tepasiga "ko'taradi".

```javascript
// var hoisting — e'lon ko'tariladi, qiymat ko'tarilmaydi
console.log(x); // undefined (xato emas!)
var x = 5;
console.log(x); // 5

// let/const hoisting — temporal dead zone (TDZ)
// console.log(y); // ❌ ReferenceError — TDZ!
let y = 5;

// Function declaration hoisting
salom(); // ✅ "Salom!" — to'liq ko'tariladi
function salom() {
  console.log("Salom!");
}

// Function expression — ko'tarilmaydi
// xayir(); // ❌ ReferenceError
const xayir = () => console.log("Xayr!");
```

---

## 📌 Closure (Yopilish)

Closure — ichki funksiya tashqi funksiyaning o'zgaruvchilarini "eslaydi".

```javascript
function hisoblagich() {
  let hisob = 0; // bu o'zgaruvchi saqlanib qoladi
  
  return function() {
    hisob++;
    return hisob;
  };
}

const hisoblash = hisoblagich();
console.log(hisoblash()); // 1
console.log(hisoblash()); // 2
console.log(hisoblash()); // 3

const yangi_hisoblash = hisoblagich(); // yangi closure
console.log(yangi_hisoblash()); // 1 — o'zining hisob o'zgaruvchisi
```

---

## 🎯 Amaliy Vazifalar

```javascript
// 1. Ikkita sonni qo'shuvchi arrow function yozing
const qo_sh = (a, b) => /* ... */;

// 2. Default parametrli salomlashish funksiyasi
function salomlash(ism = "Mehmon", murojaat = "Hurmatli") {
  // "Hurmatli Ali, xush kelibsiz!"
}

// 3. Istalgan miqdordagi sonlar yig'indisi (rest params)
const yig_indi = (...raqamlar) => /* ... */;
console.log(yig_indi(1,2,3,4,5)); // 15

// 4. Closure bilan sekretar funksiyasi
function sekretar(xabar) {
  return function() {
    console.log(`Xabar: ${xabar}`);
  };
}

// 5. Faktorial hisoblash (rekursiya)
function faktorial(n) {
  if (n <= 1) return 1;
  return n * faktorial(n - 1);
}
console.log(faktorial(5)); // 120
```

---

## ❓ 30 ta Savol-Javob

### Boshlang'ich Savolar

**1. Function Declaration va Function Expression qanday farq qiladi?**
> Function Declaration hoisting tufayli e'londan oldin ham chaqirilishi mumkin. Expression esa e'londan keyin chaqirilishi mumkin.

**2. Arrow function sintaksisi qanday?**
> `const f = (params) => ifoda;` yoki `const f = (params) => { ... return ...; };`

**3. Funksiya parametri va argumenti nima?**
> Parametr — funksiya ta'rifidagi o'zgaruvchi. Argument — chaqirishda beriladigan haqiqiy qiymat.

**4. `return` nima vazifa bajaradi?**
> Funksiyadan qiymat qaytaradi va funksiyani to'xtatadi.

**5. Default parametr qanday yoziladi?**
> `function f(x = 10) {}` — argument berilmasa `x = 10` bo'ladi.

**6. Global scope nima?**
> Funksiya yoki blok tashqarisida e'lon qilingan o'zgaruvchilar hamma joyda ko'rinadigan global scope da bo'ladi.

**7. `var` qanday scope ga ega?**
> `var` funksiya scope ga ega — u e'lon qilingan funksiya ichida ko'rinadi.

**8. `let` va `const` qanday scope ga ega?**
> Block scope — faqat `{}` bloki ichida ko'rinadi.

**9. Hoisting nima?**
> JavaScript kodni bajarishdan oldin e'lonlarni fayl yoki funksiya tepasiga "ko'taradi".

**10. `var` hoisting qanday ishlaydi?**
> E'lon ko'tariladi, lekin qiymat ko'tarilmaydi. Shuning uchun e'londan oldin `undefined` qaytaradi.

---

### O'rta Savolar

**11. Closure nima?**
> Ichki funksiyaning tashqi funksiya o'zgaruvchilarini "eslash" qobiliyati. Tashqi funksiya tugagandan keyin ham o'zgaruvchilar saqlanib qoladi.

**12. Arrow function va oddiy funksiyaning `this` borasidagi farqi nima?**
> Oddiy funksiya o'zining `this` ga ega. Arrow function esa tashqi kontekstning `this` ini oladi.

**13. Rest parametr (`...`) nima?**
> Ko'p argumentlarni massiv sifatida qabul qilish: `function f(...args) {}`.

**14. `arguments` ob'ekti nima?**
> Funksiya ichida barcha argumentlarga kirish imkonini beruvchi arrayga o'xshash ob'ekt. Arrow function da mavjud emas.

**15. Scope zanjiri (Scope Chain) nima?**
> JavaScript o'zgaruvchini qidirganda avval joriy scope da, topilmasa tashqi scope da qidiradi — eng tashqarigacha.

**16. IIFE nima?**
> Immediately Invoked Function Expression — e'lon qilinishi bilan darhol chaqiriladigan funksiya: `(function() { ... })();`

**17. Pure function nima?**
> Bir xil argument uchun har doim bir xil natija qaytaruvchi va tashqi holatni o'zgartirmaydigan funksiya.

**18. Higher-Order Function nima?**
> Funksiyani argument sifatida qabul qiladigan yoki funksiya qaytaradigan funksiya. Masalan: `map`, `filter`, `forEach`.

**19. Rekursiya nima?**
> Funksiyaning o'zini o'zi chaqirishi. Albatta to'xtatuvchi shart bo'lishi kerak.

**20. Temporal Dead Zone (TDZ) nima?**
> `let` va `const` e'lonidan oldingi maydon — bu soha da o'zgaruvchiga murojaat `ReferenceError` beradi.

---

### Murakkab Savolar

**21. Quyidagi kod nima chiqaradi?**
```javascript
console.log(typeof salom);
var salom = "salom";
function salom() {}
console.log(typeof salom);
```
> `"function"` (hoisting: funksiya e'loni var dan ustun), keyin `"string"` (qiymat tayinlangach).

**22. Closure misolini tushuntiring:**
```javascript
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 100);
}
```
> Uchala console.log ham `3` chiqaradi, chunki `var` funksiya scope — loop tugaganda `i=3`.

**23. Yuqoridagi muammoni qanday hal qilish mumkin?**
> `var` o'rniga `let` ishlatish (block scope): `for (let i = 0; i < 3; i++)` → 0, 1, 2 chiqaradi.

**24. Arrow function konstruktor sifatida ishlatilishi mumkinmi?**
> Yo'q. `new ArrowFunc()` → `TypeError`. Arrow function `this` va `prototype` ga ega emas.

**25. Funksiya overloading JavaScript da mavjudmi?**
> Yo'q. Bir xil nomli funksiya ikki marta e'lon qilinsa, ikkinchisi birinchisini ustiga yozadi.

**26. `call`, `apply`, `bind` nima?**
> Funksiyaning `this` kontekstini o'zgartirish usullari. `call` va `apply` darhol chaqiradi, `bind` yangi funksiya qaytaradi.

**27. Generators nima?**
> `function*` bilan e'lon qilinadi. `yield` bilan qiymat qaytaradi va to'xtaydi. `next()` bilan davom ettiriladi.

**28. Memoization nima?**
> Funksiya natijalarini cache qilib, bir xil argumentlar uchun qayta hisoblashdan saqlovchi optimizatsiya usuli.

**29. Quyidagi kod nima chiqaradi?**
```javascript
const obj = {
  x: 10,
  getX: function() { return this.x; },
  getX2: () => this.x
};
console.log(obj.getX());  // ?
console.log(obj.getX2()); // ?
```
> `10` (oddiy funksiya — `this = obj`), keyin `undefined` (arrow function — `this = global/window`, `x` yo'q).

**30. Function currying nima?**
> Ko'p argumentli funksiyani ketma-ket bir argumentli funksiyalarga aylantirish.
```javascript
const qo_sh = a => b => a + b;
console.log(qo_sh(2)(3)); // 5
```
