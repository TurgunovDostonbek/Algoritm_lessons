# 06-Dars: useState Hook

## 📌 State nima?

**State** — komponent ichidagi o'zgaruvchan ma'lumot. State o'zgarganda React komponentni qayta renderlaydi.

```
Props  = Tashqaridan keladigan ma'lumot (O'ZGARMAYDI)
State  = Ichkaridan boshqariladigan ma'lumot (O'ZGARADI)
```

```jsx
// useState import qilish
import { useState } from 'react'

// Sintaksis:
const [qiymat, setQiymat] = useState(boshlanishQiymati)
//     ┌──┘    └────────┘            └───────────────┘
//     │       Yangilovchi funksiya  Boshlang'ich qiymat
//     O'qish uchun

// Misol:
const [son, setSon] = useState(0)
const [matn, setMatn] = useState('')
const [isVisible, setIsVisible] = useState(false)
const [massiv, setMassiv] = useState([])
const [obyekt, setObyekt] = useState({ ism: '', yosh: 0 })
```

---

## 📌 useState — Asosiy Ishlatish

```jsx
import { useState } from 'react'

function Hisoblagich() {
  const [son, setSon] = useState(0)

  return (
    <div>
      <h2>Son: {son}</h2>
      <button onClick={() => setSon(son + 1)}>+1</button>
      <button onClick={() => setSon(son - 1)}>-1</button>
      <button onClick={() => setSon(0)}>Reset</button>
    </div>
  )
}
```

---

## 📌 State Yangilash Qoidalari

```jsx
// ✅ TO'G'RI — setXxx funksiyasi orqali
setSon(son + 1)
setIsVisible(!isVisible)
setMatn('Yangi matn')

// ❌ XATO — to'g'ridan-to'g'ri o'zgartirish (React bilmaydi!)
son = son + 1          // XATO!
isVisible = true       // XATO!

// ✅ Oldingi qiymatdan foydalanish (eng to'g'ri usul)
setSon(oldingi => oldingi + 1)
setIsVisible(oldingi => !oldingi)
```

---

## 📌 Ob'ekt State

```jsx
import { useState } from 'react'

function Forma() {
  const [forma, setForma] = useState({
    ism: '',
    email: '',
    parol: ''
  })

  // Ob'ektni yangilash — spread operator bilan
  function o'zgartir(e) {
    setForma({
      ...forma,        // Oldingi barcha xususiyatlarni saqlash
      [e.target.name]: e.target.value   // Faqat o'zgarganini yangilash
    })
  }

  return (
    <form>
      <input name="ism" value={forma.ism} onChange={o'zgartir} />
      <input name="email" value={forma.email} onChange={o'zgartir} />
      <input name="parol" value={forma.parol} onChange={o'zgartir} />
      <p>Ism: {forma.ism}</p>
    </form>
  )
}
```

---

## 📌 Massiv State

```jsx
import { useState } from 'react'

function VazifaList() {
  const [vazifalar, setVazifalar] = useState([
    { id: 1, matn: 'HTML o\'rganish', bajarildi: true },
    { id: 2, matn: 'CSS o\'rganish', bajarildi: false },
  ])

  // Qo'shish
  function qo'shish(yangiMatn) {
    setVazifalar([
      ...vazifalar,
      { id: Date.now(), matn: yangiMatn, bajarildi: false }
    ])
  }

  // O'chirish
  function ochirish(id) {
    setVazifalar(vazifalar.filter(v => v.id !== id))
  }

  // Yangilash
  function bajarildiToggle(id) {
    setVazifalar(vazifalar.map(v =>
      v.id === id ? { ...v, bajarildi: !v.bajarildi } : v
    ))
  }
}
```

---

## 🎯 10 ta Amaliy Vazifa — Counter yasash

```jsx
// src/App.jsx
import { useState } from 'react'

// ============================================
// Vazifa 1-2: Oddiy Counter
// ============================================
function Counter() {
  const [son, setSon] = useState(0)
  const [qadam, setQadam] = useState(1)

  return (
    <div style={{ background: 'white', borderRadius: '20px', padding: '32px', textAlign: 'center', boxShadow: '0 8px 32px rgba(0,0,0,0.08)', marginBottom: '24px' }}>
      <h2 style={{ color: '#888', fontSize: '14px', textTransform: 'uppercase', letterSpacing: '1px', marginBottom: '8px' }}>Counter</h2>
      <div style={{ fontSize: '72px', fontWeight: '900', color: son > 0 ? 'royalblue' : son < 0 ? '#e63946' : '#1a1a2e', lineHeight: 1, marginBottom: '24px' }}>
        {son}
      </div>

      {/* Qadam tanlov */}
      <div style={{ display: 'flex', gap: '8px', justifyContent: 'center', marginBottom: '20px' }}>
        {[1, 5, 10, 100].map((q) => (
          <button key={q} onClick={() => setQadam(q)} style={{
            padding: '6px 14px', borderRadius: '8px', border: '2px solid',
            borderColor: qadam === q ? 'royalblue' : '#e5e7eb',
            background: qadam === q ? '#f0f4ff' : 'transparent',
            color: qadam === q ? 'royalblue' : '#555', fontWeight: '700', cursor: 'pointer'
          }}>
            ×{q}
          </button>
        ))}
      </div>

      <div style={{ display: 'flex', gap: '10px', justifyContent: 'center' }}>
        <button onClick={() => setSon(s => s - qadam)} style={{ padding: '12px 24px', fontSize: '20px', background: '#fee2e2', color: '#e63946', border: 'none', borderRadius: '12px', cursor: 'pointer', fontWeight: '700' }}>−</button>
        <button onClick={() => setSon(0)} style={{ padding: '12px 20px', fontSize: '14px', background: '#f3f4f6', color: '#555', border: 'none', borderRadius: '12px', cursor: 'pointer', fontWeight: '700' }}>Reset</button>
        <button onClick={() => setSon(s => s + qadam)} style={{ padding: '12px 24px', fontSize: '20px', background: '#d1fae5', color: '#10b981', border: 'none', borderRadius: '12px', cursor: 'pointer', fontWeight: '700' }}>+</button>
      </div>
    </div>
  )
}

// ============================================
// Vazifa 3-4: Toggle (Ko'rish/Yashirish)
// ============================================
function Toggle() {
  const [ochiq, setOchiq] = useState(false)
  const [tema, setTema] = useState('kunduz')

  return (
    <div style={{ background: tema === 'kecha' ? '#1a1a2e' : 'white', color: tema === 'kecha' ? 'white' : '#1a1a2e', borderRadius: '16px', padding: '24px', marginBottom: '24px', boxShadow: '0 4px 20px rgba(0,0,0,0.08)' }}>
      <div style={{ display: 'flex', justifyContent: 'space-between', alignItems: 'center', marginBottom: '16px' }}>
        <h2 style={{ fontSize: '18px' }}>⚡ Toggle Amaliyoti</h2>
        <button onClick={() => setTema(t => t === 'kunduz' ? 'kecha' : 'kunduz')} style={{ background: tema === 'kecha' ? '#f59e0b' : '#1a1a2e', color: 'white', border: 'none', padding: '8px 14px', borderRadius: '8px', cursor: 'pointer', fontWeight: '700', fontSize: '14px' }}>
          {tema === 'kecha' ? '☀️ Kunduz' : '🌙 Kecha'}
        </button>
      </div>

      <button onClick={() => setOchiq(!ochiq)} style={{ background: ochiq ? '#d1fae5' : '#f0f4ff', color: ochiq ? '#065f46' : 'royalblue', border: 'none', padding: '10px 18px', borderRadius: '10px', cursor: 'pointer', fontWeight: '700', marginBottom: '12px' }}>
        {ochiq ? '🔽 Yopish' : '▶️ Ko\'rish'}
      </button>

      {ochiq && (
        <div style={{ background: 'rgba(65,105,225,0.08)', padding: '16px', borderRadius: '10px', border: '1px solid rgba(65,105,225,0.2)' }}>
          <p>Bu kontent useState yordamida ko'rsatiladi va yashiriladi! 🎉</p>
        </div>
      )}
    </div>
  )
}

// ============================================
// Vazifa 5-6: Input State
// ============================================
function InputAmaliyot() {
  const [ism, setIsm] = useState('')
  const [telefon, setTelefon] = useState('')
  const [yuborildi, setYuborildi] = useState(false)

  function yuborish(e) {
    e.preventDefault()
    if (ism && telefon) setYuborildi(true)
  }

  if (yuborildi) {
    return (
      <div style={{ background: '#d1fae5', border: '1px solid #a7f3d0', borderRadius: '16px', padding: '24px', textAlign: 'center', marginBottom: '24px' }}>
        <div style={{ fontSize: '48px', marginBottom: '8px' }}>🎉</div>
        <h3>Muvaffaqiyat!</h3>
        <p>Ism: <strong>{ism}</strong>, Tel: <strong>{telefon}</strong></p>
        <button onClick={() => { setYuborildi(false); setIsm(''); setTelefon('') }} style={{ marginTop: '12px', background: '#10b981', color: 'white', border: 'none', padding: '10px 20px', borderRadius: '8px', cursor: 'pointer', fontWeight: '700' }}>
          Qaytish
        </button>
      </div>
    )
  }

  return (
    <div style={{ background: 'white', borderRadius: '16px', padding: '24px', marginBottom: '24px', boxShadow: '0 4px 20px rgba(0,0,0,0.08)' }}>
      <h2 style={{ marginBottom: '16px', fontSize: '18px' }}>📝 Input State</h2>
      <form onSubmit={yuborish} style={{ display: 'flex', flexDirection: 'column', gap: '12px' }}>
        <div>
          <label style={{ display: 'block', fontSize: '13px', fontWeight: '700', marginBottom: '6px' }}>Ism va Familiya</label>
          <input value={ism} onChange={e => setIsm(e.target.value)} placeholder="Ali Valiev" style={{ width: '100%', padding: '10px 14px', border: '2px solid #e5e7eb', borderRadius: '8px', fontSize: '15px', outline: 'none' }} />
          <small style={{ color: '#888', fontSize: '12px' }}>Uzunlik: {ism.length} belgi</small>
        </div>
        <div>
          <label style={{ display: 'block', fontSize: '13px', fontWeight: '700', marginBottom: '6px' }}>Telefon</label>
          <input value={telefon} onChange={e => setTelefon(e.target.value)} placeholder="+998901234567" type="tel" style={{ width: '100%', padding: '10px 14px', border: '2px solid #e5e7eb', borderRadius: '8px', fontSize: '15px', outline: 'none' }} />
        </div>
        <button type="submit" disabled={!ism || !telefon} style={{ background: ism && telefon ? 'royalblue' : '#e5e7eb', color: ism && telefon ? 'white' : '#9ca3af', border: 'none', padding: '12px', borderRadius: '8px', fontWeight: '700', cursor: ism && telefon ? 'pointer' : 'not-allowed' }}>
          Yuborish
        </button>
      </form>
    </div>
  )
}

// ============================================
// Vazifa 7-10: Todo List
// ============================================
function TodoList() {
  const [vazifalar, setVazifalar] = useState([
    { id: 1, matn: 'HTML o\'rganish', bajarildi: true },
    { id: 2, matn: 'CSS o\'rganish', bajarildi: true },
    { id: 3, matn: 'React o\'rganish', bajarildi: false },
  ])
  const [yangi, setYangi] = useState('')
  const [filter, setFilter] = useState('hammasi') // hammasi | bajarildi | kutmoqda

  function qo'shish() {
    if (!yangi.trim()) return
    setVazifalar(prev => [...prev, { id: Date.now(), matn: yangi.trim(), bajarildi: false }])
    setYangi('')
  }

  function ochirish(id) {
    setVazifalar(prev => prev.filter(v => v.id !== id))
  }

  function toggle(id) {
    setVazifalar(prev => prev.map(v => v.id === id ? { ...v, bajarildi: !v.bajarildi } : v))
  }

  const filterlangan = vazifalar.filter(v =>
    filter === 'bajarildi' ? v.bajarildi :
    filter === 'kutmoqda' ? !v.bajarildi : true
  )
  const bajarilganSon = vazifalar.filter(v => v.bajarildi).length

  return (
    <div style={{ background: 'white', borderRadius: '20px', padding: '28px', boxShadow: '0 8px 32px rgba(0,0,0,0.08)' }}>
      <div style={{ display: 'flex', justifyContent: 'space-between', alignItems: 'center', marginBottom: '20px' }}>
        <div>
          <h2 style={{ fontSize: '20px' }}>✅ Todo List</h2>
          <p style={{ fontSize: '13px', color: '#888', marginTop: '2px' }}>{bajarilganSon}/{vazifalar.length} ta bajarildi</p>
        </div>
        {/* Progress */}
        <div style={{ width: '60px', height: '60px', borderRadius: '50%', background: `conic-gradient(royalblue ${bajarilganSon/vazifalar.length*360}deg, #f0f0f0 0)`, display: 'flex', alignItems: 'center', justifyContent: 'center' }}>
          <div style={{ width: '44px', height: '44px', borderRadius: '50%', background: 'white', display: 'flex', alignItems: 'center', justifyContent: 'center', fontSize: '13px', fontWeight: '700' }}>
            {Math.round(bajarilganSon/vazifalar.length*100)}%
          </div>
        </div>
      </div>

      {/* Qo'shish */}
      <div style={{ display: 'flex', gap: '8px', marginBottom: '16px' }}>
        <input value={yangi} onChange={e => setYangi(e.target.value)} onKeyDown={e => e.key === 'Enter' && qo'shish()} placeholder="Yangi vazifa qo'shing..." style={{ flex: 1, padding: '10px 14px', border: '2px solid #e5e7eb', borderRadius: '8px', fontSize: '14px', outline: 'none' }} />
        <button onClick={qo'shish} style={{ background: 'royalblue', color: 'white', border: 'none', padding: '10px 16px', borderRadius: '8px', cursor: 'pointer', fontWeight: '700' }}>+</button>
      </div>

      {/* Filter */}
      <div style={{ display: 'flex', gap: '6px', marginBottom: '14px' }}>
        {[['hammasi','Hammasi'],['bajarildi','✅ Bajarildi'],['kutmoqda','⏳ Kutmoqda']].map(([qiymat, nom]) => (
          <button key={qiymat} onClick={() => setFilter(qiymat)} style={{ padding: '5px 12px', borderRadius: '20px', border: '1px solid', borderColor: filter===qiymat ? 'royalblue' : '#e5e7eb', background: filter===qiymat ? '#f0f4ff' : 'transparent', color: filter===qiymat ? 'royalblue' : '#555', fontSize: '12px', fontWeight: '700', cursor: 'pointer' }}>
            {nom}
          </button>
        ))}
      </div>

      {/* Ro'yxat */}
      <ul style={{ listStyle: 'none', display: 'flex', flexDirection: 'column', gap: '6px' }}>
        {filterlangan.map(v => (
          <li key={v.id} style={{ display: 'flex', alignItems: 'center', gap: '10px', padding: '10px 12px', background: '#f8f9fa', borderRadius: '10px', transition: 'all 0.2s' }}>
            <input type="checkbox" checked={v.bajarildi} onChange={() => toggle(v.id)} style={{ width: '18px', height: '18px', accentColor: 'royalblue', cursor: 'pointer' }} />
            <span style={{ flex: 1, textDecoration: v.bajarildi ? 'line-through' : 'none', color: v.bajarildi ? '#aaa' : '#1a1a2e', fontSize: '14px' }}>{v.matn}</span>
            <button onClick={() => ochirish(v.id)} style={{ background: '#fee2e2', color: '#e63946', border: 'none', width: '28px', height: '28px', borderRadius: '6px', cursor: 'pointer', display: 'flex', alignItems: 'center', justifyContent: 'center', fontWeight: '700' }}>×</button>
          </li>
        ))}
        {filterlangan.length === 0 && (
          <li style={{ textAlign: 'center', color: '#aaa', padding: '20px', fontSize: '14px' }}>Bo'sh 🎉</li>
        )}
      </ul>
    </div>
  )
}

function App() {
  return (
    <div style={{ minHeight: '100vh', background: '#f0f2f5', padding: '40px 20px', fontFamily: "'Segoe UI', sans-serif" }}>
      <div style={{ maxWidth: '520px', margin: '0 auto' }}>
        <h1 style={{ textAlign: 'center', marginBottom: '32px' }}>useState Hook Amaliyoti⚡</h1>
        <Counter />
        <Toggle />
        <InputAmaliyot />
        <TodoList />
      </div>
    </div>
  )
}
export default App
```
