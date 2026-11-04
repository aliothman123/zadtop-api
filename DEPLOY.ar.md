# رفع زاد توب على غيت هب وصفحات غيت هب

هذا المجلد هو المستودع **العام** فقط. لا ترفع معه ملفات البوت، ولا كلمات السر، ولا مفاتيح الواجهة.

بعد النشر:

- المستودع: https://github.com/aliothman123/zadtop-api
- الصفحات: https://aliothman123.github.io/zadtop-api/

## الفرع `main`

جذر المستودع: `README.md` و`docs/`. هذا ما يراه من يفتح المستودع.

## الفرع `gh-pages`

انسخ **محتويات** المجلد `gh-pages/` إلى جذر فرع `gh-pages`، بحيث يكون `index.html` في الجذر.

من PowerShell، بعد تثبيت Git وتسجيل الدخول. انسخ صفحات الموقع إلى مجلد مؤقت **قبل** إنشاء الفرع اليتيم، حتى لا يُحذف مصدر الصفحات مع شجرة العمل:

```powershell
cd "c:\Users\Ali\Desktop\مشاريع بايثون\zadtop-api"
git init -b main
git add README.md README.*.md docs .gitignore DEPLOY.ar.md
git commit -m "Publish the Zad Top API developer hub"
gh repo create zadtop-api --public --source . --remote origin --description "Zad Top HTTP API: Free Fire, PUBG, Yalla Ludo, Jawaker, iTunes and Razer Gold" --push

$pages = Join-Path $env:TEMP "zadtop-api-pages"
if (Test-Path $pages) { Remove-Item -Recurse -Force $pages }
Copy-Item -Recurse -Force .\gh-pages $pages
git checkout --orphan gh-pages
git rm -rf .
Copy-Item -Recurse -Force (Join-Path $pages "*") .
git add .
git commit -m "Publish the Zad Top API GitHub Pages hub"
git push -u origin gh-pages
git checkout main
```

في المستودع: Settings → Pages → Branch: `gh-pages` → Folder: `/ (root)` → Save.

ثم في Google Search Console افحص:

- https://aliothman123.github.io/zadtop-api/
- https://aliothman123.github.io/zadtop-api/games.html
- https://aliothman123.github.io/zadtop-api/recipes.html
- https://aliothman123.github.io/zadtop-api/bot.html

وأرسل `sitemap.xml`.
