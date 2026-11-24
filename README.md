# Clinic Landing + AI Chatbot Demo

A static landing page with an AI receptionist chatbot, booking flow, and staff approval desk. Demo only.

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Stack](https://img.shields.io/badge/stack-HTML%20%7C%20CSS%20%7C%20JavaScript-blue)](docs/TECH-STACK.md)
[![Status](https://img.shields.io/badge/status-demo-orange)](#demo-vs-live)

## What it does

- Landing page with a Book button that opens the chatbot.
- Booking: pick a date, check availability, pick a branch and slot, share name and mobile, get a reference.
- Chatbot: answers only from `data/knowledge-base.json`, with source badges.
- Staff desk: approve, decline, or undo a booking.
- Voice input and voice replies, with text fallback.

## Quick Start

```bash
npx serve .
# then open http://localhost:3000
```

Or double-click `index.html`. No build step, no backend.

## How it works

1. Retrieve first from `data/knowledge-base.json`.
2. Answer only from those facts. No fact = no guess.
3. Fees are `[TBC]`. The bot never invents a price or a discount.
4. Emergency or human request = handover to staff.

## Tech Stack

HTML5, CSS3, Vanilla JavaScript, Web Speech API, localStorage. Hosted as a static site on Vercel.

## Project Structure

```
.
├── index.html
├── data/
│   ├── business-facts.json
│   └── knowledge-base.json
└── docs/
    ├── TECH-STACK.md
    └── EXECUTION-OUTLINE.md
```

## Demo vs Live

Demo: bookings are requests saved in the browser only. No live database, calendar, or WhatsApp yet.

## License

MIT — see `LICENSE`.
