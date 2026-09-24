# Game Development Hackathon

## A 120-minute AI-assisted game jam

**Challenge:** Build a tiny browser game that makes connection fun. Deliver a playable loop, demonstrate deliberate collaboration with GitHub Copilot, and pitch what you learned.

**Recommended format:** Teams of 2-3; every team starts from scratch with an empty GitHub repository; GitHub as the source of truth; GitHub Copilot App or GitHub Copilot CLI as the primary AI workspace. This agenda assumes up to six teams pitching to one panel.

### Every team workstation

- Have Git, NodeJS, NPM package manager, a supported browser installed, and GitHub clone/push access ready.
- Install the [GitHub Copilot App](https://github.com/features/ai/github-app), the [GitHub Copilot CLI](https://docs.github.com/en/copilot/how-tos/set-up/install-copilot-cli), or both.
- **Optional**: Use PhaserJS https://github.com/phaserjs/phaser
- Be ready to initialize a small Phaser + TypeScript + Vite project and document the commands the team creates, such as `npm run dev`, `npm run build`, and `npm run test:e2e`.
- Install Playwright's required browser binaries ahead of time. Confirm automated interaction works through the corporate proxy and endpoint controls.
- Confirm local code review and at least one usable canvas. Teams using the CLI can open the Copilot App for the canvas exercise if their selected CLI workflow does not expose one.
- Confirm both selected models work with the same empty-repository baseline. Give each team the same request/time allowance.
- Rehearse a branch change, push, and GitHub pull request. Check target-branch permissions and any required workflow before the event.

**Readiness gate:** The team shows the organizer GitHub access, a working local Node/npm environment, one completed app interaction, and the ability to run a simple browser smoke test. Participants with incompatible machines pair on a prepared workstation; do not spend the game jam debugging installations.

### Organizer setup kit

Provide constraints, templates, and recovery material, not a finished competition game:

- A recommended Phaser version with matching documentation and a short from-scratch setup checklist.
- No backend, accounts, multiplayer, external runtime API, or asset-generation dependency.
- Guidance for adding a minimal HTML shell suitable for accessible controls/status, plus a seeded or controlled test scenario.
- A reference Playwright smoke-test pattern and browser configuration guidance. Participants create and document their own build/test commands.
- A lightweight pitch outline. Participants author their own project setup, instructions, and gameplay.
- A lightweight GitHub Actions pipeline if available; keep local checks runnable without waiting for CI.
- A rescue snippet or branch with a basic game loop, available to all teams if needed. Rescue behavior itself does not earn implementation credit.

## 2. Participant mission and scope contract

Build **one screen, one core mechanic, one 30-60 second round**. A player must be able to discover the controls, start, influence the result, reach an end state, and restart.

Choose one familiar mechanic: dodge, collect, deliver, or survive. Limit controls to arrows/WASD and at most one action button. No additional levels until the loop works.

Suggested activities:

These activities help teams explore GitHub Copilot, but they are not additional deliverables. The goal remains simple: build a game and present it.

1. Use the Copilot App or Copilot CLI as the primary AI workspace and Plan mode before gameplay implementation.
2. Write concise `AGENTS.md` and/or `.github/copilot-instructions.md` rules that the chosen app workflow actually loads.
3. Build a working game and preserve a known-good checkpoint.
4. Compare two explicitly selected models on the same bounded task.
5. Exercise gameplay with Playwright and a human player.
6. Perform a separate code-review pass and a rubber-duck discussion; act on the results.
7. Add purposeful game feel, without sacrificing usability.
8. Use an app canvas to inspect and improve an artifact.
9. Use an agent to assist integration into the team's GitHub delivery branch, followed by human approval.
10. Produce a one-page pitch or at most three slides and present the game.

**Canvas clarification:** Phaser's HTML canvas renderer does not satisfy the app-canvas requirement. Use the Copilot App's browser, document/editor, or another prevalidated canvas. Teams working primarily in Copilot CLI can use the Copilot App for this exercise. Creating a new canvas extension is not required.

**Data boundary:** Use invented data and original or appropriately licensed assets. No customer records, credentials, production systems, or unapproved code mirroring.

## 3. What matters

| Goal | What success looks like |
| --- | --- |
| Build a playable game | The objective and controls are understandable; input affects the game; a round reaches an outcome; restart works. |
| Make it enjoyable | Player actions have clear feedback, the game is readable, and the chosen mechanic feels satisfying. |
| Keep it reliable | The final version runs, survives a complete playthrough, and does not produce unexpected browser errors. |
| Present the result | The team demonstrates a short round and shares one useful thing learned while working with Copilot. |

## 4. Bonus

| Bonus | Idea |
| --- | --- |
| Custom agent | A focused role with suitable boundaries, actually invoked to produce a useful result. |
| Custom skill | A reusable procedure with a clear trigger and steps, actually used successfully. A prompt merely renamed "skill" does not count. |
| Inclusive play | One demonstrated improvement beyond the base controls: for example, reduced motion, remappable keys, or non-color-only cues. |

## 5. Make the constraints useful, not bureaucratic

### Instructions: short and demonstrable

Use one canonical instructions file; add a second only when the selected tool requires it. A `.github` directory can live in GitHub: the path is an assistant configuration convention, not a hosting requirement.

A quick example:

```text
Keep this a single-player, single-screen game using the pinned Phaser version.
State the smallest implementation plan and wait for approval before gameplay edits.
Do not add dependencies, network services, or external assets without approval.
Keep scoring and game-over rules separate enough to test deterministically.
Restart must reset score, timers, entities, listeners, and transient effects.
Use the documented build and Playwright commands before reporting completion.
Do not weaken tests to hide failures; report remaining failures explicitly.
Keep credentials and customer data out of code and prompts.
```

### The model duel: an experiment, not a benchmark

Spend at most ten minutes. Do not build two complete games.

- Freeze one baseline and choose a tiny task, for example: "Review restart handling and propose one minimal patch and a regression test."
- Open two fresh sessions with the same baseline, instructions, prompt, files and tools. Select Model A and Model B explicitly; do not use Auto for this comparison.
- Allow the same short time budget, one initial response and no unequal follow-up help. Separate worktrees or read-only proposed patches prevent cross-contamination.
- Compare correctness, relevance, patch size and test usefulness. Apply/run promising patches in isolation if time allows; label unexecuted proposals as unverified.
- Notice differences in speed or approach, but do not infer cost or treat one trial as a scientific performance ranking.
- If a model is unavailable, the organizer supplies the same alternate model pair to affected teams. If that is impossible, use a preprepared comparison pack of two outputs with identical provenance/context; equivalent points remain available.

Discuss what each model did differently and choose whichever response helps the game most.

### Playwright: prove behavior, not just pixels

Phaser game objects generally are not normal DOM elements. A screenshot or an assertion that a canvas exists does not prove gameplay works.

Each team should provide DOM controls/status or a documented, read-only test-state interface reflecting actual game state. Use real keyboard/pointer input and deterministic scenarios to check:

- Start changes the game to its playing state; input moves or otherwise changes the player.
- A known action produces the expected gameplay consequence, such as score or health change.
- A controlled short round reaches the correct outcome.
- Restart resets score, timer, entities and state; repeat restart to catch duplicated listeners.
- The exercised flow produces no unexpected page errors or console errors.

Do not expose arbitrary production state-mutation APIs just to pass tests. Do not replace actual play with a fake DOM status. Retain a result/trace or screenshot alongside assertions and test output.

Human playtest question: "Can a new player understand what to do within ten seconds?" Have the observer stay silent initially and improve the most obvious point of hesitation.

### Review and rubber-duck are different activities

**Review prompt:**

> Review this diff without editing. Prioritize defects in restart, timers, input, collisions and listener cleanup. Cite the relevant code and propose a way to reproduce each finding. Do not invent issues to fill a quota.

**Rubber-duck prompt:**

> I will explain how our round and restart work. Do not rewrite the code yet. Challenge one assumption at a time and help me identify an invariant we should test.

The participant explains first. Asking the agent to explain its own code is not the same learning exercise.

### Juice: a before/after, not a particle quota

Choose two small effects: a collection pop, brief hit flash, restrained particles, score-count animation, or a subtle sound with mute control. Preserve a before/after capture. Avoid violent screen shake, flashing effects, unreadable overlays, and autoplay audio.

Optional facilitator moment at minute 75: announce "Make every action readable." This is a polish prompt, not a surprise new feature requirement.

## 6. GitHub delivery and Agent Merge

Use the Copilot App or Copilot CLI against a local GitHub checkout for planning, editing, local review, and terminal/browser checks. Use the Copilot App when a canvas is required. Use GitHub's own PR interface or approved tooling for remote review and delivery. Do not assume GitHub-specific PR features operate on other hosting providers.

The documented native **Agent Merge** workflow operates on GitHub pull requests and waits for GitHub merge conditions. It is not established by that documentation as a general cross-platform feature.

For this event, replace the mandatory "Use Agent Merge" constraint with **agent-assisted integration**:

1. Keep a small feature branch and ask Copilot to inspect its changes against the target.
2. Let the agent prepare integration, resolve conflicts if any, and run relevant checks.
3. A human reviews the diff and authorizes delivery.
4. Push to GitHub, link the PR, and merge using the authorized GitHub workflow if permissions and checks allow.

No forced conflict is necessary. Do not bypass protected branches or approval rules. A policy-blocked PR may remain open with the final commit and blocker recorded.

If native Agent Merge is an important product learning objective, run a separate organizer demonstration on an approved, synthetic GitHub repository outside the competition clock. It earns no points and requires no customer-code mirroring. Do not call the GitHub substitute "native Agent Merge."

## 7. Present the game

Do not spend workshop time assembling a report. The game and the final presentation are the deliverables.

**Pitch format: one page or three slides maximum**

1. **The hook:** Game name, fantasy, controls and objective.
2. **Show it:** A short live round and restart.
3. **What we learned:** One model comparison, one defect or assumption caught, and one human decision that improved the agent's work.

Suggested 90-second delivery: 15 seconds hook, 45 seconds demo, 30 seconds learning. A recording is a useful fallback, but the frozen build must remain available for the playable-game eligibility check.

## 8. Facilitator operations and recovery

Before the day: validate the kit on representative managed laptops; confirm policies, GitHub permissions, model access and app features; publish the rubric and setup guidance; arrange one floating coach per roughly four teams.

During the event: show a countdown, check that teams are progressing toward a playable loop, and give equal access to rescue help. No surprise mechanic changes or late bonus announcements.

Recovery rules:

- **No loop at minute 50:** Cut to movement, one collectible/hazard, a timer and restart. Use the shared rescue branch if necessary; clearly identify inherited features.
- **Agent stuck for three minutes:** Ask for the smallest reproducible problem, revert only the team's failed patch to its checkpoint, or ask a coach. Do not regenerate the whole app.
- **Canvas fails:** Use the prevalidated alternate app canvas or prepared workstation. If an event-wide outage prevents the feature, award its five points uniformly and disclose it.
- **Playwright MCP fails:** Run the existing Playwright tests through terminal tools. Do not count a manual playthrough as an automated test.
- **GitHub/CI outage:** Preserve the local commit and local check output. Push later without pretending remote delivery already succeeded.
- **Model outage:** Use the alternate pair or common comparison pack described above.
- **At minute 90:** Stop adding mechanics. Spend the remaining build time on reliability, delivery and pitch.

After the event, summarize transferable practices rather than declaring a globally best model from a small game-jam experiment.

## 9. Product references and validation boundary

The plan is grounded in the following product documentation. Organizers must still rehearse their exact managed app build, operating systems and policy configuration; this document is not a claim that the customer's environment has already been tested.

- [Phaser repository and official setup guidance](https://github.com/phaserjs/phaser)
- [GitHub Copilot app setup, prerequisites and local/remote repository support](https://docs.github.com/en/enterprise-cloud@latest/copilot/get-started/quickstart-copilot-app)
- [Install GitHub Copilot CLI](https://docs.github.com/en/copilot/how-tos/set-up/install-copilot-cli)
- [Copilot app Plan mode and native Agent Merge for GitHub pull requests](https://docs.github.com/en/enterprise-cloud@latest/copilot/how-tos/github-copilot-app/managing-issues-and-pull-requests)
- [Copilot app canvases](https://docs.github.com/en/enterprise-cloud@latest/copilot/how-tos/github-copilot-app/working-with-canvas-extensions)
- [Custom-instruction support by tool](https://docs.github.com/en/enterprise-cloud@latest/copilot/reference/custom-instructions-support)
- [Copilot CLI planning, instructions and model selection](https://docs.github.com/en/enterprise-cloud@latest/copilot/how-tos/copilot-cli/cli-best-practices)
- [Copilot code review, including local IDE review paths](https://docs.github.com/en/enterprise-cloud@latest/copilot/how-tos/use-copilot-agents/request-a-code-review/use-code-review)
- [Playwright assertions and retry behavior](https://playwright.dev/docs/test-assertions)
