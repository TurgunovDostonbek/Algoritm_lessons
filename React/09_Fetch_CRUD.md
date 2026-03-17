# 09-Dars: Fetch va CRUD Metodlari

## 📌 Fetch API nima?

**Fetch API** — brauzerda o'rnatilgan, HTTP so'rovlarini yuborish uchun ishlatiladigan JavaScript funksiyasi.

```javascript
fetch(url, options)
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error(error))
```

---

## 📌 HTTP Metodlar (CRUD)

| Metod | CRUD | Maqsad | Body |
|-------|------|--------|------|
| `GET` | Read | Ma'lumot olish | ❌ |
| `POST` | Create | Yangi yaratish | ✅ |
| `PUT` | Update | To'liq yangilash | ✅ |
| `PATCH` | Update | Qisman yangilash | ✅ |
| `DELETE` | Delete | O'chirish | ❌ |

---

## 📌 GET — Ma'lumot Olish

```javascript
// Oddiy GET
fetch('https://jsonplaceholder.typicode.com/posts')
  .then(res => res.json())
  .then(data => console.log(data))

// Response to'liq ko'rish
fetch('https://jsonplaceholder.typicode.com/posts/1')
  .then(res => {
    console.log(res.status)  // 200, 404, 500...
    console.log(res.ok)      // true | false
    return res.json()
  })
  .then(post => console.log(post))
  .catch(err => console.error('Xato:', err))
```

---

## 📌 POST — Yangi Yaratish

```javascript
fetch('https://jsonplaceholder.typicode.com/posts', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    title: 'Mening Maqolam',
    body: 'Maqola matni...',
    userId: 1,
  }),
})
  .then(res => res.json())
  .then(yangiPost => console.log('Yaratildi:', yangiPost))
  .catch(err => console.error(err))
```

---

## 📌 PUT — To'liq Yangilash

```javascript
fetch('https://jsonplaceholder.typicode.com/posts/1', {
  method: 'PUT',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    id: 1,
    title: 'Yangilangan Maqola',
    body: 'Yangi matn',
    userId: 1,
  }),
})
  .then(res => res.json())
  .then(data => console.log('Yangilandi:', data))
```

---

## 📌 PATCH — Qisman Yangilash

```javascript
fetch('https://jsonplaceholder.typicode.com/posts/1', {
  method: 'PATCH',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ title: 'Yangi sarlavha' }),  // faqat sarlavha
})
  .then(res => res.json())
  .then(data => console.log('Qisman yangilandi:', data))
```

---

## 📌 DELETE — O'chirish

```javascript
fetch('https://jsonplaceholder.typicode.com/posts/1', {
  method: 'DELETE',
})
  .then(res => {
    if (res.ok) console.log("O'chirildi!")
    else console.error("Xato!")
  })
```

---

## 📌 Async/Await bilan (zamonaviy usul)

```javascript
// try-catch bilan
async function postlarniOl() {
  try {
    const res = await fetch('https://jsonplaceholder.typicode.com/posts')
    if (!res.ok) throw new Error(`Server xatosi: ${res.status}`)
    const postlar = await res.json()
    return postlar
  } catch (xato) {
    console.error('Xato:', xato.message)
    throw xato
  }
}

// React da:
async function yangiPostYarat(malumot) {
  const res = await fetch('https://jsonplaceholder.typicode.com/posts', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(malumot),
  })
  return await res.json()
}
```

---

## 📌 Try, Catch, Finally

```javascript
async function fetchMalumot() {
  try {
    // Bajarilishi mumkin bo'lgan kod
    const res = await fetch('/api/data')
    const data = await res.json()
    return data
  } catch (error) {
    // Xato bo'lsa
    console.error('Xato:', error)
  } finally {
    // Always (xato bo'lsa ham, bo'lmasa ham)
    setYuklanyapti(false)    // Har doim loading ni o'chiramiz
  }
}
```

---

## 📌 Response to'liq — `res` ob'ekti

```javascript
fetch('/api/malumot')
  .then(res => {
    // res.ok        — true (200-299) yoki false
    // res.status    — 200, 201, 400, 404, 500...
    // res.statusText— "OK", "Created", "Not Found"...
    // res.headers   — Javob sarlavhalari
    // res.url       — So'rov URL si

    return res.json()       // JSON o'qish (async!)
    // res.text()           // Matn sifatida
    // res.blob()           // Rasm/fayl uchun
    // res.arrayBuffer()    // Binary data
  })
```

---

## 🎯 10 ta Amaliy Vazifa — Dummy JSON bilan CRUD

```jsx
// src/App.jsx
// Dummy JSON API: https://dummyjson.com/products
import { useState, useEffect } from 'react'

const API = 'https://dummyjson.com'

// ============================================
// CRUD Funksiyalari
// ============================================
async function mahsulotlarniOl(cheklov = 8) {
  const res = await fetch(`${API}/products?limit=${cheklov}`)
  if (!res.ok) throw new Error('Serverdan ma\'lumot olishda xato!')
  const data = await res.json()
  return data.products
}

async function yangiMahsulotQosh(mahsulot) {
  const res = await fetch(`${API}/products/add`, {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(mahsulot),
  })
  if (!res.ok) throw new Error('Qo\'shishda xato!')
  return await res.json()
}

async function mahsulotYangilash(id, yangilangan) {
  const res = await fetch(`${API}/products/${id}`, {
    method: 'PATCH',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(yangilangan),
  })
  if (!res.ok) throw new Error('Yangilashda xato!')
  return await res.json()
}

async function mahsulotOchirish(id) {
  const res = await fetch(`${API}/products/${id}`, { method: 'DELETE' })
  if (!res.ok) throw new Error('O\'chirishda xato!')
  return await res.json()
}

// ============================================
// Yuklanish animatsiyasi
// ============================================
function LoadingKarta() {
  return (
    <div style={{ background: 'white', borderRadius: '16px', overflow: 'hidden', boxShadow: '0 4px 20px rgba(0,0,0,0.06)' }}>
      <div style={{ height: '180px', background: 'linear-gradient(90deg, #f0f0f0 25%, #e8e8e8 50%, #f0f0f0 75%)', backgroundSize: '200% 100%', animation: 'shimmer 1.5s infinite' }} />
      <div style={{ padding: '16px' }}>
        {[100, 70, 50].map((w) => (
          <div key={w} style={{ height: '14px', background: '#f0f0f0', borderRadius: '4px', marginBottom: '8px', width: `${w}%` }} />
        ))}
      </div>
    </div>
  )
}

// ============================================
// Mahsulot Kartasi
// ============================================
function MahsulotKarta({ mahsulot, onYangilash, onOchirish }) {
  const [tahrirMode, setTahrirMode] = useState(false)
  const [yangiNarx, setYangiNarx] = useState(mahsulot.price)
  const [yuklanyapti, setYuklanyapti] = useState(false)

  async function narxniSaqlash() {
    setYuklanyapti(true)
    try {
      const yangilangan = await mahsulotYangilash(mahsulot.id, { price: Number(yangiNarx) })
      onYangilash(mahsulot.id, { price: yangilangan.price })
      setTahrirMode(false)
    } catch (err) {
      alert('Yangilashda xato: ' + err.message)
    } finally {
      setYuklanyapti(false)
    }
  }

  async function ochirish() {
    if (!window.confirm(`"${mahsulot.title}"ni o'chirasizmi?`)) return
    setYuklanyapti(true)
    try {
      await mahsulotOchirish(mahsulot.id)
      onOchirish(mahsulot.id)
    } catch (err) {
      alert('O\'chirishda xato: ' + err.message)
      setYuklanyapti(false)
    }
  }

  return (
    <div style={{ background: 'white', borderRadius: '16px', overflow: 'hidden', boxShadow: '0 4px 20px rgba(0,0,0,0.07)', opacity: yuklanyapti ? 0.6 : 1, transition: 'all 0.2s', display: 'flex', flexDirection: 'column' }}>
      <div style={{ position: 'relative' }}>
        <img src={mahsulot.thumbnail} alt={mahsulot.title} loading="lazy"
          style={{ width: '100%', height: '160px', objectFit: 'cover', display: 'block' }} />
        <span style={{ position: 'absolute', top: '8px', left: '8px', background: 'rgba(0,0,0,0.6)', color: 'white', padding: '3px 8px', borderRadius: '6px', fontSize: '11px' }}>
          {mahsulot.category}
        </span>
        <span style={{ position: 'absolute', top: '8px', right: '8px', background: '#d1fae5', color: '#065f46', padding: '3px 8px', borderRadius: '6px', fontSize: '11px', fontWeight: '700' }}>
          ⭐ {mahsulot.rating}
        </span>
      </div>

      <div style={{ padding: '14px', flex: 1, display: 'flex', flexDirection: 'column' }}>
        <h3 style={{ fontSize: '14px', marginBottom: '8px', lineHeight: 1.4, flex: 1 }}>{mahsulot.title}</h3>

        {tahrirMode ? (
          <div style={{ display: 'flex', gap: '6px', marginBottom: '10px' }}>
            <input type="number" value={yangiNarx} onChange={e => setYangiNarx(e.target.value)}
              style={{ flex: 1, padding: '6px 10px', border: '2px solid royalblue', borderRadius: '6px', fontSize: '14px', outline: 'none' }} />
            <button onClick={narxniSaqlash} style={{ background: '#10b981', color: 'white', border: 'none', padding: '6px 12px', borderRadius: '6px', cursor: 'pointer', fontWeight: '700', fontSize: '12px' }}>✓</button>
            <button onClick={() => setTahrirMode(false)} style={{ background: '#f3f4f6', color: '#555', border: 'none', padding: '6px 10px', borderRadius: '6px', cursor: 'pointer', fontSize: '12px' }}>✗</button>
          </div>
        ) : (
          <div style={{ display: 'flex', justifyContent: 'space-between', alignItems: 'center', marginBottom: '10px' }}>
            <span style={{ fontWeight: '800', fontSize: '18px', color: 'royalblue' }}>${mahsulot.price}</span>
            <span style={{ fontSize: '12px', color: '#888' }}>{mahsulot.stock} ta qoldi</span>
          </div>
        )}

        <div style={{ display: 'flex', gap: '6px' }}>
          <button onClick={() => setTahrirMode(!tahrirMode)} disabled={yuklanyapti}
            style={{ flex: 1, background: '#f0f4ff', color: 'royalblue', border: 'none', padding: '8px', borderRadius: '8px', cursor: 'pointer', fontWeight: '700', fontSize: '12px' }}>
            ✏️ Tahrir
          </button>
          <button onClick={ochirish} disabled={yuklanyapti}
            style={{ flex: 1, background: '#fee2e2', color: '#e63946', border: 'none', padding: '8px', borderRadius: '8px', cursor: 'pointer', fontWeight: '700', fontSize: '12px' }}>
            🗑 O'chir
          </button>
        </div>
      </div>
    </div>
  )
}

// ============================================
// Qo'shish formasi
// ============================================
function QoshishForma({ onQo'shish }) {
  const [forma, setForma] = useState({ title: '', price: '', category: '' })
  const [yuklanyapti, setYuklanyapti] = useState(false)

  async function yuborish(e) {
    e.preventDefault()
    if (!forma.title || !forma.price) return
    setYuklanyapti(true)
    try {
      const yangi = await yangiMahsulotQosh({
        title: forma.title,
        price: Number(forma.price),
        category: forma.category || 'electronics',
        thumbnail: `https://picsum.photos/300/200?random=${Date.now()}`,
        rating: 4.5,
        stock: 10,
      })
      onQo'shish(yangi)
      setForma({ title: '', price: '', category: '' })
    } catch (err) {
      alert('Xato: ' + err.message)
    } finally {
      setYuklanyapti(false)
    }
  }

  return (
    <form onSubmit={yuborish} style={{ background: 'white', borderRadius: '16px', padding: '20px', marginBottom: '24px', boxShadow: '0 4px 20px rgba(0,0,0,0.06)' }}>
      <h2 style={{ marginBottom: '14px', fontSize: '17px' }}>➕ Yangi Mahsulot (POST)</h2>
      <div style={{ display: 'grid', gridTemplateColumns: '1fr 120px 1fr auto', gap: '10px', alignItems: 'end' }}>
        <div>
          <label style={{ fontSize: '12px', fontWeight: '700', display: 'block', marginBottom: '4px', color: '#555' }}>Nomi *</label>
          <input value={forma.title} onChange={e => setForma({...forma, title: e.target.value})} placeholder="Mahsulot nomi" required
            style={{ width: '100%', padding: '10px 12px', border: '2px solid #e5e7eb', borderRadius: '8px', fontSize: '14px', outline: 'none', boxSizing: 'border-box' }} />
        </div>
        <div>
          <label style={{ fontSize: '12px', fontWeight: '700', display: 'block', marginBottom: '4px', color: '#555' }}>Narx ($) *</label>
          <input type="number" value={forma.price} onChange={e => setForma({...forma, price: e.target.value})} placeholder="99" required min="0"
            style={{ width: '100%', padding: '10px 12px', border: '2px solid #e5e7eb', borderRadius: '8px', fontSize: '14px', outline: 'none', boxSizing: 'border-box' }} />
        </div>
        <div>
          <label style={{ fontSize: '12px', fontWeight: '700', display: 'block', marginBottom: '4px', color: '#555' }}>Kategoriya</label>
          <select value={forma.category} onChange={e => setForma({...forma, category: e.target.value})}
            style={{ width: '100%', padding: '10px 12px', border: '2px solid #e5e7eb', borderRadius: '8px', fontSize: '14px', outline: 'none', boxSizing: 'border-box' }}>
            <option value="electronics">Electronics</option>
            <option value="clothing">Clothing</option>
            <option value="furniture">Furniture</option>
            <option value="groceries">Groceries</option>
          </select>
        </div>
        <button type="submit" disabled={yuklanyapti || !forma.title || !forma.price}
          style={{ padding: '10px 16px', background: yuklanyapti ? '#e5e7eb' : 'royalblue', color: yuklanyapti ? '#9ca3af' : 'white', border: 'none', borderRadius: '8px', fontWeight: '700', cursor: yuklanyapti ? 'not-allowed' : 'pointer', whiteSpace: 'nowrap' }}>
          {yuklanyapti ? '...' : '+ Qo\'sh'}
        </button>
      </div>
    </form>
  )
}

// ============================================
// Asosiy App
// ============================================
function App() {
  const [mahsulotlar, setMahsulotlar] = useState([])
  const [yuklanyapti, setYuklanyapti] = useState(true)
  const [xato, setXato] = useState(null)
  const [xabar, setXabar] = useState(null)

  function xabarKo'rsat(matn, tur = 'muvaffaqiyat') {
    setXabar({ matn, tur })
    setTimeout(() => setXabar(null), 3000)
  }

  // GET — Birinchi yuklash
  useEffect(() => {
    mahsulotlarniOl(8)
      .then(data => setMahsulotlar(data))
      .catch(err => setXato(err.message))
      .finally(() => setYuklanyapti(false))
  }, [])

  function mahsulotQo'sh(yangi) {
    setMahsulotlar(prev => [yangi, ...prev])
    xabarKo'rsat(`"${yangi.title}" qo'shildi! ✅`)
  }

  function mahsulotYangilash_ui(id, o'zgarish) {
    setMahsulotlar(prev => prev.map(m => m.id === id ? { ...m, ...o'zgarish } : m))
    xabarKo'rsat('Narx yangilandi! ✏️')
  }

  function mahsulotOchir_ui(id) {
    setMahsulotlar(prev => prev.filter(m => m.id !== id))
    xabarKo'rsat('Mahsulot o\'chirildi! 🗑')
  }

  return (
    <div style={{ minHeight: '100vh', background: '#f0f2f5', fontFamily: "'Segoe UI', sans-serif" }}>
      <style>{`
        @keyframes shimmer { 0%{background-position:200% 0} 100%{background-position:-200% 0} }
        @keyframes slideIn { from{transform:translateY(-50px);opacity:0} to{transform:translateY(0);opacity:1} }
      `}</style>

      {/* Toast xabar */}
      {xabar && (
        <div style={{
          position: 'fixed', top: '20px', right: '20px', zIndex: 999,
          background: '#1a1a2e', color: 'white', padding: '14px 20px', borderRadius: '12px',
          boxShadow: '0 8px 32px rgba(0,0,0,0.2)', fontSize: '14px', fontWeight: '600',
          animation: 'slideIn 0.3s ease'
        }}>
          {xabar.matn}
        </div>
      )}

      {/* Header */}
      <header style={{ background: '#1a1a2e', color: 'white', padding: '24px 40px' }}>
        <h1>🛒 CRUD Admin Panel</h1>
        <p style={{ opacity: 0.7, fontSize: '14px', marginTop: '4px' }}>
          Fetch API: GET · POST · PATCH · DELETE
        </p>
      </header>

      <div style={{ maxWidth: '1100px', margin: '0 auto', padding: '32px 20px' }}>

        {/* POST forma */}
        <QoshishForma onQo'shish={mahsulotQo'sh} />

        {/* Statistika */}
        <div style={{ display: 'grid', gridTemplateColumns: 'repeat(3, 1fr)', gap: '16px', marginBottom: '24px' }}>
          {[
            { nom: 'Jami mahsulot', qiymat: mahsulotlar.length, belgi: '📦', rang: 'royalblue' },
            { nom: 'O\'rtacha narx', qiymat: `$${mahsulotlar.length ? Math.round(mahsulotlar.reduce((j,m)=>j+m.price,0)/mahsulotlar.length) : 0}`, belgi: '💰', rang: '#10b981' },
            { nom: 'Jami qiymat', qiymat: `$${mahsulotlar.reduce((j,m)=>j+m.price,0).toFixed(0)}`, belgi: '📊', rang: '#f59e0b' },
          ].map((s) => (
            <div key={s.nom} style={{ background: 'white', borderRadius: '14px', padding: '20px', boxShadow: '0 2px 12px rgba(0,0,0,0.06)', display: 'flex', alignItems: 'center', gap: '14px' }}>
              <div style={{ width: '48px', height: '48px', borderRadius: '12px', background: `${s.rang}20`, color: s.rang, display: 'flex', alignItems: 'center', justifyContent: 'center', fontSize: '22px' }}>{s.belgi}</div>
              <div><div style={{ fontSize: '22px', fontWeight: '800', color: s.rang }}>{s.qiymat}</div><div style={{ fontSize: '13px', color: '#888' }}>{s.nom}</div></div>
            </div>
          ))}
        </div>

        {/* Xato */}
        {xato && <div style={{ background: '#fee2e2', color: '#991b1b', padding: '16px', borderRadius: '12px', marginBottom: '20px' }}>❌ {xato}</div>}

        {/* Grid */}
        <div style={{ display: 'grid', gridTemplateColumns: 'repeat(auto-fill, minmax(240px, 1fr))', gap: '20px' }}>
          {yuklanyapti
            ? Array(8).fill(0).map((_, i) => <LoadingKarta key={i} />)
            : mahsulotlar.map(m => (
                <MahsulotKarta key={m.id} mahsulot={m} onYangilash={mahsulotYangilash_ui} onOchirish={mahsulotOchir_ui} />
              ))
          }
        </div>

      </div>
    </div>
  )
}
export default App
```
