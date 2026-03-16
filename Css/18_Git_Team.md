# 18-Dars: Git va GitHub — Jamoa bilan Ishlash

## 📌 Jamoa bilan Git Workflow

```
GitHub Flow (Eng keng tarqalgan):
main ──────────────────────────────────────► (Production)
        │                        │
        ├─► feature/login ──────►┤  Pull Request → Review → Merge
        │                        │
        ├─► feature/navbar ─────►┤  Pull Request → Review → Merge
        │                        │
        └─► fix/button-bug ─────►┤  Pull Request → Review → Merge
```

---

## 📌 Pull Request (PR) nima?

**Pull Request** — o'zgarishlaringizni asosiy branchga qo'shilishini so'rash. Jamoadoshlar o'zgarishlarni ko'rib chiqadi va tasdiq beradi.

```bash
# 1. Yangi branch oching
git checkout -b feature/landing-page

# 2. O'zgarishlar qiling va commit qiling
git add .
git commit -m "feat: landing page dizayni qo'shildi"

# 3. GitHubga yuking
git push origin feature/landing-page

# 4. GitHub da Pull Request yarating
# 5. Jamoadosh review qiladi va tasdiqlaydi
# 6. Merge qilinadi
```

---

## 📌 Merge Conflict — Ziddiyatlar

```bash
# Ziddiyat qachon yuzaga keladi?
# Ikki kishi bir xil faylning bir joyini o'zgartirsa

# Konflikt ko'rinishi (faylda):
<<<<<<< HEAD (Sizning kodni)
.btn { color: red; }
=======
.btn { color: blue; }
>>>>>>> feature/new-design (Boshqa shaxsning kodi)

# Yechimlari:
# 1. O'zingiznikini saqlang:
.btn { color: red; }

# 2. Boshqasini saqlang:
.btn { color: blue; }

# 3. Ikkalasini aralashtirib:
.btn { color: purple; }  /* Kelishilgan rang */

# Keyin:
git add .
git commit -m "fix: rang konflikti hal qilindi"
```

---

## 📌 Rebase — Commit Tarixini Tartiblashtirish

```bash
# Rebase — main branch dagi o'zgarishlarni o'z branch ingizga kiritish

# Merge usuli (tarix tarmoqlanadi):
git checkout main
git merge feature/login

# Rebase usuli (tarix tekis bo'ladi):
git checkout feature/login
git rebase main    # main commit lari o'z branch ingiz "ostiga" qo'yiladi
git checkout main
git merge feature/login  # Fast-forward merge

# Interactive rebase — commit larni birlashtirish
git rebase -i HEAD~3    # Oxirgi 3 ta commitni
# pick → squash (birlashtirish)
# pick → reword (xabarni o'zgartirish)
# pick → drop (o'chirish)
```

---

## 📌 Git Tags — Versiyalar

```bash
# Versiya belgilash (Semantic Versioning: MAJOR.MINOR.PATCH)
git tag v1.0.0                         # Lightweight tag
git tag -a v1.0.0 -m "Birinchi versiya" # Annotated tag

# Taglarni ko'rish
git tag
git tag -l "v1.*"

# Remote ga yuborish
git push origin v1.0.0
git push origin --tags  # Barcha taglar

# Release yaratish (GitHub da)
# Tags → Create release → v1.0.0 → Publish
```

---

## 📌 .gitignore Amaliy

```gitignore
# CSS loyiha uchun .gitignore

# Node modules
node_modules/
npm-debug.log*

# Build chiqishlari
dist/
build/
.cache/
.parcel-cache/

# Sass/CSS kompilyatsiya
*.css.map

# Environment
.env
.env.local

# OS
.DS_Store
Thumbs.db
desktop.ini

# Editor
.vscode/
.idea/
*.swp

# Locked fayllar (ba'zi holatlarda)
# package-lock.json
# yarn.lock
```

---

## 📌 GitHub Actions — Avtomatik Deploy

```yaml
# .github/workflows/deploy.yml
name: Deploy to GitHub Pages

on:
  push:
    branches: [ main ]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Setup Node
        uses: actions/setup-node@v3
        with:
          node-version: '18'
      
      - name: Install va Build
        run: |
          npm install
          npm run build
      
      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./dist
```

---

## 🎯 10 ta Amaliy Vazifa

```bash
# Vazifa 1: O'z reponi klonlash va branch yaratish
git clone https://github.com/SIZNING-USERNAME/portfolio.git
cd portfolio
git checkout -b feature/navbar-yangilash

# Vazifa 2: Navbar CSS ni yangilang
# navbar stillarini o'zgartiring...
git add Css/06_Flexbox.md style.css
git commit -m "style(navbar): yangi rang sxemasi qo'shildi"
git push origin feature/navbar-yangilash
# GitHub da PR yarating

# Vazifa 3: Conflict simulyatsiyasi
git checkout main
git checkout -b hotfix/rang-tuzatish
# style.css da bir narsa o'zgartiring
git add . && git commit -m "fix: asosiy rang tuzatildi"
git push origin hotfix/rang-tuzatish
# Agar conflict bo'lsa hal qiling

# Vazifa 4: Interactive rebase
git log --oneline -5    # Oxirgi 5 commitni ko'ring
git rebase -i HEAD~3    # Oxirgi 3ni birlashtiring
# squash yoki fixup tanlang

# Vazifa 5: Versiya belgilash
git tag -a v0.1.0 -m "Beta versiya — Navbar va Footer tayyor"
git push origin v0.1.0

# Vazifa 6: GitHub da muhofazalar
# Settings → Branches → Add rule:
# - Require pull request reviews before merging
# - Require status checks to pass
# - Include administrators

# Vazifa 7: Commit xabarlari to'g'ri yozish
# x Yomon:
git commit -m "o'zgartirdim"
git commit -m "fix"
# ✓ Yaxshi (Conventional Commits):
git commit -m "feat(navbar): responsive hamburger menu qo'shildi"
git commit -m "fix(button): hover holati mobilda ishlamas edi"
git commit -m "style(typography): font o'lchami 16px dan 15px ga tushirildi"

# Vazifa 8: git stash bilan vaqtinchalik saqlash
git stash                          # Hozirgi ishni saqlash
git checkout main                  # Boshqa branchga o'tish
git pull                           # Yangiliklar olish
git checkout feature/navbar        # Qaytish
git stash pop                      # Saqlanganlarni qaytarish

# Vazifa 9: git log bilan tarixni o'rganish
git log --oneline --graph --all    # Barcha branchlar grafigi
git log --author="Sizning Ismingiz"  # Sizning commitlaringiz
git log --since="1 week ago"       # Oxirgi haftaniklar

# Vazifa 10: GitHub Pages orqali deploy
# 1. Repository → Settings → Pages
# 2. Source: Deploy from a branch → main → /root
# 3. Save → Bir necha daqiqa kuting
# 4. https://username.github.io/repo-name/ da ko'ring
echo "Sayt: https://SIZNING_USERNAME.github.io/portfolio/"
```

```markdown
## GitHub da Jamoa Qoidalari (CONTRIBUTING.md)

### Branch nomlash:
- feature/[ism]  — yangi xususiyat
- fix/[ism]      — xato tuzatish  
- style/[ism]    — CSS o'zgarish
- docs/[ism]     — hujjat

### Commit xabarlari:
- feat: yangi xususiyat
- fix: xato tuzatish
- style: formatlash
- refactor: qayta yozish

### PR qoidalari:
- Har bir PR 1 ta maqsadga ega bo'lsin
- Screenshot ilova qiling (UI o'zgarsa)
- Reviewerga tayinlang
```
