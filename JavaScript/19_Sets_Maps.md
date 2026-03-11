# 19-Dars: Set, Map, WeakSet, WeakMap

## 📌 Set — Noyob qiymatlar to'plami

**Set** — takrorlanmaydigan qiymatlar to'plami. Tartib saqlanadi.

```javascript
// Set yaratish
let set = new Set();
let set2 = new Set([1, 2, 3, 2, 1]); // Takrorlanuvchilar avtomatik o'chiriladi

console.log(set2); // Set(3) {1, 2, 3}
console.log(set2.size); // 3 (length emas, size!)
```

---

## 📌 Set Metodlari

```javascript
let set = new Set();

// Qo'shish
set.add(1);
set.add(2);
set.add(3);
set.add(2); // Takrorlansa qo'shilmaydi
set.add("salom");
set.add({ a: 1 }); // Ob'ektlar saqlanadi (reference bo'yicha)

// Tekshirish
console.log(set.has(2));      // true
console.log(set.has(10));     // false

// O'chirish
set.delete(2);
console.log(set.has(2));      // false

// O'lcham
console.log(set.size);        // 3

// Tozalash
// set.clear();

// Aylanish
set.forEach(qiymat => console.log(qiymat));

for (let el of set) {
  console.log(el);
}

// Massivga aylantirish
let massiv = [...set];
let massiv2 = Array.from(set);
```

---

## 📌 Set bilan Amaliy Hollar

```javascript
// 1. Takrorlanuvchi elementlarni olib tashlash
let arr = [1, 2, 3, 2, 4, 3, 5, 1];
let noyob = [...new Set(arr)];
console.log(noyob); // [1, 2, 3, 4, 5]

// 2. Ikkita massivning kesishmasi
function kesishma(a, b) {
  let bSet = new Set(b);
  return a.filter(el => bSet.has(el));
}
console.log(kesishma([1,2,3,4], [2,4,6,8])); // [2, 4]

// 3. Farqni topish
function farq(a, b) {
  let bSet = new Set(b);
  return a.filter(el => !bSet.has(el));
}
console.log(farq([1,2,3,4], [2,4])); // [1, 3]

// 4. Birlashmasi
function birlashma(a, b) {
  return [...new Set([...a, ...b])];
}
console.log(birlashma([1,2,3], [2,3,4,5])); // [1, 2, 3, 4, 5]
```

---

## 📌 Map — Kalit-Qiymat To'plami

**Map** — har qanday turdagi kalit bilan ishlovchi kalit-qiymat to'plami.

```javascript
// Map yaratish
let map = new Map();
let map2 = new Map([
  ["ism", "Ali"],
  ["yosh", 25],
  [42, "yosh raqam"]
]);

console.log(map2); // Map(3) {"ism" => "Ali", "yosh" => 25, 42 => "yosh raqam"}
console.log(map2.size); // 3
```

---

## 📌 Map Metodlari

```javascript
let map = new Map();

// Qo'shish/O'zgartirish
map.set("ism", "Ali");
map.set("yosh", 25);
map.set(true, "ha");      // boolean kalit
map.set({}, "ob'ekt");   // ob'ekt kalit (reference bo'yicha!)

// Olish
console.log(map.get("ism"));   // "Ali"
console.log(map.get(true));    // "ha"
console.log(map.get("noma'lum")); // undefined

// Tekshirish
console.log(map.has("yosh"));  // true
console.log(map.has(false));   // false

// O'chirish
map.delete("yosh");

// Aylanish
for (let [kalit, qiymat] of map) {
  console.log(`${kalit}: ${qiymat}`);
}

map.forEach((qiymat, kalit) => console.log(kalit, qiymat));

// Kalitlar, qiymatlar, juftliklar
console.log([...map.keys()]);
console.log([...map.values()]);
console.log([...map.entries()]);
```

---

## 📌 Map vs Object — Qachon nimani ishlatish?

| Xususiyat        | Map                      | Object                |
|------------------|--------------------------|-----------------------|
| Kalit turi       | Har qanday               | String/Symbol         |
| Tartib           | ✅ Saqlanadi             | ⚠️ Qisman saqlanadi  |
| O'lcham          | `.size`                  | `Object.keys().length`|
| Default kalitlar | Yo'q                     | Prototipdan keladi    |
| Serialization    | ❌ JSON.stringify yo'q   | ✅ JSON.stringify ishlaydi|
| Qachon           | Ko'p qo'shish/o'chirish  | Statik tuzilma        |

```javascript
// Map dan ob'ektga
let map = new Map([["a", 1], ["b", 2]]);
let obj = Object.fromEntries(map);
console.log(obj); // { a: 1, b: 2 }

// Ob'ektdan Mapga
let obj2 = { x: 10, y: 20 };
let map2 = new Map(Object.entries(obj2));
```

---

## 📌 WeakSet — Zaif Set

```javascript
// WeakSet faqat ob'ektlarni saqlaydi
// Garbage collection ga to'sqinlik qilmaydi
let weakSet = new WeakSet();

let obj1 = { ism: "Ali" };
let obj2 = { ism: "Vali" };

weakSet.add(obj1);
weakSet.add(obj2);
// weakSet.add(1); // ❌ TypeError — faqat ob'ekt!

console.log(weakSet.has(obj1)); // true
weakSet.delete(obj1);

// WeakSet iterable EMAS — forEach, size, keys yo'q!

// Qachon ishlatish?
// → DOM elementlarni kuzatish
// → Ob'ektni qayta ishlaganini tekshirish
let ishlangan = new WeakSet();

function ishlashYoq(el) {
  if (ishlangan.has(el)) return false;
  ishlangan.add(el);
  return true;
}
```

---

## 📌 WeakMap — Zaif Map

```javascript
let weakMap = new WeakMap();

let kalit1 = {};
let kalit2 = {};

weakMap.set(kalit1, "Ali ning datasi");
weakMap.set(kalit2, "Valining datasi");

console.log(weakMap.get(kalit1)); // "Ali ning datasi"
console.log(weakMap.has(kalit2)); // true
weakMap.delete(kalit1);

// WeakMap iterable EMAS
// Faqat: get, set, has, delete

// Qachon ishlatish?
// → Ob'ektga xususiy ma'lumot biriktirilganda
// → DOM elementlar bilan meta-ma'lumot

// Xususiy-larni saqlash pattern
const xususiy = new WeakMap();

class BankHisobi {
  constructor(egasi, balans) {
    xususiy.set(this, { egasi, balans });
  }

  balansOlish() {
    return xususiy.get(this).balans;
  }

  pul_tashlash(miqdor) {
    let data = xususiy.get(this);
    data.balans += miqdor;
  }
}

let hisob = new BankHisobi("Ali", 1000000);
console.log(hisob.balansOlish()); // 1000000
// hisob.balans — undefined (tashqaridan ko'rinmaydi!)
```

---

## 📌 Set vs Array, Map vs Object — Xulosa

```javascript
// Set — noyob qiymatlar uchun
// Array — tartibli, takrorlanadigan uchun
let arr = [1, 2, 2, 3];
let set = new Set(arr); // {1, 2, 3}
arr.includes(2); // true - O(n)
set.has(2);      // true - O(1) — tezroq!

// Map — tez qidirish uchun
// Object — oddiy ma'lumot tuzilmasi uchun
```

---

## 🎯 10 ta Amaliy Vazifa

```javascript
// 1. Set bilan takrorlanuvchi elementlarni olib tashlang
function noyobQilib(arr) {
  return [...new Set(arr)];
}
console.log(noyobQilib([1,2,3,2,4,3,5,1])); // [1,2,3,4,5]

// 2. Ikkita massivning birlashmasi, kesishmasi va farqini toping
let a = [1,2,3,4,5], b = [3,4,5,6,7];
let birlashma = [...new Set([...a, ...b])];
let kesishma = a.filter(x => new Set(b).has(x));
let farq_a = a.filter(x => !new Set(b).has(x));
console.log(birlashma, kesishma, farq_a);

// 3. Map bilan so'z chastotasini hisoblang
function chastota(matn) {
  let map = new Map();
  matn.toLowerCase().split(" ").forEach(so_z => {
    map.set(so_z, (map.get(so_z) || 0) + 1);
  });
  return map;
}
let nData = chastota("men men sen sen sen biz");
console.log([...nData.entries()]); // Tartib saqlangan!

// 4. Set bilan anagram tekshirish
function anagramMi(a, b) {
  if (a.length !== b.length) return false;
  let setA = new Set(a.toLowerCase());
  let setB = new Set(b.toLowerCase());
  if (setA.size !== setB.size) return false;
  for (let harf of setA) if (!setB.has(harf)) return false;
  return true;
}
console.log(anagramMi("listen", "silent")); // true

// 5. Map bilan student baholarini saqlang (CRUD)
let baholar = new Map();
baholar.set("Ali", [85, 90, 78]);
baholar.set("Vali", [92, 88, 95]);

// O'rtacha
function o_rtachaOlish(ism) {
  let balllar = baholar.get(ism);
  return balllar ? balllar.reduce((s,b) => s+b, 0) / balllar.length : null;
}
console.log(o_rtachaOlish("Ali")); // 84.33...

// 6. Graph (qo'shni ro'yxat) Map bilan
let graph = new Map([
  ["A", new Set(["B", "C"])],
  ["B", new Set(["A", "D"])],
  ["C", new Set(["A"])],
  ["D", new Set(["B"])]
]);

function qo_shnilarTopish(tugun) {
  return [...(graph.get(tugun) || [])];
}
console.log(qo_shnilarTopish("A")); // ["B", "C"]

// 7. WeakMap bilan kesh (memoization)
function keshliHisob() {
  let kesh = new WeakMap();
  return function(ob_ekt) {
    if (!kesh.has(ob_ekt)) {
      // og'ir hisoblash simulyatsiyasi
      kesh.set(ob_ekt, Object.values(ob_ekt).reduce((s,x) => s+x, 0));
    }
    return kesh.get(ob_ekt);
  };
}

// 8. Set bilan tashrif buyurilgan URL larni kuzating
let tashrif = new Set();
function sahifaOching(url) {
  if (tashrif.has(url)) {
    console.log("Kesh dan:", url);
  } else {
    tashrif.add(url);
    console.log("Yangi yuk:", url);
  }
}
sahifaOching("google.com");  // Yangi yuk
sahifaOching("google.com");  // Kesh dan

// 9. Map bilan qidiruv tartibi (LRU kesh simulyatsiyasi)
class LRUKesh {
  constructor(sig_im) {
    this.sig_im = sig_im;
    this.kesh = new Map();
  }
  olish(kalit) {
    if (!this.kesh.has(kalit)) return -1;
    let qiymat = this.kesh.get(kalit);
    this.kesh.delete(kalit);
    this.kesh.set(kalit, qiymat); // Oxiriga ko'chirish
    return qiymat;
  }
  qo_yish(kalit, qiymat) {
    if (this.kesh.has(kalit)) this.kesh.delete(kalit);
    else if (this.kesh.size >= this.sig_im) {
      this.kesh.delete(this.kesh.keys().next().value); // Birinchisini o'chirish
    }
    this.kesh.set(kalit, qiymat);
  }
}
let lru = new LRUKesh(3);
lru.qo_yish(1, "bir");
lru.qo_yish(2, "ikki");
lru.qo_yish(3, "uch");
console.log(lru.olish(1)); // "bir"
lru.qo_yish(4, "to'rt"); // 2 o'chiriladi (eng kam ishlatilgan)

// 10. Set bilan sudoku qatori validatsiyasi
function sudokuQatoriTo'g'rimi(qator) {
  let raqamlar = qator.filter(x => x !== 0); // 0 = bo'sh
  return new Set(raqamlar).size === raqamlar.length;
}
console.log(sudokuQatoriTo'g'rimi([1,2,3,4,5,6,7,8,9])); // true
console.log(sudokuQatoriTo'g'rimi([1,2,3,4,5,6,7,8,1])); // false (1 ta
```
