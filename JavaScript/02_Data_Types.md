# 2-Dars: Data Types (Ma'lumot Turlari)

## 📌 JavaScriptda Ma'lumot Turlari

JavaScript ma'lumot turlarini 2 guruhga bo'lish mumkin:

```
Ma'lumot Turlari
├── Primitiv (Oddiy) Turlar
│   ├── String
│   ├── Number
│   ├── Boolean
│   ├── Undefined
│   ├── Null
│   ├── BigInt
│   └── Symbol
└── No-Primitiv (Murakkab) Turlar
    ├── Object
    ├── Array
    └── Function
```

---

## 📌 Primitiv Ma'lumot Turlari

Primitiv turlar **to'g'ridan-to'g'ri qiymat** saqlaydi va **o'zgarmas** (immutable) hisoblanadi.

### 1. String (Matn)

```javascript
let ism = "Ali";            // qo'sh tirnoq
let shahar = 'Toshkent';    // yagona tirnoq
let xabar = `Salom, ${ism}!`; // template literal (ES6)

console.log(typeof ism);    // "string"
console.log(ism.length);    // 3
```

**Muhim String metodlari:**

```javascript
let matn = "JavaScript";

console.log(matn.toUpperCase());   // "JAVASCRIPT"
console.log(matn.toLowerCase());   // "javascript"
console.log(matn.includes("Java")); // true
console.log(matn.slice(0, 4));     // "Java"
console.log(matn.split(""));       // ["J","a","v","a","S","c","r","i","p","t"]
```

---

### 2. Number (Son)

```javascript
let butunSon = 42;
let kasrSon = 3.14;
let manfiy = -10;
let cheksiz = Infinity;
let noSon = NaN;        // Not a Number

console.log(typeof butunSon); // "number"
console.log(10 / 0);          // Infinity
console.log("salom" * 2);     // NaN
```

**Muhim Number metodlari:**

```javascript
let son = 3.14159;

console.log(son.toFixed(2));       // "3.14"
console.log(Number.isInteger(42)); // true
console.log(Number.isNaN(NaN));    // true
console.log(Math.round(3.7));      // 4
console.log(Math.floor(3.9));      // 3
console.log(Math.ceil(3.1));       // 4
console.log(Math.max(1, 5, 3));    // 5
console.log(Math.min(1, 5, 3));    // 1
```

---

### 3. Boolean (Mantiqiy)

```javascript
let togri = true;
let noto_gri = false;

console.log(typeof togri);  // "boolean"
console.log(5 > 3);         // true
console.log(5 < 3);         // false
```

---

### 4. Undefined

```javascript
let x;              // qiymat berilmagan
console.log(x);    // undefined
console.log(typeof x); // "undefined"

function test() {
  // return yo'q
}
console.log(test()); // undefined
```

---

### 5. Null

```javascript
let o_zgaruvchi = null; // ataylab bo'sh qiymat

console.log(typeof null); // "object" ← JS dagi mashxur xato!
console.log(null == undefined);  // true
console.log(null === undefined); // false
```

---

### 6. BigInt (Juda katta sonlar)

```javascript
let kattaSon = 9007199254740991n; // n bilan tugatiladi

console.log(typeof kattaSon); // "bigint"
console.log(kattaSon + 1n);   // 9007199254740992n
```

---

### 7. Symbol (Noyob identifikator)

```javascript
let id1 = Symbol("id");
let id2 = Symbol("id");

console.log(id1 === id2); // false — har biri noyob!
console.log(typeof id1);  // "symbol"
```

---

## 📌 No-Primitiv (Murakkab) Ma'lumot Turlari

No-primitiv turlar **havola (reference)** orqali saqlanadi.

### 1. Object (Ob'ekt)

```javascript
let shaxs = {
  ism: "Ali",
  yosh: 25,
  shahar: "Toshkent",
  isStudent: true
};

// Xususiyatlarga murojaat
console.log(shaxs.ism);         // "Ali"  → nuqta orqali
console.log(shaxs["yosh"]);     // 25     → qavs orqali

// Qo'shish
shaxs.telefon = "+998901234567";

// O'chirish
delete shaxs.isStudent;

console.log(typeof shaxs); // "object"
```

---

### 2. Array (Massiv)

```javascript
let mevalar = ["olma", "banan", "nok"];

console.log(mevalar[0]);       // "olma"
console.log(mevalar.length);   // 3

mevalar.push("uzum");          // oxiriga qo'shish
mevalar.pop();                 // oxirisini o'chirish
mevalar.unshift("gilos");      // boshiga qo'shish
mevalar.shift();               // boshini o'chirish

console.log(typeof mevalar);   // "object"
console.log(Array.isArray(mevalar)); // true
```

---

### 3. Function (Funksiya)

```javascript
function salom(ism) {
  return `Salom, ${ism}!`;
}

console.log(typeof salom); // "function"
console.log(salom("Ali")); // "Salom, Ali!"
```

---

## 📌 Dinamik Tipizatsiya

JavaScript **dinamik tipizatsiyali** — o'zgaruvchi turi dastur ishlash vaqtida aniqlanadi.

```javascript
let o_zgaruvchi = 42;
console.log(typeof o_zgaruvchi); // "number"

o_zgaruvchi = "endi matn";
console.log(typeof o_zgaruvchi); // "string"

o_zgaruvchi = true;
console.log(typeof o_zgaruvchi); // "boolean"
```

---

## 📌 Primitiv vs No-Primitiv farqi

```javascript
// PRIMITIV — qiymat ko'chiriladi
let a = 10;
let b = a;
b = 20;
console.log(a); // 10 — o'zgarmadi ✅

// NO-PRIMITIV — havola ko'chiriladi
let obj1 = { x: 10 };
let obj2 = obj1;
obj2.x = 20;
console.log(obj1.x); // 20 — o'zgardi ⚠️
```

| Xususiyat       | Primitiv     | No-Primitiv      |
|-----------------|--------------|------------------|
| Saqlash usuli   | To'g'ridan   | Havola orqali    |
| Ko'chirish      | Qiymat       | Havola           |
| O'lcham         | Doimiy       | O'zgaruvchan     |
| Misol           | `string`, `number` | `object`, `array` |

---

## 📌 `typeof` operatori

```javascript
console.log(typeof "salom");     // "string"
console.log(typeof 42);          // "number"
console.log(typeof true);        // "boolean"
console.log(typeof undefined);   // "undefined"
console.log(typeof null);        // "object" ← ehtiyot bo'ling!
console.log(typeof {});          // "object"
console.log(typeof []);          // "object"
console.log(typeof function(){}); // "function"
```

---

## 🎯 Amaliy Vazifa

Ma'lumot turlarining farqini yodlang va quyidagilarni aniqlang:

```javascript
// Har bir o'zgaruvchining turini aniqlang
let a = "Salom";
let b = 100;
let c = true;
let d;
let e = null;
let f = { ism: "Ali" };
let g = [1, 2, 3];
let h = function() {};

// typeof bilan tekshiring
console.log(typeof a); // ?
console.log(typeof b); // ?
// va hokazo...
```

> 📝 **Eslatma:** `null` ning `typeof` i `"object"` bo'lishi JavaScriptdagi qadimiy xato — bu tilning o'zi shunday.
