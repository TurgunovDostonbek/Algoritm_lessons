# 17-Dars: DOM — 3-qism (Elementlarni Boshqarish + To Do List)

## 📌 Him va Atributlarni O'zgartirish

```javascript
// textContent, innerHTML, innerText
let el = document.getElementById("sarlavha");

el.textContent = "Yangi matn";          // Matn (xavfsiz)
el.innerHTML = "<em>Kursiv matn</em>";  // HTML (XSS xavfli)
el.innerText = "Ko'rinuvchi matn";      // CSS ga bog'liq

// Atributlar
let img = document.querySelector("img");
img.src = "/yangi-rasm.jpg";            // To'g'ridan property
img.alt = "Yangi rasm";
img.setAttribute("data-id", "42");
img.getAttribute("src");                // Olish
img.removeAttribute("title");           // O'chirish
img.hasAttribute("src");                // true/false

// data-* atributlar
let karta = document.querySelector("[data-user-id]");
console.log(karta.dataset.userId);      // data-user-id → camelCase
karta.dataset.status = "faol";          // Qo'shish
```

---

## 📌 Elementlarni Qo'shish va Olib Tashlash

```javascript
// Yaratish
let yangiDiv = document.createElement("div");
yangiDiv.className = "karta";
yangiDiv.textContent = "Yangi karta";

let container = document.getElementById("container");

// Qo'shish usullari
container.append(yangiDiv);                          // Oxiriga
container.prepend(yangiDiv);                         // Boshiga
container.append("Matn ham qo'shish mumkin!");        // Matn tugun
container.insertAdjacentHTML("beforeend", "<p>HTML</p>"); // HTML string
container.insertAdjacentElement("afterbegin", yangiDiv);  // Aniq joy

// insertAdjacentHTML joylari:
// "beforebegin" — elementdan oldin
// "afterbegin"  — elementning boshi
// "beforeend"   — elementning oxiri
// "afterend"    — elementdan keyin

// O'chirish
yangiDiv.remove();
// container.removeChild(yangiDiv); // Eski usul

// Almashtirish
let eskilDiv = document.querySelector(".eski");
eskilDiv.replaceWith(yangiDiv);
```

---

## 📌 Klasslarni Boshqarish — `classList`

```javascript
let el = document.querySelector(".katak");

// Asosiy metodlar
el.classList.add("active", "highlight");     // Bir nechta qo'shish
el.classList.remove("hidden", "disabled");   // Bir nechta olib tashlash
el.classList.toggle("dark-mode");            // Almashtirish
el.classList.toggle("open", true);           // Force qo'shish
el.classList.toggle("closed", false);        // Force olib tashlash
el.classList.replace("red", "blue");         // Almashtirish
el.classList.contains("active");             // boolean

// Barcha klasslar
console.log(el.classList.toString());
console.log([...el.classList]);              // Massivga

// className (eski usul)
el.className = "yangi-klass";               // Hammani almahshtiradi!
el.className += " qo_shimcha";              // Qo'shish
```

---

## 📌 Stillarni Boshqarish

```javascript
let el = document.querySelector(".box");

// Inline style — to'g'ridan
el.style.width = "200px";
el.style.height = "200px";
el.style.backgroundColor = "royalblue";    // camelCase!
el.style.border = "2px solid #333";
el.style.display = "none";                  // Yashirish
el.style.display = "";                      // Tiklanish (inline olib tashlash)

// Hisoblangan stil (computed) — aktual qiymatlar
let hisoblangan = getComputedStyle(el);
console.log(hisoblangan.width);             // "200px"
console.log(hisoblangan.backgroundColor);  // "rgb(65, 105, 225)"

// CSS o'zgaruvchilar (custom properties)
document.documentElement.style.setProperty("--asosiy-rang", "#ff6b6b");
let qiymat = getComputedStyle(document.documentElement).getPropertyValue("--asosiy-rang");
```

---

## 📌 Element O'lchamlari va Holati

```javascript
let el = document.querySelector(".box");

// O'lchamlar
el.offsetWidth;    // To'liq kengligi (padding + border bilan)
el.offsetHeight;   // To'liq balandligi
el.clientWidth;    // Faqat padding bilan (scrollbar yo'q)
el.scrollHeight;   // Ichki to'liq balandlik (scroll bilan)

// Koordinatalar
let rect = el.getBoundingClientRect();
console.log(rect.top, rect.left);    // Viewport ga nisbatan
console.log(rect.width, rect.height);

// Scroll
window.scrollTo({ top: 0, behavior: "smooth" });       // Tepaga
el.scrollIntoView({ behavior: "smooth" });              // Elementga
```

---

## 📌 `classList` bilan Toggle Patterns

```javascript
// Qorong'u/yorug' tema
document.getElementById("tema-tugma").addEventListener("click", () => {
  document.body.classList.toggle("dark-mode");
});

// Accordion (ochish/yopish)
document.querySelectorAll(".accordion-btn").forEach(btn => {
  btn.addEventListener("click", function() {
    let kontent = this.nextElementSibling;
    kontent.classList.toggle("open");
    this.classList.toggle("active");
  });
});

// Dropdown menyu
document.querySelector(".dropdown-btn").addEventListener("click", (e) => {
  e.stopPropagation(); // Yopilmaslik uchun
  document.querySelector(".dropdown-menu").classList.toggle("show");
});

// Tashqariga bosilsa yop
document.addEventListener("click", () => {
  document.querySelector(".dropdown-menu")?.classList.remove("show");
});
```

---

## 🎯 10 ta Amaliy Vazifa — "To Do List" Loyihasi

```html
<!DOCTYPE html>
<html lang="uz">
<head>
  <meta charset="UTF-8">
  <title>To Do List</title>
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }
    body { font-family: "Segoe UI", sans-serif; background: #f0f2f5; padding: 30px; }
    .app { max-width: 500px; margin: 0 auto; background: white; border-radius: 12px;
           padding: 24px; box-shadow: 0 4px 20px rgba(0,0,0,.1); }
    h1 { color: #333; margin-bottom: 20px; text-align: center; }
    .kirish-qator { display: flex; gap: 10px; margin-bottom: 20px; }
    input[type="text"] { flex: 1; padding: 10px 14px; border: 2px solid #ddd;
                         border-radius: 8px; font-size: 16px; outline: none; }
    input:focus { border-color: #667eea; }
    button { padding: 10px 18px; background: #667eea; color: white; border: none;
             border-radius: 8px; cursor: pointer; font-size: 15px; transition: .2s; }
    button:hover { background: #5a6fd6; }
    .filtrlar { display: flex; gap: 8px; margin-bottom: 16px; }
    .filtr-btn { padding: 6px 14px; border: 2px solid #ddd; background: white;
                 border-radius: 20px; cursor: pointer; font-size: 13px; }
    .filtr-btn.active { border-color: #667eea; color: #667eea; font-weight: bold; }
    ul { list-style: none; }
    li { display: flex; align-items: center; gap: 10px; padding: 12px;
         margin-bottom: 8px; background: #f8f9fa; border-radius: 8px;
         transition: .2s; border-left: 4px solid transparent; }
    li:hover { background: #e9ecef; }
    li.bajarildi { text-decoration: line-through; color: #999; border-left-color: #51cf66; }
    li .matn { flex: 1; font-size: 15px; }
    li .o_ch-btn { background: #ff6b6b; padding: 4px 10px; font-size: 13px; }
    li .o_ch-btn:hover { background: #fa5252; }
    #statistika { margin-top: 16px; font-size: 13px; color: #666; text-align: center; }
    .bo_sh-xabar { text-align: center; color: #999; padding: 20px; }
  </style>
</head>
<body>
<div class="app">
  <h1>✅ To Do List</h1>

  <!-- Vazifa 1: Kirish qatori -->
  <div class="kirish-qator">
    <input type="text" id="vazifa-kirish" placeholder="Yangi vazifa...">
    <button id="qo_sh-btn">Qo'shish</button>
  </div>

  <!-- Vazifa 2: Filtr tugmalari -->
  <div class="filtrlar">
    <button class="filtr-btn active" data-filtr="hammasi">Hammasi</button>
    <button class="filtr-btn" data-filtr="faol">Faol</button>
    <button class="filtr-btn" data-filtr="bajarildi">Bajarildi</button>
  </div>

  <ul id="vazifalar-royxati"></ul>
  <div id="statistika"></div>
  <button id="hammani-tozala" style="width:100%;margin-top:10px;background:#ff6b6b;">
    Bajarilganlarni tozala
  </button>
</div>

<script>
  // Ma'lumotlar
  let vazifalar = JSON.parse(localStorage.getItem("vazifalar")) || [];
  let joriyFiltr = "hammasi";

  // Statistika
  function statistikaYangilash() {
    let jami = vazifalar.length;
    let bajarildi = vazifalar.filter(v => v.bajarildi).length;
    document.getElementById("statistika").textContent =
      `${bajarildi}/${jami} vazifalari bajarildi`;
  }

  // LocalStorage saqlash
  function saqlash() {
    localStorage.setItem("vazifalar", JSON.stringify(vazifalar));
  }

  // Vazifa 3: Ro'yxatni render qilish
  function renderQilish() {
    let royxat = document.getElementById("vazifalar-royxati");
    royxat.innerHTML = "";

    let ko_rsatiladiganlar = vazifalar.filter(v => {
      if (joriyFiltr === "faol") return !v.bajarildi;
      if (joriyFiltr === "bajarildi") return v.bajarildi;
      return true;
    });

    if (ko_rsatiladiganlar.length === 0) {
      royxat.innerHTML = `<div class="bo_sh-xabar">Vazifalar yo'q 🎉</div>`;
      statistikaYangilash();
      return;
    }

    ko_rsatiladiganlar.forEach(vazifa => {
      let li = document.createElement("li");
      if (vazifa.bajarildi) li.classList.add("bajarildi");
      li.dataset.id = vazifa.id;

      li.innerHTML = `
        <input type="checkbox" ${vazifa.bajarildi ? "checked" : ""}>
        <span class="matn">${vazifa.matn}</span>
        <button class="o_ch-btn">🗑️</button>
      `;

      // Vazifa 4: Checkbox — bajarildi toggle
      li.querySelector("input").addEventListener("change", function() {
        let idx = vazifalar.findIndex(v => v.id == li.dataset.id);
        vazifalar[idx].bajarildi = this.checked;
        saqlash();
        renderQilish();
      });

      // Vazifa 5: O'chirish tugmasi
      li.querySelector(".o_ch-btn").addEventListener("click", () => {
        vazifalar = vazifalar.filter(v => v.id != li.dataset.id);
        saqlash();
        renderQilish();
      });

      // Vazifa 6: Ikkimarta bosish — tahrirlash
      li.querySelector(".matn").addEventListener("dblclick", function() {
        let input = document.createElement("input");
        input.type = "text";
        input.value = this.textContent;
        input.style.cssText = "flex:1;border:none;background:transparent;font-size:15px;outline:none";
        this.replaceWith(input);
        input.focus();

        input.addEventListener("blur", function() {
          let yangiMatn = this.value.trim() || this.value;
          let idx = vazifalar.findIndex(v => v.id == li.dataset.id);
          if (yangiMatn) vazifalar[idx].matn = yangiMatn;
          saqlash();
          renderQilish();
        });

        input.addEventListener("keydown", e => {
          if (e.key === "Enter") input.blur();
        });
      });

      royxat.appendChild(li);
    });

    statistikaYangilash();
  }

  // Vazifa 7: Yangi vazifa qo'shish
  function qo_sh() {
    let input = document.getElementById("vazifa-kirish");
    let matn = input.value.trim();
    if (!matn) return;

    vazifalar.push({
      id: Date.now(),
      matn,
      bajarildi: false
    });

    input.value = "";
    saqlash();
    renderQilish();
  }

  document.getElementById("qo_sh-btn").addEventListener("click", qo_sh);

  // Vazifa 8: Enter bosilsa qo'shish
  document.getElementById("vazifa-kirish").addEventListener("keydown", e => {
    if (e.key === "Enter") qo_sh();
  });

  // Vazifa 9: Filtr tugmalari — Event Delegation
  document.querySelector(".filtrlar").addEventListener("click", (e) => {
    if (!e.target.classList.contains("filtr-btn")) return;

    document.querySelectorAll(".filtr-btn").forEach(btn => btn.classList.remove("active"));
    e.target.classList.add("active");
    joriyFiltr = e.target.dataset.filtr;
    renderQilish();
  });

  // Vazifa 10: Bajarilganlarni tozalash
  document.getElementById("hammani-tozala").addEventListener("click", () => {
    vazifalar = vazifalar.filter(v => !v.bajarildi);
    saqlash();
    renderQilish();
  });

  // Boshlang'ich render
  renderQilish();
</script>
</body>
</html>
```
