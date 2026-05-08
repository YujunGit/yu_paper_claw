# Hitting Time Isomorphism for Multi-Stage Planning with Foundation Policies

## Basic info

* Title: Hitting Time Isomorphism for Multi-Stage Planning with Foundation Policies
* Authors: Listed on the arXiv entry (not re-audited here author-by-author)
* Year: 2026
* Venue / source: arXiv
* Link: https://arxiv.org/abs/2605.06470
* Date surfaced: 2026-05-08
* Why selected in one sentence: It gives a cleaner theoretical target for long-horizon compositional planning representations: directed temporal progress via hitting times.

## Quick verdict

**Highly relevant**

This is more theory-heavy than the other picks, but it has real conceptual bite. The paper argues that if you want representations for multi-stage planning, symmetric distances are the wrong primitive; expected hitting time is closer to the object you actually need. I would not trust it yet as a broad empirical answer, but I do think the framing is stronger than most foundation-policy papers.

## One-paragraph overview

The paper proposes an operator-theoretic representation-learning framework for offline reinforcement learning where the key geometric object is expected hitting time to goals, not symmetric similarity. Under a latent linear-closure assumption, the authors show that hitting times can be represented as linear functionals of latent displacements in a Hilbert space, yielding an identifiable directed temporal geometry up to bounded linear isomorphism. They then instantiate this theory in Isomorphic Embedding Learning (IEL), a goal-agnostic foundation-policy learning algorithm that regresses hitting-time structure and uses graph-based stitching for multi-stage planning.

## Key questions this summary must address

### 1. What problem is the paper trying to solve?
Learning reusable offline representations for long-horizon, multi-stage planning where planning progress is directional and compositional, not merely based on symmetric proximity.

### 2. What is the method?
Theoretical characterization of hitting-time-based latent geometry plus an algorithm, IEL, that learns embeddings and planning scores from offline trajectories.

### 3. What is the method motivation?
Many existing foundation-policy representations fail one of three things: directionality, triangle-like compositional structure, or unsupervised policy learning.

### 4. What data does it use?
Offline maze/goal-conditioned locomotion style benchmarks, according to the paper’s summary.

### 5. How is it evaluated?
Against prior offline goal-conditioned RL / foundation-policy baselines, especially on multi-stage planning performance.

### 6. What are the main results?
The paper claims state-of-the-art improvements on six offline goal-conditioned RL benchmarks and argues that directional distance plus graph-based planning each add value.

### 7. What is actually novel?
The most novel part is the representation target itself: hitting-time isomorphism as the invariant object for multi-stage planning, with identifiability and finite-sample arguments.

### 8. What are the strengths?
- Stronger conceptual target than generic metric embedding.
- Clear link between theory and planner composition.
- Useful criticism of symmetric latent geometry for irreversible environments.

### 9. What are the weaknesses, limitations, or red flags?
- The theory depends on linear-closure style assumptions that may be fragile in rich embodied settings.
- Empirical evidence appears concentrated in navigation-style benchmarks rather than perception-heavy robotics.
- “Foundation policy” language may overreach relative to current benchmark scope.

### 10. What challenges or open problems remain?
Extending the idea to high-dimensional perception, partial observability, contact-rich control, and broader task families without losing the mathematical clarity.

### 11. What future work naturally follows?
Visual versions, integration with world models, uncertainty-aware hitting-time estimates, and hierarchical planning systems that mix symbolic subgoal graphs with learned temporal geometry.

### 12. Why does this matter for my work?
It sharpens the question of what a compositional planning representation should preserve. If the downstream use is staged planning, directed progress may be a more faithful target than Euclidean semantic closeness.

### 13. What ideas are steal-worthy?
- Use direction-sensitive temporal geometry as a representation criterion.
- Judge planning embeddings by whether local distances compose through intermediate subgoals.
- Separate “good retrieval embedding” from “good planning embedding.”

### 14. Final decision
**Read for framing and theory.** Even if the exact algorithm does not transfer, the paper gives a better language for discussing compositional long-horizon planning.
