# Skills People Skip — That Quietly 10x Results

> Reference for the **human-receipt** skill. Operating loop: [`../SKILL.md`](../SKILL.md). Prompts: [`prompts.md`](./prompts.md).

The first list was the obvious skills. This is the other list:
skills almost nobody practices, that pay more than another framework.

AI makes these *more* valuable, not less. Models are fluent.
These skills are how you stop fluent nonsense.

Each item: **what it is → why people skip it → how to use it (especially with AI).**

---

## The pattern

People skip skills that feel:
- slow
- boring
- unsexy
- “I already know that”
- invisible when they work

Those are usually the highest-leverage ones.

---

## 1. Look at the data, not the code

**What:** Print the actual payload, row, header, bytes, status. Believe the runtime, not the source.

**Why skipped:** Code *looks* like it should work. Staring at JSON feels like “not programming.”

**How:** Before asking AI to “fix the bug,” paste the real input/output.

```text
Here is the actual request body.
Here is the actual DB row.
Here is the actual error.
Do not guess. Explain what this data implies.
```

Most “logic bugs” are “we never looked at the data.”

---

## 2. Make a minimal reproduction

**What:** Shrink the failure to the smallest script/file that still breaks.

**Why skipped:** It feels like extra work. People dump the whole repo into the model.

**How:** 20 lines that fail beat 2,000 lines of context. AI gets dramatically smarter on a small repro. So do you.

Rule: if you cannot reproduce it in isolation, you do not understand it yet.

---

## 3. Read the entire error

**What:** Full stack trace, first cause, file:line, the warning *above* the crash.

**Why skipped:** People read the last line (“undefined is not a function”) and prompt from that.

**How:** Paste the *whole* trace. Then ask: “What is the first frame that is *our* code?”

The first useful skill in an AI era is still: **read**.

---

## 4. Use a real debugger

**What:** Breakpoints, conditional breakpoints, watch, step into, drop to REPL.

**Why skipped:** Print-and-rerun culture. Also a leftover “debuggers are for weak programmers” myth.

**How:** One run with a breakpoint often beats 15 AI chat rounds. Then *give AI the watched values*.

Conditional breakpoint on `userId === 17` is a superpower.

---

## 5. Instrument before you guess

**What:** Add a log / metric / span at the boundary *first*. Then form a hypothesis.

**Why skipped:** Guessing is faster emotionally. AI is happy to guess with you.

**How:**

```text
Do not fix yet.
Tell me the 3 log lines that would prove which of these 3 theories is true.
```

Guessing + generating patches is how you get two bugs.

---

## 6. git archaeology

**What:** `blame`, `log -p`, `bisect`, “when did this start?”

**Why skipped:** People treat git as save/upload, not a time machine.

**How:**
- `git bisect` for “this used to work”
- `git log -p -- path` before rewriting a file
- Ask AI: “Summarize why this function exists using the commit history. Do not change it until then.”

A lot of “bad code” is load-bearing. History tells you why.

---

## 7. Smallest possible diff

**What:** The change that solves the problem and *nothing else*.

**Why skipped:** AI loves to refactor, rename, “improve,” and touch 14 files.

**How:** After every AI patch, ask:

```text
Reduce this diff. No renames. No formatting. No extra helpers.
What is the minimum hunk that fixes it?
```

Small diffs are easier to review, revert, and trust. This is a senior skill.

---

## 8. Write code that is easy to delete

**What:** Local, boring, copy-paste-ok-until-the-third-time. No premature framework.

**Why skipped:** Nobody brags about deletable code. AI defaults to architecture.

**How:** Prefer a function over a “service.” Prefer a column over an event bus. Ask:

```text
What would make this easy to delete in 3 months?
```

Flexibility you don’t need is a tax.

---

## 9. Solve it upstream (lazy optimization)

**What:** Don’t fix the symptom in your layer if the input should never have been wrong.

**Why skipped:** People own “their file” and patch locally. AI patches locally too.

**How:** Ask: “If we changed the producer / the schema / the button label, would this code even be needed?”

One validation at the edge beats 40 defensive `if`s in the middle.

---

## 10. Code orientation (navigate, don’t wander)

**What:** Jump-to-def, find-references, fuzzy file open, search by symbol, grep like you mean it.

**Why skipped:** It looks like “just using the editor.” Seniors look telepathic because navigation is cheap for them.

**How:** Before prompting, spend 90 seconds finding the *real* call site. Feed AI that file, not the whole tree.

Energy spent navigating is energy not spent thinking. Lower the tax.

---

## 11. The boring correctness cluster

These four create an absurd share of production incidents. Almost nobody drills them.

| Skill | The trap |
|---|---|
| **Timezones / DST** | “Just store local time” |
| **Unicode / encoding** | names, emoji, RTL, NFC vs NFD |
| **Money / decimals** | floats for currency |
| **Null vs empty vs zero vs missing** | `0`, `""`, `null`, `[]`, absent key |

**How:** Keep a personal checklist. Force AI to answer them explicitly:

```text
How does this handle: missing field, empty string, 0, DST, and non-ASCII names?
```

Unsexy. Extremely expensive when ignored.

---

## 12. Back-of-the-envelope math

**What:** 10-second arithmetic: rows × bytes, requests × latency, users × storage.

**Why skipped:** Feels imprecise. People jump to Redis / Kafka / “we’ll scale it.”

**How:** Before any performance prompt:

```text
100k users, 20 req/day, 2 KB payload. Is this even a problem?
Show the napkin math. Then recommend.
```

Most “scale” work is vanity. Napkin math is a taste filter.

---

## 13. Read the schema like a map

**What:** Know tables, keys, nullability, indexes, who writes what. Not just “the ORM.”

**Why skipped:** ORMs hide it. AI writes queries that *look* fine and scan 8 million rows.

**How:** Paste `\d table` / `EXPLAIN` / migration files. Ask for the query plan in words.

If you understand the data model, you can reject 80% of bad backend designs in one glance.

---

## 14. Unix text skill

**What:** `rg`, `jq`, `sort | uniq -c`, `awk`, `cut`, `head`, pipes.

**Why skipped:** GUIs and chat. Feels old.

**How:** 30 seconds of `jq '.items[] | .id'` on a production log often beats a 10-minute AI investigation.

This is still the fastest way to *see*. Seeing beats prompting.

---

## 15. “What would have to be true?”

**What:** Invert the problem. Instead of “how do we do X,” ask “what must be true for X to be easy / unnecessary?”

**Why skipped:** People (and models) jump to implementation.

**How:**

```text
Don’t write code.
List assumptions. Mark each: confirmed / unknown / dangerous.
What would have to be true for this feature to be a 20-line change?
```

This is architecture in one question.

---

## 16. Premortem (fail it on purpose, on paper)

**What:** “It is 6 months later. This blew up. Write the story of why.”

**Why skipped:** Feels negative. Teams want momentum.

**How:** Do it *before* you let AI generate the system.

You’ll hear: auth was bolted on, migrations were irreversible, the queue had no poison-pill handling, nobody owned retries.

Then make those the constraints in the prompt.

---

## 17. Write the rollback first

**What:** How do we undo this if it ships broken? Feature flag, dual-write, expand/contract migration.

**Why skipped:** Shipping feels like the finish line. AI generates the forward path only.

**How:** “No implementation until you describe rollback in 5 lines.”

If you cannot undo it, you are not done designing it.

---

## 18. Invariants, not just tests

**What:** Name the thing that must *always* be true. Assert it. In code, in types, in the DB.

**Why skipped:** Tests check examples. Invariants check laws. People only write examples.

**How:**

```text
State 5 invariants of this module.
Put the cheapest ones in the type system or DB constraints.
Then write tests for the rest.
```

Example: “a refund cannot exceed captured amount.” That’s a law, not a unit test.

---

## 19. Ask the AI to attack its own work

**What:** Red-team pass. Not “any issues?” — that’s too soft.

**Why skipped:** One-shot satisfaction. The first answer feels complete.

**How:** Use a second prompt, even a second model:

```text
You are a hostile reviewer.
Break this.
List: wrong APIs, race conditions, auth holes, silent failures, extra scope.
Only claims you can point to a line for.
```

Then: “Fix only the real ones. Do not restyle.”

---

## 20. Evidence-first (don’t fix ghosts)

**What:** Confirm the bug exists in *this* codebase, today, before changing anything.

**Why skipped:** AI will “fix” things that were never broken, and “improve” working code.

**How:**

```text
Before changing code:
1. Quote the exact lines involved.
2. Show a failing input.
3. If you cannot, say you cannot.
No drive-by cleanups.
```

Truth-first is slower for one minute and faster for the rest of the week.

---

## 21. “What breaks if we remove this?”

**What:** Understand a system by deletion, not by reading.

**Why skipped:** Reading feels productive. Deletion feels scary.

**How:** Ask AI *and* yourself: “If we deleted this function, what user-visible thing dies? If nothing, why is it here?”

Great for AI-generated layers of helpers nobody needed.

---

## 22. Finish

**What:** Close the loop: tests, docs, flag off, monitoring, ticket, revert plan. Ship.

**Why skipped:** Starting is dopamine. 90% done is the default state of AI projects.

**How:** Keep a “definition of shipped,” not a definition of coded.

```text
Shipped = merged + migrated + observable + reversible + someone else can run it.
```

Unfinished work has negative value. It rots.

---

## 23. Silence before the prompt

**What:** 2–5 minutes of thinking with no model. Write the problem in one sentence. Then prompt.

**Why skipped:** Chat is right there. Typing feels like progress.

**How:** If you cannot state:
- the user
- the symptom
- what you already tried
you are not ready to spend tokens.

The quality of the prompt is the quality of the thought *before* the prompt.

---

## 24. Write the ticket so a stranger could do it

**What:** Context, repro, expected, not-expected, out of scope.

**Why skipped:** “I’ll explain in standup.” Then you paste a vague wish into AI.

**How:** The ticket *is* the prompt. If a junior (or a model) would have to ask 8 questions, the ticket is not done.

This one skill upgrades every teammate and every agent.

---

## 25. Say no / kill work

**What:** Cut the feature. Cut the abstraction. Cut the extra endpoint.

**Why skipped:** Agreeableness. Sunk cost. AI will build whatever you hint at.

**How:** After every plan:

```text
What can we not build and still win?
Delete half the plan. What remains?
```

The best engineers are editors.

---

## 26. Time-to-feedback

**What:** Shorten the loop: save → see result. Tests in 2s beat tests in 2min. Local fixture beat staging.

**Why skipped:** People optimize the algorithm instead of the wait.

**How:** Ask: “What is the slowest step between change and knowledge?” Attack *that*.

AI + a 5-minute test suite is still slow. A 3-second test you actually run is fast.

---

## 27. Make the right thing easy

**What:** Defaults, linters, generators, paved paths. Don’t rely on memory or virtue.

**Why skipped:** Docs that say “please remember to…” lose to humans and to agents.

**How:** Encode the rule where it cannot be ignored: types, CI, a template, a pre-commit hook.

If AI is on your team, **the repo’s rails matter more than the prompt.**

---

## 28. Error messages as product

**What:** Write failures for the next human (often you, at 2am).

**Why skipped:** Happy path gets the polish. AI writes `Error: something went wrong`.

**How:** Demand:

```text
Every throw/log includes: what failed, which id, what to do next.
No generic catch.
```

A good error is a miniature runbook.

---

## 29. Talk to the user (or the ticket, or support)

**What:** The real constraint lives in a sentence a user already said.

**Why skipped:** Building is more fun than listening. AI will invent a user.

**How:** Paste 5 real support messages before designing. Ask: “What are they actually blocked on?”

Half of “engineering work” is a wording, an empty state, or a missing export.

---

## 30. Checklists under stress

**What:** When tired or on fire, you do not rise to your skill. You fall to your checklist.

**Why skipped:** Checklists feel junior. Seniors think they’ll remember.

**How:** Keep a tiny personal one:

1. Repro
2. Data
3. Trace
4. Hypothesis
5. Smallest fix
6. Test
7. Diff
8. Rollback

Run it *especially* when using AI during an incident. Incidents + vibes = outages.

---

## 31. One-way vs two-way doors

**What:** Some decisions are reversible (library, UI copy). Some are not (schema, public API, encryption, data deletion).

**Why skipped:** Everything is treated as equally “we can change it later.”

**How:** Label the door before you prompt. Slow down only for one-way doors. Let AI go fast on two-way doors.

This is how seniors use AI without being reckless.

---

## 32. Mechanical sympathy

**What:** A rough picture of what the machine actually does: disk vs memory, N+1, serialization, GC, indexes.

**Why skipped:** High-level frameworks. “The cloud will handle it.”

**How:** When AI suggests a clever approach, ask: “How many times does this touch the network/disk per request?”

You don’t need to write assembly. You need to smell an extra 10,000 queries.

---

## 33. Copy a working system

**What:** Steal a known-good pattern from a codebase that already survived production.

**Why skipped:** Originality bias. AI invents a unique architecture every time.

**How:** “Match the existing payment flow in `billing/`. Do not invent a new pattern.”

Boring and copied beats novel and yours.

---

## 34. Notes in the moment of confusion

**What:** When you go “wait, that’s weird” — write it down *then*, not after.

**Why skipped:** You’ll remember. You won’t.

**How:** A running `gotchas.md` or a comment `// surprising: refunds can be 0`. Future prompts get these as context. This is compound interest.

Confusion is a leading indicator. Capture it.

---

## 35. Environment vs code

**What:** Before blaming logic: Node version, cwd, `.env`, clock, permissions, the *other* Docker network.

**Why skipped:** We assume the bug is in the function. AI assumes that too.

**How:** “List environment reasons this could fail even if the code is correct.” Then check those in 2 minutes.

Hours are lost debugging code that never ran.

---

## 36. Naming as design

**What:** The name *is* the model. `processData` vs `capturePaymentAfter3DSecure`.

**Why skipped:** “We’ll rename later.” AI loves `handleData`, `utils`, `manager`.

**How:** Spend the extra 30 seconds. Then tell AI: “Do not invent new nouns. Use these domain words: …”

Bad names make every future prompt worse, because the model learns your muddled language.

---

## 37. Idempotency as a habit

**What:** Can I run this twice? Retry? Double-click? Webhook replay?

**Why skipped:** Happy-path demos. AI writes `create()` as if the network is perfect.

**How:** For anything that charges, emails, or writes: “What happens on retry? What’s the idempotency key?”

This one question prevents a class of million-dollar bugs.

---

## 38. Alignment before speed

**What:** Same picture of done, in writing, with the human (or with yourself tomorrow).

**Why skipped:** Coding is more comfortable than clarifying.

**How:** One paragraph. Get a yes. *Then* open the model.

Misalignment is the most expensive bug, and tests cannot catch it.

---

## 39. Teaching it back

**What:** Explain the change out loud / in a comment / to a junior / to the model.

**Why skipped:** “I get it.” Understanding that can’t be spoken is fake.

**How:** After an AI patch: “Explain this to me as if I have to on-call it tonight.” If *you* can’t, you don’t ship it.

This also fights skill atrophy from letting the model do all the thinking.

---

## 40. Do nothing (strategic neglect)

**What:** Some bugs are not worth fixing. Some features should wait. Some prompts should not be sent.

**Why skipped:** Action bias. Tools invite use.

**How:** “Cost of delay vs cost of a wrong fix?” If you cannot say why this must exist this week, don’t generate it.

Restraint is a skill. AI has none unless you do.

---

## 12 most ignored, highest payoff

If you only steal a few:

1. Look at the real data.
2. Minimal repro.
3. Full stack trace.
4. Debugger + values, not vibes.
5. Smallest diff.
6. Easy-to-delete code.
7. Napkin math.
8. Premortem + rollback.
9. Attack your own solution.
10. Finish (observe + reverse).
11. Silence before prompting.
12. Say no.

---

## A 15-minute weekly drill

Pick one shipped AI change from this week and run:

1. Could the diff have been half the size?
2. Did I look at real data or trust the story?
3. Is there an invariant, or only a happy-path test?
4. Can I roll it back?
5. What name did we get wrong?
6. What should we have refused to build?

Write 5 lines. That’s the practice. Taste is built by review, not by generating more.

---

## Why these beat “learn another framework”

Frameworks expire. These don’t.

They work on:
- any language
- any model
- any team
- production at 2am

AI made typing cheap.
These skills are how cheap typing becomes *good results*.

---

*The human receipt for skipped work: the unsexy loop — see, shrink, check, cut, finish.*
