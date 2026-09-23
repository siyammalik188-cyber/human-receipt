# human-receipt

The human part of getting results with AI — especially at coding.

AI can type. You still have to **think, specify, verify, and be accountable.**

This repo is an **[Agent Skill](https://agentskills.io/specification)** you can install, plus plain checklists and prompts you can use in any chat.

| You are… | Start here |
|---|---|
| Installing for Claude Code / Cursor / Codex | [Install](#install-every-step) |
| Using any AI chat (no install) | [Use without installing](#use-without-installing) |
| Want the full skill catalog | [references/catalog.md](./references/catalog.md) |
| Want the overlooked 10x skills | [references/underrated.md](./references/underrated.md) |

---

## What’s inside

```text
human-receipt/
├── SKILL.md                  ← agent instructions (the skill)
├── README.md                 ← you are here
├── LICENSE
├── assets/
│   └── prompt-skeleton.txt   ← copy-paste starter
└── references/
    ├── catalog.md            ← every type of skill
    ├── underrated.md         ← skills people skip
    ├── prompts.md            ← ready-to-use prompts
    └── checklists.md         ← every necessary step
```

---

## Install (every step)

The folder name must stay `human-receipt` so it matches the skill `name`.

### 1. Claude Code — your user (all projects)

```bash
mkdir -p ~/.claude/skills
git clone --depth 1 https://github.com/siyammalik188-cyber/human-receipt.git ~/.claude/skills/human-receipt
```

Restart Claude Code, or start a new session.

**Check:** you should have `~/.claude/skills/human-receipt/SKILL.md`.

**Use:** ask *“follow human-receipt”* or just start a coding task — the agent should pick it up from the description.

**Update later:**

```bash
git -C ~/.claude/skills/human-receipt pull
```

### 2. Claude Code — this project only

From the repo you are working on (not this skill repo):

```bash
mkdir -p .claude/skills
git clone --depth 1 https://github.com/siyammalik188-cyber/human-receipt.git .claude/skills/human-receipt
```

Commit `.claude/skills/human-receipt` if the whole team should get it, **or** add that path to `.gitignore` and document the clone command. Do not commit secrets; this skill has none.

### 3. Cursor

```bash
mkdir -p .cursor/skills
git clone --depth 1 https://github.com/siyammalik188-cyber/human-receipt.git .cursor/skills/human-receipt
```

### 4. OpenAI Codex / other agents that read Agent Skills

Try, in order, whichever your tool documents:

```bash
# project
mkdir -p .agents/skills
git clone --depth 1 https://github.com/siyammalik188-cyber/human-receipt.git .agents/skills/human-receipt

# user-level Codex
mkdir -p ~/.codex/skills
git clone --depth 1 https://github.com/siyammalik188-cyber/human-receipt.git ~/.codex/skills/human-receipt
```

If your agent wants a different folder, copy the **whole** `human-receipt` directory (it must contain `SKILL.md`).

### 5. GitHub Copilot (VS Code / coding agent)

```bash
mkdir -p .github/skills
git clone --depth 1 https://github.com/siyammalik188-cyber/human-receipt.git .github/skills/human-receipt
```

### 6. Manual copy (no git)

1. Download this repo as ZIP from GitHub.
2. Unzip.
3. Rename the folder to `human-receipt` if it is not already.
4. Move it into your agent’s skills directory (see above).
5. Confirm `SKILL.md` is directly inside `human-receipt/`.

### Install check

A correct install looks like this:

```text
…/skills/human-receipt/SKILL.md
…/skills/human-receipt/references/checklists.md
```

Wrong: `…/skills/human-receipt/human-receipt/SKILL.md` (extra nesting).
If that happens, move the inner folder up one level.

---

## Use without installing

Works in ChatGPT, Claude.ai, Gemini, or any model.

### Every necessary step (human loop)

1. **Think 2 minutes.** Who is blocked? What’s the symptom? What did you already try?
2. **Fill the skeleton** from [`assets/prompt-skeleton.txt`](./assets/prompt-skeleton.txt) (also below).
3. **Ask for a plan, not code.** Challenge it: *what can we not build and still win?*
4. **Approve one slice.** One goal. Name the files it may touch.
5. **Run the result yourself.** Happy path + one ugly case.
6. **Read the diff.** If it renamed/reformatted unrelated code, send it back.
7. **Hostile pass.** Paste the [attack prompt](./references/prompts.md#hostile-review).
8. **Ship only when the [after-change checklist](./references/checklists.md) is green.**

### Prompt skeleton (paste this)

```text
Follow human-receipt.

Goal: <what done looks like>
Context: <stack, files, constraints>
Do: <exact task>
Don’t: <scope limits>
Output: <format>
Done when: <tests / checks that must pass>
```

More templates: [`references/prompts.md`](./references/prompts.md).

---

## After every AI change (print this)

Copy from [`references/checklists.md`](./references/checklists.md) or run down this:

- [ ] Compiles / typechecks
- [ ] Tests exist, were read, and pass
- [ ] Happy path run by a human
- [ ] One ugly edge case tried
- [ ] Diff is only what was asked
- [ ] No secrets in the change
- [ ] Rollback is obvious
- [ ] I would own this at 2am

**Shipped** = merged + migrated + observable + reversible + someone else can run it.

---

## The 12 skills that move the needle

1. Define done in one sentence.
2. Split the problem.
3. Give constraints and examples.
4. Ask for a plan first.
5. Implement in thin slices.
6. Run the code.
7. Write or generate tests, then read them.
8. Review the diff like a senior.
9. Check docs for any API you don’t know.
10. Hunt for security and edge cases.
11. Commit small, reversible steps.
12. Write down what you learned.

Overlooked skills (data, smallest diff, napkin math, saying no): [`references/underrated.md`](./references/underrated.md).

---

## Weekly 15-minute drill

Pick one AI change you shipped this week:

1. Could the diff have been half the size?
2. Did I look at real data or trust the story?
3. Is there an invariant, or only a happy-path test?
4. Can I roll it back?
5. What name did we get wrong?
6. What should we have refused to build?

Write five lines. Taste is built by review, not by generating more.

---

## License

[MIT](./LICENSE). Use it, copy it, teach it.

*Receipt of the human part: see → shrink → check → cut → finish.*
