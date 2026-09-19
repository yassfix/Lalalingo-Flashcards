<div align="center">

<img src="asset/lalalingo-logo.png" alt="Lalalingo logo" width="96" height="96">

# Lalalingo Flashcards

**Adaptive, swipe-based vocabulary training for German and Spanish.**
Swipe to learn. Listen to remember. Sleep to reinforce.

**[Try it live → flashcards.lalalingo.app](https://flashcards.lalalingo.app/)**

<p>
  <a href="https://flashcards.lalalingo.app/"><img alt="Live demo" src="https://img.shields.io/badge/live%20demo-flashcards.lalalingo.app-2ecc71?style=flat-square"></a>
  <img alt="Open source" src="https://img.shields.io/badge/open%20source-yes-27ae60?style=flat-square">
  <img alt="Lalalingo app" src="https://img.shields.io/badge/Lalalingo%20app-launching%20early%E2%80%93mid%202027-8e44ad?style=flat-square">
  <img alt="Languages" src="https://img.shields.io/badge/languages-German%20%7C%20Spanish-3498db?style=flat-square">
  <img alt="Stack" src="https://img.shields.io/badge/stack-Vanilla%20JS%20%7C%20Firebase-e67e22?style=flat-square">
  <img alt="Last updated" src="https://img.shields.io/badge/updated-September%202026-7f8c8d?style=flat-square">
</p>

</div>

---

> [!NOTE]
> **About Lalalingo.** Lalalingo Flashcards is a standalone, open-source feature of **Lalalingo**, a comprehensive language-learning app currently in development and scheduled to launch in **early to mid 2027** at **lalalingo.app** (domain reserved). While these flashcards focus on active recall, the full Lalalingo app will centre on passive learning. This repository documents the flashcard module as of **September 2026**.

## Table of Contents

- [Overview](#overview)
- [About Lalalingo](#about-lalalingo)
- [Key Features](#key-features)
- [How It Works](#how-it-works)
- [Sleep Mode](#sleep-mode)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Roadmap](#roadmap)
- [Privacy and Data](#privacy-and-data)
- [License](#license)

## Overview

Lalalingo Flashcards is a lightweight, single-page web app for building vocabulary through short, focused review sessions. Words you struggle with come back more often, words you know fade into the background, and every card can be heard aloud, annotated, and looked up in one tap.

The app runs entirely in the browser with no build step. Sign in with Google to sync your progress across devices, or start immediately in guest mode. The hosted version is available at [flashcards.lalalingo.app](https://flashcards.lalalingo.app/).

## About Lalalingo

Lalalingo is a comprehensive language-learning app currently in development, with a planned launch in **early to mid 2027**. The domain **lalalingo.app** has been reserved for the platform. This flashcard module is one feature of that larger product, and it is released as open source in the meantime.

The two are designed to complement each other:

| | Lalalingo Flashcards (this repository) | Lalalingo app |
|---|---|---|
| **Learning style** | Active recall | Passive learning |
| **Status** | Live and open source | In development |
| **Availability** | [flashcards.lalalingo.app](https://flashcards.lalalingo.app/) | Early to mid 2027 at lalalingo.app |

## Key Features

| | Feature | Description |
|---|---|---|
| 👆 | **Swipe-based review** | Tap or swipe up to reveal a translation, swipe left for *Weak*, swipe right for *Known*. Works with touch and mouse. |
| 🔁 | **Bidirectional study** | Practice target → English, English → target, or a random mix per card. Labels adapt to the selected language. |
| 🧠 | **Adaptive repetition** | Every word carries a weight that rises and falls with your answers, so difficult words appear more often. |
| ⏱️ | **Response timer** | A 5-second timer per card rewards fast recall. |
| 🔒 | **Deck lock** | Restrict practice to words you have already swiped, so you can drill without new material. |
| 🔊 | **Text-to-speech** | Hear any word on demand, or enable auto-pronunciation as cards appear. |
| 📝 | **Personal notes** | Add context or mnemonics to both sides of every card. Notes save automatically. |
| 📚 | **Progress piles** | Review your *Weak* and *Known* words in a quick preview or a full-screen list. |
| 🔍 | **Instant lookup** | Open a web search for the current word's meaning in one tap. |
| 🌙 | **Sleep Mode** | A hands-free listening mode with a custom soundtrack and full visual customization. |
| ☁️ | **Cloud sync** | Google sign-in syncs progress, notes, and settings. Guest mode stores everything locally. |
| 🌍 | **Multi-language** | German and Spanish included, each with its own independent progress. New languages need only a word list. |

## How It Works

### Gestures

| Gesture | Action |
|---|---|
| Tap the card, or swipe up | Reveal the translation |
| Swipe left | Add to the **Weak** pile (word appears more often) |
| Swipe right | Add to the **Known** pile (word appears less often) |

### Adaptive repetition

Each word starts with a weight of **10**. The next card is chosen by weighted random selection, so a higher weight means a higher chance of appearing.

| Event | Effect on weight |
|---|---|
| Swipe left | +5 |
| Swipe right within the 5-second timer | −5 (minimum 1) |
| Swipe right after the timer expires | No change |

- **Weak pile:** words with a weight of 15 or higher.
- **Known pile:** words you have swiped whose weight is below 15.
- A recent-history buffer (up to 50 cards, capped at 60% of the deck) prevents the same word from repeating immediately.

## Sleep Mode

Sleep Mode turns your word list into a passive, hands-free listening session. For each word, in random order, the app:

1. Shows and speaks the English word.
2. Pauses for a configurable delay.
3. Shows and speaks the target-language word.
4. Repeats the target word slowly (0.6× speed) for pronunciation.

Everything is adjustable from the settings panel:

- **Soundtrack:** upload a single track or a playlist, with independent soundtrack and speech volume.
- **Session length:** all words, or a fixed word count.
- **Pacing:** delay between the English and target word.
- **Typography:** font size and color for each language.
- **Background:** a solid color or an uploaded image, fitted as cover, contain, or stretch.

Settings persist to your account when signed in, or to your browser in guest mode.

## Tech Stack

- **HTML5 / CSS3**, with no frameworks and no build tooling
- **Vanilla JavaScript (ES6+)**
- **Firebase Authentication** (Google sign-in) and **Cloud Firestore** (v10.8.0, loaded from CDN)
- **Web Speech API** for text-to-speech
- **Pointer Events API** for unified touch and mouse gestures
- **Web Storage** for guest-mode persistence

## Project Structure

```
.
├── index.html            # Application: markup, styles, and logic in a single file
├── de.txt                # German word list
├── es.txt                # Spanish word list
├── LICENSE               # MIT License
└── asset/
    ├── favicon.ico
    ├── lalalingo-logo.png
    ├── de.png            # German flag
    └── es.png            # Spanish flag
```

## Getting Started

### Run locally

Word lists are loaded with `fetch()`, so the app must be served over HTTP rather than opened directly from the file system.

```bash
# from the project root
python3 -m http.server 8000
```

Then open <http://localhost:8000>.

### Word list format

Each language reads from a plain-text file named after its language code (`de.txt`, `es.txt`). Entries take **three lines**: the target word, its English translation, and a separator line.

```text
Haus
house

Buch
book

```

### Add a language

1. Create a word list named `<code>.txt` (for example `fr.txt`) in the project root.
2. Add a flag image at `asset/<code>.png`.
3. Add an `<option value="fr">French</option>` entry to the language selector in `index.html`.
4. Map the language to a speech voice in `VOICE_MAP`, for example `'fr': 'fr-FR'`.

### Connect your own Firebase project

Cloud sync is optional. To use your own backend:

1. Create a project in the [Firebase Console](https://console.firebase.google.com/).
2. Enable **Authentication → Google** as a sign-in provider.
3. Create a **Cloud Firestore** database.
4. Replace the `firebaseConfig` object near the top of the script in `index.html` with your project's web app configuration.
5. Add your hosting domain (for example `username.github.io`) under **Authentication → Settings → Authorized domains**.
6. Restrict each user to their own data with these Firestore security rules:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
  }
}
```

User data is stored in a single document per user at `users/{uid}`, with fields `weights_<lang>`, `notes_<lang>`, and `sleepSettings`.

### Deploy with GitHub Pages

Because the app is fully static, it can be published directly: go to **Settings → Pages**, select your branch, and save.

> [!TIP]
> Text-to-speech relies on the voices installed on the user's device and browser, so pronunciation quality and voice availability vary by platform.

## Roadmap

- [x] Flashcard module with adaptive repetition, notes, and text-to-speech
- [x] Sleep Mode with customizable audio and visuals
- [x] Cloud sync with Google sign-in, plus local guest mode
- [ ] **Early to mid 2027:** Launch of the Lalalingo language-learning app at lalalingo.app, focused on passive learning and complemented by this flashcard module

## Privacy and Data

- **Guest mode:** progress, notes, and settings stay in your browser's local storage and never leave your device.
- **Signed-in mode:** progress, notes, and Sleep Mode preferences are stored in Cloud Firestore under your own account.
- **Sleep Mode media:** soundtracks and background images are processed locally in your browser. They are never uploaded, and they must be re-selected each session.

## License

Lalalingo Flashcards is open source software released under the [MIT License](LICENSE).

© 2026 Lalalingo.

---

<div align="center">
  <sub>Lalalingo Flashcards · open-source feature of the Lalalingo language-learning app, launching early to mid 2027 · Last updated September 2026</sub>
</div>
