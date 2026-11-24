# Tech stack — Demo Clinic landing + chatbot demo

## Current stack (what is in this zip)

| Layer | Choice | Notes |
|---|---|---|
| Frontend | HTML5 + CSS3 + vanilla JavaScript, one file (`index.html`) | No framework, no build step. Open it anywhere. |
| Fonts | Google Fonts — Cormorant Garamond (headings) + Manrope (body) | Needs internet for fonts; falls back to system serif/sans offline. |
| Images | Base64 embedded in `index.html` | File is ~5 MB because of this. No external image links to break. |
| Chatbot logic | Vanilla JS state machine in the page | Flow: date → availability → branch → name + phone → confirm as a request. Roman Urdu time parsing, phone validation, price-bargaining handling (restates real/[TBC] fee, never invents a discount, tags it for staff). |
| Voice | Web Speech API (SpeechRecognition + speechSynthesis) | Browser feature only; test the mic in Chrome. Not tested in every browser. |
| Staff side | Same page, Staff desk tab, localStorage lead inbox | Approve / Decline / Undo, availability slots, callback queue. Same-browser only in the demo. |
| Data | localStorage | Demo only. Clearing browser data clears bookings. |
| Hosting | Vercel static (live link in README) | `vercel.json` included. Netlify + GitHub Pages also work (`netlify.toml` included). |

## What is NOT in this stack (yet)

- No backend, no Node.js server, no database (Supabase / Firebase / Postgres).
- No user login / staff authentication.
- No calendar sync (Google Calendar / Calendly / Fresha).
- No WhatsApp Business API / ManyChat / Instagram DM automation.
- No analytics.

## Live-build stack (recommended, when the clinic says yes)

- Frontend: keep this static site, or move to Next.js (React) if the clinic wants a CMS.
- Backend + database: Next.js API routes + Supabase (Postgres + Auth) — or Firebase. One database for bookings, leads, slots, staff.
- Booking: staff set weekly hours + block slots in the dashboard; chatbot reads the same slots, so nothing double-books.
- Alerts: WhatsApp / SMS / email to reception on every new booking request.
- WhatsApp phase: Meta WhatsApp Business API via ManyChat or a direct API integration; clinic pays Meta + platform directly. Instagram DM via ManyChat, same knowledge base.
- Hosting: Vercel static hosting (live link in README).

## How to change things

- Text / hours / phone / branches: edit `index.html` AND `data/business-facts.json` together — keep them in sync.
- Prices: only add a price after the clinic confirms it in writing. Until then keep [TBC].
- Photos / reviews: replace the illustrative demo content with the clinic's real photos and reviews before any public launch.
- Colours / fonts: search `index.html` for the CSS variables at the top of the `<style>` block.
