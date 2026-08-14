# SyncBase

**An AI-assisted project alignment tool.** It reads across a project's documents and flags where teams are working from different assumptions, the kind of quiet mismatch that surfaces three weeks later as rework.

🔗 [Live demo](https://syncbase-eight.vercel.app)

---

## The problem

On any project with more than a couple of teams, the requirements doc, the meeting notes, and the delivery plan drift apart. Nobody notices, because no one person reads all three closely at the same time. The mismatch stays invisible until it becomes a missed dependency, a rebuilt feature, or a delayed release.

Reading everything manually catches it, but nobody has time to reread every document every week.

## What it does

- Ingests a project's documents
- Reads across them rather than one at a time
- Surfaces where two sources disagree about scope, ownership, timing, or dependencies
- Ranks what it finds, so the output is a short list worth acting on rather than a wall of warnings

## What I learned building it

**The model was the easy part.** Getting an LLM to spot contradictions between two documents is close to a solved problem now.

**The hard part was deciding which of fifty flags were the three that mattered.** An early version flagged everything technically inconsistent, which meant every phrasing difference and every stale date. Accurate, and completely useless, because a tool that flags everything gets ignored on day two.

So the design principle became **precision over recall**. Better to surface three real misalignments and miss one than surface thirty and have the user stop reading. That tradeoff turned out to be the actual product decision, not a tuning detail.

**Where the human stays.** SyncBase flags; it does not resolve. Deciding which version of a disagreement is correct is judgment, and judgment belongs with the person who owns the project.

## Stack

<!-- FILL THIS IN with what you actually built it with, for example: -->
<!-- Next.js, deployed on Vercel, with [model provider] handling the document analysis -->

## Running it locally

<!-- FILL THIS IN, usually something like: -->
```bash
git clone https://github.com/sameerbxba/syncbase.git
cd syncbase
npm install
npm run dev
```

---

Built by [Sameer Athili](https://github.com/sameerbxba) · [Portfolio](https://sameerbxba.github.io) · [LinkedIn](https://www.linkedin.com/in/sameer-athili)
