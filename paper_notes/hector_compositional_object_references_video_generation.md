# HECTOR: Hybrid Editable Compositional Object References for Video Generation

## Basic info

* Title: HECTOR: Hybrid Editable Compositional Object References for Video Generation
* Authors: Angtian Wang, Jacob Zhiyuan Fang, Liming Jiang, Haotian Yang, Alan Yuille, Chongyang Ma
* Year: 2026
* Venue / source: arXiv
* Link: https://arxiv.org/abs/2603.08850
* Date surfaced: 2026-03-18
* Why selected in one sentence: It turns compositional control into an explicit object-level interface with trajectories, scale, visibility, and mixed static/dynamic references.

## Quick verdict

**Useful**

This is not the deepest paper of the day, but it is one of the cleaner controllability papers. Its main value is interface design: it exposes per-object structure explicitly enough to support composition and editing, instead of pretending that compositional generation will emerge from a better prompt. The limitation is that much of the novelty seems to come from a strong orchestration of decomposition, tracking, and conditioning rather than a fundamentally new generative backbone.

## One-paragraph overview

HECTOR is a compositional video-generation pipeline that lets users control multiple scene elements independently using either static image references or dynamic video references. A Video Decompositor segments objects, tracks anchor points, and converts them into trajectories with position, scale, and visibility information. A Spatio-Temporal Alignment Module (STAM) then projects these hybrid references into the latent space of a diffusion-transformer video generator so that each object can be placed and moved according to explicit user-defined constraints.

## Key questions this summary must address

### 1. What problem is the paper trying to solve?
Most video generation systems still treat a scene as one monolithic entity, which makes explicit object-level composition and editing awkward or unreliable.

### 2. What is the method?
The method has two main parts: a Video Decompositor that extracts object references and motion/layout parameters from videos, and a DiT-based generative model with STAM that injects mixed image/video references into the latent sequence according to explicit trajectories, scales, and visibility masks.

### 3. What is the method motivation?
If users care about object identity, motion, insertion, replacement, or background control, then holistic generation is the wrong abstraction. The paper tries to replace vague scene-level prompting with explicit element-wise control.

### 4. What data does it use?
The paper builds compositional training data from decomposed videos, using segmentation and point tracking to derive object references and trajectory annotations. I did not fully verify the exact dataset mixture during this run.

### 5. How is it evaluated?
It is evaluated on visual quality, reference preservation, motion controllability, and editing scenarios such as insertion, replacement, and background modification, compared with other reference-guided or trajectory-controlled video methods.

### 6. What are the main results?
The authors report better visual quality, stronger reference fidelity, and improved motion control than existing baselines, especially when composing multiple referenced elements or mixing static and dynamic conditioning sources.

### 7. What is actually novel?
The best claim to novelty is the explicit fusion of hybrid references with trajectory-grounded latent alignment, plus a decomposition pipeline that turns ordinary videos into reusable compositional supervision.

### 8. What are the strengths?
- Clear object-level control interface.
- Static and dynamic references are handled in one pipeline.
- Supports editing use cases, not just one-shot generation demos.
- Better than many papers in making compositionality operational.

### 9. What are the weaknesses, limitations, or red flags?
- A lot depends on upstream decomposition quality, tracking stability, and segmentation.
- The work looks more like a strong systems integration paper than a new conceptual theory of composition.
- It is not obvious how well the interface would scale to heavy occlusion, many objects, or rich physical interaction.
- “First fully compositional” is probably marketing language and should be treated cautiously.

### 10. What challenges or open problems remain?
The big open problem is moving from explicit 2D compositional control to deeper scene and interaction modeling: object permanence, 3D consistency, contact, and causal effects are still only partially handled.

### 11. What future work naturally follows?
A natural next step is to connect this kind of interface to 3D-aware or physics-aware representations, so object-level control can survive viewpoint changes and interactions rather than only image-plane trajectory constraints.

### 12. Why does this matter for my work?
It matters mainly as an interface pattern. If you care about controllable generation, modular composition, or reusable abstractions, this paper is a better reference than many prompt-level “compositional” methods because it makes the control variables explicit.

### 13. What ideas are steal-worthy?
- Represent object control as trajectory plus scale plus visibility, not just boxes.
- Separate decomposition/capture from generative recomposition.
- Treat editing as a first-class evaluation mode for compositional generators.
- Fuse static identity references and dynamic motion references instead of forcing one modality to do both jobs.

### 14. Final decision
**Skim carefully.** Worth mining for interface ideas and related work, but probably not a top-priority deep method read.

---

## Confidence / access note

This note is based on the arXiv abstract and partial HTML paper access. I verified the main pipeline components and framing, but not the full experimental setup, dataset details, or all baselines.
