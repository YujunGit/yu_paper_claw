# The Predictive-Causal Gap: An Impossibility Theorem and Large-Scale Neural Evidence

## Basic info

* Title: The Predictive-Causal Gap: An Impossibility Theorem and Large-Scale Neural Evidence
* Authors: Kejun Liu
* Year: 2026
* Venue / source: arXiv (cs.LG)
* Link: https://arxiv.org/abs/2605.05029
* Date surfaced: 2026-05-07
* Why selected in one sentence: It gives a sharp theoretical and empirical argument that predictive objectives can systematically learn latents that are useful for forecasting yet wrong for causal understanding.

## Quick verdict

**Must read**

This is the strongest paper in today’s batch because it attacks a deep assumption behind world models and predictive self-supervision instead of proposing another architecture tweak. The core claim is unusually crisp: under common conditions, predictive learning is structurally incentivized to encode the environment rather than the system of interest. Even if the setup is stylized, the framing is strong enough that it should affect how I think about objective design, evaluation, and claims of “understanding.”

## One-paragraph overview

The paper studies a simple but important mismatch: a predictor trained to minimize future-prediction error over observations is not necessarily trained to recover the causal variables we actually care about. The authors formalize this in a system-plus-environment setting, prove an impossibility result for a family of linear dynamics, then back it up with larger neural sweeps and a nonlinear experiment. Their key point is that if environment modes are slower or cleaner than system modes, a prediction objective will rationally allocate representation capacity to those easier-to-predict environmental variables, even when they are causally the wrong thing to model.

## Key questions this summary must address

### 1. What problem is the paper trying to solve?
It asks whether predictive representation learning reliably recovers the causally meaningful system state, or whether it can systematically lock onto easier but less useful environmental structure.

### 2. What is the method?
The method is mainly analytical plus diagnostic. The paper defines a predictive-risk objective, proves an impossibility theorem for linear-Gaussian dynamics, then runs large neural sweeps and a nonlinear Duffing-GRU experiment to see whether the same failure appears in practice.

### 3. What is the method motivation?
A lot of current work quietly assumes that better prediction yields better latent understanding. The paper is motivated by the suspicion that this premise is false when the observation stream mixes system variables with environmental variables that are more predictable but not the real target of reasoning or control.

### 4. What data does it use?
Mostly synthetic dynamical systems: a large family of linear-Gaussian systems plus a nonlinear Duffing oscillator coupled to a hidden Ornstein-Uhlenbeck environment. This is a strength for clean diagnosis but a limitation for external realism.

### 5. How is it evaluated?
The main diagnostic is **causal fidelity**, defined as how much encoder sensitivity lands on system degrees of freedom rather than environmental ones. The paper also compares predictive error and checks out-of-distribution robustness under environment shift.

### 6. What are the main results?
In the linear setting, the theorem says there are open sets of dynamics where every predictive-risk minimizer is misaligned with the true system variables. In the neural sweeps, average causal fidelity is low and only a small minority of runs exceed a high-fidelity threshold. In higher dimensions the effect gets worse, and in the nonlinear experiment the unconstrained predictor becomes more environment-dominant and more OOD-fragile than a grounded variant.

### 7. What is actually novel?
The novelty is not a new model; it is the combination of a constructive impossibility theorem, a concrete alignment metric, and large-scale neural evidence tied to a useful conceptual distinction between predictive and causal adequacy.

### 8. What are the strengths?
The paper is unusually clear about mechanism rather than vibes. It gives a falsifiable failure mode, proves it in a nontrivial setting, and then checks whether the same pattern persists in larger nonlinear learners. It is also valuable as framing: it separates “predictively optimal” from “causally useful” in a way many world-model papers blur.

### 9. What are the weaknesses, limitations, or red flags?
The biggest limitation is ecological validity. The setup depends on an explicit system-environment split and stylized dynamics, so the theorem does not automatically transfer to full-scale multimodal world models or language models. The causal-fidelity metric is reasonable for this setting, but it is also a designer-chosen metric whose usefulness depends on the assumed decomposition.

### 10. What challenges or open problems remain?
The obvious open problem is how to design objectives that recover the system variables we actually care about without already assuming the answer. The paper shows “just predict better” is not enough, but it does not fully solve how to define the right operational interface in realistic settings.

### 11. What future work naturally follows?
Grounded or intervention-aware objectives, partial observability settings with explicit action/control channels, and more realistic world-model benchmarks where predictive performance and causal usefulness can diverge cleanly.

### 12. Why does this matter for my work?
It matters because it weakens a lazy but common inference: that strong prediction implies good latent structure for reasoning, planning, or scientific interpretation. If I care about transferable structure, I should explicitly test for that rather than inherit predictive metrics as a proxy.

### 13. What ideas are steal-worthy?
Three steal-worthy ideas: (1) define evaluation metrics that separate predictive quality from mechanism quality; (2) create benchmarks where environment-dominant shortcuts are available so representation claims can be stress-tested; (3) use explicit operational grounding as an ablation, not just an intuition.

### 14. Final decision
**Read closely.** Even if the formal setup is narrower than the authors imply, the paper is strong enough as both a conceptual warning and a reusable evaluation lens.

## Access note
This note is based on the arXiv abstract page and substantial arXiv HTML text, not a full PDF/appendix audit. Exact baseline fairness details and some supplementary derivations were not independently verified.