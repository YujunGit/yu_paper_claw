# BRICKS: Compositional Neural Markov Kernels for Zero-Shot Radiation-Matter Simulation

## Basic info

* Title: BRICKS: Compositional Neural Markov Kernels for Zero-Shot Radiation-Matter Simulation
* Authors: Richard Hildebrandt, Evangelos Kourlitis, Baran Hashemi, Manuel Bünstorf, Thierry Meyer, Nikola Boskov, Michael Kagan, Dan Rosenbaum, Sanmay Ganguly, Lukas Heinrich
* Year: 2026
* Venue / source: arXiv
* Link: https://arxiv.org/abs/2605.06591
* Date surfaced: 2026-05-09
* Why selected in one sentence: It learns a reusable local transition kernel rather than a monolithic end-to-end simulator, which is exactly the kind of compositional abstraction that often matters more than raw fidelity.

## Quick verdict

**Highly relevant**

This is one of the more conceptually serious “compositional generative model” papers I saw today. The main idea is to distill a local stochastic interaction rule with tractable likelihoods, then compose it autoregressively on unseen material layouts. The domain is specialized, so it is not a direct methods baseline for your work, but the abstraction level is strong and unusually transferable.

## One-paragraph overview

BRICKS targets radiation-matter simulation, where classical Monte Carlo simulators repeatedly sample local stochastic particle-material interactions. Instead of learning an end-to-end surrogate for one fixed global geometry, the paper learns a *next-particle Markov kernel* that maps one incident particle plus local material properties to a variable-sized typed set of outgoing particles and a material side effect. The kernel is implemented with a hybrid discrete/continuous generative model: an autoregressive transformer predicts per-type output cardinalities, and a continuous conditional flow-matching model predicts continuous particle features and deposited energy. Because the learned object is local and Markovian, the authors can compose it zero-shot over larger unseen material configurations.

## Key questions this summary must address

### 1. What problem is the paper trying to solve?
Most neural surrogates for radiation transport learn whole-system responses for fixed geometries, which makes them fast but not truly reusable or compositional. The paper tries to recover the compositional advantage of mechanistic simulators while keeping neural benefits like speed, differentiability, and likelihood access.

### 2. What is the method?
The method learns a conditional local interaction kernel \(q_\phi(y|\theta)\) where the condition includes the incoming particle and local material descriptor, and the output is a variable-size set of outgoing particles plus a scalar side effect. It factorizes generation into (i) a cardinality model over per-type particle counts using a causal transformer and (ii) a continuous feature model using Riemannian flow matching on mixed manifolds. At inference time, the kernel is rolled out autoregressively to simulate larger compositions.

### 3. What is the method motivation?
The motivation is strong: if the underlying physics is local and Markovian, then learning the local transition rule is a cleaner abstraction than learning one large detector- or geometry-specific response map. This also preserves a path to zero-shot reuse on unseen compositions.

### 4. What data does it use?
The paper introduces **CaloBricks**, a new 20M-event dataset of particle-material interactions. In the current demonstrator, the setting is simplified to homogeneous cubic environments with varying density and electromagnetic cascades involving photons, electrons, and positrons.

### 5. How is it evaluated?
Evaluation happens at two levels: (i) **single-kernel quality** using two-sample statistics such as MMD, energy distance, and a learned classifier AUC against Geant4 outputs, and (ii) **composition stability** under multi-round autoregressive rollouts. The paper also reports runtime/quality tradeoffs for different model sizes, ODE solvers, and integration-step counts.

### 6. What are the main results?
At kernel level, the learned model is substantially closer to the simulator than naive or physics-inspired base distributions, with classifier AUCs not too far from chance in some priors, which suggests nontrivial distribution matching. More importantly, the authors report stable multi-round autoregressive behavior and a meaningful GPU speed advantage over CPU-bound mechanistic simulation for single-kernel execution. The exact full-system realism should be treated cautiously, because the current setup is still simplified.

### 7. What is actually novel?
The key novelty is not “use generative models for physics simulation.” It is learning a **composable local particle-material Markov kernel** with explicit mixed discrete/continuous set outputs, tractable likelihoods, and zero-shot reuse across unseen material compositions. That abstraction level is more interesting than the application branding.

### 8. What are the strengths?
- Very good abstraction choice: local reusable kernel instead of fixed end-to-end simulator surrogate.
- Explicitly compositional and zero-shot by construction, not only by evaluation story.
- Mixed discrete/continuous modeling is a natural fit for the problem.
- Differentiability and likelihood access make it more useful than a pure black-box sampler.
- The paper seems aware that kernel quality and rollout stability are different questions.

### 9. What are the weaknesses, limitations, or red flags?
- The current demonstrator is still a simplified world: homogeneous cubes, limited particle types, and relatively controlled interaction families.
- “Zero-shot generalization” here is real in the compositional sense, but within a fairly bounded material-building-block family.
- Runtime comparisons are favorable, but the comparison is partly GPU neural surrogate versus CPU mechanistic simulation, so the systems angle needs careful reading.
- The quality metrics rely on summary statistics and a learned discriminator; those are useful but not a complete physical-faithfulness guarantee.

### 10. What challenges or open problems remain?
Scaling from the current kernel demonstrator to richer geometries, more particle species, more complex side effects, and fully featured 3D simulation remains open. Long-horizon error accumulation and rare-event fidelity are also likely hard.

### 11. What future work naturally follows?
- Extend the local building blocks beyond homogeneous cubes.
- Model richer side effects, such as spatial energy deposition maps.
- Stress-test rollouts on more complex composed geometries.
- Explore downstream gradient-based design or inference tasks that exploit tractable likelihoods.

### 12. Why does this matter for my work?
It matters because it is a strong example of **choosing the right compositional unit**. If you care about modular generative systems, world models, or structured simulation, this paper argues that the reusable object should often be a local transition kernel rather than a global monolith.

### 13. What ideas are steal-worthy?
- Learn local reusable kernels instead of full end-to-end generators.
- Separate discrete multiplicity structure from continuous feature generation.
- Evaluate compositional models both locally and under recursive rollout.
- Treat differentiability and likelihood access as first-class design goals, not afterthoughts.

### 14. Final decision
**Read if you want serious compositional design inspiration.** It is not the closest topical match, but it is one of the better mechanism papers in today’s pool.

---

## Confidence / access note

This note is based on the arXiv abstract and partial arXiv HTML text, including method framing and some evaluation details. I did not do a full PDF audit, so detailed fairness checks, physical edge cases, and exact runtime conditions should be verified before citing strongly.
