# LAMP: Lift Image-Editing as General 3D Priors for Open-world Manipulation

## Basic info

* Title: LAMP: Lift Image-Editing as General 3D Priors for Open-world Manipulation
* Authors: Jingjing Wang, Zhengdong Hong, Chong Bao, Yuke Zhu, Junhan Sun, Guofeng Zhang
* Year: 2026
* Venue / source: arXiv
* Link: https://arxiv.org/abs/2604.08475
* Date surfaced: 2026-04-11
* Why selected in one sentence: It turns image-editing outputs into explicit inter-object 3D transformations for open-world manipulation, which is a much stronger interface than vague visual subgoals.

## Quick verdict

**Must read**

This is the strongest paper in today’s batch because the intermediate representation is concrete, geometrically meaningful, and actually tied to execution. The key move is not “use image editing for robotics,” which would be easy to overhype, but “use image editing to propose a target scene and then extract a 3D inter-object transform from it.” The main caveat is that the whole pipeline still inherits fragility from editing quality, monocular depth, segmentation, and registration.

## One-paragraph overview

LAMP tackles open-world manipulation by treating image editing as a source of spatial priors rather than as an end product. Given an RGB-D observation and a language instruction, it first edits the current image into a plausible post-manipulation target state. It then lifts both observed and edited states into 3D, segments the active and passive objects, and estimates an inter-object SE(3) transformation through cross-state point-cloud registration. That transformation becomes the action-relevant representation used for execution. The conceptual claim is that image editing contains richer continuous geometric intent than sparse language constraints or brittle 2D keypoint formulations.

## Key questions this summary must address

### 1. What problem is the paper trying to solve?
It targets a real weakness in open-world manipulation: language and VLM-derived 2D constraints are often too sparse, ambiguous, or viewpoint-sensitive to support fine-grained 3D interaction. The paper wants a more generalizable manipulation representation that captures continuous geometric relations between objects.

### 2. What is the method?
The method is a perception-reasoning-execution pipeline. It uses an image-editing model to generate a target post-action image from the current scene and instruction, lifts the edited and observed states into 3D with depth estimation plus RGB-D geometry, segments task-relevant objects, filters noisy points, aligns current and edited point clouds, and extracts an inter-object 3D transformation that is converted into a target pose for control.

### 3. What is the method motivation?
The motivation is good. Language-level constraints like “move left” or even explicit 2D keypoints do not capture rich contact geometry, alignment, and relative pose. Image editing often encodes these relations implicitly, and the authors try to convert that implicit visual prior into an explicit geometric one.

### 4. What data does it use?
From the paper text available through arXiv HTML, the setup uses monocular RGB-D observations at test time and evaluates on diverse real-world open-world manipulation tasks. I could verify that the paper emphasizes zero-shot generalization across varied real-world tasks, but I did not fully extract the exact dataset/task table from the full paper during this pass.

### 5. How is it evaluated?
It is evaluated on real-world open-world manipulation tasks, with comparisons against prior VLM/LLM-based manipulation methods and related image-editing/subgoal approaches. The important evaluation axis is zero-shot generalization under viewpoint variation, depth noise, and real-world object diversity.

### 6. What are the main results?
The authors report strong zero-shot generalization and argue that their lifted 3D priors outperform previous explicit 2D or language-heavy representations. I verified the qualitative and methodological claims from the paper text, but I am not quoting exact aggregate numbers here because I did not fully audit the experiment tables.

### 7. What is actually novel?
The real novelty is the interface design: image editing is not used merely to create a goal image for a downstream policy, but to derive a dense 3D inter-object transformation. The hierarchical 2D-3D filtering and unified scale correction are also important practical details because they make the registration step less brittle in real scenes.

### 8. What are the strengths?
- Strong intermediate representation with direct execution relevance.
- Clear bridge from generative prior to geometric action interface.
- Better conceptual grounding than papers that stop at visual subgoals.
- Explicit attention to failure sources like depth noise, floating edge points, and scale inconsistency.
- Likely transferable beyond the exact tasks if the registration machinery holds up.

### 9. What are the weaknesses, limitations, or red flags?
- The system depends on a long chain of components: editing, segmentation, depth, reconstruction, registration, and execution.
- If the edit is semantically plausible but geometrically sloppy, the extracted transform may be wrong in precisely the cases that matter most.
- Monocular lifting and cross-state registration remain brittle under severe occlusion, thin structures, or large appearance distortions introduced by editing.
- The method is strongest for subtask-level manipulation; long-horizon planning is still offloaded elsewhere.

### 10. What challenges or open problems remain?
The main challenge is making these lifted priors robust when generative edits become unreliable, ambiguous, or multi-step. Another open problem is whether the same interface can support branching uncertainty, contact-rich manipulation, and persistent world-state updates rather than one-shot target transforms.

### 11. What future work naturally follows?
- Replace single edited targets with multi-hypothesis target structures.
- Learn uncertainty over extracted transforms.
- Extend from single-step subgoals to longer-horizon structured plans.
- Combine with world models that maintain persistent object-centric state over time.

### 12. Why does this matter for my work?
It matters because it is an unusually clean example of turning a foundation-model prior into an explicit, controllable, reusable geometric representation. If you care about structured generation, manipulation interfaces, or explicit intermediate state, this is exactly the kind of paper worth reading carefully.

### 13. What ideas are steal-worthy?
- Use generative models as latent proposal mechanisms, not as the final representation.
- Convert edited future states into explicit inter-object transforms.
- Filter cross-state geometry hierarchically in both 2D/feature space and 3D space.
- Enforce unified scale consistency during edited-to-observed alignment.

### 14. Final decision
**Read first.** This is the best direct paper today and the one most likely to sharpen thinking about explicit intermediate structure for manipulation.

---

## Confidence / access note

This note is based on the arXiv abstract plus substantial arXiv HTML paper text, including the introduction, method framing, and parts of the method section. I have moderate confidence in the high-level method characterization and its main strengths/limitations, but I did not fully audit every experiment table or appendix detail.