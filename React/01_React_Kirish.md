# 01-Dars: React ga Kirish

## 📌 React nima?

**React** — Facebook tomonidan yaratilgan, foydalanuvchi interfeyslari (UI) yaratish uchun ishlatiladigan JavaScript kutubxonasi.

```
React = UI Kutubxonasi (Library)
      ≠ Framework (Angular, Vue kabi to'liq framework emas)
```

**Nima uchun React?**
- ⚡ **Tezkor** — Virtual DOM tufayli faqat o'zgargan qism yangilanadi
- 🔧 **Komponentlar** — UI ni kichik, qayta ishlatiladigan bo'laklarga bo'lish
- 🌍 **Katta ekotizim** — npm da millionlab paketlar
- 💼 **Ish bozori** — O'zbekistonda eng ko'p ishlatiladigan frontend texnologiyasi

---

## 📌 React loyihasini yaratish (Vite bilan)

```bash
# Vite bilan yangi React loyiha yaratish
npm create vite@latest mening-loyiham -- --template react

# Papkaga kirish
cd mening-loyiham

# Paketlarni o'rnatish
npm install

# Serverni ishga tushirish
npm run dev
```

**Node.js va npm tekshirish:**
```bash
node --version    # v18+ bo'lishi kerak
npm --version     # v9+ bo'lishi kerak
```

---

## 📌 Vite loyiha tuzilmasi

```
mening-loyiham/
├── node_modules/          ← npm paketlari (git ga qo'shilmaydi)
├── public/
│   └── vite.svg           ← Statik fayllar
├── src/
│   ├── assets/            ← Rasmlar, shriftlar
│   │   └── react.svg
│   ├── App.css            ← App komponent uslublari
│   ├── App.jsx            ← Asosiy komponent ⭐
│   ├── index.css          ← Global uslublar
│   └── main.jsx           ← Kirish nuqtasi ⭐
├── .gitignore
├── index.html             ← Asosiy HTML fayl
├── package.json           ← Loyiha ma'lumotlari
├── package-lock.json
└── vite.config.js         ← Vite sozlamalari
```

---

## 📌 Asosiy Fayllar

### `index.html`
```html
<!DOCTYPE html>
<html lang="uz">
  <head>
    <meta charset="UTF-8" />
    <link rel="icon" type="image/svg+xml" href="/vite.svg" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Mening React Loyiham</title>
  </head>
  <body>
    <!-- React butun ilovasini shu div ichiga joylashtiradi -->
    <div id="root"></div>
    <script type="module" src="/src/main.jsx"></script>
  </body>
</html>
```

### `src/main.jsx` — Kirish nuqtasi
```jsx
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import './index.css'
import App from './App.jsx'

// HTML dagi #root div ni topib, React ilovasini unga ulash
createRoot(document.getElementById('root')).render(
  <StrictMode>
    <App />
  </StrictMode>,
)
```

### `src/App.jsx` — Asosiy komponent
```jsx
import './App.css'

function App() {
  return (
    <div className="App">
      <h1>Salom, React! 👋</h1>
      <p>Mening birinchi React ilovam</p>
    </div>
  )
}

export default App
```

---

## 📌 React npm Asosiy Buyruqlar

```bash
npm run dev        # Development server ishga tushirish (localhost:5173)
npm run build      # Production uchun build qilish (dist/ papkasi)
npm run preview    # Build ni preview qilish
npm install        # package.json dagi paketlarni o'rnatish
npm install axios  # Yangi paket o'rnatish
npm uninstall axio # Paket o'chirish
```

---

## 📌 React haqida Maqola o'qish

- 📖 [React rasmiy sayt](https://react.dev)
- 📖 [React o'zbek tilida](https://uz.react.dev) — React.dev ning o'zbek tarjimasi
- 📖 [Vite rasmiy sayt](https://vitejs.dev)

---

## 🎯 10 ta Amaliy Vazifa

### Vazifa 1: Yangi React loyiha yaratish
```bash
# Terminal da:
npm create vite@latest mening-portfolio -- --template react
cd mening-portfolio
npm install
npm run dev
```
*Localhost:5173 da ochilganini tekshiring*

---

### Vazifa 2-10: Birinchi React Ilovasi — Haqida Sahifasi

```jsx
// src/App.jsx — ni shu kabi o'zgartiring:
import './App.css'

function App() {
  return (
    <div style={{ minHeight: '100vh', background: 'linear-gradient(135deg, #1a1a2e, #16213e)', display: 'flex', alignItems: 'center', justifyContent: 'center' }}>
      <div style={{ textAlign: 'center', color: 'white', maxWidth: '600px', padding: '40px' }}>

        {/* Vazifa 2: Rasm qo'shish */}
        <div style={{ width: '120px', height: '120px', borderRadius: '50%', background: 'linear-gradient(135deg, royalblue, purple)', margin: '0 auto 24px', display: 'flex', alignItems: 'center', justifyContent: 'center', fontSize: '48px' }}>
          👤
        </div>

        {/* Vazifa 3: Sarlavha */}
        <h1 style={{ fontSize: '2.5rem', marginBottom: '8px' }}>Salom, Men Ali! 👋</h1>

        {/* Vazifa 4: Tavsif */}
        <p style={{ fontSize: '1.1rem', opacity: 0.8, marginBottom: '24px' }}>
          Frontend Developer | React & JavaScript
        </p>

        {/* Vazifa 5: Skills */}
        <div style={{ display: 'flex', gap: '10px', justifyContent: 'center', flexWrap: 'wrap', marginBottom: '32px' }}>
          {['HTML', 'CSS', 'JavaScript', 'React'].map((til) => (
            <span key={til} style={{ background: 'rgba(65,105,225,0.3)', border: '1px solid rgba(65,105,225,0.5)', padding: '6px 14px', borderRadius: '20px', fontSize: '14px' }}>
              {til}
            </span>
          ))}
        </div>

        {/* Vazifa 6: Tugmalar */}
        <div style={{ display: 'flex', gap: '12px', justifyContent: 'center', flexWrap: 'wrap', marginBottom: '40px' }}>
          <a href="https://github.com" target="_blank" rel="noopener noreferrer"
             style={{ background: '#333', color: 'white', padding: '12px 24px', borderRadius: '10px', textDecoration: 'none', fontWeight: '700' }}>
            🐙 GitHub
          </a>
          <a href="mailto:ali@mail.com"
             style={{ background: 'royalblue', color: 'white', padding: '12px 24px', borderRadius: '10px', textDecoration: 'none', fontWeight: '700' }}>
            📧 Email
          </a>
        </div>

        {/* Vazifa 7: Stats */}
        <div style={{ display: 'grid', gridTemplateColumns: 'repeat(3, 1fr)', gap: '16px', marginBottom: '32px' }}>
          {[
            { raqam: '15+', nom: 'Loyihalar' },
            { raqam: '2 yil', nom: 'Tajriba' },
            { raqam: '100%', nom: 'Mas\'uliyat' }
          ].map((stat) => (
            <div key={stat.nom} style={{ background: 'rgba(255,255,255,0.05)', padding: '20px', borderRadius: '12px' }}>
              <div style={{ fontSize: '28px', fontWeight: '800', color: 'royalblue' }}>{stat.raqam}</div>
              <div style={{ fontSize: '13px', opacity: 0.7, marginTop: '4px' }}>{stat.nom}</div>
            </div>
          ))}
        </div>

        {/* Vazifa 8: Loyihalar ro'yxati */}
        <h2 style={{ marginBottom: '16px', fontSize: '1.3rem' }}>💼 Oxirgi Loyihalar</h2>
        <div style={{ display: 'flex', flexDirection: 'column', gap: '10px', marginBottom: '32px' }}>
          {[
            { nom: 'Portfolio Sayt', texnologiya: 'React, CSS', yil: '2024' },
            { nom: 'Todo App', texnologiya: 'React, LocalStorage', yil: '2023' },
            { nom: 'Blog Sayt', texnologiya: 'HTML, CSS, JS', yil: '2023' },
          ].map((loyiha) => (
            <div key={loyiha.nom} style={{ background: 'rgba(255,255,255,0.05)', padding: '14px 18px', borderRadius: '10px', display: 'flex', justifyContent: 'space-between', alignItems: 'center' }}>
              <div style={{ textAlign: 'left' }}>
                <div style={{ fontWeight: '600', marginBottom: '2px' }}>{loyiha.nom}</div>
                <div style={{ fontSize: '12px', opacity: 0.6 }}>{loyiha.texnologiya}</div>
              </div>
              <span style={{ fontSize: '12px', opacity: 0.5 }}>{loyiha.yil}</span>
            </div>
          ))}
        </div>

        {/* Vazifa 9: Ilova nomi va versiya */}
        <p style={{ fontSize: '12px', opacity: 0.4 }}>
          React v18 bilan yaratilgan • 2024
        </p>

        {/* Vazifa 10: Pastki tugma */}
        <button
          onClick={() => alert('Salom React! 🎉')}
          style={{ marginTop: '16px', background: 'none', border: '1px solid rgba(255,255,255,0.2)', color: 'white', padding: '10px 20px', borderRadius: '8px', cursor: 'pointer', fontSize: '14px' }}
        >
          Meni bosing! 🚀
        </button>

      </div>
    </div>
  )
}

export default App
```
