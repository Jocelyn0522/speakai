# SpeakAI

An English speaking practice PWA for iOS. Single HTML file, no backend, no build step.

**Live URL:** https://jocelyn0522.github.io/speakai/

## How to Update

1. `git clone https://github.com/Jocelyn0522/speakai.git`
2. Edit `index.html` (this is the file GitHub Pages serves)
3. `git add index.html && git commit -m "your message" && git push origin main`
4. Wait ~1 min, site auto-updates

> ⚠️ **Always edit `index.html`, NOT `SpeakAI.html`.** GitHub Pages serves `index.html` by default.

## Architecture

- **Single file:** `index.html` — all HTML, CSS, JS in one file
- **No backend:** API calls go directly to OpenAI from the browser
- **No build step:** push HTML → live
- **PWA:** add to iPhone home screen for full-screen app experience

## Features

### Speaking Practice (5 modes)
| Tab | What it does |
|-----|-------------|
| 🗣 Free Chat | Daily English conversation, AI corrects grammar |
| 👔 Interview | Mock Staff Product Designer interview |
| 🎨 Design Talk | Discuss UX/design topics in English |
| 📝 Grammar | Strict grammar correction mode |
| 🔥 Debate | AI takes opposing view, practice arguing |

### Daily Words
- 📖 456 built-in vocabulary words (no API cost)
- 10 words per day, auto-rotates
- Categories: Design & UX, Product, Workplace, Interview, Phrasal Verbs, Idioms, Grammar, Tech, Travel, Emotions
- Tap "Practice this word" → jumps to Free Chat with a pre-filled prompt

### Voice Input
- Uses MediaRecorder API + OpenAI Whisper API for speech-to-text
- Mic permission requested once, stream kept alive
- Works in Safari and PWA mode on iOS

### Feedback System
- AI returns structured JSON with `reply` + `feedback` array
- Corrections appear under user's message (not in AI reply)
- Error categories: grammar, vocabulary, phrasing, natural
- Shows: original → correction → explanation

## Tech Details

- **AI Model:** `gpt-4o` (chat) + `whisper-1` (speech-to-text)
- **API Key:** User enters their own OpenAI key, stored in `localStorage`
- **JSON Mode:** Uses `response_format: { type: "json_object" }` for reliable structured output
- **Mic:** `navigator.mediaDevices.getUserMedia({ audio: true })` → `MediaRecorder` → Whisper API
- **No `webkitSpeechRecognition`:** doesn't work in iOS PWA mode

## OpenAI API Endpoints

- Chat: `POST https://api.openai.com/v1/chat/completions`
- Whisper: `POST https://api.openai.com/v1/audio/transcriptions`

## File Structure

```
speakai/
├── index.html      ← MAIN FILE (GitHub Pages serves this)
├── SpeakAI.html    ← Backup copy (keep in sync with index.html)
└── README.md       ← This file
```

## For New AI / Developer Handoff

To take over development of this app, you need:

1. **GitHub repo access:** `https://github.com/Jocelyn0522/speakai.git`
2. **GitHub token:** Personal Access Token with `repo` permission (for git push)
3. **Edit `index.html`** — this is the deployed file
4. **OpenAI API key** (optional): only needed if you want to test API features. Users enter their own key in the app UI.

That's it. No environment setup, no dependencies, no build tools.

## Known Issues / TODO

- [ ] Expand vocabulary to 3,650 words (1 year at 10/day) — currently 456
- [ ] Add word bookmark/favorite feature
- [ ] Add pronunciation audio (could use OpenAI TTS or browser SpeechSynthesis)
- [ ] Track learned words progress
