# 20-Dars: Local Storage, Session Storage & Cookies

## 📌 Web Storage Taqqoslash

| Xususiyat     | localStorage   | sessionStorage    | Cookies          |
|---------------|----------------|-------------------|------------------|
| Muddat        | Doimiy         | Tab yopilguncha   | Belgilangan sana |
| O'lcham       | ~5-10 MB       | ~5 MB             | ~4 KB            |
| Server bilimi | ❌             | ❌                | ✅ HTTP bilan    |
| Domenga bog'liq | Ha           | Ha (tab)          | Ha               |

---

## 📌 localStorage

```javascript
// Saqlash
localStorage.setItem("ism", "Ali");
localStorage.setItem("ob'ekt", JSON.stringify({ yosh: 25 }));

// Olish
let ism = localStorage.getItem("ism");           // "Ali"
let ob = JSON.parse(localStorage.getItem("ob'ekt")); // {yosh: 25}

// Mavjud bo'lmasa → null
let yoq = localStorage.getItem("email");         // null

// O'chirish
localStorage.removeItem("ism");
localStorage.clear(); // Hammasini

// Barcha kalitlar
for (let i = 0; i < localStorage.length; i++) {
  let kalit = localStorage.key(i);
  console.log(kalit, localStorage.getItem(kalit));
}
```

---

## 📌 JSON.stringify() va JSON.parse()

```javascript
let foydalanuvchi = {
  ism: "Ali",
  yosh: 25,
  sevimlilar: ["JS", "React"],
  manzil: { shahar: "Toshkent" }
};

// Ob'ektni JSONga aylantirish
let json = JSON.stringify(foydalanuvchi);
console.log(typeof json);  // "string"
console.log(json);
// '{"ism":"Ali","yosh":25,"sevimlilar":["JS","React"],...}'

// JSONni ob'ektga qaytarish
let qayta = JSON.parse(json);
console.log(qayta.ism);    // "Ali"

// Chiroyli format (debug uchun)
console.log(JSON.stringify(foydalanuvchi, null, 2));

// ⚠️ Yo'qoluvchilar:
// undefined, funksiya, Symbol → yo'qoladi
// Date → string ga aylanadi
// RegExp → {} bo'ladi
```

---

## 📌 sessionStorage

```javascript
// localStorage bilan bir xil API, farqi — tab yopilsa o'chadi
sessionStorage.setItem("forma_qiymati", "Ali");
let q = sessionStorage.getItem("forma_qiymati");
sessionStorage.removeItem("forma_qiymati");
sessionStorage.clear();

// ✅ Forma ma'lumotlari (sahifani tasodifan yopib qolsa)
// ✅ Bir martalik sessiya ma'lumotlari
```

---

## 📌 Cookies

```javascript
// O'rnatish
document.cookie = "ism=Ali";
document.cookie = "token=abc; max-age=3600"; // 1 soat
document.cookie = "tema=qorongu; path=/; secure";

// O'qish — barcha cookie lar string sifatida
function cookieOlish(nomi) {
  return document.cookie.split("; ")
    .find(c => c.startsWith(nomi + "="))
    ?.split("=")[1] || null;
}
console.log(cookieOlish("ism")); // "Ali"

// O'chirish — sana o'tganini bering
document.cookie = "ism=; expires=Thu, 01 Jan 1970 00:00:00 GMT";
```

---

## 📌 localStorage CRUD Yordamchi Sinf

```javascript
class LocalStorage {
  static saqlash(kalit, qiymat) {
    localStorage.setItem(kalit, JSON.stringify(qiymat));
  }

  static olish(kalit, sukut = null) {
    let q = localStorage.getItem(kalit);
    if (q === null) return sukut;
    try { return JSON.parse(q); }
    catch { return q; }
  }

  static o_chirish(kalit) { localStorage.removeItem(kalit); }
  static tozalash()        { localStorage.clear(); }
  static barcha()          {
    let ob = {};
    for (let i = 0; i < localStorage.length; i++) {
      let k = localStorage.key(i);
      ob[k] = this.olish(k);
    }
    return ob;
  }
}

// Ishlatish
LocalStorage.saqlash("foydalanuvchi", { ism: "Ali", yosh: 25 });
let f = LocalStorage.olish("foydalanuvchi");
console.log(f.ism); // "Ali"
```

---

## 📌 storage Event

```javascript
// Boshqa tabda localStorage o'zgarganda ishlaydi
window.addEventListener("storage", (e) => {
  console.log("Kalit:", e.key);
  console.log("Yangi qiymat:", e.newValue);
});
```

---

## 🎯 10 ta Amaliy Vazifa

```javascript
// 1. Sahifani yuklash sonini saqlash
let ko_rishlar = parseInt(localStorage.getItem("ko_rishlar") || "0") + 1;
localStorage.setItem("ko_rishlar", ko_rishlar);
console.log(`Bu sahifani ${ko_rishlar}-marta ko'rdingiz`);

// 2. Oxirgi kirish vaqtini saqlash
let oxirgi = localStorage.getItem("oxirgi_kirish");
if (oxirgi) console.log("Oxirgi kirish:", new Date(oxirgi).toLocaleString());
localStorage.setItem("oxirgi_kirish", new Date().toISOString());

// 3. Foydalanuvchi sozlamalarini saqlash/yuklash
function sozlamalarSaqlash(sozlamalar) {
  localStorage.setItem("sozlamalar", JSON.stringify(sozlamalar));
}
function sozlamalarOlish() {
  return JSON.parse(localStorage.getItem("sozlamalar")) || { tema: "yorug", font: 16 };
}
sozlamalarSaqlash({ tema: "qorongu", font: 18 });
console.log(sozlamalarOlish()); // {tema:"qorongu", font:18}

// 4. Savat (Shopping Cart) CRUD
const savat = {
  olish: () => JSON.parse(localStorage.getItem("savat")) || [],
  qo_sh(mahsulot) {
    let s = this.olish();
    let mavjud = s.find(m => m.id === mahsulot.id);
    if (mavjud) mavjud.soni++;
    else s.push({ ...mahsulot, soni: 1 });
    localStorage.setItem("savat", JSON.stringify(s));
  },
  o_chir(id) {
    let s = this.olish().filter(m => m.id !== id);
    localStorage.setItem("savat", JSON.stringify(s));
  },
  tozala() { localStorage.removeItem("savat"); }
};
savat.qo_sh({ id: 1, nomi: "Olma", narx: 5000 });
savat.qo_sh({ id: 1, nomi: "Olma", narx: 5000 }); // soni++ bo'ladi
console.log(savat.olish()); // [{id:1, nomi:"Olma", narx:5000, soni:2}]

// 5. Sevimlilar ro'yxati
const sevimlilar = {
  olish: () => JSON.parse(localStorage.getItem("sevimlilar")) || [],
  toggle(id) {
    let s = this.olish();
    let i = s.indexOf(id);
    if (i === -1) s.push(id);
    else s.splice(i, 1);
    localStorage.setItem("sevimlilar", JSON.stringify(s));
    return i === -1; // true = qo'shildi, false = o'chirildi
  },
  borMi: (id) => JSON.parse(localStorage.getItem("sevimlilar") || "[]").includes(id)
};
console.log(sevimlilar.toggle(42)); // true (qo'shildi)
console.log(sevimlilar.toggle(42)); // false (o'chirildi)

// 6. Auto-save forma
function autosaveBosh() {
  document.querySelectorAll("input, textarea").forEach(el => {
    let kalit = "forma_" + el.id;
    el.value = localStorage.getItem(kalit) || "";
    el.addEventListener("input", () => localStorage.setItem(kalit, el.value));
  });
}

function formaniYuborish() {
  // Forma yuborilganda tozalash
  document.querySelectorAll("input, textarea").forEach(el => {
    localStorage.removeItem("forma_" + el.id);
  });
}

// 7. Izlash tarixi (oxirgi 10 ta)
function izlashQo'sh(so_rov) {
  let tarix = JSON.parse(localStorage.getItem("izlash") || "[]");
  tarix = [so_rov, ...tarix.filter(s => s !== so_rov)].slice(0, 10);
  localStorage.setItem("izlash", JSON.stringify(tarix));
  return tarix;
}
console.log(izlashQo'sh("JavaScript")); // ["JavaScript"]
console.log(izlashQo'sh("React"));      // ["React", "JavaScript"]

// 8. sessionStorage bilan forma backupi
function sessionFormaSaqlash(forma) {
  let ma_lumot = {};
  for (let [k, v] of new FormData(forma)) ma_lumot[k] = v;
  sessionStorage.setItem("forma_backup", JSON.stringify(ma_lumot));
}
function sessionFormaYuklash(forma) {
  let backup = JSON.parse(sessionStorage.getItem("forma_backup") || "null");
  if (!backup) return;
  for (let [kalit, qiymat] of Object.entries(backup)) {
    let el = forma.querySelector(`[name="${kalit}"]`);
    if (el) el.value = qiymat;
  }
}

// 9. JSON stringify bilan filtrlash
let maxfiyMa_lumot = {
  ism: "Ali",
  parol: "secret123",  // Bu saqlanmasin!
  email: "ali@mail.com"
};
let xavfsiz = JSON.stringify(maxfiyMa_lumot, (kalit, qiymat) => {
  if (kalit === "parol") return undefined; // Filtrlash
  return qiymat;
});
console.log(xavfsiz); // {"ism":"Ali","email":"ali@mail.com"}

// 10. LocalStorage holati ko'rsatuvchi funksiya
function storageHolati() {
  let ob = {};
  for (let i = 0; i < localStorage.length; i++) {
    let k = localStorage.key(i);
    try { ob[k] = JSON.parse(localStorage.getItem(k)); }
    catch { ob[k] = localStorage.getItem(k); }
  }
  console.log("=== LocalStorage holati ===");
  console.log(JSON.stringify(ob, null, 2));
  console.log(`Jami: ${localStorage.length} kalit`);
  return ob;
}
storageHolati();
```
