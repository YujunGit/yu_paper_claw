# Edit-As-Act: Goal-Regressive Planning for Open-Vocabulary 3D Indoor Scene Editing

## Basic info

* Title: Edit-As-Act: Goal-Regressive Planning for Open-Vocabulary 3D Indoor Scene Editing
* Authors: Seongrae Noh, SeungWon Seo, Gyeong-Moon Park, HyeongYeop Kang
* Year: 2026
* Venue / source: CVPR 2026 / arXiv
* Link: https://arxiv.org/abs/2603.17583
* Date surfaced: 2026-03-21
* Why selected in one sentence: It frames 3D scene editing as symbolic goal satisfaction with explicit preconditions and effects, which is a real mechanism rather than prompt-level pseudo-planning.

## Quick verdict

**Highly relevant**

This is not a direct world-model paper, but it is exactly the kind of explicit intermediate-structure paper worth tracking. The contribution is conceptually simple and strong: turn language-guided scene editing into backward planning over symbolic predicates and action schemas, with validation for feasibility and monotonic progress. The benchmark is not huge, and indoor editing is a bounded domain, but the mechanism is credible and transferable.

## One-paragraph overview

Instead of treating 3D scene editing as another generation problem, the paper treats an instruction as specifying a desired target world state. It introduces EditLang, a PDDL-inspired symbolic action language for 3D editing with explicit predicates, preconditions, add/delete effects, and geometric constraints such as support, contact, collision, and stability. An LLM-based planner proposes actions to satisfy current goals, a validator checks goal-directedness, monotonicity, contextual plausibility, and formal validity, and a source-aware regression operator pushes unsatisfied preconditions backward until all required conditions are grounded in the source scene. The final plan is then executed by a deterministic runtime over the 3D scene.

## Key questions this summary must address

### 1. What problem is the paper trying to solve?
Open-vocabulary 3D scene editing methods often either regenerate too much of the scene, operate in 2D then lift back to 3D, or solve global constraints in ways that disturb untouched regions. The paper wants edits that are instruction-faithful, localized, and physically plausible at the same time.

### 2. What is the method?
- Convert a language instruction and source scene into symbolic goal predicates.
- Represent editing operations in EditLang, a PDDL-like action language.
- Use a planner to propose one action at a time.
- Use a validator to reject actions that fail progress, monotonicity, contextual consistency, or formal schema checks.
- Regress remaining goals backward using a source-aware STRIPS-style operator.
- Reverse the resulting backward plan and execute it with a deterministic Python DSL runtime.

### 3. What is the method motivation?
The authors argue editing should be understood as the minimal sequence of valid state changes needed to make a target world state true, not as free-form generation. This motivates explicit symbolic structure and backward reasoning.

### 4. What data does it use?
The method is evaluated on E2A-Bench, introduced in the paper, with 63 editing tasks across 9 indoor environments. The paper also references scene assets/catalogs and symbolic state extraction from source scenes.

### 5. How is it evaluated?
The benchmark measures three key criteria: instruction fidelity, semantic consistency, and physical plausibility. The paper compares against data-driven layout editing, constraint-based layout synthesis, and image-based editing/lifting baselines.

### 6. What are the main results?
The paper reports that Edit-As-Act achieves the strongest and most consistent performance across its three main criteria and across scene categories. I only verified this from the paper text and table descriptions, not from the full numeric appendix.

### 7. What is actually novel?
The main novelty is not “use an LLM planner”; that part is now common. The actual novelty is the combination of: (1) source-aware goal regression for scene editing, (2) an explicit action language designed around 3D geometric and physical relations, and (3) validator-enforced monotone progress and feasibility.

### 8. What are the strengths?
- The intermediate structure is executable and testable.
- Planning is tied to explicit preconditions/effects rather than free-form chain-of-thought.
- The source-aware regression step is a good idea for edit locality.
- The paper targets a real failure mode in 3D editing: unnecessary global changes.
- Strong conceptual transfer to robotics, simulation editing, and structured generation pipelines.

### 9. What are the weaknesses, limitations, or red flags?
- The domain is relatively constrained: indoor scenes with a hand-designed symbolic language.
- The benchmark is still modest in scale.
- Open-vocabulary claims are bounded by what can be grounded into the predefined predicate/action schema and asset catalog.
- LLM planner/validator loops can hide brittleness if prompt sensitivity is high; the paper summary does not yet convince me that this is robust across much broader domains.

### 10. What challenges or open problems remain?
- Learning the symbolic interface instead of hand-designing so much of it.
- Scaling beyond bounded indoor scenes to richer dynamic environments.
- Handling uncertainty, perception noise, and incomplete object/state grounding.
- Extending the framework from editing to multi-step embodied planning with execution feedback.

### 11. What future work naturally follows?
A natural extension is to integrate learned predicate grounding, object-centric perception, or world-model rollouts into the planning loop. Another is to move from static scene edits toward dynamic manipulation tasks and embodied simulation curricula.

### 12. Why does this matter for my work?
It is strong support for the claim that explicit structure is valuable when it has operational consequences. It also provides a clean contrast against papers that call themselves compositional or agentic without an executable intermediate interface.

### 13. What ideas are steal-worthy?
- Source-aware goal regression that ignores conditions already satisfied by the source scene.
- Action languages whose predicates correspond to physical/geometric constraints, not just semantic labels.
- Validator-enforced monotonicity to reduce cyclic or decorative planning.
- Minimal-edit framing as a way to preserve scene identity during structured generation/editing.

### 14. Final decision
**Read if you care about structured generation, symbolic interfaces, or controllable 3D editing.** This is a useful mechanism paper, even if the domain remains narrow.
