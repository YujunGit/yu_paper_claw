# Controllable Image Generation with Composed Parallel Token Prediction

## Basic info

* Title: Controllable Image Generation with Composed Parallel Token Prediction
* Authors: Jamie Stirling, Noura Al-Moubayed, Chris G. Willcocks, Hubert P. H. Shum
* Year: 2026
* Venue / source: arXiv, accepted to CVPR Workshops 2026 (LoViF)
* Link: https://arxiv.org/abs/2604.05730
* Date surfaced: 2026-04-24
* Why selected in one sentence: It gives a concrete composition rule for discrete iterative generation, with weighting and negation, instead of relying on prompt-level hope.

## Quick verdict

**Highly relevant**

This is one of the cleaner controllability papers I have seen recently because the main contribution is a composition mechanism, not just another conditioning trick. The paper derives a product-of-experts style rule for composing discrete sequential generation processes, then instantiates it in parallel token prediction over VQ latents. My main caution is that the evaluation is mostly CLEVR-style controlled composition plus FFHQ, so the conceptual contribution looks stronger than the evidence for broad real-world robustness.

## One-paragraph overview

The paper targets a familiar weakness of conditional generators: they often fail when asked to satisfy multiple conditions simultaneously, especially combinations not seen during training. Instead of treating this as a prompt engineering or guidance tuning problem, the authors derive a general rule for composing discrete conditional generation processes. They show how to combine unconditional and per-condition token distributions inside a masked parallel token prediction model, effectively extending product-of-experts composition into discrete iterative generation. This gives them explicit multi-condition control, concept weighting, and even negation, while keeping the speed benefits of parallel token sampling in VQ-VAE or VQ-GAN latent space.

## Key questions this summary must address

### 1. What problem is the paper trying to solve?
It addresses the failure of conditional discrete generators to reliably compose multiple constraints, especially when the requested combination or number of conditions lies outside the training distribution.

### 2. What is the method?
The method derives a composition rule for discrete conditional distributions based on a product-of-experts assumption. In sequential generation form, the next-state distribution under multiple conditions is proportional to the unconditional distribution multiplied by the ratio of each per-condition distribution to the unconditional one. The paper instantiates this inside conditional parallel token prediction, where a masked latent is iteratively unmasked in VQ latent space.

### 3. What is the method motivation?
The motivation is solid. Continuous diffusion and energy-based composition methods already showed that explicit composition can outperform monolithic conditioning, but similar machinery for discrete latent generators was missing. If discrete models already have speed and vocabulary advantages, it makes sense to ask for composition there too.

### 4. What data does it use?
The paper reports experiments on positional CLEVR, relational CLEVR, and FFHQ. It also shows a qualitative application to the open pretrained text-to-image model aMUSEd.

### 5. How is it evaluated?
It is evaluated mainly on compositional generation error and FID across datasets and across 1, 2, or 3 input components. The paper also reports generation speed relative to continuous compositional baselines and shows qualitative concept weighting and negation examples.

### 6. What are the main results?
The headline claim is a 63.4% relative reduction in error against the previous state of the art averaged across three datasets, with an average FID improvement of -9.58. The method is also claimed to run 2.3x to 12x faster than comparable continuous approaches.

### 7. What is actually novel?
The real novelty is not “another controllable image generator.” It is the derivation of a general composition rule for discrete sequential generative processes, then showing that masked parallel token prediction is a practical instantiation of that rule.

### 8. What are the strengths?
- The paper contributes an actual mechanism, not just a conditioning recipe.
- Weighting and negation emerge naturally from the composition framework.
- It preserves the efficiency advantages of discrete parallel token generation.
- The abstract formulation appears reusable beyond image generation, in principle across discrete iterative generative processes.

### 9. What are the weaknesses, limitations, or red flags?
- The core independence assumption behind product-of-experts composition is useful but approximate, and failure cases may be sharp when conditions are strongly entangled.
- Much of the empirical evidence comes from relatively controlled compositional settings, so transfer to messier open-world generation is not yet convincing.
- The paper has an arXiv note about substantial text overlap with a previous submission, which does not invalidate the method but does slightly lower my confidence in how much is genuinely new beyond this discrete extension.
- Workshop placement means I would treat it as promising rather than fully settled.

### 10. What challenges or open problems remain?
The big open question is how robust the composition rule stays when conditions are ambiguous, contradictory, hierarchical, or heavily correlated. Another is whether the method still works well when the discrete latent vocabulary is less semantically clean than VQ setups on curated data.

### 11. What future work naturally follows?
- Extend the composition rule to larger pretrained discrete generative backbones.
- Study conflict detection and uncertainty under incompatible conditions.
- Test whether similar composition applies to discrete world models, symbolic latent planners, or multimodal token spaces.
- Replace the conditional independence approximation with a learned correction term.

### 12. Why does this matter for my work?
It matters because it treats controllability as an algebra over generative factors, not as prompt phrasing. That is exactly the kind of mechanism that can transfer into structured generation, compositional world modeling, or modular reasoning.

### 13. What ideas are steal-worthy?
- Compose per-condition predictive distributions explicitly rather than merging all conditions into one embedding.
- Use weighting and negation as first-class operations, not bolt-ons.
- Prefer discrete latent spaces when you want controllable symbolic-ish composition with fast iterative generation.
- Treat composition as an interface design problem, not only a training-data coverage problem.

### 14. Final decision
**Read soon.** I would not overclaim its empirical scope, but the mechanism is genuinely useful and more reusable than most controllability papers.

---

## Confidence / access note

This note is based on the arXiv abstract and accessible HTML sections, not a full PDF audit. I verified the composition derivation, evaluation setup at a high level, and headline claims, but I did not fully inspect all proofs, appendices, or failure analyses.
