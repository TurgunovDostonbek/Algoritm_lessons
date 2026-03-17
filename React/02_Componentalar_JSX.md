# 02-Dars: Componentalar va JSX

## 📌 Component nima?

**Component** — UI ning mustaqil, qayta ishlatiladigan bo'lagi. React ilovasi komponentlardan tashkil topgan.

```
Ilova
├── Header
│   ├── Logo
│   └── Navigation
├── Main
│   ├── HeroSection
│   ├── ProductList
│   │   ├── ProductCard
│   │   ├── ProductCard
│   │   └── ProductCard
│   └── Footer
```

```jsx
// Har bir quti = bitta komponent!
function App() {
  return (
    <div>
      <Header />      {/* Header komponenti */}
      <Main />        {/* Main komponenti */}
      <Footer />      {/* Footer komponenti */}
    </div>
  )
}
```

---

## 📌 Functional Component

```jsx
// 1. Function declaration
function Salom() {
  return <h1>Salom, Dunyo!</h1>
}

// 2. Arrow function (ko'p ishlatiladi)
const Salom = () => {
  return <h1>Salom, Dunyo!</h1>
}

// 3. Implicit return (qisqa yozuv)
const Salom = () => <h1>Salom, Dunyo!</h1>

// Komponent nomining BIRINCHI harfi KATTA bo'lishi shart!
// ✅ To'g'ri:
function MyComponent() {}
const UserCard = () => {}

// ❌ Xato:
function myComponent() {}   // kichik harf
const usercard = () => {}   // kichik harf
```

---

## 📌 JSX — JavaScript XML

**JSX** — JavaScript ichida HTML yozish imkonini beruvchi sintaksis kengaytmasi. Vite/Babel uni JavaScript ga o'giradi.

```jsx
// JSX yozamiz (biz)
const element = <h1 className="sarlavha">Salom!</h1>

// Babel JavaScript ga o'giradi (kompyuter)
const element = React.createElement(
  'h1',
  { className: 'sarlavha' },
  'Salom!'
)
```

---

## 📌 JSX Qoidalari

```jsx
// ✅ 1. Bitta ildiz element (root)
function App() {
  return (
    <div>           {/* Bitta ildiz */}
      <h1>Sarlavha</h1>
      <p>Matn</p>
    </div>
  )
}

// ✅ Fragment — qo'shimcha div qo'shmaydi
function App() {
  return (
    <>              {/* Fragment */}
      <h1>Sarlavha</h1>
      <p>Matn</p>
    </>
  )
}

// ❌ Xato — ikkita ildiz
function App() {
  return (
    <h1>Sarlavha</h1>    // Error!
    <p>Matn</p>
  )
}
```

```jsx
// ✅ 2. className (class emas!)
<div className="container">...</div>     // ✅
<div class="container">...</div>         // ❌ (HTMLAttribute!)

// ✅ 3. htmlFor (for emas!)
<label htmlFor="ism">Ism:</label>        // ✅
<label for="ism">Ism:</label>            // ❌

// ✅ 4. Self-closing teglar
<img src="rasm.jpg" alt="Rasm" />       // ✅ (/ bilan yopiladi)
<br />
<input type="text" />
<img src="rasm.jpg" alt="Rasm">         // ❌

// ✅ 5. camelCase atributlar
<div onClick={handler}>                  // ✅ (onclick emas)
<div tabIndex={0}>                       // ✅ (tabindex emas)
<input readOnly />                       // ✅ (readonly emas)
<div style={{ backgroundColor: 'red' }} // ✅ (background-color emas)
```

---

## 📌 JSX ichida JavaScript — `{}`

```jsx
function KartochkaMavzusi() {
  // O'zgaruvchilar
  const ism = "Ali Valiev"
  const yosh = 22
  const kasblar = ["HTML", "CSS", "React"]
  const isOnline = true

  return (
    <div>
      {/* O'zgaruvchi */}
      <h1>{ism}</h1>

      {/* Ifoda (expression) */}
      <p>Yosh: {yosh * 2}</p>

      {/* Shartli ko'rsatish (ternary) */}
      <span>{isOnline ? "🟢 Online" : "🔴 Offline"}</span>

      {/* && operatori */}
      {yosh >= 18 && <p>Kattalar uchun</p>}

      {/* Massiv .map() */}
      <ul>
        {kasblar.map((kasb) => (
          <li key={kasb}>{kasb}</li>
        ))}
      </ul>

      {/* Funcisa chaqirish */}
      <p>{ism.toUpperCase()}</p>

      {/* Ob'ektning xususiyati */}
      <p>{`${ism} — ${yosh} yoshda`}</p>
    </div>
  )
}
```

---

## 📌 React Renderlash Mexanizmi

```
1. JSX yoziladi
       ↓
2. Babel/Vite uni React.createElement() ga o'giradi
       ↓
3. React Virtual DOM (VDOM) yaratadi
       ↓
4. React VDOM va real DOM ni solishtiradi (Diffing)
       ↓
5. Faqat o'zgargan qismlar real DOM ga yoziladi (Reconciliation)
```

```jsx
// Virtual DOM — JavaScript ob'ekti ko'rinishida
{
  type: 'div',
  props: {
    className: 'karta',
    children: [
      { type: 'h1', props: { children: 'Ali' } },
      { type: 'p', props: { children: '22 yosh' } }
    ]
  }
}
```

---

## 🎯 10 ta Amaliy Vazifa — Componentalarni O'rganib Kelish

```jsx
// src/App.jsx
import Sarlavha from './components/Sarlavha'
import Karta from './components/Karta'
import Tugma from './components/Tugma'
import Badge from './components/Badge'
import Avatar from './components/Avatar'

function App() {
  return (
    <div style={{ minHeight: '100vh', background: '#f0f2f5', padding: '40px 20px' }}>
      <div style={{ maxWidth: '800px', margin: '0 auto' }}>
        <Sarlavha />
        <Karta />
        <Tugma />
        <Badge />
        <Avatar />
      </div>
    </div>
  )
}
export default App
```

```jsx
// src/components/Sarlavha.jsx — Vazifa 1-2
function Sarlavha() {
  const saytNomi = "React Dars"
  const sanalar = ["2024-01-15", "2024-02-20", "2024-03-16"]

  return (
    <header style={{
      background: 'linear-gradient(135deg, #1a1a2e, #16213e)',
      color: 'white', padding: '40px', borderRadius: '20px',
      marginBottom: '24px', textAlign: 'center'
    }}>
      {/* Vazifa 1: O'zgaruvchi JSX ichida */}
      <h1 style={{ fontSize: '2rem', marginBottom: '8px' }}>
        🚀 {saytNomi} — Sabaq {new Date().getFullYear()}
      </h1>
      <p style={{ opacity: 0.7 }}>
        Bugun: {new Date().toLocaleDateString('uz-UZ')}
      </p>

      {/* Vazifa 2: Array map */}
      <div style={{ display: 'flex', gap: '8px', justifyContent: 'center', marginTop: '16px' }}>
        {sanalar.map((sana, index) => (
          <span key={sana} style={{
            background: 'rgba(255,255,255,0.1)', padding: '4px 12px',
            borderRadius: '20px', fontSize: '13px'
          }}>
            {index + 1}-dars: {sana}
          </span>
        ))}
      </div>
    </header>
  )
}
export default Sarlavha
```

```jsx
// src/components/Karta.jsx — Vazifa 3-4
function Karta() {
  const ism = "Ali Valiev"
  const lavozim = "Frontend Developer"
  const isOnline = true
  const ball = 95

  return (
    <div style={{
      background: 'white', borderRadius: '16px', padding: '28px',
      boxShadow: '0 4px 24px rgba(0,0,0,0.08)', marginBottom: '16px'
    }}>
      <h2 style={{ marginBottom: '16px', fontSize: '18px' }}>👤 Foydalanuvchi Kartasi</h2>

      {/* Vazifa 3: Shartli renderlash (ternary) */}
      <div style={{ display: 'flex', alignItems: 'center', gap: '12px', marginBottom: '12px' }}>
        <div style={{
          width: '48px', height: '48px', borderRadius: '50%', background: 'royalblue',
          display: 'flex', alignItems: 'center', justifyContent: 'center', color: 'white', fontWeight: '700'
        }}>
          {ism.charAt(0)}
        </div>
        <div>
          <div style={{ fontWeight: '700' }}>{ism}</div>
          <div style={{ fontSize: '13px', color: '#888' }}>{lavozim}</div>
        </div>
        {/* Shartli ko'rsatish */}
        <span style={{ marginLeft: 'auto', color: isOnline ? '#10b981' : '#e63946' }}>
          {isOnline ? '🟢 Online' : '🔴 Offline'}
        </span>
      </div>

      {/* Vazifa 4: && operatori */}
      {ball >= 90 && (
        <div style={{ background: '#d1fae5', color: '#065f46', padding: '10px 14px', borderRadius: '8px', fontSize: '14px' }}>
          🏆 A'lo o'quvchi! Ball: {ball}/100
        </div>
      )}
    </div>
  )
}
export default Karta
```

```jsx
// src/components/Tugma.jsx — Vazifa 5-6
function Tugma() {
  const tugmalar = [
    { nom: 'Asosiy', stil: { background: 'royalblue', color: 'white' } },
    { nom: 'Muvaffaqiyat', stil: { background: '#10b981', color: 'white' } },
    { nom: 'Xavf', stil: { background: '#e63946', color: 'white' } },
    { nom: 'Oddiy', stil: { background: '#f3f4f6', color: '#1a1a2e' } },
  ]

  return (
    <div style={{ background: 'white', borderRadius: '16px', padding: '28px', marginBottom: '16px', boxShadow: '0 4px 24px rgba(0,0,0,0.08)' }}>
      <h2 style={{ marginBottom: '16px', fontSize: '18px' }}>🎛 Tugmalar Sistemasi</h2>

      {/* Vazifa 5: Tugmalar map */}
      <div style={{ display: 'flex', gap: '10px', flexWrap: 'wrap' }}>
        {tugmalar.map((tugma) => (
          <button
            key={tugma.nom}
            style={{
              ...tugma.stil,
              padding: '10px 20px', borderRadius: '8px',
              border: 'none', fontWeight: '600', cursor: 'pointer',
              fontSize: '14px'
            }}
          >
            {tugma.nom}
          </button>
        ))}
      </div>

      {/* Vazifa 6: Expression JSX da */}
      <p style={{ marginTop: '16px', color: '#888', fontSize: '13px' }}>
        Jami {tugmalar.length} ta tugma • Bugun yaratildi: {new Date().toLocaleDateString('uz-UZ')}
      </p>
    </div>
  )
}
export default Tugma
```

```jsx
// src/components/Badge.jsx — Vazifa 7-8
function Badge() {
  const texnologiyalar = [
    { nom: 'HTML', rang: '#e34c26', emoji: '🌐' },
    { nom: 'CSS', rang: '#264de4', emoji: '🎨' },
    { nom: 'JavaScript', rang: '#f7df1e', matn: '#1a1a2e', emoji: '⚡' },
    { nom: 'React', rang: '#61dafb', matn: '#1a1a2e', emoji: '⚛️' },
    { nom: 'Git', rang: '#f14e32', emoji: '🐙' },
    { nom: 'Node.js', rang: '#339933', emoji: '🟢' },
  ]

  return (
    <div style={{ background: 'white', borderRadius: '16px', padding: '28px', marginBottom: '16px', boxShadow: '0 4px 24px rgba(0,0,0,0.08)' }}>
      <h2 style={{ marginBottom: '16px', fontSize: '18px' }}>🏷 Texnologiya Badge lar</h2>

      {/* Vazifa 7: ob'ektlar massivi — map */}
      <div style={{ display: 'flex', flexWrap: 'wrap', gap: '10px' }}>
        {texnologiyalar.map((tech) => (
          <span
            key={tech.nom}
            style={{
              background: tech.rang,
              color: tech.matn || 'white',
              padding: '8px 16px', borderRadius: '20px',
              fontWeight: '700', fontSize: '14px',
              display: 'flex', alignItems: 'center', gap: '6px'
            }}
          >
            {tech.emoji} {tech.nom}
          </span>
        ))}
      </div>

      {/* Vazifa 8: Hisoblab ko'rsatish */}
      <p style={{ marginTop: '14px', color: '#888', fontSize: '13px' }}>
        Jami: {texnologiyalar.length} ta texnologiya biladi,{' '}
        shundan {texnologiyalar.filter(t => t.matn).length} ta sariq/ko'k
      </p>
    </div>
  )
}
export default Badge
```

```jsx
// src/components/Avatar.jsx — Vazifa 9-10
function Avatar() {
  const jamoasi = [
    { ism: 'Ali', rang: '#4361ee', emoji: '👨‍💻', lavozim: 'Frontend' },
    { ism: 'Malika', rang: '#e63946', emoji: '👩‍💻', lavozim: 'Backend' },
    { ism: 'Jasur', rang: '#10b981', emoji: '👨‍🎨', lavozim: 'Design' },
    { ism: 'Nilufar', rang: '#f59e0b', emoji: '👩‍📊', lavozim: 'PM' },
  ]

  return (
    <div style={{ background: 'white', borderRadius: '16px', padding: '28px', boxShadow: '0 4px 24px rgba(0,0,0,0.08)' }}>
      <h2 style={{ marginBottom: '20px', fontSize: '18px' }}>
        👥 Jamoa ({jamoasi.length} kishi)
      </h2>

      {/* Vazifa 9: Avatar kartalar */}
      <div style={{ display: 'grid', gridTemplateColumns: 'repeat(auto-fill, minmax(150px, 1fr))', gap: '14px' }}>
        {jamoasi.map((kishi) => (
          <div key={kishi.ism} style={{
            background: '#f8f9fa', borderRadius: '12px', padding: '20px',
            textAlign: 'center', transition: 'transform 0.2s'
          }}>
            <div style={{
              width: '56px', height: '56px', borderRadius: '50%',
              background: kishi.rang, color: 'white', margin: '0 auto 10px',
              display: 'flex', alignItems: 'center', justifyContent: 'center',
              fontSize: '28px'
            }}>
              {kishi.emoji}
            </div>
            <div style={{ fontWeight: '700', marginBottom: '4px' }}>{kishi.ism}</div>
            <div style={{ fontSize: '12px', color: '#888' }}>{kishi.lavozim}</div>
          </div>
        ))}
      </div>

      {/* Vazifa 10: Fragment va expression */}
      <>
        <hr style={{ border: 'none', borderTop: '1px solid #f0f0f0', margin: '20px 0' }} />
        <p style={{ textAlign: 'center', color: '#888', fontSize: '13px' }}>
          🚀 Jami {jamoasi.length} ta a'zo • Hamkorlik = Muvaffaqiyat
        </p>
      </>
    </div>
  )
}
export default Avatar
```
