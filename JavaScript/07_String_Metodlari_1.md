# 7-Dars: String Metodlari — 1-qism

## 📌 String nima?

**String** — matn (belgilar ketma-ketligi) saqlash uchun ishlatiladigan ma'lumot turi.

```javascript
let matn1 = "Qo'sh tirnoq";
let matn2 = 'Yagona tirnoq';
let matn3 = `Template literal: ${1 + 2}`; // "Template literal: 3"

// String indekslar (0 dan boshlanadi)
let s = "Salom";
//      S a l o m
//      0 1 2 3 4
console.log(s[0]);  // "S"
console.log(s[4]);  // "m"
```

---

## 📌 `.length` — Uzunlik

```javascript
let matn = "JavaScript";

console.log(matn.length); // 10

// Bo'sh string
console.log("".length); // 0

// Bo'sh joy ham hisoblanadi
console.log("Ali Vali".length); // 8

// Amaliy ishlatish
function validatsiya(ism) {
  if (ism.length < 2) {
    return "Ism juda qisqa!";
  }
  return "To'g'ri";
}
```

---

## 📌 `.charAt(indeks)` — Belgini olish

```javascript
let s = "Salom";

console.log(s.charAt(0));  // "S"
console.log(s.charAt(4));  // "m"
console.log(s.charAt(10)); // "" — indeks yo'q bo'lsa bo'sh qaytaradi

// s[indeks] bilan farqi:
console.log(s[10]);        // undefined (charAt → "")
```

---

## 📌 `.charCodeAt(indeks)` — Unicode kod

```javascript
let s = "Salom";

console.log(s.charCodeAt(0)); // 83  (S ning Unicode kodi)
console.log(s.charCodeAt(1)); // 97  (a)
console.log("A".charCodeAt(0)); // 65
console.log("a".charCodeAt(0)); // 97
console.log("0".charCodeAt(0)); // 48

// Kichik/katta harf tekshirish
function kattaHarfMi(harf) {
  let kod = harf.charCodeAt(0);
  return kod >= 65 && kod <= 90;
}
console.log(kattaHarfMi("A")); // true
console.log(kattaHarfMi("a")); // false
```

---

## 📌 `.at(indeks)` — Zamonaviy belgini olish (ES2022)

```javascript
let s = "Salom";

console.log(s.at(0));   // "S"   — boshidan
console.log(s.at(-1));  // "m"   — oxiridan ✅ (manfiy indeks!)
console.log(s.at(-2));  // "o"

// Massivda ham ishlaydi
let arr = [1, 2, 3];
console.log(arr.at(-1)); // 3
```

---

## 📌 `.concat()` — Birlashtirish

```javascript
let ism = "Ali";
let familiya = "Vali";

console.log(ism.concat(" ", familiya)); // "Ali Vali"
console.log(ism.concat("!"));           // "Ali!"

// + operatori bilan bir xil
console.log(ism + " " + familiya); // "Ali Vali"

// Template literal ko'proq ishlatiladi
console.log(`${ism} ${familiya}`); // "Ali Vali" ✅
```

---

## 📌 `.includes(qidiruv, pozitsiya?)` — Mavjudligini tekshirish

```javascript
let jumla = "JavaScript juda qiziqarli!";

console.log(jumla.includes("JavaScript")); // true
console.log(jumla.includes("Python"));    // false
console.log(jumla.includes("juda"));      // true
console.log(jumla.includes("JUDA"));      // false (katta-kichik harfga sezgir!)

// Pozitsiyadan boshlab qidirish
console.log(jumla.includes("Java", 5));   // false (5-indeksdan qidiradi)

// Amaliy: email tekshirish
function emailMi(email) {
  return email.includes("@") && email.includes(".");
}
console.log(emailMi("user@email.com")); // true
console.log(emailMi("useremail.com"));  // false
```

---

## 📌 `.endsWith(suffix, uzunlik?)` — Oxirini tekshirish

```javascript
let fayl = "hujjat.pdf";

console.log(fayl.endsWith(".pdf")); // true
console.log(fayl.endsWith(".doc")); // false
console.log(fayl.endsWith("at", 6)); // true (faqat 6 ta belgi tekshiriladi)

// Amaliy: fayl turini aniqlash
function pdfMi(nomi) {
  return nomi.endsWith(".pdf");
}
console.log(pdfMi("hisobot.pdf")); // true
console.log(pdfMi("rasm.jpg"));    // false
```

---

## 📌 `.startsWith(prefix, pozitsiya?)` — Boshini tekshirish

```javascript
let url = "https://www.google.com";

console.log(url.startsWith("https")); // true
console.log(url.startsWith("http")); // true
console.log(url.startsWith("ftp"));  // false

// Pozitsiyadan boshlab
console.log(url.startsWith("www", 8)); // true

// Amaliy: URL xavfsizligini tekshirish
function xavfsizMi(url) {
  return url.startsWith("https://");
}
console.log(xavfsizMi("https://bank.com")); // true
console.log(xavfsizMi("http://bank.com"));  // false
```

---

## 📌 `.indexOf(qidiruv, boshlanish?)` — Birinchi pozitsiyani topish

```javascript
let s = "JavaScript juda yaxshi, JavaScript ajoyib!";

console.log(s.indexOf("JavaScript")); // 0  (birinchi topilgan joy)
console.log(s.indexOf("juda"));       // 11
console.log(s.indexOf("Python"));     // -1 (topilmadi)

// Qidiruvni ma'lum pozitsiyadan boshlash
console.log(s.indexOf("JavaScript", 5)); // 23 (5-indeksdan qidiradi)

// Amaliy: barcha pozitsiyalarni topish
function hammaPozitsiya(matn, qidiruv) {
  let pozitsiyalar = [];
  let indeks = 0;
  
  while ((indeks = matn.indexOf(qidiruv, indeks)) !== -1) {
    pozitsiyalar.push(indeks);
    indeks++;
  }
  return pozitsiyalar;
}

console.log(hammaPozitsiya("banana", "a")); // [1, 3, 5]
```

---

## 📌 `.search(regex)` — Regex bilan qidirish

```javascript
let s = "Mening telefon raqamim: +998901234567";

console.log(s.search("telefon"));     // 7  (birinchi pozitsiya)
console.log(s.search(/\d+/));         // 24 (birinchi raqam pozitsiyasi)
console.log(s.search(/Python/));      // -1 (topilmadi)

// indexOf vs search farqi:
// indexOf → oddiy string qidiradi
// search  → regex qidiradi (kuchli, lekin sekinroq)

// Katta-kichik harfni e'tiborsiz qidirish
let jumla = "JavaScript juda YAXSHI!";
console.log(jumla.search(/yaxshi/i)); // 15 (i = case insensitive)
```

---

## 🎯 Amaliy Vazifalar

```javascript
// 1. Berilgan so'zning palindrom ekanligini tekshiring
// (oldinga va orqaga o'qilganda bir xil: "mom", "level")
function palindromMi(so_z) {
  // .split('') .reverse() .join('') ishlating
}

// 2. Email validatsiya funksiyasi
function emailValidatsiya(email) {
  // @ belgisi va nuqta bo'lishi kerak
  // @ belgisi boshida va oxirida bo'lmasligi kerak
}

// 3. Jumlaning so'z sonini hisoblang
function so_zSoni(jumla) {
  // "Salom men Ali" → 3
}

// 4. Matnning birinchi va oxirgi belgisini toping
function birinchiVaOxirgi(matn) {
  return {
    birinchi: matn.at(0),
    oxirgi: matn.at(-1)
  };
}

// 5. Berilgan belgining matnda necha marta uchraganini toping
function nechaMarta(matn, belgi) {
  let hisob = 0;
  // indexOf ishlatib hisoblang
  return hisob;
}
console.log(nechaMarta("mississippi", "s")); // 4
```

---

## ❓ 30 ta Savol-Javob

### Boshlang'ich Savolar

**1. String uzunligini qanday topamiz?**
> `.length` xususiyati: `"Salom".length → 5`

**2. Stringning ma'lum bir indeksidagi belgini qanday olamiz?**
> `.charAt(i)` yoki `str[i]` — lekin `charAt` yo'q indeks uchun `""`, `str[i]` esa `undefined` qaytaradi.

**3. `.at()` metodi `.charAt()` dan qanday farq qiladi?**
> `.at()` manfiy indekslarni qo'llaydi (`at(-1)` = oxirgi belgi). `charAt` manfiy indeks uchun `""` qaytaradi.

**4. `.includes()` nima qaytaradi?**
> `true` yoki `false` — string berilgan qatorni o'z ichiga oladimi yoki yo'qmi.

**5. `.startsWith()` qachon ishlatiladi?**
> String ma'lum bir prefiks bilan boshlananiga tekshirish uchun: URL, fayl nomi va h.k.

**6. `.endsWith()` qachon ishlatiladi?**
> String ma'lum bir suffiks bilan tugashini tekshirish uchun: fayl kengaytmasi, va h.k.

**7. `.indexOf()` topilmasa nima qaytaradi?**
> `-1` qaytaradi.

**8. `.concat()` ning amaliy alternativasi nima?**
> `+` operatori yoki template literal (`` ` `` `` ` ``) — bular ko'proq ishlatiladi.

**9. `.charCodeAt()` nima uchun ishlatiladi?**
> Belgining Unicode (UTF-16) kodini olish uchun.

**10. `.search()` va `.indexOf()` ning farqi nima?**
> `indexOf` oddiy string qidiradi. `search` regex qo'llab-quvvatlaydi va kuchiroq, lekin sekinroq.

---

### O'rta Savolar

**11. `.includes()` katta-kichik harfga sezgirmi?**
> Ha. `"Salom".includes("salom")` → `false`. Oldin `.toLowerCase()` qo'llang.

**12. `.indexOf()` bilan barcha har uchraydigan joyni qanday topamiz?**
> Loop ichida `indexOf(qidiruv, i+1)` qilib davom eting.

**13. `.startsWith()` ning ikkinchi parametri nimaga kerak?**
> Pozitsiya — qaysi indeksdan boshlab tekshirish. `"abcde".startsWith("cd", 2)` → `true`.

**14. `.charCodeAt()` bilan harf katta yoki kichik ekanligini qanday aniqlash mumkin?**
> A-Z: 65-90, a-z: 97-122 oraliqda bo'lsa.

**15. Template literal va `.concat()` qaysi biri afzal?**
> Template literal ko'proq tavsiya etiladi — o'qish va yozish oson.

**16. `.charAt()` orqali butun stringni qanday aylanib chiqamiz?**
```javascript
for (let i = 0; i < str.length; i++) {
  console.log(str.charAt(i));
}
```

**17. Palindrom tekshirishda qaysi metodlar ishlatiladr?**
> `split('')`, `reverse()`, `join('')` yoki `charAt` bilan ikki tomondan solishtirish.

**18. `.search()` regex topilmasa nima qaytaradi?**
> `-1` qaytaradi.

**19. String indekslari qaysi raqamdan boshlanadi?**
> `0` dan boshlanadi. Oxirgi belgi `str.length - 1` indeksida.

**20. `.at(-1)` bilan `.charAt(str.length-1)` bir xilmi?**
> Ha, ikkisi ham oxirgi belgini qaytaradi. Lekin `.at(-1)` qisqaroq yoziladi.

---


