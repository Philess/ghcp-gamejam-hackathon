---
published: false
type: workshop
title: GitHub Copilot Game Jam - Participant Workshop
short_title: GitHub Copilot Game Jam
description: Build, test, review, and pitch a small browser game from scratch with GitHub Copilot.
level: intermediate
authors:
  - Philippe DIDIERGEORGES
contacts:
  - '@philess'
duration_minutes: 120
tags: GitHub, GitHub Copilot, AI, game development, TypeScript, Phaser, Playwright
navigation_levels: 3
navigation_numbering: false
---

# GitHub Copilot Game Jam

## Build a tiny browser game from scratch in 120 minutes

Your team will begin with an empty GitHub repository and use GitHub Copilot to design, build, test, review, and present a complete browser game.

The goal is not to create the largest game. The goal is to finish a clear, playable loop while showing deliberate collaboration between people and AI.

By the end of the workshop, your team should have:

- One screen and one core mechanic.
- A round lasting approximately 30-60 seconds.
- Clear controls, an objective, an end state, and a working restart.
- Project-specific instructions for GitHub Copilot.
- A documented comparison of two AI models.
- Automated gameplay checks with Playwright.
- Evidence from a human playtest, code review, and rubber-duck discussion.
- Two small game-feel improvements.
- A GitHub pull request containing the frozen version of the game.
- A 90-second pitch.

<div class="warning" data-title="Keep the scope small">

> Choose one mechanic: dodge, collect, deliver, or survive. Use arrows or WASD and no more than one action button. Do not add another level until the complete loop works.

</div>

## Workshop rules

1. Start from an empty repository. Every team creates its own project.
2. Use either the GitHub Copilot App or GitHub Copilot CLI as the primary AI workspace.
3. Use Plan mode before asking Copilot to implement gameplay.
4. Keep humans responsible for scope, acceptance, review, and delivery.
5. Do not use customer data, production credentials, private code, or unapproved assets.
6. Use original, generated, public-domain, or appropriately licensed assets.
7. Preserve a known-good commit before risky changes.
8. Stop adding mechanics when the facilitator announces the reliability phase.

## How you are judged

The detailed criteria are in the repository [README](../README.md#3-expectations). Judges will look for a playable loop, plan-first discipline, applied project instructions, a fair model comparison, meaningful Playwright checks, separate review and rubber-duck activities, purposeful game feel, a canvas-informed improvement, GitHub delivery, and a concise pitch.

A clean review can earn full credit when it is documented. Rescue code must be declared and does not earn implementation credit for inherited behavior.

## Manage your time - Schedule suggestion

| Time | Phase | Required outcome |
| --- | --- | --- |
| 0-15 min | Define and initialize | Game concept, repository, and running blank project |
| 15-30 min | Instruct and plan | Copilot instructions and an approved implementation plan |
| 30-60 min | Build the playable loop | Start, controls, mechanic, outcome, and restart |
| 60-80 min | Model duel | Same bounded task compared with two models |
| 80-90 min | Playtest and add game feel | One human observation and two purposeful feedback effects |
| 90-100 min | Test | Playwright checks proving the core behavior |
| 100-105 min | Review and explain | Code-review decision and rubber-duck insight |
| 105-110 min | Inspect and finalize | Canvas-based improvement and passing local checks |
| 110-120 min | Prepare delivery | Frozen commit, GitHub PR, evidence, and pitch preparation |

When the timers is exhausted, prepare to showcase your project in 2 minutes to the reste of the teams

# Before the timer starts

## Minimum prerequisites

| Requirement | Check |
| --- | --- |
| GitHub account with repository access | You can create, clone, push, and open a pull request |
| GitHub Copilot access | The Copilot App or Copilot CLI opens and can access your repository |
| Git | Git is installed and available to Copilot |
| Node.js and npm | A supported Node.js version and npm are installed |
| Supported browser | The browser can open a local Vite application |
| Playwright browser | The Playwright Chromium browser has been installed successfully before the event |

Recommended:

- Node.js 20 or later.
- A current Chromium-based browser.
- Phaser 3 with TypeScript and Vite.
- Teams of two or three people.

## Assign team roles

Choose lightweight roles. You can rotate them during the workshop.

- **Driver:** operates the computer and the selected Copilot App or Copilot CLI workflow.
- **Scope keeper:** protects the one-screen, one-mechanic constraint.
- **Tester/reviewer:** watches behavior, records evidence, and challenges assumptions.

For a two-person team, combine the scope keeper and tester/reviewer roles.


# Level 1: Define and initialize

## Step 1: Choose the smallest complete game

Agree on one sentence that describes the game:

> The player uses **[controls]** to **[action]** while trying to **[objective]** before **[end condition]**.

Examples:

- The player uses arrow keys to collect five signals before the timer expires.
- The player uses WASD to dodge moving hazards for 30 seconds.
- The player uses arrows and Space to deliver objects to matching zones.

Define acceptance criteria before writing code:

```markdown
- The game displays its controls and objective.
- The player can explicitly start the round.
- Player input changes the game state.
- The core mechanic affects score, health, progress, or time.
- The round reaches a visible win or loss state.
- Restart returns every relevant value and entity to its initial state.
```

Also write at least three non-goals:

```markdown
- No accounts, backend, database, or network API.
- No multiplayer.
- No additional levels.
- No complex asset pipeline.
- No mobile controls unless the core loop is already complete.
```


## Step 2: Create the project from scratch

Create or clone an empty GitHub repository. Open the repository with the Copilot App or launch Copilot CLI from its root, then ask:

```markdown
Initialize this empty repository as a Vite application using the vanilla TypeScript template.
Install the project dependencies, Phaser, and Playwright Test.
Do not overwrite any existing file without explaining why.
When finished, summarize the files and dependencies that were added.
```

Ask Copilot to start and verify the application:

```markdown
Start the development server and verify that the application loads in a browser.
Report the local URL and any browser or console errors.
Keep the server running only if it will be useful for the next steps.
```

Open the local URL and confirm the page loads before adding gameplay.

Create the GitHub repository without a README, `.gitignore`, or license so the clone is empty. If Vite reports that the directory is not empty, cancel, remove or relocate the unexpected files, and rerun the command. Do not overwrite files you intend to keep.

## Step 3: Establish the first checkpoint

Ask Copilot to establish the base and delivery branches:

```markdown
Review the current changes and make sure generated dependencies or temporary files are not included.
Commit the running blank application to the main branch with the message "Initialize browser game".
Push main to the GitHub remote.
Then create and switch to a new branch named game.
```

This creates the target `main` branch and a `game` delivery branch. Later, your pull request will merge `game` into `main` in your own repository.

**Checkpoint:** You have a blank application running in a browser and pushed to GitHub.

# Level 2: Instruct and plan

## Step 1: Add project instructions

Create `.github/copilot-instructions.md`. An `AGENTS.md` file is also acceptable if your selected Copilot workflow loads it, but use one canonical project-instructions file and record its path.

You can take inspiration and adapt from the following instructions to your game:

```markdown
# Project instructions

- Keep this a single-player, single-screen browser game.
- Use the installed Phaser version, TypeScript, and Vite.
- State the smallest implementation plan and wait for approval before gameplay edits.
- Do not add dependencies, services, external assets, or network calls without approval.
- Keep game rules separate enough to test deterministically.
- Keep the controls and objective visible in the page UI.
- Expose only read-only game state needed for automated testing.
- Restart must reset score, timers, player state, entities, listeners, and transient effects.
- Run the documented build and Playwright commands before reporting completion.
- Do not weaken tests to hide failures.
- Report errors and unfinished work explicitly.
- Keep credentials, private code, and customer data out of code and prompts.
```

The instructions should describe your actual project. Remove rules that do not apply and add rules for your chosen mechanic.

## Step 2: Ask Copilot for a plan

Open the repository in the GitHub Copilot App or launch GitHub Copilot CLI from the repository root, then start in Plan mode.

This is an example of a sample prompt you can use:

```markdown
We are building a small browser game from scratch

Game concept:
[Paste your one-sentence game description.]

Acceptance criteria:
[Paste your acceptance criteria.]

Non-goals:
[Paste your non-goals.]

Inspect the current repository and propose the smallest implementation plan.
Include:
- the minimum file structure;
- the game states and transitions;
- deterministic game rules;
- restart cleanup;
- visible DOM status for accessibility and Playwright assertions;
- the smallest useful automated tests.

Do not edit files yet. Identify risks and ask us to approve the plan.
```

Review the plan as a team.

Before approval, check:

- Does it fit one screen and one mechanic?
- Can the first playable loop be finished by minute 65?
- Does it avoid unnecessary dependencies?
- Is restart behavior explicit?
- Is there a testable state or visible status?
- Did Copilot invent requirements you did not request?

Reject or simplify anything that exceeds the scope.

## Step 3: Approve implementation

When the plan is ready, DON'T validate the implementation imediately but ask Copilot to implement only the first playable slice:

```markdown
Implement the approved plan in the smallest playable increments.

First make the page load with visible controls and a Start action.
Then add player input and the core mechanic.
Then add the end state and restart.

After each increment, run the smallest relevant check and stop if it fails.
Do not add polish, assets, or additional mechanics yet.
```

**Checkpoint:** Your instructions file is committed, and the team has approved a bounded implementation plan.

# Level 3: Build the playable loop

## Your challenge

Turn your approved plan into the smallest complete game you can finish.

How you organize the code and collaborate with Copilot is up to your team. Keep asking whether each change brings you closer to a complete playable round.

Your game should let a new player:

- Understand the objective and controls.
- Start a round.
- Influence what happens.
- Reach a visible outcome.
- Restart without refreshing the page.

## Hints

- Get one complete loop working before adding visual polish.
- Keep important state observable so that people and automated tests can understand what happened.
- Try restart repeatedly; duplicated timers, entities, or listeners often appear only on the second round.
- Preserve a known-good commit when the loop becomes playable.
- If Copilot proposes a large architecture, challenge it to find a smaller path.

**Evidence:** Record the playable commit and any major scope decision in `HACKATHON.md`.

**Checkpoint:** Someone outside the implementation can play a complete round without coaching.

# Level 4: Run the model duel

## Your challenge

Use two named models on the same small task and decide which response is more useful for your game.

Choose a task that can be understood and evaluated quickly, such as reviewing restart behavior, diagnosing one defect, simplifying one area, or suggesting one regression test.

Keep the comparison fair:

- Use the same commit, context, instructions, prompt, tools, and time limit.
- Do not use Auto.
- Give each model one initial response without unequal follow-up help.
- Judge the result rather than the model's reputation.

Consider correctness, relevance, simplicity, testability, and respect for your project instructions. You may accept one answer, combine ideas, or reject both.

<div class="info" data-title="This is not a benchmark">

> One short trial cannot establish that a model is universally better. Report what happened on this task and baseline only.

</div>

**Evidence:** Complete the model comparison table in `HACKATHON.md` and record your decision.

**Checkpoint:** Another team could understand why you preferred one response.

# Level 5: Playtest and add game feel

## Your challenge

Let someone who did not drive the implementation try the game. For the first ten seconds, do not explain anything.

Observe where they hesitate, what they misunderstand, and whether the game clearly communicates actions, danger, progress, success, and failure.

Use the remaining time to improve readability and game feel. Choose small effects that support the mechanic rather than distract from it.

## Hints

- Ask: "Can a new player understand what to do within ten seconds?"
- Favor feedback tied directly to player actions.
- A small animation, restrained particle effect, score response, transition, or optional sound can be enough.
- Avoid rapid flashing, violent screen shake, unreadable overlays, and autoplay audio without mute control.
- It is valid to reject playtest feedback when you can explain why it falls outside the scope.

**Evidence:** Record one observation, the decision it produced, and the two feedback improvements in `HACKATHON.md`.

**Checkpoint:** The game communicates its rules and reactions more clearly than before the playtest.

# Level 6: Test, review, and rubber-duck

## Your challenge

Build confidence in your game using three different perspectives:

1. **Automated proof:** Use Playwright to exercise real input and prove meaningful behavior.
2. **Independent review:** Ask a fresh Copilot session to review the diff without editing it.
3. **Rubber-duck discussion:** Explain one important part of the game while Copilot challenges your assumptions.

Decide what the highest-value checks are for your mechanic. At minimum, your automation should prove that the game starts, reacts to input, restarts, and produces no unexpected browser errors. A test that only checks for a canvas is not sufficient.

For review, focus on high-risk areas such as state reset, timers, listeners, collisions, and outcome transitions. A clean review is acceptable; invented findings are not.

For the rubber-duck activity, the participant explains first. Try to discover one invariant that should always remain true.

## Hints

- Keep automated scenarios deterministic and short.
- Use visible status or a read-only state interface when canvas pixels are not enough.
- Do not weaken tests just to make them pass.
- Fix the highest-confidence review finding, or record why you rejected it.
- Preserve test output, a trace, or a screenshot when useful.

**Evidence:** Record build and test results, the review decision, and the rubber-duck insight in `HACKATHON.md`.

**Checkpoint:** Your team can explain why the frozen game is reliable, not merely why it appears to work.

# Level 7: Inspect and finalize

## Your challenge

Use a Copilot App canvas to inspect something that matters to your submission. This could be the running game, your evidence file, the pitch, a diagram, or a test artifact. The Phaser rendering canvas itself does not count.

If you worked primarily with Copilot CLI, open the relevant repository artifact in the Copilot App for this activity.

Make one improvement because of something you noticed in the canvas.

Then decide whether the game is ready to freeze. Run the relevant automated checks, play one final round, inspect the final diff, and fix only release-blocking problems.

## Hints

- Do not add another mechanic during finalization.
- Check restart more than once.
- Look for browser errors and accidental files in the final diff.
- Ask Copilot to commit and push only after a human reviews the final state.
- Record the exact frozen commit.

**Evidence:** Record the canvas used, the improvement it informed, final validation results, and the frozen commit SHA.

**Checkpoint:** The frozen commit is pushed, reproducible, tested, and playable.

# Level 8: Deliver and pitch

## Your challenge

Deliver a reviewable frozen version and prepare a short live pitch.

Ask Copilot to help inspect the `game` branch against `main`, summarize the work, and prepare a pull request. A human must review the final diff and proposed pull request before it is created. Do not bypass repository protections or merge conditions.

Your pull request should make it easy for someone else to understand how to run and judge the game. Include the hook, controls, objective, validation results, known limitations, `HACKATHON.md`, and frozen commit.

For the pitch, show the game rather than describing the implementation. Cover:

- What the player does.
- One short round and restart.
- One useful lesson from the model comparison.
- One defect, assumption, or decision that improved the result.

Use one page or no more than three slides, and stay within the facilitator's time limit.

## Final submission checklist

- [ ] A new player can understand, play, finish, and restart the game.
- [ ] Project-specific Copilot instructions are present.
- [ ] The model comparison is fair and documented.
- [ ] Playwright proves meaningful gameplay behavior.
- [ ] Human playtest, review, and rubber-duck evidence is recorded.
- [ ] The final build and tests have recorded results.
- [ ] The pitch is ready and fits the facilitator's time limit.

# Recovery guide

## No playable loop by minute 50

Cut scope immediately:

- Keep movement.
- Keep one collectible or hazard.
- Add one timer or score target.
- Add an outcome and restart.

Remove assets, menus, extra enemies, levels, and secondary mechanics.

Ask a coach for the shared rescue branch or rescue snippet if the reduced loop is still blocked. Declare every inherited feature in `HACKATHON.md`; inherited behavior does not earn implementation credit.

## Copilot is stuck

After three minutes without progress:

1. Stop the broad request.
2. State the smallest reproducible problem.
3. Provide the relevant file and exact error.
4. Ask for one diagnosis and one minimal patch.
5. Restore your known-good commit if the attempted change made the game less stable.

Do not ask Copilot to regenerate the entire application.

## Playwright integration is blocked

Ask Copilot to run the existing browser test through the available terminal tools and keep the test as small as possible. If automation remains blocked, preserve:

- The command and full error.
- The attempted test.
- A manual playthrough result.

A manual playthrough does not count as an automated test, but honest evidence is better than claiming an unverified result.

## A canvas is unavailable

Use the facilitator's prevalidated alternate app canvas or a prepared workstation. Record the outage and the alternate canvas used.

## GitHub or CI is unavailable

Preserve:

- The local frozen commit.
- Local build and test output.
- The attempted push or pull-request error.

Push when service returns. Do not claim that remote delivery succeeded before it does.

## A selected model is unavailable

Use the facilitator's alternate model pair or common comparison pack. Apply the same prompt, baseline, context, and evaluation criteria.

# Bonus challenges

Attempt bonuses only after the required submission is complete.

## Custom agent

Create and use a narrowly scoped agent, such as:

- Restart auditor.
- Playwright gameplay tester.
- Accessibility reviewer.
- Pitch editor.

Document what the agent produced and why the custom role was useful.

## Custom skill

Create a reusable procedure with:

- A clear trigger.
- Defined inputs.
- Ordered steps.
- A verifiable output.

Use it successfully during the workshop. A saved prompt renamed as a skill is not sufficient.

## Inclusive play

Demonstrate one improvement beyond the base controls:

- Reduced-motion mode.
- Remappable keys.
- Non-color-only status cues.
- Mute control.
- High-contrast mode.
- Keyboard-accessible menus.

# Product references

- [Phaser repository and setup guidance](https://github.com/phaserjs/phaser)
- [GitHub Copilot app quickstart](https://docs.github.com/en/enterprise-cloud@latest/copilot/get-started/quickstart-copilot-app)
- [Install GitHub Copilot CLI](https://docs.github.com/en/copilot/how-tos/set-up/install-copilot-cli)
- [Managing issues and pull requests with the Copilot app](https://docs.github.com/en/enterprise-cloud@latest/copilot/how-tos/github-copilot-app/managing-issues-and-pull-requests)
- [Working with canvas extensions](https://docs.github.com/en/enterprise-cloud@latest/copilot/how-tos/github-copilot-app/working-with-canvas-extensions)
- [Custom instructions support](https://docs.github.com/en/enterprise-cloud@latest/copilot/reference/custom-instructions-support)
- [Copilot CLI best practices](https://docs.github.com/en/enterprise-cloud@latest/copilot/how-tos/copilot-cli/cli-best-practices)
- [Requesting a code review](https://docs.github.com/en/enterprise-cloud@latest/copilot/how-tos/use-copilot-agents/request-a-code-review/use-code-review)
- [Playwright assertions](https://playwright.dev/docs/test-assertions)
