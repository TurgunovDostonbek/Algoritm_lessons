# 10-Dars: Git va GitHub

## 📌 Git nima?

**Git** — fayllar tarixini kuzatuvchi versiya nazorat tizimi (VCS). Kod o'zgarishlarini saqlaydi, jamoa bilan ishlashni osonlashtiradi.

**GitHub** — Git repozitoriyalarini onlayn saqlash va ulashish platformasi.

---

## 📌 Git O'rnatish va Sozlash

```bash
# Git versiyasini tekshirish
git --version

# Foydalanuvchi ma'lumotlarini sozlash (bir marta)
git config --global user.name "Ismingiz"
git config --global user.email "email@example.com"

# Sozlamalarni ko'rish
git config --list

# Default branch nomini main qilish
git config --global init.defaultBranch main
```

---

## 📌 Asosiy Git Tushunchalari

```
Working Directory → Staging Area → Repository
(Ish papkasi)      (git add)      (git commit)

git add .      ← O'zgarishlarni sahnaga qo'yish
git commit     ← Sahnadan repoga saqlash
git push       ← Reponi GitHubga yuborish
git pull       ← GitHubdan yangiliklar olish
```

---

## 📌 Repository Yaratish

```bash
# Yangi repozitoriy yaratish (lokal)
mkdir loyiham
cd loyiham
git init

# Repozitoriy holatini ko'rish
git status

# .gitignore — kuzatilmaydigan fayllar
echo "node_modules/" >> .gitignore
echo ".env" >> .gitignore
echo "*.log" >> .gitignore
```

---

## 📌 Asosiy Workflow

```bash
# 1. Faylni yaratamiz/o'zgartiramiz
echo "# Mening Loyiham" > README.md

# 2. Staging area ga qo'shamiz
git add README.md        # Faqat shu fayl
git add .                # Barcha o'zgarishlar
git add -p               # Qismma-qism tanlash

# 3. Commit qilamiz (kichik, aniq xabar bilan!)
git commit -m "Dastlabki commit"
git commit -m "feat: login sahifasi qo'shildi"
git commit -m "fix: navbar mobilda buzilgan holati tuzatildi"
git commit -m "style: tugmalar rangi yangilandi"

# 4. Tarixni ko'rish
git log
git log --oneline           # Qisqa ko'rinish
git log --oneline --graph   # Branchlar bilan

# 5. O'zgarishlarni ko'rish
git diff              # Unstaged o'zgarishlar
git diff --staged     # Staged o'zgarishlar
```

---

## 📌 GitHub bilan Ishlash

```bash
# === GitHub.com da yangi repo yaratgandan keyin ===

# Mavjud lokal reponi GitHubga ulash
git remote add origin https://github.com/username/loyiha.git

# Uzokni tekshirish
git remote -v

# Birinchi push
git push -u origin main     # -u = tracking o'rnatadi

# Keyingi pushlar
git push                    # origin main avtomatik

# GitHubdan klonlash
git clone https://github.com/username/loyiha.git
git clone https://github.com/username/loyiha.git papka_nomi  # Nom bilan

# Yangiliklar olish
git pull                    # fetch + merge
git fetch                   # Faqat yuklab olish (merge qilmasdan)
```

---

## 📌 Branchlar

```bash
# Branch yaratish va o'tish
git branch yangi-xususiyat          # Yaratish
git checkout yangi-xususiyat        # O'tish
git checkout -b yangi-xususiyat     # Yaratish + O'tish

# Zamonaviy usul (Git 2.23+)
git switch yangi-xususiyat
git switch -c yangi-xususiyat       # Create + switch

# Branchlarni ko'rish
git branch                          # Lokal
git branch -a                       # Lokal + remote
git branch -r                       # Faqat remote

# Branchni birlashtirish
git checkout main
git merge yangi-xususiyat

# Branch o'chirish
git branch -d yangi-xususiyat       # Xavfsiz (merged bo'lsa)
git branch -D yangi-xususiyat       # Majburiy
git push origin --delete yangi-xususiyat  # Remotedagi
```

---

## 📌 Xatolarni Tuzatish

```bash
# Oxirgi commitni o'zgartirish (push qilmagan bo'lsangiz)
git commit --amend -m "To'g'ri xabar"

# Staged ni bekor qilish
git restore --staged fayl.txt   # Zamonaviy
git reset HEAD fayl.txt          # Eski

# O'zgarishlarni bekor qilish
git restore fayl.txt             # Ishchi papkadagi o'zgarishni

# Eski versiyaga qaytish
git revert abc123               # Yangi commit yaratib eski holatga
git reset --soft HEAD~1         # Oxirgi commitni bekor qil (fayllar qoladi)
git reset --hard HEAD~1         # Oxirgi commitni + fayllarni ham bekor qil ⚠️

# Saqlash (stash) — hali commit qilmagan ishni vaqtincha saqlash
git stash                        # Saqlash
git stash pop                    # Qaytarish
git stash list                   # Ro'yxat
git stash drop                   # O'chirish
```

---

## 📌 .gitignore

```gitignore
# node_modules — paketlar
node_modules/

# Muhit o'zgaruvchilari (maxfiy!)
.env
.env.local
.env.production

# Build fayllar
dist/
build/
.next/

# Log fayllar
*.log
npm-debug.log*

# OS tizim fayllar
.DS_Store
Thumbs.db

# Editor sozlamalari
.vscode/settings.json
.idea/

# Test coverage
coverage/
```

---

## 📌 Commit Xabarlari Yaxshi Yozish

```bash
# Conventional Commits formati (tavsiya!)
<tur>(<qamrov>): <tavsif>

# Turlar:
feat:     # Yangi xususiyat
fix:      # Xato tuzatish
docs:     # Hujjat o'zgartirish
style:    # Formatlash (mantiqqa ta'sir qilmaydi)
refactor: # Qayta yozish (xususiyat qo'shmasdan)
test:     # Testlar
chore:    # Qurish jarayoni, kutubxonalar

# Misollar:
git commit -m "feat: foydalanuvchi ro'yxatdan o'tish qo'shildi"
git commit -m "fix: login da parol xushi tuzatildi"
git commit -m "docs: README yangilandi"
git commit -m "style(navbar): bo'sh joylar to'g'irlandi"
git commit -m "refactor: autentifikatsiya module ajratildi"
```

---

## 📌 Git GUI Vositalari

```
Mashhur GUI vositalar:
├── GitHub Desktop — eng oson
├── VS Code Git — built-in
├── GitKraken — kuchli
├── SourceTree — Atlassian
└── Tower — Mac & Windows
```

---

## 🎯 10 ta Amaliy Vazifa

```bash
# === BOSQICH 1: Lokal repozitoriy ===

# Vazifa 1: Git sozlash
git config --global user.name "Ismingiz"
git config --global user.email "email@mail.com"
git config --list  # Tekshirish

# Vazifa 2: Yangi loyiha va birinchi commit
mkdir mening-saytim
cd mening-saytim
git init
echo "# Mening Saytim" > README.md
git add README.md
git commit -m "feat: dastlabki commit"

# Vazifa 3: HTML va CSS qo'shish
# index.html va style.css fayllarini yarating
git add .
git commit -m "feat: asosiy HTML va CSS qo'shildi"

# Vazifa 4: .gitignore yaratish
echo "node_modules/" > .gitignore
echo ".env" >> .gitignore
echo ".DS_Store" >> .gitignore
git add .gitignore
git commit -m "chore: .gitignore qo'shildi"

# Vazifa 5: O'zgarish va commit
# style.css ga navbar stillari qo'shing
git diff  # O'zgarishlarni ko'ring
git add style.css
git commit -m "style: navbar stillari qo'shildi"

# === BOSQICH 2: GitHub ===

# Vazifa 6: GitHub da repo yaratish
# 1. github.com ga boring
# 2. "New repository" bosing
# 3. Nom: "mening-saytim", Public, README qo'shmasdan
# 4. "Create repository"

# Vazifa 7: Lokal ni GitHub ga ulash
git remote add origin https://github.com/SIZNING_USERNAME/mening-saytim.git
git push -u origin main

# Vazifa 8: Branch bilan ishlash
git checkout -b header-komponenti
# header qismini yozing
git add .
git commit -m "feat: header komponenti yaratildi"
git push origin header-komponenti
# GitHub da Pull Request yarating

# Vazifa 9: main ga merge qilish (GitHub UI da)
git checkout main
git pull  # yangiliklar olish
git merge header-komponenti
git push origin main
git branch -d header-komponenti  # O'chirish

# Vazifa 10: Loyiha to'liq workflow
# a) Yangi feature uchun branch oching
git checkout -b footer-qo_shish
# b) Footer yarating
# c) Commit qiling
git add footer.html
git commit -m "feat: footer komponenti qo'shildi"
# d) Push qiling
git push origin footer-qo_shish
# e) GitHub da PR yarating va merge qiling
# f) main ni yangilang
git checkout main
git pull
echo "Loyiha muvaffaqiyatli GitHub da!"
```

```markdown
## GitHub Profile README (bonus)

GitHub profileingizni bezash uchun:
1. GitHub da o'z username-ingizga teng nomli repo yarating
2. README.md fayl yarating

### profile/README.md namunasi:

# Salom! Men [Ismingiz] 👋

## Men haqimda
- 🔭 Hozir: [Loyiha nomi] ustida ishlamoqdaman
- 🌱 O'rganmoqdaman: React, Node.js
- 👯 Hamkorlik: Open source loyihalarga

## Texnologiyalar
![HTML](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white)
![CSS](https://img.shields.io/badge/CSS3-1572B6?style=flat&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)

## GitHub Statistikam
![Stats](https://github-readme-stats.vercel.app/api?username=SIZNING_USERNAME&show_icons=true&theme=radical)
```
