# 05-Dars: Props

## 📌 Props nima?

**Props** (properties) — ota komponentdan bola komponentga ma'lumot uzatish usuli. Props **faqat bir tomonga** ishlaydi (ota → bola).

```jsx
// Props PROPERTIES — xuddi HTML atributlari kabi
// <img src="..." alt="..." /> — src va alt propslar!

// Ota komponent — props YO'NALTIRADI
function App() {
  return <Salom ism="Ali" yosh={22} />
}

// Bola komponent — props QABUL QILADI
function Salom(props) {
  return (
    <h1>Salom, {props.ism}! Siz {props.yosh} yoshdasiz.</h1>
  )
}
```

---

## 📌 Props Destructuring

```jsx
// 1. Oddiy (props ob'ekti)
function Karta(props) {
  return <h2>{props.sarlavha}</h2>
}

// 2. Destructuring (tavsiya etiladi!)
function Karta({ sarlavha, tavsif, rasm }) {
  return (
    <div>
      <img src={rasm} alt={sarlavha} />
      <h2>{sarlavha}</h2>
      <p>{tavsif}</p>
    </div>
  )
}

// 3. Funksiya parametrida destructuring
const Karta = ({ sarlavha, tavsif, bolalar }) => (
  <div>
    <h2>{sarlavha}</h2>
    <p>{tavsif}</p>
    {bolalar}
  </div>
)
```

---

## 📌 Default Props

```jsx
// 1. Parametrda default qiymat (tavsiya etiladi)
function Tugma({ matn = 'Bosing', turi = 'asosiy', katta = false }) {
  return (
    <button className={`btn btn-${turi} ${katta ? 'btn-lg' : ''}`}>
      {matn}
    </button>
  )
}

// Ishlatish:
<Tugma />                           // matn="Bosing", turi="asosiy"
<Tugma matn="Saqlash" turi="xavf"  // matn="Saqlash", turi="xavf"

// 2. defaultProps (eski usul)
Tugma.defaultProps = {
  matn: 'Bosing',
  turi: 'asosiy',
}
```

---

## 📌 `children` Props

```jsx
// children — komponent ichiga joylashtirilgan elementlar

function Karta({ sarlavha, children }) {
  return (
    <div style={{ border: '1px solid #ddd', borderRadius: '12px', padding: '20px' }}>
      <h2>{sarlavha}</h2>
      <hr />
      {children}       {/* Bu yerga ichki kontent chiqadi */}
    </div>
  )
}

// Ishlatish:
<Karta sarlavha="Mening Kartam">
  <p>Bu children props!</p>
  <button>Bosing</button>
</Karta>

// Modal komponenti:
function Modal({ sarlavha, children, onYopish }) {
  return (
    <div className="modal-overlay">
      <div className="modal">
        <div className="modal-header">
          <h2>{sarlavha}</h2>
          <button onClick={onYopish}>×</button>
        </div>
        <div className="modal-body">
          {children}
        </div>
      </div>
    </div>
  )
}
```

---

## 📌 Props dan Funksiya Uzatish

```jsx
// Ota komponent
function App() {
  function xabarBer(ism) {
    alert(`Salom, ${ism}!`)
  }

  return <Tugma onClick={() => xabarBer('Ali')} />
}

// Bola komponent — funksiyani props orqali oladi
function Tugma({ onClick }) {
  return <button onClick={onClick}>Bosing</button>
}
```

---

## 📌 Component Hierarchy — Komponent Daraxti

```
App
├── Header
│   └── NavItem (navHavola="Bosh") → props: navHavola
│   └── NavItem (navHavola="Blog") → props: navHavola
│   └── NavItem (navHavola="Aloqa") → props: navHavola
│
└── Main
    ├── HeroSection (sarlavha="Salom!" tavsif="...") → props: sarlavha, tavsif
    └── KartaRoyhat (kartalar=[...]) → props: kartalar
        ├── Karta (sarlavha="..." rasm="...") → props: sarlavha, rasm
        ├── Karta (sarlavha="..." rasm="...") → props: sarlavha, rasm
        └── Karta (sarlavha="..." rasm="...") → props: sarlavha, rasm
```

---

## 🎯 10 ta Amaliy Vazifa — Figurani Props bilan Qilib Keladi

```jsx
// src/App.jsx
import FigureKarta from './components/FigureKarta'
import ProfileKarta from './components/ProfileKarta'
import StatistikKarta from './components/StatistikKarta'
import Alert from './components/Alert'
import Tugma from './components/Tugma'

const raqamlar = [
  { belgi: '👥', qiymat: '12,400', nom: 'Foydalanuvchilar' },
  { belgi: '📦', qiymat: '3,240', nom: 'Mahsulotlar' },
  { belgi: '⭐', qiymat: '4.9', nom: 'Reyting' },
  { belgi: '🚀', qiymat: '99.9%', nom: 'Uptime' },
]

function App() {
  return (
    <div style={{ minHeight: '100vh', background: '#f0f2f5', padding: '40px 20px', fontFamily: "'Segoe UI', sans-serif" }}>
      <div style={{ maxWidth: '900px', margin: '0 auto' }}>
        <h1 style={{ textAlign: 'center', marginBottom: '8px' }}>Props Amaliyoti 🎭</h1>
        <p style={{ textAlign: 'center', color: '#888', marginBottom: '40px' }}>Barcha komponentlar props orqali ma'lumot oladi</p>

        {/* Vazifa 1-2: Tugmalar */}
        <section style={{ marginBottom: '40px' }}>
          <h2 style={{ marginBottom: '16px' }}>Tugmalar</h2>
          <div style={{ display: 'flex', gap: '12px', flexWrap: 'wrap' }}>
            <Tugma matn="Saqlash" turi="asosiy" />
            <Tugma matn="O'chirish" turi="xavf" />
            <Tugma matn="Bekor qilish" turi="ikkilamchi" />
            <Tugma matn="Katta tugma" turi="asosiy" katta={true} />
            <Tugma />  {/* Default props */}
          </div>
        </section>

        {/* Vazifa 3: Alert xabarlari */}
        <section style={{ marginBottom: '40px' }}>
          <h2 style={{ marginBottom: '16px' }}>Alertlar (children props)</h2>
          <Alert turi="muvaffaqiyat">✅ Saqlash muvaffaqiyatli amalga oshirildi!</Alert>
          <Alert turi="xavf">❌ Xato yuz berdi. Qaytadan urinib ko'ring.</Alert>
          <Alert turi="ogohlantirish">⚠️ Bu amalni ortga qaytarib bo'lmaydi!</Alert>
          <Alert turi="ma'lumot">ℹ️ Yangi versiya chiqdi. Yangilang!</Alert>
        </section>

        {/* Vazifa 4-5: Statistika kartalar */}
        <section style={{ marginBottom: '40px' }}>
          <h2 style={{ marginBottom: '16px' }}>Statistika</h2>
          <div style={{ display: 'grid', gridTemplateColumns: 'repeat(auto-fill, minmax(180px, 1fr))', gap: '16px' }}>
            {raqamlar.map((r) => (
              <StatistikKarta key={r.nom} belgi={r.belgi} qiymat={r.qiymat} nom={r.nom} />
            ))}
          </div>
        </section>

        {/* Vazifa 6-8: Profil kartalar */}
        <section style={{ marginBottom: '40px' }}>
          <h2 style={{ marginBottom: '16px' }}>Jamoa</h2>
          <div style={{ display: 'grid', gridTemplateColumns: 'repeat(auto-fill, minmax(260px, 1fr))', gap: '20px' }}>
            <ProfileKarta ism="Ali Valiev" lavozim="Frontend Developer" rang="#4361ee" emoji="👨‍💻" reyting={5} tajriba="2 yil" />
            <ProfileKarta ism="Malika Saidova" lavozim="UI/UX Designer" rang="#e63946" emoji="👩‍🎨" reyting={5} tajriba="3 yil" />
            <ProfileKarta ism="Jasur Toshmatov" lavozim="Backend Developer" rang="#10b981" emoji="👨‍💻" reyting={4} tajriba="1 yil" />
          </div>
        </section>

        {/* Vazifa 9-10: Figure kartalar */}
        <section>
          <h2 style={{ marginBottom: '16px' }}>Figure Galereyasi</h2>
          <div style={{ display: 'grid', gridTemplateColumns: 'repeat(auto-fill, minmax(280px, 1fr))', gap: '20px' }}>
            <FigureKarta
              rasm="https://picsum.photos/400/300?random=31"
              sarlavha="Tog' manzarasi"
              tavsif="Oʻzbekistonning go'zal tog'lari orasida sayohat"
              yoyilma="Toshkent, O'zbekiston"
            />
            <FigureKarta
              rasm="https://picsum.photos/400/300?random=32"
              sarlavha="Samarqand Me'morchiligi"
              tavsif="Buyuk ipak yo'lining markazidagi tarixiy shahar"
              yoyilma="Samarqand, O'zbekiston"
            />
            <FigureKarta
              rasm="https://picsum.photos/400/300?random=33"
              sarlavha="Buxoro Ko'chalari"
              tavsif="Qadimiy shahar ko'chalari va medrasa larini kashf eting"
              yoyilma="Buxoro, O'zbekiston"
            />
          </div>
        </section>

      </div>
    </div>
  )
}
export default App
```

```jsx
// src/components/Tugma.jsx — Vazifa 1-2
function Tugma({ matn = 'Bosing', turi = 'asosiy', katta = false, onClick }) {
  const stillar = {
    asosiy:     { background: 'royalblue', color: 'white' },
    xavf:       { background: '#e63946', color: 'white' },
    ikkilamchi: { background: '#f3f4f6', color: '#1a1a2e' },
    muvaffaqiyat: { background: '#10b981', color: 'white' },
  }
  return (
    <button onClick={onClick} style={{
      ...stillar[turi],
      padding: katta ? '14px 28px' : '10px 20px',
      fontSize: katta ? '16px' : '14px',
      border: 'none', borderRadius: '10px', fontWeight: '700', cursor: 'pointer',
      transition: 'opacity 0.2s'
    }}
    onMouseEnter={e => e.target.style.opacity = '0.85'}
    onMouseLeave={e => e.target.style.opacity = '1'}
    >
      {matn}
    </button>
  )
}
export default Tugma
```

```jsx
// src/components/Alert.jsx — Vazifa 3 (children props)
function Alert({ turi = 'ma\'lumot', children }) {
  const stillar = {
    muvaffaqiyat: { background: '#d1fae5', color: '#065f46', border: '#a7f3d0' },
    xavf:         { background: '#fee2e2', color: '#991b1b', border: '#fca5a5' },
    ogohlantirish:{ background: '#fef3c7', color: '#92400e', border: '#fcd34d' },
    "ma'lumot":   { background: '#dbeafe', color: '#1e40af', border: '#93c5fd' },
  }
  const s = stillar[turi] || stillar["ma'lumot"]
  return (
    <div style={{ background: s.background, color: s.color, border: `1px solid ${s.border}`, padding: '12px 16px', borderRadius: '10px', marginBottom: '10px', fontSize: '14px' }}>
      {children}
    </div>
  )
}
export default Alert
```

```jsx
// src/components/StatistikKarta.jsx — Vazifa 4-5
function StatistikKarta({ belgi, qiymat, nom }) {
  return (
    <div style={{ background: 'white', borderRadius: '14px', padding: '24px', textAlign: 'center', boxShadow: '0 2px 12px rgba(0,0,0,0.06)' }}>
      <div style={{ fontSize: '32px', marginBottom: '8px' }}>{belgi}</div>
      <div style={{ fontSize: '26px', fontWeight: '800', color: 'royalblue', marginBottom: '4px' }}>{qiymat}</div>
      <div style={{ fontSize: '13px', color: '#888' }}>{nom}</div>
    </div>
  )
}
export default StatistikKarta
```

```jsx
// src/components/ProfileKarta.jsx — Vazifa 6-8
function ProfileKarta({ ism, lavozim, rang, emoji, reyting, tajriba }) {
  return (
    <div style={{ background: 'white', borderRadius: '16px', padding: '24px', boxShadow: '0 4px 20px rgba(0,0,0,0.07)', textAlign: 'center' }}>
      <div style={{ width: '72px', height: '72px', borderRadius: '50%', background: rang, color: 'white', display: 'flex', alignItems: 'center', justifyContent: 'center', fontSize: '36px', margin: '0 auto 14px' }}>
        {emoji}
      </div>
      <h3 style={{ marginBottom: '4px' }}>{ism}</h3>
      <p style={{ color: '#888', fontSize: '13px', marginBottom: '12px' }}>{lavozim}</p>
      <div style={{ color: '#f59e0b', marginBottom: '12px' }}>
        {'★'.repeat(reyting)}{'☆'.repeat(5 - reyting)}
      </div>
      <span style={{ background: '#f0f4ff', color: 'royalblue', padding: '4px 12px', borderRadius: '20px', fontSize: '12px', fontWeight: '700' }}>
        {tajriba} tajriba
      </span>
    </div>
  )
}
export default ProfileKarta
```

```jsx
// src/components/FigureKarta.jsx — Vazifa 9-10
function FigureKarta({ rasm, sarlavha, tavsif, yoyilma }) {
  return (
    <figure style={{ margin: 0, background: 'white', borderRadius: '16px', overflow: 'hidden', boxShadow: '0 4px 20px rgba(0,0,0,0.08)' }}>
      <img src={rasm} alt={sarlavha} loading="lazy"
           style={{ width: '100%', height: '180px', objectFit: 'cover', display: 'block' }} />
      <figcaption style={{ padding: '18px' }}>
        <h3 style={{ marginBottom: '6px' }}>{sarlavha}</h3>
        <p style={{ color: '#666', fontSize: '13px', marginBottom: '10px', lineHeight: 1.6 }}>{tavsif}</p>
        <span style={{ fontSize: '12px', color: '#888' }}>📍 {yoyilma}</span>
      </figcaption>
    </figure>
  )
}
export default FigureKarta
```
