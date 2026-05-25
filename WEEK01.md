# Week 1 — Git Foundations + Shell Starter

> **Theme:** Stop being scared of the terminal and Git. Build the muscle for daily commits.
> **Time budget:** 10 hours (2 evenings × 2 hrs + 1 weekend × 6 hrs)
> **End state:** A public GitHub repo with senior-level hygiene and two working bash scripts.

---

## Why this week matters

Every week of Pulse depends on Git and Shell. If these are weak, everything else is slower. Most developers with 5 years experience have huge gaps here — not because they're dumb, but because tutorials skip the parts that actually matter day-to-day. Fix that this week and you'll be faster than 80% of working engineers for the rest of your career.

---

## ✅ Checklist

### Day 1 — Repo setup (2 hrs)

- [ ] **Create public GitHub repo** named `pulse`. Description: "A self-hosted service monitoring system. Built in public over 16 weeks."
- [ ] **Clone locally**, drop in this `README.md`, `ROADMAP.md`, and `weeks/WEEK01.md`
- [ ] **Add a proper `.gitignore`** (Python + Node + OS + IDE — get the full one from gitignore.io)
- [ ] **Add `LICENSE`** (MIT is fine)
- [ ] **First commit:** `chore: initial repo setup` — must be signed (see below)

### Day 1 — Sign your commits (1 hr — non-negotiable)

- [ ] Generate a GPG key: `gpg --full-generate-key`
- [ ] Add it to GitHub: Settings → SSH and GPG keys → New GPG key
- [ ] Configure git globally:
  ```bash
  git config --global user.signingkey <YOUR_KEY_ID>
  git config --global commit.gpgsign true
  git config --global tag.gpgsign true
  ```
- [ ] Verify: make a test commit, run `git log --show-signature` — should show "Good signature"
- [ ] On GitHub, your commits now have a green "Verified" badge. **This single thing puts you ahead of 95% of resumes.**

### Day 1 — Git aliases that change your life (30 min)

Add these to `~/.gitconfig`:

- [ ] `lg` — pretty log graph
- [ ] `st` — short status
- [ ] `co` — checkout
- [ ] `br` — branch
- [ ] `cm` — commit
- [ ] `cma` — commit --amend
- [ ] `ri` — rebase --interactive
- [ ] `unstage` — reset HEAD --
- [ ] `last` — log -1 HEAD

Then **commit your dotfiles config to a separate `dotfiles` repo** (you'll thank yourself later when you set up a new machine).

### Day 2 — Ship `pulse-check.sh` (3 hrs)

This is the seed of Pulse. It will live in `scripts/` forever and the Python worker in Week 6 will replace it. But for now, bash.

Requirements:
- [ ] Takes a URL as argument
- [ ] Optionally takes `--timeout=N`, `--expected-status=N` flags
- [ ] Curls the URL, measures response time
- [ ] Outputs **JSON** to stdout (so it composes with other tools): `{"url": "...", "status": 200, "duration_ms": 142, "timestamp": "2026-..."}`
- [ ] Exits 0 on success, 1 on failure, 2 on misuse
- [ ] Has `--help`
- [ ] Uses `set -euo pipefail` at the top
- [ ] Has a `# tested manually with:` block at the bottom listing 4 test cases
- [ ] **Commit:** `feat(scripts): add pulse-check.sh for HTTP monitoring`

### Day 3 — Ship `repo-stats.sh` (2 hrs)

A script that introspects a git repo. You'll use this on Pulse itself by Week 16 to write the "what I built" blog post.

Requirements:
- [ ] Run inside any git repo, produces a summary
- [ ] Total commits, top 5 contributors, longest commit streak
- [ ] Files changed most (`git log --name-only | sort | uniq -c | sort -rn | head`)
- [ ] Lines added/removed (use `git log --shortstat` + awk)
- [ ] **Use only:** `git`, `awk`, `sort`, `uniq`, `head`, `cut` — no Python, no jq
- [ ] **Commit:** `feat(scripts): add repo-stats.sh`

### Day 3 — Practice `git bisect` (1 hr)

This skill alone separates senior devs from mid-level. Most engineers have never used it.

- [ ] Create a branch `practice/bisect`
- [ ] Make 15 commits, each modifying `scripts/pulse-check.sh`
- [ ] In commit #7, deliberately introduce a bug (wrong exit code)
- [ ] Switch to `main`, then use `git bisect` to find which commit broke it
- [ ] Document the session in `weeks/week01-bisect-log.md` — show the actual terminal output
- [ ] **Commit:** `docs(week01): bisect practice session`

### Day 4 — Practice `git rebase -i` (1 hr)

- [ ] On `practice/bisect`, use `git rebase -i HEAD~10`
- [ ] Squash 3 commits into 1
- [ ] Reorder 2 commits
- [ ] Reword a commit message
- [ ] Drop one commit entirely
- [ ] Document what you did in `weeks/week01-rebase-log.md`
- [ ] **Commit:** `docs(week01): rebase practice`

### End of week — Reflection (30 min)

- [ ] Write `weeks/WEEK01-REFLECTION.md`. 200 words, honest. Format:
  - **Hardest moment this week**
  - **Aha moment this week**
  - **What I would tell past-me on Monday**
  - **What I'm not yet confident about**
- [ ] Update root `README.md` progress table: Week 1 → ✅
- [ ] **Final commit of the week:** `docs: complete week 1`

---

## 🎯 End-of-week deliverable

Your repo should now have:

```
pulse/
├── README.md
├── ROADMAP.md
├── LICENSE
├── .gitignore
├── scripts/
│   ├── pulse-check.sh
│   └── repo-stats.sh
└── weeks/
    ├── WEEK01.md
    ├── WEEK01-REFLECTION.md
    ├── week01-bisect-log.md
    └── week01-rebase-log.md
```

Minimum **10 signed commits** with conventional commit messages, pushed to a public repo.

---

## 🌉 Bridge to Week 2

Week 2 builds directly on this week:

- `pulse-check.sh` gets hardened — proper error handling for DNS failures, timeouts, SSL errors. You'll write **test cases** for it using a tiny bash test framework.
- You'll add **`scripts/find-stale.sh`** — uses `find -exec` and `xargs` to find log files older than N days. This becomes the cleanup job in Week 14.
- Pre-commit hooks: every commit will run `shellcheck` on your bash scripts and reject commits with conventional-commit violations.
- You'll get fluent in `awk` and `sed`. By Friday of Week 2, you'll be able to write one-liners that take 50 lines of Python.

---

## 🚫 Anti-checklist (what NOT to do this week)

- ❌ Don't start learning Python debugging "early"
- ❌ Don't install Docker
- ❌ Don't read about FastAPI
- ❌ Don't watch DevOps YouTube videos
- ❌ Don't sign up for any new course
- ❌ Don't perfect-polish the scripts. **Shipped > perfect.** You'll refactor in Week 2.

---

## 🆘 If you get stuck

- **GPG signing on Windows**: Use Git Bash + Gpg4win. If it's painful, defer signing to Day 2 — don't let it block the rest.
- **Bash on Windows**: Use WSL2 (Ubuntu). Native Windows bash is a worse experience.
- **Stuck on a script for >45 minutes**: Commit what you have with `wip:` prefix, move on, come back fresh. Stuck time is wasted time.

---

## 📝 Daily commit log (fill this in as you go)

| Day | Date | Hours | Commits | Notes |
| --- | ---- | ----- | ------- | ----- |
| Mon | | | | |
| Tue | | | | |
| Wed | | | | |
| Thu | | | | |
| Fri | | | | |
| Sat | | | | |
| Sun | | | | |
