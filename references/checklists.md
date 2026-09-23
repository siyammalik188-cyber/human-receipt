# Checklists — every necessary step

Print these. Use them when tired. You will not remember.

---

## A. Before you prompt

- [ ] I can say who is blocked in one sentence
- [ ] I can say what “done” looks like in one sentence
- [ ] I know what is **out of scope**
- [ ] I have the real error / input / file paths (not a vibe)
- [ ] I will ask for a **plan first**, not a whole app
- [ ] No secrets or PII will go into the prompt

---

## B. The coding loop

1. [ ] **Done** written
2. [ ] **Plan** written (slices, won’t-build, rollback, verify)
3. [ ] **One slice** implemented
4. [ ] **Ran** it (or recorded the exact command I still must run)
5. [ ] **Tests** added or updated — and I read them
6. [ ] **Diff** reviewed — only what I asked
7. [ ] **Hostile pass** done
8. [ ] **Commit** small and reversible
9. [ ] Repeat from 3 until done

If stuck 15 minutes: shrink the slice, write a failing test, or look at data. Do not keep prompting the same way.

---

## C. After every AI change

- [ ] Compiles / typechecks
- [ ] Tests exist, were read, and pass
- [ ] Happy path run by a human
- [ ] One ugly edge case tried
- [ ] Diff is only what was asked (no drive-by refactor)
- [ ] APIs / packages exist in *this* repo or official docs
- [ ] No secrets in the change
- [ ] Errors say what / which id / what next
- [ ] Retry / double-submit is safe if this writes, emails, or charges
- [ ] Rollback is obvious
- [ ] I would own this at 2am

---

## D. Definition of shipped

Not shipped: “the code exists.”

Shipped:

- [ ] Merged (or equivalent)
- [ ] Migrated (if schema)
- [ ] Observable (log, metric, or trace I can find)
- [ ] Reversible (flag, revert, expand/contract)
- [ ] Someone else can run it

---

## E. Incident / “it’s on fire”

1. [ ] Repro
2. [ ] Data (payload, row, header)
3. [ ] Full trace
4. [ ] Hypothesis (written)
5. [ ] Smallest fix
6. [ ] Test
7. [ ] Diff
8. [ ] Rollback known

Do **not** vibe-fix production with a freeform chat.

---

## F. Boring correctness (surprisingly expensive)

- [ ] Timezones / DST
- [ ] Unicode / encoding / names
- [ ] Money — no floats
- [ ] Null vs empty vs `0` vs missing key
- [ ] Idempotency (retry, webhook replay, double-click)

---

## G. Weekly 15-minute drill

Pick one shipped AI change:

1. Could the diff have been half the size?
2. Did I look at real data or trust the story?
3. Is there an invariant, or only a happy-path test?
4. Can I roll it back?
5. What name did we get wrong?
6. What should we have refused to build?

Write five lines.

---

## H. Install check (this skill)

- [ ] Folder is named `human-receipt`
- [ ] `SKILL.md` is **directly** inside that folder
- [ ] `references/` and `assets/` came along
- [ ] Agent session restarted after copy
- [ ] A test ask: “follow human-receipt and define done for X”
