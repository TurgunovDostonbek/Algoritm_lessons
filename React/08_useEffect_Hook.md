# 08-Dars: useEffect Hook

## 📌 useEffect nima?

**useEffect** — komponentdagi **yon ta'sirlar** (side effects) ni boshqarish uchun Hook.

```
Yon ta'sirlar (Side Effects):
├── API dan ma'lumot olish (fetch, axios)
├── localStorage ga yozish/o'qish
├── Taymerni o'rnatish (setInterval, setTimeout)
├── Hujjat sarlavhasini o'zgartirish (document.title)
├── Event listener qo'shish/olib tashlash
└── Obuna bo'lish va bekor qilish
```

---

## 📌 useEffect Sintaksisi

```jsx
import { useEffect } from 'react'

// Zamonaviy React (19+) da: React.use() ham mavjud, lekin asosiysi useEffect

useEffect(() => {
  // Yon ta'sir kodi shu yerda

  return () => {
    // Tozalash (cleanup) — ixtiyoriy
  }
}, [bog'liqlar])  // Dependency array (bog'liqlik massivi)
```

---

## 📌 Dependency Array — 3 holat

```jsx
// 1. [] — Faqat bir marta (mount bo'lganda)
useEffect(() => {
  console.log('Komponent birinchi marta yuklandi')
  fetchMaʼlumot()
}, [])

// 2. [qiymat] — qiymat o'zgarganda
useEffect(() => {
  console.log('Son o'zgardi:', son)
}, [son])

// 3. Yo'q (bo'sh) — Har bir renderda
useEffect(() => {
  console.log('Har safar render bo'lganda')
})  // ⚠️ Ehtiyot bo'ling! Cheksiz loop bo'lishi mumkin
```

---

## 📌 Tozalash Funksiyasi (Cleanup)

```jsx
// Event listener — qo'shish va olib tashlash
useEffect(() => {
  function klaviatura(e) {
    if (e.key === 'Escape') setModal(false)
  }

  window.addEventListener('keydown', klaviatura)

  return () => {
    window.removeEventListener('keydown', klaviatura)  // Tozalash!
  }
}, [])

// Taymer — o'rnatish va o'chirish
useEffect(() => {
  const interval = setInterval(() => {
    setVaqt(prev => prev + 1)
  }, 1000)

  return () => clearInterval(interval)  // Tozalash!
}, [])
```

---

## 📌 Functional Component Life-Cycle

```
Mount (Birinchi render):
  1. Komponent render qilinadi
  2. DOM ga qo'shiladi
  3. useEffect(() => {...}, []) ishlaydi  ← Mount

Update (Yangilanish):
  1. State/Props o'zgardi
  2. Komponent qayta render qilinadi
  3. useEffect(() => {...}, [son]) ishlaydi  ← Update

Unmount (O'chirilish):
  1. Komponent DOMdan olib tashlanadi
  2. useEffect cleanup funksiyasi ishlaydi  ← Cleanup
```

---

## 📌 LocalStorage + useEffect

```jsx
import { useState, useEffect } from 'react'

function App() {
  const [ism, setIsm] = useState(() => {
    // Boshlang'ich qiymat localStorage dan
    return localStorage.getItem('ism') || ''
  })

  // Ism o'zgarganda localStorage ga saqlash
  useEffect(() => {
    localStorage.setItem('ism', ism)
  }, [ism])

  return <input value={ism} onChange={e => setIsm(e.target.value)} />
}
```

---

## 🎯 10 ta Amaliy Vazifa — Fetch bilan Ishlash

```jsx
// src/App.jsx
import { useState, useEffect } from 'react'

// ============================================
// Vazifa 1-2: document.title + Taymer
// ============================================
function Saat() {
  const [vaqt, setVaqt] = useState(new Date())
  const [isRunning, setIsRunning] = useState(true)

  // Vazifa 1: setInterval bilan vaqt yangilanishi
  useEffect(() => {
    if (!isRunning) return

    const interval = setInterval(() => {
      setVaqt(new Date())
    }, 1000)

    return () => clearInterval(interval)  // Cleanup!
  }, [isRunning])

  // Vazifa 2: document.title ga vaqt yozish
  useEffect(() => {
    document.title = `⏰ ${vaqt.toLocaleTimeString('uz-UZ')}`
    return () => { document.title = 'React App' }
  }, [vaqt])

  const soat = vaqt.getHours().toString().padStart(2, '0')
  const daqiqa = vaqt.getMinutes().toString().padStart(2, '0')
  const soniya = vaqt.getSeconds().toString().padStart(2, '0')

  return (
    <div style={{ background: '#1a1a2e', borderRadius: '20px', padding: '32px', textAlign: 'center', marginBottom: '24px' }}>
      <p style={{ color: 'rgba(255,255,255,0.5)', fontSize: '12px', textTransform: 'uppercase', letterSpacing: '2px', marginBottom: '8px' }}>
        {vaqt.toLocaleDateString('uz-UZ', { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' })}
      </p>
      <div style={{ display: 'flex', gap: '8px', justifyContent: 'center', alignItems: 'center', marginBottom: '20px' }}>
        {[soat, ':', daqiqa, ':', soniya].map((q, i) => (
          <span key={i} style={{
            ...(q === ':' ? { color: 'rgba(255,255,255,0.4)', fontSize: '32px' } : {
              background: 'rgba(255,255,255,0.08)', color: 'white', padding: '12px 16px',
              borderRadius: '10px', fontSize: '36px', fontWeight: '900', minWidth: '60px',
              display: 'inline-block', textAlign: 'center', letterSpacing: '-1px'
            })
          }}>
            {q}
          </span>
        ))}
      </div>
      <button onClick={() => setIsRunning(!isRunning)} style={{
        background: isRunning ? '#fee2e2' : '#d1fae5', color: isRunning ? '#e63946' : '#10b981',
        border: 'none', padding: '8px 20px', borderRadius: '8px', fontWeight: '700', cursor: 'pointer'
      }}>
        {isRunning ? '⏸ Pauza' : '▶ Davom'}
      </button>
    </div>
  )
}

// ============================================
// Vazifa 3-6: Fetch bilan ma'lumot olish
// ============================================
function FoydalanuvchiRoyhat() {
  const [foydalanuvchilar, setFoydalanuvchilar] = useState([])
  const [yuklanyapti, setYuklanyapti] = useState(true)
  const [xato, setXato] = useState(null)
  const [qidiruv, setQidiruv] = useState('')
  const [tanlangan, setTanlangan] = useState(null)

  // Vazifa 3: Ma'lumot olish (mount da)
  useEffect(() => {
    setYuklanyapti(true)
    fetch('https://jsonplaceholder.typicode.com/users')
      .then(res => {
        if (!res.ok) throw new Error('Server xatosi!')
        return res.json()
      })
      .then(data => setFoydalanuvchilar(data))
      .catch(err => setXato(err.message))
      .finally(() => setYuklanyapti(false))
  }, [])

  // Vazifa 4: Tanlanganda batafsil ma'lumot
  useEffect(() => {
    if (!tanlangan) return
    document.title = `👤 ${tanlangan.name}`
    return () => { document.title = 'React App' }
  }, [tanlangan])

  // Filterlash
  const filterlangan = foydalanuvchilar.filter(f =>
    f.name.toLowerCase().includes(qidiruv.toLowerCase()) ||
    f.email.toLowerCase().includes(qidiruv.toLowerCase())
  )

  if (yuklanyapti) return (
    <div style={{ background: 'white', borderRadius: '16px', padding: '40px', textAlign: 'center', marginBottom: '24px' }}>
      <div style={{ fontSize: '32px', marginBottom: '12px' }}>⏳</div>
      <p>Ma'lumot yuklanmoqda...</p>
    </div>
  )

  if (xato) return (
    <div style={{ background: '#fee2e2', color: '#991b1b', borderRadius: '16px', padding: '20px', marginBottom: '24px' }}>
      ❌ Xato: {xato}
    </div>
  )

  return (
    <div style={{ background: 'white', borderRadius: '16px', overflow: 'hidden', boxShadow: '0 4px 20px rgba(0,0,0,0.08)', marginBottom: '24px' }}>
      <div style={{ padding: '20px', borderBottom: '1px solid #f0f0f0' }}>
        <h2 style={{ marginBottom: '12px' }}>👥 Foydalanuvchilar ({filterlangan.length})</h2>
        {/* Vazifa 5: Qidiruv — useEffect bilan emas, filter bilan */}
        <input value={qidiruv} onChange={e => setQidiruv(e.target.value)}
          placeholder="Ism yoki email qidiring..."
          style={{ width: '100%', padding: '10px 14px', border: '2px solid #e5e7eb', borderRadius: '8px', fontSize: '14px', outline: 'none', boxSizing: 'border-box' }} />
      </div>

      <div style={{ display: 'grid', gridTemplateColumns: '1fr 1fr' }}>
        {/* Ro'yxat */}
        <div style={{ borderRight: '1px solid #f0f0f0', maxHeight: '400px', overflowY: 'auto' }}>
          {filterlangan.map((user) => (
            <div key={user.id} onClick={() => setTanlangan(user)}
              style={{
                padding: '14px 16px', cursor: 'pointer', borderBottom: '1px solid #f8f8f8',
                background: tanlangan?.id === user.id ? '#f0f4ff' : 'transparent',
                borderLeft: tanlangan?.id === user.id ? '3px solid royalblue' : '3px solid transparent',
                transition: 'all 0.15s'
              }}>
              <div style={{ display: 'flex', alignItems: 'center', gap: '10px' }}>
                <div style={{
                  width: '36px', height: '36px', borderRadius: '50%', flexShrink: 0,
                  background: `hsl(${user.id * 36}, 70%, 60%)`, color: 'white',
                  display: 'flex', alignItems: 'center', justifyContent: 'center', fontWeight: '700', fontSize: '14px'
                }}>
                  {user.name.charAt(0)}
                </div>
                <div>
                  <div style={{ fontWeight: '600', fontSize: '14px' }}>{user.name}</div>
                  <div style={{ fontSize: '12px', color: '#888' }}>{user.email}</div>
                </div>
              </div>
            </div>
          ))}
        </div>

        {/* Batafsil */}
        <div style={{ padding: '20px' }}>
          {tanlangan ? (
            <>
              <div style={{ width: '56px', height: '56px', borderRadius: '50%', background: `hsl(${tanlangan.id * 36}, 70%, 60%)`, color: 'white', display: 'flex', alignItems: 'center', justifyContent: 'center', fontWeight: '800', fontSize: '22px', marginBottom: '14px' }}>
                {tanlangan.name.charAt(0)}
              </div>
              <h3 style={{ marginBottom: '4px' }}>{tanlangan.name}</h3>
              <p style={{ color: '#888', fontSize: '13px', marginBottom: '14px' }}>@{tanlangan.username}</p>
              {[
                ['📧', tanlangan.email],
                ['📞', tanlangan.phone],
                ['🌐', tanlangan.website],
                ['🏢', tanlangan.company?.name],
                ['📍', `${tanlangan.address?.city}, ${tanlangan.address?.street}`],
              ].map(([belgi, qiymat]) => (
                <div key={belgi} style={{ display: 'flex', gap: '8px', fontSize: '13px', marginBottom: '6px', color: '#555' }}>
                  <span>{belgi}</span>
                  <span>{qiymat}</span>
                </div>
              ))}
            </>
          ) : (
            <div style={{ height: '100%', display: 'flex', alignItems: 'center', justifyContent: 'center', color: '#aaa', fontSize: '14px', textAlign: 'center', flexDirection: 'column', gap: '8px' }}>
              <span style={{ fontSize: '32px' }}>👈</span>
              Foydalanuvchini tanlang
            </div>
          )}
        </div>
      </div>
    </div>
  )
}

// ============================================
// Vazifa 7-8: localStorage + useEffect
// ============================================
function LocalStorageMisol() {
  const [tugmalar_hisobi, setHisob] = useState(() =>
    Number(localStorage.getItem('bosishlar') || 0)
  )
  const [tema, setTema] = useState(() =>
    localStorage.getItem('tema') || 'kunduz'
  )

  useEffect(() => {
    localStorage.setItem('bosishlar', tugmalar_hisobi)
  }, [tugmalar_hisobi])

  useEffect(() => {
    localStorage.setItem('tema', tema)
  }, [tema])

  return (
    <div style={{
      background: tema === 'kecha' ? '#1a1a2e' : 'white',
      color: tema === 'kecha' ? 'white' : '#1a1a2e',
      borderRadius: '16px', padding: '24px', marginBottom: '24px',
      boxShadow: '0 4px 20px rgba(0,0,0,0.08)', transition: 'all 0.3s'
    }}>
      <div style={{ display: 'flex', justifyContent: 'space-between', alignItems: 'center', marginBottom: '16px' }}>
        <h2>💾 LocalStorage (useEffect)</h2>
        <button onClick={() => setTema(t => t === 'kecha' ? 'kunduz' : 'kecha')}
          style={{ background: tema === 'kecha' ? '#f59e0b' : '#1a1a2e', color: 'white', border: 'none', padding: '8px 14px', borderRadius: '8px', cursor: 'pointer', fontWeight: '700' }}>
          {tema === 'kecha' ? '☀️' : '🌙'}
        </button>
      </div>
      <p style={{ opacity: 0.7, fontSize: '14px', marginBottom: '16px' }}>
        Sahifani yangilang — ma'lumotlar saqlanadi!
      </p>
      <div style={{ textAlign: 'center' }}>
        <div style={{ fontSize: '48px', fontWeight: '900', color: 'royalblue', marginBottom: '12px' }}>
          {tugmalar_hisobi}
        </div>
        <p style={{ opacity: 0.6, fontSize: '13px', marginBottom: '12px' }}>Jami bosishlar (localStorage ga saqlangan)</p>
        <div style={{ display: 'flex', gap: '8px', justifyContent: 'center' }}>
          <button onClick={() => setHisob(h => h + 1)} style={{ background: 'royalblue', color: 'white', border: 'none', padding: '10px 20px', borderRadius: '8px', cursor: 'pointer', fontWeight: '700' }}>+1</button>
          <button onClick={() => setHisob(0)} style={{ background: '#f3f4f6', color: '#555', border: 'none', padding: '10px 20px', borderRadius: '8px', cursor: 'pointer', fontWeight: '700' }}>Reset</button>
        </div>
      </div>
    </div>
  )
}

// ============================================
// Vazifa 9-10: Scroll position + resize
// ============================================
function ScrollEffect() {
  const [scrollY, setScrollY] = useState(0)
  const [ekranKenglik, setEkranKenglik] = useState(window.innerWidth)

  // Vazifa 9: Scroll event listener
  useEffect(() => {
    function scrollHandler() { setScrollY(window.scrollY) }
    window.addEventListener('scroll', scrollHandler)
    return () => window.removeEventListener('scroll', scrollHandler)
  }, [])

  // Vazifa 10: Resize event listener
  useEffect(() => {
    function resizeHandler() { setEkranKenglik(window.innerWidth) }
    window.addEventListener('resize', resizeHandler)
    return () => window.removeEventListener('resize', resizeHandler)
  }, [])

  return (
    <div style={{ background: 'white', borderRadius: '16px', padding: '24px', boxShadow: '0 4px 20px rgba(0,0,0,0.08)' }}>
      <h2 style={{ marginBottom: '16px' }}>📊 Window Events (useEffect)</h2>
      <div style={{ display: 'grid', gridTemplateColumns: '1fr 1fr', gap: '12px' }}>
        <div style={{ background: '#f0f4ff', borderRadius: '12px', padding: '16px', textAlign: 'center' }}>
          <div style={{ fontSize: '28px', fontWeight: '800', color: 'royalblue' }}>{scrollY}px</div>
          <div style={{ fontSize: '12px', color: '#888', marginTop: '4px' }}>📜 Scroll Y</div>
        </div>
        <div style={{ background: '#f0fdf4', borderRadius: '12px', padding: '16px', textAlign: 'center' }}>
          <div style={{ fontSize: '28px', fontWeight: '800', color: '#10b981' }}>{ekranKenglik}px</div>
          <div style={{ fontSize: '12px', color: '#888', marginTop: '4px' }}>📐 Ekran kengligi</div>
        </div>
      </div>
      <p style={{ fontSize: '13px', color: '#888', marginTop: '12px', textAlign: 'center' }}>
        Sahifani aylantiring yoki ekranni o'zgartiring
      </p>
    </div>
  )
}

function App() {
  return (
    <div style={{ minHeight: '100vh', background: '#f0f2f5', padding: '40px 20px', fontFamily: "'Segoe UI', sans-serif" }}>
      <div style={{ maxWidth: '700px', margin: '0 auto' }}>
        <h1 style={{ textAlign: 'center', marginBottom: '32px' }}>⚡ useEffect Hook Amaliyoti</h1>
        <Saat />
        <FoydalanuvchiRoyhat />
        <LocalStorageMisol />
        <ScrollEffect />
      </div>
    </div>
  )
}
export default App
```
