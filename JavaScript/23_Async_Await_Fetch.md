# 23-Dars: Async/Await va Fetch API

## 📌 Async/Await nima?

**async/await** — Promise lar bilan ishlashni osonlashtiradigan sintaksik shakar (ES2017). Asinxron kodni sinxron kabi yozish imkonini beradi.

```javascript
// Promise bilan
function ma_lumotOlish() {
  return fetch("https://api.example.com/users")
    .then(r => r.json())
    .then(data => { console.log(data); })
    .catch(e => console.log(e));
}

// async/await bilan — ancha tushunarli!
async function ma_lumotOlish() {
  try {
    let javob = await fetch("https://api.example.com/users");
    let data = await javob.json();
    console.log(data);
  } catch (e) {
    console.log("Xato:", e.message);
  }
}
```

---

## 📌 `async` funksiya

```javascript
// async funksiya har doim Promise qaytaradi
async function salom() {
  return "Salom!"; // Promise.resolve("Salom!") bilan bir xil
}

salom().then(n => console.log(n)); // "Salom!"

// async arrow function
const hisoblash = async (a, b) => a + b;

// async method
const ob'ekt = {
  async ma_lumot() {
    return await fetch("...").then(r => r.json());
  }
};
```

---

## 📌 `await` kalit so'zi

```javascript
// await — faqat async funksiya ichida ishlatiladi
// Promise tugaguncha kutadi va natijani qaytaradi

async function misol() {
  // ❌ Bu xato:
  // let n = await somePromise(); // async tashqarisida!

  // ✅ Bu to'g'ri:
  let n = await new Promise(r => setTimeout(() => r(42), 1000));
  console.log(n); // 42 (1 soniyadan keyin)

  // Zanjirli await
  let a = await Promise.resolve(1);
  let b = await Promise.resolve(a + 2);
  let c = await Promise.resolve(b * 3);
  console.log(c); // 9
}
```

---

## 📌 Xatolarni Qayta Ishlash

```javascript
// 1. Try-Catch bilan
async function xavfsizFetch(url) {
  try {
    let javob = await fetch(url);
    if (!javob.ok) {
      throw new Error(`HTTP xato: ${javob.status}`);
    }
    return await javob.json();
  } catch (xato) {
    console.error("Fetch xatosi:", xato.message);
    return null;
  }
}

// 2. .catch() bilan
async function fetch_catch(url) {
  let data = await fetch(url).catch(e => null);
  return data;
}

// 3. Yordamchi funksiya bilan
async function to_[ok, err](promise) {
  try {
    return [await promise, null];
  } catch (e) {
    return [null, e];
  }
}

// Ishlatish
async function ishlatish() {
  let [data, xato] = await to_[ok, err](fetch("...").then(r => r.json()));
  if (xato) return console.log("Xato:", xato);
  console.log("Ma'lumot:", data);
}
```

---

## 📌 Parallel va Ketma-Ket

```javascript
// ❌ Ketma-ket (sekin) — 2+1 = 3 soniya
async function ketmaKet() {
  let a = await serverSo_rov(1, 2000); // 2 soniya kutadi
  let b = await serverSo_rov(2, 1000); // 1 soniya kutadi
  console.log(a, b); // 3 soniyada
}

// ✅ Parallel (tez) — max(2,1) = 2 soniya
async function parallel() {
  let [a, b] = await Promise.all([
    serverSo_rov(1, 2000),
    serverSo_rov(2, 1000)
  ]);
  console.log(a, b); // 2 soniyada!
}
```

---

## 📌 Fetch API — Asosiy

```javascript
// GET so'rovi
async function userlarOlish() {
  let javob = await fetch("https://jsonplaceholder.typicode.com/users");
  
  // Status tekshirish
  console.log(javob.status);     // 200
  console.log(javob.ok);         // true (200-299)
  console.log(javob.statusText); // "OK"
  
  // Ma'lumotni olish
  let foydalanuvchilar = await javob.json();
  return foydalanuvchilar;
}

// URL lar bilan ishlash
let javob = await fetch("https://api.example.com/users?page=1&limit=10");
let ma_lumot = await javov.json();
let matn = await javov.text();     // Matn sifatida
let blob = await javov.blob();     // Fayl sifatida
```

---

## 📌 Fetch API — Headers va Options

```javascript
// GET bilan headers
let javob = await fetch("https://api.example.com/data", {
  method: "GET",
  headers: {
    "Content-Type": "application/json",
    "Authorization": "Bearer mytoken123"
  }
});

// POST so'rovi
async function yangiUserYaratish(userData) {
  let javob = await fetch("https://jsonplaceholder.typicode.com/users", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(userData)
  });
  
  let yangiUser = await javob.json();
  console.log("Yaratildi:", yangiUser);
  return yangiUser;
}

await yangiUserYaratish({ ism: "Ali", email: "ali@example.com" });
```

---

## 🎯 10 ta Amaliy Vazifa

```javascript
const BASE_URL = "https://jsonplaceholder.typicode.com";

// 1. Barcha postlarni olish
async function postlarOlish() {
  let javob = await fetch(`${BASE_URL}/posts`);
  let postlar = await javob.json();
  console.log(`${postlar.length} ta post topildi`);
  return postlar;
}

// 2. Bitta foydalanuvchini olish
async function foydalanuvchiOlish(id) {
  let javob = await fetch(`${BASE_URL}/users/${id}`);
  if (!javov.ok) throw new Error(`Foydalanuvchi topilmadi: ${id}`);
  return javob.json();
}

// 3. Parallel ravishda bir nechta so'rov
async function parallelSo_rovlar() {
  let [postlar, foydalanuvchilar, sharxlar] = await Promise.all([
    fetch(`${BASE_URL}/posts`).then(r => r.json()),
    fetch(`${BASE_URL}/users`).then(r => r.json()),
    fetch(`${BASE_URL}/comments`).then(r => r.json())
  ]);
  console.log(postlar.length, foydalanuvchilar.length, sharxlar.length);
}

// 4. Loading holati bilan fetch
async function loadingBilan(url) {
  console.log("Yuklanmoqda...");
  try {
    let javob = await fetch(url);
    let data = await javob.json();
    console.log("Yuklandi!");
    return data;
  } finally {
    console.log("Yuklanish tugadi.");
  }
}

// 5. Sahifalash (Pagination)
async function sahifalab_olish(sahifa = 1, limit = 10) {
  let javob = await fetch(`${BASE_URL}/posts?_page=${sahifa}&_limit=${limit}`);
  let postlar = await javob.json();
  let jami = javob.headers.get("X-Total-Count");
  return { postlar, jami: parseInt(jami), sahifa };
}

// 6. Qidirish
async function postlarQidirish(sorov) {
  let javob = await fetch(`${BASE_URL}/posts?q=${encodeURIComponent(sorov)}`);
  return javob.json();
}

// 7. Retry bilan fetch
async function retryFetch(url, urinishlar = 3) {
  for (let i = 0; i < urinishlar; i++) {
    try {
      let javob = await fetch(url);
      if (!javob.ok) throw new Error(`${javob.status}`);
      return await javob.json();
    } catch (xato) {
      if (i === urinishlar - 1) throw xato;
      console.log(`Qayta urinish ${i + 1}/${urinishlar}...`);
      await new Promise(r => setTimeout(r, 1000 * (i + 1))); // Ortib boruvchi kutish
    }
  }
}

// 8. POST so'rovi bilan yangi post yaratish
async function postYaratish(sarlavha, matn, userId) {
  let javob = await fetch(`${BASE_URL}/posts`, {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify({ title: sarlavha, body: matn, userId })
  });
  
  if (!javob.ok) throw new Error("Post yaratilmadi!");
  let yangi = await javob.json();
  console.log("Yangi post ID:", yangi.id);
  return yangi;
}

// 9. Foydalanuvchining postlarini olish va filtrlash
async function foydalanuvchiPostlari(userId, kalit_so_z = "") {
  let [user, postlar] = await Promise.all([
    fetch(`${BASE_URL}/users/${userId}`).then(r => r.json()),
    fetch(`${BASE_URL}/posts?userId=${userId}`).then(r => r.json())
  ]);
  
  let filtrlangan = kalit_so_z
    ? postlar.filter(p => p.title.includes(kalit_so_z))
    : postlar;
    
  return { user: user.name, postSoni: postlar.length, filtrlangan };
}
foydalanuvchiPostlari(1).then(console.log);

// 10. Universal API mijoz (client)
class APIClient {
  constructor(baseURL) {
    this.baseURL = baseURL;
  }

  async so_rov(endpoint, options = {}) {
    let url = `${this.baseURL}${endpoint}`;
    let javob = await fetch(url, {
      headers: { "Content-Type": "application/json", ...options.headers },
      ...options
    });
    if (!javob.ok) throw new Error(`API xato: ${javob.status}`);
    return javob.json();
  }

  get(endpoint) { return this.so_rov(endpoint); }
  post(endpoint, data) {
    return this.so_rov(endpoint, { method: "POST", body: JSON.stringify(data) });
  }
  put(endpoint, data) {
    return this.so_rov(endpoint, { method: "PUT", body: JSON.stringify(data) });
  }
  delete(endpoint) {
    return this.so_rov(endpoint, { method: "DELETE" });
  }
}

const api = new APIClient(BASE_URL);
api.get("/posts/1").then(console.log);
api.post("/posts", { title: "Test", body: "...", userId: 1 }).then(console.log);
```
