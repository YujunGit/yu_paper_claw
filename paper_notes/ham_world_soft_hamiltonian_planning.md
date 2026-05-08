# HaM-World: Soft-Hamiltonian World Models with Selective Memory for Planning

## Basic info

* Title: HaM-World: Soft-Hamiltonian World Models with Selective Memory for Planning
* Authors: Listed on the arXiv entry (not re-audited here author-by-author)
* Year: 2026
* Venue / source: arXiv
* Link: https://arxiv.org/abs/2605.05951
* Date surfaced: 2026-05-08
* Why selected in one sentence: It proposes a planner-facing latent structure with explicit role separation between canonical dynamics, semantic/non-conservative context, and history-conditioned memory.

## Quick verdict

**Must read**

This is one of the better recent “structured world model” papers because the structure is not decorative. The q/p/c split and selective memory are used by the same latent state that supports rollout, reward/value prediction, and CEM planning. The evidence is still in controlled continuous-control settings, so the embodied scaling story is not solved, but the mechanism is concrete and testable.

## One-paragraph overview

The paper argues that world-model planning fails for two linked reasons: the latent state is often not Markov enough under partial observability, and it also entangles qualitatively different factors like configuration, momentum, and task semantics. HaM-World addresses this by combining selective sequence memory with a latent split into canonical coordinates q/p and a context variable c. The q/p subspace is updated with a soft Hamiltonian prior plus residual/control terms, while c absorbs semantic and dissipative factors that should not be forced into conservative physics. The result is a single planner-facing latent used for imagined rollouts, reward/value estimation, and CEM action search.

## Key questions this summary must address

### 1. What problem is the paper trying to solve?
Long-horizon rollout drift and poor OOD planning robustness in latent world models, especially when latents are both under-informed by history and over-entangled internally.

### 2. What is the method?
A world model with: (i) Mamba selective memory for history-conditioned state completion, (ii) a latent split z=[q,p,c], and (iii) soft-Hamiltonian dynamics on q/p plus learned residual/control dynamics, with c carrying semantics and non-conservative effects.

### 3. What is the method motivation?
Planning needs both approximate Markov completeness and geometry that respects dynamics. A single opaque latent makes neither explicit.

### 4. What data does it use?
Four DeepMind Control Suite tasks.

### 5. How is it evaluated?
Control AUC, long-horizon rollout MSE, 12 OOD perturbation settings, and mechanism-oriented diagnostics like energy drift and latent geometry behavior.

### 6. What are the main results?
It reports best average AUC, lower long-horizon rollout error than strong baselines, and strongest OOD returns across the tested perturbations.

### 7. What is actually novel?
Not “physics in world models” by itself. The novelty is the coupled planner-facing design: selective memory for approximate Markovity plus a q/p/c role split where only part of the latent is given Hamiltonian structure.

### 8. What are the strengths?
- Structure is attached to the state the planner actually uses.
- Good mechanism taste: rollout stability and OOD robustness are evaluated, not just return.
- The soft-Hamiltonian design is more realistic than strict conservation in controlled dissipative systems.

### 9. What are the weaknesses, limitations, or red flags?
- Evidence is still in relatively clean control benchmarks, not perception-heavy robotics.
- The q/p/c partition is principled but still hand-designed.
- “Hamiltonian” can become branding if the benefit mostly comes from regularization plus memory; the causal contribution needs careful ablation reading.

### 10. What challenges or open problems remain?
Learning this kind of structure directly from raw visual input, dealing with contact-rich real robotics, and knowing when the canonical split is actually appropriate.

### 11. What future work naturally follows?
Pixel-based versions, object-centric or geometry-grounded variants, uncertainty-aware extensions, and tests in manipulation rather than DMControl only.

### 12. Why does this matter for my work?
It is a good example of planner-facing structure that actually constrains rollouts. The useful lesson is not “use Hamiltonians everywhere,” but “separate conservative dynamics, non-conservative context, and history completion instead of hiding them in one latent.”

### 13. What ideas are steal-worthy?
- Separate latent roles by downstream use, not by interpretability aesthetics.
- Treat memory and latent geometry as coupled design decisions.
- Evaluate world models on planner-facing OOD perturbations, not visual prediction alone.

### 14. Final decision
**Read.** This is one of today’s strongest mechanism papers and worth citing or borrowing from when arguing for structured planner-facing latents.
