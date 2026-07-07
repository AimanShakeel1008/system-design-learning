# The System Design Toolkit

The living cheat-sheet of this course: the numbers, formulas, and decision rules that real designs are built from. Every lesson that produces a reusable number or tradeoff rule adds it here. **Reread this file before any real design or interview.**

Seeded in Lesson 00; first real entries arrive with Lesson 02 (estimation) and Lesson 03 (latency numbers).

---

## 1. Latency numbers every engineer should know

*(To be filled in Lesson 03.)*

## 2. Powers of two and size shorthand

*(To be filled in Lesson 02.)*

## 3. Estimation shortcuts

QPS (queries per second), storage per year, bandwidth, cache memory. *(To be filled in Lesson 02.)*

## 4. Decision tables

Which database when · SQL vs NoSQL · which cache strategy when · queue vs stream · strong vs eventual consistency. *(Built up from Phase 2 onward.)*

---

## 5. The design framework (Lesson 01)

**Every design problem, same 7 steps — always start at step 1:**

1. **Requirements** — functional + non-functional; ask clarifying questions first.
2. **Capacity estimation** — QPS, storage/year, bandwidth (Lesson 02).
3. **API design** — the endpoints, request/response shapes.
4. **Data model** — entities, relationships, which database and why.
5. **High-level design** — the boxes and arrows (architecture diagram).
6. **Deep dives** — the 2–4 genuinely hard parts.
7. **Bottlenecks, failures, tradeoffs** — what breaks first, what you gave up.

**Two kinds of requirements:**
- **Functional** = *what it does* (features; "the user can ___").
- **Non-functional** = *how well it does it* (qualities that shape the architecture).

**Big-five non-functional checklist (ask these every time):**

| Dial | Question to ask | Rough handles |
|---|---|---|
| Scale | How many users / requests / how much data? | 1K vs 1M vs 100M → different machine counts |
| Latency | How fast must a response feel? | ms; <100 ms forces caches + nearby servers |
| Availability | How much downtime is OK? | 99.9% ≈ 8.7 hrs/yr · 99.99% ≈ 52 min/yr |
| Consistency | Must everyone see identical data instantly? | strong (bank) vs eventual (like count) |
| Cost | What is the budget? | bounds every other choice |

**Clarifying-question reflex (narrow before solving):** who/what · which features in scope · scale · read-heavy vs write-heavy · latency/availability/consistency targets · hard constraints.

**One-line rule:** *system design = choosing tradeoffs; requirements decide which trade is right.* The same technique can be correct in one system and wrong in another — only the requirements tell you which.
