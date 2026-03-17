# 03-Dars: Tag lar va Attribute lar

## 📌 HTML Tag nima?

```html
<!-- Sintaksis -->
<tagNomi atribut="qiymat">Kontent</tagNomi>

<!-- Anatomiya -->
<p class="kirish" id="bosh-para">Bu paragraf.</p>
 ↑   ↑              ↑            ↑
Tag  Attribute      Attribute    Kontent

<!-- Yopuvchi tag bo'lmagan (self-closing) -->
<img src="rasm.jpg" alt="Rasm">
<br>
<hr>
<input type="text">
<meta charset="UTF-8">
<link rel="stylesheet" href="style.css">
```

---

## 📌 HTML Tags va Ularning Vazifalari

```html
<!-- Sarlavhalar (h1 eng muhim, h6 eng kam muhim) -->
<h1>Bosh sarlavha — sahifada BITTA bo'lishi kerak</h1>
<h2>Ikkinchi darajali sarlavha</h2>
<h3>Uchinchi darajali sarlavha</h3>
<h4>To'rtinchi darajali sarlavha</h4>
<h5>Beshinchi darajali sarlavha</h5>
<h6>Oltinchi darajali sarlavha</h6>

<!-- Matn teglar -->
<p>Paragraf — matn uchun asosiy tag</p>
<br>        <!-- Yangi qator (satr uzilishi) -->
<hr>        <!-- Gorizontal chiziq (tematik ajratuvchi) -->

<!-- Matn formatlash -->
<strong>Muhim (qalin)</strong>        <!-- Semantik: muhimlik -->
<b>Qalin (faqat vizual)</b>          <!-- Vizual: faqat qalin -->
<em>Ta'kidlangan (kursiv)</em>       <!-- Semantik: ta'kid -->
<i>Kursiv (faqat vizual)</i>        <!-- Vizual: faqat kursiv -->
<u>Tagiga chizilgan</u>
<s>Ustiga chizilgan</s>              <!-- Eskirgan kontent -->
<del>O'chirilgan</del>               <!-- Semantik: o'chirilgan -->
<ins>Qo'shilgan</ins>               <!-- Semantik: yangi qo'shilgan -->
<mark>Belgilangan (sariq)</mark>     <!-- Ta'kidlash -->
<sub>Pastki</sub>                    <!-- H₂O, log₂ -->
<sup>Yuqori</sup>                    <!-- x², 10³ -->
<code>console.log('kode')</code>    <!-- Kod matni -->
<pre>   Bo'shliqlar    saqlanadi</pre> <!-- Formatlangan matn -->
<blockquote>Iqtibos matni</blockquote>
<q>Qisqa iqtibos</q>
<abbr title="HyperText Markup Language">HTML</abbr>
<kbd>Ctrl + S</kbd>                 <!-- Klaviatura tugmasi -->
```

---

## 📌 Juft va To'q Taglar

```html
<!-- JUFT TAGLAR — ochuvchi va yopuvchi -->
<h1>Sarlavha</h1>
<p>Paragraf</p>
<div>Blok</div>
<span>Inline</span>
<a href="#">Havola</a>

<!-- TO'Q TAGLAR — faqat ochuvchi (self-closing) -->
<br>           <!-- Satr uzilishi -->
<hr>           <!-- Gorizontal chiziq -->
<img src="rasm.jpg" alt="Rasm tavsifi">
<input type="text" placeholder="Yozing">
<meta charset="UTF-8">
<link rel="stylesheet" href="style.css">

<!-- HTML5 da to'q taglarni yopish shart emas -->
<br>     yoki     <br/>   (ikkisi ham to'g'ri)
```

---

## 📌 Atributlar va Ularning Vazifalari

```html
<!-- Umumiy atributlar (har qanday elementda ishlatiladi) -->
<div
  id="noyob-id"               <!-- Noyob identifikator (CSS #id, JS getElementById) -->
  class="klass1 klass2"       <!-- CSS sinflari (bo'sh joy bilan ajratiladi) -->
  style="color: red;"         <!-- Inline CSS (kamdan-kam) -->
  title="Qo'shimcha ma'lumot" <!-- Hover tooltip -->
  lang="uz"                   <!-- Element tili -->
  hidden                      <!-- Elementni yashirish -->
  tabindex="0"                <!-- Klaviatura navigatsiya tartibi -->
  aria-label="Tavsif"         <!-- Ekran o'quvchi uchun -->
  data-id="42"                <!-- Custom atribut (JavaScript uchun) -->
>
```

---

## 📌 Atribut Turlari

```html
<!-- 1. Qiymatli atribut -->
<img src="rasm.jpg" alt="Tavsif">
<a href="https://google.com">Google</a>
<input type="email" placeholder="Email kiriting">

<!-- 2. Boolean atribut (faqat nomi, qiymatsiz) -->
<input disabled>          <!-- O'chirilgan input -->
<input required>          <!-- Majburiy input -->
<input checked>           <!-- Belgilangan checkbox -->
<input readonly>          <!-- Faqat o'qish -->
<video autoplay muted>    <!-- Avtoyuklash, ovozisiz -->
<details open>            <!-- Ochiq holat -->

<!-- 3. Enumerated (aniq qiymatlar ro'yxati) -->
<input type="text">       <!-- text, password, email, number... -->
<a target="_blank">       <!-- _blank, _self, _parent, _top -->
<form method="get">       <!-- get, post -->

<!-- 4. Global data atributlar (JavaScript uchun) -->
<div data-user-id="123" data-role="admin">
  Foydalanuvchi
</div>
<!-- JS: element.dataset.userId  → "123" -->
<!-- JS: element.dataset.role    → "admin" -->
```

---

## 📌 Style Attribute (Inline CSS)

```html
<!-- style atributi — to'g'ridan to'g'ri CSS -->
<p style="color: royalblue; font-size: 18px; font-weight: bold;">
  Bu ko'k, qalin, 18px matn
</p>

<div style="
  background: linear-gradient(135deg, #667eea, #764ba2);
  padding: 20px;
  border-radius: 12px;
  color: white;
">
  Gradient blok
</div>

<!-- ⚠️ Inline style → Faqat test/prototip uchun -->
<!-- Production da external CSS qiling! -->
```

---

## 📌 Tag lar (i, u, b, mark, strong)

```html
<!-- Semantik vs Vizual farqi -->

<!-- MUHIM (Semantik) — ekran o'quvchilar uchun ma'nosi bor -->
<strong>Bu juda muhim ma'lumot!</strong>  <!-- screen reader: alohida o'qiydi -->
<em>Bu ta'kidlangan narsa</em>            <!-- screen reader: alohida o'qiydi -->

<!-- VIZUAL (Faqat ko'rinish) — semantik ma'no yo'q -->
<b>Faqat qalin ko'rsatish uchun</b>
<i>Faqat kursiv ko'rsatish uchun</i>
<u>Faqat tagiga chizish uchun</u>

<!-- mark — ta'kidlash -->
<p>Qidiruv natijasida <mark>HTML</mark> topildi</p>

<!-- Amaliy misollar -->
<p>Do'konda <mark>chegirma</mark> mavjud!</p>
<p>To'lov: <del>150,000</del> <ins>99,000</ins> so'm</p>
<p>H<sub>2</sub>O — suv formulasi</p>
<p>E = mc<sup>2</sup> — Eynshteyn formulasi</p>
```

---

## 🎯 10 ta Amaliy Vazifa

### Vazifa 1: Matn formatlash sahifasi
```html
<!DOCTYPE html>
<html lang="uz">
<head>
  <meta charset="UTF-8">
  <title>Matn Formatlash</title>
</head>
<body>
  <h1>HTML Matn Formatlash</h1>

  <p>Bu <strong>juda muhim</strong> narsa va bu <em>ta'kidlangan</em> so'z.</p>
  <p>Bu <b>qalin</b> va bu <i>kursiv</i> va bu <u>tagiga chizilgan</u>.</p>
  <p>H<sub>2</sub>O va E = mc<sup>2</sup></p>
  <p>Narx: <del>100,000</del> <ins>75,000</ins> so'm</p>
  <p>Qidiruv: <mark>HTML</mark> mavzusi topildi</p>
  <p>Tugma: <kbd>Ctrl + S</kbd> = Saqlash</p>
  <p>Kod: <code>console.log("Salom")</code></p>

  <blockquote>
    "Dasturlash — bu she'r yozishga o'xshaydi, faqat kompyuter uchun."
  </blockquote>
</body>
</html>
```

### Vazifa 2: Atributlardan foydalanish
```html
<!-- id, class, style, title, data- atributlarini ishlatib ko'ring -->
<div
  id="asosiy-blok"
  class="karta aktiv"
  style="padding: 20px; background: #f0f4ff; border-radius: 12px;"
  title="Bu blok ustiga surganda bu matn chiqadi"
  data-user="100"
  data-rang="ko'k"
>
  Atribut sinov bloki
</div>
```

### Vazifa 3: Haftalik imtihon — Text Content sahifasi
```html
<!DOCTYPE html>
<html lang="uz">
<head>
  <meta charset="UTF-8">
  <title>Mening Blog Postim</title>
</head>
<body>
  <h1>CSS nima va nima uchun kerak?</h1>
  <p><strong>CSS (Cascading Style Sheets)</strong> — veb sahifalarning ko'rinishini boshqaruvchi til.</p>
  <h2>CSS ning asosiy afzalliklari</h2>
  <p>CSS yordamida <em>ranglar, shriftlar, bo'shliqlar</em> va ko'plab xossalarni boshqarish mumkin.</p>
  <h3>Misol kod</h3>
  <pre><code>
h1 {
  color: royalblue;
  font-size: 48px;
}
  </code></pre>
  <hr>
  <p><mark>Eslatma:</mark> CSS o'rganish qiyin emas!</p>
</body>
</html>
```

### Vazifa 4: Boolean atributlarni sinash
```html
<form>
  <input type="text" value="O'zgartirib bo'lmaydi" readonly><br><br>
  <input type="text" placeholder="Yozip bo'lmaydi" disabled><br><br>
  <input type="checkbox" checked> Belgilangan<br>
  <input type="checkbox"> Belgilanmagan<br><br>
  <input type="text" required placeholder="Bu majburiy maydon">
  <button type="submit">Yuborish</button>
</form>
```

### Vazifa 5: data- atributlarini JavaScript bilan
```html
<!DOCTYPE html>
<html lang="uz">
<head><meta charset="UTF-8"><title>Data Atribut</title></head>
<body>
  <button data-rang="ko'k" data-hajm="katta" onclick="ma'lumotKo'rsat(this)">
    Ma'lumotni Ko'rsat
  </button>
  <p id="natija"></p>

  <script>
    function ma'lumotKo'rsat(el) {
      const rang = el.dataset.rang;
      const hajm = el.dataset.hajm;
      document.getElementById("natija").textContent =
        `Rang: ${rang}, Hajm: ${hajm}`;
    }
  </script>
</body>
</html>
```

### Vazifa 6: abbr va title taglarini ishlatish
```html
<p>
  <abbr title="HyperText Markup Language">HTML</abbr>,
  <abbr title="Cascading Style Sheets">CSS</abbr> va
  <abbr title="JavaScript">JS</abbr> — veb texnologiyalarining uchburchagi.
</p>
<p>
  <abbr title="World Wide Web Consortium">W3C</abbr>
  veb standartlarini belgilaydigan tashkilot.
</p>
```

### Vazifa 7: pre va code teglarini ishlatish
```html
<h2>JavaScript Kodi</h2>
<pre><code>
// Massiv yaratish
const mevalar = ["olma", "nok", "banan"];

// Har biri uchun chiqarish
mevalar.forEach(meva => {
  console.log(meva);
});
</code></pre>
```

### Vazifa 8: Wikipedia dan o'rganish
```
1. https://en.wikipedia.org/wiki/Avicenna oching
2. Sahifada quyidagi teglarni toping (DevTools bilan):
   - strong teglar (muhim so'zlar)
   - em teglar (lotin nomlari)
   - sup teglar (izohlar raqami)
   - blockquote teglar
   - abbr teglar
3. Ularning qanday ishlatilganini kuzating
```

### Vazifa 9: W3School dan o'rganish
```
1. https://www.w3schools.com/html/html_formatting.asp oching
2. Barcha formatlash teglarini o'qing
3. "Try it Yourself" da har birini sinab ko'ring
4. Quyidagi teglarni o'rganing:
   <bdo dir="rtl">O'ngdan chapga matn</bdo>
   <wbr> — majburiy uzilish nuqtasi
```

### Vazifa 10: To'liq maqola sahifasi
```html
<!DOCTYPE html>
<html lang="uz">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Avitsenna — Buyuk Alloma</title>
  <style>
    body { max-width: 800px; margin: 0 auto; padding: 40px 20px; font-family: Georgia, serif; line-height: 1.8; }
    h1 { font-size: 36px; margin-bottom: 8px; }
    .muallif { color: #888; font-size: 14px; margin-bottom: 24px; }
    blockquote { border-left: 4px solid royalblue; padding-left: 20px; font-style: italic; color: #555; }
    mark { background: #fff3cd; padding: 0 2px; }
  </style>
</head>
<body>
  <article>
    <h1>Ibn Sino — <abbr title="Abu Ali al-Husayn ibn Abd Allah ibn Sina">Avitsenna</abbr></h1>
    <p class="muallif">Muallif: Ali Valiev | <time datetime="2024-01-15">15 yanvar 2024</time></p>
    <hr>
    <p>
      <strong>Ibn Sino</strong> (<em>Abu Ali al-Husayn ibn Abd Allah ibn Sina</em>),
      G'arbda <mark>Avitsenna</mark> nomi bilan mashhur, <strong>980</strong>-yilda
      tug'ilgan buyuk alloma, tabib va faylasuf.
    </p>
    <blockquote>
      "Bilim — g'azna, uni izlamoq esa qurollanuv."
      <br>— Ibn Sino
    </blockquote>
    <p>
      Uning asosiy asari <cite>Tib Qonunlari</cite><sup>[1]</sup> bo'lib,
      bu asar asrlar davomida tibbiyot <del>fan</del> <ins>ilmining</ins> asosi bo'lib keldi.
    </p>
    <p>
      Kimyoviy formula: H<sub>2</sub>O — suv.
      Matematik ifoda: E = mc<sup>2</sup>.
    </p>
  </article>
</body>
</html>
```
