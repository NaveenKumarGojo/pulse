# Pulse

A self-hosted service monitoring and alerting system, built in public over 16 weeks.

---

## What is Pulse?

Pulse checks if your services are alive — HTTP endpoints, databases, scheduled jobs — and tells you when they're not. Think of it as your own minimal UptimeRobot, built from scratch.

## Why does this repo exist?

This repo is the public record of my 16-week journey from backend engineer to production-grade systems engineer. Every week I ship a real piece of Pulse and learn one core skill by **building**, not by watching tutorials. By the end, Pulse is a containerized, AWS-deployed, observable distributed system with CI/CD.

This isn't a tutorial repo. It's a portfolio. Every commit is real work.

## Current status

**Week 1 of 16** — Foundations.

See [`ROADMAP.md`](./ROADMAP.md) for the full plan and [`weeks/`](./weeks) for what's been shipped each week.

## Progress

| Week | Theme | Shipped | Status |
| ---- | ----- | ------- | ------ |
| 01 | Git + Shell foundations | `scripts/pulse-check.sh`, `scripts/repo-stats.sh` | 🚧 In progress |
| 02 | Git + Shell mastery | — | ⏳ Pending |
| 03 | SQL system design | — | ⏳ Pending |
| 04 | SQL performance | — | ⏳ Pending |
| 05 | Python debugging | — | ⏳ Pending |
| 06 | Python debugging | — | ⏳ Pending |
| 07 | FastAPI core | — | ⏳ Pending |
| 08 | FastAPI production | — | ⏳ Pending |
| 09 | Docker basics | — | ⏳ Pending |
| 10 | Docker production | — | ⏳ Pending |
| 11 | Async + queues | — | ⏳ Pending |
| 12 | System design | — | ⏳ Pending |
| 13 | AWS foundations | — | ⏳ Pending |
| 14 | AWS production | — | ⏳ Pending |
| 15 | Terraform + CI/CD | — | ⏳ Pending |
| 16 | Capstone polish | — | ⏳ Pending |

## Architecture

_Will grow as the system grows. Right now: nothing exists. By Week 16:_

```
Internet
   │
   ▼
[ALB] → [FastAPI on ECS] → [Postgres RDS]
                    │
                    ▼
              [Redis] ─── [Celery workers] ─── checks scheduled here
                                  │
                                  ▼
                          [CloudWatch logs/metrics]
                                  │
                                  ▼
                          [Alert dispatcher → webhooks]
```

## How to run

_Will be filled in starting Week 9 when Docker arrives._

## Engineering principles I'm enforcing on myself

- **Every commit signed.** No exceptions.
- **Conventional commits** (`feat:`, `fix:`, `docs:`, `refactor:`, `test:`, `chore:`).
- **Every script tested.** If it can't be tested, it gets a `# tested manually with:` comment block.
- **No copy-paste from tutorials.** If I don't understand it, I don't ship it.
- **Document the why, not the what.** Code shows what. Comments and READMEs show why.

## License

MIT
