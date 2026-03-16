# 25-Dars: Functions (Advanced) — this, call, apply, bind

## 📌 `this` konteksti

`this` — funksiya qayerda chaqirilganiga qarab o'zgaradi.

```javascript
// 1. Global kontekst
console.log(this); // Window (brauzer) yoki global (Node.js)

// 2. Ob'ekt metodi
let shaxs = {
  ism: "Ali",
  salom() {
    console.log(this.ism); // "Ali" — this = shaxs
  }
};
shaxs.salom();

// 3. Funksiya (strict mode'da — undefined)
function test() {
  "use strict";
  console.log(this); // undefined
}

// 4. Arrow function — tashqi this ni oladi
let obj = {
  ism: "Vali",
  salom: () => {
    console.log(this.ism); // undefined — arrow this = global
  },
  async_salom() {
    setTimeout(() => {
      console.log(this.ism); // "Vali" ✅ — arrow tashqi this ni oladi
    }, 100);
  }
};

// 5. Konstruktor (new)
function Mashina(model) {
  this.model = model; // this = yangi ob'ekt
}
let mashina = new Mashina("Cobalt");
console.log(mashina.model); // "Cobalt"
```

---

## 📌 `call()` — this ni o'zgartirish (darhol chaqirish)

```javascript
function salomlash(shahar, davlat) {
  console.log(`${this.ism} - ${shahar}, ${davlat}`);
}

let ali = { ism: "Ali" };
let vali = { ism: "Vali" };

// call(this, arg1, arg2, ...)
salomlash.call(ali, "Toshkent", "O'zbekiston");  // "Ali - Toshkent, O'zbekiston"
salomlash.call(vali, "Samarqand", "O'zbekiston"); // "Vali - Samarqand, O'zbekiston"

// Metod olish (borrowing)
let hayvon = {
  nomi: "Mitti",
  tavsif() { return `Men ${this.nomi}`; }
};
let mashina2 = { nomi: "Cobalt" };

console.log(hayvon.tavsif.call(mashina2)); // "Men Cobalt"
```

---

## 📌 `apply()` — call ga o'xshash, argumentlar massivda

```javascript
function yigindi(a, b, c) {
  return a + b + c;
}

// call — argumentlar ketma-ket
yigindi.call(null, 1, 2, 3); // 6

// apply — argumentlar MASSIVDA
yigindi.apply(null, [1, 2, 3]); // 6

// Amaliy: massivdan max topish
let sonlar = [5, 3, 8, 1, 9, 2];
console.log(Math.max.apply(null, sonlar)); // 9
// Zamonaviy: Math.max(...sonlar)

// arguments ob'ektini massivga aylantirish
function argsToArray() {
  return Array.prototype.slice.call(arguments);
}
console.log(argsToArray(1, 2, 3)); // [1, 2, 3]
```

---

## 📌 `bind()` — Yangi funksiya yaratadi (darhol chaqirmaydi)

```javascript
function salomlash(shahar) {
  return `${this.ism} - ${shahar}`;
}

let ali = { ism: "Ali" };

// bind — yangi funksiya qaytaradi
let aliSalomlash = salomlash.bind(ali);
console.log(aliSalomlash("Toshkent")); // "Ali - Toshkent"
console.log(aliSalomlash("Buxoro"));   // "Ali - Buxoro"

// Qisman tatbiq (Partial Application)
function ko_paytirish(a, b) { return a * b; }
let ikkiBaravar = ko_paytirish.bind(null, 2); // a = 2 qotib qoladi
console.log(ikkiBaravar(5));  // 10
console.log(ikkiBaravar(10)); // 20

// Event listener da bind
class Hisoblagich {
  constructor() { this.hisob = 0; }
  
  oshir() { this.hisob++; console.log(this.hisob); }
  
  boshlash() {
    // ❌ this yo'qoladi:
    // document.getElementById("btn").addEventListener("click", this.oshir);
    
    // ✅ bind bilan:
    document.getElementById("btn")?.addEventListener("click", this.oshir.bind(this));
    
    // ✅ yoki arrow:
    document.getElementById("btn2")?.addEventListener("click", () => this.oshir());
  }
}
```

---

## 📌 call vs apply vs bind

| Metod   | Chaqiriladi? | Argumentlar     | Qaytarish      |
|---------|-------------|-----------------|----------------|
| `call`  | Darhol ✅   | Ketma-ket       | Funksiya natijasi |
| `apply` | Darhol ✅   | Massivda        | Funksiya natijasi |
| `bind`  | Keyinroq ❌ | Ketma-ket (qotib) | Yangi funksiya |

---

## 🎯 10 ta Amaliy Vazifa

```javascript
// 1. call bilan metod "olish"
let massiv = { 0:"a", 1:"b", 2:"c", length: 3 };
let haqiqiyMassiv = Array.prototype.slice.call(massiv);
console.log(haqiqiyMassiv); // ["a","b","c"]

// 2. apply bilan eng katta elementni toping
let sonlar = [3, 1, 7, 2, 9, 4];
console.log(Math.max.apply(null, sonlar)); // 9
console.log(Math.min.apply(null, sonlar)); // 1

// 3. bind bilan multiplier
function ko_paytir(x, y) { return x * y; }
let uchBaravar = ko_paytir.bind(null, 3);
let tortBaravar = ko_paytir.bind(null, 4);
console.log([1,2,3,4,5].map(uchBaravar));   // [3,6,9,12,15]
console.log([1,2,3,4,5].map(tortBaravar));  // [4,8,12,16,20]

// 4. this kontekstini tushunib, natijani taxmin qiling
function kim() { return this?.ism || "Global"; }
let obj1 = { ism: "Ali", kim };
let obj2 = { ism: "Vali", kim };
console.log(kim());            // "Global"
console.log(obj1.kim());       // "Ali"
console.log(obj2.kim());       // "Vali"
console.log(obj1.kim.call(obj2)); // "Vali"

// 5. Inheritance call bilan
function Hayvon(nomi, ovoz) {
  this.nomi = nomi;
  this.ovoz = ovoz;
}
function Mushuk(nomi) {
  Hayvon.call(this, nomi, "Miyov"); // super() kabi
  this.tur = "mushuk";
}
let mushuk = new Mushuk("Mitti");
console.log(mushuk.nomi, mushuk.ovoz, mushuk.tur); // "Mitti Miyov mushuk"

// 6. Funksiya koleksiyasi (bind bilan)
class UzUz {
  constructor(til = "uz") {
    this.til = til;
    this.soml = this.salom.bind(this);
  }
  salom(ism) { return `Salom ${ism}, til: ${this.til}`; }
}
let uz = new UzUz();
let { soml } = uz; // Ko'chirish
console.log(soml("Ali")); // "Salom Ali, til: uz" ✅ (bind tufayli)

// 7. apply bilan console.log
function log(...args) {
  console.log.apply(console, [">>>", ...args]);
}
log(1, 2, 3); // ">>> 1 2 3"

// 8. Mixin (bir nechta ob'ektdan metodlar olish)
let yugurish = {
  yugur() { return `${this.ism} yugurmoqda`; }
};
let suzish = {
  suz() { return `${this.ism} suzmoqda`; }
};
function Inson(ism) { this.ism = ism; }
Object.assign(Inson.prototype, yugurish, suzish);
let ali = new Inson("Ali");
console.log(ali.yugur()); // "Ali yugurmoqda"
console.log(ali.suz());   // "Ali suzmoqda"

// 9. call bilan prototype metodini ishlatish
let massivSimvol = { 0:"x", 1:"y", length:2 };
Array.prototype.push.call(massivSimvol, "z");
console.log(massivSimvol); // {0:"x",1:"y",2:"z",length:3}

// 10. Currying bind bilan
function formatlash(shablon, ...qiymatlar) {
  return qiymatlar.reduce((s, q) => s.replace("{}", q), shablon);
}
let xabarFormatlash = formatlash.bind(null, "Salom {}, {} yoshsiz!");
console.log(xabarFormatlash("Ali", 25)); // "Salom Ali, 25 yoshsiz!"
```

---

# 26-Dars: Recursive Functions (Rekursiv Funksiyalar)

## 📌 Rekursiya nima?

**Rekursiya** — funksiyaning o'zini o'zi chaqirishi. Har bir rekursiv funksiyada:
1. **Asosiy holat (Base case)** — rekursiyani to'xtatuvchi shart
2. **Rekursiv holat** — funksiya o'zini chaqiradi

```javascript
// ❌ Cheksiz rekursiya (xatoli)
function cheksiz() {
  cheksiz(); // Stack Overflow!
}

// ✅ To'g'ri rekursiya
function sanash(n) {
  if (n <= 0) return; // Base case
  console.log(n);
  sanash(n - 1);       // Rekursiv chaqiruv
}
sanash(5); // 5, 4, 3, 2, 1
```

---

## 📌 Klassik Rekursiv Misollar

```javascript
// 1. Faktorial
function faktorial(n) {
  if (n <= 1) return 1;        // Base case
  return n * faktorial(n - 1); // Rekursiv
}
console.log(faktorial(5)); // 120 (5*4*3*2*1)

// 2. Fibonacci
function fibonacci(n) {
  if (n <= 1) return n;                        // Base case: f(0)=0, f(1)=1
  return fibonacci(n - 1) + fibonacci(n - 2);  // Rekursiv
}
console.log(fibonacci(10)); // 55

// 3. Massiv yig'indisi
function massivYig_indi(arr) {
  if (arr.length === 0) return 0;        // Base case
  return arr[0] + massivYig_indi(arr.slice(1)); // Rekursiv
}
console.log(massivYig_indi([1,2,3,4,5])); // 15

// 4. Ichma-ich massivni tekislash (flat)
function tekisla(arr) {
  return arr.reduce((flat, el) =>
    Array.isArray(el) ? flat.concat(tekisla(el)) : flat.concat(el)
  , []);
}
console.log(tekisla([1,[2,[3,[4]]],5])); // [1,2,3,4,5]
```

---

## 📌 Rekursiya vs Loop

```javascript
// 1 dan n gacha yig'indisi

// Loop bilan
function yig_indiLoop(n) {
  let sum = 0;
  for (let i = 1; i <= n; i++) sum += i;
  return sum;
}

// Rekursiya bilan
function yig_indiRekursiv(n) {
  if (n <= 0) return 0;
  return n + yig_indiRekursiv(n - 1);
}

// Formulа bilan (eng tez)
function yig_indiFormula(n) {
  return n * (n + 1) / 2;
}

console.log(yig_indiLoop(100));     // 5050
console.log(yig_indiRekursiv(100)); // 5050
console.log(yig_indiFormula(100));  // 5050
```

---

## 📌 Daraxt Traversal (Rekursiyaning asosiy sohai)

```javascript
// Fayl tizimi simulyatsiyasi
let fayl_tizimi = {
  nomi: "uy",
  bolalar: [
    {
      nomi: "hujjatlar",
      bolalar: [
        { nomi: "resume.pdf", bolalar: [] },
        { nomi: "shartnoma.docx", bolalar: [] }
      ]
    },
    {
      nomi: "rasmlar",
      bolalar: [
        { nomi: "bayram.jpg", bolalar: [] }
      ]
    }
  ]
};

// Barcha fayl nomlarini chiqarish (rekursiv)
function fayllarniChiqar(tugun, chuqurlik = 0) {
  console.log(" ".repeat(chuqurlik * 2) + tugun.nomi);
  tugun.bolalar.forEach(bola => fayllarniChiqar(bola, chuqurlik + 1));
}
fayllarniChiqar(fayl_tizimi);
```

---

## 🎯 10 ta Amaliy Vazifa

```javascript
// 1. Faktorial (rekursiya)
const faktorial = n => n <= 1 ? 1 : n * faktorial(n - 1);
console.log(faktorial(10)); // 3628800

// 2. Fibonacci (memoizatsiya bilan)
function fibMemo(n, kesh = {}) {
  if (n in kesh) return kesh[n];
  if (n <= 1) return n;
  kesh[n] = fibMemo(n-1, kesh) + fibMemo(n-2, kesh);
  return kesh[n];
}
console.log(fibMemo(40)); // 102334155 (tez!)

// 3. Ob'ektning chuqurligini top
function chuqurlik(ob) {
  if (typeof ob !== "object" || ob === null) return 0;
  let maks = 0;
  for (let qiymat of Object.values(ob)) {
    maks = Math.max(maks, chuqurlik(qiymat));
  }
  return maks + 1;
}
console.log(chuqurlik({ a: { b: { c: 1 } } })); // 3

// 4. Ikkilik tizimga o'tkazish
function ikkilik(n) {
  if (n === 0) return "";
  return ikkilik(Math.floor(n/2)) + (n % 2);
}
console.log(ikkilik(13)); // "1101"

// 5. Massivni rekursiv qidirish
function rekursivQidirish(arr, maqsad, indeks = 0) {
  if (indeks >= arr.length) return -1;
  if (arr[indeks] === maqsad) return indeks;
  return rekursivQidirish(arr, maqsad, indeks + 1);
}
console.log(rekursivQidirish([1,5,3,7,2], 7)); // 3

// 6. Permutatsiyalar (barcha tartiblar)
function permutatsiyalar(str) {
  if (str.length <= 1) return [str];
  let natija = [];
  for (let i = 0; i < str.length; i++) {
    let harf = str[i];
    let qolgan = str.slice(0,i) + str.slice(i+1);
    permutatsiyalar(qolgan).forEach(p => natija.push(harf + p));
  }
  return natija;
}
console.log(permutatsiyalar("abc").length); // 6

// 7. JSON ni rekursiv tekshirish
function jsonNusxa(qiymat) {
  if (qiymat === null) return null;
  if (typeof qiymat !== "object") return qiymat;
  if (Array.isArray(qiymat)) return qiymat.map(jsonNusxa);
  return Object.fromEntries(Object.entries(qiymat).map(([k, v]) => [k, jsonNusxa(v)]));
}

// 8. Daraxtda qidirish
function daraxtQidirish(tugun, maqsad) {
  if (tugun.nomi === maqsad) return tugun;
  for (let bola of tugun.bolalar || []) {
    let topildi = daraxtQidirish(bola, maqsad);
    if (topildi) return topildi;
  }
  return null;
}
console.log(daraxtQidirish(fayl_tizimi, "resume.pdf")?.nomi); // "resume.pdf"

// 9. Raqamlar yig'indisi (1234 → 1+2+3+4 = 10)
function raqamYig_indi(n) {
  if (n < 10) return n;
  return (n % 10) + raqamYig_indi(Math.floor(n / 10));
}
console.log(raqamYig_indi(1234)); // 10
console.log(raqamYig_indi(9999)); // 36

// 10. Tower of Hanoi
function hanoi(n, boshlanish, tugash, yordamchi) {
  if (n === 1) {
    console.log(`Disk 1: ${boshlanish} → ${tugash}`);
    return;
  }
  hanoi(n-1, boshlanish, yordamchi, tugash);
  console.log(`Disk ${n}: ${boshlanish} → ${tugash}`);
  hanoi(n-1, yordamchi, tugash, boshlanish);
}
hanoi(3, "A", "C", "B");
```
