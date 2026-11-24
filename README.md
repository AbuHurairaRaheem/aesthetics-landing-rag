# Refine Aesthetics — Landing Page + Chatbot Demo (Whole Project)

**Business:** Refine Aesthetics by Dr. Areesha — aesthetics, skincare & dental clinic, Karachi
**Branches:** Clifton & Gulistan-e-Johar | **Hours:** Mon–Sat, 3:00–10:00 PM | **Phone:** 0334 3151514
**Instagram:** [@refineaestheticsbydrareeseha](https://www.instagram.com/refineaestheticsbydrareeseha/)
**Live demo (already deployed):** https://refine-aesthetics-landing-page.vercel.app — no login needed
**Status:** DEMO / PROTOTYPE, not a live production system. Bookings are saved in the visitor's browser only (localStorage). There is no live database, calendar sync, or WhatsApp connection yet.

## What is in this project

A landing page that opens with Dr. Areesha, then services and reviews, then a **Book** button that opens the chatbot on the same page. The chatbot asks for the date first, checks availability, then takes branch, name and mobile, and gives a booking reference. A **Staff desk** tab lets the clinic approve, decline or undo a booking, and the patient chat updates.

Verified facts only. Every fee is **[TBC]** — the bot never invents a price or a discount.

## Real-time RAG assistant (Ask Our AI Assistant)

A floating **Ask Our AI Assistant** button (bottom-right) opens a chat widget that does visible retrieval — the "real talk":

1. **Retrieve first.** Every question is matched against `data/knowledge-base.json` (8 verified facts: timings, branches, services, booking flow, contact, price policy, emergency rule, human handover). The widget shows which facts it retrieved, with source badges and a relevance bar, before it answers.
2. **Answer only from those facts.** No retrieved fact = no guess — the bot says so and gives the clinic phone 0334 3151514.
3. **Live mode (optional).** Paste your own Groq key in the chat's key box. The key stays in that browser tab only, is never saved, and is sent only to `api.groq.com`. With a key, Groq (`openai/gpt-oss-120b`, fallback `openai/gpt-oss-20b`, temperature 0.2) writes the answer from the retrieved facts. Without a key, the widget works fully in **DEMO MODE** from the retrieved facts — the badge in the chat header always shows which mode you are in.
4. **Voice.** Tap the mic to speak (Web Speech API) — the transcription appears in the box first so you can correct it before sending. Voice replies are optional (toggle in the chat); if speech is unavailable the widget says so plainly.
5. **Safety rules (hard).** Fee → [TBC] + phone, never a discount. Qualifications → not confirmed, offer staff contact. Emergency (severe pain / swelling / bleeding) → immediate handover with the clinic number. Human / complaint / price negotiation → staff handover with full chat history.

The 8 facts in `data/knowledge-base.json` are the single source of truth. The same list is embedded in `index.html` as a fallback so the widget still works when the file is opened directly (double-click, no server).

Try it: **"What are your working hours?"** → retrieves Timings. **"Kitni fee hai?"** → [TBC] + phone. **"Doctor ki qualification kya hai?"** → not confirmed. **"I have severe pain"** → emergency handover.

## Tech stack

| Layer | Technology | Why |
|---|---|---|
| Page | HTML5, single file `index.html` | No build step, opens anywhere |
| Styling | CSS3 (custom, in-file) + Google Fonts: Cormorant Garamond (display) + Manrope (body) | Luxury, light/warm, minimal look |
| Logic | Vanilla JavaScript (in-file, no framework) | Booking flow, availability check, staff approval, lead log |
| Images | Embedded as base64 inside `index.html` | No broken image links, works offline after load |
| Data (demo) | Browser localStorage | Bookings + leads stay on that device only |
| Voice (demo) | Web Speech API (browser speech-to-text / text-to-speech) | Mic button in chat; needs a browser that supports it |
| Hosting | Vercel (static) — also works on Netlify / GitHub Pages | Free static hosting, custom domain ready |
| Version control | Git + GitHub | Push this folder, import it in Vercel |

**No backend yet.** No Node.js, no database, no WhatsApp API in this zip. Those are Phase 2 (see "From demo to live" below).

## Project structure

```
refine-aesthetics-landing/
├── index.html                  # The whole site: landing + chatbot + staff desk
├── package.json                # Scripts: preview locally, deploy to Vercel
├── vercel.json                 # Static-site config for Vercel
├── netlify.toml                # Static-site config for Netlify (alternative)
├── .gitignore
├── README.md                   # This file
├── data/
│   ├── business-facts.json     # Verified facts only + [TBC] list
│   └── knowledge-base.json     # 8 RAG facts — single source of truth for the AI assistant
└── docs/
    ├── TECH-STACK.md           # Full stack + how to change it
    └── EXECUTION-OUTLINE.md    # Demo → Discovery → Live build → Pilot → Handover
```

## Run it locally (2 minutes)

Option A — just open it:
1. Unzip the project.
2. Double-click `index.html`. It opens in your browser. No install needed.

Option B — local server (better, same as live):
```bash
cd refine-aesthetics-landing
npx serve .
# or: python3 -m http.server 8000
```
Then open http://localhost:3000 (serve) or http://localhost:8000 (Python).

Try this flow: **Book → pick a date (Sundays are closed) → pick a free slot → branch → name + mobile → get a reference → open Staff desk → Approve.** The patient chat then shows the confirmation.

## Shift / deploy it (move it to your own hosting)

### Vercel (recommended — same as the live link)
1. Push this folder to a GitHub repo.
2. In Vercel: **Add New → Project → Import** the repo. Framework preset: **Other**. No build command, no output directory change.
3. Deploy. You get a `*.vercel.app` link. Add a custom domain later in Vercel → Domains.
4. Or without GitHub: `npx vercel` inside this folder, then `npx vercel --prod`.

### Netlify (alternative)
Drag the unzipped folder onto https://app.netlify.com/drop — or `netlify deploy --prod --dir=.`. `netlify.toml` is already included.

### GitHub Pages (alternative)
Push to GitHub, then Settings → Pages → Deploy from branch → `main`, folder `/ (root)`.

## Verified facts (do not change without proof)

| Fact | Value | Status |
|---|---|---|
| Business | Refine Aesthetics by Dr. Areesha | Verified — Instagram / Facebook |
| Branches | Clifton, Karachi & Gulistan-e-Johar, Karachi | Verified |
| Hours | Mon–Sat, 3:00–10:00 PM | Verified |
| Phone | 0334 3151514 | Verified |
| Instagram | @refineaestheticsbydrareeseha | Verified |
| Services in demo | Aesthetics consultation, Skincare consultation, Dental enquiry | Verified as categories only |
| Fees / prices | — | **[TBC] — not confirmed, never invent** |
| Doctor bio / qualifications | Dr. Areesha, founder & lead | Verified as role only; bio/qualifications [TBC] |
| Reviews in demo | Labelled illustrative demo content | **Replace with the clinic's real reviews before launch** |
| Photos in demo | Labelled illustrative demo content | **Replace with the clinic's real photos before launch** |

Full list: `data/business-facts.json`.

## Demo vs live — read this before you show it

- **Demo:** bookings are requests, saved in the browser. Staff approval happens in the same browser. Nothing is sent to the clinic yet.
- **Live (next build):** real database + staff login + calendar + alerts, so a booking on the patient's phone appears on the clinic's phone. That is a separate 3–5 day build — see `docs/EXECUTION-OUTLINE.md`.
- Never present this zip as the live system. Say: "This is a demo of how it will work."

## From demo to live (plan)

1. **Discovery** — confirm services, prices, hours, deposit policy, calendar access, Instagram access with the clinic. Publish nothing until the owner says yes.
2. **Live build (3–5 days)** — one-page site + chatbot with a knowledge base built only from discovery facts + staff dashboard with real database.
3. **Pilot (2 weeks)** — kill rule: fewer than 5 real bookings → review, do not keep charging.
4. **Handover** — clinic owns the domain, hosting, Instagram, and lead log. Monthly care is optional, price [TBC].

## Costs (Pakistan, from the pricing sheet — re-check before quoting)

- Launch cash cost: **Rs 9,029** (domain ~Rs 3,429/yr + first month Vercel Pro ~Rs 5,600).
- Running, website chatbot only: **~Rs 6,200–7,500/month** (Vercel Pro + AI usage).
- WhatsApp phase (later): **+Rs 50,000 setup**, running **~Rs 9,000–14,000/month** at clinic volume.
- Charge proposed for Refine: **Rs 85,000 one-time** (website + chatbot), **Rs 10,000/month** care. These are proposed prices, not confirmed by the clinic.
