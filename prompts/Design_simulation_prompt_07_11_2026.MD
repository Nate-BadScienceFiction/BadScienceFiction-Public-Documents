Review the latest “HEROS_GAME.MD” and treat it as an executable model of the game. Run three independent first-time-player simulations to test how the design behaves under different goals, decisions, and mistakes.

Act as the rules referee. You may read the full design, but reveal to each player only what the game visibly communicates. Do not give players design-document knowledge, discoveries from other runs, or invented mechanics. When the document does not define an outcome, log “THREE-SPEC-GAP”.

Simulate:

1. YOLO Player: seeks danger, novelty, spectacle, and amusing consequences.

2. Optimizer: tries to reach an ending quickly and skips anything that appears optional.

3. Explorer: follows narrative and environmental clues, talks to NPCs, and investigates interesting side paths.

Start every player from the same clean state. Track location, inventory, objectives, NPC state, resources, player knowledge, mistakes, and recovery attempts. A meaningful decision must change the player’s position, knowledge, strategy, resources, or game state.

Introduce three to five plausible perturbations per run. Examples include missing a subtle cue, misunderstanding ambiguous guidance, forgetting a weak clue, selecting the wrong nearby interaction, or abandoning an action after unclear feedback. Log each perturbation explicitly and resolve it using the documented rules.

At important decision points, briefly restore the pre-decision state and test one plausible alternative action. Record whether the interaction is:

* “ROBUST”

* “RECOVERABLE”

* “FRAGILE”

* “TRAP”

* “NOISE-SENSITIVE”

Continue each run until the player reaches an ending, becomes softlocked, reasonably abandons the game, or makes 50 meaningful decisions.

Write concise chronological logs to “THREE_SIM_RESULTS.MD”. Each entry should record the visible situation, player decision, action, result, relevant state change, and any issue discovered.

After the runs, audit the results for:

* unclear goals or affordances

* softlocks and weak recovery paths

* sequence breaks and dominant shortcuts

* hidden-knowledge requirements

* inconsistent state or inventory changes

* misleading NPC or environmental feedback

* unrewarding exploration or pacing

* interactions that fail under small, plausible player errors

Classify severity as “BLOCKER”, “MAJOR”, “FRICTION”, or “POLISH”. Separately label the evidence as “OBSERVED”, “COUNTERFACTUAL”, “NOISE-SENSITIVE”, or “THREE-SPEC-GAP”.  Annotate THREE_SIM_RESULTS.MD with classification details.

Every recommendation must cite specific log entries and propose the smallest practical player-facing fix. Avoid broad observations, invented story content, and sweeping redesigns.

Update “HEROS_GAME.MD” directly only for clearly observed failures, confirmed specification gaps, or counterfactual failures with strong evidence. Preserve the existing concept, tone, structure, and technical constraints. Record uncertain findings as build-test questions rather than changing the design.