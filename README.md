# 👋 Treasure Okeniyi

**`tokeniyi`** — I build backend systems, Telegram bots, and measurement tools, and I try to be honest about which of them actually work.

```python
bot_state_machine = "async, FSM-driven, PostgreSQL-backed"
engine_hot_path   = "zero allocation, no exceptions"
benchmarks        = "median + IQR, never a single run"
```

---

## What I'm working on

### 🔴 Live

**[chessbot](https://github.com/tokeniyi/chessbot)** · *private* · Python
A chess engine and browser UI written with no third-party packages. Magic bitboards, Zobrist hashing, alpha-beta with PVS, a 2M-entry transposition table, quiescence search, and a UCI adapter so it can hand off to Stockfish. Move encoding is a packed 16-bit int; attacks are precomputed at import.
*Where it's headed:* v0.1.0 is tagged. Next is breadth — endgames, opening book, and untapping the search loop.

**[audio-gc-benchmark](https://github.com/tokeniyi/audio-gc-benchmark)** · C++ / Python
Cross-language real-time audio callback benchmark. A C++ engine with a strictly zero-allocation hot path against a Python engine deliberately churning the cyclic heap, both instrumented at microsecond resolution.

| | mean | jitter | p99 | underruns |
|---|---|---|---|---|
| C++ (zero-alloc) | 3.51 µs | 2.16 µs | 8.20 µs | 0 |
| Python (GC churn) | 587.84 µs | 443.24 µs | 2,122.88 µs | 4 |

*Where it's headed:* the single-run table above is the weakness, not the numbers. [`FUTURE_UPDATES.md`](https://github.com/tokeniyi/audio-gc-benchmark/blob/main/FUTURE_UPDATES.md) is an honest self-critique — N trials with median/IQR, warm-up discard, GC-pressure presets, Rust and .NET columns, a lock-free control, and a headless `--mock` path so CI can run it without an audio device.

**[Biblical-E-commerce-website](https://github.com/tokeniyi/Biblical-E-commerce-website)** · Next.js 15 · NestJS · Prisma
Full-stack e-commerce monorepo. `apps/web`, `apps/api`, `packages/shared` (Zod contracts shared across both), pnpm workspaces + Turborepo. Ships four GitHub workflows: PR checks, unit tests, and staging/production deploys to Railway and Vercel.
*Where it's headed:* Auth.js on JWT (not DB sessions) so the API stays stateless, Neon Postgres, Paystack and Stripe.

**[Packitbot](https://github.com/tokeniyi/Packitbot)** · Python 3.12 · aiogram 3 · SQLAlchemy 2.0
On-campus delivery logistics for Covenant University. Students request, verified drivers claim, an admin portal arbitrates. The interesting part is the shape: role-scoped Telegram menus, multi-step FSM forms with lead-time validation, Redis-backed session state, and a domain layer where business rules live apart from handlers.
*This is the most mature thing on this page* — 77 commits, a tagged release, migrations, Docker, tests.

### 🟡 In progress

- **[school-delivery-bot1](https://github.com/tokeniyi/school-delivery-bot1)** — same problem space as Packitbot, earlier generation. Students matched with parent travelers; service-layer architecture, PostgreSQL, Redis, Docker, Fly.io config.
- **[AttendanceMaster](https://github.com/tokeniyi/AttendanceMaster)** — Next.js + Supabase. Scans paper attendance sheets with **Tesseract.js in the browser**, so no sheet image ever leaves the machine. Fuse.js fuzzy-matches names and *learns from manual corrections* — a fix where a correction would otherwise beat a legitimate exact match was the last real bug.

### 🤝 Collaborations

Write access, not owner — the projects I get to build in rather than own.

- **[eddy-mfon/Zoid](https://github.com/eddy-mfon/Zoid)** — jersey marketplace, Vite + React 19 + Express, pnpm, deploying to Vercel. I mostly work the storefront: a *Store Manager Console* admin portal, auth with checkout profile autofill, wishlist and order history, GSAP scroll choreography. Design direction is [`ideas.md`](https://github.com/eddy-mfon/Zoid/blob/main/ideas.md) — "Concrete Ritual", pigment-pink tactical route lines over a dark cinematic ground.
- **[Zion-123456/Memo-SWEP-Bot](https://github.com/Zion-123456/Memo-SWEP-Bot)** — layered Telegram + FastAPI bot: `models` / `repositories` / `services` / `schemas` / `api`, with the rule that repositories hold no business logic.

### 📚 Foundations — and a caveat

I wanted these to be the pedagogical centre of the profile, so I'm being precise about their state.

- **[ml-from-scratch](https://github.com/tokeniyi/ml-from-scratch)** — the package layout is there (`algorithms/supervised`, `unsupervised`, `neural_networks`, plus `datasets`, `notebooks`, `tests`, `utils`). **Every source file in it is currently 0 bytes.** The README describes linear regression through Adam as implemented; none of it is. That's a scaffold with a very good README, and I'd rather say so here than let a visitor discover it.
- **[transformers-from-scratch](https://github.com/tokeniyi/transformers-from-scratch)** — same story. `components/multi_head_attention.py`, `models/transformer.py`, `utils/masking.py` and the rest exist as empty files. Next commit in that repo should be a body of code, not more docs.
- **[learning-python](https://github.com/tokeniyi/learning-python)** — genuinely small and genuinely finished: a palindrome checker refactored to handle strings, numbers and sequences, and a password validator that grew into entropy analysis with an optional HIBP breach check.

### 🔒 Private

- **[hermes-backup](https://github.com/tokeniyi/hermes-backup)** — versioned backup of my agent config, skills, memories and cron jobs, with a [`RESTORE.md`](https://github.com/tokeniyi/hermes-backup/blob/main/RESTORE.md) so future-me can actually use it.

### 🍴 Forks

`[gpt-oss](https://github.com/tokeniyi/gpt-oss)` (OpenAI's open-weight models, untouched — vendored for reference) and `[flutter_ecommerce_template](https://github.com/tokeniyi/flutter_ecommerce_template)`. Not my code; I keep them close for the reference value.

---

## Stack

| | |
|---|---|
| **Languages** | Python 3.12 · TypeScript · C++ · SQL/PLpgSQL · Dart |
| **Bots** | aiogram 3 · Telegram Bot API · FSM + Redis |
| **Web** | Next.js (App Router) · NestJS · Vite · React 19 · Tailwind · shadcn/ui · GSAP |
| **Data** | PostgreSQL · asyncpg · SQLAlchemy 2.0 · Prisma · Supabase · Redis · Alembic |
| **ML** | PyTorch · NumPy · implementing attention and backprop by hand |
| **Systems** | PortAudio · latency/jitter instrumentation · aiogram, Docker, Turborepo, GitHub Actions |
| **Also** | Tesseract.js OCR, Fuse.js fuzzy matching, Zod shared contracts |

---

## How I work

- **Measure, don't assert.** The audio benchmark exists because I wanted to know, not because C++ being faster is interesting trivia. Single-run latency tables are noise; the fix is already written down in that repo's roadmap.
- **Boundaries earn their keep.** Business rules in services, not handlers. Zod schemas shared between frontend and API so they can't drift. No third-party packages in the chess engine — not as purity, but because I wanted to understand the move generator.
- **Write the ugly truth in the repo.** `FUTURE_UPDATES.md` lists eight categories of things wrong with my own benchmark. That's the most useful file in it.
- **Clean up after yourself.** `.env.local` got committed in one repo, so it went into `.dockerignore` and history got a fix commit the same week.

## Known gaps

Stated plainly because a profile that only lists strengths is marketing:

- **No CI has ever run.** Four workflow files exist in the e-commerce repo; zero recorded runs on any repository. I'm writing the pipelines faster than I trust them.
- **Zero stars and forks** across 11 public repos. I build in public and mostly alone.
- **The `*-from-scratch` repos are empty shells.** Flagged above.
- **Scratch files leak in.** Memo-SWEP-Bot has ten committed `tmp_*.py` probes. The kind of thing that gets cleaned the moment someone else reads the repo.

---

## Contact

Open an issue or PR on anything here — for a bug, a design disagreement, or a contribution. The bots, the chess engine, and the benchmark are all fair game and all benefit from outside eyes.

*Profile last audited 2026-09-26 against the live GitHub API — repo contents, commit history, and language breakdowns, not from memory.*
