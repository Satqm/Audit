
# 🎓 CA Final Audit — Pro Simulator

A single-file, offline-first quiz & revision web app for **CA Final Audit**, now extended with **GST Case Scenarios** and **Financial Reporting** sets. Built with vanilla JavaScript + Tailwind (CDN) — no build step, no backend, no dependencies to install.

Works beautifully on **mobile**, **desktop**, and **TV** (remote-friendly keyboard shortcuts).

---

## ✨ Features

| Category | What you get |
|---|---|
| **Quiz Sets** | Easy (Basic Concepts), Medium (Standard Questions), Case Studies, **GST Case Scenarios**, **Financial Reporting** |
| **Study Mode** | Reveals the correct answer instantly — no attempt needed |
| **Reading Mode** | Fullscreen distraction-free reading with swipe navigation, text highlighting, and notes |
| **Lifelines** | 🎯 50:50 Eliminator · 👔 Direct Explanation |
| **Bookmarks** | Mark any question for later review |
| **Question Palette** | Jump to any question, colour-coded by status |
| **Review Incorrect** | One-tap list of every wrong answer with the correct option |
| **Syllabus Tracker** | 3 modules · 19 chapters · topic-level progress with flashcards |
| **Key Takeaways** | Swipe deck of chapter-wise takeaways (add your own + bookmark favourites) |
| **Analytics** | Accuracy, attempted count, and per-set breakdown |
| **Backup / Restore** | Export & import your entire progress as JSON |
| **Desktop View** | Toggle a wide, two-column layout with a sticky sidebar |

---

## 🚀 Getting Started

### 1. Files you need

Place all of these in the **same folder** as `index.html`:

```

index.html                  ← the app (this file)
study.json                  ← Easy Set
mcqs.json                   ← Medium Set
audit_case_scenarios.json   ← Case Studies
gstcase_scenarios.json      ← GST Case Scenarios
fr.json                     ← Financial Reporting
syllabus.json               ← optional (falls back to built-in syllabus)
kt.json                     ← optional (Key Takeaways)

```

> The app still works if `syllabus.json` / `kt.json` are missing — built-in defaults are used.

### 2. Run it

**Option A — Local server (recommended)**

Browsers block `fetch()` on `file://`, so use any tiny static server:

```bash
# Python 3
python -m http.server 8000

# Node
npx serve .
```

Then open http://localhost:8000.

Option B — Just open index.html

Works in some browsers (Firefox usually allows it), but Chrome/Edge will refuse to load the JSON files. Use Option A if you hit loading errors.

---

📂 Data File Formats

The loader is intentionally tolerant — it accepts several JSON shapes.

Format A — Flat array of questions

```json
[
  {
    "question_text": "Which SA deals with audit documentation?",
    "options": ["SA 200", "SA 230", "SA 300", "SA 500"],
    "correct_option": "b",
    "explanation_html": "<b>SA 230</b> deals with audit documentation."
  }
]
```

Format B — Case scenario with sub-questions

```json
[
  {
    "scenario_number": 1,
    "title": "ABC Ltd — Going Concern",
    "passage_html": "<p>ABC Ltd has suffered losses...</p>",
    "questions": [
      {
        "question_text": "What should the auditor do?",
        "options": { "a": "Ignore", "b": "Issue disclaimer", "c": "Evaluate management's plan", "d": "Resign" },
        "correct_option": "c",
        "explanation": "SA 570 requires evaluating management's assessment."
      }
    ]
  }
]
```

Accepted key aliases

Field Accepted keys
Question text question_text, questionText, question, text
Options options as array ["A","B","C","D"] or object {"a":..., "b":...}
Correct answer correctOption, correct_option, answer, correct — letter ("b") or index (1)
Explanation explanation_html, explanationHtml, explanation, explain
Case passage passage_html, caseStudy, case_study, scenario, passage
Case title title, case_title, caseTitle

Root object keys also tolerated: caseScenarios, questions, scenarios, data, items — or any first array found in the root object.

---

⌨️ Keyboard Shortcuts (TV Remote Friendly)

These work on the Quiz screen and inside Reading Mode. Perfect for a TV remote with number keys.

Key Action
1 Select option A
2 Select option B
3 Select option C
4 Select option D
9 Next question
0 Previous question
7 Back / Home (also closes overlays)
← / → Previous / Next question
Esc Close current overlay

Overlay-specific keys

Overlay Keys
Flashcards ← Not Yet · → Completed · Space/Enter Flip · Esc/7 Close
Key Takeaways deck ← / 0 Previous · → / 9 Next · Esc / 7 Close
Reading Mode 1–4 answer · 9 next · 0 previous · 7 back

Shortcuts are automatically disabled while typing in a textarea (notes / prompts).

---

👆 Touch Gestures

Where Gesture Result
Reading Mode Swipe left / right Next / previous question
Reading Mode (highlighter armed) Swipe across text Highlight selected range
Quiz screen Swipe left / right Next / previous question
Flashcard deck Swipe right Mark as completed
Flashcard deck Swipe left Mark as "not yet"
Flashcard Tap card Flip to context side
Key Takeaways deck Swipe left / right Next / previous takeaway

---

📖 Reading Mode

Double-tap any question card (or case study box) to open Reading Mode.

· Swipe left / right to change question — no more escaping to the quiz list.
· Header arrows + counter (3/25) let you jump around.
· Highlight tools: yellow, green, blue, pink, and an eraser. Tap a colour, then swipe across the text.
· Highlights are saved per question and persist between sessions.
· Notes button opens a per-question notepad (a small orange dot appears when a note exists).
· On-screen tip bar reminds you of the TV remote keys.

---

📚 Syllabus Tracker & Flashcards

Open Syllabus Tracker from the home screen.

· 3 modules → 19 chapters → topics & subtopics.
· Each chapter shows a mini progress bar and a completion count.
· Tap a chapter → flashcard deck for its topics.
· Swipe right = completed, left = not yet. Progress saves to localStorage.
· The 💡 i button on a chapter opens its Key Takeaways deck (if available).

Syllabus Tracker reads syllabus.json if present. If not, it falls back to the built-in default syllabus for Advanced Auditing, Assurance and Professional Ethics.

---

💡 Key Takeaways Deck

Swipe deck of chapter-wise takeaways.

· Sources: kt.json + any custom takeaways you add yourself.
· Tap the ⭐ button to bookmark a takeaway.
· Tap + to add your own takeaway (saved to localStorage).
· Custom takeaways show a 🗑 delete button.
· Open from:
  · Home → Key Takeaways
  · Syllabus → Swipe through all Key Takeaways
  · A chapter's 💡 i button

kt.json format

```json
{
  "chapters": [
    {
      "chapter_number": 1,
      "chapter_title": "Quality Control",
      "key_takeaways": [
        "SQC 1 requires the firm to establish a system of quality control...",
        "Engagement files should be completed in not more than 60 days..."
      ]
    }
  ]
}
```

---

💾 Data Storage

Progress is stored in IndexedDB (CAAuditProDB → store progress), keyed by mode name (easy, medium, hard, gst, fr). Each entry holds:

```js
{ idx: 12, session: [ { sel, ok, mark, caseHtml, questionHtml, optionsHtml, note }, ... ] }
```

Small settings live in localStorage:

Key Purpose
auditPro_syllabusProgress Flashcards marked as completed
auditPro_customKT Your custom Key Takeaways
auditPro_favKT Bookmarked Key Takeaways
auditPro_totalAnswered Lifetime answered counter
auditPro_supportShown Whether the support toast was already shown

Backup DB exports everything to a JSON file. Restore from File imports it back.
Clearing browser data will wipe progress — back up regularly.

---

📺 Using on a TV

1. Open the app in the TV browser (or cast from a phone/PC).
2. Use the remote's number pad:
   · 1 2 3 4 → pick A / B / C / D
   · 9 → next question
   · 0 → previous question
   · 7 → back to home
3. In Reading Mode, the same keys work, plus swipe on a touch remote to change questions.
4. The Desktop View toggle (🖥 icon) gives a wider layout that reads better on large screens.

---

🌐 Browser Support

Browser Status
Chrome / Edge (desktop & Android) ✅ Full support
Safari (iOS / macOS) ✅ Full support
Firefox ✅ Full support (best for file://)
Smart TV browsers ⚠️ Mostly works; use a local server if JSON fails to load

Requires: fetch, IndexedDB, pointer events, requestAnimationFrame.

---

🛠 Customisation

· Add questions → edit any of the JSON files (see formats above).
· Change the syllabus → edit syllabus.json. If absent, DEFAULT_SYLLABUS in the <script> is used.
· Change Key Takeaways → edit kt.json.
· Colours / theme → tweak the CSS variables in :root at the top of the <style> block.
· File names → update the FILES object near the top of the script:

```js
const FILES = {
  easy:   'study.json',
  medium: 'mcqs.json',
  hard:   'audit_case_scenarios.json',
  gst:    'gstcase_scenarios.json',
  fr:     'fr.json'
};
```

---

🙏 Credits

Made with ❤️ by Observe with Satyam

📺 youtube.com/@observe_with_satyam

---

📄 License

For personal, educational, and coaching use. Not affiliated with ICAI. Question content is the responsibility of the person supplying the JSON files.

```
### README Highlights & Usage

This README gives you a complete reference for the app. It covers:

- **Feature overview** – a quick table of every major capability, from quiz sets to analytics.
- **File setup** – which JSON files to place next to `index.html` and how to run a local server for `fetch()` to work.
- **Data formats** – accepted aliases for question text, options, correct answers, and case passages, so you can adapt existing JSON files easily.
- **Keyboard shortcuts & gestures** – includes TV remote keys (1–4 for options, 9/0 for next/previous, 7 to go back) and swipe gestures for reading mode, flashcards, and KT deck.
- **Storage & customization** – where progress is saved (IndexedDB/localStorage), how to back up or restore, and how to change file names or the syllabus.
