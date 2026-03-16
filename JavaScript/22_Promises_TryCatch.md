# 22-Dars: Promises va Try-Catch

## 📌 Promise nima?

**Promise** — asinxron operatsiyaning kelajakdagi natijasini ifodalovchi ob'ekt. Hozir mavjud bo'lmagan, lekin keyinroq mavjud bo'ladigan qiymatni boshqaradi.

```
Promise holatlari:
├── pending   — kutilmoqda (boshlang'ich holat)
├── fulfilled — muvaffaqiyatli (resolve() chaqirildi)
└── rejected  — rad etildi (reject() chaqirildi)
```

---

## 📌 Promise Yaratish

```javascript
// Sintaksis
let promise = new Promise((resolve, reject) => {
  // Asinxron amal (server so'rovi, timeout, va h.k.)
  
  // Muvaffaqiyatli:
  // resolve(qiymat);
  
  // Xatolik:
  // reject(xato);
});

// Oddiy misol
let yarim_soniyaKeyin = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("Tayyor!"); // 500ms keyin ishga tushadi
  }, 500);
});

// Xatolik misoli
let xatoliPromise = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject(new Error("Nimadir noto'g'ri ketdi"));
  }, 1000);
});
```

---

## 📌 `.then()`, `.catch()`, `.finally()`

```javascript
let promise = new Promise((resolve, reject) => {
  setTimeout(() => resolve("Ma'lumot keldi!"), 1000);
});

// .then() — muvaffaqiyatli natijani qayta ishlash
promise.then(natija => {
  console.log("Muvaffaqiyat:", natija); // "Ma'lumot keldi!"
});

// Zanjirli ishlatish
let sonPromise = new Promise((resolve) => resolve(5));

sonPromise
  .then(n => n * 2)        // 10
  .then(n => n + 3)        // 13
  .then(n => console.log(n)); // 13

// .catch() — xatolikni qayta ishlash
let xatoliPromise = new Promise((resolve, reject) => {
  setTimeout(() => reject(new Error("Server xatosi!")), 500);
});

xatoliPromise
  .then(natija => console.log("Bu chiqmaydi"))
  .catch(xato => console.log("Xato:", xato.message));

// .finally() — har doim ishlaydi (muvaffaqiyat yoki xato)
yarim_soniyaKeyin
  .then(n => console.log(n))
  .catch(e => console.log(e))
  .finally(() => console.log("Yuklanish tugadi (spinner yashirish)"));
```

---

## 📌 Promise.all() — Hammasi tayyor bo'lguncha

```javascript
// Barcha promise lar tugashi uchun kutadi
let p1 = new Promise(resolve => setTimeout(() => resolve("A"), 1000));
let p2 = new Promise(resolve => setTimeout(() => resolve("B"), 500));
let p3 = new Promise(resolve => setTimeout(() => resolve("C"), 800));

Promise.all([p1, p2, p3])
  .then(natijalar => {
    console.log(natijalar); // ["A", "B", "C"] (tartib saqlanadi!)
  });

// Bittasi rejected bo'lsa — hammasi rejected!
let p4 = new Promise((_, reject) => setTimeout(() => reject("Xato!"), 600));
Promise.all([p1, p4, p3])
  .catch(xato => console.log("Biri xato:", xato)); // "Xato!"
```

---

## 📌 Promise.allSettled() — Barchasi tugaguncha

```javascript
// Xatolikda ham davom etadi, hamma natijani beradi
Promise.allSettled([p1, p4, p3])
  .then(natijalar => {
    natijalar.forEach(n => {
      if (n.status === "fulfilled") console.log("OK:", n.value);
      else console.log("Xato:", n.reason);
    });
  });
```

---

## 📌 Promise.race() — Birinchisi tayyor bo'lganda

```javascript
// Birinchi tugagan promise natijasini qaytaradi
Promise.race([p1, p2, p3])
  .then(birinchi => console.log("Birinchi:", birinchi)); // "B" (500ms)
```

---

## 📌 Promise.any() — Birinchi muvaffaqiyatli

```javascript
// Birinchi fulfilled promise ni qaytaradi (rejected larni o'tkazib ketadi)
let xatolik1 = Promise.reject("Xato 1");
let xatolik2 = Promise.reject("Xato 2");
let muvaffaq = Promise.resolve("Muvaffaqiyat!");

Promise.any([xatolik1, xatolik2, muvaffaq])
  .then(n => console.log(n)); // "Muvaffaqiyat!"
```

---

## 📌 Try-Catch — Xatolarni Qayta Ishlash

```javascript
// Sinxron kod uchun
try {
  let son = JSON.parse("noto'g'ri JSON"); // Xato!
  console.log(son); // Bu chiqmaydi
} catch (xato) {
  console.log("Xato turi:", xato.name);    // "SyntaxError"
  console.log("Xabar:", xato.message);    // "..."
} finally {
  console.log("Har doim ishlaydi");
}

// Xato tashlash
function yoshTekshirish(yosh) {
  if (yosh < 0) throw new Error("Yosh manfiy bo'lishi mumkin emas!");
  if (yosh > 150) throw new RangeError("Juda katta yosh!");
  return true;
}

try {
  yoshTekshirish(-5);
} catch (e) {
  if (e instanceof RangeError) {
    console.log("Diapazon xatosi:", e.message);
  } else {
    console.log("Xato:", e.message);
  }
}
```

---

## 📌 Xato Turlari

```javascript
// JavaScript xato turlari
try { null.property }       catch(e) { console.log(e instanceof TypeError);    } // true
try { undeclaredVar }       catch(e) { console.log(e instanceof ReferenceError); } // true
try { eval("{") }           catch(e) { console.log(e instanceof SyntaxError);  } // true
try { null[-1/0] }          catch(e) { console.log(e instanceof RangeError);   }

// O'zining xato sinfi
class ValidationError extends Error {
  constructor(xabar, maydon) {
    super(xabar);
    this.name = "ValidationError";
    this.maydon = maydon;
  }
}

try {
  throw new ValidationError("Email noto'g'ri", "email");
} catch (e) {
  if (e instanceof ValidationError) {
    console.log(`${e.maydon} da xato: ${e.message}`);
  }
}
```

---

## 🎯 10 ta Amaliy Vazifa

```javascript
// 1. 1-2 soniyadan keyin random natija beradigan Promise
function tasodifiyPromise() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      if (Math.random() > 0.5) resolve("Muvaffaqiyat!");
      else reject(new Error("Omad kulib boqmadi!"));
    }, Math.random() * 2000);
  });
}
tasodifiyPromise()
  .then(n => console.log("✅", n))
  .catch(e => console.log("❌", e.message));

// 2. Promise zanjiri — son transformatsiyasi
new Promise(resolve => resolve(1))
  .then(n => n + 1)
  .then(n => n * 2)
  .then(n => n ** 2)
  .then(n => console.log("Natija:", n)); // 16

// 3. Promise.all bilan parallel so'rovlar simulyatsiyasi
function serverSo_rovi(id, kechikish) {
  return new Promise(resolve =>
    setTimeout(() => resolve(`User #${id}`), kechikish)
  );
}
Promise.all([
  serverSo_rovi(1, 1000),
  serverSo_rovi(2, 500),
  serverSo_rovi(3, 800)
]).then(foydalanuvchilar => console.log(foydalanuvchilar));

// 4. Promisify — callback funksiyasini Promise ga aylantirish
function promisify(fn) {
  return function(...args) {
    return new Promise((resolve, reject) => {
      fn(...args, (xato, natija) => {
        if (xato) reject(xato);
        else resolve(natija);
      });
    });
  };
}

// 5. Try-Catch bilan JSON validatsiya
function xavfsizParse(json) {
  try {
    return { muvaffaqiyat: true, ma_lumot: JSON.parse(json) };
  } catch (e) {
    return { muvaffaqiyat: false, xato: e.message };
  }
}
console.log(xavfsizParse('{"ism":"Ali"}')); // {muvaffaqiyat:true, ...}
console.log(xavfsizParse("noto'g'ri"));     // {muvaffaqiyat:false, ...}

// 6. Retry mexanizmi — n marta urinish
function retryPromise(fn, urinishlar) {
  return fn().catch(xato => {
    if (urinishlar <= 1) return Promise.reject(xato);
    console.log(`Qayta urinilmoqda... (${urinishlar - 1} ta qoldi)`);
    return retryPromise(fn, urinishlar - 1);
  });
}
let urinishSoni = 0;
retryPromise(() => {
  urinishSoni++;
  if (urinishSoni < 3) return Promise.reject(new Error("Vaqtinchalik xato"));
  return Promise.resolve("Muvaffaqiyat!");
}, 5).then(n => console.log(n));

// 7. Timeout bilan Promise
function timeoutBilan(promise, ms) {
  let taymer = new Promise((_, reject) =>
    setTimeout(() => reject(new Error(`Timeout: ${ms}ms`)), ms)
  );
  return Promise.race([promise, taymer]);
}
timeoutBilan(serverSo_rovi(1, 2000), 1000)
  .catch(e => console.log(e.message)); // "Timeout: 1000ms"

// 8. O'zining ValidationError sinfi
class ValidationError extends Error {
  constructor(xabar, maydon) {
    super(xabar);
    this.name = "ValidationError";
    this.maydon = maydon;
  }
}
function formaValidatsiya({ ism, yosh, email }) {
  if (!ism || ism.length < 2) throw new ValidationError("Ism juda qisqa", "ism");
  if (!yosh || yosh < 0 || yosh > 120) throw new ValidationError("Yosh noto'g'ri", "yosh");
  if (!email?.includes("@")) throw new ValidationError("Email noto'g'ri", "email");
  return true;
}
try {
  formaValidatsiya({ ism: "A", yosh: 25, email: "test@mail.com" });
} catch (e) {
  if (e instanceof ValidationError) {
    console.log(`${e.maydon}: ${e.message}`);
  }
}

// 9. Promise.allSettled bilan barcha natijalar
let so_rovlar = [1, 2, 3, 4, 5].map(id =>
  new Promise((resolve, reject) =>
    setTimeout(() => id % 2 === 0 ? reject(`#${id} xato`) : resolve(`#${id} ok`), 500)
  )
);
Promise.allSettled(so_rovlar).then(natijalar => {
  let muvaffaqlar = natijalar.filter(n => n.status === "fulfilled").map(n => n.value);
  let xatolar = natijalar.filter(n => n.status === "rejected").map(n => n.reason);
  console.log("OK:", muvaffaqlar);
  console.log("Xato:", xatolar);
});

// 10. Keshlanadigan Promise
function keshliSo_rov(kesh = new Map()) {
  return function(url) {
    if (kesh.has(url)) {
      console.log("Keshdan:", url);
      return Promise.resolve(kesh.get(url));
    }
    return fetch(url)
      .then(r => r.json())
      .then(ma_lumot => {
        kesh.set(url, ma_lumot);
        return ma_lumot;
      });
  };
}
```
