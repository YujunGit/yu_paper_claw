# Explicit Intermediate Structure

## Scope
Notes on papers where the intermediate representation is not merely descriptive but actively constrains prediction, planning, generation, or rollout behavior.

## What this topic is really about
A lot of recent papers use words like compositional, modular, symbolic, agentic, or world-model-based. The useful distinction is whether the intermediate structure changes failure modes in a testable way.

The stronger papers usually satisfy at least one of these:
- the structure constrains the output distribution or feasible action set,
- the structure is grounded by execution or dynamics rather than text alone,
- the interfaces support recombination across tasks or mechanisms,
- the paper exposes where errors come from rather than only reporting final score gains.

## Current anchor papers

### NeSyS (2026)
- Positioning: neuro-symbolic world modeling with executable symbolic constraints.
- What it gets right: symbolic rules appear to directly shape neural prediction and training focuses on disagreement regions.
- What it does not solve: unclear scaling path when symbolic structure is incomplete or hard to specify.

### SCALAR (2026)
- Positioning: symbolic skill planning refined by RL-grounded feedback.
- What it gets right: treats LLM-generated skills as revisable abstractions instead of trusted outputs.
- What it does not solve: unclear transfer to physically realistic robotics.

### CoR-Painter (2026)
- Positioning: explicit constraint reasoning before autoregressive image generation.
- What it gets right: forces structural commitments before image synthesis.
- What it does not solve: may still be too text-centric unless constraints are grounded in richer representations.

### LegONet (2026)
- Positioning: compositional neural operator blocks for PDE learning.
- What it gets right: modularity is enforced through reusable, structure-preserving interfaces.
- What it does not solve: real transfer beyond curated PDE recombination remains to be tested.

### VisualPredicator (2025)
- Positioning: learned neuro-symbolic predicates as an abstract planning interface.
- What it gets right: tries to learn the abstraction layer itself and judges it by sample efficiency, OOD planning, and interpretability.
- What it does not solve: robustness under noisy real-world perception remains unclear.

### RISE (2026)
- Positioning: robot policy improvement via a compositional world model split into dynamics prediction and progress evaluation.
- What it gets right: decomposition corresponds to distinct control functions rather than decorative modularity.
- What it does not solve: “compositional” here may be more functional than formally compositional, and baseline fairness needs scrutiny.

### Object-Centric Representations Better At Compositional Generalization? (2026)
- Positioning: evaluation paper testing when decomposed visual representations actually help.
- What it gets right: makes a conditional claim that structure helps most under limited data, diversity, or compute.
- What it does not solve: transfer from controlled visual worlds to embodied planning or generation.

## Working heuristics for future scouting
Prefer papers that do at least two of the following:
- make the intermediate structure executable or constraining,
- verify high-level structure against low-level dynamics or outcomes,
- localize errors by module or interface,
- show recombination under changed tasks, mechanisms, or boundaries,
- improve data efficiency or robustness because of the structure, not just alongside it.

Be skeptical of papers that claim:
- “compositional” but only rewrite prompts,
- “symbolic” but only use labels as auxiliary outputs,
- “world model” without planning utility or counterfactual leverage,
- “modular” when all communication is hidden inside soft uninterpretable latents.

## Why this topic matters
This is a useful lens for evaluating whether structure is real. It also connects several of the user’s interests: controllable generation, world models, neurosymbolic reasoning, embodied planning, and reusable representations.
