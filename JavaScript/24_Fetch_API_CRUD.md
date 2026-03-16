# 24-Dars: Fetch API — CRUD Operatsiyalari

## 📌 HTTP Metodlari

| Metod    | Maqsad                     | Body kerakmi? |
|----------|----------------------------|---------------|
| GET      | Ma'lumot olish             | ❌            |
| POST     | Yangi ma'lumot yaratish    | ✅            |
| PUT      | To'liq yangilash           | ✅            |
| PATCH    | Qisman yangilash           | ✅            |
| DELETE   | O'chirish                  | ❌            |

---

## 📌 GET — Ma'lumot Olish

```javascript
const BASE = "https://jsonplaceholder.typicode.com";

// Barcha elementlarni olish
async function hammasiniOlish() {
  let javob = await fetch(`${BASE}/posts`);
  let postlar = await javob.json();
  return postlar;
}

// Bitta elementni olish (ID bo'yicha)
async function biriniOlish(id) {
  let javob = await fetch(`${BASE}/posts/${id}`);
  if (!javob.ok) throw new Error(`Topilmadi: ${id}`);
  return javob.json();
}

// Query parametrlar bilan
async function filtrlabOlish(userId) {
  let url = new URL(`${BASE}/posts`);
  url.searchParams.set("userId", userId);
  url.searchParams.set("_limit", 5);
  
  let javob = await fetch(url);
  return javob.json();
}
```

---

## 📌 POST — Yangi Ma'lumot Yaratish

```javascript
async function yaratish(yangiMa_lumot) {
  let javob = await fetch(`${BASE}/posts`, {
    method: "POST",
    headers: {
      "Content-Type": "application/json"
    },
    body: JSON.stringify(yangiMa_lumot)
  });
  
  if (!javob.ok) throw new Error(`POST xato: ${javob.status}`);
  let yaratildi = await javob.json();
  console.log("201 Created:", yaratildi);
  return yaratildi;
}

// Ishlatish
await yaratish({
  title: "Yangi post",
  body: "Bu yangi post matni",
  userId: 1
});
```

---

## 📌 PUT — To'liq Yangilash

```javascript
// PUT — elementning BARCHA maydonini yangilaydi
async function to_liqYangilash(id, ma_lumot) {
  let javob = await fetch(`${BASE}/posts/${id}`, {
    method: "PUT",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(ma_lumot)
  });
  
  let yangilandi = await javob.json();
  console.log("PUT natija:", yangilandi);
  return yangilandi;
}

await to_liqYangilash(1, {
  id: 1,
  title: "Yangilangan sarlavha",
  body: "Yangilangan matn",
  userId: 1
  // ⚠️ Barcha maydonlarni yuborish KERAK
});
```

---

## 📌 PATCH — Qisman Yangilash

```javascript
// PATCH — faqat o'zgartimoqchi bo'lgan maydonlarni yuboradi
async function qismanYangilash(id, o_zgarishlar) {
  let javob = await fetch(`${BASE}/posts/${id}`, {
    method: "PATCH",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(o_zgarishlar)
  });
  
  let yangilandi = await javob.json();
  console.log("PATCH natija:", yangilandi);
  return yangilandi;
}

// Faqat sarlavhani o'zgartirish
await qismanYangilash(1, { title: "Yangi sarlavha" });
// id, body, userId — o'zgarmaydi!
```

---

## 📌 DELETE — O'chirish

```javascript
async function o_chirish(id) {
  let javob = await fetch(`${BASE}/posts/${id}`, {
    method: "DELETE"
  });
  
  if (!javob.ok) throw new Error(`O'chirib bo'lmadi: ${id}`);
  console.log(`Post #${id} o'chirildi (Status: ${javob.status})`);
  return true;
}

await o_chirish(1); // "Post #1 o'chirildi (Status: 200)"
```

---

## 📌 HTTP Status Kodlari

```javascript
async function statusTekshirish(url) {
  let javob = await fetch(url);
  
  switch (true) {
    case javob.status === 200: console.log("OK"); break;
    case javob.status === 201: console.log("Yaratildi"); break;
    case javob.status === 204: console.log("Kontent yo'q"); break;
    case javob.status === 400: console.log("Noto'g'ri so'rov"); break;
    case javob.status === 401: console.log("Autentifikatsiya kerak"); break;
    case javob.status === 403: console.log("Ruxsat yo'q"); break;
    case javob.status === 404: console.log("Topilmadi"); break;
    case javob.status === 500: console.log("Server xatosi"); break;
    default: console.log("Status:", javob.status);
  }
}
```

---

## 📌 To'liq CRUD Sinfi

```javascript
class CRUD {
  constructor(baseURL) {
    this.baseURL = baseURL;
    this.headers = { "Content-Type": "application/json" };
  }

  async _so_rov(url, options = {}) {
    let javob = await fetch(url, { headers: this.headers, ...options });
    if (!javob.ok) throw new Error(`HTTP ${javob.status}: ${javob.statusText}`);
    if (javob.status === 204) return null;
    return javob.json();
  }

  // CREATE
  create(endpoint, data) {
    return this._so_rov(`${this.baseURL}${endpoint}`, {
      method: "POST",
      body: JSON.stringify(data)
    });
  }

  // READ (all or by id)
  read(endpoint, id = "") {
    return this._so_rov(`${this.baseURL}${endpoint}${id ? `/${id}` : ""}`);
  }

  // UPDATE (full)
  update(endpoint, id, data) {
    return this._so_rov(`${this.baseURL}${endpoint}/${id}`, {
      method: "PUT",
      body: JSON.stringify(data)
    });
  }

  // PATCH (partial)
  patch(endpoint, id, data) {
    return this._so_rov(`${this.baseURL}${endpoint}/${id}`, {
      method: "PATCH",
      body: JSON.stringify(data)
    });
  }

  // DELETE
  delete(endpoint, id) {
    return this._so_rov(`${this.baseURL}${endpoint}/${id}`, {
      method: "DELETE"
    });
  }
}

const api = new CRUD("https://jsonplaceholder.typicode.com");
```

---

## 🎯 10 ta Amaliy Vazifa

```javascript
const api = new CRUD("https://jsonplaceholder.typicode.com");

// 1. Barcha postlarni olish va ekranda ko'rsatish
async function postlarniKo_rsatish() {
  let postlar = await api.read("/posts");
  postlar.slice(0, 5).forEach(p => {
    console.log(`#${p.id}: ${p.title}`);
  });
}

// 2. Bitta userning barcha postlarini olish
async function userPostlari(userId) {
  let postlar = await api.read("/posts");
  return postlar.filter(p => p.userId === userId);
}
userPostlari(1).then(p => console.log(`User 1 ning ${p.length} ta posti`));

// 3. Yangi post yaratish
async function yangiPost() {
  let post = await api.create("/posts", {
    title: "Mening birinchi postim",
    body: "Bu test post matni",
    userId: 1
  });
  console.log("Yaratildi:", post);
}

// 4. Postni to'liq yangilash (PUT)
async function postYangilash(id) {
  let yangilangan = await api.update("/posts", id, {
    id,
    title: "Yangilangan sarlavha",
    body: "Yangilangan matn",
    userId: 1
  });
  console.log("Yangilandi:", yangilangan.title);
}

// 5. Faqat sarlavhani o'zgartirish (PATCH)
async function sarlavhaO_zgartirish(id, yangiSarlavha) {
  let natija = await api.patch("/posts", id, { title: yangiSarlavha });
  console.log(`Post #${id} sarlavhasi: "${natija.title}"`);
}

// 6. Post o'chirish
async function postO_chirish(id) {
  await api.delete("/posts", id);
  console.log(`Post #${id} muvaffaqiyatli o'chirildi`);
}

// 7. CRUD zanjiri: Yaratish → O'qish → Yangilash → O'chirish
async function to_liqCRUD() {
  console.log("=== CRUD Demo ===");
  
  // CREATE
  let yangi = await api.create("/posts", { title: "Test", body: "...", userId: 1 });
  console.log("1. Yaratildi:", yangi.id);
  
  // READ
  let olindi = await api.read("/posts", yangi.id);
  console.log("2. O'qildi:", olindi.title);
  
  // UPDATE
  let yangilandi = await api.patch("/posts", yangi.id, { title: "Yangi sarlavha" });
  console.log("3. Yangilandi:", yangilandi.title);
  
  // DELETE
  await api.delete("/posts", yangi.id);
  console.log("4. O'chirildi!");
}
to_liqCRUD();

// 8. Barcha foydalanuvchilar va ularning postlari soni
async function foydalanuvchiStatistika() {
  let [users, posts] = await Promise.all([
    api.read("/users"),
    api.read("/posts")
  ]);
  
  return users.map(user => ({
    ism: user.name,
    postSoni: posts.filter(p => p.userId === user.id).length
  })).sort((a, b) => b.postSoni - a.postSoni);
}
foydalanuvchiStatistika().then(stat => {
  stat.forEach(s => console.log(`${s.ism}: ${s.postSoni} post`));
});

// 9. POST va uning sharxlarini birga olish
async function postVaSharxlari(postId) {
  let [post, sharxlar] = await Promise.all([
    api.read("/posts", postId),
    fetch(`https://jsonplaceholder.typicode.com/posts/${postId}/comments`).then(r => r.json())
  ]);
  
  return {
    ...post,
    sharxlar,
    sharxSoni: sharxlar.length
  };
}
postVaSharxlari(1).then(data => {
  console.log(`"${data.title}" — ${data.sharxSoni} ta sharx`);
});

// 10. Optimistik yangilanish (UI ni oldin yangilash)
let lokal_postlar = [];

async function optimistikYangilash(id, yangiSarlavha) {
  // UI ni darhol yangilash
  let indeks = lokal_postlar.findIndex(p => p.id === id);
  let eskilSarlavha = lokal_postlar[indeks]?.title;
  if (indeks !== -1) lokal_postlar[indeks].title = yangiSarlavha;
  console.log("UI yangilandi (optimistik)");
  
  try {
    await api.patch("/posts", id, { title: yangiSarlavha });
    console.log("Server ham yangilandi ✅");
  } catch (e) {
    // Xato bo'lsa orqaga qaytarish
    if (indeks !== -1) lokal_postlar[indeks].title = eskilSarlavha;
    console.log("Xato, orqaga qaytarildi ❌");
    throw e;
  }
}
```
