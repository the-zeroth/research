# Software development group

[中文](software-development.zh.md) · [All working-group notes](README.md) · [Method](method.md)

`polished_software_dev` is The One's default team for building software: a solution lead at maximum reasoning effort
that can start helpers. It is the configuration measured on Terminal-Bench 4.1 in
[Teams on a Fixed Model](../papers/2026-11-teams-on-a-fixed-model). This note records why it got a task list of its
own on 27 November 2026, how the list was built, and its first baseline.

## Why a list of its own

The team shares the front-end skill with the design group, so its version moves with every change to that skill.
A Terminal-Bench 4.1 run per version (189 attempts at maximum effort) is too costly to repeat that often, and a
benchmark of terminal puzzles says little about the work this team does every day: changing a large product.

## The list

- **A pool of thirty jobs** the company had already finished in The One's own code, six in each of five strata: the
  agent kernel and runtime; the local service's features and API; the desktop renderer's behaviour; Plugins, the SDK
  and the registry; tooling and services outside the app. Twenty-one are features or changes in behaviour, nine are
  defects.
- **Fifteen picked**, three per stratum, sizes small to large; **five held out** by a seeded draw, one per stratum.
  The held-out packages were built by agents that reported back only whether each package was built and the last
  line of its validation (how many defects it catches, how many sound variants pass); we never open them.
- Each task starts at the commit before the accepted change, gives the request as it was made, and checks the result
  through the product's outside: the project's own test suite, the running service over HTTP, the renderer in a
  browser, plus the product's charter rules (for example, agents retry errors forever; a change must not cap that).
- **Packaging found three faults in the task images** before any trial ran, each fixed in every package: the
  repository was unpacked group-writable, which the app rightly refuses for a Plugin folder, so one feature answered
  errors that had nothing to do with the task; a missing GUI library interrupted the test suite at collection, so
  nothing ran; two images lacked an optional database dependency. After the fixes every image collects the project's
  whole suite offline (7,788 to 13,430 tests depending on the starting commit).

## Baseline

The first record, version 7.5, two trials a readable task and two a held-out one:

| | Result |
| --- | --- |
| Readable tasks | 15 of 20 trials, mean 0.750 |
| Held out | 8 of 10 |

The readable misses, read one by one: a rule stated for one member applied only to that member and not to the rest
of its kind (0 of 2); a change that touched a shipped group's files without raising that group's version (0 of 2); one
other task passed one of two. Before the record, four checks were corrected after reading the first attempts (the
wording of one check, a keyboard gate, a time bound, best-effort screenshots).

Version 7.5 was then taken back on main (the browser page check it carried was reverted; see the front-end note), so
the list waits for the team's next version.

## What we took from building it

- An agent-packaged task counts only after we rerun its validation ourselves; on the first try our own "reruns" did
  not run at all (a backgrounded command received an empty script), which we caught only by listing the output.
- Environment faults are worth hunting before the first trial. The missing GUI library had also been in the
  deployment group's images: it appears in 197 of 434 of those trials' records. Every version there met the same
  images, so those comparisons stand, but the teams lost turns to it.
