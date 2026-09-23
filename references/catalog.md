# Human Receipt: Skills That Make AI Actually Work

> Reference for the **human-receipt** skill. Operating loop: [`../SKILL.md`](../SKILL.md). Checklists: [`checklists.md`](./checklists.md).

AI is not a substitute for skill. It multiplies the skills you already have.
The people getting the best results are not “better at ChatGPT.” They are
better at thinking, specifying, checking, and shipping.

This is a complete skill list — every type that matters if you want
reliable results, especially in coding.

---

## 1. Thinking Skills (the real multiplier)

These decide whether AI produces gold or garbage.

| Skill | Why it matters with AI |
|---|---|
| **Problem framing** | Name the real problem, not the first idea. Bad frame = wasted hours. |
| **Decomposition** | Break work into small, testable pieces AI can actually finish. |
| **Abstraction** | See patterns so you can reuse prompts, templates, and architecture. |
| **First-principles thinking** | Don’t accept AI’s first answer. Ask *why* it should work. |
| **Tradeoff thinking** | Speed vs quality, simple vs flexible, now vs later. AI defaults to “more.” |
| **Constraint setting** | Limits (time, stack, style, security) make AI sharper. |
| **Mental models** | Input/output, state, layers, failure modes. AI follows your model. |
| **Systems thinking** | Code lives in a system: users, data, deploy, cost, support. |
| **Prioritization** | Tell AI what matters *now*. Otherwise it builds the wrong 80%. |
| **Ambiguity tolerance** | You will not have full specs. You must still move, then tighten. |

**Use it:** Before prompting, write one sentence: *What must be true when this is done?*

---

## 2. Communication & Prompting Skills

Talking to AI is a professional skill, not magic words.

| Skill | What “good” looks like |
|---|---|
| **Clarity** | One goal per request. No mixed tasks. |
| **Specificity** | Stack, files, inputs, outputs, edge cases, “don’t do this.” |
| **Context packing** | Give the smallest useful context: relevant files, errors, constraints. |
| **Role setting** | “You are a senior backend engineer reviewing for security…” |
| **Examples (few-shot)** | Show 1–3 good/bad samples. AI copies structure better than description. |
| **Output contracts** | “Return only a patch.” “JSON with fields X,Y.” “No extra prose.” |
| **Iterative prompting** | Draft → critique → tighten. Don’t expect one-shot perfection. |
| **Question design** | Ask AI to interview *you* when the spec is fuzzy. |
| **Negative constraints** | “Don’t invent APIs. Don’t refactor unrelated files.” |
| **Rubrics** | Give a grading checklist AI must satisfy before it stops. |

**Prompt skeleton that works for coding:**

```text
Goal: <what done looks like>
Context: <stack, files, constraints>
Do: <exact task>
Don’t: <scope limits>
Output: <format>
Done when: <tests / checks that must pass>
```

---

## 3. Coding Skills (every type)

AI writes code. You still need to *direct, judge, and own* it.

### 3.1 Computer science fundamentals
- Data structures (arrays, maps, trees, graphs, queues)
- Algorithms (search, sort, traversal, recursion, complexity)
- Time/space complexity (Big-O) so you can reject slow “clever” code
- Memory, pointers/references, stack vs heap (even in high-level languages)
- Concurrency basics (race conditions, locks, async, deadlocks)
- Networking (HTTP, TCP, DNS, REST, WebSockets, auth headers)
- Databases (indexes, transactions, normalization, N+1 queries)
- Operating systems (processes, files, env vars, permissions)
- Discrete math / logic (boolean algebra, sets, graphs) for correct conditions

### 3.2 Programming language skill
- Syntax + idioms of *your* main language
- Type systems (static vs dynamic, generics, null safety)
- Error handling patterns
- Standard library fluency (don’t reinvent)
- Package/module systems
- Language-specific pitfalls (JS `this`, Python mutability, Go zero values)

**Rule:** You don’t need to type every line. You *do* need to read every line you ship.

### 3.3 Software design
- Naming that matches domain language
- Functions with one job
- Separation of concerns
- DRY vs WET (don’t over-abstract because AI loves abstractions)
- SOLID, enough to smell violations
- API design (resources, errors, versioning, idempotency)
- Data modeling
- State machines for workflows
- Design patterns *when they earn their complexity*

### 3.4 Architecture
- Layered / hexagonal / modular monolith / microservices — pick on purpose
- Sync vs async
- Caching and invalidation
- Event-driven vs request/response
- AuthN / AuthZ boundaries
- Multi-tenancy
- Observability as a first-class concern
- Cost and scale assumptions

### 3.5 Frontend
- HTML semantics, accessibility (a11y)
- CSS layout (flex, grid), responsive design
- Component thinking
- State management
- Forms, validation, UX empty/error/loading states
- Performance (bundle size, render cost)
- Design taste: spacing, hierarchy, contrast

### 3.6 Backend
- HTTP APIs, status codes, pagination
- Auth (sessions, JWT, OAuth, API keys)
- Validation and sanitization
- Background jobs / queues
- File storage
- Rate limiting
- Idempotency and retries

### 3.7 Data
- SQL (joins, indexes, EXPLAIN)
- Schema design and migrations
- ETL / pipelines
- Analytics vs OLTP
- Data quality and lineage
- Privacy (PII handling)

### 3.8 DevOps / platform
- Git (branching, rebase vs merge, bisect)
- CI/CD
- Docker / containers
- Linux CLI
- Env config and secrets
- Logging, metrics, tracing
- Deploy + rollback
- Infra as code (enough to review)

### 3.9 Quality
- Unit / integration / e2e testing
- Test design (arrange-act-assert, fixtures, fakes vs mocks)
- Property-based and edge-case thinking
- Debugging (repro, isolate, hypothesize, verify)
- Profiling and performance budgets
- Code review (you are the reviewer; AI is the author)

### 3.10 Security
- OWASP Top 10 (XSS, SQLi, CSRF, SSRF, IDOR, auth flaws)
- Secrets never in source
- Least privilege
- Input validation + output encoding
- Dependency risk
- Threat modeling (who can do what to whom)

### 3.11 Product-adjacent coding
- Reading tickets / writing tickets
- Estimating and slicing MVPs
- Feature flags
- Analytics events
- Error messages humans can use
- Backward compatibility

---

## 4. Verification Skills (this is where most people fail)

AI is fluent and confident. Fluency ≠ correctness.

| Skill | Practice |
|---|---|
| **Skepticism** | Assume the first draft is wrong in a small, expensive way. |
| **Reading code** | Trace data in, data out. Don’t skim. |
| **Reproducing bugs** | “Show me the failing input.” |
| **Writing tests first or immediately after** | If you can’t test it, you don’t understand it. |
| **Running the code** | Always execute. Never trust a “this should work.” |
| **Diff review** | Read every changed line. Watch for drive-by refactors. |
| **Rubber-duck the AI** | Make it explain *why*, then try to break the explanation. |
| **Source checking** | For APIs/libraries: verify against official docs, not memory. |
| **Hallucination hunting** | Fake packages, fake flags, fake methods, outdated APIs. |
| **Security pass** | Auth, injection, secrets, user-controlled paths. |
| **Rollback thinking** | If this ships and explodes, can we undo it? |

**Done checklist for any AI-written change:**
1. Does it compile / typecheck?
2. Do tests exist and pass?
3. Did I run the happy path myself?
4. Did I try one ugly edge case?
5. Is the diff only what I asked for?
6. Would I be okay owning this at 2am?

---

## 5. Workflow Skills (how professionals use AI)

| Skill | How to use it |
|---|---|
| **Spec before code** | 10 lines of acceptance criteria beat 200 lines of hoping. |
| **Tight loops** | Small prompt → run → fix → next. Not “build the whole app.” |
| **Repo literacy** | Know the file tree, conventions, scripts, tests. Feed AI the right files. |
| **Search skill** | Docs, GitHub issues, Stack Overflow, RFCs — AI is not the only source. |
| **Tooling** | Debugger, profiler, linter, formatter, typechecker, git, HTTP client. |
| **Editor mastery** | Multi-cursor, search/replace, jump-to-def. AI + editor > AI alone. |
| **Version control hygiene** | Atomic commits, good messages, never commit secrets. |
| **Issue tracking** | One change, one reason. Link PR to problem. |
| **Timeboxing** | If AI is stuck 15 minutes, change strategy (smaller slice, write a test). |
| **Knowledge capture** | Save prompts, ADRs, runbooks. Future-you is a user. |

**A strong daily loop:**
1. Define “done”
2. Ask AI for a plan (not code)
3. Challenge the plan
4. Implement one slice
5. Run tests
6. Review diff
7. Commit
8. Repeat

---

## 6. Learning Skills (you must keep getting sharper)

AI makes learning faster *if* you use it as a tutor, not a crutch.

- **Deliberate practice** — pick a weak skill, drill it, get feedback
- **Feynman technique** — explain the code back in plain language
- **Spaced repetition** — commands, APIs, concepts you keep forgetting
- **Reading source** — libraries you depend on
- **Postmortems** — every bug becomes a rule
- **Compare answers** — two models, or model vs docs
- **Build from scratch sometimes** — keep the muscle
- **Learn in public** — write notes; teaching exposes holes
- **Stay current** — language releases, security advisories, ecosystem shifts

**Anti-skill:** copy-paste until it “works.” That produces a codebase you cannot debug.

---

## 7. Product, Design & Taste Skills

Good coding results are useless if the product is wrong.

- User empathy
- Job-to-be-done
- UX writing
- Information architecture
- Visual hierarchy
- Accessibility
- Empty/error/success states
- Performance as UX
- Scope cutting (what *not* to build)
- Metrics that matter (not vanity)

Ask AI: “What would a confused first-time user do here?”

---

## 8. Professional & Soft Skills

These decide whether your AI work survives contact with a team.

- Ownership (“I shipped it, I own the outage”)
- Code review etiquette
- Asking precise questions
- Saying “I don’t know yet”
- Stakeholder translation (tech ↔ business)
- Negotiation of scope
- Documentation
- Mentoring (and being mentored)
- Ethics: don’t generate malware, don’t hide risk, don’t fake certainty
- Calm under production pressure

---

## 9. Domain Skills (pick yours)

AI is generic. Domain knowledge is the unfair advantage.

Examples:
- Fintech (ledger, rounding, compliance)
- Healthcare (privacy, audit trails)
- E-commerce (catalog, cart, tax, inventory)
- Games (loops, netcode, physics)
- ML/data (leakage, eval, features)
- Embedded/IoT (timing, hardware limits)
- Education, media, logistics, government, etc.

**The pattern:** the more you know the domain, the better you can reject plausible nonsense.

---

## 10. AI-Specific Skills (the new layer)

| Skill | Meaning |
|---|---|
| **When to use AI** | Boilerplate, translation, tests, refactors, explanations — yes. Novel correctness-critical logic — slow down. |
| **When not to use AI** | Secrets, production incident guessing, legal/medical advice, anything you cannot verify. |
| **Context engineering** | What to paste, what to omit, what to pin as rules. |
| **Agent supervision** | Let it run, but set a leash: files it may touch, commands it may run. |
| **Eval thinking** | Golden tests for prompts and tools, not vibes. |
| **Model routing** | Fast model for glue, strong model for hard bugs/architecture. |
| **Prompt libraries** | Reusable recipes for review, tests, migrations, RFCs. |
| **Cost/latency awareness** | Tokens and round-trips are part of engineering. |
| **Data hygiene** | Don’t paste customer PII, keys, or private code into tools that aren’t allowed. |
| **Multi-step plans** | Plan → execute → verify → summarize. |

---

## 11. Meta-Skills (the short list if you only remember 12)

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

---

## 12. Skill Map by Role (use what fits)

**Beginner coder + AI**
- Problem framing, tiny slices, running code, reading errors, git basics, asking “explain like I’m new,” never shipping unread code.

**Working developer**
- Design, tests, debugging, SQL, HTTP, code review, security basics, CI, writing a tight spec.

**Senior / staff**
- Architecture tradeoffs, threat models, domain modeling, evals, mentoring, “what must not happen,” operational readiness.

**Non-coder using AI for results**
- Clarity, examples, checklists, verification with a human expert, version control of prompts, not trusting numbers/quotes without a source.

---

## 13. Practice Plan (get good, not just informed)

**Daily (20–40 min)**
- One kata *without* AI, then redo with AI and compare.
- Read one AI-generated diff line by line.

**Weekly**
- One real feature in thin slices with tests.
- One postmortem: where did AI mislead you?

**Monthly**
- One deeper fundamental (indexes, auth, a11y, concurrency).
- One security review of something you shipped.

---

## Quick reference: skills by type

| Type | Skills |
|---|---|
| Cognitive | framing, decomposition, tradeoffs, mental models |
| Communication | specs, prompts, examples, rubrics |
| CS / coding | languages, algorithms, design, architecture |
| Quality | tests, debugging, review, profiling |
| Security | OWASP, secrets, threat modeling |
| Ops | git, CI, deploy, observability |
| Product | UX, scope, taste, metrics |
| Learning | practice, explanation, source reading |
| Professional | ownership, ethics, teamwork |
| AI-native | context, evals, routing, supervision, data hygiene |
| Domain | the industry you ship into |

---

*Receipt of the human part: AI can type. You still have to think, specify, verify, and be accountable.*
