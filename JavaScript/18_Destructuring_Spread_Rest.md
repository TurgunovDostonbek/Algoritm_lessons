# 18-Dars: Destructuring, Spread & Rest

## 📌 Destructuring nima?

**Destructuring** — massiv yoki ob'ektdan qiymatlarni alohida o'zgaruvchilarga chiqarish usuli (ES6).

---

## 📌 Array Destructuring

```javascript
let arr = [1, 2, 3, 4, 5];

// Odatiy usul
let a = arr[0]; // 1
let b = arr[1]; // 2

// Destructuring
let [x, y, z] = arr;
console.log(x, y, z); // 1 2 3

// Ba'zilarini o'tkazib ketish
let [birinchi, , uchinchi] = arr; // ikkinchisini o'tkazib ketding
console.log(birinchi, uchinchi); // 1 3

// Default qiymat
let [p = 10, q = 20, r = 30] = [1, 2];
console.log(p, q, r); // 1 2 30

// Rest element bilan
let [bosh, ...qolgan] = arr;
console.log(bosh);    // 1
console.log(qolgan);  // [2, 3, 4, 5]

// Ikkita o'zgaruvchini almashtirish!
let m = 5, n = 10;
[m, n] = [n, m];
console.log(m, n); // 10 5 ✅
```

---

## 📌 Object Destructuring

```javascript
let shaxs = {
  ism: "Ali",
  yosh: 25,
  shahar: "Toshkent",
  ish: { kompaniya: "Tech Corp", lavozim: "Developer" }
};

// Asosiy destructuring
let { ism, yosh } = shaxs;
console.log(ism, yosh); // "Ali" 25

// Qayta nomlash
let { ism: talabaNomi, yosh: muddati } = shaxs;
console.log(talabaNomi); // "Ali"

// Default qiymat
let { email = "noma'lum@email.com" } = shaxs;
console.log(email); // "noma'lum@email.com"

// Ichki ob'ekt destructuring
let { ish: { kompaniya, lavozim } } = shaxs;
console.log(kompaniya, lavozim); // "Tech Corp" "Developer"

// Rest bilan
let { ism: nom, ...qolganlar } = shaxs;
console.log(nom);       // "Ali"
console.log(qolganlar); // { yosh:25, shahar:"Toshkent", ish:{...} }
```

---

## 📌 Funksiya Parametrlarida Destructuring

```javascript
// Ob'ekt parametr
function salomlash({ ism, yosh = 18, shahar = "Toshkent" }) {
  return `${ism} (${yosh} yosh, ${shahar})`;
}

console.log(salomlash({ ism: "Ali", yosh: 25 }));        // "Ali (25 yosh, Toshkent)"
console.log(salomlash({ ism: "Vali", shahar: "Buxoro" })); // "Vali (18 yosh, Buxoro)"

// Array parametr
function birinchiIkkinchi([birinchi, ikkinchi]) {
  return `${birinchi} va ${ikkinchi}`;
}
console.log(birinchiIkkinchi([10, 20, 30])); // "10 va 20"
```

---

## 📌 Spread Operator (`...`) — Yoying

```javascript
// Massivda
let a = [1, 2, 3];
let b = [4, 5, 6];

let birlashdi = [...a, ...b];
console.log(birlashdi); // [1, 2, 3, 4, 5, 6]

// O'rtaga qo'shish
let c = [...a, 99, ...b];
console.log(c); // [1, 2, 3, 99, 4, 5, 6]

// Nusxa ko'chirish (shallow)
let nusxa = [...a];

// Ob'ektda
let obj1 = { a: 1, b: 2 };
let obj2 = { c: 3, d: 4 };

let birlashdOb = { ...obj1, ...obj2 };
console.log(birlashdOb); // { a:1, b:2, c:3, d:4 }

// Xususiyatni o'zgartirish
let yangi = { ...obj1, b: 999 };
console.log(yangi); // { a:1, b:999 }

// Funksiya chaqirishda
let sonlar = [3, 1, 4, 1, 5, 9];
console.log(Math.max(...sonlar));  // 9
console.log(Math.min(...sonlar));  // 1

// String ni massivga
let harflar = [..."JavaScript"];
console.log(harflar); // ["J","a","v","a","S","c","r","i","p","t"]
```

---

## 📌 Rest Parametr (`...`) — Yig'ing

```javascript
// Funksiyada — qolgan argumentlarni massivga yig'adi
function yigindi(...sonlar) {
  return sonlar.reduce((s, x) => s + x, 0);
}
console.log(yigindi(1, 2, 3));       // 6
console.log(yigindi(1, 2, 3, 4, 5)); // 15

// Birinchi argumentlardan keyin qolganlari
function birinchiVaQolgan(birinchi, ikkinchi, ...qolgan) {
  console.log(birinchi); // 1
  console.log(ikkinchi); // 2
  console.log(qolgan);   // [3, 4, 5]
}
birinchiVaQolgan(1, 2, 3, 4, 5);

// ⚠️ Rest faqat oxirda bo'lishi mumkin!
// function xato(a, ...rest, b) {} // SyntaxError!
```

---

## 📌 Spread vs Rest — Farqi

| Xususiyat    | Spread (`...`)            | Rest (`...`)             |
|--------------|---------------------------|--------------------------|
| Maqsad       | Massiv/ob'ektni yoyish    | Elementlarni yig'ish      |
| Joyi         | Chaqirishda, yaratishda   | Funksiya parametrida      |
| Natija       | Ko'p qiymat               | Massiv                    |

```javascript
// Spread — yoyish
let arr = [1, 2, 3];
funksiya(...arr);   // funksiya(1, 2, 3)

// Rest — yig'ish
function f(...args) {} // f(1,2,3) → args=[1,2,3]
```

---

## 🎯 10 ta Amaliy Vazifa

```javascript
// 1. Ko'paytirish jadvalini destructuring bilan yozing
let [satr, ustun] = [5, 4];
console.log(`${satr} × ${ustun} = ${satr * ustun}`); // 5 × 4 = 20

// 2. Funksiyadan bir nechta qiymat qaytarish
function minMax(arr) {
  return [Math.min(...arr), Math.max(...arr)];
}
let [min, max] = minMax([3, 1, 7, 2, 9]);
console.log(min, max); // 1 9

// 3. Ob'ektni boshqa formatga aylantiring
function formatFoydalanuvchi({ ism, familiya, yosh }) {
  return { toliIsm: `${ism} ${familiya}`, muddati: yosh };
}
let f = formatFoydalanuvchi({ ism: "Ali", familiya: "Valiev", yosh: 25 });
console.log(f); // { toliIsm: "Ali Valiev", muddati: 25 }

// 4. Nested destructuring
let data = {
  foydalanuvchi: {
    profil: { ism: "Bobur", shahar: "Samarqand" },
    sozlamalar: { tema: "qorongu", til: "uz" }
  }
};
let { foydalanuvchi: { profil: { ism, shahar }, sozlamalar: { tema } } } = data;
console.log(ism, shahar, tema); // "Bobur" "Samarqand" "qorongu"

// 5. Massivni teskari aylantiring (destructuring bilan)
function teskari([birinchi, ...qolgan]) {
  if (qolgan.length === 0) return [birinchi];
  return [...teskari(qolgan), birinchi];
}
console.log(teskari([1, 2, 3, 4, 5])); // [5, 4, 3, 2, 1]

// 6. Har qanday sondagi argumentlarni hisobalovchi funksiya
function hisob(amal, ...sonlar) {
  switch (amal) {
    case "q": return sonlar.reduce((s, x) => s + x, 0);
    case "k": return sonlar.reduce((p, x) => p * x, 1);
    case "a": return sonlar.reduce((s, x) => s + x, 0) / sonlar.length;
    default: return "Noma'lum amal";
  }
}
console.log(hisob("q", 1, 2, 3, 4));    // 10
console.log(hisob("k", 2, 3, 4));       // 24

// 7. Ob'ektlarni birlashtirish (chuqur)
function birlashtir(...ob_ektlar) {
  return Object.assign({}, ...ob_ektlar);
}
let natija = birlashtir({ a: 1 }, { b: 2 }, { c: 3 });
console.log(natija); // { a:1, b:2, c:3 }

// 8. Massivning 1,3,5 indexed elementlarini oling (destructuring bilan)
let [, b1, , d1, , f1] = [10, 20, 30, 40, 50, 60];
console.log(b1, d1, f1); // 20 40 60

// 9. API javobini parse qiling
function apiParse({ data: { users, total }, meta: { page = 1 } = {} }) {
  return { foydalanuvchilar: users.map(u => u.name), jami: total, sahifa: page };
}
let apiJavob = {
  data: { users: [{ name: "Ali" }, { name: "Vali" }], total: 2 },
  meta: { page: 3 }
};
console.log(apiParse(apiJavob));
// { foydalanuvchilar: ["Ali","Vali"], jami: 2, sahifa: 3 }

// 10. Karta o'yini — aralash kartalar
function aralash(kartalar) {
  let nusxa = [...kartalar];
  for (let i = nusxa.length - 1; i > 0; i--) {
    let j = Math.floor(Math.random() * (i + 1));
    [nusxa[i], nusxa[j]] = [nusxa[j], nusxa[i]]; // Destructuring bilan almashtirish!
  }
  return nusxa;
}
let kortlar = ["♠A", "♥K", "♦Q", "♣J", "♠10"];
console.log(aralash(kortlar));
```
