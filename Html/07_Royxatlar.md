# 07-Dars: Ro'yxatlar — `<ol>`, `<ul>`, `<dl>`

## 📌 Unordered List `<ul>` — Tartibsiz Ro'yxat

```html
<!-- Asosiy -->
<ul>
  <li>Olma</li>
  <li>Nok</li>
  <li>Banan</li>
</ul>

<!-- type atributi (CSS yaxshiroq) -->
<ul style="list-style-type: disc;">    <!-- • (default) -->
<ul style="list-style-type: circle;">  <!-- ○ -->
<ul style="list-style-type: square;">  <!-- ■ -->
<ul style="list-style-type: none;">    <!-- Belgi yo'q -->

<!-- CSS bilan boshqarish -->
<style>
.custom-list {
  list-style: none;
  padding: 0;
}
.custom-list li::before {
  content: "✅ ";  /* Custom marker */
}
</style>
```

---

## 📌 Ordered List `<ol>` — Tartibli Ro'yxat

```html
<!-- Asosiy -->
<ol>
  <li>HTML o'rgan</li>
  <li>CSS o'rgan</li>
  <li>JavaScript o'rgan</li>
</ol>

<!-- type atributi -->
<ol type="1">  <!-- 1, 2, 3 (default) -->
<ol type="a">  <!-- a, b, c -->
<ol type="A">  <!-- A, B, C -->
<ol type="i">  <!-- i, ii, iii (rim raqamlari) -->
<ol type="I">  <!-- I, II, III -->

<!-- start — boshlanish raqami -->
<ol start="5">  <!-- 5, 6, 7... -->

<!-- reversed — teskari tartib -->
<ol reversed>  <!-- 3, 2, 1 -->

<!-- value — alohida li uchun -->
<ol>
  <li value="10">O'ninchi</li>
  <li>O'n birinchi</li>
  <li value="20">Yigirmanchi</li>
</ol>
```

---

## 📌 Description List `<dl>` — Izolli Ro'yxat

```html
<!-- dt = termin, dd = tavsif -->
<dl>
  <dt>HTML</dt>
  <dd>HyperText Markup Language — sahifa tarkibi</dd>

  <dt>CSS</dt>
  <dd>Cascading Style Sheets — sahifa ko'rinishi</dd>

  <dt>JavaScript</dt>
  <dd>Veb sahifalarga interaktivlik qo'shadigan til</dd>
</dl>

<!-- Bir terminga bir nechta tavsif -->
<dl>
  <dt>Ibn Sino</dt>
  <dd>Buyuk tabib (980-1037)</dd>
  <dd>Faylasuf va matematik</dd>
  <dd>"Tib Qonunlari" muallifi</dd>
</dl>
```

---

## 📌 Nested List — Ichkilashgan Ro'yxat

```html
<!-- ul ichida ul -->
<ul>
  <li>Frontend
    <ul>
      <li>HTML</li>
      <li>CSS
        <ul>
          <li>Flexbox</li>
          <li>Grid</li>
          <li>Animation</li>
        </ul>
      </li>
      <li>JavaScript</li>
    </ul>
  </li>
  <li>Backend
    <ul>
      <li>Node.js</li>
      <li>Python</li>
    </ul>
  </li>
</ul>

<!-- ol ichida ul -->
<ol>
  <li>Birinchi qadam
    <ul>
      <li>Kichik vazifa 1</li>
      <li>Kichik vazifa 2</li>
    </ul>
  </li>
  <li>Ikkinchi qadam</li>
</ol>
```

---

## 🎯 10 ta Amaliy Vazifa

```html
<!DOCTYPE html>
<html lang="uz">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Ro'yxatlar Amaliyot</title>
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    body { font-family: "Segoe UI", sans-serif; color: #1a1a2e; background: #f8f9fa; }
    .sahifa { max-width: 1000px; margin: 0 auto; padding: 40px 20px; }
    h2 { font-size: 24px; margin-bottom: 20px; padding-bottom: 8px; border-bottom: 2px solid #f0f0f0; }
    section { margin-bottom: 48px; background: white; padding: 28px; border-radius: 16px; box-shadow: 0 2px 12px rgba(0,0,0,0.06); }

    /* === Vazifa 1: Navigatsiya ul tizimi === */
    .nav-tizim { display: flex; gap: 0; }
    .nav-tizim ul { list-style: none; display: flex; gap: 4px; }
    .nav-tizim a { text-decoration: none; color: #555; padding: 8px 16px; border-radius: 8px; transition: all 0.2s; }
    .nav-tizim a:hover, .nav-tizim a.faol { background: #f0f4ff; color: royalblue; font-weight: 600; }

    /* === Vazifa 2: Bozor ro'yxati (checked list) === */
    .bozor-royhat { list-style: none; }
    .bozor-royhat li {
      display: flex; align-items: center; gap: 12px;
      padding: 12px; border-bottom: 1px solid #f5f5f5;
      transition: background 0.2s; cursor: pointer;
    }
    .bozor-royhat li:hover { background: #f8f9ff; }
    .bozor-royhat input[type="checkbox"] { width: 18px; height: 18px; accent-color: royalblue; }
    .bozor-royhat .miqdor { margin-left: auto; color: #888; font-size: 13px; }

    /* === Vazifa 3: IT kompaniyalar === */
    .kompaniya-royhat { list-style: none; display: grid; grid-template-columns: repeat(auto-fill, minmax(200px, 1fr)); gap: 12px; }
    .kompaniya-karta {
      background: #f8f9fa; border-radius: 10px; padding: 16px;
      transition: transform 0.2s, box-shadow 0.2s;
    }
    .kompaniya-karta:hover { transform: translateY(-3px); box-shadow: 0 4px 16px rgba(0,0,0,0.1); }
    .kompaniya-karta .raqam { font-size: 24px; font-weight: 700; color: royalblue; }
    .kompaniya-karta .nom { font-weight: 600; margin: 4px 0; }
    .kompaniya-karta .mamlakat { font-size: 12px; color: #888; }

    /* === Vazifa 4: Steps (Qadamlar) === */
    .qadamlar { list-style: none; position: relative; }
    .qadamlar li {
      display: flex; gap: 16px; padding: 20px 0;
      border-bottom: 1px solid #f0f0f0;
    }
    .qadam-raqam {
      width: 36px; height: 36px; border-radius: 50%;
      background: royalblue; color: white; font-weight: 700;
      display: flex; align-items: center; justify-content: center; flex-shrink: 0;
    }
    .qadam-info h4 { margin-bottom: 4px; }
    .qadam-info p  { color: #666; font-size: 14px; }

    /* === Vazifa 5: Glossariy (dl) === */
    .glossariy { display: grid; grid-template-columns: auto 1fr; gap: 12px 24px; }
    .glossariy dt { font-weight: 700; color: royalblue; padding-top: 4px; }
    .glossariy dd { color: #555; line-height: 1.6; border-left: 3px solid #f0f0f0; padding-left: 16px; }

    /* === Vazifa 6: Daraxt navigatsiya === */
    .daraxt { list-style: none; }
    .daraxt ul { list-style: none; padding-left: 24px; border-left: 2px solid #f0f0f0; }
    .daraxt li { padding: 6px 0; }
    .daraxt > li > span { font-weight: 700; color: royalblue; }
    .daraxt details > summary { cursor: pointer; font-weight: 600; padding: 4px 0; }
    .daraxt details > summary:hover { color: royalblue; }

    /* === Vazifa 7: O'quv dastur === */
    .dastur { counter-reset: section; list-style: none; }
    .dastur > li {
      counter-increment: section;
      display: flex; gap: 16px; padding: 14px;
      border: 1px solid #f0f0f0; border-radius: 10px; margin-bottom: 8px;
    }
    .dastur > li::before {
      content: counter(section, decimal-leading-zero);
      font-size: 20px; font-weight: 700; color: royalblue;
      min-width: 32px;
    }
    .dastur li h4 { margin-bottom: 4px; }
    .dastur li p  { font-size: 13px; color: #666; }
  </style>
</head>
<body>
<div class="sahifa">

  <!-- Vazifa 1: Navigatsiya -->
  <section>
    <div class="nav-tizim">
      <ul>
        <li><a href="#" class="faol">Bosh sahifa</a></li>
        <li><a href="#">Kurslar</a></li>
        <li><a href="#">Blog</a></li>
        <li><a href="#">Portfolio</a></li>
        <li><a href="#">Aloqa</a></li>
      </ul>
    </div>
  </section>

  <!-- Vazifa 2: Bozor ro'yxati (checkbox) -->
  <section>
    <h2>🛒 Bozor Ro'yxati</h2>
    <ul class="bozor-royhal">
      <li class="bozor-royhal"><input type="checkbox"> <span>Olma</span> <span class="miqdor">2 kg</span></li>
      <li><input type="checkbox" checked> <span style="text-decoration:line-through; color: #aaa;">Nok</span> <span class="miqdor">1 kg</span></li>
      <li><input type="checkbox"> <span>Banan</span> <span class="miqdor">5 dona</span></li>
      <li><input type="checkbox"> <span>Sabzi</span> <span class="miqdor">0.5 kg</span></li>
      <li><input type="checkbox" checked> <span style="text-decoration:line-through; color: #aaa;">Sut</span> <span class="miqdor">2 litr</span></li>
    </ul>
  </section>

  <!-- Vazifa 3: IT kompaniyalar -->
  <section>
    <h2>🏢 Mashhur IT Kompaniyalar</h2>
    <ol class="kompaniya-royhat" type="1">
      <li class="kompaniya-karta">
        <div class="raqam">1</div>
        <div class="nom">Apple</div>
        <div class="mamlakat">🇺🇸 AQSh</div>
      </li>
      <li class="kompaniya-karta">
        <div class="raqam">2</div>
        <div class="nom">Microsoft</div>
        <div class="mamlakat">🇺🇸 AQSh</div>
      </li>
      <li class="kompaniya-karta">
        <div class="raqam">3</div>
        <div class="nom">Google</div>
        <div class="mamlakat">🇺🇸 AQSh</div>
      </li>
      <li class="kompaniya-karta">
        <div class="raqam">4</div>
        <div class="nom">Amazon</div>
        <div class="mamlakat">🇺🇸 AQSh</div>
      </li>
      <li class="kompaniya-karta">
        <div class="raqam">5</div>
        <div class="nom">Samsung</div>
        <div class="mamlakat">🇰🇷 Koreya</div>
      </li>
      <li class="kompaniya-karta">
        <div class="raqam">6</div>
        <div class="nom">Meta</div>
        <div class="mamlakat">🇺🇸 AQSh</div>
      </li>
    </ol>
  </section>

  <!-- Vazifa 4: Qadamlar (ol) -->
  <section>
    <h2>🚀 Frontend O'rganish Yo'li</h2>
    <ol class="qadamlar">
      <li>
        <div class="qadam-raqam">1</div>
        <div class="qadam-info">
          <h4>HTML Asoslari</h4>
          <p>Teglar, atributlar, semantik elementlar. ~2 hafta</p>
        </div>
      </li>
      <li>
        <div class="qadam-raqam">2</div>
        <div class="qadam-info">
          <h4>CSS va Dizayn</h4>
          <p>Box model, Flexbox, Grid, Responsive. ~4 hafta</p>
        </div>
      </li>
      <li>
        <div class="qadam-raqam">3</div>
        <div class="qadam-info">
          <h4>JavaScript</h4>
          <p>DOM, Events, Fetch API, ES6+. ~8 hafta</p>
        </div>
      </li>
      <li>
        <div class="qadam-raqam">4</div>
        <div class="qadam-info">
          <h4>React.js</h4>
          <p>Komponentlar, Hooks, State. ~6 hafta</p>
        </div>
      </li>
    </ol>
  </section>

  <!-- Vazifa 5: Glossariy (dl) -->
  <section>
    <h2>📚 Atamalar Lug'ati</h2>
    <dl class="glossariy">
      <dt>HTML</dt>
      <dd>HyperText Markup Language — veb sahifalar tarkibini belgilash tili</dd>
      <dt>CSS</dt>
      <dd>Cascading Style Sheets — sahifa ko'rinishi va dizaynini boshqarish tili</dd>
      <dt>JavaScript</dt>
      <dd>Brauzerda amalga oshiriladigan dasturlash tili, interaktivlik uchun</dd>
      <dt>DOM</dt>
      <dd>Document Object Model — HTML elementlarini JavaScript orqali boshqarish interfeysi</dd>
      <dt>API</dt>
      <dd>Application Programming Interface — dasturlar o'rtasidagi muloqot qoidalari</dd>
    </dl>
  </section>

  <!-- Vazifa 6: Daraxt (nested) -->
  <section>
    <h2>🌳 Texnologiyalar Daraxti</h2>
    <ul class="daraxt">
      <li>
        <details open>
          <summary>Frontend</summary>
          <ul>
            <li>HTML5</li>
            <li>
              <details>
                <summary>CSS3</summary>
                <ul>
                  <li>Flexbox</li>
                  <li>Grid</li>
                  <li>Animation</li>
                  <li>Sass/SCSS</li>
                </ul>
              </details>
            </li>
            <li>
              <details>
                <summary>JavaScript</summary>
                <ul>
                  <li>ES6+</li>
                  <li>React</li>
                  <li>TypeScript</li>
                </ul>
              </details>
            </li>
          </ul>
        </details>
      </li>
      <li>
        <details>
          <summary>Backend</summary>
          <ul>
            <li>Node.js</li>
            <li>Python (Django, FastAPI)</li>
            <li>PostgreSQL</li>
          </ul>
        </details>
      </li>
    </ul>
  </section>

  <!-- Vazifa 7-10: O'quv dastur -->
  <section>
    <h2>📋 Kurs Dasturi</h2>
    <ol class="dastur">
      <li>
        <div>
          <h4>HTML Kirish</h4>
          <p>Web nima, HTML tuzilmasi, teglar va atributlar</p>
        </div>
      </li>
      <li>
        <div>
          <h4>CSS Asoslari</h4>
          <p>Selektorlar, Box Model, Colors va Typography</p>
        </div>
      </li>
      <li>
        <div>
          <h4>Flexbox va Grid</h4>
          <p>Zamonaviy CSS layout tizimlari</p>
        </div>
      </li>
      <li>
        <div>
          <h4>JavaScript</h4>
          <p>Asoslar, DOM, Events, Async</p>
        </div>
      </li>
      <li>
        <div>
          <h4>Yakuniy Loyiha</h4>
          <p>Portfolio sayt — HTML, CSS, JavaScript bilan</p>
        </div>
      </li>
    </ol>
  </section>

</div>
</body>
</html>
```
