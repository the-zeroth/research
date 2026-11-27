# How we study working groups

[中文](method.zh.md) · [All working-group notes](README.md)

The One runs teams of language-model agents on a person's computer. A *working group* is one such team built for one
kind of work: designing front-end pages, deploying and operating services, developing software. This note describes
the method every group's research shares. Each group's own note tells what we tried and what happened.

Period covered: 23 to 27 November 2026. All builds use GPT-6.2 Sol; no other model makes the work.

## Why working groups

From late September to November 2026 we measured The One on public benchmarks (Terminal-Bench 4.0 and 4.1, reported
in [Teams on a Fixed Model](../papers/2026-11-teams-on-a-fixed-model)). By the end the open failures followed the
model family rather than the harness, so we turned to real work. We split groups by what is delivered, how it is
checked, and which tools and materials it needs, not by job title.

## Task lists from real, finished jobs

- A group's tasks are jobs the company has already finished, replayed: the starting state (a commit, a broken
  server, a brief), the request in the person's own words, and the accepted result.
- For each group we collected a pool of 25 to 30 candidate jobs and picked 15 across the kinds of work the group
  does (for example: deploy, diagnose, harden, document).
- Five of the fifteen are **held out**, drawn by a fixed random seed, one per kind. Held-out tasks run only at a
  version's baseline and at its final check. We read their sums only, never which task failed or why, and no change
  is ever aimed at them. The rest are *readable*: we read every trial.
- Tasks are packaged as [Harbor](https://github.com/the-zeroth/the-one-harbor) task folders so the same pipeline that
  ran Terminal-Bench runs them, each with a validation script: an empty attempt must fail and the accepted result
  must pass before a package is taken.
- Some groups also get **competition tasks** for measurement only, never for tuning: js13kGames 2026 (rank among the
  human entries), EuroSkills 2025 Web Development modules A and D (scored with the official marking scheme, compared
  with the competitors' published marks), ISUCON14 (share of the 514 teams below our score), and remakes, for
  fictional clients, of the briefs behind three 2025 Awwwards winners (compared locally, never with their assets).

## Two layers of checking

1. **Program checks.** Each task has gates a program can decide: the build passes, nothing scrolls sideways, text
   contrast and size meet a floor, a server answers, a stated rule holds ("ask before an outward step", "no secret
   in a file"). A check must go through the product's outside (the running server, a browser, HTTP), never call one
   internal function.
2. **Blind review** for what a program cannot decide (which page is better, could it ship as is). The founder picks
   between labelled entries without knowing which arm made which; for the creative work we added AI judges (Claude
   Opus) under the same blinding. The key that maps labels to arms is kept apart and never shown before scoring.

**Read every first failure before counting it.** By 26 November, twenty-three checks had misjudged a sound result on
their first contact with a real team (a skip link counted as text outside the page, controls behind a pane's switch counted as missing,
a time zone folder of the bundle counted as the machine's, a scenario replayed in the past). Each was fixed, given
validation cases from the real attempts, and every recorded trial of that task was re-scored under the fixed check.

## Measuring a change

- One variable at a time. A change (a *lever*) is registered in writing, with the rule that will decide it, before
  its first run.
- The control runs beside it, at the same time, on the same tasks, so the model service's day-to-day drift hits
  both.
- With two trials a task, one miss in twelve otherwise perfect tasks decides nothing. Since 26 November a task counts
  as having **fallen** only when its drop is beyond chance (one-sided Fisher test on passes over trials, threshold
  0.2): 0 of 2 against 2 of 2 falls, 1 of 2 does not.
- For judged work we measured the instrument itself. Two judges reading the same build differ by 0.7 points out of
  40 on average; two builds of the same version on the same brief differ by 1.4. So a version's mean over ten builds
  has a standard error near 0.4, and two versions of ten builds each must differ by about a point before the
  difference stands out (see the front-end note). We now compare against fresh builds of the control in the same
  round, because a fixed set of control builds carries its own luck by brief.

## When a version ships and when it is published

- A version **ships** to the product when its registered rule held on the readable tasks, nothing fell beyond chance,
  and the held-out sums are not lower than the control's.
- It is **published** to The One's official group catalog when its record on the group's list passes the publish
  gate (`group_gate.py` in the product repository): its mean over the compared tasks is not lower than the
  baseline's, no task has fallen beyond chance, and its held-out sums are not lower. A tie does not count as an
  improvement.
- Three versions of the deployment and operations group have been published this way (1.10, 1.13, 1.15).

## What transfers

The rule we use to screen a lever before spending runs on it, learned from the failures:

- **Only direction-free or runtime-gated levers hold.** A lever that pushes every task one way (be minimal, change as
  little as possible, always hand off) wins where it was designed and costs elsewhere. Levers that hold either carry
  no direction (show the agent a fact, run a measurement) or fire only when the situation calls for them (a phrase in
  the person's request, a measured count).
- **Words that name a step of the workflow leak.** A paragraph meant for one decision changes others: the word
  "brief" in a counting rule made the deployment group's orchestrator hand work off where it used to do it itself,
  and the hand-off path is where a guard task broke.
- **Agents seldom run the tools a skill offers.** A page-check script added to the front-end skill ran in 1 of 24
  trials; a sentence with a bar to meet moved behaviour more often than a tool to call.
- **Structure moves work; wording seldom does.** Separate minds (agents started without the lead's context) and
  artifacts reused instead of rebuilt changed results; descriptions of what to avoid did not.

## Groups

| Group | Team in The One | Status on 27 November 2026 | Note |
| --- | --- | --- | --- |
| Front-end design | `frontend_design_studio`, and the default lead for site work | creativity research in progress; studio not yet published | [frontend-design.md](frontend-design.md) |
| Deployment and operations | `site_deployment_ops` | 1.15 shipped and published; levers paused | [deployment-ops.md](deployment-ops.md) |
| Software development | `polished_software_dev` | task list and baseline built; waiting for its next version | [software-development.md](software-development.md) |
| Deep research | `deep_research` | task pool being drafted | — |
