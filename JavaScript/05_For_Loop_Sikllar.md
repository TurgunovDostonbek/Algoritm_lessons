# 5-Dars: For Loop — Sikllar (Loops)

## 📌 Sikllar nima?

**Sikllar** — bir xil kodni qayta-qayta bajarishga imkon beradi. Bir xil amalni ko'p marta takrorlash o'rniga sikldan foydalanamiz.

```
JavaScript Sikllar
├── for
├── while
├── do...while
├── for...of   (massiv elementlari uchun)
└── for...in   (ob'ekt kalitlari uchun)
```

---

## 📌 for Sikli

Takrorlanish soni ma'lum bo'lganda ishlatiladi.

### Sintaksis:

```javascript
for (boshlangich; shart; qadam) {
  // bajariladigan kod
}
```

```javascript
for (let i = 0; i < 5; i++) {
  console.log(i);
}
// 0
// 1
// 2
// 3
// 4
```

**Bajarilish tartibi:**
1. `let i = 0` — bir marta bajariladi
2. `i < 5` — shart tekshiriladi
3. Shart `true` → kod bajariladi
4. `i++` — qadam bajariladi
5. 2-bandga qaytiladi... (shart `false` bo'lguncha)

---

### for Sikli — Amaliy Misollar

**1 dan 10 gacha chiqarish:**

```javascript
for (let i = 1; i <= 10; i++) {
  console.log(i);
}
```

**Faqat juft sonlar:**

```javascript
for (let i = 0; i <= 20; i += 2) {
  console.log(i); // 0, 2, 4, 6, 8, 10, 12, 14, 16, 18, 20
}
```

**Teskari tartibda:**

```javascript
for (let i = 10; i >= 1; i--) {
  console.log(i); // 10, 9, 8, 7, 6, 5, 4, 3, 2, 1
}
```

**Massiv bilan ishlash:**

```javascript
let mevalar = ["olma", "banan", "nok", "uzum"];

for (let i = 0; i < mevalar.length; i++) {
  console.log(`${i + 1}. ${mevalar[i]}`);
}
// 1. olma
// 2. banan
// 3. nok
// 4. uzum
```

**Sonlar yig'indisi:**

```javascript
let yigindi = 0;

for (let i = 1; i <= 100; i++) {
  yigindi += i;
}

console.log(yigindi); // 5050
```

---

## 📌 Nested for (Ichma-ich Sikllar)

Sikl ichida sikl — jadvallar va 2D massivlar uchun qulay.

```javascript
for (let i = 1; i <= 3; i++) {
  for (let j = 1; j <= 3; j++) {
    console.log(`i=${i}, j=${j}`);
  }
}
```

**Ko'paytirish jadvali (9x9):**

```javascript
for (let i = 1; i <= 9; i++) {
  for (let j = 1; j <= 9; j++) {
    process.stdout.write(`${i * j}\t`); // Node.js da
    // console.log(`${i} × ${j} = ${i * j}`); // Brauzerda
  }
  console.log(); // Yangi qator
}
```

**Yulduzchalar patterni:**

```javascript
// To'g'ri uchburchak
for (let i = 1; i <= 5; i++) {
  let qator = "";
  for (let j = 1; j <= i; j++) {
    qator += "* ";
  }
  console.log(qator);
}
// *
// * *
// * * *
// * * * *
// * * * * *
```

---

## 📌 while Sikli

Shart `true` bo'lguncha ishlaydi. Takrorlanish soni noma'lum bo'lganda qulay.

### Sintaksis:

```javascript
while (shart) {
  // bajariladigan kod
}
```

```javascript
let i = 0;

while (i < 5) {
  console.log(i);
  i++; // ⚠️ buni unutmang! aks holda cheksiz sikl
}
// 0, 1, 2, 3, 4
```

**Amaliy misollar:**

```javascript
// Tasodifiy son 5 bo'lguncha
let son;
let urinish = 0;

while (son !== 5) {
  son = Math.floor(Math.random() * 10) + 1;
  urinish++;
  console.log(`Urinish ${urinish}: ${son}`);
}
console.log(`5 ni ${urinish} urinishda topdik!`);
```

```javascript
// Raqamlar yig'indisi 50 dan oshguncha
let yigindi = 0;
let son2 = 1;

while (yigindi <= 50) {
  yigindi += son2;
  son2++;
}
console.log(`Yig'indi ${yigindi} ga yetdi, oxirgi son: ${son2 - 1}`);
```

---

## 📌 do...while Sikli

Kod **kamida bir marta** bajariladi, keyin shart tekshiriladi.

### Sintaksis:

```javascript
do {
  // bajariladigan kod
} while (shart);
```

```javascript
let i = 0;

do {
  console.log(i);
  i++;
} while (i < 5);
// 0, 1, 2, 3, 4
```

**while vs do-while farqi:**

```javascript
// while — shart false bo'lsa, hech narsani bajarmaydi
let x = 10;
while (x < 5) {
  console.log("while:", x); // ❌ bajarilmaydi
  x++;
}

// do-while — bir marta bajaradi, so'ng tekshiradi
let y = 10;
do {
  console.log("do-while:", y); // ✅ bir marta bajariladi!
  y++;
} while (y < 5);
```

**Amaliy misol — foydalanuvchi kirishi:**

```javascript
// Brauzerda
let javob;
do {
  javob = prompt("Parolni kiriting (1234):");
} while (javob !== "1234");

console.log("To'g'ri parol!");
```

---

## 📌 for...of Sikli (ES6)

Massiv va boshqa iterable ob'ektlar uchun qulay.

```javascript
let mevalar = ["olma", "banan", "nok"];

for (let meva of mevalar) {
  console.log(meva);
}
// olma
// banan
// nok
```

**String bilan:**

```javascript
for (let harf of "Salom") {
  console.log(harf);
}
// S, a, l, o, m
```

---

## 📌 for...in Sikli

Ob'ekt kalitlari uchun ishlatiladi.

```javascript
let shaxs = {
  ism: "Ali",
  yosh: 25,
  shahar: "Toshkent"
};

for (let kalit in shaxs) {
  console.log(`${kalit}: ${shaxs[kalit]}`);
}
// ism: Ali
// yosh: 25
// shahar: Toshkent
```

---

## 📌 continue va break

### `break` — Siklni to'xtatib chiqish

```javascript
for (let i = 0; i < 10; i++) {
  if (i === 5) {
    break; // i=5 da sikldan chiqadi
  }
  console.log(i);
}
// 0, 1, 2, 3, 4
```

### `continue` — Joriy iteratsiyani o'tkazib ketish

```javascript
for (let i = 0; i < 10; i++) {
  if (i % 2 === 0) {
    continue; // juft sonlarni o'tkazib ketadi
  }
  console.log(i);
}
// 1, 3, 5, 7, 9
```

**Amaliy misol:**

```javascript
let sonlar = [1, -3, 5, -2, 8, -7, 4];

// Faqat musbat sonlarni chiqarish
for (let son of sonlar) {
  if (son < 0) continue;
  console.log(son); // 1, 5, 8, 4
}

// Birinchi manfiy sonda to'xtash
for (let son of sonlar) {
  if (son < 0) break;
  console.log(son); // 1 (to'xtaydi)
}
```

---

## 📌 increment va decrement

```javascript
let x = 5;

// Post-increment: avval ishlatadi, keyin oshiradi
console.log(x++); // 5
console.log(x);   // 6

// Pre-increment: avval oshiradi, keyin ishlatadi
console.log(++x); // 7

// Post-decrement
console.log(x--); // 7
console.log(x);   // 6

// Pre-decrement
console.log(--x); // 5
```

**Foyda/zarar:**

```javascript
let a = 5;
let b = a++; // b=5, a=6
let c = ++a; // a=7, c=7

console.log(a, b, c); // 7 5 7
```

---

## 📌 Qaysi Siklni Ishlatish?

| Holat                                    | Sikl turi    |
|------------------------------------------|--------------|
| Takrorlanish soni ma'lum                 | `for`        |
| Shart o'zgarib turadi                   | `while`      |
| Kamida bir marta bajarilsin             | `do-while`   |
| Massiv elementlari bilan ishlash         | `for...of`   |
| Ob'ekt kalitlari bilan ishlash           | `for...in`   |

---

## 🎯 Amaliy Vazifa

```javascript
// 1. 1 dan 50 gacha 3 ga bo'linadigan sonlarni chiqaring
for (let i = 1; i <= 50; i++) {
  // ...
}

// 2. Massivdagi sonlarning o'rtachasini hisoblang
let sonlar = [12, 5, 8, 130, 44, 7, 23];
// o'rtacha = ?

// 3. Fibonacci ketma-ketligining dastlabki 10 ta sonini chiqaring
// 0, 1, 1, 2, 3, 5, 8, 13, 21, 34
let a = 0, b = 1;
for (let i = 0; i < 10; i++) {
  // ...
}

// 4. Yulduzchalar bilan kvadrat chizing (5x5)
// * * * * *
// * * * * *
// * * * * *
// * * * * *
// * * * * *

// 5. while bilan 1 dan 100 gacha sonlar ko'paytmasini hisoblang
// (lekin 1000 dan oshsa to'xtang)
```

> 📝 **Eslatma:** Cheksiz sikldan qo'rqing! `while` da shart o'zgarishiga ishonch hosil qiling.
