# Modular Open-Vocabulary Robotics

## Scope
Notes on systems that combine open-vocabulary perception or language grounding with explicit task structure, planning, or symbolic abstractions.

## What this topic is really about
The interesting question is not whether a robot can ingest language and images. That is now table stakes. The real question is whether the system has an internal structure that supports:
- semantic grounding,
- decomposition of multi-step tasks,
- geometric feasibility,
- debuggability,
- extension to new skills,
- transfer across embodiments.

A lot of recent work uses modular language while still hiding most reasoning inside a large policy. That can work, but it makes mechanism claims harder to trust. The more useful papers are the ones that expose interfaces and failure boundaries.

## Current anchor papers

### TiPToP (2026)
- Positioning: planning-first hybrid system using pretrained perception and explicit symbolic goal grounding.
- What it gets right: clear module interfaces, good task-category evaluation, strong failure analysis, cross-embodiment portability evidence.
- What it does not solve: reactive robustness, uncertainty handling, strong 3D scene completion.

### Grounded World Model (2026)
- Positioning: world-model-based MPC where candidate futures are scored in a vision-language-aligned latent space against task instructions rather than a goal image.
- What it gets right: places semantic grounding inside the planning objective itself, which is a stronger interface claim than using language only for front-end conditioning.
- What it does not solve: current evidence still appears bounded to motions seen in training, and the robustness story under long-horizon replanning or uncertainty remains unclear.

## Working heuristics for future scouting
Prefer papers that satisfy at least two of the following:
- explicit intermediate representation between language/perception and action,
- non-trivial multi-step or constrained manipulation,
- meaningful comparison to end-to-end learned baselines,
- failure analysis by module,
- evidence that adding a new skill changes only localized parts of the system,
- handling of uncertainty or closed-loop replanning.

Be skeptical of papers that claim:
- “compositional” but only chain prompted modules without causal analysis,
- “agentic” but just do retry loops,
- “world model” without actual planning or counterfactual utility,
- “modular” when the interfaces are soft and uninterpretable.

## Why this topic matters
This topic is a good lens on broader research questions:
- when explicit structure still beats scale-only learning,
- how representations should support planning rather than just prediction,
- how to combine foundation models with reliable control,
- what kinds of modularity are real versus cosmetic.
