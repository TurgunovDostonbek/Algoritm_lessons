# 12-Dars: Array — 1-qism (Massivlar)

## 📌 Array (Massiv) nima?

**Massiv** — tartiblangan elementlar to'plami. Har bir elementga indeks orqali murojaat qilinadi (0 dan boshlanadi).

```javascript
// Array yaratish usullari

// 1. Literal (eng ko'p ishlatiladi)
let mevalar = ["olma", "banan", "nok"];

// 2. new Array()
let sonlar = new Array(1, 2, 3);
let bo_sh = new Array(5);  // 5 ta bo'sh joylik massiv
console.log(bo_sh); // [empty × 5]

// 3. Array.from()
let harflar = Array.from("Salom"); // ["S","a","l","o","m"]
let raqamlar = Array.from({length: 5}, (_, i) => i + 1); // [1,2,3,4,5]

// 4. Array.of()
let arr = Array.of(1, 2, 3); // [1, 2, 3]
```

---

## 📌 Massiv Elementlariga Murojaat

```javascript
let arr = ["olma", "banan", "nok", "uzum"];

console.log(arr[0]);    // "olma"
console.log(arr[3]);    // "uzum"
console.log(arr[-1]);   // undefined (salbiy indeks ishlamaydi!)
console.log(arr.at(-1)); // "uzum" (at() metodi — ES2022)
console.log(arr.at(-2)); // "nok"

// Uzunlik
console.log(arr.length); // 4

// Oxirgi elementni olish
console.log(arr[arr.length - 1]); // "uzum"
console.log(arr.at(-1));          // "uzum" (qulayroq)
```

---

## 📌 `push()` va `pop()` — Oxirga qo'shish va o'chirish

```javascript
let arr = [1, 2, 3];

// push — oxiriga qo'shadi, yangi uzunlikni qaytaradi
arr.push(4);       // [1, 2, 3, 4]
arr.push(5, 6);    // [1, 2, 3, 4, 5, 6]
console.log(arr.push(7)); // 7 (yangi uzunlik)

// pop — oxirini o'chiradi, o'chirilgan elementni qaytaradi
let oxirgi = arr.pop(); // 7
console.log(oxirgi); // 7
console.log(arr);    // [1, 2, 3, 4, 5, 6]
```

---

## 📌 `unshift()` va `shift()` — Boshiga qo'shish va o'chirish

```javascript
let arr = [1, 2, 3];

// unshift — boshiga qo'shadi
arr.unshift(0);       // [0, 1, 2, 3]
arr.unshift(-2, -1);  // [-2, -1, 0, 1, 2, 3]

// shift — boshini o'chiradi, o'chirilgan elementni qaytaradi
let birinchi = arr.shift(); // -2
console.log(birinchi); // -2
console.log(arr);      // [-1, 0, 1, 2, 3]
```

---

## 📌 `delete` — Elementni o'chirish (bo'shliq qoldiradi)

```javascript
let arr = [1, 2, 3, 4, 5];

delete arr[2];
console.log(arr);        // [1, 2, empty, 4, 5]
console.log(arr[2]);     // undefined
console.log(arr.length); // 5 — uzunlik o'zgarmadi!

// Tavsiya: splice ishlating — bo'shliq qoldirmaydi
```

---

## 📌 `.length` — Uzunlik (va array kesish)

```javascript
let arr = [1, 2, 3, 4, 5];

console.log(arr.length); // 5

// Length ni o'zgartirish — massivni kesish!
arr.length = 3;
console.log(arr); // [1, 2, 3] — qolganlari yo'qoldi

// Uzaytirish — bo'sh joylar paydo bo'ladi
arr.length = 6;
console.log(arr); // [1, 2, 3, empty × 3]
```

---

## 📌 `.indexOf()` va `.lastIndexOf()` — Indeksni topish

```javascript
let arr = [1, 2, 3, 2, 1];

console.log(arr.indexOf(2));      // 1 (birinchi)
console.log(arr.lastIndexOf(2));  // 3 (oxirgi)
console.log(arr.indexOf(5));      // -1 (topilmadi)

// Qidiruvni ma'lum joydan boshlash
console.log(arr.indexOf(2, 2));   // 3 (2-indeksdan boshlab)

// Massivda element borligini tekshirish
let borMi = arr.indexOf(3) !== -1;
console.log(borMi); // true
```

---

## 📌 `.includes()` — Mavjudligini tekshirish

```javascript
let arr = [1, 2, 3, NaN];

console.log(arr.includes(2));     // true
console.log(arr.includes(5));     // false
console.log(arr.includes(NaN));   // true ✅ (indexOf bilan ishlamaydi!)

// indexOf vs includes (NaN uchun)
console.log(arr.indexOf(NaN));   // -1 ❌ (NaN === NaN = false!)
console.log(arr.includes(NaN));  // true ✅
```

---

## 📌 `.reverse()` — Teskari qilish

```javascript
let arr = [1, 2, 3, 4, 5];

arr.reverse(); // O'zini o'zgartiradi!
console.log(arr); // [5, 4, 3, 2, 1]

// Asl massivni saqlash uchun
let asl = [1, 2, 3, 4, 5];
let teskari = [...asl].reverse();
console.log(asl);    // [1, 2, 3, 4, 5] — o'zgarmadi
console.log(teskari); // [5, 4, 3, 2, 1]
```

---

## 📌 `.join()` — Stringga aylantirish

```javascript
let arr = ["Ali", "Vali", "Gani"];

console.log(arr.join());       // "Ali,Vali,Gani" (default: vergul)
console.log(arr.join(" "));    // "Ali Vali Gani"
console.log(arr.join(" - "));  // "Ali - Vali - Gani"
console.log(arr.join(""));     // "AliValiGani"

// Amaliy: raqamlardan string
let raqamlar = [1, 2, 3];
console.log(raqamlar.join(".")); // "1.2.3"
```

---

## 📌 `.concat()` — Birlashtirish

```javascript
let a = [1, 2, 3];
let b = [4, 5, 6];

let c = a.concat(b);
console.log(c); // [1, 2, 3, 4, 5, 6]
console.log(a); // [1, 2, 3] — o'zgarmadi

// Ko'p massivlarni birlashtirish
let d = [0].concat(a, b, [7, 8]);
console.log(d); // [0, 1, 2, 3, 4, 5, 6, 7, 8]

// Spread bilan (zamonaviy usul)
let e = [...a, ...b];
```

---

## 📌 `.slice()` — Kesib olish (aslini o'zgartirmaydi)

```javascript
let arr = [1, 2, 3, 4, 5];

console.log(arr.slice(1, 3));  // [2, 3] (1 dan 3 gacha, 3 kirmaydi)
console.log(arr.slice(2));     // [3, 4, 5] (oxirigacha)
console.log(arr.slice(-2));    // [4, 5] (oxiridan 2 ta)
console.log(arr.slice(1, -1)); // [2, 3, 4]

console.log(arr); // [1, 2, 3, 4, 5] — o'zgarmadi!

// Massivni nusxalash
let nusxa = arr.slice();
```

---

## 📌 `.splice()` — Qo'shish/O'chirish (aslini o'zgartiradi!)

```javascript
let arr = [1, 2, 3, 4, 5];

// splice(boshlanish, o'chirish_soni, ...qo'shing)
// O'chirish
let o_chirildi = arr.splice(1, 2); // 1-indeksdan 2 ta o'chir
console.log(o'chirildi); // [2, 3]
console.log(arr);       // [1, 4, 5]

// Qo'shish (0 ta o'chirish)
arr.splice(1, 0, 10, 20);
console.log(arr); // [1, 10, 20, 4, 5]

// Almashtirish
arr.splice(1, 2, 99);
console.log(arr); // [1, 99, 4, 5]

// Oxiriga qo'shish
arr.splice(arr.length, 0, 6, 7);
console.log(arr); // [1, 99, 4, 5, 6, 7]
```

---

## 📌 Array naqshlari (Patterns)

```javascript
// 0 dan n-1 gacha massiv
const nGacha = n => Array.from({length: n}, (_, i) => i);
console.log(nGacha(5)); // [0, 1, 2, 3, 4]

// Massivni tekislash (flatten)
let ichma_ich = [[1,2], [3,4], [5,6]];
console.log(ichma_ich.flat()); // [1, 2, 3, 4, 5, 6]

// Massivni tozalash (bo'sh joylar)
let sparse = [1, , 3, , 5];
let toza = sparse.filter(() => true); // [1, 3, 5]

// Noyob elementlar
let takrorli = [1, 2, 2, 3, 3, 3];
let noyob = [...new Set(takrorli)]; // [1, 2, 3]
```

---

## 🎯 10 ta Amaliy Vazifa

```javascript
// 1. Massivning oxirgi 3 ta elementini teskari tartibda qaytaring
function oxirgiUch(arr) {
  return arr.slice(-3).reverse();
}
console.log(oxirgiUch([1,2,3,4,5,6,7])); // [7, 6, 5]

// 2. Ikki massivni birlashtirib, takrorlanuvchi elementlarni olib tashlang
function noyobBirlashtir(a, b) {
  return [...new Set([...a, ...b])];
}
console.log(noyobBirlashtir([1,2,3], [2,3,4])); // [1, 2, 3, 4]

// 3. Massivning o'rtachasini hisoblang
function o_rtacha(arr) {
  return arr.reduce((s, x) => s + x, 0) / arr.length;
}
console.log(o_rtacha([1, 2, 3, 4, 5])); // 3

// 4. Massivda berilgan element necha marta uchraganini toping
function nechaMarta(arr, element) {
  return arr.filter(x => x === element).length;
}
console.log(nechaMarta([1,2,2,3,2,4], 2)); // 3

// 5. Massivni ikkita qismga bo'ling (toq va juft indekslar)
function indeksBo'yichaAjrat(arr) {
  return {
    juft: arr.filter((_, i) => i % 2 === 0),
    toq: arr.filter((_, i) => i % 2 !== 0)
  };
}
console.log(indeksbo_yichaAjrat([10,20,30,40,50]));
// { juft: [10, 30, 50], toq: [20, 40] }

// 6. Massivning eng katta va kichik elementi orasidagi farkni toping
function amolitud(arr) {
  return Math.max(...arr) - Math.min(...arr);
}
console.log(amolitud([3,1,7,2,9,5])); // 8

// 7. Massivda berilgan element borligini tekshiring (includes + NaN uchun ham)
function borMi(arr, element) {
  return arr.includes(element);
}
console.log(borMi([1,2,NaN], NaN)); // true

// 8. Massivdan juft sonlarni olib, ularning kvadratini qaytaring
function juftKvadrat(arr) {
  return arr.filter(x => x % 2 === 0).map(x => x ** 2);
}
console.log(juftKvadrat([1,2,3,4,5,6])); // [4, 16, 36]

// 9. Massiv elementlarini chapdan o'ngga va o'ngdan chapga o'qib, 
// palindrom ekanligini tekshiring
function massivPalindromMi(arr) {
  return arr.join("") === [...arr].reverse().join("");
}
console.log(massivPalindromMi([1,2,3,2,1])); // true
console.log(massivPalindromMi([1,2,3,4,5])); // false

// 10. Zipper — ikki massivni navbatma-navbat birlashtiring
function zipper(a, b) {
  const uzun = Math.max(a.length, b.length);
  let natija = [];
  for (let i = 0; i < uzun; i++) {
    if (i < a.length) natija.push(a[i]);
    if (i < b.length) natija.push(b[i]);
  }
  return natija;
}
console.log(zipper([1,3,5], [2,4,6])); // [1,2,3,4,5,6]
```
