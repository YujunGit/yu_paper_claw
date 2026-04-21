# ShapeGen: Robotic Data Generation for Category-Level Manipulation

## Basic info

* Title: ShapeGen: Robotic Data Generation for Category-Level Manipulation
* Authors: Yirui Wang and collaborators (full author list not fully surfaced in current access)
* Year: 2026
* Venue / source: arXiv
* Link: https://arxiv.org/abs/2604.15569
* Date surfaced: 2026-04-21
* Why selected in one sentence: It treats category-level manipulation generalization as a correspondence problem over shape and affordance, not just a data-augmentation gimmick.

## Quick verdict

**Useful**

This is a good adjacent paper because the mechanism is more serious than the title first suggests. The important idea is to build function-aware dense geometric warpings and a plug-and-play shape library so that new demonstrations preserve affordance structure when transferred to unseen shapes. I do not think it is a field-defining paper, but it has a reusable mechanism and avoids the shallowness of many “generated robot data” papers.

## One-paragraph overview

The paper focuses on improving category-level manipulation, where a robot should handle many differently shaped instances of an object category rather than memorizing a few seen shapes. Instead of relying on simulator-only shape scaling or naive asset substitution, ShapeGen builds a library of 3D shapes plus learned spatial warpings from a common template. Those warpings aim to map points to functionally corresponding points across shapes using SDF-based geometric supervision and regularization. Given a real demonstration and minimal human annotation, the system can align a new object shape, transfer relevant keypoints and interaction geometry, and generate physically plausible new demonstrations intended to improve policy generalization.

## Key questions this summary must address

### 1. What problem is the paper trying to solve?
Real manipulation policies struggle with within-category shape variation. The paper tries to generate additional training data that respects functional affordances across varied shapes, especially for fine-grained manipulation tasks where simple trajectory replay is not enough.

### 2. What is the method?
Two stages. First, shape-library curation: learn dense spatial warpings between category-level 3D shapes using SDF supervision plus pointwise and point-pair regularization, anchored by a common template. Second, function-aware generation: given a source demonstration, a scanned object, object tracking, and minimal human annotations, use the learned warpings to align new shapes and adjust interaction geometry and gripper actions automatically.

### 3. What is the method motivation?
The authors argue that fine-grained manipulation depends on the functional parts of objects, so realistic data generation must preserve affordance-relevant correspondence, not just visual similarity. Dense geometric alignment is their route to transferring functionality across shape variants.

### 4. What data does it use?
From the accessible sections, it uses real RGB-D demonstrations, scanned 3D object models, tracked object poses, and category-level shape libraries. Policies are trained on point-cloud observations rather than RGB.

### 5. How is it evaluated?
The paper reports real-world experiments aimed at category-level shape generalization in manipulation. I could confirm the real-world evaluation claim from abstract and intro, but not all task names and quantitative tables from the currently accessed sections.

### 6. What are the main results?
The authors report that ShapeGen improves real-world in-category generalization relative to baselines. I can support the directional claim, but not every exact metric from full result tables.

### 7. What is actually novel?
The novelty is the combination of dense function-aware geometric warpings, a reusable plug-and-play shape library, and a real-to-real data generation pipeline for fine-grained manipulation. The paper is more about affordance-preserving transfer than about generic synthetic data production.

### 8. What are the strengths?
- Mechanism is grounded in geometry instead of prompt-level augmentation.
- Treats functional correspondence as the core problem.
- Supports nonlinear shape variation rather than only axis-aligned scaling.
- Real-to-real pipeline is more believable than pure simulation claims.
- The library construction idea looks reusable.

### 9. What are the weaknesses, limitations, or red flags?
- Still depends on object scanning, tracking, and some human annotation.
- The correspondence mechanism is geometry-founded, which is strong, but may miss cases where function is not well captured by shape alone.
- Likely category-specific setup cost for each new library.
- Current access did not include the full experimental spread, so robustness across many categories remains uncertain.

### 10. What challenges or open problems remain?
The big open problem is scaling this from curated categories to messy open-world manipulation. Another is handling articulated, deformable, or partially observed objects where geometric correspondence is less stable.

### 11. What future work naturally follows?
- Learn library construction and correspondence jointly with downstream policy learning.
- Extend from rigid objects to articulated or deformable categories.
- Reduce human annotation further.
- Combine geometric correspondence with learned semantic or physical interaction priors.

### 12. Why does this matter for my work?
It is a nice example of structure that earns its keep. The transferable lesson is that category-level generalization may come from a good intermediate correspondence space, not only from more data or larger policy models.

### 13. What ideas are steal-worthy?
- Build a reusable library of transformations around a shared template.
- Treat function transfer as dense correspondence, not coarse label transfer.
- Use geometric supervision to bootstrap affordance-aligned intermediate structure.
- Separate augmentation infrastructure from downstream policy architecture.

### 14. Final decision
**Keep and skim carefully.** It is not as central as Lyra 2.0, but the correspondence mechanism is solid and more reusable than many robot-data-generation papers.
