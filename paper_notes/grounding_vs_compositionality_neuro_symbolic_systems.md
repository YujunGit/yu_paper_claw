# Grounding vs. Compositionality: On the Non-Complementarity of Reasoning in Neuro-Symbolic Systems

## Basic info

* Title: Grounding vs. Compositionality: On the Non-Complementarity of Reasoning in Neuro-Symbolic Systems
* Authors: Mahnoor Shahid, Hannes Rothe
* Year: 2026
* Venue / source: arXiv (accepted at AAAI MAKE 2026)
* Link: https://arxiv.org/abs/2604.26521
* Date surfaced: 2026-05-02
* Why selected in one sentence: It directly tests a common but weakly examined assumption in neuro-symbolic work—that grounded symbols alone should induce compositional reasoning.

## Quick verdict

**Highly relevant**

This is a useful diagnosis paper because it attacks a lazy premise that shows up all over neuro-symbolic and multimodal reasoning papers. The main contribution is conceptual and experimental rather than infrastructural: grounding and reasoning are separated, then shown not to be interchangeable. The caveat is that the result lives or dies by the benchmark design and the fairness of the grounding-only comparison.

## One-paragraph overview

The paper asks whether perceptual grounding is enough to produce compositional reasoning, or whether reasoning needs its own explicit training objective. To test this, it introduces an Iterative Logic Tensor Network (iLTN), a differentiable neuro-symbolic architecture for multi-step deduction, and evaluates it under different training regimes. The core finding is that a model optimized only for grounding does not generalize compositionally, while a jointly trained system with explicit reasoning objectives does. The paper’s real value is less the specific architecture than the stronger causal claim about what grounding does and does not buy you.

## Key questions this summary must address

### 1. What problem is the paper trying to solve?
Many neuro-symbolic systems quietly assume that once symbols are well grounded in perception, compositional reasoning will emerge. This paper tests that assumption directly.

### 2. What is the method?
A differentiable multi-step neuro-symbolic architecture called iLTN, paired with an evaluation taxonomy that separates novel entities, unseen relations, and harder rule compositions.

### 3. What is the method motivation?
If grounding and reasoning are conflated, the field risks misdiagnosing why systems fail to generalize. The motivation is to disentangle the two capabilities rather than treating them as one blob.

### 4. What data does it use?
From the abstract, it uses controlled compositional-generalization tasks designed to probe different forms of novelty. I do not yet have full dataset details from the full paper.

### 5. How is it evaluated?
The paper compares grounding-only versus jointly trained grounding-plus-reasoning settings and measures zero-shot generalization over multiple compositional regimes.

### 6. What are the main results?
Grounding alone fails to generalize compositionally, whereas the full joint system achieves high zero-shot accuracy across the tested categories.

### 7. What is actually novel?
The strongest novelty is the explicit empirical disentangling of grounding from reasoning. That is more valuable than yet another vague claim that a hybrid architecture is “more compositional.”

### 8. What are the strengths?
- Sharp question with real field-level relevance.
- Refuses to treat grounding and reasoning as interchangeable.
- Uses a taxonomy of generalization failure modes instead of a single score.
- Gives a concrete citation against overclaiming from grounding success.

### 9. What are the weaknesses, limitations, or red flags?
- The impact depends on how realistic and challenging the controlled tasks are.
- A positive result for explicit reasoning objectives is not the same as showing scalability.
- The conclusion may be stronger conceptually than practically if the setup remains synthetic.
- I have not yet checked how competitive the non-reasoning baselines really are.

### 10. What challenges or open problems remain?
The harder question is how to inject explicit reasoning objectives into large perceptual systems without making them brittle, expensive, or benchmark-specific.

### 11. What future work naturally follows?
Perception-grounded reasoning benchmarks with richer observation spaces, more realistic transfer settings, and finer analysis of what kinds of reasoning supervision matter most.

### 12. Why does this matter for my work?
It matters as framing, critique, and defense. If your work cares about compositionality, this paper helps argue that better symbol grounding alone is not enough; explicit reasoning pressure may need to be part of the method.

### 13. What ideas are steal-worthy?
- Separate grounding and reasoning experimentally rather than assuming they co-emerge.
- Evaluate distinct kinds of compositional novelty instead of one aggregate metric.
- Treat explicit reasoning objectives as first-class design choices.

### 14. Final decision
**Read selectively, probably soon.** Even if the full method is not your endgame, the paper is useful for framing and for pruning weak assumptions.

---

## Confidence / access note

This note is based on the arXiv abstract and partial HTML paper access. I am confident in the main claim and setup framing, but not yet in the fine details of the benchmarks or optimization scheme.