# Thinking Deeper, Not Longer: Depth-Recurrent Transformers for Compositional Generalization

## Basic info

* Title: Thinking Deeper, Not Longer: Depth-Recurrent Transformers for Compositional Generalization
* Authors: Hung-Hsuan Chen and collaborators (full author list not verified from the abstract page)
* Year: 2026
* Venue / source: arXiv
* Link: https://arxiv.org/abs/2603.21676
* Date surfaced: 2026-04-03
* Why selected in one sentence: It offers a concrete mechanism for variable-depth inference in a shared-weight Transformer, which is more interesting than generic test-time reasoning claims.

## Quick verdict

**Useful**

The paper is worth attention because it gives a specific architectural recipe for inference-time depth scaling rather than treating longer reasoning as a prompting trick. The key contribution is not the headline that more compute helps, but the stabilizing design choices that make 20+ recurrent reasoning steps viable. The main limitation is that the tasks are controlled compositional reasoning settings rather than broad real-world generation or embodied decision-making.

## One-paragraph overview

This paper proposes a depth-recurrent Transformer that repeatedly applies a shared-weight Transformer block in latent space, allowing the model to increase computational depth at inference time without increasing parameter count. To stabilize deep recurrence, it combines a final-output-only “silent thinking” objective, LayerScale initialization, and identity-biased recurrence. The system is tested on graph reachability, nested boolean logic, and unstructured relational text, where the authors report a computational frontier: performance rises sharply once the number of recurrent thinking steps matches task complexity. The broader claim is that a task-invariant recurrent reasoning core can support compositional generalization better than a fixed-depth feedforward stack.

## Key questions this summary must address

### 1. What problem is the paper trying to solve?
It targets the fixed-depth limitation of standard Transformers on tasks that require variable-depth reasoning, especially compositional tasks where difficulty scales with the structure of the input.

### 2. What is the method?
A shared-weight Transformer block is applied recurrently in latent space. Three stabilizers are added: silent thinking supervision on the final output only, LayerScale initialization, and identity-biased recurrence.

### 3. What is the method motivation?
The motivation is that many reasoning problems require variable internal computation, but standard Transformers have a fixed number of layers. If reasoning depth matters, the model should be able to spend more computation when the task demands it.

### 4. What data does it use?
The abstract mentions three reasoning domains: graph reachability, nested boolean logic, and unstructured relational text. These are synthetic or controlled tasks designed to probe compositional generalization.

### 5. How is it evaluated?
The evaluation measures how performance changes as recurrent thinking steps scale with task complexity and compares generalization behavior across tasks with different inductive biases.

### 6. What are the main results?
The paper reports a clear computational frontier where performance shifts from chance to near-perfect as recurrence depth increases appropriately. It also reports different styles of generalization across graph, logic, and text settings.

### 7. What is actually novel?
The novelty is not just adding recurrence. It is the combination of a shared recurrent reasoning core with specific training/stabilization choices that make deep latent recurrence usable and interpretable as a mechanism for variable-depth reasoning.

### 8. What are the strengths?
- Mechanism-first framing rather than prompt-centric “thinking” rhetoric.
- Clean separation between parameter count and inference-time compute.
- The idea of a task-invariant reasoning core plus task-specific interfaces is transferable.
- The computational-frontier framing is a useful lens for future experiments.

### 9. What are the weaknesses, limitations, or red flags?
- Controlled reasoning tasks can flatter architectures that may not scale cleanly to messy real-world settings.
- The paper may show that more depth helps without fully resolving how to decide when to stop or how to allocate compute adaptively.
- It is not obvious that latent recurrence alone gives the kind of modularity or interpretability many compositionality papers promise.
- Without the full paper, I cannot inspect baselines, training cost, or whether simpler recurrent baselines already capture most of the gain.

### 10. What challenges or open problems remain?
A major open problem is extending variable-depth reasoning from toy or controlled settings to multimodal generation, planning, and embodied tasks where perceptual uncertainty and memory matter.

### 11. What future work naturally follows?
- Adaptive halting or uncertainty-based compute allocation.
- Combining recurrent reasoning cores with explicit memory or symbolic state.
- Plugging this style of depth scaling into world models or structured planners.
- Testing whether the recurrent core improves controllable generation or long-horizon decision making.

### 12. Why does this matter for my work?
It matters if you care about reusable reasoning mechanisms rather than just larger models. The idea of a shared reasoning core with scalable inference-time depth could transfer to structured generation, planning, or world-model rollouts.

### 13. What ideas are steal-worthy?
- Decouple reasoning depth from parameter count.
- Treat “thinking” as latent recurrent computation, not only extra output tokens.
- Use final-output-only supervision to discourage shallow shortcut traces.
- Analyze task difficulty through a compute frontier rather than a single operating point.

### 14. Final decision
**Good conceptual read.** Probably not a direct baseline for your current repo, but useful if you are collecting mechanism-level ideas about compositional reasoning.

---

## Confidence / access note

This note is based on the arXiv abstract page only. I could verify the architecture idea and headline claims, but not the detailed recurrence equations, baselines, or training dynamics.
