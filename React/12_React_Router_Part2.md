# 12-Dars: React Router Part 2

## 📌 Bu Darsda Nimalarni O'rganamiz?

| Mavzu | Tavsif |
|-------|--------|
| `useParams` | URL dan parametr olish (`:id`) |
| `useNavigate` | Koddan boshqa sahifaga yo'naltirish |
| **Nested Routes** | Ichma-ich (nested) route'lar |
| **404 Error** | Sahifa topilmadi xatosi |
| **Loading** | Yuklanish holati |

---

## 📌 useParams — URL dan Parametr Olish

URL da `:id` yoki `:slug` kabi dinamik qismlarni olish uchun ishlatiladi.

### Route belgilash:

```jsx
// src/App.jsx
import { Routes, Route } from 'react-router-dom'
import Products from './pages/Products'
import ProductDetail from './pages/ProductDetail'

function App() {
  return (
    <Routes>
      <Route path="/products" element={<Products />} />

      {/* :id — dinamik parametr */}
      <Route path="/products/:id" element={<ProductDetail />} />

      {/* Ko'p parametr ham bo'lishi mumkin */}
      <Route path="/shop/:category/:id" element={<ShopItem />} />
    </Routes>
  )
}
```

### Parametrni olish:

```jsx
// src/pages/ProductDetail.jsx
import { useParams } from 'react-router-dom'

function ProductDetail() {
  // URL: /products/5 → { id: "5" }
  const { id } = useParams()

  return (
    <div>
      <h2>Mahsulot ID: {id}</h2>
      <p>Bu mahsulot haqida batafsil ma'lumot...</p>
    </div>
  )
}

export default ProductDetail
```

### Ko'p parametrli misol:

```jsx
// Route: path="/shop/:category/:id"
// URL:   /shop/electronics/42

function ShopItem() {
  const { category, id } = useParams()
  // category = "electronics"
  // id = "42"

  return (
    <div>
      <p>Kategoriya: {category}</p>
      <p>ID: {id}</p>
    </div>
  )
}
```

---

## 📌 useParams + API dan Ma'lumot Olish

```jsx
// src/pages/ProductDetail.jsx
import { useParams } from 'react-router-dom'
import { useState, useEffect } from 'react'

function ProductDetail() {
  const { id } = useParams()
  const [mahsulot, setMahsulot] = useState(null)
  const [yuklanyapti, setYuklanyapti] = useState(true)
  const [xato, setXato] = useState(null)

  useEffect(() => {
    setYuklanyapti(true)
    setXato(null)

    fetch(`https://dummyjson.com/products/${id}`)
      .then(res => {
        if (!res.ok) throw new Error('Mahsulot topilmadi!')
        return res.json()
      })
      .then(data => setMahsulot(data))
      .catch(err => setXato(err.message))
      .finally(() => setYuklanyapti(false))
  }, [id])  // id o'zgarganda qayta so'rov

  if (yuklanyapti) return <p>⏳ Yuklanmoqda...</p>
  if (xato) return <p>❌ Xato: {xato}</p>
  if (!mahsulot) return <p>Mahsulot topilmadi</p>

  return (
    <div>
      <img src={mahsulot.thumbnail} alt={mahsulot.title} />
      <h2>{mahsulot.title}</h2>
      <p>{mahsulot.description}</p>
      <strong>${mahsulot.price}</strong>
    </div>
  )
}

export default ProductDetail
```

---

## 📌 useNavigate — Koddan Navigatsiya

`useNavigate` — foydalanuvchi amalidan keyin (masalan, forma yuborilsa) boshqa sahifaga yo'naltirish.

```jsx
import { useNavigate } from 'react-router-dom'

function LoginPage() {
  const navigate = useNavigate()

  function handleLogin() {
    // ... login logikasi

    // Muvaffaqiyatli bo'lsa → bosh sahifaga
    navigate('/')

    // yoki ma'lum sahifaga
    navigate('/dashboard')

    // Orqaga qaytish (brauzer "Back" tugmasi kabi)
    navigate(-1)

    // 2 qadam orqaga
    navigate(-2)

    // Oldinga
    navigate(1)
  }

  return (
    <div>
      <h2>Login</h2>
      <button onClick={handleLogin}>Kirish</button>
    </div>
  )
}
```

### navigate options:

```jsx
const navigate = useNavigate()

// Oddiy o'tish
navigate('/products')

// Tarixni almashtirish (orqaga qaytib bo'lmaydi)
navigate('/dashboard', { replace: true })

// Ma'lumot yuborish (state bilan)
navigate('/success', { state: { buyurtmaId: 123, xabar: 'Muvaffaqiyat!' } })
```

### State ni olish (useLocation):

```jsx
import { useLocation } from 'react-router-dom'

function SuccessPage() {
  const location = useLocation()
  const { buyurtmaId, xabar } = location.state || {}

  return (
    <div>
      <h2>✅ {xabar}</h2>
      <p>Buyurtma ID: {buyurtmaId}</p>
    </div>
  )
}
```

---

## 📌 useNavigate — Amaliy Misollar

### 1. Forma yuborilgandan keyin yo'naltirish:

```jsx
function ContactForm() {
  const navigate = useNavigate()
  const [yuborilmoqda, setYuborilmoqda] = useState(false)

  async function handleSubmit(e) {
    e.preventDefault()
    setYuborilmoqda(true)

    // API ga yuborish simulyatsiyasi
    await new Promise(r => setTimeout(r, 1500))

    // Muvaffaqiyat sahifasiga yo'naltirish
    navigate('/success', {
      state: { xabar: 'Xabaringiz yuborildi!' }
    })
  }

  return (
    <form onSubmit={handleSubmit}>
      <input placeholder="Ismingiz" required />
      <input placeholder="Email" type="email" required />
      <textarea placeholder="Xabar" required />
      <button disabled={yuborilmoqda}>
        {yuborilmoqda ? 'Yuborilmoqda...' : 'Yuborish'}
      </button>
    </form>
  )
}
```

### 2. O'chirish + orqaga qaytish:

```jsx
function ProductDetail() {
  const { id } = useParams()
  const navigate = useNavigate()

  async function handleDelete() {
    if (!window.confirm("O'chirasizmi?")) return

    await fetch(`https://dummyjson.com/products/${id}`, {
      method: 'DELETE'
    })

    // Mahsulotlar ro'yxatiga qaytish
    navigate('/products', { replace: true })
  }

  return (
    <div>
      <button onClick={() => navigate(-1)}>← Orqaga</button>
      <h2>Mahsulot #{id}</h2>
      <button onClick={handleDelete}>🗑 O'chirish</button>
    </div>
  )
}
```

---

## 📌 Nested Routes — Ichma-ich Route'lar

Bir sahifa ichida yana bir nechta sub-sahifalar bo'lishi mumkin.

### Oddiy misol:

```jsx
// src/App.jsx
import { Routes, Route } from 'react-router-dom'
import Dashboard from './pages/Dashboard'
import DashHome from './pages/DashHome'
import DashUsers from './pages/DashUsers'
import DashSettings from './pages/DashSettings'

function App() {
  return (
    <Routes>
      <Route path="/" element={<Home />} />

      {/* Nested Routes */}
      <Route path="/dashboard" element={<Dashboard />}>
        {/* index — /dashboard ga kirganda default ko'rinadi */}
        <Route index element={<DashHome />} />

        {/* /dashboard/users */}
        <Route path="users" element={<DashUsers />} />

        {/* /dashboard/settings */}
        <Route path="settings" element={<DashSettings />} />
      </Route>
    </Routes>
  )
}
```

### Parent komponent — Outlet bilan:

```jsx
// src/pages/Dashboard.jsx
import { NavLink, Outlet } from 'react-router-dom'

function Dashboard() {
  const linkStyle = ({ isActive }) => ({
    padding: '10px 20px',
    borderRadius: '8px',
    textDecoration: 'none',
    background: isActive ? 'royalblue' : '#f3f4f6',
    color: isActive ? 'white' : '#555',
    fontWeight: isActive ? '700' : '400',
  })

  return (
    <div style={{ display: 'flex', minHeight: '80vh' }}>
      {/* Sidebar */}
      <aside style={{
        width: '220px',
        background: '#1a1a2e',
        padding: '24px 16px',
        display: 'flex',
        flexDirection: 'column',
        gap: '8px',
      }}>
        <h3 style={{ color: 'white', marginBottom: '16px' }}>📊 Dashboard</h3>
        <NavLink to="/dashboard" end style={linkStyle}>🏠 Bosh</NavLink>
        <NavLink to="/dashboard/users" style={linkStyle}>👥 Foydalanuvchilar</NavLink>
        <NavLink to="/dashboard/settings" style={linkStyle}>⚙️ Sozlamalar</NavLink>
      </aside>

      {/* Kontent — ichki route shu yerda */}
      <main style={{ flex: 1, padding: '32px' }}>
        <Outlet />
      </main>
    </div>
  )
}

export default Dashboard
```

> **`end`** — NavLink da `end` qo'ymasak, `/dashboard/users` da ham "Bosh" aktiv bo'lib qoladi.

### Child sahifalar:

```jsx
// src/pages/DashHome.jsx
function DashHome() {
  return (
    <div>
      <h2>📊 Dashboard — Umumiy</h2>
      <div style={{ display: 'grid', gridTemplateColumns: 'repeat(3, 1fr)', gap: '16px' }}>
        <div style={{ background: '#e0f2fe', padding: '24px', borderRadius: '12px' }}>
          <h3>👥 150</h3>
          <p>Foydalanuvchilar</p>
        </div>
        <div style={{ background: '#d1fae5', padding: '24px', borderRadius: '12px' }}>
          <h3>📦 89</h3>
          <p>Buyurtmalar</p>
        </div>
        <div style={{ background: '#fef3c7', padding: '24px', borderRadius: '12px' }}>
          <h3>💰 $12,400</h3>
          <p>Daromad</p>
        </div>
      </div>
    </div>
  )
}

// src/pages/DashUsers.jsx
function DashUsers() {
  return (
    <div>
      <h2>👥 Foydalanuvchilar</h2>
      <p>Foydalanuvchilar ro'yxati...</p>
    </div>
  )
}

// src/pages/DashSettings.jsx
function DashSettings() {
  return (
    <div>
      <h2>⚙️ Sozlamalar</h2>
      <p>Sozlamalar sahifasi...</p>
    </div>
  )
}
```

---

## 📌 Nested Routes — Chuqurroq Darajalar

```jsx
<Routes>
  <Route path="/" element={<MainLayout />}>
    <Route index element={<Home />} />
    <Route path="about" element={<About />} />

    {/* 2-daraja: /products */}
    <Route path="products" element={<ProductsLayout />}>
      <Route index element={<ProductList />} />
      <Route path=":id" element={<ProductDetail />} />
      <Route path=":id/reviews" element={<ProductReviews />} />
    </Route>

    {/* 2-daraja: /dashboard */}
    <Route path="dashboard" element={<DashLayout />}>
      <Route index element={<DashHome />} />
      <Route path="users" element={<Users />} />
      <Route path="users/:userId" element={<UserDetail />} />
      <Route path="settings" element={<Settings />} />
    </Route>

    {/* 404 */}
    <Route path="*" element={<NotFound />} />
  </Route>
</Routes>
```

### URL'lar natijasi:

| URL | Ko'rinadigan komponent |
|-----|----------------------|
| `/` | MainLayout → Home |
| `/about` | MainLayout → About |
| `/products` | MainLayout → ProductsLayout → ProductList |
| `/products/5` | MainLayout → ProductsLayout → ProductDetail |
| `/products/5/reviews` | MainLayout → ProductsLayout → ProductReviews |
| `/dashboard` | MainLayout → DashLayout → DashHome |
| `/dashboard/users` | MainLayout → DashLayout → Users |
| `/dashboard/users/3` | MainLayout → DashLayout → UserDetail |
| `/asdfgh` | MainLayout → NotFound |

---

## 📌 404 Error Page — Sahifa Topilmadi

```jsx
// src/pages/NotFound.jsx
import { Link, useNavigate } from 'react-router-dom'

function NotFound() {
  const navigate = useNavigate()

  return (
    <div style={{
      textAlign: 'center',
      padding: '80px 20px',
      minHeight: '60vh',
      display: 'flex',
      flexDirection: 'column',
      alignItems: 'center',
      justifyContent: 'center',
    }}>
      <div style={{ fontSize: '120px', marginBottom: '16px' }}>🔍</div>
      <h1 style={{
        fontSize: '72px',
        fontWeight: '900',
        background: 'linear-gradient(135deg, #e63946, #f77f00)',
        WebkitBackgroundClip: 'text',
        WebkitTextFillColor: 'transparent',
        marginBottom: '12px',
      }}>
        404
      </h1>
      <p style={{ fontSize: '20px', color: '#555', marginBottom: '8px' }}>
        Sahifa topilmadi!
      </p>
      <p style={{ color: '#888', marginBottom: '32px' }}>
        Siz qidirayotgan sahifa mavjud emas yoki ko'chirilgan.
      </p>

      <div style={{ display: 'flex', gap: '12px' }}>
        <button
          onClick={() => navigate(-1)}
          style={{
            padding: '12px 24px', borderRadius: '10px', border: '2px solid #e5e7eb',
            background: 'white', cursor: 'pointer', fontWeight: '700', fontSize: '14px',
          }}
        >
          ← Orqaga
        </button>
        <Link
          to="/"
          style={{
            padding: '12px 24px', borderRadius: '10px', background: 'royalblue',
            color: 'white', textDecoration: 'none', fontWeight: '700', fontSize: '14px',
          }}
        >
          🏠 Bosh sahifa
        </Link>
      </div>
    </div>
  )
}

export default NotFound
```

### Route da ishlatish:

```jsx
<Routes>
  <Route path="/" element={<Home />} />
  <Route path="/about" element={<About />} />

  {/* ⬇️ Eng oxirida — boshqa hech narsa mos kelmasa */}
  <Route path="*" element={<NotFound />} />
</Routes>
```

---

## 📌 Loading — Yuklanish Holati

### Oddiy Loading:

```jsx
function Products() {
  const [mahsulotlar, setMahsulotlar] = useState([])
  const [yuklanyapti, setYuklanyapti] = useState(true)

  useEffect(() => {
    fetch('https://dummyjson.com/products?limit=12')
      .then(res => res.json())
      .then(data => setMahsulotlar(data.products))
      .finally(() => setYuklanyapti(false))
  }, [])

  // Loading holati
  if (yuklanyapti) {
    return (
      <div style={{ textAlign: 'center', padding: '60px' }}>
        <div style={{
          width: '40px', height: '40px',
          border: '4px solid #e5e7eb',
          borderTopColor: 'royalblue',
          borderRadius: '50%',
          animation: 'spin 0.8s linear infinite',
          margin: '0 auto 16px',
        }} />
        <p style={{ color: '#888' }}>Yuklanmoqda...</p>
        <style>{`@keyframes spin { to { transform: rotate(360deg) } }`}</style>
      </div>
    )
  }

  return (
    <div>
      {mahsulotlar.map(m => <div key={m.id}>{m.title}</div>)}
    </div>
  )
}
```

### Skeleton Loading (Silliq Yuklanish):

```jsx
function SkeletonCard() {
  return (
    <div style={{
      background: 'white',
      borderRadius: '16px',
      overflow: 'hidden',
      boxShadow: '0 2px 12px rgba(0,0,0,0.06)',
    }}>
      {/* Rasm skeleton */}
      <div style={{
        height: '180px',
        background: 'linear-gradient(90deg, #f0f0f0 25%, #e0e0e0 50%, #f0f0f0 75%)',
        backgroundSize: '200% 100%',
        animation: 'shimmer 1.5s infinite',
      }} />

      {/* Matn skeleton */}
      <div style={{ padding: '16px' }}>
        <div style={{ height: '16px', background: '#f0f0f0', borderRadius: '4px', width: '80%', marginBottom: '10px' }} />
        <div style={{ height: '14px', background: '#f0f0f0', borderRadius: '4px', width: '60%', marginBottom: '10px' }} />
        <div style={{ height: '14px', background: '#f0f0f0', borderRadius: '4px', width: '40%' }} />
      </div>

      <style>{`
        @keyframes shimmer {
          0% { background-position: 200% 0 }
          100% { background-position: -200% 0 }
        }
      `}</style>
    </div>
  )
}

// Ishlatish:
function Products() {
  const [mahsulotlar, setMahsulotlar] = useState([])
  const [yuklanyapti, setYuklanyapti] = useState(true)

  useEffect(() => {
    fetch('https://dummyjson.com/products?limit=8')
      .then(res => res.json())
      .then(data => setMahsulotlar(data.products))
      .finally(() => setYuklanyapti(false))
  }, [])

  return (
    <div style={{
      display: 'grid',
      gridTemplateColumns: 'repeat(auto-fill, minmax(240px, 1fr))',
      gap: '20px',
    }}>
      {yuklanyapti
        ? Array(8).fill(0).map((_, i) => <SkeletonCard key={i} />)
        : mahsulotlar.map(m => <ProductCard key={m.id} product={m} />)
      }
    </div>
  )
}
```

---

## 📌 Loading + Error + Empty holatlari birgalikda

```jsx
function ProductList() {
  const [mahsulotlar, setMahsulotlar] = useState([])
  const [yuklanyapti, setYuklanyapti] = useState(true)
  const [xato, setXato] = useState(null)

  useEffect(() => {
    setYuklanyapti(true)
    setXato(null)

    fetch('https://dummyjson.com/products?limit=12')
      .then(res => {
        if (!res.ok) throw new Error(`Server xatosi: ${res.status}`)
        return res.json()
      })
      .then(data => setMahsulotlar(data.products))
      .catch(err => setXato(err.message))
      .finally(() => setYuklanyapti(false))
  }, [])

  // 1️⃣ LOADING
  if (yuklanyapti) {
    return <LoadingSpinner />
  }

  // 2️⃣ ERROR
  if (xato) {
    return (
      <div style={{ textAlign: 'center', padding: '60px' }}>
        <div style={{ fontSize: '48px', marginBottom: '12px' }}>❌</div>
        <h3>Xato yuz berdi</h3>
        <p style={{ color: '#888' }}>{xato}</p>
        <button onClick={() => window.location.reload()}>
          🔄 Qayta urinish
        </button>
      </div>
    )
  }

  // 3️⃣ EMPTY
  if (mahsulotlar.length === 0) {
    return (
      <div style={{ textAlign: 'center', padding: '60px' }}>
        <div style={{ fontSize: '48px', marginBottom: '12px' }}>📭</div>
        <h3>Mahsulotlar topilmadi</h3>
        <p style={{ color: '#888' }}>Hozircha hech narsa yo'q</p>
      </div>
    )
  }

  // 4️⃣ SUCCESS — Ma'lumotlar ko'rsatish
  return (
    <div style={{ display: 'grid', gridTemplateColumns: 'repeat(auto-fill, minmax(240px, 1fr))', gap: '20px' }}>
      {mahsulotlar.map(m => (
        <ProductCard key={m.id} product={m} />
      ))}
    </div>
  )
}
```

---

## 📌 Barcha Hook'lar — Xulosa

```jsx
import {
  useParams,      // URL parametrlari: /products/:id → { id: "5" }
  useNavigate,    // Koddan navigatsiya: navigate('/home')
  useLocation,    // Joriy URL ma'lumotlari: pathname, search, state
  useSearchParams,// Query string: ?page=1&sort=name
} from 'react-router-dom'
```

| Hook | Nima qiladi | Misol |
|------|-------------|-------|
| `useParams()` | URL parametrini olish | `const { id } = useParams()` |
| `useNavigate()` | Sahifaga o'tish | `navigate('/home')` |
| `useLocation()` | Joriy URL ma'lumotlari | `location.pathname` |
| `useSearchParams()` | `?key=value` bilan ishlash | `searchParams.get('page')` |

### useSearchParams misol:

```jsx
// URL: /products?page=2&sort=price
import { useSearchParams } from 'react-router-dom'

function Products() {
  const [searchParams, setSearchParams] = useSearchParams()

  const page = Number(searchParams.get('page')) || 1
  const sort = searchParams.get('sort') || 'default'

  function keyingiSahifa() {
    setSearchParams({ page: page + 1, sort })
  }

  return (
    <div>
      <p>Sahifa: {page} | Tartiblash: {sort}</p>
      <button onClick={keyingiSahifa}>Keyingi →</button>
    </div>
  )
}
```

---

## 🎯 10 ta Amaliy Vazifa

### Vazifa 1: useParams bilan Foydalanuvchi Profili
**Qiyinlik:** ⭐

Foydalanuvchilar ro'yxati sahifasi va har bir foydalanuvchiga o'tganda uning profilini ko'rsating.

```
/users         → Foydalanuvchilar ro'yxati
/users/1       → Foydalanuvchi #1 profili
/users/2       → Foydalanuvchi #2 profili
```

```jsx
// Statik ma'lumotlar bilan ishlang:
const foydalanuvchilar = [
  { id: 1, ism: 'Ali', yosh: 22, kasb: 'Dasturchi' },
  { id: 2, ism: 'Vali', yosh: 25, kasb: 'Dizayner' },
  { id: 3, ism: 'Guli', yosh: 20, kasb: 'PM' },
]
```

---

### Vazifa 2: useParams + API (DummyJSON)
**Qiyinlik:** ⭐⭐

DummyJSON API dan mahsulot detalni olib ko'rsating.

```
/products         → Mahsulotlar ro'yxati (GET /products?limit=12)
/products/:id     → Bitta mahsulot (GET /products/:id)

Talablar:
✅ Ro'yxatda Link bilan har bir mahsulotga o'tish
✅ Detail sahifada: rasm, nom, narx, tavsif
✅ "← Orqaga" tugmasi (useNavigate(-1))
✅ Loading va Error holatlari
```

---

### Vazifa 3: useNavigate bilan Login Forma
**Qiyinlik:** ⭐⭐

Login sahifasi yarating — muvaffaqiyatli kirganda `/dashboard` ga yo'naltirsin.

```jsx
// Talablar:
// 1. Login formasi (email + parol)
// 2. "admin@mail.com" va "12345" to'g'ri bo'lsa → /dashboard
// 3. Noto'g'ri bo'lsa → xato xabari ko'rsatsin
// 4. Dashboard ga kirganda "Xush kelibsiz!" ko'rsatsin
// 5. Dashboard da "Chiqish" tugmasi → /login ga qaytarsin
```

---

### Vazifa 4: Nested Routes — Dashboard
**Qiyinlik:** ⭐⭐

Dashboard sahifasida 3 ta ichki sahifa yarating: Overview, Users, Settings.

```
/dashboard              → Overview (index)
/dashboard/users        → Foydalanuvchilar ro'yxati
/dashboard/settings     → Sozlamalar

Talablar:
✅ Sidebar bilan navigatsiya (NavLink)
✅ Aktiv sahifa ajratilib ko'rinsin
✅ Outlet orqali ichki kontent
```

---

### Vazifa 5: 404 Sahifa (Chiroyli Dizayn)
**Qiyinlik:** ⭐⭐

Professional 404 sahifa yarating:

```
Talablar:
✅ Katta "404" raqami (gradient rangli)
✅ "Sahifa topilmadi" xabari
✅ "← Orqaga" tugmasi (navigate(-1))
✅ "🏠 Bosh sahifa" havolasi
✅ Animatsiya (bounce yoki fade-in)
```

---

### Vazifa 6: Loading Spinner + Skeleton
**Qiyinlik:** ⭐⭐⭐

Ikki xil loading yarating va API dan ma'lumot olishda ko'rsating:

```
1. Spinner Loading — aylanuvchi doira
2. Skeleton Loading — shimmer effekt bilan karta

Talablar:
✅ `/products` — skeleton loading bilan
✅ `/products/:id` — spinner loading bilan
✅ Error holati ham bo'lsin
```

---

### Vazifa 7: Nested Routes — Blog Sayt
**Qiyinlik:** ⭐⭐⭐

Blog sayti yarating nested route'lar bilan:

```
/                      → Bosh sahifa
/blog                  → Blog postlar ro'yxati
/blog/:id              → Bitta post batafsil
/blog/:id/comments     → Post sharhlari
/about                 → Haqida sahifasi
*                      → 404

Talablar:
✅ MainLayout (Navbar + Outlet + Footer)
✅ BlogLayout (/blog ichida — sidebar + Outlet)
✅ Loading va Error holatlari
✅ API: https://dummyjson.com/posts
```

---

### Vazifa 8: useSearchParams bilan Filter/Pagination
**Qiyinlik:** ⭐⭐⭐

Mahsulotlarni filter va pagination bilan ko'rsating (URL da saqlansin).

```
/products                          → Barcha mahsulotlar (1-sahifa)
/products?page=2                   → 2-sahifa
/products?category=phones          → Faqat telefonlar
/products?page=1&category=laptops  → Laptoplar, 1-sahifa

Talablar:
✅ useSearchParams bilan URL dan o'qish/yozish
✅ Kategoriya tugmalari — bosganda URL yangilansin
✅ Pagination — sahifa raqamlari
✅ Sahifa yangilanganda ham filter saqlansin
```

---

### Vazifa 9: Multi-Layout Ilova
**Qiyinlik:** ⭐⭐⭐⭐

2 ta turli layout ishlatadigan ilova yarating:

```
PublicLayout (Navbar + Footer):
├── /           → Home
├── /about      → About
├── /contact    → Contact
└── /login      → Login

AdminLayout (Sidebar):
├── /admin              → Dashboard
├── /admin/products     → Mahsulotlar boshqaruvi
├── /admin/users        → Foydalanuvchilar
└── /admin/settings     → Sozlamalar

Talablar:
✅ 2 ta Layout — har biri o'z dizayni bilan
✅ Login → /admin ga yo'naltirsin (navigate)
✅ Admin sahifalarida sidebar NavLink
✅ 404 sahifa ikkala layout uchun
```

---

### Vazifa 10: To'liq E-commerce Sayt (Router + API)
**Qiyinlik:** ⭐⭐⭐⭐⭐

To'liq e-commerce sayti yarating barcha o'rganganlarimiz bilan:

```
Sahifalar:
├── /                          → Home (Hero + Featured Products)
├── /products                  → Barcha mahsulotlar (skeleton loading)
├── /products?category=phones  → Filtrlangan mahsulotlar
├── /products/:id              → Mahsulot batafsil (spinner loading)
├── /about                     → Haqida
├── /contact                   → Aloqa formasi
├── /login                     → Login sahifasi
├── /dashboard                 → Admin Dashboard
│   ├── /dashboard             → Statistika (index)
│   ├── /dashboard/products    → CRUD boshqaruvi
│   └── /dashboard/orders      → Buyurtmalar
└── *                          → 404 sahifa

Talablar:
✅ BrowserRouter + Routes + Route
✅ useParams — mahsulot detail
✅ useNavigate — login → dashboard
✅ useSearchParams — kategoriya filter
✅ Nested Routes — dashboard ichida
✅ 2 ta Layout (Public + Admin)
✅ NavLink — aktiv sahifa
✅ Loading (skeleton + spinner)
✅ Error holati
✅ 404 sahifa
✅ API: https://dummyjson.com
✅ Chiroyli, professional dizayn
```

```
src/
├── components/
│   ├── Navbar.jsx
│   ├── Footer.jsx
│   ├── Sidebar.jsx
│   ├── LoadingSpinner.jsx
│   └── SkeletonCard.jsx
├── layouts/
│   ├── PublicLayout.jsx    → Navbar + Outlet + Footer
│   └── AdminLayout.jsx     → Sidebar + Outlet
├── pages/
│   ├── Home.jsx
│   ├── Products.jsx
│   ├── ProductDetail.jsx
│   ├── About.jsx
│   ├── Contact.jsx
│   ├── Login.jsx
│   ├── NotFound.jsx
│   └── dashboard/
│       ├── DashHome.jsx
│       ├── DashProducts.jsx
│       └── DashOrders.jsx
├── App.jsx
└── main.jsx
```
