# SyncBase

A cross-functional alignment hub for product managers. One place for the
communication layer of a project: what happened, what was decided and why, who
owes what to whom, and where two teams are quietly working from different
assumptions.

Live at [syncbase-eight.vercel.app](https://syncbase-eight.vercel.app). Four
sample projects are preloaded, so there is something to look at before you
create anything.

```
git clone https://github.com/sameerbxba/syncbase.git && cd syncbase
npm install
npm run dev
```

---

## Why this exists

The status of a project is rarely in one place. It is spread across a Slack
thread, a slide from last week, a decision someone made in a meeting that half
the team was not in, and an action item that lives in one person's head. The
cost is not the time spent looking. It is the rework three weeks later, when
two teams discover they built to different assumptions.

SyncBase is an attempt to give that communication layer a home, and to test
one specific idea: that the useful place for a language model in this problem
is not writing the updates, but reading across them for the contradictions a
person would miss.

---

## What it does

Each project gets its own dashboard, and the dashboard is made of the things a
PM actually maintains by hand:

- **Timeline.** A chronological feed of updates, milestones and blockers, with
  a health score derived from what is at risk, open and overdue.
- **Decision log.** Every decision with its rationale and the tradeoffs
  accepted, so "why did we do it this way" has an answer three months later.
- **Action tracker.** Cross-team action items with owners, status and due
  dates.
- **Stakeholder sync.** Who needs to be kept informed, and whether each of
  them is current or flagged as needing an update.
- **RACI matrix and RAID log.** Responsibility assignment, and the risks,
  assumptions, issues and dependencies register, both per project.
- **Weekly digest.** One click generates the week's summary from the data
  above, ready to paste into wherever the update is expected.
- **Import.** Projects can be brought in from Jira, Azure DevOps or a file
  export.
- **Archive and templates.** A finished project's structure can be reused
  without its data.

And one feature that is different in kind:

- **Alignment Scanner.** Reads across a project's updates, decisions and
  actions and flags places where teams appear to be working from
  contradicting assumptions. This is the only part of the application that
  uses a model. Everything else is deterministic.

The scanner is tuned for precision over recall. A tool that flags everything
is ignored by day two, so it is designed to surface the few mismatches that
would actually cause rework rather than every inconsistency it can find. That
choice has a cost, and the cost is stated in the governance assessment linked
below rather than left implicit.

---

## What this does not do

Stated plainly, because a portfolio piece that overclaims is worse than none.

- **There is no backend.** Everything is stored in the browser's
  `localStorage`. Your data does not leave your machine, and it also does not
  follow you to another one. Two people cannot share a project.
- **Accounts are local.** Sign-up and sign-in exist so the flows can be
  exercised, but there is no server verifying anything. Do not use a real
  password.
- **The scanner does not run in the deployed version.** It calls a model API,
  and this deployment has no backend proxy to route that call through. On
  the four sample projects it returns pre-computed results so the feature can
  be seen working; on anything else it says so and returns nothing. Wiring it
  to a real backend is the obvious next step and has not been done.
- **The health score is a heuristic**, not a prediction. It is a weighted
  mix of the share of timeline items at risk, the share of open actions that
  are overdue, and the share of stakeholders flagged as needing an update. It
  does not know anything the data does not say.
- **It has not been used by a real team.** The sample projects are fictional
  and the workflows were designed from co-op experience of being the person
  chasing the updates, not from a customer.

---

## The governance document

SyncBase has a NIST AI Risk Management Framework assessment written about it,
the way one would be written about a system somebody had to sign off on. It
separates the one model-backed feature from the rule-based ones, covers eight
risks with likelihood, impact and treatments, and sets the numeric thresholds
at which the scanner would be switched off. Checking that document against
this source code turned up a control marked as implemented that did not
exist; the correction is in its change log.

The assessment and the case study are on
[sameerbxba.github.io](https://sameerbxba.github.io/case-syncbase.html).

---

## Built with

React 19, Vite. No UI framework; the styling is CSS custom properties with a
light and dark theme. The whole application is one component file, which was
a deliberate choice for a solo build and would be the first thing to change
with a second contributor.
