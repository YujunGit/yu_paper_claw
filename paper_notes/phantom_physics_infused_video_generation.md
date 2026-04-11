# Phantom: Physics-Infused Video Generation via Joint Modeling of Visual and Latent Physical Dynamics

## Basic info

* Title: Phantom: Physics-Infused Video Generation via Joint Modeling of Visual and Latent Physical Dynamics
* Authors: Ying Shen, Jerry Xiong, Tianjiao Yu, Ismini Lourentzou
* Year: 2026
* Venue / source: arXiv / CVPR 2026
* Link: https://arxiv.org/abs/2604.08503
* Date surfaced: 2026-04-11
* Why selected in one sentence: It internalizes a latent physics branch inside a video generator instead of relying on prompt-time or post-hoc physics guidance.

## Quick verdict

**Useful**

The central mechanism is interesting and more honest than a lot of “physics-aware” video work: the model jointly predicts video content and latent physical dynamics through a coupled dual-branch architecture. I am less convinced that the latent state here amounts to real physical understanding, because the physics signal is inherited from a learned representation rather than grounded in an explicit dynamical model. Still, the design is worth tracking.

## One-paragraph overview

Phantom augments a pretrained video generation model with a parallel physics branch that operates in a latent representation space derived from V-JEPA2 embeddings. The model jointly predicts future visual latents and future latent physical states, with bidirectional cross-attention allowing the visual and physics branches to influence each other during generation. The goal is to improve physical plausibility without depending on external simulators, prompt engineering, or inference-time physical reasoning scaffolds.

## Key questions this summary must address

### 1. What problem is the paper trying to solve?
It aims to address the gap between visual realism and physical plausibility in generative video models. Current models often generate convincing-looking videos that still violate basic physical expectations.

### 2. What is the method?
The method is a dual-branch flow-matching architecture built on top of a pretrained video generator. One branch models visual latent trajectories, the other models latent physical dynamics using physics-aware embeddings extracted from V-JEPA2, and the two branches exchange information through cross-attention while jointly predicting future states.

### 3. What is the method motivation?
The motivation is that next-frame prediction alone does not force models to internalize physical dynamics. If physical state is modeled jointly during training, the generator may develop a more usable internal representation of dynamics.

### 4. What data does it use?
It uses standard video-generation data and evaluates on physics-focused video benchmarks such as VideoPhy, VideoPhy-2, and Physics-IQ. From the available text, the paper does not require explicit simulators or manually labeled physical variables at test time.

### 5. How is it evaluated?
The model is evaluated on both standard perceptual video-generation metrics and dedicated physics-aware benchmarks. The key question is whether physical-consistency gains come without collapsing visual fidelity.

### 6. What are the main results?
The paper reports consistent gains over its base generator on multiple physics-aware benchmarks while keeping perceptual quality competitive. The exact claims include large improvements on VideoPhy and Physics-IQ, suggesting that the added branch is doing something useful at least by current benchmark definitions.

### 7. What is actually novel?
The important novelty is not merely “add physics features.” It is the joint generative treatment of visual and latent physical dynamics through a trainable coupled architecture, rather than injecting physics only through prompts, external simulators, or latent alignment losses.

### 8. What are the strengths?
- Better mechanism story than prompt-level physics guidance.
- Physics is inside the generator, not only outside it.
- Reuses a pretrained physics-aware representation rather than hand-specifying physical variables.
- Clear empirical target: improve physical consistency without sacrificing realism.

### 9. What are the weaknesses, limitations, or red flags?
- The latent physics representation is still indirect and learned, not an explicit physical state.
- Success on current physics benchmarks may overstate actual mechanistic understanding.
- The method depends on the quality and biases of V-JEPA2’s representation space.
- It is still unclear whether the resulting latent dynamics are controllable, interpretable, or useful beyond better benchmark scores.

### 10. What challenges or open problems remain?
The biggest open problem is whether latent physics embeddings can support controllable, compositional, or intervention-aware generation rather than just improved passive prediction. Another is disentangling genuine physical structure from benchmark-specific shortcuts.

### 11. What future work naturally follows?
- Add intervention-based evaluations rather than only benchmark scoring.
- Expose the latent physics branch as a controllable interface.
- Compare against explicit state or simulator-grounded models more aggressively.
- Test transfer to downstream planning or world-model settings.

### 12. Why does this matter for my work?
It matters because it offers one plausible route to embedding structured dynamics into a generator without demanding fully explicit simulators. Even if imperfect, it is a useful design point between raw scaling and hard-coded physics.

### 13. What ideas are steal-worthy?
- Jointly predict appearance and latent dynamics instead of collapsing everything into one stream.
- Use cross-attention between visual and dynamics branches.
- Reuse a self-supervised physics-aware encoder as latent state supervision.
- Judge “physics-aware generation” by whether dynamics live inside the model, not only in prompts.

### 14. Final decision
**Worth skimming carefully.** I would not overclaim this as a true world model, but it is a meaningful step beyond superficial physics prompting.

---

## Confidence / access note

This note is based on the arXiv abstract plus substantial arXiv HTML text, including the introduction, related-work positioning, and parts of the method section. I have moderate confidence in the architectural summary and the main critique, but I did not verify every experimental detail from the full paper.