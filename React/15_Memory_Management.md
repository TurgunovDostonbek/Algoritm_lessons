# 15-Dars: Memory Management (localStorage, sessionStorage, Cookie)

## 📌 Web Storage nima?

Brauzerda ma'lumotlarni saqlash uchun 3 ta asosiy usul mavjud:

| Xususiyat | localStorage | sessionStorage | Cookie |
|-----------|-------------|----------------|--------|
| **Hajmi** | ~5-10 MB | ~5-10 MB | ~4 KB |
| **Muddati** | Doimiy (o'chirmaguningizcha) | Tab yopilganda o'chadi | Muddat belgilanadi |
| **Qayerda** | Faqat brauzerda | Faqat brauzerda | Brauzer + Server |
| **Avtomatik yuborilishi** | ❌ | ❌ | ✅ Har bir so'rovda |
| **Ishlatilishi** | Theme, til, savatcha | Forma vaqtinchalik data | Auth token, sessiya |

---

## 📌 localStorage — Doimiy Saqlash

Ma'lumot brauzer yopilsa ham saqlanadi. Faqat qo'lda o'chiriladi.

### Asosiy Metodlar:

```javascript
// 1. SAQLASH
localStorage.setItem('ism', 'Ali')
localStorage.setItem('yosh', '22')        // faqat string!

// 2. OLISH
const ism = localStorage.getItem('ism')    // "Ali"
const yosh = localStorage.getItem('yosh')  // "22" (string!)

// 3. O'CHIRISH (bitta)
localStorage.removeItem('ism')

// 4. HAMMASINI O'CHIRISH
localStorage.clear()

// 5. KALIT NOMI
localStorage.key(0)                        // birinchi kalit nomi

// 6. SONI
localStorage.length                        // nechta element bor
```

### Ob'ekt saqlash (JSON):

```javascript
// ⚠️ localStorage faqat STRING saqlaydi!

// ❌ NOTO'G'RI:
localStorage.setItem('user', { ism: 'Ali' })    // "[object Object]" bo'lib qoladi!

// ✅ TO'G'RI — JSON.stringify / JSON.parse:
const user = { ism: 'Ali', yosh: 22, rol: 'admin' }

// Saqlash — ob'ektni string ga aylantirish
localStorage.setItem('user', JSON.stringify(user))

// Olish — string ni ob'ektga aylantirish
const saqlanganUser = JSON.parse(localStorage.getItem('user'))
console.log(saqlanganUser.ism)  // "Ali"
```

### Massiv saqlash:

```javascript
const mahsulotlar = [
  { id: 1, nom: 'Telefon', narx: 500 },
  { id: 2, nom: 'Laptop', narx: 1200 },
]

// Saqlash
localStorage.setItem('savatcha', JSON.stringify(mahsulotlar))

// Olish
const savatcha = JSON.parse(localStorage.getItem('savatcha')) || []
console.log(savatcha)  // [{id:1, nom:"Telefon"...}, ...]
```

---

## 📌 localStorage — React da Ishlatish

### Oddiy misol — Theme saqlash:

```jsx
import { useState, useEffect } from 'react'

function App() {
  // localStorage dan boshlang'ich qiymat olish
  const [qorongʻu, setQorongʻu] = useState(() => {
    const saqlangan = localStorage.getItem('theme')
    return saqlangan === 'dark'
  })

  // Har safar o'zgarganda saqlash
  useEffect(() => {
    localStorage.setItem('theme', qorongʻu ? 'dark' : 'light')
  }, [qorongʻu])

  return (
    <div style={{
      minHeight: '100vh',
      background: qorongʻu ? '#1a1a2e' : '#f8f9fa',
      color: qorongʻu ? '#fff' : '#1a1a2e',
      padding: '40px',
      transition: 'all 0.3s',
    }}>
      <h1>Theme: {qorongʻu ? '🌙 Qorong\'u' : '☀️ Yorug\''}</h1>
      <button onClick={() => setQorongʻu(!qorongʻu)} style={{
        padding: '12px 24px', borderRadius: '10px', border: 'none',
        background: qorongʻu ? '#e94560' : 'royalblue', color: 'white',
        cursor: 'pointer', fontWeight: '700', fontSize: '16px',
      }}>
        {qorongʻu ? '☀️ Yorug\' rejim' : '🌙 Qorong\'u rejim'}
      </button>
    </div>
  )
}
```

### Custom Hook — useLocalStorage:

```jsx
// src/hooks/useLocalStorage.js
import { useState, useEffect } from 'react'

function useLocalStorage(kalit, boshlangich) {
  const [qiymat, setQiymat] = useState(() => {
    try {
      const saqlangan = localStorage.getItem(kalit)
      return saqlangan ? JSON.parse(saqlangan) : boshlangich
    } catch {
      return boshlangich
    }
  })

  useEffect(() => {
    localStorage.setItem(kalit, JSON.stringify(qiymat))
  }, [kalit, qiymat])

  return [qiymat, setQiymat]
}

export default useLocalStorage
```

```jsx
// Ishlatish — juda oson!
function App() {
  const [theme, setTheme] = useLocalStorage('theme', 'light')
  const [til, setTil] = useLocalStorage('til', 'uz')
  const [savatcha, setSavatcha] = useLocalStorage('cart', [])

  // Sahifa yangilansa ham ma'lumot saqlanadi!
}
```

---

## 📌 sessionStorage — Vaqtinchalik Saqlash

`localStorage` bilan bir xil metodlar, lekin **tab yopilganda ma'lumot o'chadi**.

```javascript
// Metodlar localStorage bilan bir xil:
sessionStorage.setItem('step', '3')
sessionStorage.getItem('step')        // "3"
sessionStorage.removeItem('step')
sessionStorage.clear()
```

### Qachon ishlatiladi?

| Holat | Misol |
|-------|-------|
| Ko'p qadamli forma | 1-qadam → 2-qadam → 3-qadam (tab yopilsa boshidan) |
| Vaqtinchalik filter | Mahsulot filtrini saqlab turish |
| Bir martalik xabar | "Xush kelibsiz!" faqat shu tab da |

### React da — Ko'p qadamli forma:

```jsx
function Step1({ onNext }) {
  const [ism, setIsm] = useState(() => sessionStorage.getItem('form_ism') || '')
  const [email, setEmail] = useState(() => sessionStorage.getItem('form_email') || '')

  function davomEt() {
    sessionStorage.setItem('form_ism', ism)
    sessionStorage.setItem('form_email', email)
    onNext()
  }

  return (
    <div>
      <h3>1-Qadam: Shaxsiy ma'lumotlar</h3>
      <input value={ism} onChange={e => setIsm(e.target.value)} placeholder="Ism" />
      <input value={email} onChange={e => setEmail(e.target.value)} placeholder="Email" />
      <button onClick={davomEt}>Keyingi →</button>
    </div>
  )
}

function Step3Tasdiqlash() {
  // Barcha qadamlar ma'lumotlarini olish
  const ism = sessionStorage.getItem('form_ism')
  const email = sessionStorage.getItem('form_email')
  const manzil = sessionStorage.getItem('form_manzil')

  function yuborish() {
    // API ga yuborish...
    sessionStorage.clear()  // Formani tozalash
    alert('Yuborildi!')
  }

  return (
    <div>
      <h3>3-Qadam: Tasdiqlash</h3>
      <p>Ism: {ism}</p>
      <p>Email: {email}</p>
      <p>Manzil: {manzil}</p>
      <button onClick={yuborish}>✅ Tasdiqlash</button>
    </div>
  )
}
```

---

## 📌 Cookie — Server bilan Ma'lumot Almashish

Cookie — brauzer va server o'rtasida ma'lumot almashish uchun. Har bir HTTP so'rovda avtomatik yuboriladi.

### JavaScript da Cookie:

```javascript
// YARATISH
document.cookie = "ism=Ali"
document.cookie = "til=uz"

// Muddatli cookie (7 kun)
const muddat = new Date()
muddat.setDate(muddat.getDate() + 7)
document.cookie = `token=abc123; expires=${muddat.toUTCString()}; path=/`

// Max-age bilan (soniyada)
document.cookie = "sessiya=xyz; max-age=3600; path=/"  // 1 soat

// O'QISH
console.log(document.cookie)
// "ism=Ali; til=uz; token=abc123"

// O'CHIRISH (muddatni o'tkazib yuborish)
document.cookie = "ism=; expires=Thu, 01 Jan 1970 00:00:00 UTC; path=/"
```

### Cookie yordamchi funksiyalar:

```javascript
// Cookie o'rnatish
function setCookie(nom, qiymat, kunlar = 7) {
  const muddat = new Date()
  muddat.setDate(muddat.getDate() + kunlar)
  document.cookie = `${nom}=${encodeURIComponent(qiymat)}; expires=${muddat.toUTCString()}; path=/`
}

// Cookie olish
function getCookie(nom) {
  const cookielar = document.cookie.split('; ')
  const topilgan = cookielar.find(c => c.startsWith(nom + '='))
  return topilgan ? decodeURIComponent(topilgan.split('=')[1]) : null
}

// Cookie o'chirish
function deleteCookie(nom) {
  document.cookie = `${nom}=; expires=Thu, 01 Jan 1970 00:00:00 UTC; path=/`
}

// Ishlatish:
setCookie('token', 'eyJhbGci...', 30)     // 30 kunlik
const token = getCookie('token')            // "eyJhbGci..."
deleteCookie('token')                       // o'chirish
```

### Cookie xususiyatlari:

| Xususiyat | Tavsif | Misol |
|-----------|--------|-------|
| `expires` | Tugash sanasi | `expires=Fri, 31 Dec 2025...` |
| `max-age` | Yashash muddati (soniya) | `max-age=86400` (1 kun) |
| `path` | Qaysi yo'lda amal qiladi | `path=/` (butun sayt) |
| `domain` | Qaysi domenda | `domain=.example.com` |
| `secure` | Faqat HTTPS | `secure` |
| `HttpOnly` | JS dan o'qib bo'lmaydi | Server tomondan |
| `SameSite` | CSRF himoyasi | `SameSite=Strict` |

---

## 📌 React da Auth bilan Ishlash

```jsx
// src/utils/auth.js
export function tokenSaqlash(token) {
  localStorage.setItem('auth_token', token)
}

export function tokenOlish() {
  return localStorage.getItem('auth_token')
}

export function tokenOchirish() {
  localStorage.removeItem('auth_token')
}

export function foydalanuvchiSaqlash(user) {
  localStorage.setItem('user', JSON.stringify(user))
}

export function foydalanuvchiOlish() {
  const data = localStorage.getItem('user')
  return data ? JSON.parse(data) : null
}
```

```jsx
// src/context/AuthContext.jsx
import { createContext, useState, useContext, useEffect } from 'react'
import { tokenSaqlash, tokenOlish, tokenOchirish, foydalanuvchiSaqlash, foydalanuvchiOlish } from '../utils/auth'

const AuthContext = createContext()

export function AuthProvider({ children }) {
  const [user, setUser] = useState(() => foydalanuvchiOlish())
  const [token, setToken] = useState(() => tokenOlish())

  const login = async (email, parol) => {
    const res = await fetch('https://dummyjson.com/auth/login', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ username: email, password: parol }),
    })
    if (!res.ok) throw new Error('Login xato!')
    const data = await res.json()

    setUser(data)
    setToken(data.accessToken)
    foydalanuvchiSaqlash(data)
    tokenSaqlash(data.accessToken)
  }

  const logout = () => {
    setUser(null)
    setToken(null)
    tokenOchirish()
    localStorage.removeItem('user')
  }

  return (
    <AuthContext.Provider value={{ user, token, login, logout, isLoggedIn: !!token }}>
      {children}
    </AuthContext.Provider>
  )
}

export const useAuth = () => useContext(AuthContext)
```

---

## 📌 Xulosa — Qachon Qaysi?

```
localStorage    → Doimiy saqlash (theme, til, savatcha)
sessionStorage  → Vaqtinchalik (forma, filter, bir martalik)
Cookie          → Server bilan (auth token, sessiya)
```

| Holat | Yechim |
|-------|--------|
| Theme (qorong'u/yorug') | `localStorage` |
| Til tanlash | `localStorage` |
| Savatcha | `localStorage` |
| Login token | `localStorage` yoki `Cookie` |
| Ko'p qadamli forma | `sessionStorage` |
| "Xush kelibsiz" xabar | `sessionStorage` |
| Auth sessiya (server) | `Cookie` (HttpOnly) |

---

## 🎯 10 ta Amaliy Vazifa

### Vazifa 1: Theme Saqlovchi
**⭐** — Qorong'u/Yorug' rejim. Sahifa yangilansa ham saqlansin (`localStorage`).

---

### Vazifa 2: Eslatma (Notes) Ilovasi
**⭐⭐** — Eslatmalar yozish, o'chirish. Barcha eslatmalar `localStorage` da saqlansin.

```jsx
// Talablar:
// ✅ Yangi eslatma qo'shish (input + button)
// ✅ Eslatmalar ro'yxati
// ✅ O'chirish tugmasi
// ✅ localStorage da saqlash
// ✅ Sahifa yangilansa ham saqlansin
```

---

### Vazifa 3: useLocalStorage Custom Hook
**⭐⭐** — Universal `useLocalStorage` hook yarating va 3 ta turli ma'lumot bilan sinang.

---

### Vazifa 4: Ko'p Qadamli Forma (sessionStorage)
**⭐⭐⭐** — 3 qadamli registratsiya formasi. Har qadam `sessionStorage` da saqlansin.

```
1-Qadam: Ism, Email
2-Qadam: Parol, Telefon
3-Qadam: Tasdiqlash + Yuborish
```

---

### Vazifa 5: Savatcha (localStorage)
**⭐⭐⭐** — Mahsulotlar + Savatcha. Sahifa yangilansa ham savatcha saqlansin.

---

### Vazifa 6: Cookie bilan Til Saqlash
**⭐⭐⭐** — Cookie yordamchi funksiyalar (set, get, delete). Til tanlaganda cookie da saqlansin.

---

### Vazifa 7: Auth — Login/SignUp
**⭐⭐⭐⭐** — Login va SignUp sahifalari. Token `localStorage` da saqlansin.

```
/login    → Email + Parol → token saqlash → /dashboard
/signup   → Ism + Email + Parol → /login ga yo'naltirish
/dashboard → Faqat login bo'lganlar uchun
Logout    → token o'chirish → /login ga
```

---

### Vazifa 8: localStorage + useContext
**⭐⭐⭐⭐** — AuthContext + CartContext + localStorage. Hammasi sahifa yangilansa saqlansin.

---

### Vazifa 9: "Yaqinda Ko'rilgan" Mahsulotlar
**⭐⭐⭐⭐** — Mahsulot detail sahifasini ochganda, `localStorage` da "yaqinda ko'rilganlar" ro'yxatiga qo'shing (max 5 ta).

---

### Vazifa 10: To'liq Auth + Cart + Theme Ilova
**⭐⭐⭐⭐⭐**

```
Sahifalar:
├── /              → Home
├── /products      → Mahsulotlar (API)
├── /products/:id  → Detail
├── /cart          → Savatcha (localStorage)
├── /login         → Login
├── /signup        → Ro'yxatdan o'tish
├── /profile       → Profil (himoyalangan)
└── *              → 404

Saqlash:
├── localStorage   → theme, savatcha, user, token
├── sessionStorage → forma qadamlari
└── Cookie         → til (7 kunlik)

Talablar:
✅ AuthContext — login/logout + localStorage
✅ CartContext — savatcha + localStorage
✅ ThemeContext — theme + localStorage
✅ React Router — useParams, useNavigate
✅ API: dummyjson.com/auth/login
✅ Himoyalangan route (login bo'lmasak → /login)
✅ Professional dizayn
```
