# 3D-Fixer: Coarse-to-Fine In-place Completion for 3D Scenes from a Single Image

## Basic info

* Title: 3D-Fixer: Coarse-to-Fine In-place Completion for 3D Scenes from a Single Image
* Authors: Ze-Xin Yin, Liu Liu, Xinjie Wang, Wei Sui, Zhizhong Su, Jian Yang, Jin Xie
* Year: 2026
* Venue / source: arXiv / CVPR 2026
* Link: https://arxiv.org/abs/2604.04406
* Date surfaced: 2026-04-15
* Why selected in one sentence: It replaces generate-then-align scene assembly with geometry-anchored in-place completion, which is a cleaner structural interface for compositional 3D scene generation.

## Quick verdict

**Useful**

This is a good 3D scene paper, though not as central as today’s two world-model picks. Its best idea is using fragmented observed geometry as a spatial anchor and completing assets at their original locations, which avoids fragile pose optimization loops. The main caution is that a lot of the gain may come from strong priors and a large synthetic dataset, so the broader conceptual jump is real but not huge.

## One-paragraph overview

The paper targets single-view compositional 3D scene generation, where current methods either predict whole scenes feed-forward but generalize poorly, or generate per-instance assets and then spend a lot of effort aligning them back into the scene. 3D-Fixer proposes an in-place completion pipeline instead. It first obtains fragmented geometry from geometry-estimation methods, crops partial object point clouds at their observed locations, and then completes each asset there rather than regenerating and aligning from scratch. To make this work under occlusion, it uses a coarse-to-fine completion strategy, a dual-branch conditioning design that adds scene context while preserving an object-generation prior, and an occlusion-robust feature alignment loss. It also introduces a large synthetic scene dataset, ARSG-110K.

## Key questions this summary must address

### 1. What problem is the paper trying to solve?
It tries to improve single-view compositional 3D scene generation, especially the tradeoff between efficient feed-forward generation and more general but slower divide-and-conquer pipelines that require explicit pose alignment.

### 2. What is the method?
The method uses estimated scene geometry as a hard spatial anchor, crops partial instance geometry, and performs in-place coarse-to-fine completion with a dual-branch conditioned generative model plus occlusion-robust feature alignment.

### 3. What is the method motivation?
The motivation is sensible: if geometry estimation already provides visible object fragments at approximately correct locations, then the system should complete missing structure in place rather than regenerate an object elsewhere and solve a difficult alignment problem afterward.

### 4. What data does it use?
It uses ARSG-110K, a large synthetic dataset with over 110K scenes and about 3M annotated images, built from a large asset library with object-level geometry and pose annotations. The paper also claims experiments on complex, real-world, and outdoor scenes.

### 5. How is it evaluated?
It is evaluated against prior scene-generation methods such as MIDI and Gen3DSR, with emphasis on geometric accuracy, efficiency, and generalization to more complex scenes.

### 6. What are the main results?
The accessible text claims state-of-the-art geometric accuracy over baselines while preserving diffusion-level efficiency, plus stronger generalization to complex real-world and outdoor scenes.

### 7. What is actually novel?
The strongest novelty is the in-place completion paradigm itself. Using partial observed geometry as the anchor point for generation is a more grounded structural choice than doing object generation and explicit scene alignment as separate stages.

### 8. What are the strengths?
- Good structural framing of the alignment problem.
- Partial geometry is used as a real constraint, not just an auxiliary hint.
- Coarse-to-fine completion matches the occlusion ambiguity problem reasonably well.
- The released dataset could be useful infrastructure for this area.

### 9. What are the weaknesses, limitations, or red flags?
- A lot may depend on the quality of the upstream geometry estimator.
- The method is still fundamentally tied to visible-fragment anchoring, so very severe occlusion or missing instances may remain hard.
- Synthetic-data scale may explain part of the gain.
- It is not yet a richer relational or interactive scene model; it is mainly a better reconstruction-generation interface.

### 10. What challenges or open problems remain?
Open issues include dynamic scenes, stronger object relations, persistent object identity, uncertainty over unseen geometry, and extension beyond one-shot scene completion into editable or interactive world representations.

### 11. What future work naturally follows?
- Add explicit relational constraints between completed objects.
- Incorporate uncertainty over ambiguous occluded regions.
- Connect in-place completion to editable scene graphs or simulation-ready world states.
- Test whether the same anchor-based idea helps interactive scene editing.

### 12. Why does this matter for my work?
It matters as a useful example of explicit structural anchoring in 3D generation. Even if the domain is narrower, the core lesson transfers: when partial geometry is known, generation should preserve and extend that structure rather than hallucinate everything globally.

### 13. What ideas are steal-worthy?
- Use observed partial geometry as a hard spatial anchor.
- Complete assets in place instead of generate-then-register.
- Resolve heavy occlusion with coarse-to-fine generation.
- Keep the pretrained object prior mostly intact while adding scene-context conditioning.

### 14. Final decision
**Worth keeping, but not urgent.** This is a solid adjacent paper with a real mechanism, mainly useful for 3D generation framing and related work rather than as a top-priority must-read.

---

## Confidence / access note

This note is based on the arXiv abstract page and partial arXiv HTML text, not a full PDF read. I verified the main pipeline components and dataset claims from accessible text, but not the exact metrics, ablations, or robustness details.
