# On the Expressive Power and Limitations of Multi-Layer SSMs

## Basic info

* Title: On the Expressive Power and Limitations of Multi-Layer SSMs
* Authors: Nikola Zubić, Qian Li, Yuyi Wang, Davide Scaramuzza
* Year: 2026
* Venue / source: arXiv
* Link: https://arxiv.org/abs/2604.14501
* Date surfaced: 2026-04-20
* Why selected in one sentence: It gives a useful theoretical account of when multi-layer SSMs fail on compositional tasks and why online intermediate computation changes the story.

## Quick verdict

**Useful**

This is theory, not a new practical architecture, but it is one of the more relevant theory papers for anyone who cares about compositional reasoning and sequence-model limitations. The strongest contribution is the contrast between offline and online chain-of-thought, which helps separate “extra tokens” from “extra computation at the right time.” I only read the abstract and part of the arXiv HTML, so this is not a theorem-by-theorem verification.

## One-paragraph overview

The paper studies what multi-layer state-space models can and cannot express, especially on compositional tasks based on function composition. It proves lower bounds showing that without the right resources, multi-layer SSMs face real limitations, then shows that online chain-of-thought can dramatically increase their computational power while offline chain-of-thought does not fundamentally help. It also analyzes tradeoffs between width and precision, arguing that these are not freely interchangeable in the base model but become much more fungible once online intermediate computation is allowed.

## Key questions this summary must address

### 1. What problem is the paper trying to solve?
It aims to clarify the real expressive limits of multi-layer SSMs, especially relative to compositional computation and the recent hype around chain-of-thought.

### 2. What is the method?
A theoretical analysis using communication-complexity style lower bounds, explicit constructions for upper bounds, and formal definitions of offline versus online chain-of-thought for SSMs.

### 3. What is the method motivation?
SSMs are increasingly used at scale, but empirical success does not tell you which structured computations they can reliably implement. The paper wants a principled account of where depth, precision, and intermediate computation actually matter.

### 4. What data does it use?
No empirical dataset in the usual sense. The central setting is formal compositional tasks based on function composition and streaming-algorithm style reasoning.

### 5. How is it evaluated?
By theorems, lower bounds, equivalence results, and constructive proofs rather than benchmark experiments.

### 6. What are the main results?
The paper claims multi-layer SSMs have provable limitations on compositional tasks, offline chain-of-thought does not remove those limits, and online chain-of-thought can elevate them to the power of streaming algorithms. It also argues width and precision are not equivalent resources in the base model.

### 7. What is actually novel?
The useful novelty is the unified framing across three axes: compositional lower bounds, the timing of chain-of-thought, and width-precision tradeoffs. The online versus offline distinction feels especially important.

### 8. What are the strengths?
- Sharp theoretical question.
- Distinguishes two kinds of chain-of-thought that are often conflated.
- Gives language for discussing what intermediate computation is buying.
- Useful corrective to loose claims about recurrent efficiency implying compositional competence.

### 9. What are the weaknesses, limitations, or red flags?
- Formal tasks may only partially map to messy real model behavior.
- Theory results can be overinterpreted if people ignore constants, training dynamics, or approximate computation.
- It is more useful for framing and skepticism than for immediate design recipes.

### 10. What challenges or open problems remain?
Bridging the theory to real finite-trained SSMs on natural tasks remains open. It is also unclear which architectural modifications besides online CoT recover the missing expressive power in practice.

### 11. What future work naturally follows?
Empirical probes of online intermediate computation in SSMs, theory for more realistic noisy or approximate settings, and analyses of hybrid architectures that mix recurrence with explicit working memory.

### 12. Why does this matter for my work?
If your work touches compositional reasoning, structured planning, or world-model-like sequence computation, this paper gives a principled way to talk about why certain models may fail even when they look efficient and scalable.

### 13. What ideas are steal-worthy?
- Separate offline from online intermediate reasoning.
- Evaluate structured computation with resource-sensitive analyses, not just benchmarks.
- Treat persistent memory and intermediate-token timing as architectural variables.

### 14. Final decision
**Skim with intent.** Worth citing for framing and limitations, especially around compositional reasoning claims, but probably not a paper to spend a whole afternoon on unless this theory question is central.
