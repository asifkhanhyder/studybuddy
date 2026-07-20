# StudyBuddy

**AI-powered quiz generator that tracks your weak topics over time.**

## The problem

Students revise by re-reading notes, which feels productive but rarely reveals what they *actually* don't know. StudyBuddy solves this for university students (built with MUET Batch 2 students in mind, but usable by anyone): paste your notes or a topic, get an instant quiz, and let the app quietly track which sub-topics you keep getting wrong — so your next revision session targets exactly what's weak instead of re-reading everything.

## Live URL

🔗 **[PASTE YOUR VERCEL/GITHUB PAGES URL HERE]**

## GitHub repo

🔗 **[PASTE YOUR PUBLIC REPO LINK HERE]**

## Features

- Paste any notes or a topic name and generate a custom multiple-choice quiz
- Choose 5, 8, or 12 questions per quiz
- Each question is tagged with a specific sub-topic
- Instant feedback per question (correct/incorrect shown immediately)
- **Weak-area tracker**: every wrong answer is logged per sub-topic in your browser, building a ranked list of what to revise
- **"Focus on my weak areas"** button — generates a new quiz weighted toward your worst sub-topics
- All progress persists across visits (stored locally in your browser — no account/login needed)
- Fully responsive, keyboard-accessible

## The AI feature

StudyBuddy's core AI feature is the **quiz generator**: it takes the student's raw notes (or just a topic name) and turns them into a structured multiple-choice quiz, with each question labeled by the specific sub-topic it tests. That per-question topic tag is what powers the weak-area tracking — it's how the app knows *which* part of the material a wrong answer belongs to.

**Model used:** `claude-sonnet-4-6` via the Anthropic Messages API, called directly from the browser.

**System prompt (written by me):**

```
You are StudyBuddy's quiz generator. Given a student's notes or a topic name, generate exactly {N} multiple-choice questions that test real understanding of the material, not just rote recall.

Rules:
- Each question has exactly 4 options, only one correct.
- Each question gets a short "topic" tag (2-4 words) naming the specific sub-topic it tests, so a student can see which sub-topics they're weak in. Reuse the same topic tag across questions that test the same sub-topic.
- Vary difficulty: mix straightforward recall with a few application/reasoning questions.
- Base every question strictly on the provided material or topic. Do not invent facts unrelated to it.
- Return ONLY valid JSON, no markdown code fences, no commentary, in exactly this schema:
[{"question":"...", "options":["...","...","...","..."], "correctIndex":0, "topic":"..."}]
```

When a student taps **"Focus on my weak areas,"** the app appends their top 5 most-missed topics to the user message, so the same system prompt generates a new quiz specifically weighted toward those sub-topics.

## Tools, services & models used

- **Frontend:** plain HTML, CSS, and vanilla JavaScript (no framework, no build step — single file)
- **AI model:** Claude (`claude-sonnet-4-6`) via the Anthropic Messages API, called client-side
- **Storage:** browser `localStorage` for weak-topic history (no database/backend)
- **Hosting:** [Vercel / GitHub Pages — say which one you used]
- **Fonts:** Fraunces & Space Mono & Inter (Google Fonts)

## Screenshots

_(Add 3+ screenshots here — landing page, an active quiz question, and the results/weak-areas screen)_

1. ![Landing page](screenshots/landing.png)
2. ![Quiz in progress](screenshots/quiz.png)
3. ![Results & weak areas](screenshots/results.png)

## How to run

This is a static, single-file app — no build step, no server required.

**Locally:**
1. Clone the repo: `git clone [your repo URL]`
2. Open `index.html` directly in your browser (or run `python3 -m http.server` in the folder and visit `localhost:8000`)
3. Click **⚙ API key settings** and paste your own Anthropic API key (get one free at [console.anthropic.com](https://console.anthropic.com)) — it's stored only in your browser's localStorage and is never committed to this repo
4. Paste some notes, hit **Generate quiz**, and go

**Live:** just open the live URL above — same steps, no install needed.

## Notes on security

No API keys are committed anywhere in this repo. Each user (including graders) supplies their own Anthropic API key through the in-app settings panel, which is stored client-side only.
