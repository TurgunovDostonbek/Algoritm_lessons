# 13-Dars: React Router Part 3 (Amaliyot)

## 📌 Bu Darsda Nimalarni Mustahkamlaymiz?

| Mavzu | Tavsif |
|-------|--------|
| **Single Route** | Oddiy va dinamik route'lar |
| **Nested Routes** | Ichma-ich layout'lar |
| **404 Error** | NotFound sahifasi |
| **Loading** | Skeleton va Spinner |
| **Uyga vazifa** | Landing Page loyihasi |

> Bu dars — oldingi 2 ta darsning **amaliy mustahkamlash** darsi. Barcha tushunchalarni bitta loyihada birlashtiramiz.

---

## 📌 Loyiha Strukturasi

```
src/
├── components/
│   ├── Navbar.jsx
│   ├── Footer.jsx
│   ├── LoadingSpinner.jsx
│   └── SkeletonCard.jsx
├── layouts/
│   └── MainLayout.jsx
├── pages/
│   ├── Home.jsx
│   ├── Products.jsx
│   ├── ProductDetail.jsx
│   ├── About.jsx
│   ├── Contact.jsx
│   └── NotFound.jsx
├── App.jsx
└── main.jsx
```

---

## 📌 1-Qadam: main.jsx — BrowserRouter

```jsx
// src/main.jsx
import ReactDOM from 'react-dom/client'
import { BrowserRouter } from 'react-router-dom'
import App from './App'
import './index.css'

ReactDOM.createRoot(document.getElementById('root')).render(
  <BrowserRouter>
    <App />
  </BrowserRouter>
)
```

---

## 📌 2-Qadam: App.jsx — Routes

```jsx
// src/App.jsx
import { Routes, Route } from 'react-router-dom'
import MainLayout from './layouts/MainLayout'
import Home from './pages/Home'
import Products from './pages/Products'
import ProductDetail from './pages/ProductDetail'
import About from './pages/About'
import Contact from './pages/Contact'
import NotFound from './pages/NotFound'

function App() {
  return (
    <Routes>
      {/* MainLayout — Navbar + Outlet + Footer */}
      <Route element={<MainLayout />}>
        <Route path="/" element={<Home />} />
        <Route path="/products" element={<Products />} />
        <Route path="/products/:id" element={<ProductDetail />} />
        <Route path="/about" element={<About />} />
        <Route path="/contact" element={<Contact />} />
        <Route path="*" element={<NotFound />} />
      </Route>
    </Routes>
  )
}

export default App
```

---

## 📌 3-Qadam: MainLayout — Outlet bilan

```jsx
// src/layouts/MainLayout.jsx
import { Outlet } from 'react-router-dom'
import Navbar from '../components/Navbar'
import Footer from '../components/Footer'

function MainLayout() {
  return (
    <div style={{ minHeight: '100vh', display: 'flex', flexDirection: 'column', background: '#f8f9fa', fontFamily: "'Segoe UI', sans-serif" }}>
      <Navbar />
      <main style={{ flex: 1, maxWidth: '1100px', width: '100%', margin: '0 auto', padding: '32px 20px' }}>
        <Outlet />
      </main>
      <Footer />
    </div>
  )
}

export default MainLayout
```

---

## 📌 4-Qadam: Navbar — NavLink bilan

```jsx
// src/components/Navbar.jsx
import { NavLink } from 'react-router-dom'

const havolalar = [
  { yo_l: '/', nom: '🏠 Bosh sahifa' },
  { yo_l: '/products', nom: '📦 Mahsulotlar' },
  { yo_l: '/about', nom: 'ℹ️ Haqida' },
  { yo_l: '/contact', nom: '📞 Aloqa' },
]

function Navbar() {
  return (
    <nav style={{
      background: 'linear-gradient(135deg, #1a1a2e, #16213e)',
      padding: '0 40px', height: '64px',
      display: 'flex', alignItems: 'center', gap: '8px',
      boxShadow: '0 2px 20px rgba(0,0,0,0.15)',
    }}>
      <span style={{ color: 'white', fontWeight: '900', fontSize: '20px', marginRight: 'auto' }}>
        ⚡ MySite
      </span>

      {havolalar.map((h) => (
        <NavLink
          key={h.yo_l}
          to={h.yo_l}
          end={h.yo_l === '/'}
          style={({ isActive }) => ({
            color: isActive ? '#fff' : 'rgba(255,255,255,0.6)',
            textDecoration: 'none',
            padding: '8px 16px',
            borderRadius: '8px',
            background: isActive ? 'rgba(255,255,255,0.15)' : 'transparent',
            fontWeight: isActive ? '700' : '400',
            fontSize: '14px',
            transition: 'all 0.2s',
          })}
        >
          {h.nom}
        </NavLink>
      ))}
    </nav>
  )
}

export default Navbar
```

---

## 📌 5-Qadam: Footer

```jsx
// src/components/Footer.jsx
function Footer() {
  return (
    <footer style={{
      background: '#1a1a2e', color: 'rgba(255,255,255,0.5)',
      textAlign: 'center', padding: '24px 20px', fontSize: '13px',
    }}>
      <p>© 2025 MySite — React Router bilan yaratilgan</p>
    </footer>
  )
}

export default Footer
```

---

## 📌 6-Qadam: Loading Komponentlar

```jsx
// src/components/LoadingSpinner.jsx
function LoadingSpinner({ text = 'Yuklanmoqda...' }) {
  return (
    <div style={{ textAlign: 'center', padding: '80px 20px' }}>
      <div style={{
        width: '44px', height: '44px', margin: '0 auto 16px',
        border: '4px solid #e5e7eb', borderTopColor: 'royalblue',
        borderRadius: '50%', animation: 'spin 0.8s linear infinite',
      }} />
      <p style={{ color: '#888' }}>{text}</p>
      <style>{`@keyframes spin { to { transform: rotate(360deg) } }`}</style>
    </div>
  )
}

export default LoadingSpinner
```

```jsx
// src/components/SkeletonCard.jsx
function SkeletonCard() {
  return (
    <div style={{
      background: 'white', borderRadius: '16px',
      overflow: 'hidden', boxShadow: '0 2px 12px rgba(0,0,0,0.06)',
    }}>
      <div style={{
        height: '180px',
        background: 'linear-gradient(90deg, #f0f0f0 25%, #e0e0e0 50%, #f0f0f0 75%)',
        backgroundSize: '200% 100%', animation: 'shimmer 1.5s infinite',
      }} />
      <div style={{ padding: '16px' }}>
        {[80, 60, 40].map((w) => (
          <div key={w} style={{
            height: '14px', background: '#f0f0f0',
            borderRadius: '4px', width: `${w}%`, marginBottom: '10px',
          }} />
        ))}
      </div>
      <style>{`@keyframes shimmer { 0%{background-position:200% 0} 100%{background-position:-200% 0} }`}</style>
    </div>
  )
}

export default SkeletonCard
```

---

## 📌 7-Qadam: Home sahifasi

```jsx
// src/pages/Home.jsx
import { Link } from 'react-router-dom'

function Home() {
  return (
    <div>
      {/* Hero */}
      <div style={{
        background: 'linear-gradient(135deg, #667eea, #764ba2)',
        borderRadius: '20px', padding: '60px 40px',
        color: 'white', textAlign: 'center', marginBottom: '40px',
      }}>
        <h1 style={{ fontSize: '42px', fontWeight: '900', marginBottom: '16px' }}>
          React Router DOM
        </h1>
        <p style={{ fontSize: '18px', opacity: 0.85, marginBottom: '28px' }}>
          SPA navigatsiyani o'rganamiz — sahifa qayta yuklanmasdan!
        </p>
        <Link to="/products" style={{
          background: 'white', color: '#764ba2', padding: '14px 32px',
          borderRadius: '12px', fontWeight: '800', textDecoration: 'none',
          fontSize: '16px',
        }}>
          Mahsulotlarni ko'rish →
        </Link>
      </div>

      {/* Statistika */}
      <div style={{ display: 'grid', gridTemplateColumns: 'repeat(3, 1fr)', gap: '16px' }}>
        {[
          { belgi: '📦', son: '150+', nom: 'Mahsulotlar' },
          { belgi: '👥', son: '1200+', nom: 'Mijozlar' },
          { belgi: '⭐', son: '4.9', nom: 'Reyting' },
        ].map((s) => (
          <div key={s.nom} style={{
            background: 'white', borderRadius: '16px', padding: '28px',
            textAlign: 'center', boxShadow: '0 2px 12px rgba(0,0,0,0.06)',
          }}>
            <div style={{ fontSize: '32px', marginBottom: '8px' }}>{s.belgi}</div>
            <div style={{ fontSize: '28px', fontWeight: '900', color: '#1a1a2e' }}>{s.son}</div>
            <div style={{ color: '#888', fontSize: '14px' }}>{s.nom}</div>
          </div>
        ))}
      </div>
    </div>
  )
}

export default Home
```

---

## 📌 8-Qadam: Products — Skeleton Loading bilan

```jsx
// src/pages/Products.jsx
import { useState, useEffect } from 'react'
import { Link } from 'react-router-dom'
import SkeletonCard from '../components/SkeletonCard'

function Products() {
  const [mahsulotlar, setMahsulotlar] = useState([])
  const [yuklanyapti, setYuklanyapti] = useState(true)
  const [xato, setXato] = useState(null)

  useEffect(() => {
    fetch('https://dummyjson.com/products?limit=12')
      .then(res => {
        if (!res.ok) throw new Error('Server xatosi!')
        return res.json()
      })
      .then(data => setMahsulotlar(data.products))
      .catch(err => setXato(err.message))
      .finally(() => setYuklanyapti(false))
  }, [])

  if (xato) {
    return (
      <div style={{ textAlign: 'center', padding: '60px' }}>
        <div style={{ fontSize: '48px' }}>❌</div>
        <h3>Xato: {xato}</h3>
        <button onClick={() => window.location.reload()}>🔄 Qayta urinish</button>
      </div>
    )
  }

  return (
    <div>
      <h2 style={{ marginBottom: '24px' }}>📦 Mahsulotlar</h2>
      <div style={{
        display: 'grid',
        gridTemplateColumns: 'repeat(auto-fill, minmax(240px, 1fr))',
        gap: '20px',
      }}>
        {yuklanyapti
          ? Array(8).fill(0).map((_, i) => <SkeletonCard key={i} />)
          : mahsulotlar.map(m => (
            <Link to={`/products/${m.id}`} key={m.id} style={{ textDecoration: 'none', color: 'inherit' }}>
              <div style={{
                background: 'white', borderRadius: '16px', overflow: 'hidden',
                boxShadow: '0 2px 12px rgba(0,0,0,0.06)', transition: 'transform 0.2s',
              }}
                onMouseEnter={e => e.currentTarget.style.transform = 'translateY(-4px)'}
                onMouseLeave={e => e.currentTarget.style.transform = 'translateY(0)'}
              >
                <img src={m.thumbnail} alt={m.title} style={{ width: '100%', height: '180px', objectFit: 'cover' }} />
                <div style={{ padding: '16px' }}>
                  <p style={{ fontSize: '12px', color: '#888', textTransform: 'capitalize' }}>{m.category}</p>
                  <h3 style={{ fontSize: '14px', margin: '6px 0 10px', lineHeight: 1.4 }}>{m.title}</h3>
                  <div style={{ display: 'flex', justifyContent: 'space-between', alignItems: 'center' }}>
                    <span style={{ fontWeight: '800', fontSize: '18px', color: 'royalblue' }}>${m.price}</span>
                    <span style={{ fontSize: '12px', color: '#f59e0b' }}>⭐ {m.rating}</span>
                  </div>
                </div>
              </div>
            </Link>
          ))
        }
      </div>
    </div>
  )
}

export default Products
```

---

## 📌 9-Qadam: ProductDetail — useParams + Loading

```jsx
// src/pages/ProductDetail.jsx
import { useParams, useNavigate } from 'react-router-dom'
import { useState, useEffect } from 'react'
import LoadingSpinner from '../components/LoadingSpinner'

function ProductDetail() {
  const { id } = useParams()
  const navigate = useNavigate()
  const [mahsulot, setMahsulot] = useState(null)
  const [yuklanyapti, setYuklanyapti] = useState(true)
  const [xato, setXato] = useState(null)

  useEffect(() => {
    setYuklanyapti(true)
    fetch(`https://dummyjson.com/products/${id}`)
      .then(res => {
        if (!res.ok) throw new Error('Mahsulot topilmadi!')
        return res.json()
      })
      .then(data => setMahsulot(data))
      .catch(err => setXato(err.message))
      .finally(() => setYuklanyapti(false))
  }, [id])

  if (yuklanyapti) return <LoadingSpinner text="Mahsulot yuklanmoqda..." />

  if (xato) {
    return (
      <div style={{ textAlign: 'center', padding: '60px' }}>
        <div style={{ fontSize: '48px' }}>❌</div>
        <h3>{xato}</h3>
        <button onClick={() => navigate('/products')} style={{
          marginTop: '16px', padding: '10px 24px', background: 'royalblue',
          color: 'white', border: 'none', borderRadius: '8px', cursor: 'pointer',
        }}>← Mahsulotlarga qaytish</button>
      </div>
    )
  }

  return (
    <div>
      <button onClick={() => navigate(-1)} style={{
        background: '#f3f4f6', border: 'none', padding: '10px 20px',
        borderRadius: '8px', cursor: 'pointer', fontWeight: '600', marginBottom: '24px',
      }}>← Orqaga</button>

      <div style={{ display: 'grid', gridTemplateColumns: '1fr 1fr', gap: '40px', background: 'white', borderRadius: '20px', padding: '32px', boxShadow: '0 4px 20px rgba(0,0,0,0.06)' }}>
        <img src={mahsulot.thumbnail} alt={mahsulot.title} style={{ width: '100%', borderRadius: '16px', objectFit: 'cover' }} />
        <div>
          <span style={{ fontSize: '12px', color: '#888', textTransform: 'capitalize', background: '#f3f4f6', padding: '4px 12px', borderRadius: '20px' }}>{mahsulot.category}</span>
          <h1 style={{ fontSize: '28px', margin: '16px 0 12px', fontWeight: '800' }}>{mahsulot.title}</h1>
          <p style={{ color: '#666', lineHeight: 1.7, marginBottom: '20px' }}>{mahsulot.description}</p>
          <div style={{ display: 'flex', alignItems: 'center', gap: '16px', marginBottom: '20px' }}>
            <span style={{ fontSize: '32px', fontWeight: '900', color: 'royalblue' }}>${mahsulot.price}</span>
            <span style={{ color: '#f59e0b', fontSize: '16px' }}>⭐ {mahsulot.rating}</span>
            <span style={{ color: '#888', fontSize: '14px' }}>{mahsulot.stock} ta qoldi</span>
          </div>
          <button style={{
            background: 'royalblue', color: 'white', border: 'none',
            padding: '14px 32px', borderRadius: '12px', fontWeight: '700',
            fontSize: '16px', cursor: 'pointer', width: '100%',
          }}>🛒 Savatchaga qo'shish</button>
        </div>
      </div>
    </div>
  )
}

export default ProductDetail
```

---

## 📌 10-Qadam: NotFound — 404 Sahifa

```jsx
// src/pages/NotFound.jsx
import { Link, useNavigate } from 'react-router-dom'

function NotFound() {
  const navigate = useNavigate()

  return (
    <div style={{ textAlign: 'center', padding: '80px 20px' }}>
      <div style={{ fontSize: '80px', marginBottom: '16px' }}>🔍</div>
      <h1 style={{
        fontSize: '96px', fontWeight: '900',
        background: 'linear-gradient(135deg, #e63946, #f77f00)',
        WebkitBackgroundClip: 'text', WebkitTextFillColor: 'transparent',
      }}>404</h1>
      <p style={{ fontSize: '20px', color: '#555', marginBottom: '8px' }}>Sahifa topilmadi!</p>
      <p style={{ color: '#888', marginBottom: '32px' }}>Kechirasiz, siz qidirayotgan sahifa mavjud emas.</p>
      <div style={{ display: 'flex', gap: '12px', justifyContent: 'center' }}>
        <button onClick={() => navigate(-1)} style={{
          padding: '12px 24px', borderRadius: '10px', border: '2px solid #e5e7eb',
          background: 'white', cursor: 'pointer', fontWeight: '700',
        }}>← Orqaga</button>
        <Link to="/" style={{
          padding: '12px 24px', borderRadius: '10px', background: 'royalblue',
          color: 'white', textDecoration: 'none', fontWeight: '700',
        }}>🏠 Bosh sahifa</Link>
      </div>
    </div>
  )
}

export default NotFound
```

---

## 📌 About va Contact sahifalari

```jsx
// src/pages/About.jsx
function About() {
  return (
    <div style={{ background: 'white', borderRadius: '20px', padding: '40px', boxShadow: '0 2px 12px rgba(0,0,0,0.06)' }}>
      <h2 style={{ marginBottom: '16px' }}>ℹ️ Biz Haqimizda</h2>
      <p style={{ color: '#555', lineHeight: 1.8 }}>
        Biz zamonaviy texnologiyalar bilan ishlaydigan jamoamiz.
        React, Node.js va boshqa texnologiyalar bo'yicha tajribamiz bor.
      </p>
    </div>
  )
}
export default About

// src/pages/Contact.jsx
function Contact() {
  return (
    <div style={{ background: 'white', borderRadius: '20px', padding: '40px', boxShadow: '0 2px 12px rgba(0,0,0,0.06)' }}>
      <h2 style={{ marginBottom: '24px' }}>📞 Biz bilan bog'laning</h2>
      <form style={{ display: 'flex', flexDirection: 'column', gap: '16px', maxWidth: '500px' }}>
        <input placeholder="Ismingiz" style={{ padding: '12px 16px', border: '2px solid #e5e7eb', borderRadius: '10px', fontSize: '14px', outline: 'none' }} />
        <input type="email" placeholder="Email" style={{ padding: '12px 16px', border: '2px solid #e5e7eb', borderRadius: '10px', fontSize: '14px', outline: 'none' }} />
        <textarea placeholder="Xabar" rows="4" style={{ padding: '12px 16px', border: '2px solid #e5e7eb', borderRadius: '10px', fontSize: '14px', outline: 'none', resize: 'vertical' }} />
        <button type="button" style={{ padding: '14px', background: 'royalblue', color: 'white', border: 'none', borderRadius: '10px', fontWeight: '700', cursor: 'pointer' }}>
          Yuborish →
        </button>
      </form>
    </div>
  )
}
export default Contact
```

---

## 📌 Xulosa — Barcha Router Tushunchalari

| # | Tushuncha | Import | Ishlatish |
|---|-----------|--------|-----------|
| 1 | `BrowserRouter` | `main.jsx` | Ilovani o'raydi |
| 2 | `Routes` + `Route` | `App.jsx` | Sahifalar belgilash |
| 3 | `Link` | Komponentlar | Oddiy havola |
| 4 | `NavLink` | Navbar | Aktiv sahifa |
| 5 | `Outlet` | Layout | Child route joy |
| 6 | `useParams` | Detail sahifa | URL parametr olish |
| 7 | `useNavigate` | Har qayerda | Koddan navigatsiya |
| 8 | `path="*"` | Routes ichida | 404 sahifa |
| 9 | `index` | Nested route | Default child |
| 10 | `end` | NavLink | Aniq mos kelish |

---

## 🎯 10 ta Amaliy Vazifa

### Vazifa 1: Oddiy Landing Page
**⭐** — 3 sahifali sayt: Home (hero), About, Contact. Navbar + Footer + Layout.

---

### Vazifa 2: Mahsulotlar Katalogi
**⭐⭐** — `/products` (ro'yxat) + `/products/:id` (detail). API: `dummyjson.com/products`. Skeleton loading.

---

### Vazifa 3: Blog Platformasi
**⭐⭐** — `/blog` (postlar) + `/blog/:id` (post detail). API: `dummyjson.com/posts`. Loading + 404.

---

### Vazifa 4: Foydalanuvchilar Paneli
**⭐⭐** — `/users` (ro'yxat) + `/users/:id` (profil). API: `dummyjson.com/users`. Orqaga tugma.

---

### Vazifa 5: Dashboard + Nested Routes
**⭐⭐⭐** — Sidebar layout: `/dashboard` (index), `/dashboard/analytics`, `/dashboard/users`, `/dashboard/settings`.

---

### Vazifa 6: Restaurant Sayti
**⭐⭐⭐** — Home, Menu (`/menu`), Menu item (`/menu/:id`), About, Contact. Chiroyli dizayn.

---

### Vazifa 7: Online Kurs Platformasi
**⭐⭐⭐** — Kurslar ro'yxati, kurs detail, darslar nested route. API dan yoki statik data.

---

### Vazifa 8: Portfolio + Blog
**⭐⭐⭐⭐** — Home, Projects, Project Detail, Blog, Blog Post, About, Contact. 2 ta layout.

---

### Vazifa 9: Admin Panel
**⭐⭐⭐⭐** — Public layout (Home, Login) + Admin layout (Dashboard, Products CRUD, Users, Settings). useNavigate bilan login.

---

### Vazifa 10: To'liq Landing Page (Uyga Vazifa)
**⭐⭐⭐⭐⭐**

Professional landing page yarating — login sahifasidan navigatedan foydalanib, home page ga o'tish:

```
Sahifalar:
├── /                → Home (Hero + Features + Testimonials)
├── /products        → Mahsulotlar (API + Skeleton)
├── /products/:id    → Mahsulot batafsil (Spinner)
├── /about           → Kompaniya haqida
├── /contact         → Aloqa formasi
├── /login           → Login → navigate('/') ga
├── *                → 404 sahifa

Talablar:
✅ MainLayout (Navbar + Outlet + Footer)
✅ NavLink — aktiv sahifa belgilansin
✅ useParams — mahsulot detail
✅ useNavigate — login dan home ga, orqaga tugma
✅ Skeleton + Spinner loading
✅ 404 sahifa (gradient, animatsiya)
✅ Responsive dizayn
✅ API: https://dummyjson.com
```
