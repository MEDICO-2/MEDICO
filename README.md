# Medico AI

**Your Health, Your Language, Your Care.**

A mobile-first web app that helps people, especially senior citizens, follow their prescribed medicine schedule. It speaks reminders in English or Hindi and, with the patient's consent, prepares a message to a caregiver when reminders go unanswered.

> Medico AI is not a medical device and does not replace advice from a doctor or pharmacist. It only repeats what the user enters from their prescription. It never suggests, changes or checks doses and never identifies pills.

No build step, no dependencies, no accounts. All data stays in the browser (`localStorage`).

## Features

| Area | Status |
|---|---|
| Medicine schedule with start/end dates, doctor, instructions | Implemented |
| Spoken reminders (Web Speech API, `en-IN` / `hi-IN`) | Implemented; voice quality depends on the device |
| Taken / Remind me later / I need help, with timestamped history | Implemented |
| Escalation: reminder, one follow-up, caregiver message | Implemented |
| Consent, revoke access, quiet hours, configurable delays | Implemented |
| Emergency number (configurable) and `tel:` call button | Implemented |
| Find care: opens Google Maps / OpenStreetMap searches near the user | Implemented (no provider data stored or verified) |
| Export and delete all data | Implemented |
| Automated phone calls and delivery-confirmed caregiver alerts | Not included: needs a backend and a provider (see roadmap) |
| Accounts, multi-device sync, health-record storage, appointments | Not included: needs Supabase or similar |

### How escalation works

1. At the scheduled time the reminder is shown and spoken.
2. No answer after the grace period (default 5 min): one follow-up.
3. No answer after another grace period: if the patient consented and saved a caregiver number, the app opens a pre-filled SMS for the patient to send. The activity log records "prepared", never "delivered".
4. The medicine is marked missed. A missed reminder is never treated as an emergency.

Each stage runs at most once per medicine per day. Quiet hours suppress everything.

Reminders only fire while the page is open. Reliable background reminders need a native app, push notifications or a server.

## Run locally

```bash
git clone <your-repo-url> && cd medico-ai
npm start          # serves http://localhost:8080 (needs Python 3)
npm test           # Node 18+, no installs
```

ES modules need an http server; opening `index.html` directly from disk will not work.

## Deploy to GitHub Pages

Push to GitHub, then **Settings → Pages → Deploy from a branch → `main` / root**.

## Project structure

```
index.html          app shell
css/styles.css      design system, responsive layout, dark mode
js/logic.js         pure scheduling and escalation logic (tested)
js/app.js           UI, storage, speech, reminder loop
tests/logic.test.js unit tests (node:test)
```

## Roadmap

- Supabase auth, Postgres with row-level security, private storage for health records
- Server-side escalation with a calling/SMS provider that reports delivery status
- Appointments and a verified provider directory with a documented verification process
- More Indian languages (add a dictionary to `L` in `js/app.js`)
- Web Push and PWA install

## Contributing

Issues and pull requests are welcome. Please keep the safety rules: no invented medical data, no unverified "verified" labels, no claims of delivery without provider confirmation.

## License

MIT

