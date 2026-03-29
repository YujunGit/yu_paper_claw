# WildWorld: A Large-Scale Dataset for Dynamic World Modeling with Actions and Explicit State toward Generative ARPG

## Basic info

* Title: WildWorld: A Large-Scale Dataset for Dynamic World Modeling with Actions and Explicit State toward Generative ARPG
* Authors: Zhen Li, Zian Meng, Shuwei Shi, Wenshuo Peng, Yuwei Wu, Bo Zheng, Chuanhao Li, Kaipeng Zhang
* Year: 2026
* Venue / source: arXiv
* Link: https://arxiv.org/abs/2603.23497
* Date surfaced: 2026-03-29
* Why selected in one sentence: It is a useful recent benchmark paper because it exposes explicit state and state-alignment evaluation for interactive world modeling, instead of conflating action control with pixel change.

## Quick verdict

**Useful**

This is not the deepest methodological paper today, but it is one of the cleaner dataset/benchmark contributions for state-aware world modeling. The key value is not the 108M-frame scale by itself; it is the decision to log explicit world state, skeletons, camera pose, depth, and a rich action space, then evaluate both action following and state alignment. The main caution is obvious: it is still a game-derived dataset, so transfer to real-world embodied dynamics is limited.

## One-paragraph overview

WildWorld is a large-scale action-conditioned video/world-model dataset collected from *Monster Hunter: Wilds*. The paper argues that many existing datasets entangle actions with visible pixel changes and therefore do not force models to represent the latent world state that mediates future outcomes. To address that, it logs per-frame actions, skeletons, world-state variables, camera poses, and depth, and pairs the dataset with WildBench, a benchmark that measures not only whether generated trajectories follow actions but also whether their underlying state evolution remains aligned with ground truth. The core contribution is better infrastructure for training and evaluating interactive world models that claim to be state-aware.

## Key questions this summary must address

### 1. What problem is the paper trying to solve?
It targets a data/evaluation problem: many “interactive world model” datasets are weak proxies because their actions are simple and their consequences are visually obvious, so a model can look action-conditioned without really modeling latent state transitions.

### 2. What is the method?
The paper builds a data acquisition and automated gameplay pipeline inside a photorealistic AAA game to log RGB video together with actions, skeletons, world states, camera poses, and depth. It also introduces WildBench with two main metrics: Action Following and State Alignment.

### 3. What is the method motivation?
The motivation is sensible. If actions affect internal state variables that are only partially visible, then world models should be tested on whether they preserve the hidden state logic, not just whether frames look plausible after a keyboard command.

### 4. What data does it use?
WildWorld contains over 108 million frames, more than 450 actions, and synchronized annotations for skeletons, depth, camera pose, and world state, all collected from *Monster Hunter: Wilds*.

### 5. How is it evaluated?
The benchmark evaluates generated sequences on action following and state alignment, including state-transition quality inferred from skeletal consistency and other annotations. The paper also compares baseline models for state-aware video generation.

### 6. What are the main results?
The main result is negative but useful: current models still struggle with semantically rich actions and long-horizon state consistency, even on a benchmark designed to expose those weaknesses. That is more informative than another leaderboard showing tiny visual gains.

### 7. What is actually novel?
The novelty is not just “big game dataset.” The more important parts are:
- explicit per-frame state annotations,
- a richer action space than simple movement/camera control,
- evaluation that separates action following from state consistency.

### 8. What are the strengths?
- Better problem formulation for interactive world models.
- Explicit state supervision is more diagnostic than pure video evaluation.
- The benchmark seems designed to expose long-horizon failure, not hide it.
- Useful citation for arguing that state matters beyond appearance.

### 9. What are the weaknesses, limitations, or red flags?
- It is still constrained by the inductive biases of a specific game engine and genre.
- Large scale can be impressive without guaranteeing conceptual diversity.
- Explicit state labels from a simulator are easier to obtain than in real embodied settings, so real-world transfer is uncertain.
- Dataset papers can overstate downstream significance if baseline methods remain underdeveloped.

### 10. What challenges or open problems remain?
The big open problem is how to translate state-aware world-modeling lessons from game data to robotics or physical environments with noisy, partial, and ambiguous state observations.

### 11. What future work naturally follows?
- Adapt similar state-aware logging to robotics simulators or real robot datasets.
- Learn world models that explicitly factor hidden state from observations.
- Design evaluation for persistent memory, causality, and intervention sensitivity.
- Study whether explicit state annotations can supervise better abstractions rather than only better metrics.

### 12. Why does this matter for my work?
It matters mainly as framing and benchmark support. If you want to argue that world models should be judged on structured state transition fidelity rather than cinematic realism, this is a helpful recent citation.

### 13. What ideas are steal-worthy?
- Separate action alignment from state alignment in evaluation.
- Treat explicit state as benchmark scaffolding, not only training supervision.
- Use richer action semantics to stress-test long-horizon consistency.
- Make hidden-state failure visible in the metric design.

### 14. Final decision
**Keep as a citation and benchmark reference, not as today’s main read.** Useful infrastructure paper, but not the day’s deepest mechanism paper.

---

## Confidence / access note

This note is based on the arXiv abstract and partial HTML full text. I could verify the dataset scope, annotations, and evaluation framing, but not all baseline details or metric definitions from the complete paper.