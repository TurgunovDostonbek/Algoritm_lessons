# 10-Dars: Axios

## 📌 Axios nima?

**Axios** — HTTP so'rovlar uchun mashhur JavaScript kutubxonasi. Fetch ga qaraganda ko'proq imkoniyatlar beradi.

```bash
# O'rnatish:
npm install axios
```

```javascript
// Fetch vs Axios farqi:

// --- FETCH ---
const res = await fetch('/api/users')
if (!res.ok) throw new Error('Xato!')       // Qo'lda tekshirish
const data = await res.json()                // Qo'lda JSON'ga aylantirish

// --- AXIOS ---
const { data } = await axios.get('/api/users')  // Avtomatik JSON!
// 4xx, 5xx — avtomatik throw Error
```

---

## 📌 Axios vs Fetch — Asosiy Farqlar

| Xususiyat | Fetch | Axios |
|-----------|-------|-------|
| O'rnatish | O'rnatish shart emas | `npm install axios` |
| JSON | `res.json()` kerak | Avtomatik |
| Xato | Faqat network xato | 4xx, 5xx ham xato |
| Timeout | Qo'lda | `timeout: 5000` |
| Interceptors | Yo'q | ✅ Mavjud |
| So'rov bekor qilish | AbortController | `CancelToken` |
| Progress | Yo'q | ✅ `onUploadProgress` |
| XSRF Himoya | Yo'q | ✅ Mavjud |

---

## 📌 Axios — Asosiy Metodlar

```javascript
import axios from 'axios'

// GET
const { data } = await axios.get('/api/users')
const { data } = await axios.get('/api/users', { params: { page: 1, limit: 10 } })

// POST
const { data } = await axios.post('/api/users', { ism: 'Ali', yosh: 22 })

// PUT
const { data } = await axios.put('/api/users/1', { ism: 'Ali', yosh: 23 })

// PATCH
const { data } = await axios.patch('/api/users/1', { yosh: 23 })

// DELETE
await axios.delete('/api/users/1')
```

---

## 📌 Axios Instance (Konfiguratsiya)

```javascript
// src/api/axiosInstance.js
import axios from 'axios'

// Asosiy konfiguratsiya
const api = axios.create({
  baseURL: 'https://dummyjson.com',  // Asosiy URL
  timeout: 10000,                     // 10 soniya
  headers: {
    'Content-Type': 'application/json',
  },
})

// Request Interceptor (So'rov oldidan)
api.interceptors.request.use(
  (config) => {
    const token = localStorage.getItem('token')
    if (token) {
      config.headers.Authorization = `Bearer ${token}`
    }
    return config
  },
  (error) => Promise.reject(error)
)

// Response Interceptor (Javob kelganda)
api.interceptors.response.use(
  (response) => response,
  (error) => {
    if (error.response?.status === 401) {
      localStorage.removeItem('token')
      window.location.href = '/login'
    }
    return Promise.reject(error)
  }
)

export default api
```

---

## 📌 Axios bilan CRUD

```javascript
import api from './api/axiosInstance'

// GET — Mahsulotlar
export const mahsulotlarniOl = async (limit = 12, skip = 0) => {
  const { data } = await api.get('/products', { params: { limit, skip } })
  return data
}

// POST — Yangi mahsulot
export const mahsulotQo'sh = async (mahsulot) => {
  const { data } = await api.post('/products/add', mahsulot)
  return data
}

// PATCH — Yangilash
export const mahsulotYangilash = async (id, o'zgarish) => {
  const { data } = await api.patch(`/products/${id}`, o'zgarish)
  return data
}

// DELETE — O'chirish
export const mahsulotOchirish = async (id) => {
  const { data } = await api.delete(`/products/${id}`)
  return data
}
```

---

## 📌 Xato Boshqaruvi

```javascript
try {
  const { data } = await axios.get('/api/users')
} catch (error) {
  if (error.response) {
    // Server javob berdi, lekin xato status
    console.log(error.response.status)   // 404, 500...
    console.log(error.response.data)     // Server xabar berdi
  } else if (error.request) {
    // So'rov yuborildi, lekin javob kelmadi (internet yo'q)
    console.log('Internet aloqasi yo'q!')
  } else {
    // Boshqa xato
    console.log('Xato:', error.message)
  }
}
```

---

## 🎯 10 ta Amaliy Vazifa — Axios bilan E-commerce Ilovasini Qilib Kelish

```jsx
// npm install axios — kerak!

// src/api/axiosConfig.js
import axios from 'axios'
const api = axios.create({ baseURL: 'https://dummyjson.com', timeout: 10000 })
api.interceptors.response.use(r => r, err => {
  const msg = err.response?.data?.message || err.message || 'Noma\'lum xato'
  return Promise.reject(new Error(msg))
})
export default api
```

```jsx
// src/App.jsx — E-commerce Savatcha
import axios from 'axios'
import { useState, useEffect, useCallback } from 'react'

const api = axios.create({ baseURL: 'https://dummyjson.com', timeout: 10000 })

// ============================================
// Vazifa 1-2: Axios GET — Mahsulotlar olish
// ============================================
async function kategoriyaliMahsulotlar(kategoriya, limit = 8) {
  const url = kategoriya === 'hammasi'
    ? `/products?limit=${limit}`
    : `/products/category/${kategoriya}?limit=${limit}`
  const { data } = await api.get(url)
  return data.products || data
}

async function kategoriyalarniOl() {
  const { data } = await api.get('/products/categories')
  return data
}

// ============================================
// Savatcha
// ============================================
function useSavatcha() {
  const [savatcha, setSavatcha] = useState([])

  const qo'sh = useCallback((mahsulot) => {
    setSavatcha(prev => {
      const bor = prev.find(s => s.id === mahsulot.id)
      if (bor) return prev.map(s => s.id === mahsulot.id ? { ...s, soni: s.soni + 1 } : s)
      return [...prev, { ...mahsulot, soni: 1 }]
    })
  }, [])

  const ochir = useCallback((id) => {
    setSavatcha(prev => prev.filter(s => s.id !== id))
  }, [])

  const soniO'zgartir = useCallback((id, yangiSon) => {
    if (yangiSon < 1) return ochir(id)
    setSavatcha(prev => prev.map(s => s.id === id ? { ...s, soni: yangiSon } : s))
  }, [ochir])

  const jami = savatcha.reduce((sum, s) => sum + s.price * s.soni, 0)
  const sonJami = savatcha.reduce((sum, s) => sum + s.soni, 0)

  return { savatcha, qo'sh, ochir, soniO'zgartir, jami, sonJami }
}

// ============================================
// Mahsulot Kartasi
// ============================================
function MahsulotKarta({ mahsulot, onSavatchaQo'sh }) {
  const [qo'shildi, setQo'shildi] = useState(false)

  function handleQo'sh() {
    onSavatchaQo'sh(mahsulot)
    setQo'shildi(true)
    setTimeout(() => setQo'shildi(false), 1500)
  }

  return (
    <div style={{ background: 'white', borderRadius: '16px', overflow: 'hidden', boxShadow: '0 4px 20px rgba(0,0,0,0.07)', display: 'flex', flexDirection: 'column', transition: 'transform 0.2s' }}
      onMouseEnter={e => e.currentTarget.style.transform = 'translateY(-4px)'}
      onMouseLeave={e => e.currentTarget.style.transform = 'translateY(0)'}
    >
      <div style={{ position: 'relative' }}>
        <img src={mahsulot.thumbnail} alt={mahsulot.title} loading="lazy"
          style={{ width: '100%', height: '170px', objectFit: 'cover', display: 'block' }} />
        <span style={{ position: 'absolute', top: '8px', left: '8px', background: '#e63946', color: 'white', padding: '3px 8px', borderRadius: '20px', fontSize: '11px', fontWeight: '700' }}>
          -{mahsulot.discountPercentage?.toFixed(0)}%
        </span>
      </div>
      <div style={{ padding: '14px', flex: 1, display: 'flex', flexDirection: 'column' }}>
        <p style={{ fontSize: '11px', color: '#888', marginBottom: '4px', textTransform: 'capitalize' }}>{mahsulot.category}</p>
        <h3 style={{ fontSize: '14px', lineHeight: 1.4, marginBottom: '8px', flex: 1 }}>{mahsulot.title}</h3>
        <div style={{ display: 'flex', alignItems: 'center', gap: '6px', marginBottom: '10px' }}>
          <span style={{ fontWeight: '800', fontSize: '18px', color: 'royalblue' }}>${mahsulot.price}</span>
          <span style={{ fontSize: '12px', color: '#aaa', textDecoration: 'line-through' }}>
            ${(mahsulot.price / (1 - mahsulot.discountPercentage / 100)).toFixed(0)}
          </span>
          <span style={{ marginLeft: 'auto', fontSize: '12px', color: '#f59e0b' }}>⭐ {mahsulot.rating}</span>
        </div>
        <button onClick={handleQo'sh} style={{
          background: qo'shildi ? '#d1fae5' : 'royalblue',
          color: qo'shildi ? '#10b981' : 'white',
          border: 'none', padding: '10px', borderRadius: '10px', fontWeight: '700',
          cursor: 'pointer', fontSize: '13px', transition: 'all 0.2s'
        }}>
          {qo'shildi ? '✅ Qo\'shildi!' : '🛒 Savatchaga'}
        </button>
      </div>
    </div>
  )
}

// ============================================
// Savatcha Modal
// ============================================
function SavatchaModal({ savatcha, ochir, soniO'zgartir, jami, onYopish }) {
  return (
    <div style={{ position: 'fixed', inset: 0, background: 'rgba(0,0,0,0.5)', zIndex: 999, display: 'flex', justifyContent: 'flex-end' }}
      onClick={e => e.target === e.currentTarget && onYopish()}>
      <div style={{ background: 'white', width: '400px', maxWidth: '100%', height: '100vh', display: 'flex', flexDirection: 'column', animation: 'slideRight 0.3s ease' }}>
        <div style={{ padding: '20px 24px', borderBottom: '1px solid #f0f0f0', display: 'flex', justifyContent: 'space-between', alignItems: 'center' }}>
          <h2>🛒 Savatcha ({savatcha.length} xil)</h2>
          <button onClick={onYopish} style={{ background: '#f3f4f6', border: 'none', width: '32px', height: '32px', borderRadius: '50%', cursor: 'pointer', fontSize: '16px' }}>×</button>
        </div>

        <div style={{ flex: 1, overflowY: 'auto', padding: '16px 24px' }}>
          {savatcha.length === 0 ? (
            <div style={{ textAlign: 'center', padding: '60px 0', color: '#aaa' }}>
              <div style={{ fontSize: '48px', marginBottom: '12px' }}>🛒</div>
              <p>Savatcha bo'sh</p>
            </div>
          ) : savatcha.map(item => (
            <div key={item.id} style={{ display: 'flex', gap: '12px', padding: '12px 0', borderBottom: '1px solid #f8f8f8' }}>
              <img src={item.thumbnail} alt={item.title} style={{ width: '64px', height: '64px', objectFit: 'cover', borderRadius: '10px', flexShrink: 0 }} />
              <div style={{ flex: 1 }}>
                <p style={{ fontSize: '13px', fontWeight: '600', marginBottom: '4px', lineHeight: 1.3 }}>{item.title}</p>
                <p style={{ fontSize: '14px', fontWeight: '800', color: 'royalblue', marginBottom: '8px' }}>${item.price}</p>
                <div style={{ display: 'flex', alignItems: 'center', gap: '8px' }}>
                  <button onClick={() => soniO'zgartir(item.id, item.soni - 1)} style={{ width: '26px', height: '26px', border: '1px solid #e5e7eb', background: 'white', borderRadius: '6px', cursor: 'pointer', fontSize: '16px', display: 'flex', alignItems: 'center', justifyContent: 'center' }}>−</button>
                  <span style={{ fontWeight: '700', minWidth: '20px', textAlign: 'center' }}>{item.soni}</span>
                  <button onClick={() => soniO'zgartir(item.id, item.soni + 1)} style={{ width: '26px', height: '26px', border: '1px solid #e5e7eb', background: 'white', borderRadius: '6px', cursor: 'pointer', fontSize: '16px', display: 'flex', alignItems: 'center', justifyContent: 'center' }}>+</button>
                </div>
              </div>
              <div style={{ display: 'flex', flexDirection: 'column', alignItems: 'flex-end', justifyContent: 'space-between' }}>
                <span style={{ fontWeight: '800', fontSize: '15px' }}>${(item.price * item.soni).toFixed(2)}</span>
                <button onClick={() => ochir(item.id)} style={{ color: '#e63946', background: 'none', border: 'none', cursor: 'pointer', fontSize: '12px' }}>O'chir</button>
              </div>
            </div>
          ))}
        </div>

        {savatcha.length > 0 && (
          <div style={{ padding: '20px 24px', borderTop: '1px solid #f0f0f0' }}>
            <div style={{ display: 'flex', justifyContent: 'space-between', marginBottom: '14px' }}>
              <span style={{ fontWeight: '700' }}>Jami:</span>
              <span style={{ fontWeight: '900', fontSize: '22px', color: 'royalblue' }}>${jami.toFixed(2)}</span>
            </div>
            <button onClick={() => alert('Buyurtma berildi! 🎉')} style={{ width: '100%', background: 'royalblue', color: 'white', border: 'none', padding: '14px', borderRadius: '12px', fontWeight: '800', fontSize: '16px', cursor: 'pointer' }}>
              Buyurtma berish →
            </button>
          </div>
        )}
      </div>
    </div>
  )
}

// ============================================
// Asosiy App
// ============================================
function App() {
  const [mahsulotlar, setMahsulotlar] = useState([])
  const [kategoriyalar, setKategoriyalar] = useState([])
  const [tanlangan, setTanlangan] = useState('hammasi')
  const [yuklanyapti, setYuklanyapti] = useState(true)
  const [xato, setXato] = useState(null)
  const [savatchaOchiq, setSavatchaOchiq] = useState(false)

  const { savatcha, qo'sh, ochir, soniO'zgartir, jami, sonJami } = useSavatcha()

  // Kategoriyalar
  useEffect(() => {
    kategoriyalarniOl()
      .then(k => {
        const sluglar = k.slice(0, 6).map(kat => typeof kat === 'string' ? kat : kat.slug)
        setKategoriyalar(['hammasi', ...sluglar])
      })
      .catch(console.error)
  }, [])

  // Mahsulotlar
  useEffect(() => {
    setYuklanyapti(true)
    setXato(null)
    kategoriyaliMahsulotlar(tanlangan)
      .then(setMahsulotlar)
      .catch(err => setXato(err.message))
      .finally(() => setYuklanyapti(false))
  }, [tanlangan])

  return (
    <div style={{ minHeight: '100vh', background: '#f8f9fa', fontFamily: "'Segoe UI', sans-serif" }}>
      <style>{`@keyframes slideRight { from{transform:translateX(100%)} to{transform:translateX(0)} }`}</style>

      {/* Header */}
      <header style={{ background: '#1a1a2e', color: 'white', padding: '0 40px', position: 'sticky', top: 0, zIndex: 100 }}>
        <div style={{ maxWidth: '1100px', margin: '0 auto', height: '64px', display: 'flex', alignItems: 'center', justifyContent: 'space-between' }}>
          <div>
            <h1 style={{ fontSize: '20px', fontWeight: '800' }}>⚡ AxiosShop</h1>
            <p style={{ fontSize: '11px', opacity: 0.5 }}>Axios bilan CRUD</p>
          </div>
          <button onClick={() => setSavatchaOchiq(true)} style={{ position: 'relative', background: 'royalblue', color: 'white', border: 'none', padding: '10px 18px', borderRadius: '10px', cursor: 'pointer', fontWeight: '700', display: 'flex', alignItems: 'center', gap: '8px' }}>
            🛒 Savatcha
            {sonJami > 0 && (
              <span style={{ position: 'absolute', top: '-8px', right: '-8px', background: '#e63946', color: 'white', width: '22px', height: '22px', borderRadius: '50%', display: 'flex', alignItems: 'center', justifyContent: 'center', fontSize: '12px', fontWeight: '800' }}>
                {sonJami}
              </span>
            )}
          </button>
        </div>
      </header>

      <div style={{ maxWidth: '1100px', margin: '0 auto', padding: '32px 20px' }}>

        {/* Kategoriyalar */}
        <div style={{ display: 'flex', gap: '8px', flexWrap: 'wrap', marginBottom: '28px' }}>
          {kategoriyalar.map(k => (
            <button key={k} onClick={() => setTanlangan(k)} style={{
              padding: '8px 18px', borderRadius: '20px', border: '2px solid', cursor: 'pointer', fontWeight: '700', fontSize: '13px',
              borderColor: tanlangan === k ? 'royalblue' : '#e5e7eb',
              background: tanlangan === k ? 'royalblue' : 'white',
              color: tanlangan === k ? 'white' : '#555',
              textTransform: 'capitalize'
            }}>
              {k === 'hammasi' ? '✨ Hammasi' : k}
            </button>
          ))}
        </div>

        {xato && (
          <div style={{ background: '#fee2e2', color: '#991b1b', padding: '16px', borderRadius: '12px', marginBottom: '20px' }}>❌ {xato}</div>
        )}

        <div style={{ display: 'grid', gridTemplateColumns: 'repeat(auto-fill, minmax(230px, 1fr))', gap: '20px' }}>
          {yuklanyapti
            ? Array(8).fill(0).map((_, i) => (
                <div key={i} style={{ background: 'white', borderRadius: '16px', overflow: 'hidden', boxShadow: '0 4px 20px rgba(0,0,0,0.06)' }}>
                  <div style={{ height: '170px', background: 'linear-gradient(90deg, #f0f0f0 25%, #e8e8e8 50%, #f0f0f0 75%)', backgroundSize: '200% 100%' }} />
                  <div style={{ padding: '14px' }}>
                    {[80, 60, 40].map(w => <div key={w} style={{ height: '12px', background: '#f0f0f0', borderRadius: '4px', marginBottom: '8px', width: `${w}%` }} />)}
                  </div>
                </div>
              ))
            : mahsulotlar.map(m => <MahsulotKarta key={m.id} mahsulot={m} onSavatchaQo'sh={qo'sh} />)
          }
        </div>
      </div>

      {savatchaOchiq && (
        <SavatchaModal savatcha={savatcha} ochir={ochir} soniO'zgartir={soniO'zgartir} jami={jami} onYopish={() => setSavatchaOchiq(false)} />
      )}
    </div>
  )
}
export default App
```
