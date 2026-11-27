# Front-end design group

[中文](frontend-design.zh.md) · [All working-group notes](README.md) · [Method](method.md)

The question: can a team of agents on a fixed model (GPT-6.2 Sol) make web pages that are both creative and finished,
at the level of sites that win Awwwards Site of the Day or of the Year? This note records what we tried from 23 to
27 November 2026, in order, with the negative results.

Two teams in The One build pages. `frontend_design_studio` (a director, an implementer and a reviewer) is the
specialised group. The default lead (one solution lead with helpers it can start) takes most site work when the main
assistant routes it. We measured both.

## The tasks

- **The group's list:** fifteen front-end jobs the company had already finished (pages of the product and of its
  website), five held out by a seeded draw. Program checks: the page builds and opens, nothing scrolls sideways at
  390, 1024 and 1440 pixels, text meets contrast and size floors, the facts in the brief are on the page.
- **Competition tasks**, for measurement only: js13kGames 2026; EuroSkills 2025 Web Development modules A and D,
  scored with the official marking scheme; and three briefs for fictional clients of the same kind as three 2025
  Awwwards winners: a racing driver's site (the winner: Lando Norris, by OFF+BRAND, Site of the Year), an electric
  off-road brand's launch site (Scout Motors, by Locomotive, E-commerce Site of the Year) and an interactive 3D piece
  for a courier (Messenger, by abeto, Developer Site of the Year). We never used their assets and never published
  pictures of them; they were photographed locally as the bar the judges compare with.
- **Fresh briefs**, written for this research and modelled on no winner: a sourdough bakery with a subscription, a
  ten-day dance festival, and the 1.0 launch of an open-source time-series database. A lever that helps on the
  award briefs must help here too.

## Phase 1 (23-24 Nov): the studio against the default lead

- On program checks the two teams were close (7 and 6 of 8 tasks); the studio was faster.
- In the founder's blind review of the first round, the default lead won 7 of 9 pairs. Neither came near the award
  sites: no idea of its own, nothing moving.
- On the competition tasks: the default lead scored 21.00 of 22 on EuroSkills module D, the gold medallist's mark
  (the competitors' average was 10.09); the studio scored 14.17 of 16.5 on module A (median 12.94, gold 15.66).
- Cause of the studio's gap: every studio role ran on a medium-effort model slot while the lead ran on the coding slot
  at maximum effort (on one task, 2,475 reasoning tokens against 18,055). Studio 2.1 put the director and reviewer on
  the planning slot and the implementer on the coding slot. The founder saw no change in kind in round 2.
- AI judges joined the founder: fresh Claude Opus agents, given the task text and pictures under the same blinding,
  made the same picks as the founder on 3 of 3 tasks, with scores compressed toward the middle.

## Phase 2 (24-25 Nov): visuals with code, then with generated images

- **Code alone can render award-grade visuals.** On three subjects unrelated to the briefs (a watch, a coast at dawn,
  a brand's motion loop), the default lead made hero stills and loops with code only, Blender as a Python module
  with Cycles, or OpenGL shaders on a CPU renderer, in 32 to 77 minutes; the watch rendered in Cycles was photo-grade. Live three.js versions of the same
  subjects were weaker (no reflections, plastic materials). The site tasks had never asked for such work.
- **An art director's notes help; choosing is the bottleneck.** Each round of notes lifted the pictures, and the
  leaps came only from notes that changed the direction; the team's own critique polished inside its first
  direction. Asked for three different directions, the team sketched three and picked the conventional one each time.
  One sentence from outside the team picking a direction beat two rounds of notes. So the skill shipped as: three rendered
  directions, ask the person to pick, build the pick.
- **On whole sites the picks did not show.** The judges' scores moved by about 3 points between rounds for the same
  site, more than the direction lever's effect. We calibrated: the award winner is photographed the same way and
  shown as a reference entry, and two judges a round agree within 0 to 2 points per entry.
- A rule to make the first view move raised motion in 2 of 6 builds and about 0.7 a task (noise); not shipped.
- **Image generation.** Through the image-generation Plugin (an OpenRouter route), leads generated photographic
  material whenever a connection was ready (never without one) and the judged score rose 1.25 to 1.75 a task where
  they did, still 1 to 3 points under the winners. A still can also be filmed into a short loop for the first view.
  The founder found generated images clearly better; the Plugin is published.

## Phase 3 (26-27 Nov): creativity with code only

The founder's direction on 26 November: the scenario with no image or video model comes first; our work is far from
the winners, not by a point or two; build the creative side so the results stop looking alike; GPT Sol only.

### How it is judged

Each judging folder holds the brief, pictures of every build at 1440 and 390 pixels, and a *walk*: twelve frames
taken while a script moves the mouse, holds, clicks, drags, presses keys, scrolls and waits, each captioned with the
share of the screen that changed. The award winner is walked and photographed the same way. A creativity-first
judge writes, for every entry before any score: the idea in one sentence ("the visitor [does X], because [this true
thing]") or "none"; whether the page is its category's default shape (the *template*: the name in big type beside
the subject's object, a strip of facts, then stacked sections that fade in); whether the idea would still work with
a competitor's name (the *transplant test*); the moment a visitor would describe to a friend; whether a juror who saw
thirty sites that day would remember it a week later; and whether it would win Site of the Day. Then the four
Awwwards scores (design 40%, usability 30%, creativity 20%, content 10%), 1 to 10.

The first calibration (round 11): the winners 31.6 of 40, our builds 24 to 26, no idea of their own on any reading,
every build in one composition, and generated images raising finish but not ideas.

### Levers that moved the judges

| Lever | What changed | Measured |
| --- | --- | --- |
| Separate minds | The lead starts three concept agents that cannot see its drafts or each other, one true fact of the subject each; each writes one idea the visitor performs and prototypes only its signature moment | Creativity +1.6, total +1.8 over control; ideas that belong only to the client on 12 of 12 readings (one mind asked for three ideas wrote one idea three times) |
| Prototype first | The chosen prototype is copied in as the first screen and edited, never rebuilt from a blank page | Fresh briefs: creativity +2.4, total +3.4 over control; Site of the Day on 6 of 12 readings (control 0) |
| Hand on the subject | The pointer acts on the subject itself and something visible happens the instant it moves; the subject owns the screen, the words sit small at its edges | Award briefs: creativity 7.00 against 5.49; remembered 5 of 12 against 0; judged the template on 7 of 12 readings against 12 of 12. Shipped |
| The studio with the same process | The studio's director starts the three concept agents | Creativity +1.6 and total +2.5 on the award briefs, +2.3 and +3.1 on the fresh ones |
| A juror before delivery | When the site works, a juror started without context judges it as an Awwwards jury from screenshots and a visitor's try, names the ten costliest flaws; the team fixes them, then a second juror | Total +1.13, ahead in 10 of 10 readings (sign test p 0.002); about 1.6 times the spend. Shipped |

Two of these are worth stating as findings. Separate minds fixed the sameness of *ideas*, not where the idea landed:
the built pages put the idea into a section under the template's first screen, and telling the builder "the first
screen is the idea" was obeyed only in letter (a small slider in the hero's corner). Reusing the prototype as an
artifact is what moved it onto the first screen.

### Levers that did not

Every one of these was a single change on the shipped process, two builds a brief on five briefs, judged blind
against the same control in the same round:

| Lever | Total against control | Note |
| --- | --- | --- |
| Carry the subject's object through every part of the page | about 0 | |
| Push past the first idea | +0.34, about 0 over both its rounds | higher best builds, lower worst ones |
| Render in a register code does well (draw the object as a plate or line drawing when a render reads as a toy) | +0.49 | barely moved design, the score it aimed at |
| A juror, not the builder, picks among the three prototypes | +0.43, then +0.34 in a second run | ahead in 9 of 20 readings; remembered and Site of the Day rose; not confirmed |
| A fourth concept agent joining two truths | -0.21 | no site grew from it |
| The juror sees every screen, top to bottom | -0.57 | the opening's fixes went undone |
| Later screens prototyped by separate agents | -0.30 | |
| Display words lettered in SVG | +0.05 | |
| The signature moment never finishes | -0.23 | |
| Gestures that turn the subject into another true version of itself | -0.18 | |
| Screens laid out as spreads, not components | +0.02 | |
| The first screen answers a passing pointer (with a browser check) | -0.08 | the pointer response rose from 0.6% to 14.6% of the screen; the scores did not move |
| Three of the above together | -0.58 | |
| Open-licensed fonts allowed in the brief | +0.20 | design +0.3; the "default type" complaint went from 55% of notes to 0% |
| Juror rounds until none names a flaw over half a point (up to four) | +0.01 | its builds were named for more floor defects, not fewer |
| Prototypes of about three screens, carrying two content blocks in the idea's own container | -0.02 | judged the template less often (50% against 65%); scores flat |

A browser page check added to the skill (sideways scroll, small text, contrast, cut text, script errors) shipped as
studio 2.5, tied 2.1 on the group's list, and was taken back out: the agents ran it in 1 of 24 trials.

### What the judges' sheets say

Across 420 readings (rounds 16 to 22):

- **The brief sets the ceiling.** Readings at 30 of 40 or more: database launch 23%, dance festival 11%, bakery 4%,
  off-road brand 2%, racing driver 0%. What code draws well (gauges, paper records, light, type) reaches 30; cars,
  helmets, faces and bread stay near 28.
- **Most builds are still the template.** 60 to 95% of readings in every arm; builds judged otherwise score 0.8 more.
- **Where the idea came from matters a little.** Builds grown from the concept agent that started from the subject's
  data or medium fail the transplant test in 43% of readings, from its objects or name in 2%; the total differs by
  about 0.3.
- **What the notes name.** "Below the first screen it goes back to regular sections": 34% of notes, mostly on the
  better builds. "The idea fits any brand in the category": 14%, about a point lower. "Type like the system
  default": 17% (the briefs banned fonts from the web until 27 November). "Rendered like a toy": 9%.
- **On the racing driver brief nearly every build replays the helmet's stripe that widens with each win,** in every
  arm: the brief's most striking fact wins the pick. The winner's idea, the visitor wiping the driver's own helmet
  designs onto his face, needs his photograph.

### How precise the measurement is

- Two judges reading one build differ by 0.72 points of 40 on average; two builds of the same arm on the same brief
  differ by 1.41 (one build's standard deviation is about 1.2). An arm's mean over ten builds therefore has a
  standard error near 0.4, and two arms of ten fresh builds must differ by about 1.1 points to stand two standard
  errors apart (0.8 with twenty builds, 0.5 with forty).
- For a while every arm was compared with the same ten control builds. Those builds happened to be weak on one brief
  and strong on another: every arm "won" the database brief in 22 of 24 readings and "lost" the festival brief in 20
  of 24. Since round 24 the control is built fresh in every round.
- So the levers above that landed within about half a point of the control are not distinguishable from noise, and
  the two that were real moved far more.

## Where it stands on 27 November

- The process plateaus near 7.1 a criterion. Since the juror step, every lever has measured zero within the
  instrument's resolution, and fixing a named defect (the first screen answering a passing pointer) did not move the
  scores: the defects the judges name move with the overall level.
- The GPT jurors inside the team do not see what the judges see: with four rounds of them, more floor defects were
  named, not fewer.
- The bench now allows open-licensed fonts, as real use does; the scenario still has no image or video model.
- Two levers that bring taste in from outside are running on the fresh briefs, twelve builds each against twelve of
  the shipped process: the lead studies six recent award winners before the concept step and hands its notes on; or
  ideation stays blind to outside sites and each juror first looks at screenshots of four award winners from other
  categories, then judges ours beside them.
- The studio's catalog publication waits on its list: versions 2.3 and 2.4 fell from 0.667 to 0.583 on the list's
  mean, each because one task passed one of its two trials where the 2.1 record had a single passing trial, and the
  gate's mean rule is strict.

## What we take from it

1. Ideas get better when they come from separate minds, and land on the page when the artifact is reused; words that
   describe the template do not stop it.
2. Choosing is the weak step: teams keep the brief's most striking fact or the conventional direction. A one-sentence
   pick from outside the team moved the work more than rounds of notes.
3. A single change worth less than about a point cannot be told apart from noise at ten builds an arm. Compare with
   fresh control builds in the same round, and screen levers by whether they could move a point at all.
4. The model's own taste is the bound we hit; what is left to try brings in what it lacks.
