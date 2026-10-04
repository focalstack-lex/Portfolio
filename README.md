# Portfolio - Lex Matondo

**Live:** https://lex-portfolio-swart.vercel.app · **Repo:** https://github.com/focalstack-lex/Portfolio

Pages:

1. **`index.html` - Entry split.** Two panels, TECH and CREATE, each opening the main portfolio in that mode.
2. **`portfolio.html` - Main portfolio.** Monochrome editorial system (white on obsidian). Tech mode: hero intro, COE student portal case study with video and screenshots, other work, stack, about, GitHub activity. Create mode: about, filterable photo archive with lightbox, production gear.
3. **`gallery.html` - Full shoot archive.** `resume.html` - printable CV. `404.html` - branded not-found page.

No build step - plain HTML/CSS/JS.

## Run

Open `index.html`, or serve the folder (`npx serve .`).

## Deploy

Deployed on Vercel (static, no build step). To ship updates: commit + push to GitHub, then run `vercel --prod` in the project folder. (For full auto-deploy-on-push: link GitHub under Vercel → Settings → Login Connections, then `vercel git connect`.) GitHub Pages is also enabled on the repo but inherits the `chemlab-system.me` custom domain - Vercel is the canonical host.

## Make it yours

Everything personal is marked with `EDIT` comments in `index.html`; on `portfolio.html` edit directly:

| What | Where |
|---|---|
| Name / role / avatar | `index.html` topbar; `portfolio.html` logo + portrait |
| Profile links (email, code, work) | `index.html` topbar-actions; `portfolio.html` footer socials + CTA `mailto:` |
| Hero pitch lines | `index.html` `.code-lines` |
| Portfolio stats & bento copy | `portfolio.html` hero-stats + bento cards (24 projects, 40+ shipped etc. are placeholders) |
| Testimonial / method copy | `portfolio.html` method section |

Design tokens live as CSS custom properties at the top of `styles.css` (entry) and `portfolio.css` (main page).

## AI Chatbot & Knowledge Base

The portfolio includes an AI portfolio guide widget powered by a personal knowledge base about Lex Matondo (`docs/lex-bio.md` and `assets/data/lex-profile.json`). It answers questions strictly about Lex's projects, skills, education, and photography while politely declining off-topic queries.

### Free API Configuration

The chatbot is wired to a Vercel Serverless Function (`/api/chat`) that supports NVIDIA NIM DeepSeek, Gemini, and Groq:

1. **NVIDIA NIM Free Endpoint (DeepSeek)**:
 - Generate your free key on [NVIDIA Build](https://build.nvidia.com/).
 - Add environment variable `NVIDIA_API_KEY` (e.g. `nvapi-...`) in Vercel (*Settings* → *Environment Variables*).
 - *(Optional)* Specify `NVIDIA_MODEL` if you want to use a specific model tag (defaults to `deepseek-ai/deepseek-v3`).
2. **Google Gemini (Free Tier)**:
 - Generate a key at [Google AI Studio](https://aistudio.google.com/).
 - Add `GEMINI_API_KEY` in Vercel.
3. **Groq (Free Tier)**:
 - Generate a key at [Groq Console](https://console.groq.com/).
 - Add `GROQ_API_KEY` in Vercel.

*(If no API key is present, the widget automatically falls back to an internal knowledge engine so the chat continues to work seamlessly.)*

## Files

- `index.html` / `styles.css` / `script.js` - hero entry page
- `portfolio.html` / `portfolio.css` / `portfolio.js` - main portfolio page
- `gallery.html` / `gallery.css` / `gallery.js` - photography gallery archive
- `chatbot.css` / `chatbot.js` - floating AI portfolio assistant widget
- `vercel.json` - security and cache headers; `.vercelignore` - keeps docs and oversized originals out of deploys
- `robots.txt` / `sitemap.xml` - search indexing
- `api/chat.js` - Vercel serverless function for AI completions
- `docs/lex-bio.md` & `assets/data/lex-profile.json` - verified knowledge base about Lex Matondo
- `docs/superpowers/specs/` - build specs mapping decisions to the design docs
