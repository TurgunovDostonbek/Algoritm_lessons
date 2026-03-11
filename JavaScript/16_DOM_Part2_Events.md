# 16-Dars: DOM — 2-qism (Events va Event Listeners)

## 📌 Event nima?

**Event (hodisa)** — brauzerda sodir bo'ladigan narsa: tugma bosilishi, sichqoncha harakatlanishi, sahifa yuklanishi va h.k.

```
Event turlari:
├── Mouse: click, dblclick, mouseenter, mouseleave, mousemove
├── Keyboard: keydown, keyup, keypress
├── Form: submit, change, input, focus, blur, reset
├── Window: load, DOMContentLoaded, resize, scroll
└── Touch: touchstart, touchend, touchmove
```

---

## 📌 `addEventListener()` — Event Qo'shish

```javascript
let tugma = document.getElementById("btn");

// Sintaksis: element.addEventListener(hodisa, handler, options)
tugma.addEventListener("click", function(event) {
  console.log("Tugma bosildi!");
  console.log(event);        // Event ob'ekti
  console.log(event.type);   // "click"
  console.log(event.target); // Bosishlagan element
});

// Arrow function bilan
tugma.addEventListener("click", (e) => {
  console.log("Arrow function:", e.target.id);
});

// Alohida funksiya bilan (tavsiya etiladi)
function tugmaBosildi(e) {
  console.log("Funksiya:", e.target.textContent);
}
tugma.addEventListener("click", tugmaBosildi);
```

---

## 📌 `removeEventListener()` — Event O'chirish

```javascript
function handler() {
  console.log("Bir marta!");
}

document.getElementById("btn").addEventListener("click", handler);

// O'chirish — bir xil funksiya reference kerak!
document.getElementById("btn").removeEventListener("click", handler);

// ⚠️ Anonymous funksiya o'chirib bo'lmaydi!
btn.addEventListener("click", () => console.log("Bu o'chirilmaydi!"));
// btn.removeEventListener("click", ???); // Imkonsiz!
```

---

## 📌 Event Ob'ekti

```javascript
document.addEventListener("click", function(event) {
  // Asosiy xususiyatlar
  console.log(event.type);          // "click"
  console.log(event.target);        // Bosishlagan element
  console.log(event.currentTarget); // Listener qo'shilgan element
  console.log(event.timeStamp);     // Vaqt (ms)

  // Mouse xususiyatlari
  console.log(event.clientX, event.clientY); // Viewport koordinatasi
  console.log(event.pageX, event.pageY);     // Sahifa koordinatasi
  console.log(event.button);        // 0=chap, 1=o'rta, 2=o'ng

  // Klaviatura xususiyatlari
  // event.key, event.code, event.ctrlKey, event.shiftKey
});
```

---

## 📌 Event Bubbling (Ko'pchish)

Event ichki elementdan tashqi elementga "ko'tariladi".

```html
<div id="tashqi">
  <div id="ichki">
    <button id="tugma">Bosing</button>
  </div>
</div>
```

```javascript
document.getElementById("tashqi").addEventListener("click", () => {
  console.log("Tashqi div");  // 3-chi chiqadi
});

document.getElementById("ichki").addEventListener("click", () => {
  console.log("Ichki div");   // 2-chi chiqadi
});

document.getElementById("tugma").addEventListener("click", () => {
  console.log("Tugma");        // 1-chi chiqadi
});

// Tugma bosilsa: Tugma → Ichki div → Tashqi div
```

### `event.stopPropagation()` — Ko'pchishni to'xtatish

```javascript
document.getElementById("tugma").addEventListener("click", (e) => {
  console.log("Faqat tugma!");
  e.stopPropagation(); // Tashqiga ko'tarilmaydi
});
```

---

## 📌 Event Capturing (Tutish)

Tashqi elementdan ichkiga qarab ishlaydi.

```javascript
// 3-parameter true = capturing phase
document.getElementById("tashqi").addEventListener("click", () => {
  console.log("Tashqi — capturing"); // Birinchi chiqadi
}, true);

document.getElementById("tugma").addEventListener("click", () => {
  console.log("Tugma — bubbling"); // Ikkinchi
});

// Tartib: Capturing (tashqidan) → Bubbling (ichkidan)
```

---

## 📌 `event.preventDefault()` — Default Harakatni Bloklash

```javascript
// Link bosilganda sahifa o'zgarmasin
document.querySelector("a").addEventListener("click", (e) => {
  e.preventDefault();
  console.log("Link bosildi, lekin o'tkazilmadi");
});

// Form submitda sahifa yangilanmasin
document.querySelector("form").addEventListener("submit", (e) => {
  e.preventDefault();
  // O'zimiz ma'lumotni qayta ishlaymiz
  let qiymat = document.querySelector("input").value;
  console.log("Kiritildi:", qiymat);
});
```

---

## 📌 Event Delegation (Delegatsiya)

Ko'p elementlarga alohida event qo'shish o'rniga, ota elementga bitta event qo'shamiz.

```javascript
// ❌ Samarasiz usul — har bir elementga alohida
document.querySelectorAll("li").forEach(li => {
  li.addEventListener("click", () => console.log(li.textContent));
});

// ✅ Samarali usul — Event Delegation
document.getElementById("royxat").addEventListener("click", (e) => {
  if (e.target.tagName === "LI") {
    console.log(e.target.textContent);
    e.target.classList.toggle("active");
  }
});

// Dinamik qo'shilgan elementlar uchun ham ishlaydi!
const yangiLi = document.createElement("li");
yangiLi.textContent = "Yangi element";
document.getElementById("royxat").appendChild(yangiLi);
// Yangi li ham click eventi bilan ishlaydi ✅
```

---

## 📌 Klaviatura Eventlari

```javascript
document.addEventListener("keydown", (e) => {
  console.log(e.key);    // "Enter", "a", "ArrowLeft"
  console.log(e.code);   // "Enter", "KeyA", "ArrowLeft"
  console.log(e.ctrlKey); // Ctrl bosilganda true
  console.log(e.shiftKey); // Shift bosilganda true

  // Enter bosilsa
  if (e.key === "Enter") {
    console.log("Enter bosildi!");
  }

  // Ctrl + S (saqlab qo'yish)
  if (e.ctrlKey && e.key === "s") {
    e.preventDefault();
    console.log("Saqlandi!");
  }
});

// Input o'zgarishida
document.querySelector("input").addEventListener("input", (e) => {
  console.log("Joriy qiymat:", e.target.value);
});
```

---

## 📌 Mouse Eventlari

```javascript
let div = document.querySelector(".box");

div.addEventListener("mouseenter", () => div.style.background = "lightblue");
div.addEventListener("mouseleave", () => div.style.background = "white");

div.addEventListener("mousemove", (e) => {
  div.textContent = `X: ${e.clientX}, Y: ${e.clientY}`;
});

div.addEventListener("dblclick", () => {
  console.log("Ikki marta bosildi!");
});

// O'ng tugma
div.addEventListener("contextmenu", (e) => {
  e.preventDefault(); // Default menyuni bloklash
  console.log("O'ng tugma!");
});
```

---

## 📌 once Option — Bir martalik Event

```javascript
document.getElementById("btn").addEventListener("click", () => {
  console.log("Faqat bir marta ishlaydi!");
}, { once: true }); // Birinchi clickdan keyin o'chadi

// Boshqa optionlar:
// { capture: true } — capturing phase
// { passive: true } — scroll uchun, preventDefault bloklanadi
```

---

## 🎯 10 ta Amaliy Vazifa — "Typing Club" O'yini

```html
<!DOCTYPE html>
<html>
<head>
  <title>Typing Club</title>
  <style>
    body { font-family: Arial, sans-serif; padding: 20px; }
    #vazifa-matn { font-size: 24px; letter-spacing: 2px; margin: 20px 0; }
    .correct { color: green; }
    .wrong { color: red; background: #ffcccc; }
    #kirish { font-size: 20px; width: 100%; padding: 10px; }
    #natija { margin-top: 20px; font-size: 18px; }
    #hisoblagich { color: blue; font-size: 16px; }
  </style>
</head>
<body>
  <h1>⌨️ Typing Club</h1>
  <div id="vazifa-matn">JavaScript</div>
  <input id="kirish" type="text" placeholder="Yozing..." autocomplete="off">
  <div id="natija"></div>
  <div id="hisoblagich">Vaqt: <span id="vaqt">30</span>s | Ball: <span id="ball">0</span></div>
  <button id="qayta">Qayta boshlash</button>

  <script>
    const so_zlar = ["JavaScript", "programming", "function", "variable", "array", "object", "loop", "event"];
    let joriySo_z = "", ball = 0, vaqtLeft = 30, timer;

    function yangiSo_z() {
      joriySo_z = so_zlar[Math.floor(Math.random() * so_zlar.length)];
      document.getElementById("vazifa-matn").textContent = joriySo_z;
      document.getElementById("kirish").value = "";
    }

    // 1. input eventida tekshiring
    document.getElementById("kirish").addEventListener("input", (e) => {
      let kiritilgan = e.target.value;
      let matn = document.getElementById("vazifa-matn");

      // 2. Har bir harf uchun rangni o'zgartiring
      let html = "";
      for (let i = 0; i < joriySo_z.length; i++) {
        if (i < kiritilgan.length) {
          let klass = kiritilgan[i] === joriySo_z[i] ? "correct" : "wrong";
          html += `<span class="${klass}">${joriySo_z[i]}</span>`;
        } else {
          html += joriySo_z[i];
        }
      }
      matn.innerHTML = html;

      // 3. To'g'ri yozilsa yangi so'z
      if (kiritilgan === joriySo_z) {
        ball++;
        document.getElementById("ball").textContent = ball;
        yangiSo_z();
      }
    });

    // 4. 30 soniyalik hisoblagich
    function boshlash() {
      ball = 0; vaqtLeft = 30;
      document.getElementById("ball").textContent = 0;
      yangiSo_z();
      clearInterval(timer);
      timer = setInterval(() => {
        vaqtLeft--;
        document.getElementById("vaqt").textContent = vaqtLeft;
        if (vaqtLeft <= 0) {
          clearInterval(timer);
          document.getElementById("kirish").disabled = true;
          document.getElementById("natija").textContent = `O'yin tugadi! Ballingiz: ${ball}`;
        }
      }, 1000);
    }

    // 5. Qayta boshlash tugmasi
    document.getElementById("qayta").addEventListener("click", () => {
      document.getElementById("kirish").disabled = false;
      document.getElementById("natija").textContent = "";
      boshlash();
    });

    // 6. ESC bosilsa inputni tozalash
    document.getElementById("kirish").addEventListener("keydown", (e) => {
      if (e.key === "Escape") e.target.value = "";
    });

    // 7. Sahifa yuklanishida avtomatik boshlash
    window.addEventListener("DOMContentLoaded", boshlash);

    // 8. Click event delegation — so'z bosilsa rang o'zgarsin
    document.getElementById("vazifa-matn").addEventListener("click", (e) => {
      e.target.style.color = `hsl(${Math.random()*360}, 70%, 50%)`;
    });

    // 9. Double click — so'zni ko'chirish
    document.getElementById("vazifa-matn").addEventListener("dblclick", () => {
      navigator.clipboard?.writeText(joriySo_z);
    });

    // 10. Visibility change — o'yin to'xtatish/davom ettirish
    document.addEventListener("visibilitychange", () => {
      if (document.hidden) clearInterval(timer);
    });
  </script>
</body>
</html>
```
