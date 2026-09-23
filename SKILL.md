---
name: human-receipt
description: Human operating loop for reliable AI coding — spec-before-code, thin slices, evidence-first debugging, smallest diffs, tests, hostile review, and a definition of shipped. Use when writing, reviewing, debugging, or planning code with an AI assistant; when the user mentions human-receipt, AI coding skills, prompting, vibe coding, getting better AI results, or asks to plan then implement.
license: MIT
metadata:
  version: "1.0.0"
  author: human-receipt
---

# Human Receipt

AI can type. The human still has to think, specify, verify, and be accountable.

This skill is the operating loop. Follow it for every coding task. Do not skip to implementation.

Load extra material only when needed:
- Skill catalog (every type): `references/catalog.md`
- Overlooked high-leverage skills: `references/underrated.md`
- Copy-paste prompts: `references/prompts.md`
- Checklists: `references/checklists.md`

## Hard rules

1. Do not write application code until “done” is one sentence and a plan exists.
2. One slice per change. No drive-by refactors, renames, or formatting.
3. Never invent APIs, flags, packages, or files. Verify against the repo and official docs.
4. Do not claim something works unless it was run, or say clearly that it was not run.
5. Prefer deleting and shrinking over adding layers.
6. No secrets, PII, or production credentials in prompts, logs, or commits.
7. You are the author. The human is the reviewer. Make the diff easy to reject.

## The loop (do every step)

### Step 0 — Silence (10–60 seconds)

Restate, in one sentence each:
- Who is blocked
- The symptom or goal
- What was already tried (if a bug)

If you cannot, ask. Do not guess a product.

### Step 1 — Define done

Write:

```text
Done when: <observable result a stranger could check>
Out of scope: <what we will not do>
```

Get agreement if the request is ambiguous. Misalignment is the most expensive bug.

### Step 2 — Evidence (bugs) or constraints (features)

**Bug:** Do not patch yet.
- Full error / stack trace (first frame in *our* code)
- Real input / output / DB row / screenshot — not a paraphrase
- Minimal repro if the failure is large
- Environment vs code (cwd, env, version, permissions)

**Feature:** List constraints: stack, files allowed to touch, compatibility, security, rollback.

If evidence is missing, ask for it or gather it with tools. Do not invent a failing input.

### Step 3 — Plan, not code

Output a short plan:
1. Assumptions (confirmed / unknown / dangerous)
2. Slices (each independently shippable)
3. What we will **not** build
4. Rollback in 5 lines (especially schema, public API, data)
5. How we will verify (command, test, or manual check)

Ask: “What would have to be true for this to be a 20-line change?”
Ask: “What can we not build and still win?”

Wait for a go if the change is a one-way door (schema, public API, encryption, deletion). Two-way doors (copy, local UI, a function) may proceed.

### Step 4 — Implement one slice

- Match existing patterns in this repo. Do not invent a new architecture.
- Smallest diff that works. No extra helpers “for later.”
- Domain names, not `handleData` / `utils` / `manager`.
- Errors must say what failed, which id, what to do next.
- For anything that charges, emails, or writes: say what happens on retry (idempotency).
- Handle missing / empty / `0` / non-ASCII where it matters.

### Step 5 — Verify

Run the relevant checks. Prefer the project’s real commands.

Minimum:
1. Lint / typecheck if the project has them
2. Tests that cover the change — read generated tests, do not trust them unread
3. Happy path actually executed
4. One ugly edge case
5. Diff contains only what was asked

If you cannot run, say so and give the exact commands the human should run.

### Step 6 — Hostile review (before you stop)

Attack your own diff:
- Wrong or hallucinated APIs
- Auth / injection / secrets
- Races, retries, silent catches
- Extra scope
- Timezones, encoding, money, null vs zero

Only claims you can point to a line for. Then fix the real ones — still no restyle.

### Step 7 — Hand off

Report:
- What changed (files + why)
- How to verify (commands)
- What was not done
- Rollback
- Residual risk

Shipped is not “code exists.” Shipped = merged + migrated + observable + reversible + someone else can run it.

## Task switchboard

| User intent | Start at | Extra |
|---|---|---|
| Vague “build X” | Steps 0–3, stop for agreement | `references/prompts.md` → spec |
| Bug / “it doesn’t work” | Step 2 evidence | `references/underrated.md` §§1–5, 35 |
| Review my diff | Step 6 | `references/checklists.md` → after-change |
| Architecture / scale | Napkin math, then plan | `references/underrated.md` §§12, 15–17, 31 |
| “Just fix it fast” | Still 0–2, then smallest slice | Timebox 15 min; if stuck, shrink |
| Learn / explain | Teach back; do not only paste code | `references/catalog.md` |

## Never

- Whole-app generation in one shot
- “This should work” without a run or a caveat
- Fake packages, outdated APIs, invented config keys
- Disabling tests, skipping auth, catching-and-swallowing
- Expanding scope because it “seemed useful”
- Pasting secrets into the session

## Timebox

If 15 minutes of generation is not converging: shrink the slice, write a failing test first, or gather data. Do not keep prompting the same way.

## Default prompt shape (when the human has not given one)

Fill this before coding:

```text
Goal:
Context: (stack, files, constraints)
Do:
Don’t:
Output:
Done when:
```

Full templates: `references/prompts.md`.
Printable checklists: `references/checklists.md`.
