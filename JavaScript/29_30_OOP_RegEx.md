# 29-Dars: OOP — Class va Ob'ektga Yo'naltirilgan Dasturlash

## 📌 OOP 4 ta asosi

```
OOP Asoslari
├── Encapsulation  — ma'lumotni yashirish
├── Inheritance    — meros olish
├── Polymorphism   — ko'p shakllilik
└── Abstraction    — murakkablikni yashirish
```

---

## 📌 Class Sintaksisi

```javascript
class Hayvon {
  // Konstruktor — ob'ekt yaratilganda chaqiriladi
  constructor(nomi, tovush) {
    this.nomi = nomi;    // Public property
    this.tovush = tovush;
    this._yosh = 0;      // Convention: _ = "private" (aslida public)
    #id = Math.random(); // Private field (ES2022) — haqiqiy yashirish
  }

  // Metod
  gapir() {
    return `${this.nomi} deydi: "${this.tovush}!"`;
  }

  // Getter
  get ma_lumot() {
    return `${this.nomi}, ${this._yosh} yosh`;
  }

  // Setter
  set yosh(yangiYosh) {
    if (yangiYosh < 0) throw new Error("Yosh manfiy bo'lmaydi!");
    this._yosh = yangiYosh;
  }

  // Static method — instansiyaga emas, sinfga tegishli
  static taqqosla(a, b) {
    return a.nomi.localeCompare(b.nomi);
  }

  // toString override
  toString() { return `[Hayvon: ${this.nomi}]`; }
}

let mushuk = new Hayvon("Mitti", "Miyov");
console.log(mushuk.gapir());   // "Mitti deydi: "Miyov!""
mushuk.yosh = 3;               // Setter ishlatdi
console.log(mushuk.ma_lumot);  // "Mitti, 3 yosh"
```

---

## 📌 Inheritance (Meros olish) — `extends` va `super`

```javascript
class Hayvon {
  constructor(nomi) { this.nomi = nomi; }
  gapir() { return `${this.nomi} ovoz chiqaryapti`; }
  harakat() { return `${this.nomi} harakatlanmoqda`; }
}

class Mushuk extends Hayvon {
  constructor(nomi, rang) {
    super(nomi); // Ota sinfning constructorini chaqirish — MAJBURIY!
    this.rang = rang;
  }
  
  // Override — ota metodini qayta yozish
  gapir() {
    return `${this.nomi} (${this.rang}) deydi: "Miyov!"`;
  }
  
  // Ota metodini chaqirish
  tavsif() {
    return `${super.gapir()} va miyovlaydi`; // super bilan
  }
}

class It extends Hayvon {
  gapir() { return `${this.nomi} deydi: "Vov vov!"` ; }
}

let mushuk = new Mushuk("Mitti", "oq");
let it = new It("Rex");

console.log(mushuk.gapir());    // "Mitti (oq) deydi: "Miyov!""
console.log(it.gapir());        // "Rex deydi: "Vov vov!""
console.log(mushuk.harakat());  // Ota metodini meros oldi ✅

// instanceof
console.log(mushuk instanceof Mushuk); // true
console.log(mushuk instanceof Hayvon); // true — meros!
```

---

## 📌 Polymorphism (Ko'p shakllilik)

```javascript
class Shakl {
  maydon() { return 0; }
  tovsif() { return `Maydon: ${this.maydon().toFixed(2)}`; }
}

class Doira extends Shakl {
  constructor(r) { super(); this.r = r; }
  maydon() { return Math.PI * this.r ** 2; }
}

class To_g_riburchak extends Shakl {
  constructor(k, h) { super(); this.k = k; this.h = h; }
  maydon() { return this.k * this.h; }
}

class Uchburchak extends Shakl {
  constructor(a, b, c) { super(); this.a=a; this.b=b; this.c=c; }
  maydon() {
    let p = (this.a + this.b + this.c) / 2;
    return Math.sqrt(p * (p-this.a) * (p-this.b) * (p-this.c));
  }
}

// Polymorphizm — bir xil metod, turli xil natija
let shakllar = [new Doira(5), new To_g_riburchak(4,6), new Uchburchak(3,4,5)];
shakllar.forEach(s => console.log(s.constructor.name + ": " + s.tovsif()));
```

---

## 📌 Encapsulation — Private Fields

```javascript
class BankHisobi {
  #balans;          // Private field — tashqaridan KIRISH YO'Q
  #tarix = [];      // Private array

  constructor(egasi, boshlangich) {
    this.egasi = egasi;
    this.#balans = boshlangich;
  }

  kirim(miqdor) {
    if (miqdor <= 0) throw new Error("Miqdor musbat bo'lishi kerak!");
    this.#balans += miqdor;
    this.#tarix.push({ tur: "kirim", miqdor, sana: new Date() });
    return this;  // Method chaining uchun
  }

  chiqim(miqdor) {
    if (miqdor > this.#balans) throw new Error("Balans yetarli emas!");
    this.#balans -= miqdor;
    this.#tarix.push({ tur: "chiqim", miqdor, sana: new Date() });
    return this;
  }

  get balans() { return this.#balans; }
  get tarix() { return [...this.#tarix]; } // Nusxa qaytaradi
}

let hisob = new BankHisobi("Ali", 1000000);
hisob.kirim(500000).chiqim(200000); // Method chaining
console.log(hisob.balans);  // 1300000
// hisob.#balans — ❌ SyntaxError (private!)
```

---

## 📌 Static Metodlar va Xususiyatlar

```javascript
class IDGenerator {
  static #joriyId = 0;      // Private static
  static preFiks = "ID";    // Public static
  
  static keyingisi() {
    return `${IDGenerator.preFiks}-${++IDGenerator.#joriyId}`;
  }
  
  static reset() { IDGenerator.#joriyId = 0; }
}

console.log(IDGenerator.keyingisi()); // "ID-1"
console.log(IDGenerator.keyingisi()); // "ID-2"
IDGenerator.preFiks = "USR";
console.log(IDGenerator.keyingisi()); // "USR-3"
```

---

## 🎯 10 ta Amaliy Vazifa

```javascript
// 1. Hayvon sinf iyerarxiyasi
class Hayvon2 {
  constructor(nomi, yosh) { this.nomi = nomi; this.yosh = yosh; }
  tavsif() { return `${this.nomi} (${this.yosh} yosh)`; }
}
class Qush extends Hayvon2 {
  constructor(nomi, yosh, qanotKengligi) {
    super(nomi, yosh);
    this.qanotKengligi = qanotKengligi;
  }
  uch() { return `${this.nomi} uchmoqda!`; }
}
let qush = new Qush("Burgut", 5, 200);
console.log(qush.tavsif()); // "Burgut (5 yosh)"
console.log(qush.uch());    // "Burgut uchmoqda!"

// 2. Stack (LIFO) sinfi
class Stack {
  #elementlar = [];
  push(el) { this.#elementlar.push(el); return this; }
  pop() { return this.#elementlar.pop(); }
  peek() { return this.#elementlar.at(-1); }
  get uzunlik() { return this.#elementlar.length; }
  bo_shMi() { return this.#elementlar.length === 0; }
}
let stek = new Stack();
stek.push(1).push(2).push(3);
console.log(stek.pop()); // 3

// 3. Queue (FIFO) sinfi
class Queue {
  #elementlar = [];
  kirish(el) { this.#elementlar.push(el); return this; }
  chiqish() { return this.#elementlar.shift(); }
  get front() { return this.#elementlar[0]; }
  get uzunlik() { return this.#elementlar.length; }
}
let navbat = new Queue();
navbat.kirish("Ali").kirish("Vali").kirish("Gani");
console.log(navbat.chiqish()); // "Ali"

// 4. Konfiguratsiya Builder pattern
class Sorov {
  #sozlamalar = { method: "GET", headers: {}, timeout: 5000 };
  
  method(m) { this.#sozlamalar.method = m; return this; }
  header(k, v) { this.#sozlamalar.headers[k] = v; return this; }
  timeout(ms) { this.#sozlamalar.timeout = ms; return this; }
  qur() { return { ...this.#sozlamalar }; }
}
let sozlamalar = new Sorov()
  .method("POST")
  .header("Content-Type", "application/json")
  .header("Authorization", "Bearer token")
  .timeout(3000)
  .qur();
console.log(sozlamalar);

// 5. Polymorphizm — to'lov usullari
class To_lovUsuli {
  to'la(miqdor) { throw new Error("Bu metodn overlap qiling!"); }
}
class KartaBilan extends To_lovUsuli {
  constructor(karta) { super(); this.karta = karta; }
  to'la(miqdor) { return `${this.karta} orqali ${miqdor} to'landi`; }
}
class NaqddaBilan extends To_lovUsuli {
  to'la(miqdor) { return `${miqdor} naqd to'landi`; }
}
[new KartaBilan("**** 1234"), new NaqddaBilan()]
  .forEach(usul => console.log(usul.to'la(50000)));

// 6. Singleton pattern
class Konfiguratsiya {
  static #instansiya = null;
  #ma_lumotlar = {};
  
  constructor() {
    if (Konfiguratsiya.#instansiya) return Konfiguratsiya.#instansiya;
    Konfiguratsiya.#instansiya = this;
  }
  
  o'rnat(k, v) { this.#ma_lumotlar[k] = v; return this; }
  ol(k) { return this.#ma_lumotlar[k]; }
}
let k1 = new Konfiguratsiya();
let k2 = new Konfiguratsiya();
k1.o'rnat("tema", "qorongu");
console.log(k2.ol("tema")); // "qorongu" (bir xil instansiya!)
console.log(k1 === k2);      // true

// 7-10: Talaba menejment tizimi (to'liq OOP)
class Shaxs {
  constructor(ism, email) {
    this.ism = ism; this.email = email;
    this.id = ++Shaxs.hisoblagich;
  }
  static hisoblagich = 0;
  toString() { return `${this.ism} (${this.email})`; }
}

class Talaba extends Shaxs {
  #ballar = new Map();
  constructor(ism, email, yo_nalish) {
    super(ism, email);
    this.yo_nalish = yo_nalish;
  }
  ball_qo'y(fan, ball) { this.#ballar.set(fan, ball); return this; }
  get o'rtacha() {
    if (!this.#ballar.size) return 0;
    return [...this.#ballar.values()].reduce((s,b) => s+b, 0) / this.#ballar.size;
  }
  tavsif() {
    return `${super.toString()} | ${this.yo'nalish} | O'rtacha: ${this.o'rtacha.toFixed(1)}`;
  }
}

class O'qituvchi extends Shaxs {
  #talabalar = new Set();
  constructor(ism, email, fan) { super(ism, email); this.fan = fan; }
  talaba_qo'sh(t) { this.#talabalar.add(t); }
  eng_yaxshi() { return [...this.#talabalar].sort((a,b) => b.o'rtacha - a.o'rtacha)[0]; }
}
```

---

# 30-Dars: RegEx (Regular Expressions)

## 📌 RegEx nima?

```javascript
// Yaratish
let regex1 = /pattern/;         // Literal
let regex2 = new RegExp("pattern"); // Konstruktor (dinamik)

// Flaglar
let i_flag = /salom/i;   // i = case insensitive
let g_flag = /a/g;       // g = global (hammasi)
let m_flag = /^start/m;  // m = multiline
let s_flag = /./s;       // s = dotAll (\n ham .)
```

---

## 📌 Asosiy Metodlar

```javascript
let matn = "JavaScript juda yaxshi!";

// test() — true/false qaytaradi
/JavaScript/.test(matn);  // true
/Python/.test(matn);      // false

// match() — mosliklarni massivda qaytaradi
"banana".match(/a/g);     // ["a","a","a"]
"hello".match(/(\w+)/);   // ["hello", "hello"] + groups

// matchAll() — iterator qaytaradi
for (let moslik of "a1b2c3".matchAll(/[a-z](\d)/g)) {
  console.log(moslik[0], moslik[1]); // "a1" "1" ...
}

// exec() — bitta moslikni qaytaradi
let regex = /(\d+)/g;
let m;
while ((m = regex.exec("abc123def456")) !== null) {
  console.log(m[0], m.index); // "123" 3, "456" 9
}

// replace() va replaceAll()
"hello world".replace(/o/g, "0");    // "hell0 w0rld"
"one two three".replace(/\s+/, ","); // "one,two three" (birinchi)
"a1b2c3".replace(/[0-9]/g, "#");     // "a#b#c#"
```

---

## 📌 Meta Belgilar

```javascript
// Belgilar
\d   // Raqam [0-9]
\D   // Raqam emas
\w   // So'z belgisi [a-zA-Z0-9_]
\W   // So'z belgisi emas
\s   // Bo'sh joy (space, tab, newline)
\S   // Bo'sh joy emas
.    // Istalgan belgi (\n dan tashqari)

// Chegaralar
^    // Boshlanish
$    // Tugash
\b   // So'z chegarasi
\B   // So'z chegarasi emas

// Miqdorlar
*    // 0 yoki ko'p
+    // 1 yoki ko'p
?    // 0 yoki 1
{n}  // Aniq n ta
{n,} // n va undan ko'p
{n,m}// n dan m gacha

// Guruhlar
(abc) // Capture group
(?:abc) // Non-capture group
[abc] // To'plam
[^abc]// Inkori to'plam
a|b  // YOKI
```

---

## 📌 Amaliy Patternlar

```javascript
// Email
const email_regex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
email_regex.test("ali@mail.com"); // true
email_regex.test("notanemail");   // false

// Telefon (O'zbekiston)
const tel_regex = /^\+998\d{9}$/;
tel_regex.test("+998901234567"); // true

// URL
const url_regex = /^https?:\/\/.+\..+/;
url_regex.test("https://google.com"); // true

// Parol tekshirish (katta, kichik, raqam)
const parol_regex = /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d).{8,}$/;
parol_regex.test("Abc12345"); // true

// Sana (DD.MM.YYYY)
const sana_regex = /^(\d{2})\.(\d{2})\.(\d{4})$/;
"15.03.2024".match(sana_regex); // ["15.03.2024", "15", "03", "2024"]

// HTML teglarni olib tashlash
"<h1>Salom</h1>".replace(/<[^>]*>/g, ""); // "Salom"
```

---

## 🎯 10 ta Amaliy Vazifa

```javascript
// 1. Email validatsiya
function emailValid(email) {
  return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email);
}
console.log(emailValid("ali@mail.com")); // true
console.log(emailValid("notvalid"));     // false

// 2. Matndagi barcha sonlarni toping
function sonlarTopish(matn) {
  return matn.match(/\d+(\.\d+)?/g)?.map(Number) || [];
}
console.log(sonlarTopish("10 ta olma va 3.5 kg banan")); // [10, 3.5]

// 3. CamelCase ni snake_case ga aylantiring
function camelToSnake(s) {
  return s.replace(/([A-Z])/g, m => `_${m.toLowerCase()}`);
}
console.log(camelToSnake("myVariableName")); // "my_variable_name"

// 4. Template engine
function template(shablon, ma_lumotlar) {
  return shablon.replace(/\{\{(\w+)\}\}/g, (m, kalit) => ma_lumotlar[kalit] ?? m);
}
console.log(template("Salom {{ism}}, {{yosh}} yoshsiz!", { ism: "Ali", yosh: 25 }));
// "Salom Ali, 25 yoshsiz!"

// 5. Parol kuchi tekshirish
function parolKuchi(parol) {
  if (/^.{0,7}$/.test(parol)) return "Juda zaif";
  if (/^(?=.*[A-Z])(?=.*[a-z])(?=.*\d)(?=.*[!@#$]).{12,}$/.test(parol)) return "A'lo";
  if (/^(?=.*[A-Z])(?=.*[a-z])(?=.*\d).{8,}$/.test(parol)) return "Yaxshi";
  return "O'rtacha";
}
console.log(parolKuchi("abc"));         // "Juda zaif"
console.log(parolKuchi("Abc12345"));    // "Yaxshi"
console.log(parolKuchi("Abc12!@#long")); // "A'lo"

// 6. URL dan parametrlarni olish
function urlParams(url) {
  let params = {};
  url.replace(/[?&]([^=&]+)=([^&]*)/g, (m, k, v) => {
    params[k] = decodeURIComponent(v);
  });
  return params;
}
console.log(urlParams("https://example.com?ism=Ali&yosh=25&shahar=Toshkent"));
// {ism:"Ali", yosh:"25", shahar:"Toshkent"}

// 7. Markdown qalin matnini HTMLga aylantirish
function markdownToHtml(md) {
  return md
    .replace(/\*\*(.+?)\*\*/g, "<strong>$1</strong>")
    .replace(/\*(.+?)\*/g, "<em>$1</em>")
    .replace(/`(.+?)`/g, "<code>$1</code>");
}
console.log(markdownToHtml("Bu **qalin** va *kursiv* va `kod`"));
// "Bu <strong>qalin</strong> va <em>kursiv</em> va <code>kod</code>"

// 8. Takrorlanuvchi so'zlarni toping
function takrorSo_zlar(matn) {
  let uchrashlar = {};
  matn.toLowerCase().match(/\b\w+\b/g)?.forEach(s => {
    uchrashlar[s] = (uchrashlar[s] || 0) + 1;
  });
  return Object.entries(uchrashlar).filter(([,n]) => n > 1);
}
console.log(takrorSo_zlar("men va sen va biz va men"));
// [["men",2],["va",3]]

// 9. Kredit karta raqamini formatlash
function kartaFormatlash(raqam) {
  return raqam.replace(/\D/g,"").replace(/(\d{4})(?=\d)/g,"$1 ");
}
console.log(kartaFormatlash("1234567890123456")); // "1234 5678 9012 3456"

// 10. Lookahead/Lookbehind bilan narx formatlash
function narxFormatlash(son) {
  return son.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
}
console.log(narxFormatlash(1000000));  // "1,000,000"
console.log(narxFormatlash(12345678)); // "12,345,678"
```
