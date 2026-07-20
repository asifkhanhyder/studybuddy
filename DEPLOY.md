# Deploy Guide (asaan steps)

Yeh app **static** hai (sirf `index.html`), isliye deploy karna bohot simple hai — koi backend/server nahi chahiye.

## 1. GitHub par public repo banao
1. GitHub par login karo → **New repository**
2. Naam do: `studybuddy` (ya jo chaho)
3. **Public** select karo (zaroori hai — private hui to 0 marks milenge)
4. `index.html`, `README.md`, `.gitignore` upload karo (drag & drop kar sakte ho GitHub ke "Add file → Upload files" se, ya git commands se)

```bash
git init
git add .
git commit -m "StudyBuddy: AI quiz app"
git branch -M main
git remote add origin https://github.com/<your-username>/studybuddy.git
git push -u origin main
```

## 2. Vercel par deploy karo
1. [vercel.com](https://vercel.com) par GitHub se login karo
2. **Add New → Project** → apna `studybuddy` repo select karo
3. Framework preset: **Other** (kyunke yeh plain HTML hai)
4. Build command: **khali chodo** (empty) — Output directory: `.`
5. **Deploy** dabao — 30 second mein live URL mil jayega (kuch is tarah: `studybuddy.vercel.app`)

(Alternative: GitHub Pages bhi chalega — repo Settings → Pages → source: main branch → 30 seconds mein live)

## 3. Apni API key kabhi commit mat karo
- App mein "⚙ API key settings" se apni Anthropic API key browser mein hi save hoti hai (localStorage) — yeh repo ka hissa nahi banti.
- Jab grader app kholega, wo apni khud ki key daal ke test kar sakta hai.
- Key [console.anthropic.com](https://console.anthropic.com) se milti hai.

## 4. Test karo (incognito mein!)
- Apna live URL incognito/private window mein kholo
- GitHub repo link bhi incognito mein kholo — login na maange to sab theek hai

## 5. Screenshots lo
- Landing page
- Quiz question (ek MCQ dikhte hue)
- Result screen with weak areas list
Yeh 3 screenshots README mein daalne hain.
