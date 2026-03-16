# 13-Dars: Transform va Transition

## 📌 CSS Transform

**transform** — elementni o'zgartirish (siljitish, aylantirish, kattalashtirish).
Hujjat oqimiga ta'sir qilmaydi!

---

## 📌 translate — Siljitish

```css
.el {
  transform: translateX(100px);      /* O'ngga 100px */
  transform: translateX(-50px);      /* Chapga 50px */
  transform: translateY(50px);       /* Pastga 50px */
  transform: translate(100px, 50px); /* X va Y bir vaqtda */
  transform: translate(-50%, -50%);  /* O'zining yarimiga */
}

/* Markazlash uchun klassik usul */
.markaz {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
```

---

## 📌 rotate — Aylantirish

```css
.el {
  transform: rotate(45deg);     /* 45 darajaga aylantirish */
  transform: rotate(-30deg);    /* Teskari aylantirish */
  transform: rotate(0.5turn);   /* Yarim aylanish (180deg) */
  transform: rotateX(45deg);    /* X o'qi atrofida */
  transform: rotateY(45deg);    /* Y o'qi atrofida */
  transform: rotate3d(1,1,0, 45deg); /* 3D */
}
```

---

## 📌 scale — Kattalashtirish/Kichraytirish

```css
.el {
  transform: scale(2);       /* 2 marta kattalashtirish */
  transform: scale(0.5);     /* Yarmi qilish */
  transform: scaleX(1.5);    /* Faqat kenglik */
  transform: scaleY(0.8);    /* Faqat balandlik */
  transform: scale(1.2, 0.9); /* X, Y alohida */

  /* Hover da kattalashish */
}
.el:hover { transform: scale(1.05); }
```

---

## 📌 skew — Qiyshitish

```css
.el {
  transform: skewX(20deg);        /* Gorizontal qiyshitish */
  transform: skewY(10deg);        /* Vertikal qiyshitish */
  transform: skew(20deg, 10deg);  /* Ikkisi */
}
```

---

## 📌 Bir nechta Transform

```css
.el {
  /* Ketma-ket yozing (tartib muhim!) */
  transform: translate(100px, 0) rotate(45deg) scale(1.2);
  
  /* ⚠️ Har bir transform alohida yozmang! */
  /* transform: translateX(100px); ← Bu oldingisini o'chiradi */
  /* transform: rotate(45deg);     ← Faqat bu qoladi */
}
```

---

## 📌 transform-origin

```css
.el {
  transform-origin: center;    /* Default — elementning markazi */
  transform-origin: top left;  /* Yuqori chap burchak */
  transform-origin: 50% 50%;   /* Markazda */
  transform-origin: right bottom;
  transform-origin: 100% 100%;
  
  /* Misol: pastdan aylantirish */
  transform-origin: bottom center;
  transform: rotate(30deg);
}
```

---

## 📌 Transition

**transition** — CSS qiymatlarining o'zgarishini silliqlashtiradi.

```css
.el {
  /* Barcha xossalarga */
  transition: all 0.3s ease;
  
  /* Aniq xossa */
  transition: color 0.3s ease;
  transition: background-color 0.5s ease-in;
  transition: transform 0.4s cubic-bezier(0.34, 1.56, 0.64, 1);
  
  /* Bir nechta */
  transition: color 0.3s, background 0.3s, transform 0.4s;
}

/* Timing funksiyalar */
.el { transition: all 0.3s linear; }      /* Teng tezlikda */
.el { transition: all 0.3s ease; }        /* Sekin-tez-sekin (Default) */
.el { transition: all 0.3s ease-in; }     /* Sekin boshlanadi */
.el { transition: all 0.3s ease-out; }    /* Sekin tugaydi */
.el { transition: all 0.3s ease-in-out; } /* Ikkalasi ham */

/* cubic-bezier — maxsus */
.el { transition: all 0.4s cubic-bezier(0.68, -0.55, 0.265, 1.55); } /* Spring */

/* transition-delay */
.el { transition: all 0.3s ease 0.1s; } /* 0.1 soniya kechikish */
```

---

## 📌 Amaliy Pattern — Hover Card

```css
.karta {
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  transform: translateY(0);
}
.karta:hover {
  transform: translateY(-8px);
  box-shadow: 0 20px 40px rgba(0,0,0,0.15);
}

/* Tugma hover effekti */
.btn {
  background: royalblue;
  transition: background 0.2s, transform 0.2s;
}
.btn:hover {
  background: #2c5282;
  transform: scale(1.05);
}
.btn:active { transform: scale(0.97); }
```

---

## 🎯 10 ta Amaliy Vazifa

```html
<!DOCTYPE html>
<html lang="uz">
<head>
  <meta charset="UTF-8">
  <title>Transform va Transition</title>
  <link rel="stylesheet" href="transform.css">
</head>
<body>
<div class="sahifa">

  <!-- Vazifa 1: Hover kartalar (translate + scale) -->
  <section class="sektsiya">
    <h2>Hover Kartalar</h2>
    <div class="kartalar-grid">
      <div class="hover-karta">
        <div class="karta-icon">🚀</div>
        <h3>Tezkor</h3>
        <p>translateY + scale effekti</p>
      </div>
      <div class="hover-karta">
        <div class="karta-icon">🎨</div>
        <h3>Chiroyli</h3>
        <p>box-shadow transition</p>
      </div>
      <div class="hover-karta">
        <div class="karta-icon">⚡</div>
        <h3>Zamonaviy</h3>
        <p>cubic-bezier timing</p>
      </div>
    </div>
  </section>

  <!-- Vazifa 2: Rotate effektlari -->
  <section class="sektsiya rotate-sektsiya">
    <h2>Rotate Effektlar</h2>
    <div class="rotate-demo">
      <div class="rotate-el rotate-45">45°</div>
      <div class="rotate-el rotate-90">90°</div>
      <div class="rotate-el rotate-hover">Hover</div>
      <div class="rotate-el flip">Flip</div>
    </div>
  </section>

  <!-- Vazifa 3: Tugmalar kolleksiyasi -->
  <section class="sektsiya">
    <h2>Tugma Effektlar</h2>
    <div class="tugmalar">
      <button class="btn btn-slide">Slide</button>
      <button class="btn btn-scale">Scale</button>
      <button class="btn btn-shake">Shake ≡</button>
      <button class="btn btn-3d">3D Press</button>
      <button class="btn btn-glow">Glow</button>
    </div>
  </section>

  <!-- Vazifa 4: Avatar/profil hover -->
  <section class="sektsiya">
    <h2>Profil Kartalar</h2>
    <div class="profil-kartalar">
      <div class="profil-karta">
        <div class="profil-avatar">👨‍💻</div>
        <h3>Ali Valiev</h3>
        <p>Frontend Dev</p>
        <div class="profil-social">
          <a href="#">GH</a><a href="#">LI</a><a href="#">TW</a>
        </div>
      </div>
      <div class="profil-karta">
        <div class="profil-avatar">👩‍🎨</div>
        <h3>Malika Saidova</h3>
        <p>UI Designer</p>
        <div class="profil-social">
          <a href="#">GH</a><a href="#">LI</a><a href="#">TW</a>
        </div>
      </div>
    </div>
  </section>

  <!-- Vazifa 5: skew bilan dekorativ -->
  <section class="skew-sektsiya">
    <div class="skew-kontent">
      <h2>Qiyshiq sektsiya</h2>
      <p>skewY bilan yaratilgan</p>
    </div>
  </section>

</div>
</body>
</html>
```

```css
/* transform.css */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
body { font-family: "Segoe UI", sans-serif; background: #f0f2f5; color: #1a1a2e; }
.sahifa { max-width: 1100px; margin: 0 auto; padding: 40px 20px; }
.sektsiya { margin-bottom: 60px; }
h2 { font-size: 28px; margin-bottom: 28px; text-align: center; }

/* Vazifa 1: Hover kartalar */
.kartalar-grid { display: flex; gap: 24px; flex-wrap: wrap; justify-content: center; }
.hover-karta {
  width: 260px; background: white; padding: 36px 28px; border-radius: 20px;
  text-align: center; cursor: pointer;
  /* ← TRANSITION bu yerda bo'lishi kerak, :hover da emas */
  transition: transform 0.3s cubic-bezier(0.34, 1.56, 0.64, 1),
              box-shadow 0.3s ease;
  box-shadow: 0 4px 20px rgba(0,0,0,0.06);
}
.hover-karta:hover {
  transform: translateY(-12px) scale(1.02);
  box-shadow: 0 24px 48px rgba(0,0,0,0.12);
}
.karta-icon { font-size: 48px; margin-bottom: 16px; }
.hover-karta h3 { margin-bottom: 8px; }
.hover-karta p { color: #888; font-size: 14px; }

/* Vazifa 2: Rotate */
.rotate-sektsiya { background: #16213e; border-radius: 20px; padding: 40px; }
.rotate-sektsiya h2 { color: white; }
.rotate-demo { display: flex; gap: 24px; justify-content: center; flex-wrap: wrap; }
.rotate-el {
  width: 100px; height: 100px; background: royalblue; color: white;
  display: flex; align-items: center; justify-content: center;
  border-radius: 12px; font-weight: 700; cursor: pointer;
  transition: transform 0.4s ease;
}
.rotate-45  { transform: rotate(45deg); }
.rotate-90  { transform: rotate(90deg); }
.rotate-hover:hover { transform: rotate(360deg); }
.flip:hover { transform: rotateY(180deg); }

/* Vazifa 3: Tugmalar effektlari */
.tugmalar { display: flex; gap: 16px; flex-wrap: wrap; justify-content: center; padding: 20px; }
.btn {
  padding: 14px 28px; border: none; border-radius: 10px; font-size: 15px;
  font-weight: 600; cursor: pointer; background: royalblue; color: white;
  transition: all 0.3s ease; position: relative; overflow: hidden;
}
.btn-slide {
  background: #16213e;
  box-shadow: inset 0 0 0 0 royalblue;
  transition: box-shadow 0.3s ease, color 0.3s ease;
}
.btn-slide:hover {
  box-shadow: inset 200px 0 0 0 royalblue;
  color: white;
}
.btn-scale { background: #764ba2; }
.btn-scale:hover { transform: scale(1.1); }
.btn-scale:active { transform: scale(0.95); }
.btn-shake:hover { animation: silkish 0.4s ease; }
@keyframes silkish {
  0%,100% { transform: translateX(0); }
  25% { transform: translateX(-8px) rotate(-1deg); }
  75% { transform: translateX(8px) rotate(1deg); }
}
.btn-3d {
  background: #e63946;
  box-shadow: 0 6px 0 #a11d27;
  transition: transform 0.1s, box-shadow 0.1s;
}
.btn-3d:active { transform: translateY(4px); box-shadow: 0 2px 0 #a11d27; }
.btn-glow { background: #43e97b; color: #1a1a2e; }
.btn-glow:hover { box-shadow: 0 0 20px rgba(67,233,123,0.6), 0 0 40px rgba(67,233,123,0.3); transform: translateY(-2px); }

/* Vazifa 4: Profil kartalar */
.profil-kartalar { display: flex; gap: 24px; justify-content: center; flex-wrap: wrap; }
.profil-karta {
  width: 220px; background: white; padding: 32px 20px; border-radius: 20px;
  text-align: center; cursor: pointer;
  transition: transform 0.4s cubic-bezier(0.34, 1.56, 0.64, 1);
  box-shadow: 0 4px 20px rgba(0,0,0,0.08);
}
.profil-karta:hover { transform: translateY(-10px) rotate(-2deg); }
.profil-avatar { font-size: 56px; margin-bottom: 12px; }
.profil-karta h3 { font-size: 16px; margin-bottom: 4px; }
.profil-karta p { color: #888; font-size: 13px; margin-bottom: 16px; }
.profil-social { display: flex; gap: 8px; justify-content: center; }
.profil-social a {
  width: 34px; height: 34px; background: #f0f0f0; border-radius: 50%;
  display: flex; align-items: center; justify-content: center;
  font-size: 11px; font-weight: 700; color: #333; text-decoration: none;
  transition: transform 0.2s, background 0.2s;
}
.profil-social a:hover { transform: scale(1.2); background: royalblue; color: white; }

/* Vazifa 5: skewY sektsiya */
.skew-sektsiya {
  position: relative; margin: 40px 0;
  background: linear-gradient(135deg, royalblue, #764ba2);
  color: white; text-align: center; padding: 80px 40px;
  transform: skewY(-3deg); /* Qiyshiq sektsiya */
}
.skew-kontent { transform: skewY(3deg); } /* Matnni tik qilish */
.skew-sektsiya h2 { font-size: 36px; margin-bottom: 12px; }
```
