# 03-Dars: Components — Image, Icon, Style

## 📌 Komponentlarda Rasm Ishlatish

```jsx
// 1. Public papkasidan (URL ko'rinishida)
function App() {
  return <img src="/logo.svg" alt="Logo" />
}

// 2. src/assets dan import qilib
import reactLogo from './assets/react.svg'
import viteLogo from '/vite.svg'

function App() {
  return (
    <>
      <img src={viteLogo} alt="Vite logo" />
      <img src={reactLogo} alt="React logo" />
    </>
  )
}

// 3. Tashqi URL (Internet)
function App() {
  return (
    <img
      src="https://picsum.photos/400/300"
      alt="Random rasm"
      style={{ borderRadius: '12px' }}
    />
  )
}

// 4. Rasm komponenti yaratish
function Rasm({ src, alt, kenglik = 300, radius = 8 }) {
  return (
    <img
      src={src}
      alt={alt}
      width={kenglik}
      loading="lazy"
      style={{ borderRadius: `${radius}px`, maxWidth: '100%', display: 'block' }}
    />
  )
}

// Ishlatish:
<Rasm src="https://picsum.photos/400/300" alt="Tasvir" kenglik={400} radius={16} />
```

---

## 📌 Ikonlar — React Icons

```bash
# React Icons kutubxonasini o'rnatish
npm install react-icons
```

```jsx
// Ikonlarni import qilish
// Fi = Feather Icons
import { FiHome, FiUser, FiMail, FiGithub, FiStar } from 'react-icons/fi'
// Bi = Bootstrap Icons
import { BiCode, BiHeart, BiSearch } from 'react-icons/bi'
// Ai = Ant Design Icons
import { AiFillHtml5 } from 'react-icons/ai'
// Fa = Font Awesome
import { FaReact, FaJs, FaCss3Alt, FaHtml5 } from 'react-icons/fa'
// Si = Simple Icons
import { SiTailwindcss, SiTypescript } from 'react-icons/si'

function IkonlarDemo() {
  return (
    <div>
      {/* Oddiy ishlatish */}
      <FiHome />

      {/* O'lcham va rang */}
      <FiUser size={32} color="royalblue" />

      {/* CSS bilan */}
      <FiMail style={{ fontSize: '24px', color: '#e63946' }} />
      <FiMail className="my-icon" />

      {/* Inline */}
      <p>
        <FiGithub /> GitHub da kuzating
      </p>
    </div>
  )
}
```

---

## 📌 Komponentlarda Stil Berish

### 1. Inline Style
```jsx
// JSX da style — JavaScript ob'ekti!
function Karta() {
  return (
    <div style={{
      background: '#ffffff',        // camelCase!
      borderRadius: '16px',
      padding: '24px',
      boxShadow: '0 4px 24px rgba(0,0,0,0.08)'
    }}>
      <h2 style={{ color: '#1a1a2e', fontSize: '20px' }}>Sarlavha</h2>
    </div>
  )
}

// Dinamik stil
function Tugma({ turi = 'asosiy' }) {
  const stillar = {
    asosiy: { background: 'royalblue', color: 'white' },
    xavf:   { background: '#e63946', color: 'white' },
    oddiy:  { background: '#f3f4f6', color: '#1a1a2e' },
  }

  return (
    <button style={{
      ...stillar[turi],
      padding: '10px 20px', borderRadius: '8px',
      border: 'none', cursor: 'pointer', fontWeight: '600'
    }}>
      Tugma
    </button>
  )
}
```

### 2. CSS Module
```jsx
// Button.module.css
// .tugma { background: royalblue; color: white; padding: 10px 20px; }
// .tugma--katta { padding: 14px 28px; font-size: 18px; }

import styles from './Button.module.css'

function Tugma({ katta = false }) {
  return (
    <button className={`${styles.tugma} ${katta ? styles['tugma--katta'] : ''}`}>
      Bosing
    </button>
  )
}
```

### 3. Oddiy CSS fayl
```jsx
// Button.css
// .tugma { background: royalblue; color: white; }

import './Button.css'

function Tugma() {
  return <button className="tugma">Bosing</button>
}
```

---

## 🎯 10 ta Amaliy Vazifa — Componentalar bilan img, style, icon

```jsx
// npm install react-icons dan keyin:

// src/App.jsx
import KartaGrid from './components/KartaGrid'
import NavigatsiyaBari from './components/NavigatsiyaBari'
import TechStack from './components/TechStack'

function App() {
  return (
    <div style={{ minHeight: '100vh', background: '#f0f2f5', fontFamily: "'Segoe UI', sans-serif" }}>
      <NavigatsiyaBari />
      <div style={{ maxWidth: '1000px', margin: '0 auto', padding: '40px 20px' }}>
        <TechStack />
        <KartaGrid />
      </div>
    </div>
  )
}
export default App
```

```jsx
// src/components/NavigatsiyaBari.jsx — Vazifa 1-2 (Nav + Ikonlar)
import { FiHome, FiUser, FiBriefcase, FiMail, FiMenu } from 'react-icons/fi'
import { FaReact } from 'react-icons/fa'

function NavigatsiyaBari() {
  const havolalar = [
    { nom: 'Bosh', icon: <FiHome />, href: '#' },
    { nom: 'Haqimda', icon: <FiUser />, href: '#' },
    { nom: 'Loyihalar', icon: <FiBriefcase />, href: '#' },
    { nom: 'Aloqa', icon: <FiMail />, href: '#' },
  ]

  return (
    <nav style={{
      background: '#1a1a2e', padding: '0 40px',
      display: 'flex', alignItems: 'center', justifyContent: 'space-between',
      height: '64px', position: 'sticky', top: 0, zIndex: 100
    }}>
      {/* Vazifa 1: Logo — Icon + Matn */}
      <div style={{ display: 'flex', alignItems: 'center', gap: '10px', color: 'white', fontSize: '20px', fontWeight: '800' }}>
        <FaReact style={{ color: '#61dafb', fontSize: '28px' }} />
        MyPortfolio
      </div>

      {/* Vazifa 2: Nav havolalar — ikonlar bilan */}
      <ul style={{ list: 'none', display: 'flex', gap: '4px', margin: 0, padding: 0, listStyle: 'none' }}>
        {havolalar.map((havola) => (
          <li key={havola.nom}>
            <a href={havola.href} style={{
              color: 'rgba(255,255,255,0.7)', textDecoration: 'none',
              padding: '8px 14px', borderRadius: '8px',
              display: 'flex', alignItems: 'center', gap: '6px', fontSize: '14px',
              transition: 'all 0.2s'
            }}
            onMouseEnter={e => { e.target.style.background = 'rgba(255,255,255,0.1)'; e.target.style.color = 'white'; }}
            onMouseLeave={e => { e.target.style.background = 'none'; e.target.style.color = 'rgba(255,255,255,0.7)'; }}
            >
              {havola.icon} {havola.nom}
            </a>
          </li>
        ))}
      </ul>

      <FiMenu style={{ color: 'white', fontSize: '22px', cursor: 'pointer' }} />
    </nav>
  )
}
export default NavigatsiyaBari
```

```jsx
// src/components/TechStack.jsx — Vazifa 3-5 (Ikonlar + Style)
import { FaHtml5, FaCss3Alt, FaJs, FaReact, FaNodeJs, FaGitAlt } from 'react-icons/fa'
import { SiTypescript, SiTailwindcss, SiFigma } from 'react-icons/si'

const texnologiyalar = [
  { nom: 'HTML5', icon: FaHtml5, rang: '#e34c26' },
  { nom: 'CSS3', icon: FaCss3Alt, rang: '#264de4' },
  { nom: 'JavaScript', icon: FaJs, rang: '#f7df1e', matnRang: '#1a1a2e' },
  { nom: 'React', icon: FaReact, rang: '#61dafb', matnRang: '#1a1a2e' },
  { nom: 'TypeScript', icon: SiTypescript, rang: '#3178c6' },
  { nom: 'Tailwind', icon: SiTailwindcss, rang: '#06b6d4' },
  { nom: 'Node.js', icon: FaNodeJs, rang: '#339933' },
  { nom: 'Git', icon: FaGitAlt, rang: '#f14e32' },
  { nom: 'Figma', icon: SiFigma, rang: '#a259ff' },
]

function TechStack() {
  return (
    <section style={{ marginBottom: '40px' }}>
      <h2 style={{ fontSize: '22px', marginBottom: '4px' }}>🛠 Texnologiyalar</h2>
      <p style={{ color: '#888', fontSize: '14px', marginBottom: '20px' }}>Bilgan texnologiyalarim</p>

      {/* Vazifa 3: Icon + Matn grid */}
      <div style={{ display: 'grid', gridTemplateColumns: 'repeat(auto-fill, minmax(100px, 1fr))', gap: '12px' }}>
        {texnologiyalar.map((tech) => {
          const Icon = tech.icon
          return (
            <div key={tech.nom} style={{
              background: 'white', borderRadius: '14px', padding: '20px 12px',
              textAlign: 'center', boxShadow: '0 2px 12px rgba(0,0,0,0.06)',
              cursor: 'pointer', transition: 'transform 0.2s',
            }}
            onMouseEnter={e => e.currentTarget.style.transform = 'translateY(-4px)'}
            onMouseLeave={e => e.currentTarget.style.transform = 'translateY(0)'}
            >
              {/* Vazifa 4: Icon komponent dinamik rang bilan */}
              <Icon style={{ fontSize: '36px', color: tech.rang, display: 'block', margin: '0 auto 8px' }} />
              <span style={{ fontSize: '12px', fontWeight: '600', color: '#444' }}>{tech.nom}</span>
            </div>
          )
        })}
      </div>
    </section>
  )
}
export default TechStack
```

```jsx
// src/components/KartaGrid.jsx — Vazifa 6-10 (Image + Style)
import { FiGithub, FiExternalLink, FiStar, FiGitBranch } from 'react-icons/fi'

const loyihalar = [
  {
    id: 1,
    nom: 'Portfolio Sayt',
    tavsif: 'Shaxsiy portfolio — HTML, CSS, React bilan yaratilgan',
    rasm: 'https://picsum.photos/400/240?random=21',
    texnologiyalar: ['React', 'CSS', 'Vite'],
    yulduzlar: 24,
    forklar: 8,
    rang: '#4361ee',
  },
  {
    id: 2,
    nom: 'Todo App',
    tavsif: 'useState va localStorage bilan qurilgan vazifalar ilovasi',
    rasm: 'https://picsum.photos/400/240?random=22',
    texnologiyalar: ['React', 'Hooks'],
    yulduzlar: 15,
    forklar: 5,
    rang: '#10b981',
  },
  {
    id: 3,
    nom: 'E-commerce',
    tavsif: 'Mahsulotlar katalogi — API dan ma\'lumot olish',
    rasm: 'https://picsum.photos/400/240?random=23',
    texnologiyalar: ['React', 'Axios', 'CSS'],
    yulduzlar: 41,
    forklar: 12,
    rang: '#e63946',
  },
]

function LoyihaKarta({ loyiha }) {
  return (
    <article style={{
      background: 'white', borderRadius: '16px', overflow: 'hidden',
      boxShadow: '0 4px 20px rgba(0,0,0,0.08)', transition: 'transform 0.2s',
    }}
    onMouseEnter={e => e.currentTarget.style.transform = 'translateY(-4px)'}
    onMouseLeave={e => e.currentTarget.style.transform = 'translateY(0)'}
    >
      {/* Vazifa 6: Rasm komponenti */}
      <div style={{ position: 'relative' }}>
        <img
          src={loyiha.rasm}
          alt={`${loyiha.nom} loyihasining ekran ko'rinishi`}
          loading="lazy"
          style={{ width: '100%', height: '180px', objectFit: 'cover', display: 'block' }}
        />
        {/* Vazifa 7: Style — rangdor ustki qatim */}
        <div style={{
          position: 'absolute', top: '12px', right: '12px',
          background: loyiha.rang, color: 'white',
          padding: '4px 10px', borderRadius: '20px', fontSize: '12px', fontWeight: '700'
        }}>
          #{loyiha.id}
        </div>
      </div>

      <div style={{ padding: '20px' }}>
        <h3 style={{ fontSize: '17px', marginBottom: '6px' }}>{loyiha.nom}</h3>
        <p style={{ color: '#666', fontSize: '13px', marginBottom: '14px', lineHeight: 1.6 }}>
          {loyiha.tavsif}
        </p>

        {/* Vazifa 8: Texnologiya badge lar */}
        <div style={{ display: 'flex', gap: '6px', flexWrap: 'wrap', marginBottom: '16px' }}>
          {loyiha.texnologiyalar.map((tech) => (
            <span key={tech} style={{
              background: '#f0f4ff', color: 'royalblue',
              padding: '3px 10px', borderRadius: '20px', fontSize: '12px', fontWeight: '600'
            }}>
              {tech}
            </span>
          ))}
        </div>

        {/* Vazifa 9: Stats + Ikonlar */}
        <div style={{ display: 'flex', justifyContent: 'space-between', alignItems: 'center' }}>
          <div style={{ display: 'flex', gap: '14px', color: '#888', fontSize: '13px' }}>
            <span style={{ display: 'flex', alignItems: 'center', gap: '4px' }}>
              <FiStar /> {loyiha.yulduzlar}
            </span>
            <span style={{ display: 'flex', alignItems: 'center', gap: '4px' }}>
              <FiGitBranch /> {loyiha.forklar}
            </span>
          </div>

          {/* Vazifa 10: Havolalar — ikonlar bilan */}
          <div style={{ display: 'flex', gap: '8px' }}>
            <a href="https://github.com" target="_blank" rel="noopener noreferrer"
               style={{ width: '32px', height: '32px', background: '#1a1a2e', color: 'white', borderRadius: '8px', display: 'flex', alignItems: 'center', justifyContent: 'center' }}>
              <FiGithub size={15} />
            </a>
            <a href="#" style={{ width: '32px', height: '32px', background: 'royalblue', color: 'white', borderRadius: '8px', display: 'flex', alignItems: 'center', justifyContent: 'center' }}>
              <FiExternalLink size={15} />
            </a>
          </div>
        </div>
      </div>
    </article>
  )
}

function KartaGrid() {
  return (
    <section>
      <h2 style={{ fontSize: '22px', marginBottom: '4px' }}>💼 Loyihalar</h2>
      <p style={{ color: '#888', fontSize: '14px', marginBottom: '20px' }}>
        Jami {loyihalar.length} ta loyiha
      </p>
      <div style={{ display: 'grid', gridTemplateColumns: 'repeat(auto-fill, minmax(280px, 1fr))', gap: '20px' }}>
        {loyihalar.map((loyiha) => (
          <LoyihaKarta key={loyiha.id} loyiha={loyiha} />
        ))}
      </div>
    </section>
  )
}
export default KartaGrid
```
