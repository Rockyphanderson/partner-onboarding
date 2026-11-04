# Partner Onboarding Assistant (demo)

A portfolio demo showing how a new B2B partner (hotel, airline, bank/card, affiliate) goes from **Signed** to **Live & growing**.

**Rules check, AI explains & drafts, a human decides.**

> Demo mode only. Fictional partners, sample data in the browser, canned AI output. No login, no backend, no API keys, no real partner data, and no emails are sent. Every sample number is tagged `example`.

## The 6 stages

| # | Stage | Who | What happens |
|---|-------|-----|--------------|
| 1 | Intake & setup | Partner | One form. Required: name, type, market, launch date, contact. Warns if launch is under 7 days away. |
| 2 | Smart checklist + readiness tracker | Fixed rules | Base items + extras by partner type. Due dates count back from launch (contract −14d, brand −10d, tracking −7d, creatives −7d, landing −5d, final check −2d). Items are flagged **LATE** if not done after their due date. Readiness = done required ÷ required. |
| 3 | Integration test | Fixed rules | Each tracking/booking link must be a valid URL, use https, have `utm_source`, `utm_medium`, `utm_campaign`, `partner_id`, and `partner_id` must match the partner. The response check is simulated. Failing links get a rule-based fix. |
| 4 | Self-serve portal + AI | AI drafts | AI drafts a welcome email, plain-words explanations of pending items, FAQs from a guidelines text, and a localized welcome. Each is labelled **AI draft**, editable, and reviewed by the partner manager. A preview shows what the partner sees. |
| 5 | Approve & launch | Human decides | **Approve & launch** stays locked until readiness = 100% and all link tests pass. A named partner manager approves, and the approval is logged with a timestamp. The AI has no approve action. |
| 6 | Early performance | Live | 30-day snapshot (example data): CVR = bookings ÷ clicks, ROI = (revenue − cost) ÷ cost. Flags "needs attention" for 0 bookings by day 14 or CVR under a threshold. "Create campaign brief" links out to Synq. |

A **Who does what** toggle shows the Partner, Rules & AI, and Partner manager lanes. A success-metrics strip shows time to first booking, emails avoided, tracking errors caught pre-launch, and partner activity after 90 days.

## Run locally

```bash
npm install
npm run dev            # http://localhost:5173
# or a production build:
npm run build && npm run preview   # http://localhost:4174
```

Append `?today=2026-11-03` to pin the demo date (used by the tests so LATE flags are stable).

## Tests

```bash
npm test               # unit tests: intake, checklist extras, due dates, LATE, readiness, link rules, launch gate, approval, snapshot
npm run build && npm run preview &   # then:
npm run e2e            # headless Chrome walkthrough + screenshots in screenshots/ (needs Chrome at /usr/bin/google-chrome or CHROME=...)
```

## GitHub Pages build (later)

```bash
npm run build:pages    # same as: npx vite build --base=/partner-onboarding/
```

Not deployed yet.

## Stack

Vite + React + TypeScript, plain CSS (Inter, light/dark). No backend. The rules live in `src/lib/` (pure functions, unit-tested). Demo AI output is in `src/demo/ai.ts`.
