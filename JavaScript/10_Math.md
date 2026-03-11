# 10-Dars: Math (Matematika Ob'ekti)

## 📌 Math ob'ekti nima?

`Math` — JavaScript da matematik hisoblashlar uchun tayyor metodlar va konstantalar to'plami. U **statik** ob'ekt — `new Math()` qilib yaratilmaydi.

```javascript
// Math konstantalari
console.log(Math.PI);      // 3.141592653589793
console.log(Math.E);       // 2.718281828459045 (Eyler soni)
console.log(Math.SQRT2);   // 1.4142135623730951 (√2)
console.log(Math.LN2);     // 0.6931471805599453
console.log(Math.LOG2E);   // 1.4426950408889634
```

---

## 📌 `Math.abs()` — Mutlaq qiymat

```javascript
console.log(Math.abs(5));    // 5
console.log(Math.abs(-5));   // 5
console.log(Math.abs(-3.7)); // 3.7
console.log(Math.abs(0));    // 0

// Amaliy: ikkita sonning farqini hisoblash
function masofa(a, b) {
  return Math.abs(a - b);
}
console.log(masofa(10, 3));   // 7
console.log(masofa(-5, 3));   // 8
```

---

## 📌 `Math.floor()` — Pastga yaxlitlash (Tagiga)

```javascript
console.log(Math.floor(4.9));   // 4
console.log(Math.floor(4.1));   // 4
console.log(Math.floor(-4.1));  // -5 ← e'tibor bering!
console.log(Math.floor(-4.9));  // -5

// Amaliy: butun qismni olish
console.log(Math.floor(7 / 2)); // 3 (3.5 → 3)
```

---

## 📌 `Math.ceil()` — Yuqoriga yaxlitlash (Ustiga)

```javascript
console.log(Math.ceil(4.1));   // 5
console.log(Math.ceil(4.9));   // 5
console.log(Math.ceil(-4.1));  // -4 ← e'tibor bering!
console.log(Math.ceil(-4.9));  // -4

// Amaliy: sahifa soni hisoblash
function sahifaSoni(elementlar, sahifadagilar) {
  return Math.ceil(elementlar / sahifadagilar);
}
console.log(sahifaSoni(95, 10)); // 10 (9 to'la + 1 to'liqmas)
```

---

## 📌 `Math.round()` — Odatiy yaxlitlash

```javascript
console.log(Math.round(4.4));   // 4
console.log(Math.round(4.5));   // 5 (0.5 → yuqoriga)
console.log(Math.round(4.6));   // 5
console.log(Math.round(-4.5));  // -4 ← e'tibor bering!
console.log(Math.round(-4.6));  // -5

// Kasr o'rinlar bilan yaxlitlash
function yaxlitla(son, o_rin) {
  const koeffitsient = Math.pow(10, o_rin);
  return Math.round(son * koeffitsient) / koeffitsient;
}
console.log(yaxlitla(3.14159, 2)); // 3.14
console.log(yaxlitla(3.14159, 3)); // 3.142
```

---

## 📌 `Math.trunc()` — Kasr qismini olib tashlash (ES6)

```javascript
console.log(Math.trunc(4.9));   // 4  (pastga emas, kesib tashlaydi!)
console.log(Math.trunc(4.1));   // 4
console.log(Math.trunc(-4.9));  // -4 (floor: -5, trunc: -4 ← farq!)
console.log(Math.trunc(-4.1));  // -4

// floor vs trunc (manfiy sonlar uchun farq):
console.log(Math.floor(-4.5)); // -5
console.log(Math.trunc(-4.5)); // -4
```

---

## 📌 `Math.random()` — Tasodifiy son

`Math.random()` → `[0, 1)` oraliqda tasodifiy kasr son (0 kiradi, 1 kirmaydi).

```javascript
console.log(Math.random());         // 0.6231... (har safar o'zgaradi)

// 0 dan n gacha (n kirmaydi)
function tasodifiy(n) {
  return Math.floor(Math.random() * n);
}
console.log(tasodifiy(10)); // 0-9 orasida

// min dan max gacha (ikkalasi ham kiradi)
function tasodifiyOraliq(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min;
}
console.log(tasodifiyOraliq(1, 6));   // 1-6 (zar)
console.log(tasodifiyOraliq(10, 99)); // ikki xonali tasodifiy son

// Massivdan tasodifiy element
function tasodifiyElement(arr) {
  return arr[Math.floor(Math.random() * arr.length)];
}
console.log(tasodifiyElement(["olma", "banan", "nok"]));
```

---

## 📌 `Math.min()` va `Math.max()` — Minimum va Maksimum

```javascript
console.log(Math.min(1, 2, 3));      // 1
console.log(Math.max(1, 2, 3));      // 3
console.log(Math.min(-5, 0, 5));     // -5
console.log(Math.min());             // Infinity (bo'sh)
console.log(Math.max());             // -Infinity (bo'sh)

// Massivdagi min/max
let sonlar = [3, 1, 4, 1, 5, 9, 2, 6];
console.log(Math.min(...sonlar)); // 1 (spread operator bilan)
console.log(Math.max(...sonlar)); // 9
```

---

## 📌 `Math.pow()` va `Math.sqrt()` — Daraja va Ildiz

```javascript
// Daraja
console.log(Math.pow(2, 10));  // 1024 (2^10)
console.log(Math.pow(3, 3));   // 27
console.log(Math.pow(4, 0.5)); // 2 (√4 = 4^0.5)

// Zamonaviy usul (ES6)
console.log(2 ** 10);  // 1024 (Math.pow bilan bir xil)

// Ildiz
console.log(Math.sqrt(9));   // 3
console.log(Math.sqrt(2));   // 1.4142135623730951
console.log(Math.sqrt(-1));  // NaN (manfiy ildiz — kompleks son)
```

---

## 📌 `Math.cbrt()` — Kub ildiz

```javascript
console.log(Math.cbrt(27));   // 3 (∛27 = 3)
console.log(Math.cbrt(8));    // 2
console.log(Math.cbrt(-8));   // -2 (manfiy kub ildiz ishlaydi!)
console.log(Math.cbrt(1));    // 1
```

---

## 📌 `Math.sign()` — Ishorasi

```javascript
console.log(Math.sign(5));    // 1  (musbat)
console.log(Math.sign(-5));   // -1 (manfiy)
console.log(Math.sign(0));    // 0  (nol)
console.log(Math.sign(-0));   // -0

// Amaliy: tenglamaning ishorasini aniqlash
function qadam(son) {
  return Math.sign(son) === 1 ? "Yuqori" : Math.sign(son) === -1 ? "Pastga" : "Joyida";
}
```

---

## 📌 `Math.log()`, `Math.log2()`, `Math.log10()`

```javascript
console.log(Math.log(1));         // 0    (ln 1 = 0)
console.log(Math.log(Math.E));    // 1    (ln e = 1)
console.log(Math.log2(8));        // 3    (log₂ 8 = 3)
console.log(Math.log10(1000));    // 3    (log₁₀ 1000 = 3)
console.log(Math.log10(1));       // 0
```

---

## 📌 Trigonometrik Funksiyalar

```javascript
// Radianda ishlaydi (daraja emas!)
console.log(Math.sin(0));            // 0
console.log(Math.cos(0));            // 1
console.log(Math.sin(Math.PI / 2)); // 1 (sin 90° = 1)
console.log(Math.cos(Math.PI));     // -1

// Darajadan radiaanga
function darajaRadianGa(daraja) {
  return daraja * (Math.PI / 180);
}
console.log(Math.sin(darajaRadianGa(90))); // ≈ 1
```

---

## 📌 Foydali Kombinatsiyalar

```javascript
// Sonni ma'lum oraliqqa cheklash (clamp)
function chekla(son, min, max) {
  return Math.min(Math.max(son, min), max);
}
console.log(chekla(150, 0, 100)); // 100
console.log(chekla(-10, 0, 100)); // 0
console.log(chekla(50, 0, 100));  // 50

// Gipotenuza (Pifagor teoremasi)
function gipotenuza(a, b) {
  return Math.sqrt(Math.pow(a, 2) + Math.pow(b, 2));
}
console.log(gipotenuza(3, 4)); // 5

// Faktoriyel yordamida kombinatsiya hisoblash
// Tasodifiy rangni generatsiya qilish
function tasodifiyRang() {
  return "#" + Math.floor(Math.random() * 16777215).toString(16).padStart(6, "0");
}
console.log(tasodifiyRang()); // "#a3f2c1" — har safar farq qiladi
```

---

## 🎯 Amaliy Vazifalar

```javascript
// 1. Doira maydonini hisoblang (PI * r^2)
function doiraMaydoni(r) {
  return +(Math.PI * Math.pow(r, 2)).toFixed(2);
}
console.log(doiraMaydoni(5)); // 78.54

// 2. Sonni eng yaqin 10 ga yaxlitlang
function o_nGaYaxlitla(son) {
  return Math.round(son / 10) * 10;
}
console.log(o_nGaYaxlitla(45)); // 50
console.log(o_nGaYaxlitla(44)); // 40

// 3. 1 dan 100 gacha tasodifiy tort raqam generatsiya qiling
function tortRaqam() {
  let set = new Set();
  while (set.size < 4) {
    set.add(tasodifiyOraliq(1, 100));
  }
  return [...set].sort((a, b) => a - b);
}

// 4. Massivdagi eng katta va kichik qiymat o'rtachasini toping
function o_rtacha(arr) {
  return (Math.max(...arr) + Math.min(...arr)) / 2;
}
console.log(o_rtacha([3, 1, 7, 2, 9])); // (9+1)/2 = 5

// 5. Quvvat yig'indisi: 1^2 + 2^2 + ... + n^2
function kvadratYig_indi(n) {
  let yig = 0;
  for (let i = 1; i <= n; i++) yig += Math.pow(i, 2);
  return yig;
}
console.log(kvadratYig_indi(5)); // 55
```

---

## ❓ 30 ta Savol-Javob

### Boshlang'ich Savolar

**1. `Math.floor()` va `Math.ceil()` farqi nima?**
> `floor` — pastga, `ceil` — yuqoriga yaxlitlaydi.

**2. `Math.round(-4.5)` nima qaytaradi?**
> `-4` (0.5 yuqoriga, ya'ni -4 ga).

**3. `Math.random()` qanday oraliqda qaytaradi?**
> `[0, 1)` — 0 kiradi, 1 kirmaydi.

**4. 1 dan 10 gacha (ikkalasi ham kiradi) tasodifiy son qanday olinadi?**
> `Math.floor(Math.random() * 10) + 1`.

**5. `Math.pow(2, 10)` nima qaytaradi?**
> `1024`.

**6. `Math.sqrt(16)` nima?**
> `4`.

**7. `Math.abs(-7.5)` nima?**
> `7.5`.

**8. `Math.PI` qanday qiymatga ega?**
> `3.141592653589793`.

**9. `Math.min()` bo'sh chaqirilsa nima qaytaradi?**
> `Infinity`.

**10. `Math.max()` bo'sh chaqirilsa nima qaytaradi?**
> `-Infinity`.

---

### O'rta Savolar

**11. `Math.trunc()` va `Math.floor()` manfiy sonlar uchun qanday farq qiladi?**
> `Math.trunc(-4.7)` → `-4` (kesib tashlaydi), `Math.floor(-4.7)` → `-5` (pastga yaxlitlaydi).

**12. Massivdagi maksimal sonni `Math.max` bilan qanday topamiz?**
> `Math.max(...massiv)` yoki `Math.max.apply(null, massiv)`.

**13. `Math.cbrt(-27)` nima?**
> `-3`.

**14. `Math.sign(-0)` nima?**
> `-0`.

**15. Tasodifiy rangni qanday yasaymiz?**
> `"#" + Math.floor(Math.random() * 16777215).toString(16).padStart(6, "0")`.

**16. `Math.log10(10000)` nima?**
> `4`.

**17. `Math.sqrt(-4)` nima?**
> `NaN`.

**18. Sonni oraliqqa cheklash (clamp) qanday amalga oshiriladi?**
> `Math.min(Math.max(son, min), max)`.

**19. `Math.pow(4, 0.5)` nima?**
> `2` — bu `√4` bilan bir xil.

**20. Doira maydonini qanday hisoblaymiz?**
> `Math.PI * r * r` yoki `Math.PI * Math.pow(r, 2)`.

---

### Murakkab Savolar

**21. Quyidagi kod nima chiqaradi?**
```javascript
console.log(Math.max([], 0));
```
> `0`. `[]` → `0` ga aylanadi.

**22. `Math.round()` bilan ikki o'rinli kasr yaxlitlash qanday?**
> `Math.round(son * 100) / 100`.

**23. `Math.random()` kriptografik xavfsizmi?**
> Yo'q. Kripto uchun `crypto.getRandomValues()` ishlatiladi.

**24. `Math.log(0)` nima?**
> `-Infinity`.

**25. Pifagor teoremasi qanday yoziladi?**
> `Math.sqrt(Math.pow(a, 2) + Math.pow(b, 2))` yoki `Math.hypot(a, b)`.

**26. `Math.hypot()` nima?**
> Ko'p argumentli gipotenuza: `Math.hypot(3, 4)` → `5`.

**27. `** ` operatori va `Math.pow()` farqi?**
> Funksional jihatdan bir xil. `2 ** 10` ES6 dan beri mavjud, `Math.pow(2, 10)` eski usul.

**28. `Math.fround()` nimaga xizmat qiladi?**
> 32-bit (single precision) float qiymat olish uchun: WebGL va binary hisoblashlarda.

**29. Quyidagi kod nima chiqaradi?**
```javascript
console.log(Math.round(0.5));
console.log(Math.round(-0.5));
```
> `1` va `-0`. (-0.5 → yuqoriga: -0).

**30. Sonni eng yaqin 5 ga yaxlitlash?**
```javascript
function beshGaYaxlitla(n) {
  return Math.round(n / 5) * 5;
}
console.log(beshGaYaxlitla(13)); // 15
console.log(beshGaYaxlitla(12)); // 10
```
