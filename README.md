# Hi, I'm Alena

I bridge **lighting design** and **AI automation**.

For 9+ years I've been the only in-house lighting engineer on architectural lighting projects: facades, Christmas lighting and seasonal decorations, 3ds Max modeling and visualizations, Dialux calculations, AutoCAD project work, endless photo reports and documentation. At some point I got tired of doing the same work by hand and started replacing it with Python + LLMs.

Now I'm moving towards **AI-powered tools for real-world workflows** — photos, documents, Telegram data, creative tasks.

- Based in Batumi, Georgia · remote / Batumi-based
- Languages: Russian, English (B2)
- Interested in roles around AI automation / prompt engineering / creative tech

---

## What I like to build

- Small tools that turn a few days of routine into a few minutes of scripts  
- Prototypes with LLMs and Hugging Face models (CLIP, Stable Diffusion, etc.)  
- Tools for photo-heavy and Telegram-based workflows (reports, rentals, content creation)  

I care about tools that remove real manual work, not just “cool demos”.

---

## Selected projects

### RentGram — Telegram rental scraper + viewer

[RentGram](https://github.com/AlenaYashkina/rent_gram)

Scraper + frontend viewer for Telegram rental listings.

- walks Telegram channels and topics, stores messages in SQLite  
- deduplicates listings by normalized text hash + photo hashes  
- asks an LLM to extract structured fields (price, currency, location, term, pets, notes, etc.)  
- exposes a JSON API + React frontend with filters for quick search

Stack: Python 3.11, Telethon, SQLite, Ollama/LLM, Node + React + Vite.

---

### Photo reports automation (production)

[photo_reports_automation](https://github.com/AlenaYashkina/photo-report-generator)

Toolchain that takes thousands of photos in dated folders and turns them into:

- stamped images with location, date/time and other metadata as watermarks
- structured folders by object, issue type and fix stage (detected / in_progress / fixed)
- ready-to-send PowerPoint reports

Used in real architectural lighting inspections instead of manual Photoshop + PowerPoint.  
In practice it cut a **2–3 week** reporting cycle down to about **2–3 days** per season.

Stack: Python, Pillow/OpenCV, python-pptx, etc.

---

### CLIP-based photo clusterer with UI (WIP)

Interactive app for clustering large photo sets:

- embeds images with CLIP (Hugging Face / OpenAI)
- lets you quickly label a small subset
- auto-assigns labels to the rest when confidence is high
- supports manual corrections and export

Initial version was in Streamlit; now I’m moving the logic into a clean backend with a separate frontend.

Stack: Python, PyTorch, CLIP, (was Streamlit), pandas.

---

### Offline batch AI retouch (local, WIP)

Local, scriptable pipeline for AI-based portrait/photo retouching:

- face / portrait masking
- skin smoothing / blemish control
- global tone / contrast adjustments
- optional background blur
- presets and batch CLI for whole folders

Stack: Python, OpenCV, MediaPipe, GFPGAN, CLI tooling.

---

## Other tools & experiments

- **Telegram media loader**  
  Telethon-based loader that walks channels and supergroup topics in batches, downloads media by date ranges, keeps album/grouped messages together and organizes everything into a clean folder structure.

- **Social content assistant (WIP)**  
  Small assistant that turns a high-level prompt into ready content for social media (texts, structure, asset hooks) to speed up posting for my music projects.

- **Metal music generation**  
  Fine-tuning a MIDI model on my own heavy music dataset for riff/phrase generation.

- **Stable Diffusion inpainting for work tasks**  
  Quick edits and “night / snow / decoration” variants for architecture and real-estate visuals.

Most of this started as internal tools; I’ll gradually open what’s stable enough to share.

---

## Contact

- Email: _your.email@example.com_  
- Telegram: `@alenayashkina`  
- [LinkedIn](https://www.linkedin.com/in/%D0%B0%D0%BB%D1%91%D0%BD%D0%B0-%D1%8F%D1%88%D0%BA%D0%B8%D0%BD%D0%B0-a9994a35a/)
