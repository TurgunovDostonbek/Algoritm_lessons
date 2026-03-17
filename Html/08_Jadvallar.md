# 08-Dars: Jadvallar (Tables)

## 📌 Jadval Tuzilmasi

```html
<table>
  <thead>                          <!-- Jadval sarlavha qismi -->
    <tr>                           <!-- Table Row (qator) -->
      <th>ID</th>                  <!-- Table Header (sarlavha hujayrasi) -->
      <th>Ism</th>
      <th>Yosh</th>
    </tr>
  </thead>

  <tbody>                          <!-- Jadval asosiy qismi -->
    <tr>
      <td>1</td>                   <!-- Table Data (ma'lumot hujayrasi) -->
      <td>Ali</td>
      <td>22</td>
    </tr>
    <tr>
      <td>2</td>
      <td>Vali</td>
      <td>25</td>
    </tr>
  </tbody>

  <tfoot>                          <!-- Jadval pastki qismi -->
    <tr>
      <td colspan="2">Jami:</td>   <!-- colspan = bir nechta ustun birlashtirish -->
      <td>2 ta</td>
    </tr>
  </tfoot>

</table>
```

---

## 📌 Jadval Atributlari

```html
<!-- colspan — gorizontal birlashtirish -->
<td colspan="3">Bu 3 ta ustunni egallaydi</td>

<!-- rowspan — vertikal birlashtirish -->
<td rowspan="2">Bu 2 ta qatorni egallaydi</td>

<!-- scope — accessibility uchun -->
<th scope="col">Ustun sarlavhasi</th>
<th scope="row">Qator sarlavhasi</th>

<!-- headers — hujayrani sarlavhaga bog'lash -->
<th id="ism">Ism</th>
<td headers="ism">Ali</td>

<!-- caption — jadval sarlavhasi -->
<table>
  <caption>O'quvchilar reytingi 2024</caption>
  ...
</table>
```

---

## 📌 CSS Bilan Jadval Stillar

```css
/* Asosiy reset */
table {
  width: 100%;
  border-collapse: collapse;   /* Ikki chegara birga */
  border-spacing: 0;           /* Hujayralar orasidagi bo'shliq */
}

/* Sarlavha */
th {
  background: #16213e;
  color: white;
  padding: 14px 16px;
  text-align: left;
  font-weight: 600;
}

/* Hujayralar */
td {
  padding: 12px 16px;
  border-bottom: 1px solid #f0f0f0;
  color: #555;
}

/* Alternatsiv qator rangi */
tr:nth-child(even) { background: #f9fafb; }
tr:hover { background: #f0f4ff; }

/* Birinchi va oxirgi qatorlar */
tr:first-child td { padding-top: 16px; }
tr:last-child td  { border-bottom: none; }

/* Sticky sarlavha */
thead th {
  position: sticky;
  top: 0;
  z-index: 1;
}
```

---

## 🎯 10 ta Amaliy Vazifa

```html
<!DOCTYPE html>
<html lang="uz">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Jadvallar Amaliyot</title>
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    body { font-family: "Segoe UI", sans-serif; background: #f0f2f5; color: #1a1a2e; }
    .sahifa { max-width: 1000px; margin: 0 auto; padding: 40px 20px; }
    h2 { font-size: 22px; margin-bottom: 16px; }
    section { margin-bottom: 48px; }
    .jadval-wrapper { background: white; border-radius: 16px; overflow: hidden; box-shadow: 0 4px 20px rgba(0,0,0,0.06); }
    .jadval-sarlavha { padding: 20px 24px; border-bottom: 1px solid #f0f0f0; }
    .jadval-sarlavha h3 { font-size: 18px; }

    /* === Umumiy jadval stillari === */
    table { width: 100%; border-collapse: collapse; }
    th {
      background: #16213e; color: white;
      padding: 14px 16px; text-align: left; font-weight: 600; font-size: 13px;
    }
    td { padding: 13px 16px; border-bottom: 1px solid #f5f5f5; font-size: 14px; color: #444; }
    tr:hover td { background: #f8f9ff; }
    tr:last-child td { border-bottom: none; }

    /* Holat badgelari */
    .belgi { padding: 4px 10px; border-radius: 20px; font-size: 12px; font-weight: 600; }
    .belgi--yashil  { background: #d1fae5; color: #065f46; }
    .belgi--sariq   { background: #fef3c7; color: #92400e; }
    .belgi--qizil   { background: #fee2e2; color: #991b1b; }
    .belgi--kul     { background: #f3f4f6; color: #374151; }

    /* O'chirish/Tahrirlash tugmalar */
    .amal-tugmalar { display: flex; gap: 6px; }
    .amal-tugma { padding: 5px 12px; border: none; border-radius: 6px; font-size: 12px; cursor: pointer; font-weight: 600; }
    .amal-tugma--tahrir { background: #dbeafe; color: #1d4ed8; }
    .amal-tugma--ochir  { background: #fee2e2; color: #dc2626; }

    /* Reyting yulduzlari */
    .yulduzlar { color: #f59e0b; letter-spacing: -2px; }

    /* O'tish effekti */
    tr { transition: background 0.15s; }

    /* Qator ranglari */
    .qator-1 { --rang: royalblue; }
    .qator-2 { --rang: #7c3aed; }
    .qator-3 { --rang: #059669; }
    .rang-qo'lda { width: 8px; height: 8px; border-radius: 50%; background: var(--rang); display: inline-block; }

    /* Responsive jadval */
    .jadval-scroll { overflow-x: auto; }
  </style>
</head>
<body>
<div class="sahifa">

  <!-- Vazifa 1: Oddiy talabalar jadvali -->
  <section>
    <h2>📋 Vazifa 1-2: Talabalar Jadvali</h2>
    <div class="jadval-wrapper">
      <div class="jadval-sarlavha">
        <h3>Talabalar Ro'yxati (2024)</h3>
      </div>
      <table>
        <caption style="text-align:left;padding:12px 16px;color:#888;font-size:13px">
          Jami: 6 ta talaba
        </caption>
        <thead>
          <tr>
            <th>#</th>
            <th>Ism va Familiya</th>
            <th>Guruh</th>
            <th>Kurs</th>
            <th>O'rtacha Ball</th>
            <th>Holati</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>1</td>
            <td><strong>Ali Valiev</strong></td>
            <td>FE-101</td>
            <td>1-kurs</td>
            <td>
              <span class="yulduzlar">★★★★★</span> 98
            </td>
            <td><span class="belgi belgi--yashil">A'lo</span></td>
          </tr>
          <tr>
            <td>2</td>
            <td><strong>Malika Saidova</strong></td>
            <td>FE-101</td>
            <td>1-kurs</td>
            <td><span class="yulduzlar">★★★★☆</span> 85</td>
            <td><span class="belgi belgi--yashil">Yaxshi</span></td>
          </tr>
          <tr>
            <td>3</td>
            <td><strong>Jasur Toshmatov</strong></td>
            <td>FE-102</td>
            <td>2-kurs</td>
            <td><span class="yulduzlar">★★★☆☆</span> 71</td>
            <td><span class="belgi belgi--sariq">Qoniqarli</span></td>
          </tr>
          <tr>
            <td>4</td>
            <td><strong>Nilufar Karimova</strong></td>
            <td>FE-102</td>
            <td>2-kurs</td>
            <td><span class="yulduzlar">★★★★☆</span> 88</td>
            <td><span class="belgi belgi--yashil">Yaxshi</span></td>
          </tr>
          <tr>
            <td>5</td>
            <td><strong>Bobur Rahimov</strong></td>
            <td>FE-103</td>
            <td>3-kurs</td>
            <td><span class="yulduzlar">★★☆☆☆</span> 54</td>
            <td><span class="belgi belgi--qizil">Kam</span></td>
          </tr>
          <tr>
            <td>6</td>
            <td><strong>Zulfiya Hasanova</strong></td>
            <td>FE-103</td>
            <td>3-kurs</td>
            <td><span class="yulduzlar">★★★★★</span> 96</td>
            <td><span class="belgi belgi--yashil">A'lo</span></td>
          </tr>
        </tbody>
        <tfoot>
          <tr>
            <td colspan="4" style="font-weight:700; color:#1a1a2e">O'rtacha Ball:</td>
            <td style="font-weight:700; color: royalblue">82</td>
            <td></td>
          </tr>
        </tfoot>
      </table>
    </div>
  </section>

  <!-- Vazifa 3-5: colspan va rowspan -->
  <section>
    <h2>📊 Vazifa 3-5: Dars Jadvali (colspan va rowspan)</h2>
    <div class="jadval-wrapper">
      <table>
        <thead>
          <tr>
            <th>Vaqt</th>
            <th>Dushanba</th>
            <th>Seshanba</th>
            <th>Chorshanba</th>
            <th>Payshanba</th>
            <th>Juma</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td style="font-weight:600; background:#f8f9ff">09:00–10:30</td>
            <td style="background:#dbeafe; text-align:center">HTML</td>
            <td style="background:#d1fae5; text-align:center">CSS</td>
            <td style="background:#dbeafe; text-align:center">HTML</td>
            <td style="background:#fef3c7; text-align:center">JavaScript</td>
            <td style="background:#f3e8ff; text-align:center">Amaliyot</td>
          </tr>
          <tr>
            <td style="font-weight:600; background:#f8f9ff">10:45–12:15</td>
            <td style="background:#d1fae5; text-align:center">CSS</td>
            <td style="background:#fef3c7; text-align:center" colspan="2">JavaScript (2 soat)</td>
            <td style="background:#d1fae5; text-align:center">CSS</td>
            <td style="background:#fee2e2; text-align:center" rowspan="2">Imtihon</td>
          </tr>
          <tr>
            <td style="font-weight:600; background:#f8f9ff">13:00–14:30</td>
            <td style="background:#f3e8ff; text-align:center">Amaliyot</td>
            <td style="background:#dbeafe; text-align:center">HTML</td>
            <td style="background:#f3e8ff; text-align:center">Amaliyot</td>
            <td style="background:#fef3c7; text-align:center">JavaScript</td>
          </tr>
        </tbody>
      </table>
    </div>
  </section>

  <!-- Vazifa 6-8: Admin jadval (CRUD amallar bilan) -->
  <section>
    <h2>⚙️ Vazifa 6-8: Mahsulotlar Admin Jadvali</h2>
    <div class="jadval-wrapper">
      <div class="jadval-sarlavha" style="display:flex; justify-content:space-between; align-items:center;">
        <h3>Mahsulotlar (124 ta)</h3>
        <button style="background:royalblue;color:white;border:none;padding:8px 16px;border-radius:8px;cursor:pointer;font-weight:600;">+ Qo'shish</button>
      </div>
      <div class="jadval-scroll">
        <table>
          <thead>
            <tr>
              <th><input type="checkbox"></th>
              <th>Mahsulot</th>
              <th>Kategoriya</th>
              <th>Narxi</th>
              <th>Miqdori</th>
              <th>Holati</th>
              <th>Amallar</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td><input type="checkbox"></td>
              <td>
                <div style="display:flex;align-items:center;gap:10px">
                  <img src="https://picsum.photos/40/40?random=1" style="width:36px;height:36px;border-radius:6px;object-fit:cover" alt="Mahsulot">
                  <div><div style="font-weight:600">Laptop Dell XPS</div><div style="font-size:11px;color:#888">SKU: LPT-001</div></div>
                </div>
              </td>
              <td>Elektronika</td>
              <td style="font-weight:700;color:royalblue">12,500,000</td>
              <td>24 ta</td>
              <td><span class="belgi belgi--yashil">Mavjud</span></td>
              <td>
                <div class="amal-tugmalar">
                  <button class="amal-tugma amal-tugma--tahrir">✏️ Tahrir</button>
                  <button class="amal-tugma amal-tugma--ochir">🗑 O'chir</button>
                </div>
              </td>
            </tr>
            <tr>
              <td><input type="checkbox"></td>
              <td>
                <div style="display:flex;align-items:center;gap:10px">
                  <img src="https://picsum.photos/40/40?random=2" style="width:36px;height:36px;border-radius:6px;object-fit:cover" alt="Mahsulot">
                  <div><div style="font-weight:600">iPhone 15 Pro</div><div style="font-size:11px;color:#888">SKU: IPH-015</div></div>
                </div>
              </td>
              <td>Telefon</td>
              <td style="font-weight:700;color:royalblue">18,900,000</td>
              <td>0 ta</td>
              <td><span class="belgi belgi--qizil">Tugagan</span></td>
              <td>
                <div class="amal-tugmalar">
                  <button class="amal-tugma amal-tugma--tahrir">✏️ Tahrir</button>
                  <button class="amal-tugma amal-tugma--ochir">🗑 O'chir</button>
                </div>
              </td>
            </tr>
            <tr>
              <td><input type="checkbox"></td>
              <td>
                <div style="display:flex;align-items:center;gap:10px">
                  <img src="https://picsum.photos/40/40?random=3" style="width:36px;height:36px;border-radius:6px;object-fit:cover" alt="Mahsulot">
                  <div><div style="font-weight:600">Samsung 4K TV</div><div style="font-size:11px;color:#888">SKU: TV-4K1</div></div>
                </div>
              </td>
              <td>Televizor</td>
              <td style="font-weight:700;color:royalblue">9,800,000</td>
              <td>5 ta</td>
              <td><span class="belgi belgi--sariq">Kam qoldi</span></td>
              <td>
                <div class="amal-tugmalar">
                  <button class="amal-tugma amal-tugma--tahrir">✏️ Tahrir</button>
                  <button class="amal-tugma amal-tugma--ochir">🗑 O'chir</button>
                </div>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </section>

  <!-- Vazifa 9-10: Solishtirish jadvali -->
  <section>
    <h2>📈 Vazifa 9-10: Texnologiyalar Solishtirish</h2>
    <div class="jadval-wrapper">
      <table>
        <thead>
          <tr>
            <th>Xususiyat</th>
            <th style="background:#0f3460">Tailwind</th>
            <th style="background:#7c2d8e">Bootstrap</th>
            <th style="background:#2d6a6a">Vanilla CSS</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td><strong>O'rganish qulayligi</strong></td>
            <td style="text-align:center">⭐⭐⭐</td>
            <td style="text-align:center">⭐⭐⭐⭐⭐</td>
            <td style="text-align:center">⭐⭐⭐⭐</td>
          </tr>
          <tr>
            <td><strong>Moslashuvchanlik</strong></td>
            <td style="text-align:center">⭐⭐⭐⭐⭐</td>
            <td style="text-align:center">⭐⭐⭐</td>
            <td style="text-align:center">⭐⭐⭐⭐⭐</td>
          </tr>
          <tr>
            <td><strong>Fayl hajmi</strong></td>
            <td style="text-align:center">Kichik</td>
            <td style="text-align:center">O'rtacha</td>
            <td style="text-align:center">Bog'liq</td>
          </tr>
          <tr>
            <td><strong>Tayyor komponent</strong></td>
            <td style="text-align:center">❌ Yo'q</td>
            <td style="text-align:center">✅ Ko'p</td>
            <td style="text-align:center">❌ Yo'q</td>
          </tr>
          <tr>
            <td><strong>Production</strong></td>
            <td style="text-align:center">✅</td>
            <td style="text-align:center">✅</td>
            <td style="text-align:center">✅</td>
          </tr>
        </tbody>
      </table>
    </div>
  </section>

</div>
</body>
</html>
```
