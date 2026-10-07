# GitHub account audit (October 2026)

An audit and clean-up of every **public** repository on this account: CI, branch protection,
security settings, documentation and repo hygiene. Sensitive findings (credentials, personal
data, private repositories) were reported to the owner privately and are deliberately left out of
this public file.

Shared tooling lives in [`yogigodaraa/.github`](https://github.com/yogigodaraa/.github): default
community-health files, issue and PR templates, and reusable `node-ci` / `python-ci` workflows.
The day-to-day workflow is in [docs/WORKFLOW.md](docs/WORKFLOW.md).

## Status by repository

Legend: ✅ done · 🟡 done, follow-up open · ⛔ blocked · ➖ not applicable

| Repo | CI | Tests | Ruleset | Docs | Security | Notes |
|---|---|---|---|---|---|---|
| .github | ✅ actionlint | ➖ | ✅ | ✅ | ✅ | Reusable workflows |
| yogigodaraa | ✅ markdownlint | ➖ | ✅ | ✅ | ✅ | Profile, project index, this report |
| orbit | ✅ web | 🟡 none yet ([#19](https://github.com/yogigodaraa/orbit/issues/19)) | ✅ | ✅ PRIVACY + ARCHITECTURE | ✅ | Privacy copy corrected |
| careers-hunter | ✅ web | 🟡 none yet ([#17](https://github.com/yogigodaraa/careers-hunter/issues/17)) | ✅ | ✅ | ✅ | MIT licence added |
| SOCShield | 🟡 backend red | 🟡 51 pass / 7 fail / 4 err ([#29](https://github.com/yogigodaraa/SOCShield/issues/29)) | ✅ | ✅ | ✅ | Install was broken; fixed |
| tradingbot | ✅ | ✅ 13 (risk gate + paper default) | ✅ | ✅ disclaimer | ✅ | Sell sizing bug ([#9](https://github.com/yogigodaraa/tradingbot/issues/9)) |
| frame-map | ✅ | ✅ 56 | ✅ | ✅ | ✅ | Two stacks ([#12](https://github.com/yogigodaraa/frame-map/issues/12)) |
| care-route | ✅ | ✅ 15 (triage) | ✅ | ✅ medical notice | ✅ | Red-flag triage gap fixed |
| BlueSentinel-Log-Analyzer | 🟡 python red | 🟡 27 pass / 2 fail ([#11](https://github.com/yogigodaraa/BlueSentinel-Log-Analyzer/issues/11)) | ✅ | ✅ | ✅ | 2 MITRE regex bugs fixed |
| MIB | ✅ | ✅ 3 smoke | ✅ | ✅ | ✅ | `.gitignore` added, junk untracked |
| TensionBot | ✅ | ✅ 8 + 6 | ✅ | ✅ | ✅ | Both suites were broken |
| bhp | ✅ scripts | ✅ 2 smoke | ✅ | ✅ | ✅ | ⛔ app missing ([#2](https://github.com/yogigodaraa/bhp/issues/2)) |
| cctv-lab | ✅ | ➖ (models need GPU) | ✅ | ✅ ETHICS.md | ✅ | Licence decision pending |
| western-suburbs-…-converter | ✅ | ✅ 2 | ✅ | ✅ | ✅ | 18 empty files removed |
| budgetproof | existing | ➖ | ✅ | ⛔ | ✅ | ⛔ Held for owner review |
| customer-support-dashboard | ⛔ | ➖ | ⛔ | ⛔ | ✅ | ⛔ Held for owner review |
| CyberBreachAnalytics-, coursework ×2, visagio-hackathon | ➖ | ➖ | ➖ | ➖ | ➖ | Archived, so read-only |

**Applied to every active public repo except `customer-support-dashboard` (held for owner review):** squash-only merges (PR title becomes the commit title),
auto-merge allowed, merged branches auto-deleted, a `protect-main` ruleset (PR required, 0
approvals, required CI checks, branch up to date, conversations resolved, no force-push or deletion,
automatic Copilot code review), Dependabot alerts and security updates, private vulnerability
reporting, CodeQL default setup, a weekly `dependabot.yml`, and patch/minor-only Dependabot auto-merge.

## What's good and what's weak

| Repo | What's good | What's weak |
|---|---|---|
| orbit | Deterministic stats ground the LLM (`lib/analysis/`); clean per-relationship config; rate limiting | No tests; LLM JSON isn't schema-validated; the UI claimed keys went "directly to the provider" (fixed) |
| careers-hunter | Tiny, readable provider adapter; all state client-side; prompt forbids invented emails | "Research" is model memory, not live search; no tests |
| SOCShield | Rich, well-documented services (BEC, header forensics, MITRE); graceful fallback when Postgres/Redis are down | Install and test config were broken; several advertised features are config-only; dated model ids; ~30 overlapping status docs |
| tradingbot | Clear interfaces; paper default; walk-forward and regime-aware backtesting | Risk gate had no tests (now 11); sells sized like buys; engine never started |
| frame-map | Clean LangGraph state machine; offline stub mode makes tests credential-free | The deployed v1 has no tests while the tested v2 isn't deployed; unused heavy dependencies; Vite 8 upgrade had broken installs |
| care-route | Sensible keyword plus combination triage rules; "call 000" escape hatch in the UI | "Worst headache of my life" was routed to GP (fixed); 14 lint errors; NT postcodes map to SA |
| BlueSentinel | Strong v2 design (Drain3, DeepLog, Sigma, MITRE); a real test suite | Two detection regexes never matched as intended; graph scoring issues; v1 code duplicated |
| MIB | Thoughtful data-quality service (outliers, drift, confidence) | Only smoke tests so far; two conflicting READMEs; root-level scripts duplicate `app/` |
| TensionBot | Small and focused; good README | Neither test suite could run; generator origin needs crediting |
| bhp | Detailed data-quality documentation | The actual app isn't in the repo (broken submodule) |
| cctv-lab | Privacy by design in code (clip deletion, passcode, no identity) | No licence; no automated tests (GPU models) |
| western-suburbs-…-converter | Useful real tool; web and Python converters agree | 18 empty placeholder files; a `logging.py` shadowed the standard library |

## Risks found

- **Secrets and personal data:** reported privately. Nothing in this file.
- **Dependabot auto-merge raced CI:** between enabling `dependabot.yml` and creating the
  rulesets, Dependabot PRs auto-merged without waiting for checks (auto-merge only waits for
  *required* checks). Mostly harmless (patch/minor bumps, and the failing check was a CI bug,
  not the dependency), but `main` should be re-verified once CI is green everywhere. Rulesets now
  prevent this.
- **Red CI by design:** SOCShield (backend) and BlueSentinel (python) have pre-existing test
  failures. Their required checks will block merges until those issues are fixed. That's
  intentional; tests weren't weakened.
- **Dead demos (HTTP 404):** SOCShield, tradingbot, BlueSentinel, TensionBot, and the
  western-suburbs converter. Redeploy, or clear the homepage field.

## Decisions for the owner

| Topic | Recommendation |
|---|---|
| Rename `bhp` | `mooring-portal` (after fixing the submodule) |
| Rename `MIB` | `mooring-intelligence-backend` |
| Rename `TensionBot` | `mooring-data-generator` (matches its package name) |
| Rename `CyberBreachAnalytics-` | `cyber-breach-analytics` (archived; may need a temporary unarchive) |
| Rename `western-suburbs-cricket-club-fixture-converter` | `wscc-fixtures` |
| Rename `budgetproof` | Keep. It's short and distinctive. |
| `visagio-hackathon` | Empty and archived: delete it, or point its description at care-route |
| Mooring group (bhp, MIB, TensionBot) | Keep separate with cross-links (done). Consider a `mooring-monitoring` monorepo once bhp's app is in Git. |
| frame-map v1 vs v2 | Pick one ([#12](https://github.com/yogigodaraa/frame-map/issues/12)) |
| Coursework repos | Keep archived. To add an academic-integrity README, unarchive briefly, add it, re-archive. |
| cctv-lab licence | Consider a responsible-use licence (e.g. OpenRAIL) rather than MIT |
| TensionBot `backend/` origin | Confirm the licence of the hackathon-provided generator |

## Manual steps (web UI or extra token scopes)

1. **Pin 6 repos:** orbit, SOCShield, frame-map, tradingbot, careers-hunter, BlueSentinel-Log-Analyzer.
2. **Profile:** bio *"AI developer & security engineer · building BYOK AI tools, SOC automation and data-quality systems"*, website `yogigodara.com`, and keep your existing location line.
3. **Social preview images** (Settings → Social preview, 1280×640):
   orbit (two chat bubbles orbiting a heart/graph), SOCShield (shield over an email envelope with IOC tags),
   frame-map (an SOP page turning into a storyboard strip), tradingbot (candlesticks behind a "risk gate" barrier),
   careers-hunter (a world map with pins and an envelope).
4. **Roadmap project board:** run `gh auth refresh -s project`, then create a "Roadmap" project and add the open issues from the flagships.
5. **v0.1.0 releases** once each flagship's `main` CI is green:
   `gh release create v0.1.0 -R yogigodaraa/<repo> --generate-notes --title "v0.1.0"`.
6. **Merge queue:** not available for repos owned by a personal account. Revisit if these move to an organisation.
7. **Clean up stale branches** (all merged or one-off): `chore/trigger-*` on orbit, care-route, frame-map,
   customer-support-dashboard, tradingbot, SOCShield, BlueSentinel, MIB and the western-suburbs converter; plus
   `copilot/*`, `feat/advanced-v2`, `frontend-fixes`, `feature/backend-frontend-integration` (SOCShield),
   `feat/attack-graph`, `feat/live-demo`, `blue_sentinel` (BlueSentinel), and `yogigodaraa-patch-1` (profile).
   Check each with `git log main..origin/<branch>` before deleting.
