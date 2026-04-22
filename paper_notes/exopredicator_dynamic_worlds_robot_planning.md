# ExoPredicator: Learning Abstract Models of Dynamic Worlds for Robot Planning

## Basic info

* Title: ExoPredicator: Learning Abstract Models of Dynamic Worlds for Robot Planning
* Authors: Yichao Liang, Dat Nguyen, Cambridge Yang, Tianyang Li, Joshua B. Tenenbaum, Carl Edward Rasmussen, Adrian Weller, Zenna Tavares, Tom Silver, Kevin Ellis
* Year: 2026
* Venue / source: ICLR 2026 / arXiv
* Link: https://arxiv.org/abs/2509.26255
* Date surfaced: 2026-04-22
* Why selected in one sentence: It extends learned abstract world models beyond action-triggered transitions by explicitly modeling delayed exogenous causal processes.

## Quick verdict

**Highly relevant**

This is a serious abstraction paper, not just symbolic decoration. The attractive part is that it treats time-evolving external mechanisms as first-class objects in the world model, which is a real blind spot in many learned planning abstractions. My main caution is that the evidence I checked is limited to abstract and early sections, so the exact scope of the empirical win and failure cases still need a full read.

## One-paragraph overview

The paper argues that long-horizon planning needs more than abstract symbolic states. It also needs abstractions for processes that continue unfolding after the agent acts, like water heating or dominoes cascading. ExoPredicator learns abstract world models with two linked components: predicates that map observations into symbolic state, and causal processes that can be either endogenous actions or exogenous mechanisms with delayed stochastic effects. These models are learned from limited data using variational Bayesian inference plus LLM proposals, then used by a planner that reasons over discrete abstract jumps instead of frame-by-frame simulation.

## Key questions this summary must address

### 1. What problem is the paper trying to solve?
It is trying to solve long-horizon robot planning in environments where important changes occur autonomously over time, not only as immediate consequences of the agent’s actions.

### 2. What is the method?
The method learns an abstract world model composed of symbolic predicates and causal-process schemas. Each process has start conditions, persistence conditions, delayed effects, and stochastic strength, allowing the planner to reason about both agent actions and external processes in one abstraction.

### 3. What is the method motivation?
The motivation is that many abstraction learners effectively assume a classical instantaneous-action world. That misses a large class of realistic tasks where the agent triggers a process and then must plan around its delayed evolution.

### 4. What data does it use?
From the accessible text, the experiments use five simulated tabletop robotics environments and limited interaction data. The paper also assumes built-in low-level skills such as pick and place.

### 5. How is it evaluated?
It is evaluated on fast planning and generalization to held-out tasks with more objects and more complex goals, compared with several baseline approaches.

### 6. What are the main results?
The paper claims the learned models outperform a range of baselines across five simulated environments, especially on held-out tasks requiring reasoning about temporal physical constraints and exogenous change. I did not verify the full result tables numerically.

### 7. What is actually novel?
The key novelty is not predicate learning by itself. It is the joint abstraction of state and delayed causal processes, including exogenous mechanisms that evolve independently once activated.

### 8. What are the strengths?
- Better problem formulation than action-only symbolic abstraction.
- Explicitly handles delayed and concurrent external dynamics.
- Uses abstraction for planning speed, not only interpretability theater.
- The representation is conceptually close to what many embodied systems actually need.
- Bayesian learning of process structure is more serious than pure prompting-based symbolic proposal.

### 9. What are the weaknesses, limitations, or red flags?
- The current evidence is in simulated tabletop domains, which may undersell real perceptual noise and control messiness.
- Predicate representations still rely on VLM-queryable functions, so perception may be a practical bottleneck.
- The abstraction may become brittle if exogenous processes are numerous, continuous, or poorly factorized.
- It is still a high-level planner sitting on assumed low-level skills, not an end-to-end embodied learner.

### 10. What challenges or open problems remain?
Open problems include scaling to richer real-world exogenous dynamics, handling latent or partially observed process state, and learning when abstraction granularity is too coarse for safe control.

### 11. What future work naturally follows?
- Combine process abstractions with uncertainty-aware perception and execution monitoring.
- Learn object-centric continuous state alongside symbolic process structure.
- Extend the framework to real robot data with asynchronous sensor noise and failure recovery.
- Study whether similar process abstractions help generative world models, not only planners.

### 12. Why does this matter for my work?
It matters because it sharpens an important design question: if the world keeps changing after the agent acts, then a useful world model should abstract processes, not just states. That framing is highly relevant to compositional planning and embodied reasoning.

### 13. What ideas are steal-worthy?
- Model exogenous processes explicitly instead of forcing everything into action effects.
- Learn abstractions over temporal granularity, not only perceptual state.
- Separate endogenous control from autonomous world dynamics in the planner’s representation.
- Use abstract delayed processes to make long-horizon planning tractable.

### 14. Final decision
**Read soon.** The representation idea is strong and directly relevant to structured world modeling, even if the current validation still looks mostly like controlled robotics simulation.

---

## Confidence / access note

This note is based on the arXiv abstract and early HTML sections, not a full PDF read. The causal-process representation and motivation are clearly supported, but the exact ablation depth and empirical edge over each baseline still need full-paper confirmation.
