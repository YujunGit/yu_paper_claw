# ADAPT: Benchmarking Commonsense Planning under Unspecified Affordance Constraints

## Basic info

* Title: ADAPT: Benchmarking Commonsense Planning under Unspecified Affordance Constraints
* Authors: Pei-An Chen, Yong-Ching Liang, Jia-Fong Yeh, Hung-Ting Su, Yi-Ting Chen, Min Sun
* Year: 2026
* Venue / source: arXiv preprint
* Link: https://arxiv.org/abs/2604.14902
* Date surfaced: 2026-04-18
* Why selected in one sentence: It makes implicit affordance preconditions an explicit planning problem instead of assuming instruction-following agents will infer them for free.

## Quick verdict

**Useful**

This looks like a solid and relevant interface paper, not a breakthrough. Its strongest contribution is framing dynamic affordance inference as a missing planning module in embodied instruction following, plus introducing a benchmark that makes that failure mode visible. Based on abstract-level access, the main risk is that the method may be more of a well-targeted augmentation layer than a deeper representational advance.

## One-paragraph overview
The paper argues that embodied agents often fail because instructions do not spell out whether an object is currently manipulable, openable, reachable, or otherwise usable. To test that problem, it introduces DynAfford, a benchmark with dynamic and unspecified affordance constraints, and ADAPT, a plug-in module that augments existing planners with explicit affordance reasoning. The system appears to use perception to infer latent object-state preconditions and then feeds those inferred affordances into downstream planning, improving robustness in seen and unseen environments.

## Key questions this summary must address

### 1. What problem is the paper trying to solve?
Embodied planners often act as if instructions fully specify the task, but many real tasks depend on hidden or changing affordance constraints. The paper targets this gap.

### 2. What is the method?
A benchmark called DynAfford plus a plug-in planning augmentation called ADAPT. ADAPT explicitly infers affordances or preconditions that are not given in the instruction and uses them to improve planning.

### 3. What is the method motivation?
Instruction following fails when the agent cannot tell whether the intended object interaction is currently possible. The authors want a layer that reasons about object state and latent preconditions before action execution.

### 4. What data does it use?
From the abstract, the central evaluation setting is DynAfford, a benchmark of dynamic embodied environments with unspecified affordance constraints. I have not verified the full dataset construction details from the paper body.

### 5. How is it evaluated?
The abstract says it is tested across seen and unseen environments and compared both with and without the ADAPT module. It also compares different affordance-inference backends, including a task-adapted VLM and GPT-4o.

### 6. What are the main results?
The reported result is that ADAPT substantially improves robustness and task success, and that a domain-adapted LoRA-finetuned VLM outperforms GPT-4o as the affordance inference backend.

### 7. What is actually novel?
The main novelty seems to be the problem framing and benchmark design, plus the explicit insertion of affordance reasoning into the planning stack. That is more interesting than claiming a new end-to-end policy.

### 8. What are the strengths?
- Targets a real failure mode rather than a cosmetic modularity story.
- Makes hidden preconditions measurable instead of anecdotal.
- Keeps the affordance layer explicit and inspectable.
- The comparison against a generic large model is useful, because it tests whether task-specific grounding still matters.

### 9. What are the weaknesses, limitations, or red flags?
- Based on current access, the method may still rely on relatively narrow benchmark construction and curated affordance categories.
- A plug-in module can improve robustness without fundamentally changing representation quality.
- It is not yet clear how open-ended the affordance space really is, or whether this mainly handles benchmark-local preconditions.

### 10. What challenges or open problems remain?
Scaling from benchmark-defined affordances to messier real-world object states, partial observability, long-horizon error accumulation, and uncertainty-aware replanning.

### 11. What future work naturally follows?
Learning richer latent preconditions from interaction data, combining affordance inference with explicit world-state memory, and propagating uncertainty from affordance estimates into the planner.

### 12. Why does this matter for my work?
It is a useful citation for the claim that explicit intermediate structure still matters in embodied systems. More specifically, it supports the idea that some planning failures come from missing latent state variables, not from weak action decoders alone.

### 13. What ideas are steal-worthy?
- Treat missing preconditions as a first-class inference target.
- Evaluate planners on tasks where instructions intentionally under-specify what matters.
- Compare generic foundation backends against domain-adapted grounding modules instead of assuming larger models dominate.

### 14. Final decision
**Save, cite selectively, do not overrate.** This is worth keeping as a concrete embodied-planning paper about implicit constraints, but it currently looks more like a sharp problem-interface contribution than a major conceptual leap.
