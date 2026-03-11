# 14-Dars: Array — 3-qism (Metodlar Taqqoslash)

## 📌 `find()` va `findIndex()` — Farqlari

| Xususiyat       | `find()`              | `findIndex()`        |
|-----------------|-----------------------|----------------------|
| Qaytarish       | Elementning o'zini    | Elementning indeksini |
| Topilmasa       | `undefined`           | `-1`                 |
| Ishlatish holat | Element kerak bo'lsa  | Indeks kerak bo'lsa  |

```javascript
let arr = [10, 20, 30, 40, 50];

// find — elementning o'zini qaytaradi
let el = arr.find(x => x > 25);
console.log(el);         // 30

// findIndex — indeksini qaytaradi
let idx = arr.findIndex(x => x > 25);
console.log(idx);        // 2

// Qachon findIndex kerak?
// → Elementni o'chirish yoki o'zgartirish kerak bo'lganda

let users = [
  { id: 1, ism: "Ali" },
  { id: 2, ism: "Vali" },
  { id: 3, ism: "Gani" }
];

// Elementni o'zgartirish uchun findIndex zarur
let i = users.findIndex(u => u.id === 2);
if (i !== -1) {
  users[i] = { ...users[i], ism: "Valixon" };
}
console.log(users[1]); // { id: 2, ism: "Valixon" }

// Elementni o'chirish
users.splice(i, 1);
console.log(users.length); // 2
```

---

## 📌 `filter()` va `find()` — Farqlari

| Xususiyat     | `filter()`             | `find()`            |
|---------------|------------------------|---------------------|
| Nechta topadi | HAMMA mos elementlarni | BITTA (birinchisini) |
| Qaytarish     | Massiv (bo'sh bo'lishi mumkin) | Element yoki `undefined` |
| Ishlatish     | Ko'p elementlar kerak  | Bitta element kerak |

```javascript
let sonlar = [1, 4, 7, 2, 9, 3, 8];

// filter — BARCHAA 5 dan katta elementlarni
let kattalar = sonlar.filter(x => x > 5);
console.log(kattalar); // [7, 9, 8]

// find — BIRINCHI 5 dan katta element
let birinchi = sonlar.find(x => x > 5);
console.log(birinchi); // 7

// Topilmasa:
console.log(sonlar.filter(x => x > 100)); // [] (bo'sh massiv)
console.log(sonlar.find(x => x > 100));   // undefined

// Amaliy:
let mahsulotlar = [
  { nomi: "Olma", omborda: true },
  { nomi: "Banan", omborda: false },
  { nomi: "Nok", omborda: true },
  { nomi: "Uzum", omborda: false }
];

// BARCHAA mavjud mahsulotlar
let mavjudlar = mahsulotlar.filter(m => m.omborda);
console.log(mavjudlar.map(m => m.nomi)); // ["Olma", "Nok"]

// BIRINCHI mavjud mahsulot
let birinchiMavjud = mahsulotlar.find(m => m.omborda);
console.log(birinchiMavjud.nomi); // "Olma"
```

---

## 📌 `forEach()` va `map()` — Farqlari

| Xususiyat     | `forEach()`             | `map()`               |
|---------------|-------------------------|-----------------------|
| Qaytarish     | `undefined` (hech narsa)| Yangi massiv qaytaradi|
| Maqsad        | Yon ta'sir (logging, DOM)| Transformatsiya       |
| Chaining      | ❌ (undefined qaytaradi) | ✅ (massiv qaytaradi) |
| Asl massiv    | O'zgarmaydi            | O'zgarmaydi           |

```javascript
let arr = [1, 2, 3, 4, 5];

// forEach — faqat amal bajaradi, natija yo'q
let forEachNatija = arr.forEach(x => x * 2);
console.log(forEachNatija); // undefined

// map — yangi massiv qaytaradi
let mapNatija = arr.map(x => x * 2);
console.log(mapNatija); // [2, 4, 6, 8, 10]
console.log(arr);       // [1, 2, 3, 4, 5] — o'zgarmadi

// forEach qachon?
// → Console.log, DOM o'zgartirish, API chaqirish
arr.forEach(x => console.log(x)); // 1, 2, 3, 4, 5

// map qachon?
// → Ma'lumotni o'zgantirish, yangi massiv kerak
let ikkiBarobar = arr.map(x => x * 2); // [2, 4, 6, 8, 10]

// Chaining — map bilan mumkin
let natija = arr
  .map(x => x * 2)    // [2, 4, 6, 8, 10]
  .filter(x => x > 4) // [6, 8, 10]
  .reduce((s, x) => s + x, 0); // 24
console.log(natija); // 24

// forEach bilan chain bo'lmaydi:
// arr.forEach(...).map(...) ← ❌ TypeError
```

---

## 📌 Metodlar Zanjiri (Method Chaining)

```javascript
let mahsulotlar = [
  { nomi: "Olma", narx: 5000, tur: "Meva" },
  { nomi: "Sabzi", narx: 3000, tur: "Sabzavot" },
  { nomi: "Banan", narx: 8000, tur: "Meva" },
  { nomi: "Kartoshka", narx: 2000, tur: "Sabzavot" },
  { nomi: "Nok", narx: 6000, tur: "Meva" }
];

// Mevalarni toping → narx bo'yicha saralang → faqat nomlarini oling
let natija = mahsulotlar
  .filter(m => m.tur === "Meva")
  .sort((a, b) => a.narx - b.narx)
  .map(m => `${m.nomi}: ${m.narx} so'm`);

console.log(natija);
// ["Olma: 5000 so'm", "Nok: 6000 so'm", "Banan: 8000 so'm"]
```

---

## 📌 Mutatsiya vs Yangi Massiv

| Mutatsiya (O'zgartiradi) | Yangi Massiv (O'zgartirmaydi) |
|--------------------------|-------------------------------|
| `push()`, `pop()`        | `map()`                       |
| `unshift()`, `shift()`   | `filter()`                    |
| `splice()`               | `slice()`                     |
| `sort()`                 | `concat()`                    |
| `reverse()`              | `flat()`, `flatMap()`         |
| `fill()`                 | `find()`, `findIndex()`       |
| `copyWithin()`           | `every()`, `some()`           |

```javascript
// sort va reverse aslini o'zgartiradi!
let arr = [3, 1, 4, 1, 5];

// Aslini saqlab saralash
let saralangan = [...arr].sort((a, b) => a - b);
// yoki arr.slice().sort(...)
console.log(arr);       // [3, 1, 4, 1, 5] — o'zgarmadi
console.log(saralangan); // [1, 1, 3, 4, 5]
```

---

## 📌 `reduce()` vs `map()` + `filter()`

```javascript
let arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

// Juft sonlarning kvadratlari yig'indisi

// map + filter + reduce — 3 marta yuradi
let usul1 = arr
  .filter(x => x % 2 === 0)
  .map(x => x ** 2)
  .reduce((s, x) => s + x, 0);

// reduce — 1 marta yuradi (samaraliroq)
let usul2 = arr.reduce((s, x) => {
  if (x % 2 === 0) s += x ** 2;
  return s;
}, 0);

console.log(usul1); // 220
console.log(usul2); // 220
```

---

## 🎯 10 ta Amaliy Vazifa

```javascript
// 1. find() va findIndex() farqini ko'rsating
// Massivdan birinchi manfiy sonni toping (element va indeks)
let arr1 = [5, 3, -2, 8, -4, 1];
let manfiyEl = arr1.find(x => x < 0);
let manfiyIdx = arr1.findIndex(x => x < 0);
console.log(manfiyEl, manfiyIdx); // -2, 2

// 2. filter() vs find() — ikki so'rov yozing
// Ko'p: 100000 dan katta barcha sonlar
// Bitta: birinchi 100000 dan katta son
let aholi = [75000, 120000, 85000, 200000, 50000, 150000];
let kattaAholi = aholi.filter(a => a > 100000);
let birinchiKatta = aholi.find(a => a > 100000);
console.log(kattaAholi);   // [120000, 200000, 150000]
console.log(birinchiKatta); // 120000

// 3. forEach vs map — yon ta'sir va transformatsiya
let narxlar = [50000, 80000, 30000];
let diskontNarx = narxlar.map(n => n * 0.9); // 10% chegirma
console.log(diskontNarx); // [45000, 72000, 27000]

// forEach bilan DOM yangilash (simulyatsiya)
let elementlar = [];
narxlar.forEach((n, i) => {
  elementlar.push(`<li>Mahsulot ${i+1}: ${n} so'm</li>`);
});
console.log(elementlar.join(""));

// 4. Zanjirli metodlar bilan murakkab filtr
// 50-90 ball olganlari toping, ballarini 2 ga bo'ling, o'rtachasini hisoblang
let ballar = [45, 60, 85, 92, 55, 78, 30, 88];
let qayta = ballar
  .filter(b => b >= 50 && b <= 90)
  .map(b => b / 2)
  .reduce((s, b, _, arr) => s + b / arr.length, 0);
console.log(qayta.toFixed(2)); // ~34.17

// 5. findIndex bilan element almashtiring
// ID si 2 bo'lgan foydalanuvchini yangilang
let users = [
  { id: 1, ism: "Ali", faol: true },
  { id: 2, ism: "Vali", faol: false },
  { id: 3, ism: "Gani", faol: true }
];
let idx = users.findIndex(u => u.id === 2);
if (idx !== -1) users[idx] = { ...users[idx], faol: true, ism: "Valixon" };
console.log(users[1]); // { id:2, ism:"Valixon", faol:true }

// 6. reduce bilan ob'ektlar massividan statistika chiqaring
let xaridlar = [
  { mahsulot: "Kitob", narx: 50000 },
  { mahsulot: "Qalam", narx: 10000 },
  { mahsulot: "Daftar", narx: 25000 },
  { mahsulot: "Kitob", narx: 45000 }
];
let stat = xaridlar.reduce((acc, x) => {
  acc.jami += x.narx;
  acc.soni++;
  return acc;
}, { jami: 0, soni: 0 });
stat.o_rtacha = stat.jami / stat.soni;
console.log(stat);

// 7. Saralangan massivga element qo'shib, tartibini saqla
function saralab_qo_sh(arr, yangi) {
  let klon = [...arr, yangi];
  return klon.sort((a, b) => a - b);
}
console.log(saralab_qo_sh([1,3,5,7,9], 4)); // [1,3,4,5,7,9]

// 8. Takrorlanuvchi elementlarni toping
function takrorlanuchilar(arr) {
  return arr.filter((el, i) => arr.indexOf(el) !== i);
}
console.log(takrorlanuchilar([1,2,3,2,4,3,5])); // [2, 3]

// 9. Ikki massivning kesishmasini toping (ikkalasida ham bor elementlar)
function kesishma(a, b) {
  return a.filter(el => b.includes(el));
}
console.log(kesishma([1,2,3,4], [2,4,6,8])); // [2, 4]

// 10. Massivdan CRUD operatsiyalari
let mahsulotlar2 = [
  { id: 1, nomi: "Olma" },
  { id: 2, nomi: "Banan" },
  { id: 3, nomi: "Nok" }
];

// Create
function qo_shish(arr, yangi) {
  return [...arr, { id: Math.max(...arr.map(m => m.id)) + 1, ...yangi }];
}

// Read
function topish(arr, id) {
  return arr.find(m => m.id === id);
}

// Update
function yangilash(arr, id, o_zgarish) {
  return arr.map(m => m.id === id ? { ...m, ...o_zgarish } : m);
}

// Delete
function o_chirish(arr, id) {
  return arr.filter(m => m.id !== id);
}

let yangi = qo_shish(mahsulotlar2, { nomi: "Uzum" });
console.log(yangi); // 4 ta element, oxirgisi id:4, nomi:"Uzum"
```
