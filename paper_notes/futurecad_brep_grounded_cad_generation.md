# Towards High-Fidelity CAD Generation via LLM-Driven Program Generation and Text-Based B-Rep Primitive Grounding

## Basic info

* Title: Towards High-Fidelity CAD Generation via LLM-Driven Program Generation and Text-Based B-Rep Primitive Grounding
* Authors: Jiahao Li and collaborators (full author list not fully recovered from current access)
* Year: 2026
* Venue / source: arXiv
* Link: https://arxiv.org/abs/2603.11831
* Date surfaced: 2026-03-17
* Why selected in one sentence: It uses an explicit grounded interface between language-generated programs and evolving geometry, which is a strong transferable pattern for structured generation.

## Quick verdict

**Highly relevant**

This is not directly a world-model or robotics paper, but it is methodologically interesting because it refuses to flatten structured generation into plain sequence prediction. The key move is to let the LLM generate executable CAD programs while delegating ambiguous geometric reference resolution to a state-conditioned grounding model over the current B-Rep. That division of labor is much more compelling than asking the LLM to infer exact low-level references from text alone.

## One-paragraph overview

FutureCAD tackles text-to-CAD generation in realistic feature-based design settings, where parametric operations and boundary-representation geometry are tightly coupled. Instead of choosing between pure parametric program generation and direct B-Rep synthesis, it combines them. An LLM writes CadQuery programs that describe the feature sequence, and when an operation requires selecting specific faces or edges from the current geometric state, the program emits a natural-language query. A separate transformer, BRepGround, then resolves that query against the transient B-Rep and returns the referenced primitives needed for execution. The system is trained with supervised fine-tuning, then RL based on geometric fidelity, and supported by a large dataset of real-world CAD models converted to executable programs.

## Key questions this summary must address

### 1. What problem is the paper trying to solve?
It tries to bridge a real gap in CAD generation: parametric modeling preserves editability and intent but struggles with advanced operations that depend on selecting intermediate geometric primitives, while direct B-Rep synthesis captures geometry but loses reusable modeling structure.

### 2. What is the method?
The method has three main pieces:
- an LLM that generates executable CadQuery code from text descriptions,
- a text-based primitive-reference mechanism where the program specifies target geometry in natural language,
- a BRepGround module that grounds those queries to faces/edges in the current B-Rep using geometric encoders, a graph neural network, text encoding, and attention-based fusion.
It then uses GSPO-style RL with Chamfer-distance rewards to improve generalization and execution validity.

### 3. What is the method motivation?
The motivation is strong. In realistic CAD workflows, advanced operations like fillet or chamfer require references to the current geometric state. Treating CAD generation as only code generation or only direct geometry synthesis misses that state-dependent interface.

### 4. What data does it use?
The paper reports a new dataset of roughly 140k real-world CAD models, with geometric descriptions, CadQuery program representations, and primitive-grounding annotations. It also augments the code side with rewritten programs for greater programmatic diversity.

### 5. How is it evaluated?
It is evaluated on the authors’ FutureCAD dataset and an out-of-distribution Fusion360 test set, with metrics that include geometric fidelity and command-level performance for both generation commands and refinement commands such as fillet/chamfer/shell.

### 6. What are the main results?
The paper claims state-of-the-art text-to-CAD performance, especially on high-fidelity feature-based modeling with advanced operations, while maintaining a low invalid-program rate. The exact headline numbers were not fully recovered in the current partial read.

### 7. What is actually novel?
The strongest novelty is the interface design:
- explicit unification of program generation with B-Rep grounding,
- introducing text-based primitive grounding as a first-class subproblem,
- training a dedicated BRepGround model rather than relying on heuristic rule matching,
- tying RL reward to executed geometric outcomes instead of only token accuracy.

### 8. What are the strengths?
- The decomposition feels real, not theatrical: the submodule exists because the CAD process genuinely requires it.
- The intermediate structure is executable and state-dependent.
- The paper treats editability and geometric fidelity as joint requirements.
- The method is conceptually transferable to any domain where high-level generated actions must bind to low-level evolving entities.

### 9. What are the weaknesses, limitations, or red flags?
- The domain is specialized, so direct transfer claims should be modest.
- Part of the pipeline depends on large curated datasets and substantial annotation/rewriting effort.
- RL reward based on geometric fidelity does not by itself guarantee that the induced program structure is the most human-meaningful or reusable.
- The use of LLM-generated auxiliary descriptions and rewrites raises the usual questions about annotation consistency and training-data cleanliness.

### 10. What challenges or open problems remain?
The hard problem is scaling this style of grounded program generation beyond well-instrumented CAD systems into messier physical or multimodal settings. Another open issue is whether the grounding mechanism can handle much more ambiguous or underspecified user intent without brittle failure.

### 11. What future work naturally follows?
- editing and repair loops over generated CAD programs,
- uncertainty-aware primitive grounding,
- richer interaction between geometric simulation and program synthesis,
- extension to robotics or manufacturing pipelines where generated plans must bind to evolving scene entities.

### 12. Why does this matter for my work?
It matters as a reusable mechanism pattern. The interesting lesson is not CAD specifically; it is that structured generation works better when the model emits high-level executable intent and a separate grounded module resolves references against a changing internal state. That idea could transfer to scene generation, planning, and neurosymbolic world modeling.

### 13. What ideas are steal-worthy?
- Separate high-level generative intent from low-level entity grounding.
- Make intermediate state explicit and queryable during generation.
- Judge structure by executability, not by whether it looks interpretable in the paper diagram.
- Use downstream execution fidelity as part of training, not only next-token imitation.

### 14. Final decision
**Read selectively but seriously.** This is more useful as a mechanism paper than as a domain paper. If you are thinking about explicit interfaces between neural generation and executable structure, it is worth attention.

---

## Confidence / access note

This note is based on the arXiv abstract and partial HTML full text. I was able to recover the main method and problem formulation, but not the complete author list or all headline quantitative results from the truncated extract.
