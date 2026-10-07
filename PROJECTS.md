# Project index

Every public repository on [@yogigodaraa](https://github.com/yogigodaraa), grouped by area.
Stacks are taken from each repo's `package.json` / `requirements.txt` / `pyproject.toml`.

**Status:** `active` = code changes in the last 6 months · `prototype` = hackathon or
research build, not developed further · `archived` = read-only on GitHub.

## 🤖 AI apps

| Repo | One-liner | Stack | Status | Notes |
|---|---|---|---|---|
| [orbit](https://github.com/yogigodaraa/orbit) | AI relationship & chat analysis from WhatsApp/Instagram exports, BYOK | Next.js, TypeScript, Tailwind | active | Flagship · [demo](https://orbit-theta-one.vercel.app) |
| [careers-hunter](https://github.com/yogigodaraa/careers-hunter) | Researches companies hiring for a target role and drafts CV-grounded application emails, BYOK Claude/OpenAI/Gemini | Next.js, TypeScript, Tailwind | active | Flagship · [demo](https://careers-hunter.vercel.app) |
| [frame-map](https://github.com/yogigodaraa/frame-map) | ProcViz: 5-agent LangGraph pipeline turning industrial SOPs into animated storyboards | Python, FastAPI, LangGraph, Anthropic; React, Vite | active | Flagship · [demo](https://frame-map.vercel.app) |
| [care-route](https://github.com/yogigodaraa/care-route) | Little Help: AI care routing that triages symptoms before you default to the ER | Next.js, TypeScript, Zod; FastAPI, Anthropic | prototype | Visagio Hackathon 2025 · [demo](https://care-route-beta.vercel.app) |
| [cctv-lab](https://github.com/yogigodaraa/cctv-lab) | CCTV-style test bench for privacy-preserving fight-detection research | Node.js, Express; Python, Transformers | active | Research · [demo](https://cctv-lab.vercel.app) |

## 🛡️ Security / SOC

| Repo | One-liner | Stack | Status | Notes |
|---|---|---|---|---|
| [SOCShield](https://github.com/yogigodaraa/SOCShield) | Autonomous AI phishing detection & response: multi-provider LLM classification, IOC extraction, real-time dashboard | Python, FastAPI, Celery, Redis, SQLAlchemy, Transformers; Next.js | active | Flagship |
| [BlueSentinel-Log-Analyzer](https://github.com/yogigodaraa/BlueSentinel-Log-Analyzer) | Log anomaly detection with Isolation Forest + LLM incident summaries | Python, scikit-learn, pandas, OpenAI; Next.js | active | |
| [CyberBreachAnalytics-](https://github.com/yogigodaraa/CyberBreachAnalytics-) | Bash + awk analysis of a healthcare cyber-breach TSV dataset | Bash, awk | archived | |

## 💹 Finance

| Repo | One-liner | Stack | Status | Notes |
|---|---|---|---|---|
| [tradingbot](https://github.com/yogigodaraa/tradingbot) | Quant trading research bot for US stocks on Alpaca: ML signals + FinBERT sentiment behind a mandatory risk gate | Python, FastAPI, alpaca-py, XGBoost, scikit-learn, Transformers, uv; Next.js, pnpm | active | Flagship · paper trading · not financial advice |
| [budgetproof](https://github.com/yogigodaraa/budgetproof) | Personal finance dashboard: income, expenses, GST, tax, debt and merchant categorisation | Next.js, TypeScript, Anthropic SDK | active | No personal data in the repo by design |

## ⚓ Mooring / maritime

Three separate takes on real-time mooring-hook tension monitoring from the BHP / UWA hackathon work.

| Repo | One-liner | Stack | Status | Notes |
|---|---|---|---|---|
| [bhp](https://github.com/yogigodaraa/bhp) | Mooring Portal: hook-tension monitoring with a 4-pillar data-quality pipeline | Next.js, TypeScript; Python data generator | prototype | |
| [MIB](https://github.com/yogigodaraa/MIB) | Mooring Intelligence Backend: tension forecasting, tiered alerts, 3D hook view | Python, FastAPI, Jinja2; Next.js | active | [demo](https://mib-psi.vercel.app) |
| [TensionBot](https://github.com/yogigodaraa/TensionBot) | Synthetic mooring/oceanographic sensor generator + live Socket.io dashboard | Python, FastAPI, Click; Node.js, Express, Socket.io | prototype | |

## 🧰 Tools

| Repo | One-liner | Stack | Status | Notes |
|---|---|---|---|---|
| [customer-support-dashboard](https://github.com/yogigodaraa/customer-support-dashboard) | WeSupport: one search across Luciq, Intercom, Front and Retool | Next.js, TypeScript; Express, Prisma, Socket.io, Anthropic SDK | active | [demo](https://customer-support-dashboard.vercel.app) |
| [western-suburbs-cricket-club-fixture-converter](https://github.com/yogigodaraa/western-suburbs-cricket-club-fixture-converter) | Converts cricket fixture CSV exports into a calendar-ready format | Python, pandas; Next.js | active | |

## 🎓 Coursework (CITS1401, 2023)

| Repo | One-liner | Stack | Status | Notes |
|---|---|---|---|---|
| [regional-population-statistics](https://github.com/yogigodaraa/regional-population-statistics) | Pure-Python regional population analysis (no imports allowed) | Python | archived | University coursework |
| [world-population-analysis](https://github.com/yogigodaraa/world-population-analysis) | Web app analysing world population CSV data | JavaScript | archived | University coursework |

## 🗄️ Other

| Repo | One-liner | Stack | Status | Notes |
|---|---|---|---|---|
| [visagio-hackathon](https://github.com/yogigodaraa/visagio-hackathon) | Visagio Hackathon 2025 working repo (empty; the code lives in care-route) | — | archived | |
| [.github](https://github.com/yogigodaraa/.github) | Shared community-health files and reusable CI workflows | GitHub Actions | active | |
