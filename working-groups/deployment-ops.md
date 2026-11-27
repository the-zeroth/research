# Deployment and operations group

[中文](deployment-ops.zh.md) · [All working-group notes](README.md) · [Method](method.md)

`site_deployment_ops` is the team in The One that deploys, diagnoses and hardens services: an orchestrator that
plans, accepts or hands work back, and an engineer it can hand work to. This note records how its versions went from
1.7 to 1.15 between 23 and 27 November 2026, what shipped, what did not, and why. Three of these versions were the
first groups published to The One's official catalog.

## The tasks

- Fifteen jobs the company had already finished, picked from a pool of thirty across five kinds of work; five held
  out by a seeded draw, one per kind. Held-out tasks ran only at baselines and final checks, read as sums.
- Examples of readable tasks: a server answers 500 when a time zone is given as a region only; a script whose
  `PATH` loses a tool when it runs outside a login shell; a headless run that must survive a crash; a test suite that
  hangs on one Python version; a cloud route that fails on text the database cannot store; Chinese bold text that
  the docs site renders wrongly; a cleanup job that deleted work it should have kept; a "not found" page that answers
  200.
- The readable list grew from 10 to 16 tasks on 25 November and to 20 on 26 November (four harder tasks picked by
  design, never by how the current version did on them); the same five stayed held out.
- No competition task fits this group yet. Two candidates were dropped (one can only run on its organiser's hosted
  machines; packaging the other was stopped by the model's cyber-safety rules, and we did not work around it).
  ISUCON14, a performance-tuning contest, is on the list for measurement.

## Baseline: the group against the default team

On the same tasks, the operations group and the default team passed the same number (6 of 8 in the first round;
12 of 16 each when repeated), and the group did it in about half the time and two thirds of the cost. Two tasks
failed for every team, and the failures were real, not misjudged: every fix to the time-zone bug still let a
region-only name raise an error deeper down, and every fix to the `PATH` bug added a preamble that moved the line
numbers in the script's error messages. The common cause: no team ran the starting state and its change side by side on
the inputs that fail.

## The versions

| Version | Change | Result | Decision |
| --- | --- | --- | --- |
| 1.8 | The orchestrator's acceptance and the engineer's self-check compare before and after on the failing inputs | The two always-failed tasks went 0 of 4 to 3 of 4; but one other task fell, because "no other behaviour may change" read as "change as little as possible" and steered away from the framework-wide fix | Not shipped |
| 1.9 | "A regression is a worse answer for the same input; name other differences" | Control 11 of 16, 1.9 12 of 16 | Not shipped |
| 1.10 | 1.8's comparison, fired only when the person's request says other behaviour must stay as it is | 16 of 18 against 13 of 18; the two hard tasks 3 of 4 against 0 of 4; guards 14 of 14; held-out 6 of 10 against 6 of 10 | **Shipped and published** (the first official group) |
| 1.11 | "A count with fewer items named than the count: recover the list by measurement" | The target task 3 of 4 against 0 of 4, but three guard tasks one miss each | Not shipped |
| 1.12 | 1.11, held to items at hand; past-event counts are evidence; the count never decides the verdict | Target better; one guard 3 of 6 against 6 of 6 in a symmetric re-test | Not shipped |
| 1.13 | 1.12's paragraph without the word "brief" | Target 5 of 6 against 0 of 4 (p 0.024); no task worse beyond chance | **Shipped and published** |
| 1.14 | The engineer on the maximum-effort coding slot instead of a fast one | One guard fell (3 of 6 against 9 of 10); 1.65 times the cost, twice the minutes | Not shipped |
| 1.15 | "A stated rule's whole kind is the list": measure the rule on every member as the product reads it, report start and result counts | The two hardest new tasks 7 of 8 against 2 of 8 (p 0.02); readable mean 0.912 against 0.892; held-out 6 of 10 against 6 of 10 | **Shipped and published** |

After 1.15 the founder paused new levers for this group (27 November).

## What we learned

1. **Fire a rule on the situation, not everywhere.** 1.8's before-and-after comparison fixed the two tasks nobody
   passed, but as a standing instruction it pushed every task toward minimal change and broke one that needed a
   wide fix. Gated on a phrase in the person's request ("leave everything else as it is"), the same comparison
   helped where it was asked for and cost nothing elsewhere (1.10).
2. **Words that name a step of the workflow leak into other decisions.** The counting rule in 1.11 and 1.12 never
   fired on the task it broke. Its wording ("before the brief", "the brief lists every member") made the
   orchestrator hand that task off in 5 of 8 trials where it had worked alone in all 18 before, and the hand-off path
   is where the miss came from. Removing one word (1.13) removed the effect.
3. **More reasoning effort is not a free improvement.** At maximum effort the engineer's polished first round drew
   fewer hand-backs from the orchestrator (1.3 against 2.3 a trial), and a gap that 1.13's orchestrator had found
   with its own probe and sent back (an unreadable stored version still emptied the catalog) went through. Twice
   the minutes, worse on that task (1.14).
4. **Guards need the control beside them.** A guard task that missed twice under 1.15 was missed by 1.13 too when run
   at the same time; read against an old record it would have looked like a fall.
5. **The gate has to know chance.** With two trials a task, a strict "no task lower" rule fails any version on a
   single miss among a dozen perfect tasks. From 26 November a task counts as fallen only when its drop is beyond
   chance (one-sided Fisher test, threshold 0.2), with the founder's approval.
6. **Read passes too.** One task was passed by teams that capped an agent's error retries, which the product's
   charter forbids (agents retry forever); its wording had invited it. Those trials were voided, a guard gate was
   added, and the task was rerun.

## A caveat found later

While building the software group's list on 27 November we found that the task images lacked a GUI library the
product's test collection imports, so the project's own test suite stopped at collection in many trials (the
error appears in 197 of 434 readable trial records here). Every version met the same images, so the comparisons
above stand, but the teams lost turns to it.

## Cost

Each lever's measurement cost between about $50 and $290 of model use at list price (the counting rule, 1.11 to 1.13,
was the most expensive). The group is cheaper and faster than the default team on the same tasks.
