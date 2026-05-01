# One Life to Learn: Inferring Symbolic World Models for Stochastic Environments from Unguided Exploration

## Basic info

* Title: One Life to Learn: Inferring Symbolic World Models for Stochastic Environments from Unguided Exploration
* Authors: Zaid Khan, Archiki Prasad, Elias Stengel-Eskin, Jaemin Cho, Mohit Bansal
* Year: 2026
* Venue / source: arXiv
* Link: https://arxiv.org/abs/2510.12088
* Date surfaced: 2026-05-01
* Why selected in one sentence: It tackles symbolic world modeling in the harder regime that actually matters—stochastic dynamics, minimal unguided interaction, and executable law induction rather than static symbolic labels.

## Quick verdict

**Must read**

This is one of the sharper recent papers in the symbolic-world-model lane because it does not hide in deterministic toy settings or assume abundant guided interaction. The main idea—a probabilistic mixture of conditionally activated programmatic laws inferred from a single unguided episode—is conceptually strong and directly relevant to executable abstraction learning. The main caution is that the environment is still a custom symbolic testbed rather than messy real perception.

## One-paragraph overview

OneLife tries to infer an executable symbolic world model from very limited experience in a hostile stochastic environment. Instead of predicting next states with one monolithic neural latent, it represents dynamics as a collection of modular laws with precondition-effect structure inside a probabilistic programming framework. A law synthesizer proposes candidate rules from exploration data, an inference procedure reweights them based on predictive usefulness, and forward simulation uses only the laws relevant to the current transition. The key claim is that this conditional, law-based decomposition makes symbolic world modeling tractable even when most rules are inactive most of the time.

## Key questions this summary must address

### 1. What problem is the paper trying to solve?
Learning symbolic world models usually assumes deterministic mechanics, lots of interaction data, or hand-designed guidance. This paper targets a harder and more realistic case: infer executable transition laws in a stochastic environment from a single unguided exploration episode.

### 2. What is the method?
A probabilistic symbolic world model represented as a mixture of modular laws. Each law has preconditions and effects, a synthesizer proposes laws from observed trajectories, and an inference routine updates only the laws relevant to changed state variables.

### 3. What is the method motivation?
If the world is complex and hierarchical, asking every rule to explain every transition is wasteful and brittle. Modular laws with conditional activation give a more scalable interface for sparse, stochastic dynamics and make the model executable for planning.

### 4. What data does it use?
It is evaluated on Crafter-OO, a re-engineered object-oriented version of Crafter that exposes structured symbolic state and a pure transition function. The key training regime is minimal unguided interaction rather than reward-shaped task data.

### 5. How is it evaluated?
The paper uses state-ranking and state-fidelity metrics over multiple scenarios, compares against a strong baseline, and also tests whether planning with the learned world model can improve multi-step decision making.

### 6. What are the main results?
The abstract claims OneLife outperforms a strong baseline on 16 of 23 tested scenarios and that the learned model is useful for planning via simulated rollouts. The important result profile is not just predictive accuracy but usable executable dynamics under severe data limits.

### 7. What is actually novel?
The meaningful novelty is not “symbolic world model” by itself. It is the combination of one-episode unguided learning, stochastic law modeling, conditional modular execution, and gradient-based reweighting over synthesized rules.

### 8. What are the strengths?
- Attacks a hard regime instead of an easy symbolic sandbox.
- Uses executable laws with real operational meaning.
- The conditional-activation design is a good answer to sparse-rule environments.
- Evaluates planning utility, not just one-step prediction.

### 9. What are the weaknesses, limitations, or red flags?
- Still depends on structured symbolic state rather than raw perception.
- Crafter-OO is richer than toy domains but still curated.
- The law synthesizer may hide substantial prompt or proposal sensitivity.
- “One life” is a compelling framing, but the exact difficulty depends on how informative that single episode is.

### 10. What challenges or open problems remain?
The big open step is learning this kind of modular executable world model from noisy perceptual streams, partial observability, and contact-rich embodied interaction. Another open problem is how to revise the symbolic law library when early hypotheses are wrong or incomplete.

### 11. What future work naturally follows?
Perception-grounded law discovery, uncertainty-aware rule revision, richer embodied environments, and tighter coupling between discovered laws and active exploration strategies.

### 12. Why does this matter for my work?
It is directly relevant to world models, neurosymbolic reasoning, compositional planning, and representation learning. It supports a research direction where the useful predictive state is executable, modular, and sparse rather than only latent and monolithic.

### 13. What ideas are steal-worthy?
- Model dynamics as conditionally activated modular laws.
- Update only the rules that touch changed variables.
- Judge world models by planning utility and state ranking, not only next-state likelihood.
- Treat minimal unguided interaction as a first-class design constraint.

### 14. Final decision
**Read now.** This is a strong mechanism paper and a better reference than many recent “symbolic world model” papers that quietly assume easier conditions.

---

## Confidence / access note

This note is based on the arXiv abstract and partial HTML paper access. I have enough to trust the main framing and mechanism, but not enough to verify every implementation detail or ablation.