# 21-Dars: Date Objects (Sana va Vaqt)

## 📌 Date ob'ekti nima?

**Date** — JavaScript da sana va vaqt bilan ishlash uchun ishlatiladigan o'rnatilgan ob'ekt.

```javascript
// Joriy vaqt
let hozir = new Date();
console.log(hozir); // Wed Mar 11 2026 12:49:00 GMT+0500

// Muayyan sana
let belgilangan = new Date("2024-12-31");
let belgilangan2 = new Date(2024, 11, 31); // oy 0 dan boshlanadi! (11 = dekabr)
let belgilangan3 = new Date(2024, 11, 31, 23, 59, 59); // soat:daqiqa:soniya

// Timestamp (1970-01-01 dan millisekund)
let timestamp = new Date(0);       // 1970-01-01 00:00:00
let ts2 = new Date(1000);          // 1970-01-01 00:00:01

// Date.now() — joriy timestamp
console.log(Date.now()); // masalan: 1710154740000
```

---

## 📌 Sana Olish Metodlari

```javascript
let sana = new Date();

// Komponentlar olish
console.log(sana.getFullYear());     // Yil (masalan: 2024)
console.log(sana.getMonth());        // Oy (0-11) — 0=Yanvar!
console.log(sana.getDate());         // Kun (1-31)
console.log(sana.getDay());          // Hafta kuni (0-6) — 0=Yakshanba!
console.log(sana.getHours());        // Soat (0-23)
console.log(sana.getMinutes());      // Daqiqa (0-59)
console.log(sana.getSeconds());      // Soniya (0-59)
console.log(sana.getMilliseconds()); // Millisekund (0-999)
console.log(sana.getTime());         // Timestamp (ms)

// UTC versiyalari
console.log(sana.getUTCHours());     // UTC soat
console.log(sana.getTimezoneOffset()); // UTC dan farq (daqiqada)
```

---

## 📌 Sana O'rnatish Metodlari

```javascript
let sana = new Date();

sana.setFullYear(2025);
sana.setMonth(11);        // Dekabr (0-based)
sana.setDate(31);
sana.setHours(23);
sana.setMinutes(59);
sana.setSeconds(59);

// Bir vaqtda bir nechta
sana.setFullYear(2025, 0, 1); // 2025 yil 1 yanvar
```

---

## 📌 Sana Formatlash

```javascript
let sana = new Date(2024, 2, 15, 14, 30, 0); // 15 mart 2024, 14:30

// O'rnatilgan metodlar
console.log(sana.toString());          // "Fri Mar 15 2024 14:30:00..."
console.log(sana.toISOString());       // "2024-03-15T09:30:00.000Z"
console.log(sana.toLocaleDateString()); // "3/15/2024" (local)
console.log(sana.toLocaleTimeString()); // "2:30:00 PM" (local)
console.log(sana.toLocaleString());     // "3/15/2024, 2:30:00 PM"

// O'zbek tilida formatlash
console.log(sana.toLocaleDateString("uz-UZ"));
// "15.03.2024"

// Intl.DateTimeFormat — kuchli formatlash
let formatlash = new Intl.DateTimeFormat("uz-UZ", {
  year: "numeric",
  month: "long",
  day: "numeric",
  weekday: "long"
});
console.log(formatlash.format(sana)); // "15 mart 2024, juma"

// O'zim yozgan format funksiyasi
function sananiFormatlash(sana) {
  let k = sana.getDate().toString().padStart(2, "0");
  let o = (sana.getMonth() + 1).toString().padStart(2, "0");
  let y = sana.getFullYear();
  return `${k}.${o}.${y}`;
}
console.log(sananiFormatlash(new Date())); // "11.03.2026"
```

---

## 📌 Sana Hisoblash

```javascript
let bugun = new Date();

// Kelajakdagi sana
let ertaga = new Date(bugun);
ertaga.setDate(ertaga.getDate() + 1);

let bir_hafta_keyin = new Date(bugun);
bir_hafta_keyin.setDate(bir_hafta_keyin.getDate() + 7);

let bir_oy_keyin = new Date(bugun);
bir_oy_keyin.setMonth(bir_oy_keyin.getMonth() + 1);

// Ikki sana orasidagi farq
let tug_ilgan = new Date(2000, 0, 15); // 2000 yil 15 yanvar
let hozir = new Date();
let farq_ms = hozir - tug_ilgan;       // Millisekund
let farq_kun = Math.floor(farq_ms / (1000 * 60 * 60 * 24));
let yosh = Math.floor(farq_ms / (1000 * 60 * 60 * 24 * 365.25));
console.log(`${yosh} yosh, ${farq_kun} kun`);

// Vaqt o'tishini o'lchash
let boshlanish = Date.now();
// ... og'ir hisoblash ...
let tugash = Date.now();
console.log(`${tugash - boshlanish} ms ketdi`);
```

---

## 📌 `setTimeout()` — Kechiktirilgan Bajarish

```javascript
// Sintaksis: setTimeout(funksiya, kechikish_ms, ...argumentlar)

// Bir marta bajarish
let taymer1 = setTimeout(() => {
  console.log("3 soniyadan keyin!");
}, 3000);

// Argument bilan
setTimeout((ism) => {
  console.log(`Salom, ${ism}!`);
}, 1000, "Ali");

// clearTimeout — bekor qilish
let taymer2 = setTimeout(() => console.log("Bu hech qachon chiqmaydi"), 5000);
clearTimeout(taymer2);

// Zanjirli timeout (rekursiv)
function takrorla(n) {
  if (n <= 0) return;
  console.log(n);
  setTimeout(() => takrorla(n - 1), 1000);
}
takrorla(5); // 5, 4, 3, 2, 1 (har soniyada)
```

---

## 📌 `setInterval()` — Takroriy Bajarish

```javascript
// Sintaksis: setInterval(funksiya, interval_ms, ...argumentlar)

let i = 0;
let interval = setInterval(() => {
  i++;
  console.log(`Soniya: ${i}`);
  if (i >= 5) {
    clearInterval(interval); // To'xtatish!
    console.log("Tugadi!");
  }
}, 1000);

// clearInterval — to'xtatish
let interval2 = setInterval(() => console.log("Ishlayapti"), 500);
setTimeout(() => clearInterval(interval2), 3000); // 3 soniyadan keyin to'xtat
```

---

## 📌 Taymerlarni Tozalash

```javascript
// Barcha taymerlar ID qaytaradi
let timeoutId = setTimeout(() => {}, 1000);
let intervalId = setInterval(() => {}, 500);

// Bekor qilish
clearTimeout(timeoutId);
clearInterval(intervalId);

// Bir nechta intervalni boshqarish
class TaymerBoshqaruvi {
  constructor() {
    this.taymerlar = new Set();
  }

  setTimeout(fn, ms) {
    let id = setTimeout(() => {
      this.taymerlar.delete(id);
      fn();
    }, ms);
    this.taymerlar.add(id);
    return id;
  }

  setInterval(fn, ms) {
    let id = setInterval(fn, ms);
    this.taymerlar.add(id);
    return id;
  }

  hammaniTozala() {
    this.taymerlar.forEach(id => {
      clearTimeout(id);
      clearInterval(id);
    });
    this.taymerlar.clear();
  }
}
```

---

## 🎯 10 ta Amaliy Vazifa

```javascript
// 1. Bugungi sanani "DD.MM.YYYY" formatda chiqaring
function bugungiSana() {
  let d = new Date();
  let k = String(d.getDate()).padStart(2, "0");
  let o = String(d.getMonth() + 1).padStart(2, "0");
  return `${k}.${o}.${d.getFullYear()}`;
}
console.log(bugungiSana()); // "11.03.2026"

// 2. Yosh hisoblash
function yoshHisoblash(tug_ilganSana) {
  let tug = new Date(tug_ilganSana);
  let hozir = new Date();
  let yosh = hozir.getFullYear() - tug.getFullYear();
  let oyFarq = hozir.getMonth() - tug.getMonth();
  if (oyFarq < 0 || (oyFarq === 0 && hozir.getDate() < tug.getDate())) yosh--;
  return yosh;
}
console.log(yoshHisoblash("2000-05-15")); // ~25

// 3. Haftaning nomini aniqlang
function haftaKunNomi(sana) {
  const kunlar = ["Yakshanba","Dushanba","Seshanba","Chorshanba","Payshanba","Juma","Shanba"];
  return kunlar[new Date(sana).getDay()];
}
console.log(haftaKunNomi("2024-03-15")); // "Juma"

// 4. Ikki sana orasidagi kunlarni hisoblang
function kunlarFarqi(sana1, sana2) {
  let farq = Math.abs(new Date(sana2) - new Date(sana1));
  return Math.floor(farq / (1000 * 60 * 60 * 24));
}
console.log(kunlarFarqi("2024-01-01", "2024-12-31")); // 365

// 5. Sananing formatlash funksiyasi
function sananiFormat(sana, format) {
  let d = new Date(sana);
  let qiymatlar = {
    DD: String(d.getDate()).padStart(2, "0"),
    MM: String(d.getMonth() + 1).padStart(2, "0"),
    YYYY: d.getFullYear(),
    HH: String(d.getHours()).padStart(2, "0"),
    mm: String(d.getMinutes()).padStart(2, "0"),
    ss: String(d.getSeconds()).padStart(2, "0")
  };
  return format.replace(/DD|MM|YYYY|HH|mm|ss/g, m => qiymatlar[m]);
}
console.log(sananiFormat(new Date(), "DD.MM.YYYY HH:mm")); // "11.03.2026 12:49"

// 6. Countdown taymer (konsol)
function countdown(soniyalar) {
  let qolgan = soniyalar;
  let interval = setInterval(() => {
    let d = Math.floor(qolgan / 86400);
    let s = Math.floor((qolgan % 86400) / 3600);
    let dq = Math.floor((qolgan % 3600) / 60);
    let sn = qolgan % 60;
    console.log(`${d}k ${s}s ${dq}d ${sn}sn`);
    if (qolgan-- <= 0) { clearInterval(interval); console.log("Taymer tugadi!"); }
  }, 1000);
  return interval;
}

// 7. Debounce funksiyasi (setTimeout bilan)
function debounce(fn, kechikish) {
  let taymer;
  return function(...args) {
    clearTimeout(taymer);
    taymer = setTimeout(() => fn.apply(this, args), kechikish);
  };
}

const qidirish = debounce((matn) => {
  console.log("Qidirildi:", matn);
}, 500);

// 8. Throttle funksiyasi (setTimeout bilan)
function throttle(fn, interval) {
  let oxirgiVaqt = 0;
  return function(...args) {
    let hozir = Date.now();
    if (hozir - oxirgiVaqt >= interval) {
      fn.apply(this, args);
      oxirgiVaqt = hozir;
    }
  };
}

// 9. Ishlash vaqtini o'lchash dekorator
function vaqtO_lchash(fn) {
  return function(...args) {
    let boshlanish = Date.now();
    let natija = fn.apply(this, args);
    console.log(`${fn.name}: ${Date.now() - boshlanish}ms`);
    return natija;
  };
}

let o_lchanganYig_indi = vaqtO_lchash(function yig_indi(n) {
  let s = 0;
  for (let i = 0; i <= n; i++) s += i;
  return s;
});
o_lchanganYig_indi(1000000); // "yig_indi: ?ms"

// 10. Sodda vaqt jadval rejasi
class VaqtJadvali {
  constructor() { this.vazifalar = []; }

  qo_sh(vaqt, fn) {
    let [soat, daqiqa] = vaqt.split(":").map(Number);
    this.vazifalar.push({ soat, daqiqa, fn });
  }

  boshlash() {
    setInterval(() => {
      let hozir = new Date();
      this.vazifalar.forEach(v => {
        if (hozir.getHours() === v.soat && hozir.getMinutes() === v.daqiqa) {
          v.fn();
        }
      });
    }, 60000); // Har daqiqada tekshirish
  }
}

let jadval = new VaqtJadvali();
jadval.qo_sh("09:00", () => console.log("Ish boshlandi!"));
jadval.qo_sh("13:00", () => console.log("Tushlik vaqti!"));
jadval.qo_sh("18:00", () => console.log("Ish tugadi!"));
// jadval.boshlash();
```
