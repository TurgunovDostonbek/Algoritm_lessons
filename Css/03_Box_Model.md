# 03-Dars: Box Model (Quti Modeli)

## 📌 Box Model nima?

Har bir HTML element to'rtburchak quti sifatida ko'riladi.

```
┌─────────────────────────────┐
│         MARGIN              │  ← Tashqi bo'sh joy
│  ┌───────────────────────┐  │
│  │       BORDER          │  │  ← Chegara
│  │  ┌─────────────────┐  │  │
│  │  │    PADDING       │  │  │  ← Ichki bo'sh joy
│  │  │  ┌───────────┐  │  │  │
│  │  │  │  CONTENT  │  │  │  │  ← Mazmun
│  │  │  └───────────┘  │  │  │
│  │  └─────────────────┘  │  │
│  └───────────────────────┘  │
└─────────────────────────────┘
```

---

## 📌 Margin

```css
/* Margin — TASHQI bo'sh joy */
div {
  margin: 20px;              /* Barcha tomonlar */
  margin: 10px 20px;         /* Yuqori/Pastki | Chap/O'ng */
  margin: 10px 15px 20px;    /* Yuqori | Chap/O'ng | Pastki */
  margin: 10px 15px 20px 5px;/* Yuqori | O'ng | Pastki | Chap (saat strelkasi) */

  margin-top: 10px;
  margin-right: 15px;
  margin-bottom: 20px;
  margin-left: 5px;

  /* Markazga joylash */
  margin: 0 auto;  /* Yon tomonlar auto = tenglab markazga */

  /* Salbiy margin */
  margin-top: -20px;  /* Elementlar ustma-ust chiqadi */
}
```

---

## 📌 Margin Collapsing (Qo'shilishi)

```css
/* ⚠️ Vertikal marginlar qo'shilib ketadi! */
h1 { margin-bottom: 30px; }
p  { margin-top: 20px; }

/* Ular orasidagi bo'shliq = max(30, 20) = 30px (ikkalasi emas!) */

/* Qachon collapse bo'lmaydi: */
/* 1. Flexbox/Grid ichida */
/* 2. Floated elementlar */
/* 3. Absolute/Fixed positioned */
/* 4. Overflow: hidden/auto belgilansa */
```

---

## 📌 Padding

```css
/* Padding — ICHKI bo'sh joy */
div {
  padding: 20px;
  padding: 10px 20px;
  padding: 10px 20px 15px;
  padding: 10px 20px 15px 5px;

  padding-top: 10px;
  padding-right: 20px;
  padding-bottom: 15px;
  padding-left: 5px;

  /* Padding meros olmaydi, lekin background ni kengaytiradi */
}
```

---

## 📌 Border

```css
/* Border qisqartma */
div {
  border: kengligi uslubi rangi;
  border: 2px solid royalblue;   /* ← Mashhur */
  border: 1px dashed #ccc;
  border: 3px dotted red;
  border: 4px double navy;
  border: none;                   /* Yopish */
}

/* Alohida tomonlar */
div {
  border-top: 2px solid red;
  border-right: 1px dashed blue;
  border-bottom: 3px dotted green;
  border-left: none;
}

/* Border xossalari */
div {
  border-width: 2px;
  border-style: solid;       /* solid, dashed, dotted, double, none, hidden */
  border-color: royalblue;
  border-radius: 10px;       /* Burchaklar yumaloqlash */
  border-radius: 50%;        /* Doira */
  border-radius: 10px 20px 10px 20px;  /* TL TR BR BL */
}

/* Chiziq */
hr { border: none; border-top: 2px solid #eee; }
```

---

## 📌 box-sizing

```css
/* content-box (default) — width faqat content */
.content-box {
  box-sizing: content-box;
  width: 300px;
  padding: 20px;
  border: 2px solid;
  /* Asl kenglik: 300 + 40 (padding) + 4 (border) = 344px */
}

/* border-box (tavsiya!) — width = content + padding + border */
.border-box {
  box-sizing: border-box;
  width: 300px;
  padding: 20px;
  border: 2px solid;
  /* Asl kenglik: 300px (o'zgarmaydi!) */
}

/* Barcha elementlar uchun (tavsiya!) */
*, *::before, *::after {
  box-sizing: border-box;
}
```

---

## 📌 Shorthandlar (Qisqartmalar)

```css
/* Font shorthand */
.el {
  font-style: italic;
  font-weight: bold;
  font-size: 18px;
  line-height: 1.6;
  font-family: Arial, sans-serif;
  
  /* Qisqartma: style weight size/line-height family */
  font: italic bold 18px/1.6 Arial, sans-serif;
}

/* Background shorthand */
.el {
  background-color: #fff;
  background-image: url("rasm.jpg");
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
  
  /* Qisqartma */
  background: #fff url("rasm.jpg") no-repeat center/cover;
}

/* Border shorthand */
.el { border: 2px solid royalblue; }
.el { border-radius: 8px; }

/* Transition shorthand */
.el {
  transition-property: color, background;
  transition-duration: 0.3s;
  transition-timing-function: ease;
  transition-delay: 0s;
  
  /* Qisqartma */
  transition: color 0.3s ease, background 0.3s ease;
}
```

---

## 📌 Outline vs Border

```css
/* outline — border ga o'xshash, lekin joy EGALMAYDI */
input:focus { outline: 3px solid royalblue; }

/* border bilan farqi: */
/* border — joy egallaydi (box modelga ta'sir qiladi) */
/* outline — joy egollamaydi, box modelga ta'sir qilmaydi */
input { outline: none; }  /* Fokusdagi defaultni yopish */
```

---

## 🎯 10 ta Amaliy Vazifa — Karta Komponenti

```html
<!DOCTYPE html>
<html lang="uz">
<head><meta charset="UTF-8"><title>Box Model</title>
<link rel="stylesheet" href="box-model.css"></head>
<body>
  <div class="sahifa">

    <!-- Vazifa 1-3: Oddiy box model -->
    <div class="quti">Mazmun</div>

    <!-- Vazifa 4-7: To'liq karta -->
    <div class="karta">
      <div class="karta__rasm-wrapper">
        <img src="https://picsum.photos/400/250" alt="Rasm" class="karta__rasm">
        <span class="karta__yorliq">Yangi</span>
      </div>
      <div class="karta__tana">
        <h2 class="karta__sarlavha">Produkt nomi</h2>
        <p class="karta__tavsif">Bu mahsulotning qisqacha tavsifi...</p>
        <div class="karta__pastki">
          <span class="karta__narx">199,000 <small>so'm</small></span>
          <button class="btn btn--asosiy">Sotib olish</button>
        </div>
      </div>
    </div>

    <!-- Vazifa 8-10: Profil karta -->
    <div class="profil">
      <div class="profil__avatar"></div>
      <h3 class="profil__ism">Ali Valiev</h3>
      <p class="profil__mansab">Frontend Developer</p>
      <div class="profil__statistika">
        <div class="profil__stat"><strong>42</strong><span>Loyiha</span></div>
        <div class="profil__stat"><strong>128</strong><span>Kuzatuvchi</span></div>
        <div class="profil__stat"><strong>3.5K</strong><span>Yulduz</span></div>
      </div>
    </div>
  </div>
</body>
</html>
```

```css
/* box-model.css */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
body { font-family: "Segoe UI", sans-serif; background: #f0f2f5; }
.sahifa { max-width: 1200px; margin: 0 auto; padding: 40px 20px;
          display: flex; flex-wrap: wrap; gap: 24px; justify-content: center; }

/* Vazifa 1: content-box vs border-box */
.quti {
  box-sizing: border-box;   /* Tavsiya! */
  width: 300px;
  padding: 20px;
  margin: 0 auto;
  border: 3px solid royalblue;
  border-radius: 8px;
  text-align: center;
  background: white;
}

/* Vazifa 2: Karta border va border-radius */
.karta {
  width: 320px;
  background: white;
  border-radius: 16px;
  overflow: hidden;
  border: 1px solid rgba(0,0,0,0.08);
  box-shadow: 0 4px 24px rgba(0,0,0,0.08);
}

/* Vazifa 3: Rasm wrapper va yorliq */
.karta__rasm-wrapper { position: relative; }
.karta__rasm { width: 100%; height: 220px; object-fit: cover; display: block; }
.karta__yorliq {
  position: absolute; top: 12px; right: 12px;
  background: royalblue; color: white;
  padding: 4px 10px; border-radius: 20px; font-size: 12px;
}

/* Vazifa 4: Karta tana paddinglar */
.karta__tana { padding: 20px; }
.karta__sarlavha { font-size: 20px; margin-bottom: 8px; color: #1a1a1a; }
.karta__tavsif { color: #666; line-height: 1.6; margin-bottom: 20px; font-size: 14px; }

/* Vazifa 5: Pastki qism */
.karta__pastki { display: flex; align-items: center; justify-content: space-between; }
.karta__narx { font-size: 22px; font-weight: 700; color: #e63946; }
.karta__narx small { font-size: 13px; font-weight: 400; }

/* Vazifa 6: Tugma */
.btn { padding: 10px 20px; border: none; border-radius: 8px;
       cursor: pointer; font-size: 14px; font-weight: 600; }
.btn--asosiy { background: royalblue; color: white; }
.btn--asosiy:hover { background: #2c5282; }

/* Vazifa 7: Margin auto bilan markazlashtirish */
.quti { margin: 0 auto; display: block; }

/* Vazifa 8: Profil karta */
.profil {
  width: 280px; background: white; border-radius: 20px;
  padding: 32px 24px; text-align: center;
  box-shadow: 0 8px 32px rgba(0,0,0,0.1);
}

/* Vazifa 9: Avatar (border-radius: 50% = doira) */
.profil__avatar {
  width: 80px; height: 80px;
  border-radius: 50%;              /* Doira! */
  background: linear-gradient(135deg, royalblue, purple);
  margin: 0 auto 16px;
  border: 4px solid #e0e0ff;
}
.profil__ism { font-size: 20px; margin-bottom: 4px; }
.profil__mansab { color: #888; font-size: 13px; margin-bottom: 24px; }

/* Vazifa 10: Statistika + border-top separator */
.profil__statistika {
  display: flex; justify-content: space-around;
  border-top: 1px solid #f0f0f0; padding-top: 20px;
}
.profil__stat strong { display: block; font-size: 20px; color: royalblue; }
.profil__stat span { font-size: 12px; color: #999; }
```
