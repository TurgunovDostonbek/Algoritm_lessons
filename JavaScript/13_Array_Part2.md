# 13-Dars: Array — 2-qism (Kengaytirilgan Metodlar)

## 📌 `.forEach()` — Har bir element ustida amal

```javascript
let arr = [1, 2, 3, 4, 5];

// forEach — qaytarish qiymati yo'q (undefined)
arr.forEach(function(element, indeks, massiv) {
  console.log(`[${indeks}]: ${element}`);
});

// Arrow function bilan
arr.forEach((el, i) => console.log(`${i}: ${el}`));

// Amaliy: ob'ektlar massivi
let talabalar = [
  { ism: "Ali", ball: 85 },
  { ism: "Vali", ball: 92 },
  { ism: "Gani", ball: 78 }
];

talabalar.forEach(t => {
  console.log(`${t.ism}: ${t.ball}`);
});

// ⚠️ forEach ni break bilan to'xtatib bo'lmaydi!
// Buning uchun for...of yoki some() ishlating
```

---

## 📌 `.map()` — Yangi massiv yaratish (transformatsiya)

```javascript
let sonlar = [1, 2, 3, 4, 5];

// Har bir elementning kvadratini olish
let kvadratlar = sonlar.map(x => x ** 2);
console.log(kvadratlar); // [1, 4, 9, 16, 25]
console.log(sonlar);     // [1, 2, 3, 4, 5] — o'zgarmadi!

// String massivini o'zgartirish
let ismlar = ["ali", "vali", "gani"];
let katta = ismlar.map(ism => ism.toUpperCase());
console.log(katta); // ["ALI", "VALI", "GANI"]

// Ob'ektlar massivida
let talabalar = [
  { ism: "Ali", ball: 85 },
  { ism: "Vali", ball: 90 }
];
let faqatIsmlar = talabalar.map(t => t.ism);
console.log(faqatIsmlar); // ["Ali", "Vali"]

// Indeks bilan
let indeksli = ["a", "b", "c"].map((el, i) => `${i}: ${el}`);
console.log(indeksli); // ["0: a", "1: b", "2: c"]
```

---

## 📌 `.filter()` — Shartga mos elementlar

```javascript
let sonlar = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

// Juft sonlar
let juft = sonlar.filter(x => x % 2 === 0);
console.log(juft); // [2, 4, 6, 8, 10]

// 5 dan katta
let katta = sonlar.filter(x => x > 5);
console.log(katta); // [6, 7, 8, 9, 10]

// Ob'ektlar massivida
let mahsulotlar = [
  { nomi: "Olma", narx: 5000 },
  { nomi: "Banan", narx: 8000 },
  { nomi: "Nok", narx: 3000 },
  { nomi: "Uzum", narx: 12000 }
];

let arzon = mahsulotlar.filter(m => m.narx < 8000);
console.log(arzon); // [{nomi:"Olma",...}, {nomi:"Nok",...}]

// Falsy qiymatlarni olib tashlash
let aralash = [0, 1, false, 2, "", 3, null, undefined, NaN, 4];
let toza = aralash.filter(Boolean); // Boolean(x) → truthy
console.log(toza); // [1, 2, 3, 4]
```

---

## 📌 `.find()` — Birinchi mos elementni topish

```javascript
let sonlar = [2, 4, 6, 7, 8, 10];

// Birinchi toq sonni top
let birinchiToq = sonlar.find(x => x % 2 !== 0);
console.log(birinchiToq); // 7 (topildi → element qaytaradi)

// Topilmasa — undefined
let manfiy = sonlar.find(x => x < 0);
console.log(manfiy); // undefined

// Ob'ektlar massivida
let foydalanuvchilar = [
  { id: 1, ism: "Ali" },
  { id: 2, ism: "Vali" },
  { id: 3, ism: "Gani" }
];

let topildi = foydalanuvchilar.find(f => f.id === 2);
console.log(topildi); // { id: 2, ism: "Vali" }
```

---

## 📌 `.findIndex()` — Birinchi mos elementning indeksi

```javascript
let arr = [5, 12, 8, 130, 44];

let indeks = arr.findIndex(x => x > 10);
console.log(indeks); // 1 (12 ning indeksi)

// Topilmasa — -1
let yoq = arr.findIndex(x => x > 1000);
console.log(yoq); // -1

// Ob'ektlar massivida
let users = [
  { id: 1, ism: "Ali" },
  { id: 2, ism: "Vali" }
];
let idx = users.findIndex(u => u.id === 2);
users[idx].ism = "Valixon"; // O'zgartirish
console.log(users[1]); // { id: 2, ism: "Valixon" }
```

---

## 📌 `.findLast()` va `.findLastIndex()` — Oxiridan qidirish (ES2023)

```javascript
let arr = [1, 2, 3, 4, 5, 4, 3];

console.log(arr.findLast(x => x > 3));      // 4 (oxiridan birinchi)
console.log(arr.findLastIndex(x => x > 3)); // 5 (4 ning oxirgi indeksi)
```

---

## 📌 `.sort()` — Saralash

```javascript
// ⚠️ Default: Satrga aylantirib saralaydi!
let arr = [10, 1, 21, 2];
console.log(arr.sort()); // [1, 10, 2, 21] ← Noto'g'ri!

// ✅ Sonlarni to'g'ri saralash
arr.sort((a, b) => a - b); // O'sish tartibida
console.log(arr); // [1, 2, 10, 21]

arr.sort((a, b) => b - a); // Kamayish tartibida
console.log(arr); // [21, 10, 2, 1]

// Satrlarni saralash
let ismlar = ["Zebra", "Ali", "Mehmet", "Bobur"];
ismlar.sort(); // Alifbo tartibida
console.log(ismlar); // ["Ali", "Bobur", "Mehmet", "Zebra"]

// Ob'ektlar massivini saralash
let talabalar = [
  { ism: "Vali", ball: 85 },
  { ism: "Ali", ball: 95 },
  { ism: "Gani", ball: 78 }
];
talabalar.sort((a, b) => b.ball - a.ball); // Ball bo'yicha kamayish
console.log(talabalar); // Ali(95), Vali(85), Gani(78)
```

---

## 📌 `.every()` va `.some()` — Barchasi / Bittasi

```javascript
let arr = [2, 4, 6, 8, 10];

// every — barchasi shartga mos kelsa true
console.log(arr.every(x => x % 2 === 0));  // true (barchasi juft)
console.log(arr.every(x => x > 5));        // false (2, 4 < 5)

// some — kamida bittasi shartga mos kelsa true
console.log(arr.some(x => x > 8));   // true (10 > 8)
console.log(arr.some(x => x > 100)); // false

// Amaliy
let ballar = [85, 92, 78, 65, 88];
let hammaBirdan = ballar.every(b => b >= 50);  // barchasi o'tdimi?
let bittaYaxshi = ballar.some(b => b >= 90);   // bittasi a'lochi?
console.log(hammaBirdan); // true
console.log(bittaYaxshi); // true (92)
```

---

## 📌 `.flat()` va `.flatMap()` — Tekislash

```javascript
// flat — ichma-ich massivlarni tekislash
let ichma_ich = [1, [2, 3], [4, [5, 6]]];

console.log(ichma_ich.flat());    // [1, 2, 3, 4, [5, 6]] (1 chuqurlik)
console.log(ichma_ich.flat(2));   // [1, 2, 3, 4, 5, 6]  (2 chuqurlik)
console.log(ichma_ich.flat(Infinity)); // [1,2,3,4,5,6] (cheksiz)

// flatMap — map + flat (1 daraja)
let jumlalar = ["Salom Dunyo", "JavaScript Ajoyib"];
let so_zlar = jumlalar.flatMap(j => j.split(" "));
console.log(so_zlar); // ["Salom", "Dunyo", "JavaScript", "Ajoyib"]

// map + flat bilan bir xil:
// jumlalar.map(j => j.split(" ")).flat()
```

---

## 📌 `.copyWithin()` — Ichida ko'chirish

```javascript
let arr = [1, 2, 3, 4, 5];

// copyWithin(maqsad, boshlash, tugash)
console.log([1,2,3,4,5].copyWithin(0, 3));    // [4,5,3,4,5]
console.log([1,2,3,4,5].copyWithin(1, 3));    // [1,4,5,4,5]
console.log([1,2,3,4,5].copyWithin(0, 3, 4)); // [4,2,3,4,5]
```

---

## 📌 `.reduce()` — Yig'ish (qisqartirish)

```javascript
let arr = [1, 2, 3, 4, 5];

// Yig'indi
let yigindi = arr.reduce((jamlanma, joriy) => jamlanma + joriy, 0);
console.log(yigindi); // 15

// Ko'paytma
let kopaytma = arr.reduce((j, x) => j * x, 1);
console.log(kopaytma); // 120

// Eng katta element
let max = arr.reduce((max, x) => x > max ? x : max, -Infinity);
console.log(max); // 5

// Ob'ekt yaratish
let talabalar = ["Ali", "Vali", "Gani"];
let ob_ekt = talabalar.reduce((acc, ism, i) => {
  acc[i] = ism;
  return acc;
}, {});
console.log(ob_ekt); // {0:"Ali", 1:"Vali", 2:"Gani"}

// Elementlar sonini hisoblash
let mevalar = ["olma", "banan", "olma", "nok", "banan", "olma"];
let hisob = mevalar.reduce((acc, meva) => {
  acc[meva] = (acc[meva] || 0) + 1;
  return acc;
}, {});
console.log(hisob); // {olma:3, banan:2, nok:1}
```

---

## 🎯 10 ta Amaliy Vazifa

```javascript
// 1. Massivdan 18 dan katta yoshdagi foydalanuvchilar ismlarini chiqaring
let users = [
  { ism: "Ali", yosh: 15 },
  { ism: "Vali", yosh: 22 },
  { ism: "Gani", yosh: 17 },
  { ism: "Sani", yosh: 25 }
];
let kattalar = users.filter(u => u.yosh >= 18).map(u => u.ism);
console.log(kattalar); // ["Vali", "Sani"]

// 2. Sonlar massivining yig'indisi, ko'paytmasi va o'rtachasini toping
function statistika(arr) {
  const yigindi = arr.reduce((s, x) => s + x, 0);
  return {
    yigindi,
    kopaytma: arr.reduce((p, x) => p * x, 1),
    o_rtacha: yigindi / arr.length
  };
}
console.log(statistika([1, 2, 3, 4, 5])); // {yigindi:15, kopaytma:120, ...}

// 3. Massivni "chunk" larga bo'ling (n ta elementlik guruhlar)
function chunk(arr, n) {
  let natija = [];
  for (let i = 0; i < arr.length; i += n) {
    natija.push(arr.slice(i, i + n));
  }
  return natija;
}
console.log(chunk([1,2,3,4,5,6,7], 3)); // [[1,2,3],[4,5,6],[7]]

// 4. Ob'ektlar massivini berilgan kalit bo'yicha guruhlang
function guruhlash(arr, kalit) {
  return arr.reduce((acc, el) => {
    let guruh = el[kalit];
    if (!acc[guruh]) acc[guruh] = [];
    acc[guruh].push(el);
    return acc;
  }, {});
}
let mahsulotlar = [
  {nomi:"Olma", tur:"Meva"},
  {nomi:"Sabzi", tur:"Sabzavot"},
  {nomi:"Banan", tur:"Meva"}
];
console.log(guruhlash(mahsulotlar, "tur"));

// 5. Massivdagi juft sonlar yig'indisi
function juftYigindi(arr) {
  return arr.filter(x => x % 2 === 0).reduce((s, x) => s + x, 0);
}
console.log(juftYigindi([1,2,3,4,5,6])); // 12

// 6. Tartiblangan massivga element qo'ring (tartibi saqlansin)
function tartibliQo_sh(arr, element) {
  let nusxa = [...arr];
  nusxa.push(element);
  return nusxa.sort((a, b) => a - b);
}
console.log(tartibliQo_sh([1,3,5,7], 4)); // [1,3,4,5,7]

// 7. Har bir so'z necha marta uchraganini hisoblab chiqaring
function so_zHisobi(matn) {
  return matn.toLowerCase().split(" ").reduce((acc, so_z) => {
    acc[so_z] = (acc[so_z] || 0) + 1;
    return acc;
  }, {});
}
console.log(so_zHisobi("men sen men biz men sen"));
// { men:3, sen:2, biz:1 }

// 8. Massivdan kattalar (18+) ni toping va ularning o'rtacha yoshini hisoblang
function kattalarO_rtachaYosh(users) {
  let kattalar = users.filter(u => u.yosh >= 18);
  if (kattalar.length === 0) return 0;
  return kattalar.reduce((s, u) => s + u.yosh, 0) / kattalar.length;
}
console.log(kattalarO_rtachaYosh(users)); // 23.5

// 9. "Pipeline" — funksiyalar massivini ketma-ket qo'llang
function pipeline(qiymat, ...fnlar) {
  return fnlar.reduce((acc, fn) => fn(acc), qiymat);
}
let natija = pipeline(
  5,
  x => x * 2,      // 10
  x => x + 3,      // 13
  x => x ** 2      // 169
);
console.log(natija); // 169

// 10. Matritsani transpozitsiya qiling (satr ↔ ustun)
function transpozitsiya(matritsa) {
  return matritsa[0].map((_, i) => matritsa.map(satr => satr[i]));
}
let m = [[1,2,3],[4,5,6],[7,8,9]];
console.log(transpozitsiya(m));
// [[1,4,7],[2,5,8],[3,6,9]]
```
