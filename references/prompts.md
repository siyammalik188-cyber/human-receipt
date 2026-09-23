# Prompts (copy and paste)

Use with any model. Fill the brackets. Delete unused lines.

---

## Spec (always start here)

```text
Follow human-receipt. Do not write application code yet.

Goal: <what done looks like>
Context: <stack, files, constraints>
Do: <exact task>
Don’t: <scope limits>
Output: a plan with assumptions, slices, what we will not build, rollback, and how we will verify
Done when: <tests / checks that must pass>
```

---

## Implement one slice

```text
Follow human-receipt.

Implement only this slice: <one sentence>
Files you may touch: <paths>
Match existing patterns in this repo. Smallest diff. No renames, no extra helpers, no drive-by formatting.
Done when: <command or test that must pass>
```

---

## Bug — evidence first

```text
Follow human-receipt. Do not patch yet.

Symptom:
What I already tried:
Full error / stack trace:

Actual input:
Actual output / DB row:

Do not guess. Quote the lines involved. Name the first frame that is our code.
Then list 3 theories and the 3 log lines or checks that would prove which is true.
```

---

## Bug — smallest fix

```text
Follow human-receipt.

Repro: <how to see it fail>
Failing input: <exact>
Fix only the root cause. Minimum hunk. No refactors.
Add or update a test that would have caught this.
Then run: <test command>
```

---

## Hostile review

```text
You are a hostile reviewer. Follow human-receipt.

Break this diff.
List: wrong or invented APIs, race conditions, auth/injection/secrets,
silent failures, extra scope, timezone/encoding/money/null bugs.
Only claims you can point to a line for.
Then fix only the real ones. Do not restyle.
```

---

## Shrink the diff

```text
Reduce this diff. No renames. No formatting. No extra helpers.
What is the minimum hunk that still fixes it?
```

---

## Architecture / “what would have to be true?”

```text
Don’t write code.
List assumptions. Mark each: confirmed / unknown / dangerous.
What would have to be true for this feature to be a 20-line change?
What can we not build and still win?
Rollback in 5 lines.
Napkin math if scale was mentioned.
```

---

## Premortem

```text
It is 6 months later. This blew up in production.
Write the story of why (auth, data, retries, migrations, ownership).
Turn the top 5 failures into constraints for the plan.
No implementation yet.
```

---

## Teach-back (before you ship)

```text
Explain this change as if I have to on-call it tonight.
What can go wrong? How do I see it? How do I undo it?
```

---

## Ticket that a stranger (or a model) can do

```text
Context:
Repro / current behavior:
Expected:
Not expected / out of scope:
Files / area:
Done when:
```
