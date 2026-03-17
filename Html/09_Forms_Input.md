# 09-Dars: HTML Forms va Input Elementlar

## 📌 Form Asosiy Tuzilmasi

```html
<form action="/yuborish" method="POST">
  <!-- action — ma'lumot qayerga yuborilsin -->
  <!-- method — GET (URL da) yoki POST (body da) -->

  <label for="ism">Ism:</label>
  <input type="text" id="ism" name="ism" required>

  <button type="submit">Yuborish</button>
</form>
```

---

## 📌 Input Turlari

```html
<!-- Matn -->
<input type="text" placeholder="Ismingiz">

<!-- Parol -->
<input type="password" placeholder="Parol">

<!-- Email -->
<input type="email" placeholder="email@mail.com">

<!-- Raqam -->
<input type="number" min="0" max="100" step="5">

<!-- Telefon -->
<input type="tel" placeholder="+998 90 000 00 00">

<!-- URL -->
<input type="url" placeholder="https://...">

<!-- Qidiruv -->
<input type="search" placeholder="Qidiring...">

<!-- Rang tanlash -->
<input type="color" value="#4361ee">

<!-- Sana -->
<input type="date" min="2000-01-01" max="2030-12-31">

<!-- Vaqt -->
<input type="time">

<!-- Sana va vaqt -->
<input type="datetime-local">

<!-- Oy -->
<input type="month">

<!-- Hafta -->
<input type="week">

<!-- Fayl -->
<input type="file" accept="image/*,.pdf">
<input type="file" multiple accept=".jpg,.png">

<!-- Yashirin -->
<input type="hidden" name="user_id" value="42">

<!-- Diapazion (slider) -->
<input type="range" min="0" max="100" value="50" step="10">

<!-- Checkbox -->
<input type="checkbox" id="kelishaman" name="kelishaman">
<label for="kelishaman">Shartlarga roziман</label>

<!-- Radio -->
<input type="radio" id="erkak" name="jins" value="erkak">
<label for="erkak">Erkak</label>
<input type="radio" id="ayol" name="jins" value="ayol">
<label for="ayol">Ayol</label>

<!-- Submit (forma yuborish) -->
<input type="submit" value="Yuborish">

<!-- Button (forma yubormaydi) -->
<input type="button" value="Tugma" onclick="alert('OK')">

<!-- Reset (formani tozalash) -->
<input type="reset" value="Tozalash">

<!-- Image (submit rasm bilan) -->
<input type="image" src="yuborish.png" alt="Yuborish">
```

---

## 📌 Input Atributlari

```html
<input
  type="text"
  name="ism"           <!-- Server uchun maydon nomi (MUHIM) -->
  id="ism-input"       <!-- label for bilan bog'lash -->
  value="Ali"          <!-- Default qiymat -->
  placeholder="Ismingiz" <!-- Qoʻllanma matn -->
  required             <!-- Majburiy to'ldirish -->
  disabled             <!-- O'chirilgan (server ga yuborilmaydi) -->
  readonly             <!-- Faqat o'qish (server ga yuboriladi) -->
  autofocus            <!-- Sahifa ochilganda fokus -->
  autocomplete="name"  <!-- Brauzer takliflar -->
  maxlength="50"       <!-- Maksimal belgi soni -->
  minlength="2"        <!-- Minimal belgi soni -->
  pattern="[A-Za-z]+"  <!-- Regex naqshi -->
  size="30"            <!-- Ko'rinadigan kenglik (belgilar soni) -->
  step="0.5"           <!-- number/range uchun qadam -->
  min="0"              <!-- Minimal qiymat -->
  max="100"            <!-- Maksimal qiymat -->
  multiple             <!-- Bir nechta qiymat (email, file) -->
  accept=".jpg,.png"   <!-- file uchun ruxsat etilgan formatlar -->
  list="takliflar"     <!-- datalist bilan bog'lash -->
>
```

---

## 📌 Textarea va Select

```html
<!-- Ko'p qatorli matn -->
<textarea
  name="xabar"
  rows="5"
  cols="40"
  placeholder="Xabaringizni yozing..."
  maxlength="500"
  resize="vertical"
></textarea>

<!-- Tanlash ro'yxati -->
<select name="shahar">
  <option value="">— Shaharni tanlang —</option>
  <optgroup label="Uzbekiston">
    <option value="tashkent">Toshkent</option>
    <option value="samarkand">Samarqand</option>
    <option value="bukhara">Buxoro</option>
  </optgroup>
  <optgroup label="Boshqa">
    <option value="moscow">Moskva</option>
  </optgroup>
</select>

<!-- Ko'p tanlash -->
<select name="tillar" multiple size="4">
  <option value="html" selected>HTML</option>
  <option value="css">CSS</option>
  <option value="js">JavaScript</option>
  <option value="react">React</option>
</select>

<!-- datalist — autocomplete ro'yxat -->
<input type="text" list="dasturlar" placeholder="Dastur nomi">
<datalist id="dasturlar">
  <option value="VS Code">
  <option value="WebStorm">
  <option value="Sublime Text">
  <option value="Atom">
</datalist>
```

---

## 📌 fieldset va legend, label

```html
<!-- Forma guruhlash -->
<form>
  <fieldset>
    <legend>Shaxsiy Ma'lumotlar</legend>
    <label for="ism">Ism:</label>
    <input type="text" id="ism" name="ism" required><br>
    <label for="email">Email:</label>
    <input type="email" id="email" name="email" required>
  </fieldset>

  <fieldset>
    <legend>Manzil</legend>
    <label for="shahar">Shahar:</label>
    <input type="text" id="shahar" name="shahar"><br>
    <label for="manzil">Manzil:</label>
    <textarea id="manzil" name="manzil" rows="3"></textarea>
  </fieldset>
</form>
```

---

## 🎯 10 ta Amaliy Vazifa — Forma Yasab Kelish

```html
<!DOCTYPE html>
<html lang="uz">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Forma Amaliyot</title>
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    body { min-height: 100vh; background: linear-gradient(135deg, #16213e, #0f3460); display: flex; align-items: center; justify-content: center; font-family: "Segoe UI", sans-serif; padding: 40px 16px; }

    .forma-quti { background: white; padding: 40px; border-radius: 20px; width: 100%; max-width: 520px; box-shadow: 0 20px 60px rgba(0,0,0,0.3); }
    .forma-sarlavha { text-align: center; margin-bottom: 32px; }
    .forma-sarlavha h1 { font-size: 26px; color: #1a1a2e; margin-bottom: 6px; }
    .forma-sarlavha p { color: #888; font-size: 14px; }

    .guruh { margin-bottom: 20px; }
    .guruh label { display: block; font-size: 14px; font-weight: 600; color: #374151; margin-bottom: 6px; }
    .guruh .majburiy { color: #e63946; }

    .kiritish, .tanlash, .matn-maydon {
      width: 100%; padding: 12px 16px; border: 2px solid #e5e7eb; border-radius: 10px;
      font-size: 15px; font-family: inherit; color: #1a1a2e; outline: none;
      transition: border-color 0.2s, box-shadow 0.2s;
    }
    .kiritish:focus, .tanlash:focus, .matn-maydon:focus {
      border-color: royalblue;
      box-shadow: 0 0 0 3px rgba(65,105,225,0.15);
    }
    .kiritish:valid:not(:placeholder-shown) { border-color: #10b981; }
    .kiritish:invalid:not(:placeholder-shown) { border-color: #e63946; }

    /* Vazifa 1: Oddiy text inputlar */
    .ism-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; }

    /* Vazifa 2: Radio tugmalar */
    .radio-guruh { display: flex; gap: 20px; flex-wrap: wrap; }
    .radio-variant { display: flex; align-items: center; gap: 8px; cursor: pointer; }
    .radio-variant input { accent-color: royalblue; width: 16px; height: 16px; }

    /* Vazifa 3: Checkbox */
    .checkbox-variant { display: flex; align-items: center; gap: 8px; cursor: pointer; margin-bottom: 8px; }
    .checkbox-variant input { accent-color: royalblue; width: 16px; height: 16px; }

    /* Vazifa 4: Select */
    .tanlash { cursor: pointer; }

    /* Vazifa 5: Range slider */
    .slider-wrapper { display: flex; align-items: center; gap: 12px; }
    .slider-wrapper input[type="range"] { flex: 1; accent-color: royalblue; }
    .slider-qiymat { background: royalblue; color: white; padding: 4px 10px; border-radius: 6px; font-size: 13px; font-weight: 700; min-width: 40px; text-align: center; }

    /* Vazifa 6: Fayl yuklash */
    .fayl-zona { border: 2px dashed #d1d5db; border-radius: 10px; padding: 24px; text-align: center; cursor: pointer; transition: border-color 0.2s; }
    .fayl-zona:hover { border-color: royalblue; }
    .fayl-zona input { display: none; }
    .fayl-zona label { cursor: pointer; display: flex; flex-direction: column; align-items: center; gap: 8px; }

    /* Vazifa 7: Parol ko'rish/yoshirish */
    .parol-quti { position: relative; }
    .parol-quti input { padding-right: 48px; }
    .parol-ko over { position: absolute; right: 14px; top: 50%; transform: translateY(-50%); background: none; border: none; cursor: pointer; font-size: 18px; color: #888; }

    /* Vazifa 8: Rang va sana */
    .rang-sana { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; }

    /* Vazifa 9-10: Submit tugma */
    .yuborish-btn {
      width: 100%; padding: 14px; background: royalblue; color: white;
      border: none; border-radius: 10px; font-size: 16px; font-weight: 700; cursor: pointer;
      transition: all 0.2s; margin-top: 8px;
    }
    .yuborish-btn:hover { background: #2c5282; transform: translateY(-2px); }
    .yuborish-btn:active { transform: translateY(0); }

    .ajratgich { border: none; border-top: 1px solid #f0f0f0; margin: 8px 0 20px; }
    .eslatma { font-size: 12px; color: #888; text-align: center; margin-top: 16px; }
    .eslatma a { color: royalblue; }
  </style>
</head>
<body>

  <div class="forma-quti">
    <div class="forma-sarlavha">
      <h1>Ro'yxatdan O'tish</h1>
      <p>Barcha maydonlarni to'ldiring</p>
    </div>

    <form id="royhxat-forma" novalidate>

      <!-- Vazifa 1: Ism-Familiya -->
      <div class="ism-grid">
        <div class="guruh">
          <label for="ism">Ism <span class="majburiy">*</span></label>
          <input class="kiritish" type="text" id="ism" name="ism" placeholder="Ali"
                 required minlength="2" maxlength="50" autocomplete="given-name">
        </div>
        <div class="guruh">
          <label for="familya">Familiya <span class="majburiy">*</span></label>
          <input class="kiritish" type="text" id="familya" name="familya" placeholder="Valiev"
                 required minlength="2" maxlength="50" autocomplete="family-name">
        </div>
      </div>

      <!-- Vazifa 1: Email -->
      <div class="guruh">
        <label for="email">Email <span class="majburiy">*</span></label>
        <input class="kiritish" type="email" id="email" name="email"
               placeholder="ali@mail.com" required autocomplete="email">
      </div>

      <!-- Vazifa 7: Parol -->
      <div class="guruh">
        <label for="parol">Parol <span class="majburiy">*</span></label>
        <div class="parol-quti">
          <input class="kiritish" type="password" id="parol" name="parol"
                 placeholder="Kamida 8 ta belgi" required minlength="8">
          <button type="button" class="parol-ko'rsat" onclick="parolToggle()">👁</button>
        </div>
      </div>

      <hr class="ajratgich">

      <!-- Vazifa 2: Radio tugmalar (Jins) -->
      <div class="guruh">
        <label>Jins <span class="majburiy">*</span></label>
        <div class="radio-guruh">
          <label class="radio-variant">
            <input type="radio" name="jins" value="erkak" required> Erkak
          </label>
          <label class="radio-variant">
            <input type="radio" name="jins" value="ayol"> Ayol
          </label>
        </div>
      </div>

      <!-- Vazifa 4: Select (Shahar) -->
      <div class="guruh">
        <label for="shahar">Shahar</label>
        <select class="tanlash" id="shahar" name="shahar">
          <option value="">— Tanlang —</option>
          <optgroup label="O'zbekiston">
            <option value="tashkent">Toshkent</option>
            <option value="samarkand">Samarqand</option>
            <option value="namangan">Namangan</option>
          </optgroup>
          <optgroup label="Qozog'iston">
            <option value="almaty">Almaty</option>
          </optgroup>
        </select>
      </div>

      <!-- Vazifa 5: Range (Yosh) -->
      <div class="guruh">
        <label>Yosh: <span id="yosh-ko'rsatma" style="color:royalblue;font-weight:700">25</span></label>
        <div class="slider-wrapper">
          <span>16</span>
          <input type="range" id="yosh-slider" name="yosh" min="16" max="60" value="25"
                 oninput="document.getElementById('yosh-ko\'rsatma').textContent=this.value">
          <span>60</span>
        </div>
      </div>

      <!-- Vazifa 8: Tug'ilgan kun -->
      <div class="rang-sana">
        <div class="guruh">
          <label for="tugish">Tug'ilgan kun</label>
          <input class="kiritish" type="date" id="tugish" name="tug_ilgan_kun"
                 min="1960-01-01" max="2008-01-01">
        </div>
        <div class="guruh">
          <label for="rang-tanlash">Sevimli Rang</label>
          <input class="kiritish" type="color" id="rang-tanlash" name="rang" value="#4361ee"
                 style="padding: 4px; height: 48px; cursor: pointer;">
        </div>
      </div>

      <!-- Vazifa 6: Fayl yuklash (Avatar) -->
      <div class="guruh">
        <label>Profil Rasmi</label>
        <div class="fayl-zona" onclick="document.getElementById('fayl-input').click()">
          <label>
            <input type="file" id="fayl-input" name="avatar" accept="image/*"
                   onchange="faylKo'rsat(this)">
            <span style="font-size:32px">📷</span>
            <span style="font-weight:600; color:#374151">Rasm tanlash</span>
            <span id="fayl-nom" style="font-size:12px; color:#888">JPG, PNG, WebP — max 5MB</span>
          </label>
        </div>
      </div>

      <!-- Vazifa 3: Checkbox -->
      <div class="guruh">
        <label>Qiziqishlar</label>
        <label class="checkbox-variant">
          <input type="checkbox" name="qiziqish" value="dasturlash"> Dasturlash
        </label>
        <label class="checkbox-variant">
          <input type="checkbox" name="qiziqish" value="dizayn" checked> UI/UX Dizayn
        </label>
        <label class="checkbox-variant">
          <input type="checkbox" name="qiziqish" value="git"> Git va DevOps
        </label>
      </div>

      <!-- Textarea -->
      <div class="guruh">
        <label for="haqida">O'zingiz Haqingizda</label>
        <textarea class="matn-maydon" id="haqida" name="haqida" rows="3"
                  placeholder="Qisqacha tanishtiruv..." maxlength="300"></textarea>
      </div>

      <!-- Vazifa 9-10: Kelishuv checkbox va Submit -->
      <label class="checkbox-variant" style="margin-bottom:16px">
        <input type="checkbox" required id="kelishuv">
        <span style="font-size:13px">
          <a href="#" style="color:royalblue">Foydalanish shartlari</a> va
          <a href="#" style="color:royalblue">Maxfiylik</a> ga roziman
        </span>
      </label>

      <button type="submit" class="yuborish-btn">🚀 Ro'yxatdan O'tish</button>

      <p class="eslatma">
        Allaqachon hisobingiz bormi? <a href="#">Kirish →</a>
      </p>
    </form>
  </div>

  <script>
    // Parol ko'rish/yashirish
    function parolToggle() {
      const parol = document.getElementById("parol");
      parol.type = parol.type === "password" ? "text" : "password";
    }

    // Fayl nomi ko'rsatish
    function faylKo'rsat(input) {
      if (input.files.length > 0) {
        document.getElementById("fayl-nom").textContent = input.files[0].name;
      }
    }

    // Forma yuborishni to'xtatish (demo)
    document.getElementById("royhxat-forma").addEventListener("submit", (e) => {
      e.preventDefault();
      alert("✅ Forma muvaffaqiyatli yuborildi!");
    });
  </script>
</body>
</html>
```
