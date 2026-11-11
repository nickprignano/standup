# Standup spec (v1)

Status: red-teamed twice with Fable (findings and what changed are at the end). The owner took
the defaults, asked for a classic puzzle, named it Standup and created the repo (2026-11-10).
Merging this spec approves it. Nothing gets built until then.

## What it is, and what it can honestly promise

The ask was a puzzle game that helps improve cognitive function. The research (below) doesn't
let any app honestly claim that: practising a puzzle makes you much better at that puzzle and
close copies of it, and studies don't find it makes people better at other things. So this spec
builds the honest version:

**A short daily set of puzzles that adapt to you, that you get better at, and that never claims
more than that.**

Three quick drills in v1: tap tiles back in reverse (Stack), say whether a shape is turned or
mirrored (Turn), and sort cards by a rule that keeps changing (Switch). Each adapts so it stays
hard but winnable, and the app charts your level on the device. They are our own versions of
published lab tasks, built to feel like a game: short rounds, bests, sound, and a small line-art
keepsake made from each day's play.

Plus one **classic**: a daily picture-logic puzzle (a nonogram), untimed and solved at your own
pace, called **Reveal**. Fill the right cells and a pattern appears.

Named **Standup** by the owner (2026-11-10): a short daily check-in, like a team's morning
standup. Served at `standup.prignano.ai`. Plain JavaScript, DOM and canvas, no build step,
static files on Cloudflare, installable as an app (PWA) from day one like pinball.

It is a game, not a lesson app (that's Payoff and the learn-anything app), and it teaches no
subject.

## Decisions so far

| # | Question | Answer |
| --- | --- | --- |
| 1 | Ask | Asked for: a puzzle game that helps cognitive function (owner, 2026-11-10). What the evidence allows: a puzzle game you get better at. The app doesn't claim the first |
| 2 | Audience | **13 and up** (owner took the default, 2026-11-10). Nothing leaves the device, and every chart carries a line that scores wobble and this isn't a test of you, so younger players are fine too. The studies are on adults; nothing here is checked for under-18s |
| 3 | Name | **Standup** (owner, 2026-11-10), replacing the proposed Working Set |
| 4 | v1 puzzles | Three drills, Stack, Turn and Switch (owner took the default, 2026-11-10), plus one classic, the daily nonogram Reveal (owner's ask, same day). A speed puzzle (Glimpse) waits for v1.1 after a patent and trademark check |
| 5 | Honesty | Approved when this spec merges: one plain line on the first screen, a short science page, every player-facing word in one file the owner approves, and a test that blocks claim words. The self-test "Check" from the first draft is cut (it couldn't measure what it promised) |
| 6 | Accounts | Approved when this spec merges: none: progress on the device, export file, no server, no AI |
| 7 | Home | `nickprignano/standup` (created by the owner, 2026-11-10), `standup.prignano.ai`, deployed on merge by Workers Builds |
| - | License | MIT. All puzzles, art and sound are our own |

## What the research says (checked 2026-11-10)

This sets what the app may say. Short version: **you get better at what you practise; it mostly
stays there.**

| Finding | Source | What it means for us |
| --- | --- | --- |
| Computerized working-memory training programs improve the trained tasks a lot, mainly through practice | Rodas, Asimakopoulou & Greene, *Psychonomic Bulletin & Review* 2024: 52 comparisons, 3,737 adults (mean age 24.6). Criterion tasks SMD about 1.15 | "You'll get better at these puzzles" is supported |
| No gain in general reasoning or intelligence | Same paper: fluid intelligence SMD 0.007. Also Melby-Lervåg, Redick & Hulme, *Perspectives on Psychological Science* 2016; Simons et al., *Psychological Science in the Public Interest* 2016; Sala & Gobet, *Trends in Cognitive Sciences* 2019 | No "smarter", IQ, "brain age" or composite score |
| Small gains on a few nearby skills, none on others | Same paper: working memory 0.18, inhibition 0.19, but **switching −0.05 and processing speed −0.10 (not significant)** | Switch is not presented as improving flexibility; no speed claims |
| Longer spatial training (courses, long practice) spreads to other spatial tasks and lasts | Uttal et al., *Psychological Bulletin* 2013, 217 studies, g = 0.47 | Does **not** show that Turn, at a few minutes a day, transfers |
| No evidence for 13 to 17 | All of the above are adult studies | Science page says so |
| In adults 65+, one speed-training program was linked to fewer dementia diagnoses over 20 years, only in people who also had booster sessions; memory and reasoning training weren't | ACTIVE 20-year follow-up, Coe et al., *Alzheimer's & Dementia: TRCI*, Feb 2026 (Medicare records, 40% vs 49%, HR about 0.75; booster group defined after randomization) | One trial, a specific program and age group, mechanism unknown. **The app never mentions it or any health outcome.** It's here so the owner knows |
| Regulators act on overclaiming | US FTC, Jan 2016: a large brain-training company paid $2M to settle charges of unsupported ads | Claim rules below are enforced by tests and owner sign-off |

Every citation is re-opened, not written from memory, when `data/science.json` is written.

## Prior art

Checked 2026-11-10. Nothing to fork.

| Source | What we take |
| --- | --- |
| ai-brain prior-art check | Nothing in our KBs; GitHub has a few tiny unlicensed toys (reference only, nothing used) |
| Published lab tasks: backward spatial span (Corsi), mental rotation (Shepard and Metzler), task switching | The mechanics. Our own shapes, names, art and sound. We call them "our own versions of published lab tasks", not original inventions |
| Commercial brain-training apps | Nothing: no names, game names, characters, art, sounds or terms. The words test keeps their names out of shipped files, encoded so the repo never spells them out |
| Nonograms (invented in Japan in 1987, now a generic puzzle type) | The puzzle type. Brand names for it from console games and puzzle magazines stay out of shipped files (in the encoded banned list); we call it a picture-logic puzzle. Open-source solvers exist; we write our own line solver, which is short. No grid is taken from any book, site or app: every grid is generated. A trademark-register check of the generic term and of the name "Reveal" is recorded before PR 3 |
| jsPsych (MIT) | Ideas only on browser timing. Not a dependency |
| prignano-theme `art/` | The line-art library Vibes uses, for the daily keepsake |
| pinball PR #7, Payoff spec | Our own PWA recipe, export pattern, and "claims are checked by tests" rule |

## The player's path

1. **First open.** One screen: "Short puzzles that adapt to you. You'll get better at them.
   Studies don't find that this makes people better at other things." **Start**, and a link to
   the science page. No sign-up.
2. **Today's set.** The three drills, about 2 to 3 minutes each, under 10 minutes in all. Any
   puzzle can be left out in Settings. The first session of each puzzle opens with a short
   calibration.
3. **After the set.** A results card: each drill's level today and its best, the day's
   keepsake (below), and today's Reveal as not started, in progress or solved. Reveal takes from
   under a minute at 5x5 to about 10 minutes at 10x10, and can be left half-done and finished
   later that day. Then free play, as long as the player likes. Free play counts toward bests
   but not toward the chart, so the chart compares like with like.
4. **Progress.** One chart per puzzle, axis "level in this puzzle", a rolling median line with
   single days as faint dots, and days played this week. Every chart carries one fixed line:
   "Scores go up and down with sleep, mood, time of day and your device. This is a game, not a
   test of you." No streaks, warnings, push notifications or comparisons with other people.

## The keepsake

At the end of each day's set, the app draws one still line-art piece from the prignano-theme art
library, seeded by the date and the day's three levels, so every day's piece is different and
yours. A gallery shows past days. It's the "something to come back for" that a chart alone isn't,
with no streak pressure. Stills only (the library's settled frame), so no motion or flash
concerns; styles that carry a stripe flag keep the library's limits.

## The puzzles

The three drills share one look (Reveal follows it too): thin glowing lines on the prignano theme's background, big tap
targets, no color-only meaning. Player-facing text describes what you do, never a "skill".
Feedback is a small mark next to the answer, never a full-screen color change.

### Stack

A 4x4 grid of tiles. Some light up one after another, and the player taps them back in
**reverse order**. 15 trials a session (about 2.5 minutes).

- Levels 1 to 14: sequence length 2 to 8, each at a slow pace (700 ms glow, 300 ms gap) then a
  fast one (500 ms, 200 ms). So (length 4, fast) sits between (4, slow) and (5, slow).
- A tile never lights twice in a row. Lighting is a gentle brightness rise, not a flash.
- The harder "busy" form (a question between tiles) is not in v1.

### Turn

Two flat block shapes side by side. Is the right one the same piece turned, or a mirror image?
40 trials a session (about 2.5 minutes).

- Shapes have 6 to 8 blocks. The generator keeps only shapes whose mirror can't be made by
  turning: 25 shapes at 6 blocks, 88 at 7, 335 at 8. (At 4 and 5 blocks only 2 and 6 such shapes
  exist, too few: players would learn them by sight.)
- Both pictures get a random base rotation. Difficulty is the **angle between them** (30° to
  180° in 30° steps, never 0°), then block count, then time allowed (8 s down to 3 s). Half the
  trials are mirrors, and mirrors are turned too.
- 3D block figures are not in v1.

### Switch

Cards show a shape (triangle or square) and a count (one or three). A cue word and icon above
the card says **SHAPE** or **COUNT**. The mapping stays on screen: triangle and one go left,
square and three go right. The rule changes at random. 80 cards a session (about 2 minutes).

- At least 75% of cards give different answers under the two rules, so a player who ignores the
  cue scores about 62.5%, below the staircase target, and can't settle in.
- Levels: time per card (3 s down to 0.8 s) and how often the rule changes.
- Scored on accuracy. No "switch cost" number in v1: from one session it's mostly noise.

## The classic: Reveal

A grid with number clues along each row and column. Each clue lists the runs of filled cells in
that line, in order ("3 1" means three filled, a gap, then one). Fill the right cells and a
pattern appears. Untimed, no lives. It sits outside the drill set: it's offered on the results
card and the home screen, with its own done mark, and doesn't use the staircase.

### Sizes

- 5x5, 8x8 and 10x10 daily. The size setting is **Auto** (default), 5, 8 or 10. Today's size is
  fixed when the puzzle is first opened; a change applies the next day.
- Each day the player starts (changes at least one cell) ends one of three ways:
  **clean** (solved with no Check and no Show a cell), **helped** (solved after either), or
  **unfinished** (not solved by the end of that local day). A day never opened counts as
  nothing: it doesn't break a run.
- **Auto** moves up a size after three clean days in a row, and down after two helped or
  unfinished days in a row. After a move down, it takes five clean days in a row to move up
  again, so the size doesn't bounce.
- 10x10 is offered only where cells come out at least 28 px (about 370 px wide and up, with
  16 px gutters and room for 5-number clues); narrower phones top out at 8x8. Free play adds
  12x12 where the grid area is at least 470 px each way, and 15x15 at 570 px.

### The daily puzzle

- The day is the device's local calendar date, from the same function the drills and keepsake
  use. A puzzle belongs to the date it was opened on, even if solved after midnight. One row per
  date; rows dated in the future (clock changes) are kept but ignored until their date comes.
- The seed is a hash of the local date, the size and a `GEN_VERSION` constant. So it's the same
  puzzle for everyone playing that size that day on the same app version, with no server.
- The puzzle (size, solution, cell states, active time, help used) is **saved when first
  opened** and read back after that, never regenerated. An app update mid-day can't swap the
  puzzle under a half-done grid.
- Free play: unlimited puzzles from random seeds, counted but not charted.

### Always solvable by logic

- Random numbers come from a small seeded integer generator (mulberry32 seeded from a string
  hash), and generation uses integer maths only, so every engine makes the same grid.
- **5x5:** random cells. **8x8 and up:** left-right mirror symmetric, which gives more
  picture-like patterns. Fill stays between 45% and 65%. A grid is rejected if it has a blank
  row or column or more than one completely full line, or if the daily generator used it in the
  last 30 days at that size.
- A grid is kept only if the line solver solves it completely. The solver works line by line,
  using every arrangement of a line that fits the cells already known, and repeats until
  nothing changes. Solving fully that way proves there's exactly one solution and no guessing is
  ever needed. Grids also have to fall in a band of solver passes per size (in
  `data/levels.json`, a first guess of 3 to 4 at 5x5, 3 to 5 at 8x8, 4 to 7 at 10x10, tuned by
  the owner in PR 4), so one 10x10 isn't trivially easy and the next brutal.
- Fable's simulation (2026-11-11): 82% to 94% of in-band grids pass the solver, generation
  takes about 1 ms or less even at 15x15, and every kept grid had exactly one solution by an
  independent counter. So it runs synchronously on the device. The attempt counter is part of
  the seed stream; after 200 attempts the generator falls back to a fixed built-in grid for that
  size, which a test proves never happens over 1,000 seeds.

### Controls

- On touch, a **Fill / Dot** switch (Fill to start): in Fill a tap toggles filled and clear; in
  Dot it toggles dot (marked empty) and clear.
- **Drag** paints: the first cell changes as a tap would, then the drag applies the same state
  to cells that started in the first cell's state, locked to that row or column. One drag is one
  undo step. The grid sets `touch-action: none`; the page still scrolls from outside it.
- The row and column under the finger are highlighted, so a small target can be checked before
  lifting.
- **Undo**, **Check** (shows wrong cells on request) and **Show a cell** (fills one right cell).
  No error marking during play, which would turn it into guessing.
- A clue line that matches gets a tick and dims, not only a color change. Clue text is at least
  12 px; a long clue row shrinks the cells, not the text.
- Keyboard: arrows move, Space fills or clears, X dots or clears, Z or Ctrl+Z undoes, with a
  visible focus ring. The grid is a labelled DOM grid: each cell reads its row, column and state,
  and each row and column header reads its clue, so Reveal works by keyboard and screen reader.
- **Solved** when the grid matches every clue. The solution is unique, so that's always the
  intended pattern.

### Progress

- Days solved (clean and helped) per size, and median solve time per size for **clean** days
  only, as a rolling median with no line until a size has 5 clean solves. No best time.
- The timer counts only while the puzzle is on screen and the page is visible, and is never
  shown during play. The help text says time is recorded for the chart, and a setting turns the
  time chart off.
- Under the chart, as well as the fixed "scores wobble" line: "Puzzles differ in difficulty from
  day to day."

## Adaptive difficulty

One engine for the three drills (Reveal has its own size rules), in `src/staircase.js`:

- **Calibration:** the first 8 trials of a puzzle's very first session move one level per
  answer. That session is not charted.
- **Then 3-down/1-up:** three right in a row moves up a level, one wrong moves down. That
  settles where the player gets about 79% right (0.5^(1/3)): hard, but winnable. A run of right
  answers doesn't carry over between sessions.
- **Session level:** the mean of the turning points after the first two, with at least four
  counted. With fewer, no point is charted and the stored level stays as it was.
- **Next session starts** at the last session level, rounded down. (The draft started one level
  lower; Fable's simulation showed that biases the chart down by 0.5 to 1 level and makes day 1
  look like the best day.)
- **The chart** shows a rolling median of the last 5 sessions.
- Level tables live in `data/levels.json`, so tuning is a data change.

## The science page

One page, linked from the first screen and the menu. Every sentence comes from
`data/science.json` with a `source` (citation and link), and the owner approves every word.

What it says, in plain words:

1. You'll get better at these puzzles. That's real, and it's the main thing practice does.
2. Studies mostly find the gains stay with the practised task or very similar ones. They don't
   find that brain games make people better at reasoning, school or work in general.
3. Longer spatial training, like courses, has been found to spread to other spatial tasks.
   Nobody has tested whether this puzzle does.
4. These studies were on adults.
5. So play because it's a good puzzle and you like watching yourself improve. The studies are
   about tasks like the three drills; Reveal is here because it's a good puzzle.
6. Regulators have made companies pay to settle charges that their brain-game ads claimed more
   than this (no company named in visible text).
7. Links to the sources.

No health or medical information or advice, and no condition is mentioned.

## Claim rules (enforced)

1. **One strings file.** Every player-facing word lives in `data/strings.json` or
   `data/science.json`. A test fails if a view file contains a display string literal that
   isn't from them. The owner approves both files word by word in their PRs.
2. **Words test, as a second net**, on the strings and science files, manifest, README and HTML,
   with word-start matching so code like `preventDefault` or `unique` doesn't trip it:
   `\bsmarter`, `\bIQ\b`, brain age, brain score, brain training, brain health, train your
   brain, `\bboost`, `\bsharp`, `\brewir`, neuroplastic, `\bcognitive`, mental fitness, workout,
   science-backed, based on research, designed by scientists, `\bimprove your`, keep your mind,
   `\bclinical`, `\bproven`, guarantee, `\bprevent`, dementia, Alzheimer, ADHD,
   `\bcur(e|es|ed|ing)\b`, `\btreat`, therap, doctor, memory loss, younger brain, `\breasoning`,
   logical thinking, problem-solving, `\bfocus`, concentrat, `\brelax`, `\bstress`, `\bcalm`,
   mindful, `\banxi` ("logic" alone stays allowed: it names the puzzle type), plus the lab
   name and abbreviation of the commercial speed test and the names of commercial
   brain-training apps and their games, and the brand names of nonograms from console games, puzzle
   magazines and syndicators, matched as phrases (encoded). The encoded brand list also runs on
   `src/` and `test/`. The science page's own wording ("brain
   games") is checked by the owner, not exempted by the test.
3. Source URLs and citations are checked against an allow-list of approved entries, not
   exempted wholesale.
4. Default games.json blurb: "Short puzzles that adapt to you. You get better at them; that's
   all we claim."

## Look, sound and access

- Original look on the shared prignano theme (pinned files, like the other games): light and
  dark, line-art shapes, no mascot.
- Sound synthesized with the Web Audio API: a soft tick for right, a low tone for wrong, a short
  chime at the end of a puzzle. Muted until the first tap, mute saved.
- Flash safety for the whole app: no luminance change over 5% of the viewport more than 3 times a
  second, no full-screen color changes, no high-contrast regular stripes. Switch's fastest pace
  is 1.25 card changes a second, each under 5% of the screen. A test checks the feedback and
  card areas at 390x844 and 1280x720.
- Meaning never by color alone. Reduce motion (setting or system) turns off every animation that
  isn't the puzzle itself.
- Keyboard play on desktop: Stack by a 4x4 key block (1-4, Q-R, A-F, Z-V) or arrows and Enter;
  Turn by S (same) and M (mirror); Switch by the left and right arrows; Reveal as in its
  Controls.
- The three drills need sight and two are timed; Reveal is untimed and works by keyboard and
  screen reader. The About screen says so plainly.

## Data and privacy

- Stored in `localStorage`: settings, per-puzzle level and best, one summary row per session
  (date, puzzle, session level, trials, percent right), one Reveal row per day (date, size,
  outcome, active seconds), the one in-progress Reveal, and keepsake seeds. About 100 bytes a
  session, well under 1 MB for years of play. No raw trial logs.
- `navigator.storage.persist()` is requested where available. Safari can clear a site's storage
  after a week without a visit unless it's installed, so the progress screen says that
  installing or exporting keeps progress.
- If storage is blocked, the app works for the session and says progress won't be kept.
- **Export file:** Settings saves progress as JSON with a `version` field and loads one back,
  checked against the schema first. Adding Reveal bumps the version; an older file without
  Reveal rows still loads. A bad file, or one from a newer version, is refused with a plain
  message.
- Nothing leaves the device. No accounts, analytics, ads, server or AI calls. The only network
  requests are the pinned theme files; outside links are the science page's sources. The About
  screen says so.

## Installable app and hosting

Pinball PR #7's PWA recipe (manifest, original icons, iOS tags, offline service worker stamped
by `tools/sw-version.mjs`, stale-list test, update button, safe-area padding).

Cloudflare Workers static assets with no Worker script (`wrangler.jsonc` named `standup`,
`.assetsignore` leaving out tests, tools and docs), connected with Workers Builds so each merge
to `main` deploys. The owner creates the repo and adds the custom domain. Claude writes
`docs/DEPLOY.md` (with the Safari storage case in its manual checks); its last step is the
prignano.ai `content/games.json` PR that sets the entry live. Nothing on the account changes
without the owner's yes.

## Files

```
index.html, app.css
src/app.js            screens, today's set, free play, progress, keepsake gallery
src/staircase.js      calibration and 3-down/1-up engine (pure)
src/puzzles/stack.js, turn.js, switch.js   generator (pure) + view each
src/puzzles/reveal.js  nonogram generator, line solver (pure) + view
src/keepsake.js       seeds the theme art library from the day's levels
src/store.js          storage, export and import, schema check
src/audio.js          synthesized sounds, mute
data/levels.json, data/strings.json, data/science.json
tools/sw-version.mjs, sw.js, manifest.webmanifest, icons/
test/*.test.mjs
```

## Tests

`node --test` covers:

1. **Staircase:** over simulated 30-day chains for three psychometric slopes (0.5, 1 and 2
   levels) and both guess rates (none for Stack, 50% for Turn and Switch), the mean charted
   level is within 0.3 levels of the true 79% point and the day-to-day spread is under 0.6
   levels; calibration moves one level per answer and isn't charted; too few turning points
   charts nothing.
2. **Levels:** each puzzle's level table gets strictly harder by its own measures.
3. **Generators** (1,000 seeds each): Stack never repeats a tile in a row; Turn's pool has at
   least 20 shapes at every level, no shape equals its own mirror under turning, no trial has a
   0° difference, and every answer is right; Switch has at least 75% conflicting cards, a
   simulated cue-ignoring player scores under 65% at every level and a guesser about 50%.
4. **Flash and area:** feedback and card changes stay under 5% of the viewport and 3 a second.
5. **Words and strings:** no display literal outside the strings files; the banned list; every
   science entry has an allow-listed source.
6. **Store:** export then import gives the same progress; a bad or old file is refused.
7. **Reveal:** for 1,000 seeds at each size (5, 8, 10, 12, 15), the solver's result equals the
   generated grid and an independent backtracking counter, sharing no code with the line
   solver, finds exactly one solution; on 1,000 unfiltered grids per size, whenever the line
   solver completes the counter finds exactly one solution; single-line cases with known answers
   (empty clue, full line, "3 1" in 5, a contradiction); fill band, no blank lines, at most one
   full line, pass bands, no repeat within 30 days, fallback never reached; a golden test of
   three fixed dates per size against stored grid hashes (changing them needs a `GEN_VERSION`
   bump in the same PR); date to seed with an injected clock at 23:30 local in UTC-8 and 00:30
   in UTC+9, a repeated date and a future-dated row; the size rules with named cases (a Check
   day, a skipped day, unfinished then finished the next day, the 5 floor and 10 ceiling, size
   fixed mid-day, five clean days after a move down); cells at least 28 px at 390x844 and
   375x667 and no 10x10 offered at 320 and 360 wide; export and import round-trip a half-done
   Reveal.
8. **Keepsake:** same date and levels give the same piece; only still frames are drawn.
9. **PWA:** the service worker file list is current.

**Done means:** tests pass in CI, plus a scripted browser check (Playwright, not in CI, like
pinball) at phone and desktop sizes that plays one session of each puzzle. Install and offline
use are a manual check in `docs/DEPLOY.md`.

## Pull requests

1. Shell, today's set, staircase, **Stack**, storage, strings file and words test, CI. Then an
   **owner playtest gate**: play Stack for five days. If it isn't something you'd open
   unprompted, stop and rethink before building more.
2. Turn, the progress chart, the PWA recipe, `wrangler.jsonc`, `docs/DEPLOY.md`.
3. Switch and Reveal. Reveal is the largest view in the app; if the PR runs long, it splits
   rather than trimming tests.
4. The keepsake, the science page and About (owner approves every word), sound, export file, polish, and a
   level-tuning pass by the owner per puzzle.

Then, after the owner's Cloudflare setup, the prignano.ai games.json PR.

## Not in v1

- **Glimpse (a speed puzzle), v1.1 at the earliest.** The first draft's design matched the
  best-known commercial speed exercise closely. Before building any speed puzzle: a recorded
  patent and trademark check, a design of our own (for example "find the odd marker in a
  briefly shown ring"), and a timing design that copes with 30 Hz battery-saver screens and
  variable refresh rates.
- **The Check** (a self-test comparing practised and unpractised tasks). Cut: with one person,
  no comparison group, 10 to 20 items and retest effects, it couldn't separate practice from
  noise, and its tasks would become practised too. A reasoning score tracked for a teenager
  would also read as an IQ test.
- Accounts or sync, leaderboards, norms or percentiles, a composite score, 3D shapes in Turn,
  Stack's busy form, n-back, word or number puzzles, reminders or notifications, other
  languages, any health content.

## Open questions (with defaults)

Answered 2026-11-10: the owner took every default (13 and up, Stack/Turn/Switch,
keepsake in, build after the current queue), added a classic puzzle (Reveal), and named it
Standup.

1. **Name clash.** "Standup" is also a common word for team-meeting tools and comedy apps. A
   fuller app-store search for a puzzle game of that name before build 1; the owner decides if anything
   close turns up.

## Fable red team (2026-11-10)

Fable returned 20 findings. What changed:

| ID | Finding | Severity | Status |
| --- | --- | --- | --- |
| WS-1 | The Check can't separate practice from retest and noise; its text stated the result in advance | High | Fixed: Check cut from v1 |
| WS-2 | 20 fixed-level trials: a ±25-point noise band against at most +21 points of headroom | High | Fixed: Check cut |
| WS-3 | 10 matrix items is noise (±4.3 items), the tasks become practised, and it reads as an IQ test | High | Fixed: Check cut |
| WS-4 | The premise and skill labels still implied the benefit | High | Fixed: decision row 1 states the limit, first screen says it, no skill labels, "level in this puzzle", new blurb |
| WS-5 | The words test would trip on `preventDefault` and `unique`, block its own citation, and miss "sharper", "brain training" and more | High | Fixed: one owner-approved strings file is the real control; word-start deny-list as a second net; allow-listed sources |
| WS-6 | ACTIVE first author is Coe, not Albert; booster-only caveat; switching and speed nulls omitted; no under-18 data; "fined" should be "settled" | Medium | Fixed in the research table and science page |
| WS-7 | "Spatial skills are an exception" read as a claim for Turn | Medium | Fixed: "nobody has tested whether this puzzle does" |
| WS-8 | Session level biased 0.5 to 1 level low, day 1 looked best, 72 to 90% of sessions used the fallback | High | Fixed: start at last level, turning-point mean with a minimum, rolling median, calibration not charted, numeric test |
| WS-9 | "20 trials or 3 minutes" didn't add up; switch cost from 20 cards was noise | Medium | Fixed: per-puzzle trial counts; no switch-cost number |
| WS-10 | Switch: ignoring the cue scored 75% | High | Fixed: at least 75% conflicting cards (62.5%), tested |
| WS-11 | Turn: only 2 usable shapes at 4 blocks, 6 at 5; 0° trials; angle not monotone | High | Fixed: 6 to 8 blocks, angle between pictures, never 0° |
| WS-12 | Stack levels 10 to 14 unreachable or not harder | Medium | Fixed: busy form cut; length 2 to 8 at two paces |
| WS-13 | Glimpse timing changes with refresh rate and battery saver | High | Fixed: Glimpse moved out of v1 with its timing listed as a precondition |
| WS-14 | Flash area used "a quarter of the screen"; real threshold is about 6% on a phone, 1.4% on a desktop | Medium | Fixed: 5% of viewport, app-wide, no stripes; desktop's lower figure accepted because nothing in v1 flashes faster than 1.25 a second |
| WS-15 | Glimpse copied the commercial speed exercise's structure; patent status unsourced | Medium | Fixed: out of v1, needs a recorded patent and trademark check and its own design |
| WS-16 | Matrix items unique to the solver but not to a person | Medium | Fixed: matrix task cut with the Check |
| WS-17 | Charts could show decline to kids or worried adults with no framing | Medium | Fixed: fixed line on every chart |
| WS-18 | v1 too big, no fun gate | Medium | Fixed: three puzzles, Stack-only PR 1, five-day owner playtest gate, keepsake for a reason to return |
| WS-19 | Safari clears storage after a week without a visit | Low | Fixed: `persist()`, install or export note, manual check |
| WS-20 | No way to leave a puzzle out; no keys defined | Low | Fixed: Settings toggle and named keys |

Fable re-checked Rodas 2024, the ACTIVE author list and Uttal 2013 online. Its own items marked
"from memory" (Safari's 7-day rule, iOS low-power frame rate, typical span) are treated as
likely and get verified during the build.

## Fable red team of Reveal (2026-11-11)

A second pass on the classic puzzle, with simulations of the generator. It found the generator
core sound and fast; the problems were in what the draft left undefined. What changed:

| ID | Finding | Severity | Status |
| --- | --- | --- | --- |
| RV-1 | "Same puzzle on every device" broke on any generator change, and an update could swap the puzzle under a half-done grid | High | Fixed: puzzle saved on first open, seed includes `GEN_VERSION`, seeded integer generator, golden test |
| RV-2 | "Abandoned" and the size rules were undefined (a 70%-clean player moved down 43% of the time under one reading) | High | Fixed: clean, helped, unfinished; up after 3 clean in a row, down after 2 helped or unfinished in a row, 5 clean to climb back; size setting |
| RV-3 | Reveal broke the set, results card, keepsake trigger and storage row | High | Fixed: Reveal sits outside the set, own status on the results card, own storage row, export version bump |
| RV-4 | Undefined smoothing made 5x5 dull and repetitive (46% with a blank line after one pass) | Medium | Fixed: no smoothing; mirror symmetry at 8x8 and up, reject blank or multiple full lines, solver-pass bands, no repeat within 30 days |
| RV-5 | "The line solver solves every kept grid" tested the filter with itself | Medium | Fixed: independent backtracking counter on every seed, the reverse check, single-line cases |
| RV-6 | "Today" undefined (UTC date bug, midnight, clock changes) | Medium | Fixed: local date, puzzle belongs to the day opened, future rows ignored, injected-clock tests |
| RV-7 | 10x10 cells fall to 23 px at 320 px wide; tap and drag undefined | Medium | Fixed: 10x10 only at 28 px cells or more, Fill/Dot switch, drag rules, row and column highlight, layout test |
| RV-8 | A hidden timer counted pauses and help days | Medium | Fixed: timer only while visible, clean days only, says so in help, can be turned off, no best time |
| RV-9 | Color-only clue greying, ambiguous keys, wrong "all need sight" line | Medium | Fixed: tick plus dim, named keys, labelled DOM grid, About line corrected, 12 px clue minimum |
| RV-10 | "Picture" overpromised, "1 to 10 minutes" wrong for 5x5, words test missed logic and wellness claims | Medium | Fixed: "pattern", corrected times, ten more banned stems, science page says the studies are about the drills, help renamed "Show a cell" |
| RV-11 | Brand list and the name "Reveal" need a recorded check | Low | Fixed: register check before PR 3, brand list also scans `src/` and `test/` |
| RV-12 | No cap on the rejection loop; no screen size for 12x12 and 15x15 | Low | Fixed: 200-attempt fallback with a test, 470 and 570 px thresholds |

