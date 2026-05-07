# Decompose and Recompose: Reasoning New Skills from Existing Abilities for Cross-Task Robotic Manipulation

## Basic info

* Title: Decompose and Recompose: Reasoning New Skills from Existing Abilities for Cross-Task Robotic Manipulation
* Authors: Xitie Zhang, Aming Wu, Yahong Han
* Year: 2026
* Venue / source: arXiv (cs.RO), accepted by ICML 2026 per arXiv comments
* Link: https://arxiv.org/abs/2605.01448
* Date surfaced: 2026-05-07
* Why selected in one sentence: It tries to turn in-context robot transfer from trajectory imitation into explicit skill recomposition through intermediate skill-action structure.

## Quick verdict

**Useful**

I am keeping this one, but with more caution than the first two papers. The central idea—decompose demonstrations into atomic skill-action pairs, then retrieve for both task relevance and skill coverage—is sensible and aligned with the user’s tastes. My reservation is that this may still be a fairly engineered pipeline whose gains depend on the quality of the planner, the skill vocabulary, and the retrieval setup.

## One-paragraph overview

The paper studies zero-shot cross-task robotic manipulation, where the agent must solve unseen tasks using demonstrations from seen tasks without parameter updates. Its main move is to replace raw low-level action demonstrations with skill-annotated intermediate structure. Demonstrations are decomposed into atomic skills aligned with action segments, a planner predicts which skill sequence an unseen task likely needs, and the system retrieves demonstrations using both scene/task similarity and explicit coverage of missing skill patterns before prompting an LLM to generate executable actions.

## Key questions this summary must address

### 1. What problem is the paper trying to solve?
It targets cross-task generalization in robotic manipulation, especially the failure of retrieval-based in-context approaches that rely too heavily on low-level action similarity and end up imitating trajectories rather than recomposing skills.

### 2. What is the method?
The method has three main pieces: atomic skill collection from seen demonstrations, a dual-library retrieval system, and skill-augmented in-context learning. The dynamic library retrieves task-adaptive demonstrations using visual-semantic similarity plus planner-predicted skill sequences, while the static library patches missing skill-pattern coverage.

### 3. What is the method motivation?
The motivation is that low-level actions are a bad interface for transfer when unseen tasks require new compositions of known abilities. Skill-labeled intermediate representations should let the model reason about what to do and in what order, instead of matching trajectory shapes.

### 4. What data does it use?
From the available text, it uses the AGNOSTOS benchmark for cross-task manipulation plus real-world robotic environments. I did not inspect the full dataset details or annotation burden from the PDF.

### 5. How is it evaluated?
It is evaluated on zero-shot cross-task generalization, with comparisons against existing in-context manipulation baselines. The paper also includes ablations around the number and type of demonstrations, plus real-world experiments.

### 6. What are the main results?
The paper reports improved zero-shot cross-task performance and argues that explicit skill decomposition plus coverage-aware retrieval better supports unseen task composition than plain low-level demonstration retrieval. The real-world experiments are meant to show the same trend outside the benchmark.

### 7. What is actually novel?
The most novel part is not “use skills” in the abstract; it is the specific combination of atomic skill-action alignments, planner-conditioned retrieval, and a separate coverage-aware library that tries to fill missing skill patterns rather than only retrieve nearest neighbors.

### 8. What are the strengths?
The paper has a good instinct about interfaces: if transfer depends on compositional reuse, then the retrieved context should expose reusable skill units instead of opaque continuous controls. I also like the explicit distinction between task relevance and skill coverage, since nearest-neighbor retrieval alone often misses critical components.

### 9. What are the weaknesses, limitations, or red flags?
This may be a pipeline with several fragile moving parts: keyframe extraction, skill labeling, planning, retrieval, and LLM action generation. The method could owe a lot to auxiliary supervision and system design rather than a fundamentally new transfer principle. Another concern is scalability: the approach may depend on a curated atomic skill vocabulary and benchmark structure that do not transfer cleanly to messier robotic domains.

### 10. What challenges or open problems remain?
Open problems include learning the skill vocabulary rather than injecting it, handling tasks whose useful abstractions are not well captured by fixed atomic skills, and proving robustness when planners or retrieval modules are wrong.

### 11. What future work naturally follows?
Learning latent skill decompositions jointly with retrieval, uncertainty-aware skill coverage, stronger tests on truly novel compositions, and cleaner comparisons against stronger end-to-end VLA baselines.

### 12. Why does this matter for my work?
It matters because it treats decomposition as an operational interface, not a post hoc explanation. Even if the exact pipeline is too engineered, the design instinct is right: transfer should happen through reusable intermediate structure, not raw trajectories alone.

### 13. What ideas are steal-worthy?
Two ideas are clearly worth stealing: (1) retrieve for **coverage of missing subskills**, not just similarity; (2) force the context interface to expose aligned intermediate units that can be recomposed, rather than hoping the model infers them from continuous traces.

### 14. Final decision
**Keep, but do not over-trust.** Worth knowing as a robotics-transfer mechanism paper and potential baseline, but it needs a deeper read before I would treat it as strong evidence of general compositional reasoning.

## Access note
This note is based on the arXiv abstract page and substantial arXiv HTML text, not a full PDF-level audit. Exact benchmark details, annotation burden, and baseline fairness need confirmation from a deeper read.