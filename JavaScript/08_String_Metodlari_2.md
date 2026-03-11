# 8-Dars: String Metodlari — 2-qism

## 📌 `.lastIndexOf(qidiruv, boshlanish?)` — Oxirgi pozitsiya

```javascript
let s = "JavaScript juda yaxshi, JavaScript!";

console.log(s.lastIndexOf("JavaScript")); // 24 (oxirgi marta)
console.log(s.lastIndexOf("a"));          // 32
console.log(s.lastIndexOf("Python"));     // -1

// Orqadan ma'lum pozitsiyagacha qidirish
console.log(s.lastIndexOf("JavaScript", 10)); // 0 (10-indeksgacha orqadan)

// Amaliy: fayl kengaytmasini topish
function kengaytma(fayl) {
  let nuqta = fayl.lastIndexOf(".");
  return nuqta === -1 ? "" : fayl.slice(nuqta + 1);
}
console.log(kengaytma("hujjat.pdf"));         // "pdf"
console.log(kengaytma("rasm.2024.jpg"));      // "jpg"
console.log(kengaytma("fayl"));               // ""
```

---

## 📌 `.padStart(uzunlik, to'ldiruvchi?)` — Boshiga to'ldirish

```javascript
// To'ldiruvchi ko'rsatilmasa bo'sh joy ishlatiladi
console.log("5".padStart(3));         // "  5"
console.log("5".padStart(3, "0"));    // "005"
console.log("42".padStart(5, "0"));   // "00042"
console.log("salom".padStart(8, ".")); // "...salom"

// Amaliy: soat formati (HH:MM:SS)
function soatFormati(soat, daqiqa, soniya) {
  return [soat, daqiqa, soniya]
    .map(v => String(v).padStart(2, "0"))
    .join(":");
}
console.log(soatFormati(9, 5, 3)); // "09:05:03"

// Kredit karta raqamini yashirish
function karta(raqam) {
  return String(raqam).slice(-4).padStart(16, "*");
}
console.log(karta("1234567890123456")); // "************3456"
```

---

## 📌 `.padEnd(uzunlik, to'ldiruvchi?)` — Oxiriga to'ldirish

```javascript
console.log("5".padEnd(3, "0"));     // "500"
console.log("Ali".padEnd(10));       // "Ali       "
console.log("Ali".padEnd(10, "."));  // "Ali......."

// Amaliy: chiroyli jadval
function jadval(nomi, narxi) {
  return `${nomi.padEnd(20, ".")}${narxi}`;
}
console.log(jadval("Olma", "5000 so'm"));   // "Olma................5000 so'm"
console.log(jadval("Pomidor", "3000 so'm")); // "Pomidor.............3000 so'm"
```

---

## 📌 `.repeat(son)` — Takrorlash

```javascript
console.log("*".repeat(5));      // "*****"
console.log("ab".repeat(3));     // "ababab"
console.log("-".repeat(20));     // "--------------------"

// Amaliy: progressbar
function progressBar(foiz) {
  let to_la = Math.round(foiz / 10);
  return "[" + "█".repeat(to_la) + "░".repeat(10 - to_la) + "] " + foiz + "%";
}
console.log(progressBar(70)); // "[███████░░░] 70%"

// Yulduzchalar patterni
for (let i = 1; i <= 5; i++) {
  console.log("*".repeat(i));
}
```

---

## 📌 `.replace(eski, yangi)` — Birinchi almashtirish

```javascript
let s = "Men JavaScript sevaman. JavaScript ajoyib!";

// Birinchi uchraganini almashtiradi
console.log(s.replace("JavaScript", "Python"));
// "Men Python sevaman. JavaScript ajoyib!" — faqat birinchisi!

// Regex bilan
console.log(s.replace(/JavaScript/, "Go"));
// "Men Go sevaman. JavaScript ajoyib!"

// Katta-kichik harfni e'tiborsiz
console.log(s.replace(/javascript/i, "TypeScript"));
// "Men TypeScript sevaman. JavaScript ajoyib!"

// Funksiya bilan almashtirish
let natija = "salom dunyo".replace(/[a-z]/g, harf => harf.toUpperCase());
console.log(natija); // "SALOM DUNYO"
```

---

## 📌 `.replaceAll(eski, yangi)` — Hammasini almashtirish (ES2021)

```javascript
let s = "men men men";

console.log(s.replace("men", "sen"));    // "sen men men" — faqat birinchi!
console.log(s.replaceAll("men", "sen")); // "sen sen sen" ✅

// Regex bilan (g flag kerak)
console.log(s.replace(/men/g, "sen")); // "sen sen sen"

// Amaliy: matnni tozalash
let dirtySting = "JavaScript___juda___yaxshi";
console.log(dirtySting.replaceAll("_", " ")); // "JavaScript juda yaxshi"
```

---

## 📌 `.slice(boshlash, tugash?)` — Kesib olish

```javascript
let s = "JavaScript";
//       0123456789

console.log(s.slice(0, 4));   // "Java"
console.log(s.slice(4));      // "Script" (oxirigacha)
console.log(s.slice(-6));     // "Script" (oxiridan 6 ta)
console.log(s.slice(-6, -3)); // "Scr"
console.log(s.slice(4, -1));  // "Scrip"

// Amaliy: qisqartirish
function qisqartir(matn, uzunlik) {
  if (matn.length <= uzunlik) return matn;
  return matn.slice(0, uzunlik) + "...";
}
console.log(qisqartir("Bu juda uzun matn", 8)); // "Bu juda ..."
```

---

## 📌 `.substring(boshlash, tugash?)` — Kesib olish (alternative)

```javascript
let s = "JavaScript";

console.log(s.substring(0, 4)); // "Java"
console.log(s.substring(4));    // "Script"

// slice vs substring farqi:
// substring manfiy indeksni 0 deb hisoblaydi
console.log(s.slice(-4));       // "ript"   ✅
console.log(s.substring(-4));   // "JavaScript" (manfiy → 0)

// Tavsiya: slice ishlating — aniqroq
```

---

## 📌 `.split(ajratuvchi, limit?)` — Massivga aylantirlish

```javascript
let jumla = "Men JavaScript o'qiyapman";

console.log(jumla.split(" "));   // ["Men", "JavaScript", "o'qiyapman"]
console.log(jumla.split(""));    // ["M","e","n"," ","J",...] — har bir belgi
console.log(jumla.split());      // ["Men JavaScript o'qiyapman"] — bo'linmaydi

let sanalar = "2024-03-15";
console.log(sanalar.split("-")); // ["2024", "03", "15"]

// Limit bilan
console.log("a,b,c,d".split(",", 2)); // ["a", "b"]

// Amaliy: CSV parse
function csvParse(satr) {
  return satr.split(",").map(s => s.trim());
}
console.log(csvParse("Ali, 25, Toshkent")); // ["Ali", "25", "Toshkent"]
```

---

## 📌 `.trim()`, `.trimStart()`, `.trimEnd()` — Bo'sh joylarni olib tashlash

```javascript
let s = "   Salom Dunyo!   ";

console.log(s.trim());       // "Salom Dunyo!" (ikki tomondan)
console.log(s.trimStart());  // "Salom Dunyo!   " (faqat boshidan)
console.log(s.trimEnd());    // "   Salom Dunyo!" (faqat oxiridan)

// Amaliy: forma validatsiyasi
function loginValidatsiya(login) {
  let tozaLogin = login.trim();
  if (tozaLogin.length < 3) return "Juda qisqa!";
  return `Login: ${tozaLogin}`;
}
console.log(loginValidatsiya("  ali  ")); // "Login: ali"
```

---

## 📌 `.toUpperCase()` / `.toLowerCase()` — Harf o'zgartirish

```javascript
let s = "JavaScript";

console.log(s.toUpperCase()); // "JAVASCRIPT"
console.log(s.toLowerCase()); // "javascript"

// Amaliy: case-insensitive taqqoslash
function tengMi(a, b) {
  return a.toLowerCase() === b.toLowerCase();
}
console.log(tengMi("Hello", "hello")); // true

// Birinchi harfni katta qilish
function birinchiKatta(so_z) {
  return so_z[0].toUpperCase() + so_z.slice(1).toLowerCase();
}
console.log(birinchiKatta("jAVAsCRIPT")); // "Javascript"
```

---

## 📌 `.toString()` — Satrga aylantirish

```javascript
let son = 42;
console.log(son.toString());    // "42"
console.log(son.toString(2));   // "101010" (ikkilik)
console.log(son.toString(8));   // "52" (sakkizlik)
console.log(son.toString(16));  // "2a" (o'n oltilik)

// Boolean
console.log(true.toString());  // "true"

// Array
console.log([1,2,3].toString()); // "1,2,3"
```

---

## 📌 `.localeCompare(boshqa)` — Tartiblash

```javascript
// -1: kichik, 0: teng, 1: katta
console.log("a".localeCompare("b")); // -1
console.log("b".localeCompare("a")); // 1
console.log("a".localeCompare("a")); // 0

// Massivni alifbo bo'yicha saralash
let ismlar = ["Zebra", "Ali", "Mehmet", "Bobur"];
ismlar.sort((a, b) => a.localeCompare(b));
console.log(ismlar); // ["Ali", "Bobur", "Mehmet", "Zebra"]
```

---

## 📌 `String.fromCharCode()` va `String.fromCodePoint()`

```javascript
// Unicode koddan belgi yaratish (static metod)
console.log(String.fromCharCode(65));     // "A"
console.log(String.fromCharCode(65, 66, 67)); // "ABC"
console.log(String.fromCharCode(9829));   // "♥"

// fromCodePoint — kattaroq Unicode uchun (ES6)
console.log(String.fromCodePoint(128512)); // "😀" (emoji!)
console.log(String.fromCodePoint(9731));   // "☃" (qor inson)
```

---

## 📌 `String.raw` — Teskari chiziqni e'tiborsiz qoldirish

```javascript
// Oddiy template literal — escape sequences ishlaydi
console.log(`C:\nUsers\name`);
// C:
// Users
// ame

// String.raw — escape sequences ishlamaydi
console.log(String.raw`C:\nUsers\name`);
// C:\nUsers\name  (literal \n ko'rsatiladi)

// Amaliy: Windows fayl yo'li
let yo_l = String.raw`C:\Users\Documents\file.txt`;
console.log(yo_l); // C:\Users\Documents\file.txt
```

---

## 🎯 Amaliy Vazifalar

```javascript
// 1. Matnning barcha so'zlarini katta harf bilan boshlang (Title Case)
function titleCase(matn) {
  return matn.split(" ")
    .map(so_z => /* ... */)
    .join(" ");
}
console.log(titleCase("salom dunyo js")); // "Salom Dunyo Js"

// 2. Phone raqamini formatlang: "998901234567" → "+998 (90) 123-45-67"
function phoneFormat(raqam) {
  // slice va padStart ishlating
}

// 3. Matndan HTML teglarini olib tashlang
function htmlTozalash(html) {
  return html.replace(/<[^>]*>/g, "");
}
console.log(htmlTozalash("<h1>Salom</h1><p>Dunyo</p>")); // "SalomDunyo"

// 4. Matnni teskari aylantiring
function teskari(matn) {
  return matn.split("").reverse().join("");
}
console.log(teskari("JavaScript")); // "tpircSavaJ"

// 5. So'zlarning sonini va o'rtacha uzunligini hisoblang
function so_zTahlil(jumla) {
  let so_zlar = jumla.trim().split(/\s+/);
  let son = so_zlar.length;
  let jami = so_zlar.reduce((sum, s) => sum + s.length, 0);
  return { son, o_rtacha: (jami / son).toFixed(2) };
}
```

---

## ❓ 30 ta Savol-Javob

### Boshlang'ich Savolar

**1. `.replace()` faqat birinchi uchraganinami almashtiradi?**
> Ha. Hammasini almashtirish uchun `.replaceAll()` yoki regex `/pattern/g` ishlatiladi.

**2. `.slice()` va `.substring()` ning asosiy farqi nima?**
> `slice` manfiy indekslarni qo'llaydi (oxiridan hisoblaydi). `substring` manfiy indeksni 0 deb hisoblaydi.

**3. `.split("")` nima qaytaradi?**
> Har bir belgini alohida element sifatida massivga ajratadi.

**4. `.trim()` nima qiladi?**
> Stringning boshi va oxirisidagi bo'sh joylarni (space, tab, newline) olib tashlaydi.

**5. `.toUpperCase()` asl stringni o'zgartiradimiI?**
> Yo'q. Yangi string qaytaradi. Asl o'zgarmaydi (immutable).

**6. `.padStart(5, "0")` qanday ishlaydi?**
> Stringni 5 uzunlikka yetkazish uchun boshiga "0" qo'shadi: `"42".padStart(5,"0")` → `"00042"`.

**7. `.repeat(0)` nima qaytaradi?**
> Bo'sh string `""`.

**8. `.lastIndexOf()` topilmasa nima qaytaradi?**
> `-1`.

**9. `.split()` argumentsiz chaqirilsa nima bo'ladi?**
> Butun stringni bitta element sifatida massivga qo'yadi: `["string"]`.

**10. `String.fromCharCode()` va `.charCodeAt()` qanday bog'liq?**
> `charCodeAt` belgidan kodni oladi, `fromCharCode` koddan belgini yaratadi — teskarisi.

---

### O'rta Savolar

**11. Matnning oxirgi so'zini qanday olamiz?**
```javascript
let oxirgi = matn.trim().split(" ").at(-1);
```

**12. `.replaceAll()` qachon kiritildi?**
> ES2021 (ES12). Oldinroq `replace(/pattern/g, yangi)` ishlatilgan.

**13. `.localeCompare()` qachon foydali?**
> Massivlarni lokal tilga mos alifbo tartibida saralashda.

**14. `.padEnd()` va `.padStart()` string allaqachon uzun bo'lsa nima bo'ladi?**
> Hech narsa qo'shilmaydi, string o'zgarishsiz qaytariladi.

**15. `String.raw` qanday holatda ishlatiladi?**
> Windows yo'llari, regex patterlar — teskari chiziq `\` ni escape qilmaslik kerak bo'lganda.

**16. `.slice(-3)` nima qaytaradi?**
> Oxirgi 3 ta belgini: `"JavaScript".slice(-3)` → `"ipt"`.

**17. `.split(",", 2)` nima qaytaradi?**
> Faqat 2 ta element bo'lgan massiv — limit qo'yiladi.

**18. Matnni alifbo tartibida saralash uchun qanday qilish kerak?**
> `arr.sort((a, b) => a.localeCompare(b))`.

**19. `.trim()` vs `.replace(/\s+/g, "")` farqi nima?**
> `trim` faqat tashqi bo'sh joylarni, `replace(/\s+/g,"")` esa ichkaridagi barcha bo'sh joylarni ham olib tashlaydi.

**20. `.toString(16)` nima uchun ishlatiladi?**
> Sonni o'n oltilik (hexadecimal) formatga o'tkazish: rang kodlari va h.k. uchun.

---

