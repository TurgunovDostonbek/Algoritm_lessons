# 11-Dars: Objects (Ob'ektlar)

## 📌 Ob'ekt nima?

**Ob'ekt** — `kalit: qiymat` juftliklar to'plami. Murakkab ma'lumotlarni bir joyda saqlash uchun ishlatiladi.

```javascript
// Ob'ekt yaratish
let shaxs = {
  ism: "Ali",          // kalit: qiymat
  yosh: 25,
  talabami: true,
  manzil: {            // ichki ob'ekt
    shahar: "Toshkent",
    ko_cha: "Navoiy"
  }
};

console.log(typeof shaxs); // "object"
```

---

## 📌 Ob'ekt Yaratish Usullari

### 1. Literal sintaksis (eng ko'p ishlatiladi)

```javascript
let mashina = {
  marka: "Chevrolet",
  model: "Cobalt",
  yil: 2022
};
```

### 2. `new Object()` (eski usul)

```javascript
let mashina = new Object();
mashina.marka = "Chevrolet";
mashina.model = "Cobalt";
```

### 3. `Object.create()` — Prototip bilan yaratish

```javascript
let hayvonProto = {
  salom() {
    console.log(`Men ${this.ism}`);
  }
};

let mushuk = Object.create(hayvonProto);
mushuk.ism = "Mitti";
mushuk.salom(); // "Men Mitti"
```

### 4. Konstruktor funksiya

```javascript
function Shaxs(ism, yosh) {
  this.ism = ism;
  this.yosh = yosh;
  this.salom = function() {
    return `Salom, men ${this.ism}!`;
  };
}

let ali = new Shaxs("Ali", 25);
let vali = new Shaxs("Vali", 30);
console.log(ali.salom()); // "Salom, men Ali!"
```

---

## 📌 Xususiyatlarga Murojaat

```javascript
let shaxs = { ism: "Ali", yosh: 25 };

// 1. Nuqta orqali (dot notation)
console.log(shaxs.ism);   // "Ali"
shaxs.shahar = "Toshkent"; // qo'shish

// 2. Qavslar orqali (bracket notation)
console.log(shaxs["yosh"]); // 25
let kalit = "ism";
console.log(shaxs[kalit]);  // "Ali" — dinamik kalit uchun foydali!

// Mavjud bo'lmagan xususiyat
console.log(shaxs.telefon); // undefined (xato emas)
```

---

## 📌 Xususiyatlarni Qo'shish, O'zgartirish, O'chirish

```javascript
let obj = { a: 1, b: 2 };

// Qo'shish
obj.c = 3;
obj["d"] = 4;

// O'zgartirish
obj.a = 10;

// O'chirish
delete obj.b;

console.log(obj); // { a: 10, c: 3, d: 4 }
```

---

## 📌 Xususiyatlar Shorthand (ES6)

```javascript
let ism = "Ali";
let yosh = 25;

// Eski usul
let shaxs1 = { ism: ism, yosh: yosh };

// Yangi usul (shorthand) — kalit va o'zgaruvchi nomi bir xil bo'lsa
let shaxs2 = { ism, yosh };

console.log(shaxs2); // { ism: "Ali", yosh: 25 }
```

---

## 📌 Computed Property Names (Dinamik Kalit)

```javascript
let kalit = "ism";

let obj = {
  [kalit]: "Ali",        // kalit o'zgaruvchidan olinadi → ism: "Ali"
  [`${kalit}2`]: "Vali"  // "ism2": "Vali"
};

console.log(obj.ism);  // "Ali"
console.log(obj.ism2); // "Vali"
```

---

## 📌 Metodlar (Ob'ekt Funksiyalari)

```javascript
let hisoblagich = {
  qiymat: 0,

  // Metod e'lon qilish
  oshir: function() {
    this.qiymat++;
  },

  // Qisqa sintaks (ES6)
  kamayt() {
    this.qiymat--;
  },

  // Arrow funksiya — this ishlamaydi!
  nol: () => {
    // this.qiymat = 0; ← ❌ ishlamaydi
  }
};

hisoblagich.oshir();
hisoblagich.oshir();
hisoblagich.kamayt();
console.log(hisoblagich.qiymat); // 1
```

---

## 📌 `this` kalit so'zi

```javascript
let shaxs = {
  ism: "Ali",
  salom() {
    console.log(`Salom, men ${this.ism}!`);
  }
};

shaxs.salom(); // "Salom, men Ali!" ✅

// this kontekst yo'qolsa
let fn = shaxs.salom;
fn(); // "Salom, men undefined!" ← this = global
```

---

## 📌 Ob'ektni Ko'chirish

```javascript
let asl = { a: 1, b: 2 };

// ❌ Yuzaki ko'chirma (reference ko'chiriladi)
let nusxa1 = asl;
nusxa1.a = 100;
console.log(asl.a); // 100 — o'zgardi!

// ✅ Yuzaki nusxa (Shallow Copy)
let nusxa2 = { ...asl };         // Spread operator
let nusxa3 = Object.assign({}, asl); // assign
nusxa2.a = 999;
console.log(asl.a); // 1 — o'zgarmadi ✅

// ⚠️ Ichki ob'ektlar hali ham reference!
let obj = { a: 1, b: { c: 2 } };
let shallow = { ...obj };
shallow.b.c = 999;
console.log(obj.b.c); // 999 — ichki ob'ekt o'zgardi!

// ✅ Chuqur nusxa (Deep Copy)
let deep = JSON.parse(JSON.stringify(obj));
deep.b.c = 777;
console.log(obj.b.c); // 999 — o'zgarmadi ✅
```

---

## 📌 Ob'ekt Metodlari (Static)

### `Object.keys()` — Kalitlar

```javascript
let shaxs = { ism: "Ali", yosh: 25, shahar: "Toshkent" };

console.log(Object.keys(shaxs));
// ["ism", "yosh", "shahar"]
```

### `Object.values()` — Qiymatlar

```javascript
console.log(Object.values(shaxs));
// ["Ali", 25, "Toshkent"]
```

### `Object.entries()` — Juftliklar

```javascript
console.log(Object.entries(shaxs));
// [["ism", "Ali"], ["yosh", 25], ["shahar", "Toshkent"]]

// Amaliy: ob'ekt ustida loop
for (let [kalit, qiymat] of Object.entries(shaxs)) {
  console.log(`${kalit}: ${qiymat}`);
}
```

### `Object.assign()` — Qo'shish/Birlashtirish

```javascript
let maqsad = { a: 1 };
let manba = { b: 2, c: 3 };

Object.assign(maqsad, manba);
console.log(maqsad); // { a: 1, b: 2, c: 3 }

// Ob'ektlarni birlashtirish
let birlashgan = Object.assign({}, { a: 1 }, { b: 2 }, { c: 3 });
console.log(birlashgan); // { a: 1, b: 2, c: 3 }
```

### `Object.freeze()` — O'zgartirishni bloklash

```javascript
let sozlamalar = Object.freeze({ tema: "qorong'u", til: "uz" });

sozlamalar.tema = "yorug'"; // ❌ xato emas, lekin o'zgartirilmaydi
console.log(sozlamalar.tema); // "qorong'u"

console.log(Object.isFrozen(sozlamalar)); // true
```

### `Object.seal()` — Qo'shish/O'chirishni bloklash

```javascript
let obj = Object.seal({ a: 1, b: 2 });

obj.a = 10;    // ✅ O'zgartirish mumkin
obj.c = 3;     // ❌ Qo'shib bo'lmaydi
delete obj.a;  // ❌ O'chirib bo'lmaydi

console.log(obj); // { a: 10, b: 2 }
```

---

## 📌 Destructuring (Parchalash) — ES6

```javascript
let shaxs = { ism: "Ali", yosh: 25, shahar: "Toshkent" };

// Oddiy usul
let ism = shaxs.ism;
let yosh = shaxs.yosh;

// Destructuring
let { ism: nom, yosh: muddati } = shaxs; // qayta nomlash
console.log(nom);    // "Ali"
console.log(muddati); // 25

// Default qiymat
let { telefon = "+998000000000" } = shaxs;
console.log(telefon); // "+998000000000"

// Funksiyada
function kutib_ol({ ism, yosh = 18 }) {
  return `${ism} (${yosh} yosh)`;
}
console.log(kutib_ol(shaxs)); // "Ali (25 yosh)"
```

---

## 📌 Spread va Rest Operatorlari

```javascript
let obj1 = { a: 1, b: 2 };
let obj2 = { c: 3, d: 4 };

// Spread — ob'ektlarni birlashtirish
let birlashgan = { ...obj1, ...obj2 };
console.log(birlashgan); // { a:1, b:2, c:3, d:4 }

// Xususiyatni o'zgartirish (spread bilan)
let yangi = { ...obj1, b: 999 };
console.log(yangi); // { a: 1, b: 999 }

// Rest — qolgan xususiyatlarni olish
let { a, ...qolgan } = birlashgan;
console.log(a);       // 1
console.log(qolgan);  // { b:2, c:3, d:4 }
```

---

## 📌 `in` operatori va `hasOwnProperty`

```javascript
let shaxs = { ism: "Ali", yosh: 25 };

// Xususiyat mavjudligini tekshirish
console.log("ism" in shaxs);   // true
console.log("email" in shaxs); // false

// hasOwnProperty — faqat o'zining xususiyatlarini tekshiradi
console.log(shaxs.hasOwnProperty("ism"));      // true
console.log(shaxs.hasOwnProperty("toString")); // false (prototipdan meroslanadi)
```

---

## 📌 Optional Chaining `?.` — ES2020

```javascript
let foydalanuvchi = {
  ism: "Ali",
  manzil: {
    shahar: "Toshkent"
  }
};

// ❌ Xavfli usul — xato berishi mumkin
// console.log(foydalanuvchi.ish.nomi); // TypeError!

// ✅ Optional chaining
console.log(foydalanuvchi?.ish?.nomi); // undefined (xato yo'q)
console.log(foydalanuvchi?.manzil?.shahar); // "Toshkent"

// Metod bilan
let admin = null;
console.log(admin?.salom()); // undefined (xato yo'q)
```

---

## 🎯 Amaliy Vazifalar

```javascript
// 1. Talaba ob'ekti yarating (ism, yosh, fanlar massivi, o'rtachaball metodli)
const talaba = {
  ism: "Ali",
  yosh: 20,
  fanlar: { matematika: 90, fizika: 85, informatika: 95 },
  o_rtachaBall() {
    let qiymatlar = Object.values(this.fanlar);
    return qiymatlar.reduce((s, b) => s + b, 0) / qiymatlar.length;
  }
};
console.log(talaba.o_rtachaBall()); // 90

// 2. Ob'ektni massivga aylantirib, qiymatlar bo'yicha saralang
let ballar = { Ali: 85, Vali: 92, Gani: 78, Sani: 95 };
let saralangan = Object.entries(ballar)
  .sort(([, a], [, b]) => b - a)
  .map(([ism, ball]) => `${ism}: ${ball}`);
console.log(saralangan); // ["Sani: 95", "Vali: 92", ...]

// 3. Chuqur ob'ekt birlashtirish funksiyasi
function birlashtir(asl, yangi) {
  return { ...asl, ...yangi };
}

// 4. Maoshni oshiruvchi funksiya (ob'ektni o'zgartirmaydi)
function maoshOshir(xodim, foiz) {
  return { ...xodim, maosh: xodim.maosh * (1 + foiz / 100) };
}

let xodim = { ism: "Bobur", maosh: 5000000 };
let yangiXodim = maoshOshir(xodim, 20);
console.log(xodim.maosh);     // 5000000 — o'zgarmadi
console.log(yangiXodim.maosh); // 6000000

// 5. Ob'ektning necha ta xususiyati borligini aniqlang
function xususiyatSoni(obj) {
  return Object.keys(obj).length;
}
```

---

## ❓ 30 ta Savol-Javob

### Boshlang'ich Savolar

**1. Ob'ektda xususiyatga murojaat qilishning ikki usuli qanday?**
> Nuqta: `obj.ism`, qavslar: `obj["ism"]`. Dinamik kalitlar uchun qavslar kerak.

**2. `delete obj.x` nima qiladi?**
> `x` xususiyatini ob'ektdan o'chiradi.

**3. Ob'ektda mavjud bo'lmagan kalit so'ralsa nima bo'ladi?**
> `undefined` qaytaradi (xato emas).

**4. `Object.keys()` nima qaytaradi?**
> Ob'ektning o'z kalitlari massivi.

**5. Shallow copy (yuzaki nusxa) qanday yaratiladi?**
> `{ ...obj }` yoki `Object.assign({}, obj)`.

**6. `Object.freeze()` nima qiladi?**
> Ob'ektni o'zgartirib bo'lmaydigan holga keltiradi — xususiyat qo'shish, o'chirish, o'zgartirish mumkin emas.

**7. `in` operatori nima qiladi?**
> Ob'ektda (yoki prototip zanjirida) xususiyat borligini tekshiradi.

**8. Ob'ekt metodida `this` nimaga ishora qiladi?**
> O'sha ob'ektning o'ziga.

**9. Property shorthand nima?**
> `{ ism, yosh }` — o'zgaruvchi nomi bilan kalit bir xil bo'lsa qisqa yozuv.

**10. `Object.entries()` nima qaytaradi?**
> `[kalit, qiymat]` juftliklari massivi.

---

### O'rta Savolar

**11. Deep copy (chuqur nusxa) qanday yaratiladi?**
> `JSON.parse(JSON.stringify(obj))` — lekin funksiyalar, `undefined`, `Date` lar yo'qoladi. `structuredClone(obj)` yangi standart.

**12. Optional chaining `?.` qanday ishlaydi?**
> Agar chap tomon `null` yoki `undefined` bo'lsa, `TypeError` o'rniga `undefined` qaytaradi.

**13. `Object.assign()` chuqur nusxa yaratadimiI?**
> Yo'q. Faqat birinchi daraja xususiyatlarni ko'chiradi.

**14. Destructuring da default qiymat qanday beriladi?**
> `let { ism = "Noma'lum" } = obj;`

**15. `hasOwnProperty` va `in` ning farqi nima?**
> `in` prototip zanjiridagi xususiyatlarni ham topadi. `hasOwnProperty` faqat o'z xususiyatlarini tekshiradi.

**16. Ob'ekt xususiyatlari ustida `for...in` qanday ishlaydi?**
> Ob'ektning barcha enumerable xususiyatlarini (prototip bilan birga) aylanib chiqadi.

**17. Computed property nima?**
> `let k = "ism"; let obj = { [k]: "Ali" }` — dinamik kalit.

**18. `Object.seal()` va `Object.freeze()` farqi?**
> `seal` qo'shish va o'chirishni bloklaydi, lekin o'zgartirishga ruxsat beradi. `freeze` hammani bloklaydi.

**19. Spread bilan ikki ob'ektni birlashtirish muammosiI?**
> Bir xil kalit bo'lsa keyingisi oldingisin ustiga yozadi: `{ ...{a:1}, ...{a:2} }` → `{ a: 2 }`.

**20. `Object.fromEntries()` nima qiladi?**
> `entries` massividan ob'ekt yaratadi — `Object.entries()` ning teskarisi.
```javascript
let arr = [["ism","Ali"], ["yosh", 25]];
console.log(Object.fromEntries(arr)); // {ism:"Ali", yosh:25}
```

---

### Murakkab Savolar

**21. Nima uchun `{} === {}` `false` bo'ladi?**
> Ob'ektlar reference bo'yicha taqqoslanadi. Ikki alohida ob'ekt — ikki alohida adres.

**22. Ob'ektni saralash mumkinmi?**
> Ob'ektlar saralanmaydi. Saralash uchun `Object.entries()` ni saralab, `Object.fromEntries()` bilan qayta yaratiladi.

**23. Getter va Setter nima?**
```javascript
let obj = {
  _ism: "Ali",
  get ism() { return this._ism; },
  set ism(qiymat) { this._ism = qiymat.trim(); }
};
obj.ism = "  Vali  ";
console.log(obj.ism); // "Vali"
```

**24. `JSON.stringify` ob'ektda nima qiladi?**
> Ob'ektni JSON matnga aylantiradi. Funksiyalar, `undefined`, `Symbol` lari o'tkazib yuboriladi.

**25. Ob'ektlar orasidagi teng ekanligini qanday tekshiramiz?**
> `JSON.stringify(obj1) === JSON.stringify(obj2)` — lekin tartib farqida ishlamaydi. Yaxshiroq: chuqur taqqoslash funksiyasi.

**26. `Object.create(null)` nima beradi?**
> Prototipsiz toza ob'ekt — `toString`, `hasOwnProperty` metodlari yo'q, sof kalit-qiymat saqlash uchun.

**27. Ob'ektda kalit soni qanday topiladi?**
> `Object.keys(obj).length`.

**28. Prototype chain nima?**
> Har bir ob'ektning prototip ob'ekti bor. Xususiyat topilmasa prototipda qidiriladi — zanjir bo'yicha tepagacha.

**29. Quyidagi kod nima chiqaradi?**
```javascript
let a = { x: 1 };
let b = a;
b.x = 2;
console.log(a.x);
```
> `2`. `b = a` — reference ko'chirildi, ikkisi bir ob'ektga ko'rsatadi.

**30. Ob'ektni `Map` ga aylantirish:**
```javascript
let obj = { a: 1, b: 2 };
let map = new Map(Object.entries(obj));
console.log(map.get("a")); // 1
```
> `Object.entries()` bilan `Map` konstruktoriga beriladi.
