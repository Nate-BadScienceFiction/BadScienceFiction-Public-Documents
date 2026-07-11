# Implement Underwall in one controlled Claude Code delivery cycle

## Objective

Implement a complete, playable, end-to-end prototype of the latest canonical design in:

`C:\Users\natha\Dev\GITHUB_DESKTOP\AkiyaBlocks-Stories\HEROS_GAME.MD`

The playable scene belongs in:

`C:\Users\natha\Dev\GITHUB_DESKTOP\AkiyaBlocks-MiddleKingdom`

The reusable game engine is:

`C:\Users\natha\Dev\GITHUB_DESKTOP\AkiyaBlocks`

Use the existing Middle Place scene as the foundation. Follow the current engine's architecture, scene-authoring model, input grammar, save/persistence conventions, build pipeline, visual language, and performance contracts. Reuse existing mechanics and extension patterns wherever possible.

Implement the whole required path from first control through `returned`, including Gate 0 and Passes 1–5. Prioritize correctness, playability, recovery, and a complete canonical route over optional polish. Do not omit a required beat merely to produce a shallower demo.

## One-pass execution discipline

Treat this as one controlled implementation campaign. Do not request routine human approval between mapping, gates, passes, validation, or repairs. Complete Gate 0 and Passes 1–5 in sequence, repairing failed gates and rerunning cumulative tests before advancing.

The campaign spans one human authorization, one coordinated Claude Code run/session that may resume after infrastructure interruption, one implementation branch or existing authorized working branch, staged internal gates, and one final delivery after acceptance passes. "One cycle" does not mean one model response or one undifferentiated edit. Use as many internal tool calls, builds, tests, focused subagents, repairs, and regression loops as necessary.

Pause only when completion requires new authority, a destructive or external action, unavailable credentials or repositories, or a consequential specification decision that cannot be resolved from Section 16, existing engine contracts, or the bounded specification-gap policy.

The four roles are responsibilities owned by the primary session, not mandatory long-running agents. Use focused subagents only for bounded repository exploration, consequential counterfactual review, isolated test execution, or independent final playtesting. Do not create agent orchestration merely to satisfy the role names. Prefer focused subagents with isolated context over an experimental agent team unless genuine parallel, non-overlapping work makes a team clearly safer.

Keep the Architecture Mapper concise and execution-oriented. Map enough of the design to establish repository ownership, extension points, likely files, consequential risks, and acceptance tests, then begin implementation. Map at the subsystem and contract level rather than producing a second design document or cataloguing every narrative beat.

Use the Counterfactual Critic only when a requirement has multiple credible implementations or affects engine ownership, persistence, player recovery, baked content, or another difficult-to-reverse contract. Once a mapping is selected, implement it and keep the decision closed unless build, test, or play evidence materially invalidates it.

Before substantial quest work, add only the minimum test adapter needed to create a clean world, apply legal actions, advance time through supported mechanisms, save and reload, inspect state for assertions, capture errors, and take screenshots. The production runtime is the system under test; Section 16, Section 14 invariants, and explicit acceptance assertions define expected behavior. Do not build a parallel quest implementation or a second general-purpose rules engine.

For each intermediate pass, run its deterministic acceptance tests plus no more than three targeted adversarial perturbation scenarios covering the new or changed mechanics. Do not rerun three full persona playthroughs after every pass. After Pass 5, run complete YOLO, Optimizer, and Explorer simulations independently from clean states, with three to five perturbations per run and no shared discoveries.

A gate fails when a build, bake, package, canonical invariant, required-route, determinism, crash, softlock, or unresolved `BLOCKER` or `MAJOR` test fails. Repair the failure and rerun the gate; an ordinary implementation failure is not a reason to mark the campaign `BLOCKED`.

`FRICTION` and `POLISH` findings do not normally block advancement unless they obscure required progression, prevent naive-player recovery, violate an explicit presentation rule, or cause a required acceptance test to fail. Mark the campaign `BLOCKED` only when the remaining problem requires unavailable external state, new authority, or a consequential design decision the prompt does not authorize.

Create `IMPLEMENTATION_REPORT.MD` when implementation begins and maintain its gate-status section as work proceeds so the session can resume after interruption without repeating repository discovery. Do not stop after planning, scaffolding, test creation, a successful vertical slice, or partial implementation.

Run this work in Claude Code ultracode mode (`--effort ultracode`) or the highest available effort level.

---

## Source authority and scope

Read `HEROS_GAME.MD` completely before making production changes. Use this precedence when interpreting it:

1. **Section 16, "The committed rules," is the canonical implementation contract.**
2. **Section 14 defines required tests and invariants.**
3. **Section 13 defines implementation order and pass success criteria.**
4. **Section 10 defines technical ownership and integration direction.**
5. Earlier sections define story, place, tone, intended experience, and rationale. They may clarify the canonical rules but may not override them.
6. Revision 12 and Revision 13 corrections are mandatory regressions.

Do not implement retired systems, even if an earlier narrative section or another repository document mentions them. In particular, do not revive alternate entrances, combat, damage from the Count, a resource economy, humanoid quest-givers, a roaming Spitball chase, random lies, random tunneling, reusable Qyber, hidden arrival-direction gates, or failure that permanently damages the scene.

Treat `HEROS_GAME.MD` as read-only during implementation. Record implementation discoveries and genuine gaps in `IMPLEMENTATION_REPORT.MD`; do not silently redesign the source document.

---

## Repository safety and ownership

Before editing either repository:

1. Inspect repository instructions, `CLAUDE.md` files, package scripts, build tools, tests, scene-generation tools, and relevant architecture.
2. Inspect `git status` in both repositories.
3. Preserve all pre-existing and unrelated work. Never reset, discard, overwrite, or reformat unrelated changes.
4. Do not use destructive Git commands. Do not push, deploy, publish, or open a PR unless separately authorized.
5. Keep both repositories buildable and runnable throughout the implementation.

Apply this ownership rule:

> If it has authored coordinates or belongs only to Middle Place, it belongs in `AkiyaBlocks-MiddleKingdom`. If it is reusable stateful capability that conforms to an existing engine contract, it belongs in `AkiyaBlocks` and must be consumed through the engine's normal public extension path.

Accordingly:

- Middle Place geometry, `underpath-v1` data, seams, evidence, rings, perches, sightlines, encounter locations, return waypoints, scene copy, and scene-specific quest configuration belong in the game repository.
- Generic runtime hooks, descriptor contracts, persistence support, test adapters, or reusable UI capabilities belong in the engine only when they are genuinely reusable and match existing architecture.
- Do not hardcode Middle Place checks into generic engine systems when descriptor data or a scene runtime can own the behavior.
- Do not create a parallel quest engine, input layer, lighting system, save system, companion framework, modal framework, or test framework.
- If the engine already provides the needed capability under a different name or shape, map the design onto it rather than duplicating it.

If a proposed engine modification is scene-specific, difficult to reverse, or widens an engine contract, send it through the Counterfactual Critic before implementation.

---

## Leadership workflow

Use four cooperating leadership roles in this order:

`Architecture Mapper → Counterfactual Critic → Implementation Agent → Playability Validator`

The primary Claude Code session owns sequencing, scope, gate state, integration, and final delivery. It may create additional focused agents for repository exploration, isolated test execution, visual review, or adversarial analysis, but those helpers do not replace the four leadership responsibilities.

Do not use agent review for routine implementation decisions. Challenge only mappings that are ambiguous, consequential, cross-repository, player-visible, persistence-sensitive, or difficult to reverse.

### 1. Architecture Mapper

The Architecture Mapper is read-only. It must inspect both repositories and map every required subsystem to current code before production edits begin.

Produce a concise implementation map covering:

- Middle Place scene descriptors and scene runtime ownership
- the existing Night Moves runtime and `nightPhaseAt` access
- companion member indexing, suppression, perch/pose overrides, and restoration
- Scan Device inputs, field display, raycasts, pins, and modal behavior
- Moon Ledger state, observations, trance, and local contextual waits
- kiln material-loadout and quest-row extension points
- block placement, break precedence, provenance, `editStore`, and reload reconciliation
- scene baking, districts, sky occlusion, local lights, evidence proxies, and package verification
- save schema, versioning/migration expectations, and deterministic time-boundary processing
- browser/headless test infrastructure, screenshot tooling, and normal build/test commands
- exact ownership for `underpath-v1`, Underwall runtime state, UI copy, and tests

For each mapped subsystem or consequential contract, record:

- existing system or extension point
- owning repository and likely files
- mapping confidence
- whether an engine change is actually required
- tests that will prove the mapping
- consequential ambiguity, if any

Use parallel read-only exploration when helpful, especially to inspect the game and engine repositories independently. Return one compact map to the primary session and fold its material decisions into `IMPLEMENTATION_REPORT.MD`; do not create a second design document. Then advance.

### 2. Counterfactual Critic

The Counterfactual Critic reviews only mappings that meet at least one of these conditions:

- ambiguous ownership between game and engine
- save/reload or time-boundary consequences
- likely to create a softlock or sequence break
- changes an existing engine contract
- difficult to reverse after content is baked
- depends on hidden player knowledge
- could conflict with free sandbox placement or breaking
- has materially different plausible implementations

For each challenged mapping:

1. State the selected mapping.
2. Test one plausible alternative.
3. Consider out-of-order action, missed cue, repeated action, retreat, reload, time jump, partial completion, player-built obstruction, and failure midway where relevant.
4. Identify hidden knowledge, contradictory state, duplicate triggers, sequence breaks, or scene-specific engine hacks.
5. Recommend exactly one concrete mapping and its acceptance test.

Do not reopen settled story choices or propose sweeping redesigns. Finish the critique, feed its decisions into the implementation map, and continue. Reopen a selected mapping only if build, test, or play evidence materially invalidates it.

### 3. Implementation Agent

The Implementation Agent performs the selected mappings and owns fixes returned by validation.

Requirements:

- Follow existing code style, module boundaries, data formats, and build conventions.
- Implement descriptor-driven scene behavior and narrow reusable hooks.
- Keep Night Moves read-only and phase-pure.
- Preserve shipped inputs; add no quest-only control.
- Preserve normal sandbox building, kiln use, time, and surface exploration.
- Implement persisted and derived state exactly as Section 16 specifies.
- Make save/reload, trance, local waits, dawn/dusk boundaries, and interrupted contacts deterministic.
- Use test-only instrumentation only in development/test builds and through existing debug/test conventions.
- Avoid broad refactors not required for Underwall.
- Avoid placeholder behavior on the required path.
- Keep both repositories runnable after every internal checkpoint.

### 4. Playability Validator

The Playability Validator is independent and read-only with respect to production code. It reports failures to the Implementation Agent, which fixes them; the Validator then retests.

The Validator must not receive `HEROS_GAME.MD`, implementation source, hidden quest flags, future objectives, other players' discoveries, or design rationale. It may receive only what an actual player could perceive plus the action vocabulary made available by the running game or test adapter.

Validate:

- the complete intended route
- out-of-order work
- failed interactions
- missed and forgotten cues
- repeated actions
- revisited locations
- obvious alternate routes
- legal sandbox obstruction
- anchor removal and replacement
- modal and dialogue interruption
- time jumps and missed windows
- save/reload before, during, and after meaningful transitions
- post-completion ordinary play

Report crashes, softlocks, hidden-knowledge requirements, duplicate rewards or contacts, broken state transitions, stale UI, contradictory world/state feedback, missing recovery, and unclear required progression. Classify each as `BLOCKER`, `MAJOR`, `FRICTION`, or `POLISH`, and cite the exact trace and state transition.

---

## Build the verification runway first

Before substantial quest implementation, create or extend only the minimum executable Underwall verification harness needed by the gates, using the repositories' existing test conventions.

The harness must provide:

1. **Deterministic acceptance assertions** for canonical quest events, guards, effects, visible feedback, persisted state, derived state, and invariants without duplicating production behavior.
2. **A test-world adapter** that can start from a clean Middle Place state, observe player-visible state, apply legal inputs/actions, advance time, save/reload, and capture relevant runtime state for assertions.
3. **Pass-specific gate commands** for Gate 0 and Passes 1–5.
4. **A cumulative acceptance command** that reruns all completed gates.
5. **Machine-readable reports** plus concise human-readable failure summaries.
6. **Screenshot or frame capture** at actual desktop and mobile-width cameras for presentation-sensitive gates.

Prefer a thin adapter over a second implementation of the game. The production runtime is the system under test. Section 16, Section 14, and explicit acceptance assertions define expected behavior; the test adapter observes and drives the runtime rather than recreating it.

If Akiyablocks is browser-based, expose a test-only API through the existing debug/test architecture rather than shipping global debug state. It should support the equivalent of:

- create a clean world
- obtain a player-visible observation
- apply a player input or bounded test action
- set or advance ordinary time through legal mechanisms
- save and reload
- inspect persisted and derived state for referee assertions
- capture a screenshot and relevant console errors

Do not allow playtester agents to call hidden-state inspection methods. Only the referee/test runner may use them.

If Claude Code project-local hooks are already supported safely, configure a local-only completion check so the primary session cannot finish while the cumulative acceptance command fails. Do not modify global Claude Code configuration. Whether or not a hook is available, the primary session must enforce the same rule itself.

Add a circuit breaker: after repeated attempts produce the same genuine external, architectural, or specification blocker, record complete evidence and stop as `BLOCKED` rather than looping indefinitely. Test failures and difficult implementation work are not blockers by themselves.

---

## Observation-only agentic playtests

Create three independent playtester policies or subagents. Start every run from the same clean state. Do not share transcripts, discoveries, memory, or hidden state across runs.

### YOLO Player

Seeks danger, novelty, spectacle, shortcuts, premature interaction, amusing consequences, demolition, unusual building, and surface travel. Often ignores instructions and tests whether freedom is real.

### Optimizer

Tries to reach the current pass endpoint and final ending with minimum time, travel, dialogue, optional observation, and retries. Skips anything that appears optional, uses time controls aggressively, and abandons weak-feedback interactions.

### Explorer

Follows environmental and narrative clues, inspects named sources, scans evidence, investigates side paths, revisits objects, experiments with lights and anchors, and seeks optional context without design knowledge.

For each meaningful decision, give the player only an observation packet containing information such as:

- visible location and geometry
- objects currently in view or under the reticle
- visible field-strip and Ledger copy
- current hotbar/loadout and control glyphs
- audible or visible events
- the player's own retained discoveries
- recent action feedback

The player must return:

- its decision
- the visible reason for the decision
- one legal input/action
- any uncertainty or mistaken belief

The referee applies the action, checks the canonical result, updates only legitimately acquired player knowledge, and records the state difference. Flag any action whose rationale requires hidden document knowledge.

During each intermediate pass, run no more than three deterministic, targeted perturbation scenarios total across the new or changed mechanics. After Pass 5, run each complete player simulation with three to five perturbations selected from:

- missing a subtle cue
- misunderstanding an ambiguous line
- selecting the wrong nearby face
- mis-aiming a placement
- placing a block over an active or future interaction
- forgetting a weak clue
- reclaiming a required anchor
- opening a modal or trancing during a timed contact
- reloading during a modal, contact, pulse, seam, rehearsal, or handshake
- arriving early or leaving midway
- repeating an already committed interaction
- taking the overland route
- missing a phase window or pulse

Resolve perturbations only through documented mechanics. An undefined required outcome is an implementation gate failure.

Meaningful decisions change position, knowledge, strategy, inventory/loadout, resources, or game state. Do not count individual repeated seam-block clicks as separate strategic decisions. For the final full run, continue each player until `returned`, a genuine softlock, reasonable abandonment, or 50 meaningful decisions.

Retain concise chronological traces with:

- visible situation
- player decision and visible reasoning
- action
- result
- relevant state change
- player knowledge change
- perturbation, if any
- issue and severity, if any

LLM or policy playtests supplement deterministic assertions; they do not replace them.

---

## Internal implementation gates

Execute the following in order. Do not proceed past a failed gate. Fix failures in the current pass and rerun both that gate and every earlier regression gate. A failed gate is work to repair, not a campaign blocker; use `BLOCKED` only under the bounded conditions in the one-pass discipline and specification-gap policy.

### Gate 0 — bake-and-feel spike

Implement the throwaway physical spike exactly as Section 13 requires before quest code:

- 24-block, 3-wide by 4-high tunnel
- daylit mouth and properly dark interior
- one 3 by 4 seam
- one dry floor stripe
- one 5 by 5 work bay
- shared sky occlusion and shipped green-eye lighting

Verify the real bake/package pipeline, `skyQuant` expectations, cross-chunk feathering, player clearance, aimability, placement/reclaim, light ranking, evidence readability, and desktop/mobile screenshots.

If the dark does not read, required faces receive accidental shaft light, movement/aiming is unreliable, the next floor cannot be found from the edge of a totem pool, or local-light ranking starves nearby lamps, fix the bake/lighting before writing quest code. Do not compensate with scene-wide cave fog.

### Pass 1 — One Night Under vertical slice

Implement the complete opening through `local_method_learned`:

- shipped control contract
- unrestricted first control and opening alternatives
- zero embodied humanoid NPCs
- two-dusk Wall Watch
- paired-orbit observation and fallback
- Call, named absence, serialized Penelope/Harriet contacts
- interrupt-safe Call presentation
- entrance calibration and order tolerance
- S1/S2, first work light, J1 anchor, and C1
- entrance outrun recovery and active-interaction obstruction
- return home and Night 1 chapter close

Gate: a naive player can discover the controls, finish the required work, return safely, and explain in ordinary language that SKY locates an area, GROUND proves a mark, an ordinary totem lights anywhere, and a ring totem becomes an anchor.

### Pass 2 — full ground

Implement and validate:

- complete approximately 205-block underpath spine
- 3 by 4 route clearance and 5 by 5 work bays
- five required seams plus optional W1
- dry-stripe continuity
- three junctions and authored shafts
- arroyo gap and side-ramp recovery
- wrong pocket
- dead-rock band and provenance exception
- seam-tight dig zones and disjoint evidence
- phase seam prep/gate partitions
- exact break precedence and obstruction clearance sets
- save/load reconciliation from physical edits

Gate: every required dig is aimable, physically recoverable, and motivated by visible local evidence; no player needs random excavation or can bypass a locked cap.

### Pass 3 — instruments, relay, and second lesson

Implement and validate:

- source-gated ROUTE targets and stable error law
- GROUND and SKY rules
- ordinary lights versus J1/J2/J3 anchors
- empty-ring precedence and known-ring recovery
- C1, C2, and supporting optional facts
- false relay and shared refusal grammar
- Qyber review, modal close/reload, retained corner, and repeat status
- signal burn
- S3/S4 and Night 2 phase behavior
- kiln first-light preparation and phrase-three rehearsal
- slot 4 reservation
- progression through `seal_prepared`

Gate: a naive player can apply the rule `official answers need local proof`, recover from skipped anchors and interrupted interactions, and prepare the seal without hidden knowledge.

### Pass 4 — Night 3 and recovery

Implement and validate:

- Night 3 arming and physical-state-correct J3 cue
- FAR EXIT target, arroyo crossing, and S5
- retained official C3 claim
- in-shaft pulse plus fresh-scorch proof
- missed-pulse and missed-window recovery
- far-side emergence and edit-surviving destination cues
- recovery-site obstruction behavior
- stationary quest-Spitball and early-port response
- three-phrase handshake
- assist tiers, retry, persistence, and first-light grace
- transition through `recovered`

Gate: Night 3 introduces no new rule; a naive player rejects the visibly official claim, follows local proof and PULSE, reaches Spitball, and completes the handshake using rehearsed actions.

### Pass 5 — return, seal, and Almanac

Implement and validate:

- temporary port plug
- deterministic HOME reference chain
- noncolliding waypoint return pose and bounded catch-up
- truthful returning versus far-exit waiting state
- optional Penelope answer and old-light recovery
- kiln `FIRE PORT SEAL`
- atomic, monotonic `returned` transition
- companion restoration
- final service entry and `attendance: two`
- Underwall Almanac arrival and complete first open
- revisitable underpath and persistent aftermath
- unchanged subsequent Night Moves behavior

Gate: YOLO, Optimizer, and Explorer each reach `returned`; completion survives reload and later sandbox edits; the next Night Moves cycle still works; the Almanac opens already complete.

---

## Mandatory regression matrix

Encode and run every invariant in Section 14 that applies to implemented scope. At minimum, test:

- no embodied Harriet, Sheriff, Gretchen, Penelope, vendor, or substitute quest-giver
- Count and Night Moves phase purity
- first-control freedom and opening comprehension
- order-tolerant wall lessons
- first Ledger ownership and cue timing
- first-dusk companion identity and skip fallback
- second-dusk Call exactly once across natural time, trance, and reload
- first post-Call Scan consumed as absence read, never a pulse tap
- serialized and interrupt-safe Call contacts
- entrance excavation/calibration permutations
- no hidden Local Sweep requirement
- utility-light freedom and required-ring behavior
- J1/J2/J3 empty-ring recovery
- active-interaction obstruction and provenance-based reclaim
- exact seam arming, proof, prep, phase, and tool precedence
- no random deep excavation or phase-cap bypass
- stable source-gated ROUTE and `HOME` chain
- official provenance on every false answer
- relay refusal, commit, reload, retained clue, repeat review, and burn clear
- kiln reservation and self-clearing rehearsal
- C3 order independence and missed-pulse recovery
- handshake retries, assistance, dawn pause, radius exit, and reload
- early recovery-site arrival and legal pre-Call construction
- return follower lag, overland wait, reload, and truthful kiln status
- optional answer with zero, one, or multiple old lights
- atomic seal, final record, Almanac arrival, and monotonic completion
- persistence and derivation laws in Section 16.11
- all six Revision 12 and all six Revision 13 corrections

Run the four build-test questions as actual presentation tests rather than silently changing mechanics:

- `BTQ-12-1` — refused first light
- `BTQ-12-2` — edited far landmark
- `BTQ-13-1` — occluded active proxy
- `BTQ-13-2` — Call queue across trance

If a build test fails, adjust only the bounded presentation variables authorized by the question unless a canonical invariant proves a deeper defect.

---

## Specification-gap policy

Do not invent major mechanics, story content, characters, branches, resources, lore, or alternate endings.

When behavior appears underspecified:

1. Search Section 16, the determinism laws, tests, revision notes, and existing engine convention.
2. Ask the Counterfactual Critic to test the consequential interpretations.
3. Prefer an existing engine behavior.
4. If still undefined, implement only the smallest reversible behavior that:
   - uses an existing verb
   - preserves player freedom and state
   - gives truthful feedback
   - cannot advance or regress unrelated progression
   - provides a recovery path
   - adds no new story fact or system
5. Record it as `IMPLEMENTATION-SPEC-GAP` with evidence and rationale in `IMPLEMENTATION_REPORT.MD`.

If the missing choice would materially alter the story, canonical progression, engine architecture, persistence contract, or player verbs, do not guess. Record it as a blocking gap with the exact decision required.

---

## Build, test, and validation discipline

- Discover and use each repository's normal commands; do not substitute ad hoc commands when maintained scripts exist.
- Run focused tests while iterating and the full relevant suites before delivery.
- Run game and engine builds after cross-repository changes.
- Run scene baking and package verification through the maintained pipeline.
- Exercise the actual local build in the browser/runtime, not only unit tests.
- Capture console errors and presentation screenshots at the required widths.
- Treat warnings introduced by this implementation as failures unless demonstrably benign and documented.
- Verify a clean launch from the normal entry point.
- Verify saved worlds from every quest stage reload deterministically.
- Do not mark a gate complete from code inspection alone.

Use Claude Code checkpoints and small internal commits only when safe and consistent with repository instructions. Git remains the durable record. Do not include unrelated files in checkpoints or commits.

---

## Completion contract

Do not finish while any of the following is true:

- Gate 0 or any Pass 1–5 gate is incomplete or failing.
- A normal build, maintained test suite, scene verification, or package verification fails because of this work.
- A required path contains a crash, softlock, undefined outcome, hidden-knowledge dependency, duplicate transition, or stale contradictory state.
- Any canonical invariant is knowingly violated.
- Save/reload or time-boundary behavior is nondeterministic.
- The final three clean-state player simulations have not completed.
- The four build-test questions have not been exercised in the real presentation.
- The target repositories are not runnable through their normal workflow.
- `IMPLEMENTATION_REPORT.MD` is missing or incomplete.

`FRICTION` and `POLISH` findings may remain only when they do not obscure a required affordance, prevent naive-player recovery, violate a canonical presentation rule, or fail a required acceptance test. Record each one precisely. Do not use either label for incomplete required behavior.

If infrastructure interrupts the session, resume the same named session and continue from the last verified gate without changing scope. If a genuine blocker remains after reasonable repository inspection and multiple bounded attempts, stop with `BLOCKED`, leave both repositories runnable, and document exact evidence and the smallest decision or external change required.

---

## Required implementation report

Create this file when implementation begins and update it throughout the campaign:

`C:\Users\natha\Dev\GITHUB_DESKTOP\AkiyaBlocks-MiddleKingdom\IMPLEMENTATION_REPORT.MD`

Keep it evidence-based and include:

1. **Final status:** `PASS`, `PARTIAL`, or `BLOCKED`.
2. **Implemented playable path:** first control through conclusion, with optional content distinguished from required content.
3. **Gate results:** Gate 0 and Passes 1–5, including exact commands and outcomes.
4. **Files changed:** grouped by game repository and engine repository.
5. **Systems reused or extended:** existing architecture used, new extension points, and why each engine change is reusable.
6. **Design-to-code mappings:** important mappings and selected ownership.
7. **Counterfactual decisions:** only consequential choices, rejected alternative, failure modes considered, and selected mapping.
8. **State and persistence:** schema/version, derived state, reload reconciliation, and time-boundary handling.
9. **Agentic playtests:** YOLO, Optimizer, and Explorer decision counts, perturbations, outcomes, important recoveries, and cited traces.
10. **Regression results:** Revision 12/13 fixes, Section 14 invariants, save/reload matrix, and the four BTQs.
11. **Build and runtime validation:** builds, tests, bake/package checks, browser/runtime runs, console results, and screenshot locations.
12. **Implementation specification gaps:** every `IMPLEMENTATION-SPEC-GAP`, smallest behavior selected, and rationale.
13. **Known limitations:** specific remaining `POLISH` or external issues; no sweeping language.
14. **How to run:** exact commands to build, launch, test, simulate, and reproduce the final playable path.

Do not claim completion from file counts or partial test success. Lead the final response with the actual playable outcome, gate status, and any blocker. Leave both repositories in a runnable, inspectable state.
