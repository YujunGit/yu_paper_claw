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

### PlayWorld (2026)
- Positioning: robot world modeling via autonomous play data rather than success-biased demonstrations.
- What it gets right: treats data coverage as part of the mechanism, especially for contact-rich dynamics and failure-heavy rollouts.
- What it does not solve: coverage is broader, but still shaped by the proposer/executor behavior prior and hardware collection constraints.

### H-WM (2026)
- Positioning: hierarchical world model that combines symbolic task-level transition prediction with latent visual subgoal grounding.
- What it gets right: the intermediate structure has a concrete job—keeping long-horizon plans coherent while still grounding them for control.
- What it does not solve: much of the symbolic interface is still curated and annotated rather than learned.

### C3 (2025/2026)
- Positioning: uncertainty-calibrated controllable video world models.
- What it gets right: asks whether the world model knows when its own rollout is untrustworthy, which is a missing piece in many planning papers.
- What it does not solve: uncertainty estimates are only useful if they change downstream decision-making, not just visualization.

### NSGGM (2026)
- Positioning: neural proposal plus symbolic assembly for graph generation with hard guarantees.
- What it gets right: uses symbolic machinery where exact validity and user constraints actually matter.
- What it does not solve: solver-backed exactness may become expensive or brittle as structured outputs grow more complex.

### Interactive World Simulator (2026)
- Positioning: action-conditioned latent video world model used as a practical surrogate environment for robot training and evaluation.
- What it gets right: asks whether a world model is fast, stable, and faithful enough to support data generation and policy ranking, not just visual prediction.
- What it does not solve: physical consistency is still mediated through latent video prediction rather than explicit object/contact state.

### SimRecon (2026)
- Positioning: compositional 3D reconstruction aimed at simulation-ready assembly from real videos.
- What it gets right: treats perception-to-generation and generation-to-simulation interfaces as real bottlenecks and gives structure an executable role in scene assembly.
- What it does not solve: pipeline errors can still compound, and simulator plausibility is not equivalent to full real-world physical fidelity.

### MM-CondChain (2026)
- Positioning: benchmark for visually grounded deep compositional reasoning built around a verifiable programmatic intermediate representation.
- What it gets right: uses intermediate structure for mechanical verification and tests deep chained conditions rather than shallow composition.
- What it does not solve: it is evaluation infrastructure, not a mechanism for improving model reasoning or grounding.

### CoWVLA / Chain of World (2026)
- Positioning: VLA pretraining built around structure–motion disentanglement and a continuous latent motion chain instead of dense future-frame reconstruction.
- What it gets right: treats motion as the thing worth modeling, and uses the intermediate structure to reduce redundancy while preserving temporal reasoning for control.
- What it does not solve: the latent interface is still soft and only indirectly interpretable, so claims about world understanding should stay modest.

### FutureCAD (2026)
- Positioning: LLM-generated CAD programs with a separate text-to-B-Rep grounding module for resolving primitive references during execution.
- What it gets right: the intermediate structure is executable, state-dependent, and necessary; high-level intent and low-level entity binding are cleanly separated.
- What it does not solve: the mechanism is strong but domain-specific, and transfer beyond CAD will require additional grounding machinery.

### Reasoning Core (2026)
- Positioning: procedural symbolic-data infrastructure with solver-backed verification and broad formal-task distributions.
- What it gets right: argues that explicit structure in training data should be distributionally broad, difficulty-controlled, and reusable for both supervised learning and verifiable reward.
- What it does not solve: it is still mostly a training/evaluation substrate, not direct evidence that symbolic pretraining transfers cleanly into messy embodied or multimodal reasoning.

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
