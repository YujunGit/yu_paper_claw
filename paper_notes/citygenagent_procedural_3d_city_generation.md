# Imagine a City: CityGenAgent for Procedural 3D City Generation

## Basic info

* Title: Imagine a City: CityGenAgent for Procedural 3D City Generation
* Authors: Zecong Tang, Ruocheng Wu, Xinzhe Zheng, Jingyu Hu, Ka-Hei Hui, Haoran Xie, Bo Dai, Zhengzhe Liu
* Year: 2026
* Venue / source: arXiv / ICML submission
* Link: https://arxiv.org/abs/2602.05362
* Date surfaced: 2026-03-20
* Why selected in one sentence: It uses a genuinely executable hierarchical intermediate representation for city generation, separating block layout from building realization in a way that supports editing and control.

## Quick verdict

**Useful**

This is more adjacent inspiration than direct hit, but the decomposition is real enough to merit a note. The strongest part is the use of two domain-specific programs—Block Program and Building Program—as editable intermediate structure. The biggest reservation is that a meaningful chunk of the reward/evaluation stack depends on GPT-4o judgments and hand-designed priors, which weakens the epistemic cleanliness of the claims.

## One-paragraph overview

CityGenAgent frames 3D city generation as hierarchical procedural program synthesis from natural language. A first model, BlockGen, generates a block-level program that specifies object footprints, types, and coarse layout in city coordinates. A second model, BuildingGen, fills in building-level details with a separate executable program describing architectural attributes. The models are first supervised to produce valid schema-conforming programs, then refined with reinforcement learning using a spatial alignment reward for block layouts and a visual consistency reward for building appearance. Because the intermediate structure is executable, the final city can be directly manipulated through subsequent natural-language edits.

## Key questions this summary must address

### 1. What problem is the paper trying to solve?
It aims to generate controllable, editable, city-scale 3D scenes that preserve both structural correctness and visual plausibility. The paper argues that end-to-end rendering or diffusion systems often give weak geometric control and poor editability.

### 2. What is the method?
The method decomposes the task into two program-generation stages:
- **BlockGen** outputs a Block Program containing building/element footprints and coarse semantic layout.
- **BuildingGen** outputs a Building Program specifying finer architectural realization.

Training proceeds in two stages: supervised fine-tuning for valid program formatting and basic instruction following, then PPO-style RL with task-specific rewards.

### 3. What is the method motivation?
The motivation is plausible: city generation is too structurally rich to leave entirely to unstructured text-to-3D synthesis, and the kinds of edits users want often happen at different abstraction levels. A block/building split is therefore a reasonable decomposition.

### 4. What data does it use?
The accessible text indicates paired instruction–program data for supervised warm-start and additional rendered or program-derived data for reinforcement learning. The paper also emphasizes the scarcity of large-scale outdoor city datasets, which partly motivates its compact program representation.

### 5. How is it evaluated?
It is evaluated against prior city-generation systems on semantic alignment, controllability, visual quality, and interactive manipulation. The reward stack for BlockGen includes semantic alignment and plausibility judged by GPT-4o over rendered layouts, plus hand-crafted overlap and density metrics.

### 6. What are the main results?
The paper reports better semantic alignment, visual quality, and controllability than prior methods. The most believable result is improved editability and structured control from the program interface; I am less confident in the exact strength of the RL-derived quality claims because of the judge-dependent evaluation design.

### 7. What is actually novel?
The novelty is not “LLM for 3D generation.” The real contribution is using two executable DSL-style programs as the main generation interface and then training the models with rewards that explicitly target spatial coherence and appearance alignment at the right abstraction level.

### 8. What are the strengths?
- The decomposition is operational, not cosmetic.
- The intermediate representation is editable and executable.
- It separates coarse spatial reasoning from fine architectural realization.
- It is a useful example of controllable 3D generation via structured interfaces.

### 9. What are the weaknesses, limitations, or red flags?
- Heavy reliance on GPT-4o-based judging for part of the reward/evaluation loop.
- Hand-designed density/overlap priors are sensible but narrow.
- It is not clear how robust the approach is to truly open-ended urban diversity outside the curated program space.
- The method is more about procedural scene synthesis than about world models in the stronger interactive/dynamic sense.

### 10. What challenges or open problems remain?
Scaling to richer traffic dynamics, temporal city processes, infrastructure semantics, and simulation-grade physical interaction remains open. Another unresolved issue is whether the representation can generalize beyond the predefined DSL without either collapsing to invalid programs or losing editability.

### 11. What future work naturally follows?
- adding explicit dynamic agents and traffic systems,
- uncertainty-aware or verifier-backed program generation,
- stronger automatic evaluation that does not lean as much on LLM judges,
- extending the decomposition to city-scale simulation tasks rather than static generation alone.

### 12. Why does this matter for my work?
It matters as a decomposition example. The key reusable pattern is to separate high-level spatial composition from lower-level instantiation, and to make both stages executable so edits and constraints have a concrete target.

### 13. What ideas are steal-worthy?
- Use distinct executable interfaces at different abstraction levels.
- Align rewards with the specific structure each module is responsible for.
- Treat editability as a first-class design goal, not as an afterthought.
- Prefer decomposition that survives execution rather than prompt-only “planning.”

### 14. Final decision
**Useful but not urgent.** Worth citing or borrowing from for structured generation interfaces, but not a paper I would prioritize over stronger world-model or representation-learning work.

---

## Confidence / access note

This note is based on the arXiv abstract and partial HTML paper access. I verified the hierarchical program design, training structure, and reward framing, but did not fully inspect all dataset details, ablation tables, or appendix examples.