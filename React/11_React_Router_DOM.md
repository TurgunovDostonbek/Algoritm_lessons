# 11-Dars: React Router DOM

## 📌 React Router DOM nima?

**React Router DOM** — React ilovalarida sahifalar o'rtasida navigatsiya qilish uchun ishlatiladigan kutubxona. SPA (Single Page Application) da sahifa qayta yuklanmasdan URL o'zgaradi.

```bash
# O'rnatish:
npm install react-router-dom
```

---

## 📌 Asosiy Tushunchalar

| Tushuncha | Vazifasi |
|-----------|----------|
| `BrowserRouter` | Ilovani routing bilan o'rab oladi |
| `Routes` | Barcha route'larni guruhlaydi |
| `Route` | Bitta sahifa yo'nalishini belgilaydi |
| `Link` | Sahifalar o'rtasida havola (a tag o'rniga) |
| `NavLink` | Aktiv sahifani ko'rsatuvchi havola |
| `path` | URL manzili |
| `element` | Ko'rsatiladigan komponent |

---

## 📌 BrowserRouter — Asosiy O'rash

```jsx
// src/main.jsx
import { BrowserRouter } from 'react-router-dom'
import App from './App'

ReactDOM.createRoot(document.getElementById('root')).render(
  <BrowserRouter>
    <App />
  </BrowserRouter>
)
```

> ⚠️ **BrowserRouter** butun ilovani o'rab turishi kerak. Odatda `main.jsx` yoki `index.jsx` da yoziladi.

---

## 📌 Routes va Route — Sahifalarni Belgilash

```jsx
// src/App.jsx
import { Routes, Route } from 'react-router-dom'
import Home from './pages/Home'
import About from './pages/About'
import Contact from './pages/Contact'

function App() {
  return (
    <div>
      <h1>Mening Saytim</h1>

      <Routes>
        {/* path="/" — bosh sahifa */}
        <Route path="/" element={<Home />} />

        {/* path="/about" — haqida sahifasi */}
        <Route path="/about" element={<About />} />

        {/* path="/contact" — aloqa sahifasi */}
        <Route path="/contact" element={<Contact />} />
      </Routes>
    </div>
  )
}

export default App
```

### Route xususiyatlari:

| Xususiyat | Tavsif | Misol |
|-----------|--------|-------|
| `path` | URL manzili | `path="/about"` |
| `element` | Ko'rsatiladigan JSX/Komponent | `element={<About />}` |
| `index` | Bosh sahifa (path="/" bilan bir xil) | `index element={<Home />}` |

---

## 📌 Link — Sahifalar O'rtasida Navigatsiya

```jsx
import { Link } from 'react-router-dom'

function Navbar() {
  return (
    <nav>
      {/* ❌ NOTO'G'RI — sahifa qayta yuklanadi! */}
      <a href="/about">Haqida</a>

      {/* ✅ TO'G'RI — sahifa qayta yuklanmaydi! */}
      <Link to="/">Bosh sahifa</Link>
      <Link to="/about">Haqida</Link>
      <Link to="/contact">Aloqa</Link>
    </nav>
  )
}
```

### Link vs `<a>` tag farqi:

| Xususiyat | `<a href>` | `<Link to>` |
|-----------|-----------|-------------|
| Sahifa yuklash | ♻️ Qayta yuklanadi | ⚡ Yuklanmaydi |
| Tezlik | 🐌 Sekin | 🚀 Tez |
| SPA | ❌ Buzadi | ✅ Ishlaydi |
| State | ❌ Yo'qoladi | ✅ Saqlanadi |

---

## 📌 NavLink — Aktiv Sahifani Ko'rsatish

```jsx
import { NavLink } from 'react-router-dom'

function Navbar() {
  return (
    <nav style={{ display: 'flex', gap: '16px' }}>
      <NavLink
        to="/"
        style={({ isActive }) => ({
          color: isActive ? 'royalblue' : '#555',
          fontWeight: isActive ? '800' : '400',
          textDecoration: 'none',
          borderBottom: isActive ? '2px solid royalblue' : 'none',
          paddingBottom: '4px',
        })}
      >
        Bosh sahifa
      </NavLink>

      <NavLink
        to="/about"
        style={({ isActive }) => ({
          color: isActive ? 'royalblue' : '#555',
          fontWeight: isActive ? '800' : '400',
          textDecoration: 'none',
          borderBottom: isActive ? '2px solid royalblue' : 'none',
          paddingBottom: '4px',
        })}
      >
        Haqida
      </NavLink>
    </nav>
  )
}
```

### NavLink — className bilan:

```jsx
<NavLink
  to="/about"
  className={({ isActive }) => isActive ? 'nav-active' : 'nav-link'}
>
  Haqida
</NavLink>
```

```css
/* CSS */
.nav-link {
  color: #555;
  text-decoration: none;
}
.nav-active {
  color: royalblue;
  font-weight: 800;
  border-bottom: 2px solid royalblue;
}
```

---

## 📌 Sahifalar (Pages) Yaratish

```
src/
├── pages/
│   ├── Home.jsx
│   ├── About.jsx
│   └── Contact.jsx
├── components/
│   └── Navbar.jsx
├── App.jsx
└── main.jsx
```

```jsx
// src/pages/Home.jsx
function Home() {
  return (
    <div>
      <h2>🏠 Bosh Sahifa</h2>
      <p>Saytimizga xush kelibsiz!</p>
    </div>
  )
}
export default Home

// src/pages/About.jsx
function About() {
  return (
    <div>
      <h2>ℹ️ Biz Haqimizda</h2>
      <p>Biz React o'rganuvchi jamoamiz.</p>
    </div>
  )
}
export default About

// src/pages/Contact.jsx
function Contact() {
  return (
    <div>
      <h2>📞 Aloqa</h2>
      <p>Email: info@example.com</p>
      <p>Tel: +998 90 123 45 67</p>
    </div>
  )
}
export default Contact
```

---

## 📌 To'liq Asosiy Misol

```jsx
// src/main.jsx
import ReactDOM from 'react-dom/client'
import { BrowserRouter } from 'react-router-dom'
import App from './App'

ReactDOM.createRoot(document.getElementById('root')).render(
  <BrowserRouter>
    <App />
  </BrowserRouter>
)
```

```jsx
// src/components/Navbar.jsx
import { NavLink } from 'react-router-dom'

const havolalar = [
  { nom: '🏠 Bosh sahifa', yo'l: '/' },
  { nom: 'ℹ️ Haqida', yo'l: '/about' },
  { nom: '📞 Aloqa', yo'l: '/contact' },
]

function Navbar() {
  return (
    <nav style={{
      background: '#1a1a2e',
      padding: '0 40px',
      display: 'flex',
      alignItems: 'center',
      height: '60px',
      gap: '8px',
    }}>
      {havolalar.map((h) => (
        <NavLink
          key={h.yo'l}
          to={h.yo'l}
          style={({ isActive }) => ({
            color: isActive ? '#fff' : 'rgba(255,255,255,0.6)',
            textDecoration: 'none',
            padding: '8px 16px',
            borderRadius: '8px',
            background: isActive ? 'royalblue' : 'transparent',
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

```jsx
// src/App.jsx
import { Routes, Route } from 'react-router-dom'
import Navbar from './components/Navbar'
import Home from './pages/Home'
import About from './pages/About'
import Contact from './pages/Contact'

function App() {
  return (
    <div style={{ minHeight: '100vh', background: '#f0f2f5', fontFamily: "'Segoe UI', sans-serif" }}>
      <Navbar />

      <div style={{ maxWidth: '900px', margin: '0 auto', padding: '32px 20px' }}>
        <Routes>
          <Route path="/" element={<Home />} />
          <Route path="/about" element={<About />} />
          <Route path="/contact" element={<Contact />} />
        </Routes>
      </div>
    </div>
  )
}

export default App
```

---

## 📌 Route Tartibini Tushunish

```jsx
<Routes>
  {/* React Router eng mos yo'lni topadi */}

  {/* Aniq (exact) yo'llar */}
  <Route path="/" element={<Home />} />
  <Route path="/about" element={<About />} />
  <Route path="/products" element={<Products />} />

  {/* Dinamik yo'l (keyingi darsda batafsil) */}
  <Route path="/products/:id" element={<ProductDetail />} />

  {/* Wildcard — barcha noma'lum yo'llar */}
  <Route path="*" element={<NotFound />} />
</Routes>
```

### Qoidalar:

1. **`path="/"`** — faqat bosh sahifa uchun
2. **`path="/about"`** — aniq URL uchun
3. **`path="/products/:id"`** — dinamik URL (id o'zgaradi)
4. **`path="*"`** — hech qaysi route mos kelmasa (404 sahifa)

---

## 📌 Route'larni Massivdan Generatsiya Qilish

```jsx
const sahifalar = [
  { yo'l: '/', nom: 'Bosh sahifa', komponent: <Home /> },
  { yo'l: '/about', nom: 'Haqida', komponent: <About /> },
  { yo'l: '/contact', nom: 'Aloqa', komponent: <Contact /> },
  { yo'l: '/services', nom: 'Xizmatlar', komponent: <Services /> },
]

function App() {
  return (
    <Routes>
      {sahifalar.map((sahifa) => (
        <Route
          key={sahifa.yo'l}
          path={sahifa.yo'l}
          element={sahifa.komponent}
        />
      ))}
      <Route path="*" element={<NotFound />} />
    </Routes>
  )
}
```

---

## 📌 Layout bilan Ishlash

```jsx
// src/layouts/MainLayout.jsx
import { Outlet } from 'react-router-dom'
import Navbar from '../components/Navbar'

function MainLayout() {
  return (
    <div>
      {/* Navbar har doim ko'rinadi */}
      <Navbar />

      {/* Outlet — ichki route'lar shu yerda ko'rsatiladi */}
      <main style={{ maxWidth: '900px', margin: '0 auto', padding: '32px 20px' }}>
        <Outlet />
      </main>

      {/* Footer har doim ko'rinadi */}
      <footer style={{ textAlign: 'center', padding: '20px', color: '#888' }}>
        © 2025 Mening Saytim
      </footer>
    </div>
  )
}

export default MainLayout
```

```jsx
// src/App.jsx — Layout bilan
import { Routes, Route } from 'react-router-dom'
import MainLayout from './layouts/MainLayout'
import Home from './pages/Home'
import About from './pages/About'
import Contact from './pages/Contact'

function App() {
  return (
    <Routes>
      {/* MainLayout ichidagi barcha sahifalar Navbar va Footer ko'rsatadi */}
      <Route element={<MainLayout />}>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="/contact" element={<Contact />} />
      </Route>
    </Routes>
  )
}
```

> **`<Outlet />`** — bu joy ichki (child) route komponentini ko'rsatish uchun ishlatiladi.

---

## 📌 Xulosa — Asosiy Import'lar

```jsx
import {
  BrowserRouter,   // main.jsx da — butun ilovani o'raydi
  Routes,          // App.jsx da — route'larni guruhlaydi
  Route,           // Har bir sahifa uchun yo'l
  Link,            // Oddiy havola (a tag o'rniga)
  NavLink,         // Aktiv sahifani ko'rsatadigan havola
  Outlet,          // Layout ichidagi child route uchun joy
} from 'react-router-dom'
```

| Komponent | Qayerda | Nima qiladi |
|-----------|---------|-------------|
| `BrowserRouter` | `main.jsx` | Routing ni yoqadi |
| `Routes` | `App.jsx` | Route'larni saralaydi |
| `Route` | `App.jsx` | path + element juftligi |
| `Link` | Navbar, Button | Sahifaga o'tadi (reload yo'q) |
| `NavLink` | Navbar | Aktiv sahifani belgilaydi |
| `Outlet` | Layout | Child route'ni ko'rsatadi |

---

## 🎯 10 ta Amaliy Vazifa

### Vazifa 1: Oddiy 3 Sahifali Sayt
**Qiyinlik:** ⭐

3 ta sahifa yarating: Home, About, Contact. Navbar orqali ular o'rtasida harakatlanish imkoni bo'lsin.

```
src/
├── pages/
│   ├── Home.jsx       → "Bosh sahifa" matni
│   ├── About.jsx      → "Biz haqimizda" matni
│   └── Contact.jsx    → "Bog'lanish" matni
├── components/
│   └── Navbar.jsx     → 3 ta Link
├── App.jsx            → Routes
└── main.jsx           → BrowserRouter
```

---

### Vazifa 2: NavLink bilan Aktiv Sahifa
**Qiyinlik:** ⭐

Navbar dagi havolalar aktiv bo'lganda rangini o'zgartirsin (masalan, ko'k rang va qalin shrift).

```jsx
// Kutilgan natija:
// Bosh sahifada bo'lsak → "Bosh sahifa" ko'k va qalin
// About da bo'lsak → "Haqida" ko'k va qalin
```

---

### Vazifa 3: 404 Not Found Sahifa
**Qiyinlik:** ⭐⭐

Noma'lum URL kiritilsa, "Sahifa topilmadi" degan sahifa ko'rinsin.

```jsx
// path="*" — wildcard route
// Misol: /asdfgh → "404 — Sahifa topilmadi!"

function NotFound() {
  return (
    <div style={{ textAlign: 'center', padding: '80px 20px' }}>
      <h1 style={{ fontSize: '72px', color: '#e63946' }}>404</h1>
      <p>Sahifa topilmadi!</p>
      <Link to="/">Bosh sahifaga qaytish</Link>
    </div>
  )
}
```

---

### Vazifa 4: Layout + Outlet
**Qiyinlik:** ⭐⭐

`MainLayout` yarating — Navbar yuqorida, Footer pastda, o'rtada `<Outlet />` orqali sahifalar ko'rinsin.

```
┌──────────────────────────────┐
│         NAVBAR               │  ← Har doim ko'rinadi
├──────────────────────────────┤
│                              │
│       <Outlet />             │  ← Sahifa kontenti
│       (Home / About / ...)   │
│                              │
├──────────────────────────────┤
│         FOOTER               │  ← Har doim ko'rinadi
└──────────────────────────────┘
```

---

### Vazifa 5: Ko'p Sahifali Portfolio Sayt
**Qiyinlik:** ⭐⭐

5 ta sahifali portfolio sayt yarating:
- **Home** — salom xabar
- **About** — o'zingiz haqida
- **Projects** — loyihalar ro'yxati
- **Skills** — texnologiyalar ro'yxati
- **Contact** — aloqa ma'lumotlari

---

### Vazifa 6: Sahifalarni Massivdan Generatsiya
**Qiyinlik:** ⭐⭐

Route va NavLink'larni massivdan `.map()` yordamida yarating.

```jsx
const sahifalar = [
  { path: '/', label: '🏠 Home', element: <Home /> },
  { path: '/about', label: 'ℹ️ About', element: <About /> },
  { path: '/services', label: '🛠 Services', element: <Services /> },
  { path: '/contact', label: '📞 Contact', element: <Contact /> },
]

// Navbar da:
sahifalar.map(s => <NavLink to={s.path}>{s.label}</NavLink>)

// Routes da:
sahifalar.map(s => <Route path={s.path} element={s.element} />)
```

---

### Vazifa 7: Responsive Navbar (Mobil Menu)
**Qiyinlik:** ⭐⭐⭐

Mobil ekranda hamburger menu (☰) ko'rsatadigan Navbar yarating. Tugma bosilganda menyu ochilsin/yopilsin.

```jsx
// Talablar:
// 1. Katta ekranda — oddiy gorizontal navbar
// 2. Kichik ekranda — ☰ tugma
// 3. ☰ bosilsa — menyu vertikal ochiladi
// 4. Havola bosilsa — menyu yopiladi
```

---

### Vazifa 8: Footer bilan Multi-Section Sayt
**Qiyinlik:** ⭐⭐⭐

Kompaniya sayti yarating:
- **Navbar** — logo + havolalar
- **Home** — hero section bilan
- **Services** — 4 ta xizmat kartasi
- **Team** — 3 ta jamoa a'zosi
- **Contact** — forma (faqat UI)
- **Footer** — ijtimoiy tarmoqlar + copyright

---

### Vazifa 9: Sidebar Navigation
**Qiyinlik:** ⭐⭐⭐

Chap tomonda sidebar, o'ng tomonda kontent ko'rinadigan admin panel layout yarating.

```
┌─────────┬───────────────────────────┐
│         │                           │
│ SIDEBAR │      <Outlet />           │
│         │      (Dashboard/Users/    │
│ 📊 Dash │       Settings/...)       │
│ 👥 Users│                           │
│ ⚙ Sett. │                           │
│         │                           │
└─────────┴───────────────────────────┘
```

```jsx
// Talablar:
// 1. Sidebar NavLink'lar bilan (aktiv sahifa ajratilib ko'rinsin)
// 2. Dashboard, Users, Settings sahifalari
// 3. Outlet orqali kontent ko'rsatilsin
```

---

### Vazifa 10: To'liq Landing Page
**Qiyinlik:** ⭐⭐⭐⭐

5 sahifali professional landing page yarating:

```
Sahifalar:
├── Home        → Hero banner, xususiyatlar, statistika
├── About       → Kompaniya haqida, tarix
├── Products    → Mahsulotlar grid (statik data)
├── Blog        → Blog postlar ro'yxati (statik)
└── Contact     → Aloqa formasi (faqat UI)

Talablar:
✅ BrowserRouter + Routes + Route
✅ NavLink bilan aktiv sahifa
✅ MainLayout + Outlet
✅ 404 Not Found sahifa
✅ Footer barcha sahifalarda
✅ Chiroyli dizayn (gradient, shadow, hover)
```

```jsx
// Fayl strukturasi:
src/
├── components/
│   ├── Navbar.jsx
│   └── Footer.jsx
├── layouts/
│   └── MainLayout.jsx      // Navbar + Outlet + Footer
├── pages/
│   ├── Home.jsx
│   ├── About.jsx
│   ├── Products.jsx
│   ├── Blog.jsx
│   ├── Contact.jsx
│   └── NotFound.jsx
├── App.jsx
└── main.jsx
```
