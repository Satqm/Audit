# MCQ Helper — CA Final Pro Simulator

A modern, offline-first study companion for CA Final students, built as a single-file Progressive Web App. Practice MCQs, case studies, and ICAI-sourced scenarios across Audit, Financial Reporting, AFM, Direct Tax, and GST — with a distraction-free reading mode, syllabus tracker, key takeaways, and analytics.

---

## ✨ Features

### 📚 Multi-Subject MCQ Engine
- **Audit** — Easy / Medium / Case Studies
- **Financial Reporting** — Standard FR MCQs + ICAI additional case studies
- **Advanced Financial Management** — ICAI case scenarios
- **Direct Tax Laws** — ICAI case scenarios
- **GST** — Practical case scenarios
- Supports both **single-question MCQs** and **case-study bundles** (passage + multiple sub-questions)
- Auto-normalizes many JSON shapes (`options` as array or object, `answer`/`correctOption`/`correct`, etc.)
- Renders **tables** inside questions/explanations cleanly with horizontal scroll

### 📖 Study Mode (Always-Visible Explanations)
- Toggle the 🎓 icon to reveal the **correct answer + full explanation inline** below the options
- Works in both **normal quiz view** and **fullscreen Reading Mode**
- Auto-scrolls to the explanation panel so you never miss it
- Expert advice accessible via the lifeline dropdown

### 🔍 Fullscreen Reading Mode
- Double-tap any question (or press `8`) for a distraction-free reading experience
- Swipe left/right to navigate between questions
- **Lockable swipe navigation** to prevent accidental changes
- **5 highlighter colors** + eraser (yellow, green, blue, pink)
- **Per-question notes** attached to each MCQ
- Highlights and notes persist across sessions

### 📈 Syllabus Tracker
- Module → Chapter → Topic → Subtopic hierarchy for CA Final Paper 3 (Audit)
- Per-chapter progress bars with completion counts
- **Flashcard swipe mode** for topics — swipe right (completed) / left (not yet)
- Deck summary screen with completion percentage
- Persistent progress saved in `localStorage`

### 💡 Key Takeaways (KT) Deck
- Chapter-wise key takeaways (loaded from `kt.json`)
- Swipeable card deck with keyboard navigation
- **Add your own custom takeaways** (saved per chapter)
- **Favorite/bookmark** takeaways with star toggle
- **Jump-to palette** — grid-style navigation for quick access
- **Session memory** — reopens where you last left off
- Auto-highlighting of standards (`SA 700`, `Section 44AB`, `CARO 2020`, `ESG`, etc.)

### ❌ Wrong Question Bank
- Every wrong answer is automatically saved to IndexedDB
- **Filter by subject** (Audit / FR / AFM / DT / GST)
- Shows your answer vs. the correct answer, with explanation
- Wrong-count badge for repeated mistakes
- Remove individual entries or clear all
- Auto-removed from the bank when you get it right on a retry

### 📊 Analytics Dashboard
- Total attempted / correct / wrong across all subjects
- Per-set accuracy breakdown with color-coded cards

### 🎯 Quiz Experience
- **Lifelines**: 50:50 Eliminator + Direct Explanation
- **Bookmark** questions for later review
- **Question palette** (grid view) for jumping to any question
- **Review all / Review incorrect** sheets
- **Retake set** with confirmation
- **Study mode** — disables answering, previews the correct option
- **Keyboard shortcuts** for power users
- Sound feedback via Web Audio (no audio files needed)
- Auto-saves progress after every answer

### 🎨 Responsive Design
- **Mobile-first** layout (max-width 500px container)
- **Desktop view** auto-enabled above 900px — sidebar palette + side-by-side case study layout
- **TV view** auto-enabled above 1400px — larger typography, roomier spacing
- Light pastel UI with rounded cards and soft diffused shadows

### 💾 Data Management
- **IndexedDB** for question progress + wrong-question bank
- **localStorage** for syllabus progress, custom KTs, favorites, and stats
- **Export backup** → one JSON file with all progress + wrong questions
- **Restore from backup** → drop the JSON file back in

### 🎁 First-Time Onboarding
- Skippable guide overlay on first launch
- Explains subjects, study mode, tracking, and reading mode

### ❤️ Branding
- Premium floating-island footer with modern social icons (LinkedIn, YouTube, Instagram, Portfolio)
- Subtle support toast appears after 50 questions
- Link to the ICAI BoS CSB Final May 2026 source

---

## 🚀 Getting Started

### Option 1: Direct Open
1. Download the `index.html` file (the full source provided).
2. Place it in a folder along with your JSON data files (see below).
3. Open `index.html` in any modern browser.

> **Note:** Opening via `file://` will block `fetch()` in some browsers. Use a local server (see below) for full functionality.

### Option 2: Local Server (recommended)
```bash
# Python 3
python -m http.server 8000

# or Node.js
npx serve .
```
Then visit `http://localhost:8000`.

### Option 3: Static Hosting
Upload the folder to **GitHub Pages**, **Netlify**, **Vercel**, or **Cloudflare Pages** — no build step required.

---

## 📂 Required Data Files

Place these JSON files in the **same directory** as `index.html`:

| File | Purpose |
|------|---------|
| `study.json` | Audit – Basic Concepts |
| `mcqs.json` | Audit – Standard Questions |
| `audit_case_scenarios.json` | Audit – Case Studies |
| `gstcase_scenarios.json` | GST Case Scenarios |
| `fr.json` | Financial Reporting MCQs |
| `fricaics.json` | FR ICAI Case Studies |
| `afm_icaics.json` | AFM ICAI Case Scenarios |
| `dticaics.json` | DT ICAI Case Scenarios |
| `kt.json` | Key Takeaways per chapter |
| `syllabus.json` | (Optional) Custom syllabus structure |

If a file is missing, the app shows a friendly error. `kt.json` and `syllabus.json` fall back to sensible defaults.

### Supported JSON Shapes

**Flat MCQ array:**
```json
[
  {
    "question": "Which SA deals with audit documentation?",
    "options": ["SA 200", "SA 230", "SA 500", "SA 700"],
    "answer": 1,
    "explanation": "SA 230 deals with audit documentation."
  }
]
```

**Case study bundle:**
```json
[
  {
    "title": "ABC Ltd. — Audit Scenario",
    "passage_html": "<p>ABC Ltd. is a listed company...</p>",
    "questions": [
      {
        "question_text": "What is the auditor's primary responsibility?",
        "options": {"a": "...", "b": "...", "c": "...", "d": "..."},
        "correctOption": "b",
        "explanation_html": "<p>The auditor is responsible for...</p>"
      }
    ]
  }
]
```

**`kt.json` shape:**
```json
{
  "chapters": [
    {
      "chapter_number": 1,
      "chapter_title": "Quality Control",
      "key_takeaways": [
        "SQC 1 requires...",
        "Engagement files should be completed within 60 days..."
      ]
    }
  ]
}
```

---

## ⌨️ Keyboard Shortcuts

Available on desktop / TV view:

| Key | Action |
|-----|--------|
| `1` `2` `3` `4` | Select option A / B / C / D |
| `5` | Scroll down |
| `6` | Scroll up |
| `7` | Back / Close |
| `8` | Toggle fullscreen Reading Mode |
| `9` | Next question |
| `0` | Previous question |
| `←` `→` | Prev / Next (also swipes in Reading Mode) |
| `Space` / `Enter` | Flip flashcard |
| `Esc` | Close current overlay |

---

## 🛠️ Tech Stack

- **Vanilla JavaScript** (no framework, no build step)
- **Tailwind CSS** (CDN, used sparingly — mostly custom CSS)
- **Font Awesome 6** (CDN)
- **Inter + Poppins** fonts (Google Fonts)
- **IndexedDB** for structured storage
- **localStorage** for lightweight progress
- **Web Audio API** for UI sounds (no audio assets)
- **Pointer Events** for swipe gestures

---

## 📱 Supported Browsers

- ✅ Chrome / Edge 90+
- ✅ Safari 14+ (iOS + macOS)
- ✅ Firefox 88+
- ✅ Samsung Internet
- ⚠️ Older browsers may not support `pointer-events`, `backdrop-filter`, or `IndexedDB v2`

---

## 💾 Data Backup

### Export
1. From the welcome screen, tap **Backup DB**.
2. A JSON file downloads with all your progress and wrong questions.

### Restore
1. Tap **Restore** from the welcome screen.
2. Select the backup `.json` file.
3. Progress and wrong questions are restored in-place.

> Backups are **not** encrypted. Do not share them publicly.

---

## 🎨 Customization

### Change Branding
Search for `MCQ Helper` and `Observe with Satyam` in the HTML and replace with your own name.

### Update Social Links
In the `.social-footer` section:
```html
<a href="YOUR_LINKEDIN_URL" target="_blank" title="LinkedIn">...</a>
```

### Change Theme Colors
Edit the CSS variables at the top of `<style>`:
```css
:root {
  --primary: #2563eb;
  --correct: #059669;
  --wrong: #dc2626;
  --marked: #d97706;
  /* ... */
}
```

### Adjust View Breakpoints
- **Desktop view:** auto-enabled above `900px` (see `detectViewMode()`)
- **TV view:** auto-enabled above `1400px`

---

## 🐛 Troubleshooting

| Issue | Fix |
|-------|-----|
| "Could not load study.json" | Ensure the file is in the same folder as `index.html`, and you're serving via HTTP (not `file://`) |
| Questions render as HTML | Use `question_text` / `explanation_html` for HTML content, or escape `<` `>` in plain strings |
| Progress not saving | Check that IndexedDB is not blocked (private browsing on some browsers) |
| Highlights don't persist | Ensure `localStorage` is enabled for the origin |
| Stale cached data | Hard-refresh (`Ctrl+Shift+R` / `Cmd+Shift+R`) |

---

## 📖 User Guide (Quick Tour)

1. **First launch** → skippable guide walks you through the app.
2. **Pick a subject** from the welcome screen.
3. **Answer questions** — every response is auto-saved.
4. **Toggle Study Mode** (🎓) to see explanations inline for every MCQ.
5. **Double-tap** any question for distraction-free Reading Mode with highlighter.
6. **Use lifelines** (✨) for 50:50 or direct explanations.
7. **Track progress** via Syllabus Tracker, Key Takeaways, and Analytics.
8. **Review mistakes** anytime from the Wrong Question bank.
9. **Backup regularly** — your data lives only on this device.

---

## 📜 Source & Attribution

Question and case-study material for the ICAI **Final (New Scheme) May 2026** onward has been compiled with reference to the official ICAI BoS page:

🔗 [https://www.icai.org/post/bos-csb-final-may2026](https://www.icai.org/post/bos-csb-final-may2026)

All standards, sections, and case passages remain the intellectual property of their respective owners (ICAI, MCA, RBI, and others). This tool is an **unofficial study aid** and is not affiliated with or endorsed by ICAI.

---

## 👨‍💻 Author

**Satyam Kumar** — *Observe with Satyam*

- 🎥 YouTube: [@observe_with_satyam](https://youtube.com/@observe_with_satyam)
- 💼 LinkedIn: [satyam-kumar5286o](https://linkedin.com/in/satyam-kumar5286o)
- 📸 Instagram: [@observe_with_satyam](https://instagram.com/observe_with_satyam)
- 🌐 Portfolio: [satqm.github.io/Portfolio-](https://satqm.github.io/Portfolio-)

If this tool helped you, consider subscribing to the YouTube channel — it's the best way to support continued development. ❤️

---

## 📄 License

This project is provided for **personal, non-commercial educational use**. 

- The **application code** (HTML/CSS/JS) may be freely modified for personal use.
- **Question content** derived from ICAI sources remains the property of ICAI and must not be redistributed commercially.
- **Redistribution** of the compiled app for commercial purposes requires explicit permission.

---

## 🙏 Acknowledgements

- **ICAI Board of Studies** — for publicly available study material
- **Tailwind CSS** and **Font Awesome** — for utility styling and icons
- Every CA Final student who tests and gives feedback — thank you!

---

**Made with ❤️ for CA Final aspirants. Happy studying!**
