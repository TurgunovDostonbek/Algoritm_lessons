# 07-Dars: Handling Events in React

## 📌 Event nima?

**Event (Hodisa)** — foydalanuvchining harakati: bosish, yozish, yuborish va h.k.

```jsx
// HTML:
<button onclick="handler()">Bosing</button>

// React JSX (camelCase!):
<button onClick={handler}>Bosing</button>
//       ↑↑↑↑↑↑↑         ↑↑↑↑↑↑↑
//  camelCase!           {} ichida
```

---

## 📌 Asosiy Event turlari

```jsx
// Mouse Events
<button onClick={fn}>Bosish</button>
<div onDoubleClick={fn}>Ikki marta bosish</div>
<div onMouseEnter={fn}>Sichqon ustiga kelish</div>
<div onMouseLeave={fn}>Sichqon ketish</div>
<div onMouseMove={fn}>Sichqon harakat</div>

// Keyboard Events
<input onKeyDown={fn} />    // Tugma bosildi
<input onKeyUp={fn} />      // Tugma qo'yildi
<input onKeyPress={fn} />   // Tugma bosildi (eski)

// Form Events
<input onChange={fn} />     // Qiymat o'zgardi
<input onFocus={fn} />      // Focus oldi
<input onBlur={fn} />       // Focus yo'qoldi
<form onSubmit={fn} />      // Forma yuborildi

// Clipboard Events
<input onCopy={fn} />
<input onPaste={fn} />
<input onCut={fn} />

// Drag Events
<div onDrag={fn} />
<div onDrop={fn} />
```

---

## 📌 Event Ob'ekti (e)

```jsx
function handler(e) {
  console.log(e)              // SyntheticEvent ob'ekti
  console.log(e.target)       // Element o'zi
  console.log(e.target.value) // Input qiymati
  console.log(e.type)         // 'click', 'change', ...
  console.log(e.key)          // 'Enter', 'Escape', ...

  e.preventDefault()          // Default harakatni to'xtatish (forma yuborilish)
  e.stopPropagation()         // Eventning ota elementga o'tishini to'xtatish
}

// Input change:
<input onChange={(e) => console.log(e.target.value)} />

// Form submit:
function yuborish(e) {
  e.preventDefault()   // Sahifa yangilanmaydi!
  console.log('Yuborildi!')
}
<form onSubmit={yuborish}>
```

---

## 📌 Event Boshqaruvchisiga Argument Uzatish

```jsx
// ❌ Xato — darhol chaqiriladi
<button onClick={handler('Ali')}>Bosing</button>

// ✅ Arrow function orqali
<button onClick={() => handler('Ali')}>Bosing</button>
<button onClick={() => ochirish(user.id)}>O'chirish</button>

// ✅ Event ham, argument ham
<button onClick={(e) => handler(e, 'Ali')}>Bosing</button>
```

---

## 🎯 10 ta Amaliy Vazifa — To Do List yasash

```jsx
// src/App.jsx
import { useState } from 'react'

// ============================================
// Vazifa 1-3: Kalkulyator (onClick)
// ============================================
function Kalkulyator() {
  const [natija, setNatija] = useState('')
  const [amal, setAmal] = useState('')

  function tugmaBosish(qiymat) {
    if (qiymat === '=') {
      try {
        setNatija(String(eval(amal)))
      } catch {
        setNatija('Xato!')
      }
    } else if (qiymat === 'C') {
      setAmal('')
      setNatija('')
    } else if (qiymat === '⌫') {
      setAmal(amal.slice(0, -1))
    } else {
      setAmal(amal + qiymat)
    }
  }

  const tugmalar = [
    ['C', '⌫', '%', '÷'],
    ['7', '8', '9', '×'],
    ['4', '5', '6', '−'],
    ['1', '2', '3', '+'],
    ['±', '0', '.', '='],
  ].map(row => row.map(t => ({
    nom: t,
    qiymat: t === '÷' ? '/' : t === '×' ? '*' : t === '−' ? '-' : t === '±' ? '(-' : t,
    tur: ['÷','×','−','+'].includes(t) ? 'amal' : ['='].includes(t) ? 'teng' : ['C','⌫','%'].includes(t) ? 'maxsus' : 'son'
  })))

  const ranglar = {
    son: { bg: 'white', rang: '#1a1a2e' },
    amal: { bg: '#f0f4ff', rang: 'royalblue' },
    teng: { bg: 'royalblue', rang: 'white' },
    maxsus: { bg: '#f3f4f6', rang: '#555' },
  }

  return (
    <div style={{ background: '#1a1a2e', borderRadius: '24px', padding: '24px', width: '280px', boxShadow: '0 20px 60px rgba(0,0,0,0.3)', marginBottom: '24px' }}>
      {/* Ekran */}
      <div style={{ textAlign: 'right', padding: '16px 8px', marginBottom: '16px' }}>
        <div style={{ color: 'rgba(255,255,255,0.5)', fontSize: '14px', minHeight: '20px' }}>{amal || '0'}</div>
        <div style={{ color: 'white', fontSize: '36px', fontWeight: '700', minHeight: '48px' }}>{natija}</div>
      </div>

      {/* Tugmalar */}
      <div style={{ display: 'grid', gridTemplateColumns: 'repeat(4, 1fr)', gap: '8px' }}>
        {tugmalar.flat().map((t, i) => (
          <button key={i} onClick={() => tugmaBosish(t.qiymat)}
            style={{
              padding: '14px', borderRadius: '12px', border: 'none', cursor: 'pointer',
              background: ranglar[t.tur].bg, color: ranglar[t.tur].rang,
              fontSize: '16px', fontWeight: '700', transition: 'opacity 0.15s'
            }}
            onMouseEnter={e => e.target.style.opacity = '0.8'}
            onMouseLeave={e => e.target.style.opacity = '1'}
          >
            {t.nom}
          </button>
        ))}
      </div>
    </div>
  )
}

// ============================================
// Vazifa 4-6: Qidiruv (onChange, onFocus, onBlur)
// ============================================
const MEVA_ROYHAT = ['Olma', 'Nok', 'Banan', 'Uzum', 'Qulupnay', 'Apelsin', 'Limon', 'Gilos', 'Shaftoli', 'Xurmo']

function Qidiruv() {
  const [qidiruv, setQidiruv] = useState('')
  const [focused, setFocused] = useState(false)

  const natijalar = MEVA_ROYHAT.filter(m => m.toLowerCase().includes(qidiruv.toLowerCase()))

  return (
    <div style={{ marginBottom: '24px' }}>
      <h2 style={{ marginBottom: '12px' }}>🔍 Qidiruv (onChange)</h2>
      <div style={{ position: 'relative' }}>
        <input
          value={qidiruv}
          onChange={(e) => setQidiruv(e.target.value)}
          onFocus={() => setFocused(true)}
          onBlur={() => setTimeout(() => setFocused(false), 150)}
          placeholder="Meva qidiring..."
          style={{
            width: '100%', padding: '12px 16px', border: `2px solid ${focused ? 'royalblue' : '#e5e7eb'}`,
            borderRadius: '12px', fontSize: '16px', outline: 'none',
            boxShadow: focused ? '0 0 0 3px rgba(65,105,225,0.1)' : 'none',
            transition: 'all 0.2s', boxSizing: 'border-box'
          }}
        />
        {qidiruv && (
          <button onClick={() => setQidiruv('')} style={{ position: 'absolute', right: '12px', top: '50%', transform: 'translateY(-50%)', background: '#e5e7eb', border: 'none', borderRadius: '50%', width: '22px', height: '22px', cursor: 'pointer', fontSize: '12px' }}>×</button>
        )}
      </div>

      {focused && (
        <div style={{ background: 'white', border: '1px solid #e5e7eb', borderRadius: '12px', marginTop: '6px', boxShadow: '0 8px 24px rgba(0,0,0,0.1)', overflow: 'hidden' }}>
          {natijalar.length > 0 ? natijalar.map((meva) => (
            <div key={meva} onClick={() => { setQidiruv(meva); setFocused(false) }}
              style={{ padding: '10px 16px', cursor: 'pointer', fontSize: '14px', transition: 'background 0.1s' }}
              onMouseEnter={e => e.target.style.background = '#f0f4ff'}
              onMouseLeave={e => e.target.style.background = 'transparent'}
            >
              {meva}
            </div>
          )) : (
            <div style={{ padding: '12px 16px', color: '#888', fontSize: '14px' }}>Topilmadi 😢</div>
          )}
        </div>
      )}
    </div>
  )
}

// ============================================
// Vazifa 7-10: To Do List (onClick, onChange, onKeyDown, onSubmit)
// ============================================
function ToDoList() {
  const [vazifalar, setVazifalar] = useState([
    { id: 1, matn: 'React o\'rganish', bajarildi: false, muhim: true },
    { id: 2, matn: 'useState tushinish', bajarildi: true, muhim: false },
    { id: 3, matn: 'Event lar bilan ishlash', bajarildi: false, muhim: true },
  ])
  const [yangi, setYangi] = useState('')
  const [muhim, setMuhim] = useState(false)
  const [hoverItem, setHoverItem] = useState(null)

  function qo'shish(e) {
    e?.preventDefault()
    if (!yangi.trim()) return
    setVazifalar(prev => [...prev, { id: Date.now(), matn: yangi.trim(), bajarildi: false, muhim }])
    setYangi('')
    setMuhim(false)
  }

  function ochirish(id) { setVazifalar(prev => prev.filter(v => v.id !== id)) }
  function toggle(id)   { setVazifalar(prev => prev.map(v => v.id === id ? { ...v, bajarildi: !v.bajarildi } : v)) }

  const bajarilmagan = vazifalar.filter(v => !v.bajarildi).length

  return (
    <div style={{ background: 'white', borderRadius: '20px', overflow: 'hidden', boxShadow: '0 8px 32px rgba(0,0,0,0.08)' }}>
      {/* Header */}
      <div style={{ background: 'linear-gradient(135deg, royalblue, #7c3aed)', padding: '24px', color: 'white' }}>
        <h2 style={{ fontSize: '22px' }}>✅ To-Do List</h2>
        <p style={{ opacity: 0.8, fontSize: '14px' }}>{bajarilmagan} ta vazifa kutmoqda</p>
      </div>

      <div style={{ padding: '20px' }}>
        {/* Vazifa 7: onSubmit + onKeyDown */}
        <form onSubmit={qo'shish} style={{ display: 'flex', gap: '8px', marginBottom: '16px' }}>
          <div style={{ flex: 1, position: 'relative' }}>
            <input
              value={yangi}
              onChange={e => setYangi(e.target.value)}
              onKeyDown={e => e.key === 'Enter' && qo'shish()}
              placeholder="Yangi vazifa (Enter★)"
              style={{ width: '100%', padding: '10px 14px', border: '2px solid #e5e7eb', borderRadius: '8px', fontSize: '14px', outline: 'none', boxSizing: 'border-box' }}
            />
          </div>
          {/* Vazifa 8: onChange checkbox */}
          <label style={{ display: 'flex', alignItems: 'center', gap: '4px', fontSize: '12px', whiteSpace: 'nowrap', cursor: 'pointer' }}>
            <input type="checkbox" checked={muhim} onChange={e => setMuhim(e.target.checked)} style={{ accentColor: '#e63946' }} />
            ⭐
          </label>
          <button type="submit" style={{ background: 'royalblue', color: 'white', border: 'none', padding: '10px 14px', borderRadius: '8px', cursor: 'pointer', fontWeight: '700' }}>+</button>
        </form>

        {/* Vazifa 9-10: onClick, onMouseEnter, onMouseLeave */}
        <ul style={{ listStyle: 'none', display: 'flex', flexDirection: 'column', gap: '6px' }}>
          {vazifalar.map(v => (
            <li key={v.id}
              onMouseEnter={() => setHoverItem(v.id)}
              onMouseLeave={() => setHoverItem(null)}
              style={{
                display: 'flex', alignItems: 'center', gap: '10px', padding: '10px 12px',
                background: hoverItem === v.id ? '#f8f9ff' : '#f8f9fa', borderRadius: '10px',
                border: v.muhim ? '1px solid #fca5a5' : '1px solid transparent', transition: 'all 0.2s'
              }}>
              <input type="checkbox" checked={v.bajarildi} onChange={() => toggle(v.id)} style={{ width: '18px', height: '18px', accentColor: 'royalblue', cursor: 'pointer' }} />
              {v.muhim && <span title="Muhim" style={{ color: '#e63946', fontSize: '14px' }}>⭐</span>}
              <span style={{ flex: 1, textDecoration: v.bajarildi ? 'line-through' : 'none', color: v.bajarildi ? '#aaa' : '#1a1a2e', fontSize: '14px' }}>{v.matn}</span>
              {hoverItem === v.id && (
                <button onClick={() => ochirish(v.id)} style={{ background: '#fee2e2', color: '#e63946', border: 'none', width: '26px', height: '26px', borderRadius: '6px', cursor: 'pointer', fontSize: '14px' }}>
                  🗑
                </button>
              )}
            </li>
          ))}
        </ul>
      </div>
    </div>
  )
}

function App() {
  return (
    <div style={{ minHeight: '100vh', background: '#f0f2f5', padding: '40px 20px', fontFamily: "'Segoe UI', sans-serif" }}>
      <div style={{ maxWidth: '520px', margin: '0 auto' }}>
        <h1 style={{ textAlign: 'center', marginBottom: '32px' }}>🎯 Events in React</h1>
        <Kalkulyator />
        <Qidiruv />
        <ToDoList />
      </div>
    </div>
  )
}
export default App
```
