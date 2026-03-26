# 14-Dars: Prop Drilling va useContext

## 📌 Props Eslatma

**Props** — parent dan child ga ma'lumot uzatish.

```jsx
// Parent
function App() {
  const [user, setUser] = useState({ ism: 'Ali', yosh: 22 })
  return <Profil user={user} />
}

// Child
function Profil({ user }) {
  return <h2>{user.ism} — {user.yosh} yosh</h2>
}
```

---

## 📌 Prop Drilling Muammosi

**Prop Drilling** — ma'lumotni bir necha daraja pastga uzatish. Har bir oraliq komponent foydalanmasa ham, propsni qabul qilib, pastga uzatishi kerak.

```jsx
// ❌ MUAMMO — 4 daraja prop uzatish
function App() {
  const [user, setUser] = useState({ ism: 'Ali', rol: 'admin' })

  return <Layout user={user} />            // 1-daraja
}

function Layout({ user }) {
  return <Sidebar user={user} />            // 2-daraja (ishlatmayapti!)
}

function Sidebar({ user }) {
  return <UserInfo user={user} />           // 3-daraja (ishlatmayapti!)
}

function UserInfo({ user }) {
  return <p>{user.ism} — {user.rol}</p>    // 4-daraja (faqat shu ishlatadi!)
}
```

### Muammo nimada?

```
App (user bor) ──props──→ Layout ──props──→ Sidebar ──props──→ UserInfo
                          ❌ kerak emas     ❌ kerak emas      ✅ kerak!
```

| Muammo | Tavsif |
|--------|--------|
| 🔗 Ko'p uzatish | Har bir daraja propsni qabul qilishi kerak |
| 🐛 Xato topish qiyin | Props zanjiri uzun bo'lsa debug qiyin |
| 🔄 O'zgartirish qiyin | Yangi prop qo'shsak, barcha darajalarni o'zgartirish kerak |
| 📖 O'qish qiyin | Kod murakkab bo'lib ketadi |

---

## 📌 useContext — Yechim!

**useContext** — ma'lumotni to'g'ridan-to'g'ri kerakli komponentga yetkazadi, oraliq komponentlarni chetlab o'tadi.

```
App (user bor) ──Context──→ UserInfo (to'g'ridan-to'g'ri oladi!)
                Layout va Sidebar bilmaydi ham!
```

---

## 📌 Context Yaratish — 3 Qadam

### 1-Qadam: Context yaratish (`createContext`)

```jsx
// src/context/UserContext.jsx
import { createContext } from 'react'

// Context yaratish
const UserContext = createContext()

export default UserContext
```

### 2-Qadam: Provider bilan o'rash

```jsx
// src/App.jsx
import { useState } from 'react'
import UserContext from './context/UserContext'

function App() {
  const [user, setUser] = useState({ ism: 'Ali', rol: 'admin' })

  return (
    // Provider — value orqali ma'lumot beradi
    <UserContext.Provider value={{ user, setUser }}>
      <Layout />       {/* ← endi props kerak emas! */}
    </UserContext.Provider>
  )
}
```

### 3-Qadam: useContext bilan olish

```jsx
// src/components/UserInfo.jsx
import { useContext } from 'react'
import UserContext from '../context/UserContext'

function UserInfo() {
  // To'g'ridan-to'g'ri olish — prop drilling yo'q!
  const { user } = useContext(UserContext)

  return <p>{user.ism} — {user.rol}</p>
}
```

### Oraliq komponentlar endi toza:

```jsx
// Layout va Sidebar endi props olmaydi!
function Layout() {
  return <Sidebar />     // ✅ Toza!
}

function Sidebar() {
  return <UserInfo />    // ✅ Toza!
}
```

---

## 📌 Amaliy Misol — Theme (Qorong'u/Yorug' rejim)

### Context:

```jsx
// src/context/ThemeContext.jsx
import { createContext, useState, useContext } from 'react'

const ThemeContext = createContext()

// Provider komponenti
export function ThemeProvider({ children }) {
  const [qorongʻu, setQorongʻu] = useState(false)

  const almashtir = () => setQorongʻu(prev => !prev)

  const theme = {
    qorongʻu,
    almashtir,
    ranglar: qorongʻu
      ? { bg: '#1a1a2e', text: '#fff', card: '#16213e', accent: '#e94560' }
      : { bg: '#f8f9fa', text: '#1a1a2e', card: '#fff', accent: 'royalblue' },
  }

  return (
    <ThemeContext.Provider value={theme}>
      {children}
    </ThemeContext.Provider>
  )
}

// Custom Hook — ishlatishni osonlashtiradi
export function useTheme() {
  const context = useContext(ThemeContext)
  if (!context) throw new Error('useTheme — ThemeProvider ichida ishlatilishi kerak!')
  return context
}
```

### Ishlatish:

```jsx
// src/main.jsx
import { ThemeProvider } from './context/ThemeContext'

ReactDOM.createRoot(document.getElementById('root')).render(
  <ThemeProvider>
    <App />
  </ThemeProvider>
)
```

```jsx
// src/components/Navbar.jsx
import { useTheme } from '../context/ThemeContext'

function Navbar() {
  const { qorongʻu, almashtir, ranglar } = useTheme()

  return (
    <nav style={{ background: ranglar.card, padding: '16px 32px', display: 'flex', justifyContent: 'space-between' }}>
      <h2 style={{ color: ranglar.accent }}>⚡ MySite</h2>
      <button onClick={almashtir} style={{
        background: ranglar.accent, color: '#fff', border: 'none',
        padding: '8px 20px', borderRadius: '8px', cursor: 'pointer',
      }}>
        {qorongʻu ? '☀️ Yorug'' : '🌙 Qorong'u'}
      </button>
    </nav>
  )
}
```

```jsx
// src/pages/Home.jsx
import { useTheme } from '../context/ThemeContext'

function Home() {
  const { ranglar } = useTheme()

  return (
    <div style={{ background: ranglar.bg, color: ranglar.text, minHeight: '80vh', padding: '40px' }}>
      <h1>Bosh Sahifa</h1>
      <p>Theme kontekstdan olinmoqda!</p>
    </div>
  )
}
```

---

## 📌 Amaliy Misol — Savatcha (Cart Context)

```jsx
// src/context/CartContext.jsx
import { createContext, useState, useContext } from 'react'

const CartContext = createContext()

export function CartProvider({ children }) {
  const [savatcha, setSavatcha] = useState([])

  const qosh = (mahsulot) => {
    setSavatcha(prev => {
      const bor = prev.find(s => s.id === mahsulot.id)
      if (bor) return prev.map(s => s.id === mahsulot.id ? { ...s, soni: s.soni + 1 } : s)
      return [...prev, { ...mahsulot, soni: 1 }]
    })
  }

  const ochir = (id) => setSavatcha(prev => prev.filter(s => s.id !== id))

  const tozala = () => setSavatcha([])

  const jami = savatcha.reduce((sum, s) => sum + s.price * s.soni, 0)
  const sonJami = savatcha.reduce((sum, s) => sum + s.soni, 0)

  return (
    <CartContext.Provider value={{ savatcha, qosh, ochir, tozala, jami, sonJami }}>
      {children}
    </CartContext.Provider>
  )
}

export function useCart() {
  return useContext(CartContext)
}
```

### Ishlatish:

```jsx
// src/main.jsx
import { CartProvider } from './context/CartContext'

ReactDOM.createRoot(document.getElementById('root')).render(
  <BrowserRouter>
    <CartProvider>
      <App />
    </CartProvider>
  </BrowserRouter>
)
```

```jsx
// Navbar da savatcha soni
import { useCart } from '../context/CartContext'

function Navbar() {
  const { sonJami } = useCart()
  return (
    <nav>
      <button>🛒 Savatcha ({sonJami})</button>
    </nav>
  )
}
```

```jsx
// Mahsulot kartasida — qo'shish
import { useCart } from '../context/CartContext'

function ProductCard({ mahsulot }) {
  const { qosh } = useCart()

  return (
    <div>
      <h3>{mahsulot.title}</h3>
      <p>${mahsulot.price}</p>
      <button onClick={() => qosh(mahsulot)}>🛒 Qo'shish</button>
    </div>
  )
}
```

```jsx
// Savatcha sahifasida — ro'yxat
import { useCart } from '../context/CartContext'

function CartPage() {
  const { savatcha, ochir, jami, tozala } = useCart()

  if (savatcha.length === 0) return <p>Savatcha bo'sh 🛒</p>

  return (
    <div>
      <h2>🛒 Savatcha</h2>
      {savatcha.map(item => (
        <div key={item.id} style={{ display: 'flex', justifyContent: 'space-between', padding: '12px', borderBottom: '1px solid #eee' }}>
          <span>{item.title} × {item.soni}</span>
          <span>${(item.price * item.soni).toFixed(2)}</span>
          <button onClick={() => ochir(item.id)}>🗑</button>
        </div>
      ))}
      <h3>Jami: ${jami.toFixed(2)}</h3>
      <button onClick={tozala}>Tozalash</button>
    </div>
  )
}
```

---

## 📌 Custom Hook Pattern (Eng Yaxshi Usul)

```jsx
// ✅ ENG YAXSHI PATTERN:
// 1. Context yarating
// 2. Provider komponenti yarating
// 3. Custom Hook yarating (useXxx)

// src/context/AuthContext.jsx
import { createContext, useState, useContext } from 'react'

const AuthContext = createContext()

export function AuthProvider({ children }) {
  const [user, setUser] = useState(null)

  const login = (email, parol) => {
    // ... API so'rovi
    setUser({ email, ism: 'Ali' })
  }

  const logout = () => setUser(null)

  return (
    <AuthContext.Provider value={{ user, login, logout, isLoggedIn: !!user }}>
      {children}
    </AuthContext.Provider>
  )
}

// Custom Hook
export function useAuth() {
  const context = useContext(AuthContext)
  if (!context) throw new Error('useAuth faqat AuthProvider ichida ishlaydi!')
  return context
}
```

```jsx
// Istalgan komponentda:
import { useAuth } from '../context/AuthContext'

function Header() {
  const { user, isLoggedIn, logout } = useAuth()

  return (
    <header>
      {isLoggedIn ? (
        <>
          <span>Salom, {user.ism}!</span>
          <button onClick={logout}>Chiqish</button>
        </>
      ) : (
        <Link to="/login">Kirish</Link>
      )}
    </header>
  )
}
```

---

## 📌 Ko'p Context — Birgalikda

```jsx
// src/main.jsx
ReactDOM.createRoot(document.getElementById('root')).render(
  <BrowserRouter>
    <ThemeProvider>
      <AuthProvider>
        <CartProvider>
          <App />
        </CartProvider>
      </AuthProvider>
    </ThemeProvider>
  </BrowserRouter>
)
```

---

## 📌 Props vs Context — Qachon Qaysi?

| Holat | Props ✅ | Context ✅ |
|-------|---------|-----------|
| 1-2 daraja pastga | ✅ | ❌ |
| 3+ daraja pastga | ❌ | ✅ |
| Global ma'lumot (theme, auth) | ❌ | ✅ |
| Komponent ichki ma'lumoti | ✅ | ❌ |
| Tez-tez o'zgaradigan data | ✅ | ⚠️ |
| Kichik ilova | ✅ | ❌ |
| Katta ilova | Aralash | ✅ |

---

## 🎯 10 ta Amaliy Vazifa

### Vazifa 1: Theme Switcher
**⭐** — Qorong'u/Yorug' rejim almashtirgich. ThemeContext yarating, Navbar va Home da ishlating.

---

### Vazifa 2: Til Almashtirish (i18n)
**⭐⭐** — O'zbek/Ingliz tili. LanguageContext yarating, barcha matnlarni tilga qarab o'zgartiring.

```jsx
const tarjimalar = {
  uz: { salom: 'Salom!', haqida: 'Biz haqimizda' },
  en: { salom: 'Hello!', haqida: 'About us' },
}
```

---

### Vazifa 3: Auth Context — Login/Logout
**⭐⭐** — AuthContext: login, logout, isLoggedIn. Login sahifasida kirish → Navbar da "Salom, Ali!" ko'rsatish.

---

### Vazifa 4: Savatcha (Cart) Context
**⭐⭐⭐** — CartContext: qo'shish, o'chirish, jami. Statik mahsulotlar ro'yxati + Savatcha sahifasi.

---

### Vazifa 5: Prop Drilling → useContext Refactor
**⭐⭐⭐** — Avval prop drilling bilan yozing (4 daraja), keyin useContext ga o'tkazing. Farqni ko'ring.

---

### Vazifa 6: useContext + React Router
**⭐⭐⭐** — AuthContext + useNavigate: Login → Dashboard, Logout → Home. Navbar user holatini ko'rsatsin.

---

### Vazifa 7: Multi-Context Ilova
**⭐⭐⭐** — ThemeContext + AuthContext birgalikda. Theme va Auth ikkalasi ham ishlashi kerak.

---

### Vazifa 8: E-commerce (Home, Product, Cart, Basket)
**⭐⭐⭐⭐** — useContext bilan to'liq e-commerce:

```
Sahifalar:
├── /              → Home (featured products)
├── /products      → Barcha mahsulotlar (API)
├── /products/:id  → Mahsulot detail
├── /cart          → Savatcha
└── /checkout      → Buyurtma berish

Context:
├── CartContext     → savatcha boshqaruvi
└── ThemeContext    → qorong'u/yorug' rejim
```

---

### Vazifa 9: Todo App + Context
**⭐⭐⭐⭐** — TodoContext: qo'shish, o'chirish, bajarildi, filter. Sahifalar: Active, Completed, All.

---

### Vazifa 10: To'liq E-commerce + Auth + Cart + Theme
**⭐⭐⭐⭐⭐**

```
Context'lar:
├── AuthContext   → login, logout, user
├── CartContext   → savatcha CRUD
└── ThemeContext  → qorong'u/yorug'

Sahifalar:
├── /                → Home
├── /products        → Mahsulotlar (API)
├── /products/:id    → Detail
├── /cart            → Savatcha (CartContext)
├── /login           → Login (AuthContext)
├── /profile         → Profil (faqat login bo'lsa)
└── *                → 404

Talablar:
✅ 3 ta Context birgalikda
✅ Custom Hooks (useAuth, useCart, useTheme)
✅ React Router (useParams, useNavigate)
✅ API: dummyjson.com
✅ Loading + Error
✅ Professional dizayn
```
