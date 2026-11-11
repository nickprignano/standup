# Instructions for AI assistants

Standup is a browser puzzle game: three short daily drills and a daily picture-logic puzzle.
Plain JavaScript, DOM and canvas, no build step, served as static files. The plan is in
[docs/SPEC.md](docs/SPEC.md); read it first.

- It's our own work under the MIT license: our own versions of published lab tasks and of the
  generic picture-logic puzzle. No names, game names, art, sounds or terms from commercial
  brain-training apps or puzzle brands; the words test keeps them out of shipped files.
- No claims beyond the evidence. The game never says it improves memory, intelligence, focus or
  health, and never mentions a medical condition. Every player-facing word lives in
  `data/strings.json` or `data/science.json`, which the owner approves word by word. A change
  that weakens the claim rules or the words test needs the owner's explicit yes.
- Made for 13 and up. Keep the flash and pattern rules in the spec true.
- Nothing leaves the player's device: no analytics, accounts, server, AI or network calls beyond
  the pinned theme files.
- Never put API keys, account or tenant IDs, domains other than the game's own, IPs, emails,
  secrets, or employer, customer or private-project names in the repo, commits, issues or PR
  text.
- Never ask for, show or store a secret in chat. The owner runs the step that handles it.
- Propose changes as pull requests. Never change a real account, deployment or spend setting
  without the owner's explicit yes.

## How to make a change

Four rules after the community "Karpathy guidelines" (MIT), reworded for agents that work unattended.

- Say what you assumed. When the ask leaves a detail open, pick the reasonable default, say which,
  and keep going. Stop to ask only when the choice changes the goal, something the owner will
  notice, or a step no one can undo; if no one is there to answer, do the reversible part and leave
  the question in the PR body. If a simpler way exists than the one asked for, say so.
- Write the least code that does the job: no features, options or abstractions nobody asked for,
  and no handling for cases that can't happen.
- Touch only what the task needs and match the style around it. Every changed line should trace
  back to the ask. Mention unrelated dead code instead of deleting it; remove only what your own
  change left unused.
- Before you start, name the check that proves the task is done (a failing test, the "Checks to
  run" below, an expected output), and don't call it done until it passes in front of you.

## Checks to run

```bash
node --test
```
