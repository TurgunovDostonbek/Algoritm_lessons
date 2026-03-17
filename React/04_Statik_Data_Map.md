# 04-Dars: Statik Data va uni map lash

## 📌 Statik Data nima?

**Statik data** — dasturda to'g'ridan-to'g'ri yozilgan, o'zgarmaydigan ma'lumotlar. Server yoki API dan kelmaydigan.

```jsx
// Statik data turlari:

// 1. Massiv (Array)
const mevalar = ['Olma', 'Nok', 'Banan', 'Uzum']

// 2. Ob'ektlar massivi
const foydalanuvchilar = [
  { id: 1, ism: 'Ali', yosh: 22, kasb: 'Dasturchи' },
  { id: 2, ism: 'Malika', yosh: 25, kasb: 'Dizayner' },
  { id: 3, ism: 'Jasur', yosh: 20, kasb: 'Student' },
]

// 3. Alohida fayl (ma'qul yo'l)
// src/data/mahsulotlar.js
export const mahsulotlar = [
  { id: 1, nom: 'Laptop', narxi: 12500000, rasm: '...' },
  { id: 2, nom: 'Telefon', narxi: 8900000, rasm: '...' },
]
```

---

## 📌 `.map()` bilan Ro'yxat Renderlash

```jsx
// Asosiy sintaksis
const mevalar = ['Olma', 'Nok', 'Banan']

function MevaRoyhat() {
  return (
    <ul>
      {mevalar.map((meva) => (
        <li key={meva}>{meva}</li>   // key — MAJBURIY!
      ))}
    </ul>
  )
}
```

---

## 📌 `key` prop — Nima Uchun Kerak?

```jsx
// ❌ key yo'q — React xato beradi va sekinlashadi
{mevalar.map((meva) => (
  <li>{meva}</li>    // Warning: Each child in a list should have a unique "key"
))}

// ✅ Unikal key
{mahsulotlar.map((m) => (
  <div key={m.id}>{m.nom}</div>          // id — eng yaxshi variant
))}

{mevalar.map((meva) => (
  <li key={meva}>{meva}</li>             // Qiymat unikal bo'lsa
))}

// ⚠️ index — oxirgi variant (to'g'ri, lekin muammoli bo'lishi mumkin)
{mevalar.map((meva, index) => (
  <li key={index}>{meva}</li>            // Massiv o'zgarmasa ishlaydi
))}
```

---

## 📌 `.filter()` va `.map()` Birgalikda

```jsx
const mahsulotlar = [
  { id: 1, nom: 'Laptop', narxi: 12500000, kategoriya: 'Elektronika' },
  { id: 2, nom: 'Telefon', narxi: 8900000, kategoriya: 'Elektronika' },
  { id: 3, nom: 'Kitob', narxi: 50000, kategoriya: 'Ta\'lim' },
  { id: 4, nom: 'Kurs', narxi: 499000, kategoriya: 'Ta\'lim' },
]

// Faqat Elektronika mahsulotlarini ko'rsatish
function ElektronikaMahsulotlar() {
  return (
    <div>
      {mahsulotlar
        .filter((m) => m.kategoriya === 'Elektronika')
        .map((m) => (
          <div key={m.id}>
            <h3>{m.nom}</h3>
            <p>{m.narxi.toLocaleString()} so'm</p>
          </div>
        ))
      }
    </div>
  )
}
```

---

## 🎯 10 ta Amaliy Vazifa — Static Data tuzib uni maplab kelish

```jsx
// src/data/data.js — Barcha statik ma'lumotlar
export const mahsulotlar = [
  { id: 1, nom: 'MacBook Pro 14"', narxi: 45000000, rang: 'Space Gray', kategoriya: 'Laptop', rasm: 'https://picsum.photos/300/200?random=1', reyting: 4.9, soni: 12 },
  { id: 2, nom: 'iPhone 15 Pro', narxi: 18900000, rang: 'Titanium', kategoriya: 'Telefon', rasm: 'https://picsum.photos/300/200?random=2', reyting: 4.8, soni: 0 },
  { id: 3, nom: 'Samsung 4K TV', narxi: 9800000, rang: 'Qora', kategoriya: 'TV', rasm: 'https://picsum.photos/300/200?random=3', reyting: 4.6, soni: 5 },
  { id: 4, nom: 'AirPods Pro', narxi: 4200000, rang: 'Oq', kategoriya: 'Audio', rasm: 'https://picsum.photos/300/200?random=4', reyting: 4.7, soni: 23 },
  { id: 5, nom: 'iPad Air', narxi: 11500000, rang: 'Ko\'k', kategoriya: 'Tablet', rasm: 'https://picsum.photos/300/200?random=5', reyting: 4.5, soni: 8 },
  { id: 6, nom: 'Dell XPS 15', narxi: 32000000, rang: 'Kumush', kategoriya: 'Laptop', rasm: 'https://picsum.photos/300/200?random=6', reyting: 4.7, soni: 3 },
]

export const foydalanuvchilar = [
  { id: 1, ism: 'Ali Valiev', lavozim: 'Frontend Developer', yulduz: 5, avatar: 'A', rang: '#4361ee' },
  { id: 2, ism: 'Malika Saidova', lavozim: 'UI/UX Designer', yulduz: 5, avatar: 'M', rang: '#e63946' },
  { id: 3, ism: 'Jasur Toshmatov', lavozim: 'Backend Developer', yulduz: 4, avatar: 'J', rang: '#10b981' },
  { id: 4, ism: 'Nilufar Karimova', lavozim: 'Product Manager', yulduz: 4, avatar: 'N', rang: '#f59e0b' },
  { id: 5, ism: 'Bobur Rahimov', lavozim: 'DevOps Engineer', yulduz: 3, avatar: 'B', rang: '#7c3aed' },
]

export const kategoriyalar = ['Hammasi', 'Laptop', 'Telefon', 'TV', 'Audio', 'Tablet']
```

```jsx
// src/App.jsx
import { mahsulotlar, foydalanuvchilar, kategoriyalar } from './data/data'

function YulduzReyting({ ball }) {
  return (
    <span style={{ color: '#f59e0b' }}>
      {[1,2,3,4,5].map((y) => (
        <span key={y}>{y <= ball ? '★' : '☆'}</span>
      ))}
    </span>
  )
}

function MahsulotKarta({ mahsulot }) {
  const mavjud = mahsulot.soni > 0
  return (
    <div style={{
      background: 'white', borderRadius: '16px', overflow: 'hidden',
      boxShadow: '0 4px 20px rgba(0,0,0,0.08)', transition: 'transform 0.2s'
    }}
    onMouseEnter={e => e.currentTarget.style.transform = 'translateY(-4px)'}
    onMouseLeave={e => e.currentTarget.style.transform = 'translateY(0)'}
    >
      {/* Vazifa 1: Rasm */}
      <div style={{ position: 'relative' }}>
        <img src={mahsulot.rasm} alt={mahsulot.nom} loading="lazy"
             style={{ width: '100%', height: '160px', objectFit: 'cover', display: 'block' }} />
        {/* Vazifa 2: Mavjudlik badge */}
        <span style={{
          position: 'absolute', top: '10px', right: '10px',
          background: mavjud ? '#d1fae5' : '#fee2e2',
          color: mavjud ? '#065f46' : '#991b1b',
          padding: '3px 10px', borderRadius: '20px', fontSize: '11px', fontWeight: '700'
        }}>
          {mavjud ? `✅ ${mahsulot.soni} ta` : '❌ Tugagan'}
        </span>
      </div>

      <div style={{ padding: '16px' }}>
        <div style={{ fontSize: '11px', color: '#888', marginBottom: '4px' }}>{mahsulot.kategoriya}</div>
        <h3 style={{ fontSize: '15px', marginBottom: '6px' }}>{mahsulot.nom}</h3>
        <div style={{ fontSize: '12px', color: '#666', marginBottom: '8px' }}>Rang: {mahsulot.rang}</div>

        {/* Vazifa 3: Yulduz reyting — map bilan */}
        <div style={{ display: 'flex', alignItems: 'center', gap: '6px', marginBottom: '12px' }}>
          <YulduzReyting ball={Math.round(mahsulot.reyting)} />
          <span style={{ fontSize: '13px', color: '#888' }}>{mahsulot.reyting}</span>
        </div>

        <div style={{ display: 'flex', justifyContent: 'space-between', alignItems: 'center' }}>
          <span style={{ fontWeight: '800', fontSize: '16px', color: 'royalblue' }}>
            {mahsulot.narxi.toLocaleString()} so'm
          </span>
          <button disabled={!mavjud} style={{
            background: mavjud ? 'royalblue' : '#e5e7eb',
            color: mavjud ? 'white' : '#9ca3af',
            border: 'none', padding: '8px 14px', borderRadius: '8px',
            fontSize: '13px', fontWeight: '700', cursor: mavjud ? 'pointer' : 'not-allowed'
          }}>
            Sotib Ol
          </button>
        </div>
      </div>
    </div>
  )
}

function App() {
  // Vazifa 4: Kategoriya filterlash
  const laptoplar = mahsulotlar.filter(m => m.kategoriya === 'Laptop')
  // Vazifa 5: Arzon mahsulotlar
  const arzonlar = mahsulotlar.filter(m => m.narxi < 10000000)
  // Vazifa 6: Mavjud mahsulotlar
  const mavjudlar = mahsulotlar.filter(m => m.soni > 0)

  return (
    <div style={{ minHeight: '100vh', background: '#f0f2f5', fontFamily: "'Segoe UI', sans-serif" }}>

      {/* HEADER */}
      <header style={{ background: '#1a1a2e', color: 'white', padding: '20px 40px' }}>
        <h1 style={{ fontSize: '24px' }}>🛒 TechShop — Statik Data Amaliyoti</h1>
        <p style={{ opacity: 0.7, fontSize: '14px', marginTop: '4px' }}>
          Jami {mahsulotlar.length} ta mahsulot •{' '}
          Mavjud: {mavjudlar.length} ta •{' '}
          Laptoplar: {laptoplar.length} ta
        </p>
      </header>

      <div style={{ maxWidth: '1100px', margin: '0 auto', padding: '40px 20px' }}>

        {/* Vazifa 7: Kategoriya pill lari — map */}
        <div style={{ display: 'flex', gap: '8px', flexWrap: 'wrap', marginBottom: '32px' }}>
          {kategoriyalar.map((kat, i) => (
            <span key={kat} style={{
              padding: '8px 18px', borderRadius: '20px', fontSize: '14px', fontWeight: '600',
              cursor: 'pointer', border: 'none',
              background: i === 0 ? 'royalblue' : 'white',
              color: i === 0 ? 'white' : '#555',
              boxShadow: '0 2px 8px rgba(0,0,0,0.06)'
            }}>
              {kat}
            </span>
          ))}
        </div>

        {/* Vazifa 1-6: Mahsulotlar grid */}
        <div style={{ display: 'grid', gridTemplateColumns: 'repeat(auto-fill, minmax(260px, 1fr))', gap: '20px', marginBottom: '60px' }}>
          {mahsulotlar.map((mahsulot) => (
            <MahsulotKarta key={mahsulot.id} mahsulot={mahsulot} />
          ))}
        </div>

        {/* Vazifa 8-10: Foydalanuvchilar jadval */}
        <section>
          <h2 style={{ fontSize: '22px', marginBottom: '20px' }}>👥 Jamoa A'zolari</h2>
          <div style={{ background: 'white', borderRadius: '16px', overflow: 'hidden', boxShadow: '0 4px 20px rgba(0,0,0,0.06)' }}>
            <table style={{ width: '100%', borderCollapse: 'collapse' }}>
              <thead>
                <tr style={{ background: '#1a1a2e', color: 'white' }}>
                  {/* Vazifa 8: Jadval sarlavhalari — map */}
                  {['#', 'Xodim', 'Lavozim', 'Reyting', 'Holati'].map((sarlavha) => (
                    <th key={sarlavha} style={{ padding: '14px 16px', textAlign: 'left', fontSize: '13px' }}>
                      {sarlavha}
                    </th>
                  ))}
                </tr>
              </thead>
              <tbody>
                {/* Vazifa 9: Foydalanuvchilar — map */}
                {foydalanuvchilar.map((user, index) => (
                  <tr key={user.id} style={{ borderBottom: '1px solid #f5f5f5', transition: 'background 0.15s' }}
                      onMouseEnter={e => e.currentTarget.style.background = '#f8f9ff'}
                      onMouseLeave={e => e.currentTarget.style.background = 'transparent'}>
                    <td style={{ padding: '14px 16px', color: '#888', fontSize: '14px' }}>{index + 1}</td>
                    <td style={{ padding: '14px 16px' }}>
                      <div style={{ display: 'flex', alignItems: 'center', gap: '10px' }}>
                        <div style={{
                          width: '36px', height: '36px', borderRadius: '50%',
                          background: user.rang, color: 'white', fontWeight: '700',
                          display: 'flex', alignItems: 'center', justifyContent: 'center', fontSize: '14px'
                        }}>
                          {user.avatar}
                        </div>
                        <span style={{ fontWeight: '600', fontSize: '14px' }}>{user.ism}</span>
                      </div>
                    </td>
                    <td style={{ padding: '14px 16px', color: '#666', fontSize: '14px' }}>{user.lavozim}</td>
                    {/* Vazifa 10: Yulduzlar — map ichida map */}
                    <td style={{ padding: '14px 16px' }}>
                      <YulduzReyting ball={user.yulduz} />
                    </td>
                    <td style={{ padding: '14px 16px' }}>
                      <span style={{
                        background: '#d1fae5', color: '#065f46',
                        padding: '4px 10px', borderRadius: '20px', fontSize: '12px', fontWeight: '600'
                      }}>
                        Aktiv
                      </span>
                    </td>
                  </tr>
                ))}
              </tbody>
            </table>
          </div>
        </section>

      </div>
    </div>
  )
}
export default App
```
