# Explicit Intermediate Structure

## Scope
Notes on papers where the intermediate representation is not merely descriptive but actively constrains prediction, planning, generation, or rollout behavior.

## What this topic is really about
A lot of recent papers use words like compositional, modular, symbolic, agentic, or world-model-based. The useful distinction is whether the intermediate structure changes failure modes in a testable way.

The stronger papers usually satisfy at least one of these:
- the structure constrains the output distribution or feasible action set,
- the structure is grounded by execution or dynamics rather than text alone,
- the interfaces support recombination across tasks or mechanisms,
- the paper exposes where errors come from rather than only reporting final score gains.

## Current anchor papers

### NeSyS (2026)
- Positioning: neuro-symbolic world modeling with executable symbolic constraints.
- What it gets right: symbolic rules appear to directly shape neural prediction and training focuses on disagreement regions.
- What it does not solve: unclear scaling path when symbolic structure is incomplete or hard to specify.

### SCALAR (2026)
- Positioning: symbolic skill planning refined by RL-grounded feedback.
- What it gets right: treats LLM-generated skills as revisable abstractions instead of trusted outputs.
- What it does not solve: unclear transfer to physically realistic robotics.

### CoR-Painter (2026)
- Positioning: explicit constraint reasoning before autoregressive image generation.
- What it gets right: forces structural commitments before image synthesis.
- What it does not solve: may still be too text-centric unless constraints are grounded in richer representations.

### LegONet (2026)
- Positioning: compositional neural operator blocks for PDE learning.
- What it gets right: modularity is enforced through reusable, structure-preserving interfaces.
- What it does not solve: real transfer beyond curated PDE recombination remains to be tested.

### VisualPredicator (2025)
- Positioning: learned neuro-symbolic predicates as an abstract planning interface.
- What it gets right: tries to learn the abstraction layer itself and judges it by sample efficiency, OOD planning, and interpretability.
- What it does not solve: robustness under noisy real-world perception remains unclear.

### RISE (2026)
- Positioning: robot policy improvement via a compositional world model split into dynamics prediction and progress evaluation.
- What it gets right: decomposition corresponds to distinct control functions rather than decorative modularity.
- What it does not solve: “compositional” here may be more functional than formally compositional, and baseline fairness needs scrutiny.

### Object-Centric Representations Better At Compositional Generalization? (2026)
- Positioning: evaluation paper testing when decomposed visual representations actually help.
- What it gets right: makes a conditional claim that structure helps most under limited data, diversity, or compute.
- What it does not solve: transfer from controlled visual worlds to embodied planning or generation.

### PlayWorld (2026)
- Positioning: robot world modeling via autonomous play data rather than success-biased demonstrations.
- What it gets right: treats data coverage as part of the mechanism, especially for contact-rich dynamics and failure-heavy rollouts.
- What it does not solve: coverage is broader, but still shaped by the proposer/executor behavior prior and hardware collection constraints.

### H-WM (2026)
- Positioning: hierarchical world model that combines symbolic task-level transition prediction with latent visual subgoal grounding.
- What it gets right: the intermediate structure has a concrete job—keeping long-horizon plans coherent while still grounding them for control.
- What it does not solve: much of the symbolic interface is still curated and annotated rather than learned.

### Hierarchical Planning with Latent World Models / HWM (2026)
- Positioning: plug-in hierarchical MPC over pretrained latent world models, with high-level latent subgoals passed directly to low-level planning.
- What it gets right: adds temporal structure at inference time instead of requiring hierarchical policies or skill libraries, and shows a real payoff on non-greedy long-horizon control.
- What it does not solve: the subgoal interface is still a soft latent, so interpretability and explicit compositional semantics remain limited.

### Compositional Planning with Jumpy World Models (2026)
- Positioning: planning over temporally extended pretrained policies using multi-timescale occupancy-style predictive models.
- What it gets right: matches the world-model granularity to the planner’s temporal abstraction, instead of asking primitive-step dynamics to support policy-level composition for free.
- What it does not solve: compositionality remains bounded by the quality and coverage of the pretrained policy library.

### C3 (2025/2026)
- Positioning: uncertainty-calibrated controllable video world models.
- What it gets right: asks whether the world model knows when its own rollout is untrustworthy, which is a missing piece in many planning papers.
- What it does not solve: uncertainty estimates are only useful if they change downstream decision-making, not just visualization.

### World Action Verifier / WAV (2026)
- Positioning: self-improving world-model framework that verifies predictions through a decomposition into plausible future states and action-consistent reachability.
- What it gets right: treats verification as an easier structured problem than dense forward prediction, and exploits the asymmetry between abundant action-free video and scarce action-labeled data.
- What it does not solve: the verifier still depends on learned subgoal and inverse modules whose own brittleness may surface in harder open-world settings.

### World-Value-Action Model / WAV (2026)
- Positioning: VLA decision-making framework that moves planning from direct action prediction into latent future inference scored by a value model.
- What it gets right: makes the internal planning interface explicit and ties feasibility plus long-horizon utility to the search space itself rather than bolting them on afterward.
- What it does not solve: the latent future interface may still be opaque, and it is not yet clear how much of the gain comes from real planning versus better learned action regularization.

### NSGGM (2026)
- Positioning: neural proposal plus symbolic assembly for graph generation with hard guarantees.
- What it gets right: uses symbolic machinery where exact validity and user constraints actually matter.
- What it does not solve: solver-backed exactness may become expensive or brittle as structured outputs grow more complex.

### Interactive World Simulator (2026)
- Positioning: action-conditioned latent video world model used as a practical surrogate environment for robot training and evaluation.
- What it gets right: asks whether a world model is fast, stable, and faithful enough to support data generation and policy ranking, not just visual prediction.
- What it does not solve: physical consistency is still mediated through latent video prediction rather than explicit object/contact state.

### SimRecon (2026)
- Positioning: compositional 3D reconstruction aimed at simulation-ready assembly from real videos.
- What it gets right: treats perception-to-generation and generation-to-simulation interfaces as real bottlenecks and gives structure an executable role in scene assembly.
- What it does not solve: pipeline errors can still compound, and simulator plausibility is not equivalent to full real-world physical fidelity.

### MM-CondChain (2026)
- Positioning: benchmark for visually grounded deep compositional reasoning built around a verifiable programmatic intermediate representation.
- What it gets right: uses intermediate structure for mechanical verification and tests deep chained conditions rather than shallow composition.
- What it does not solve: it is evaluation infrastructure, not a mechanism for improving model reasoning or grounding.

### Behavior Consistency in Text-Based World Models (2026)
- Positioning: behavior-aligned world-model training where fidelity is judged by preserving downstream action preferences, not just next-state matching.
- What it gets right: asks what a world model should be faithful to for planning and evaluation, and replaces surface-form accuracy with a more use-oriented criterion.
- What it does not solve: the metric inherits the blind spots of the frozen reference agent and is only demonstrated in relatively clean text environments.

### CoWVLA / Chain of World (2026)
- Positioning: VLA pretraining built around structure–motion disentanglement and a continuous latent motion chain instead of dense future-frame reconstruction.
- What it gets right: treats motion as the thing worth modeling, and uses the intermediate structure to reduce redundancy while preserving temporal reasoning for control.
- What it does not solve: the latent interface is still soft and only indirectly interpretable, so claims about world understanding should stay modest.

### FutureCAD (2026)
- Positioning: LLM-generated CAD programs with a separate text-to-B-Rep grounding module for resolving primitive references during execution.
- What it gets right: the intermediate structure is executable, state-dependent, and necessary; high-level intent and low-level entity binding are cleanly separated.
- What it does not solve: the mechanism is strong but domain-specific, and transfer beyond CAD will require additional grounding machinery.

### Reasoning Core (2026)
- Positioning: procedural symbolic-data infrastructure with solver-backed verification and broad formal-task distributions.
- What it gets right: argues that explicit structure in training data should be distributionally broad, difficulty-controlled, and reusable for both supervised learning and verifiable reward.
- What it does not solve: it is still mostly a training/evaluation substrate, not direct evidence that symbolic pretraining transfers cleanly into messy embodied or multimodal reasoning.

### Seoul World Model / SWM (2026)
- Positioning: retrieval-grounded video world simulation tied to a real city rather than a fully imagined environment.
- What it gets right: makes grounding operational through concrete mechanisms for temporal mismatch, sparse-view coverage, and rollout re-anchoring.
- What it does not solve: still primarily video-centric and only partially addresses explicit dynamic state, object persistence, or intervention-level causality.

### CompACT / Planning in 8 Tokens (2026)
- Positioning: ultra-compact discrete tokenization for action-conditioned world-model planning.
- What it gets right: treats planning state as something that should preserve semantics and spatial relations, not photorealistic baggage, and evaluates the payoff in actual planning latency.
- What it does not solve: extreme compression may fail in harder partially observed or contact-rich settings where rare details matter.

### WoG / World Guidance (2026)
- Positioning: world modeling in action-condition space for VLA action generation.
- What it gets right: defines the predictive target by what the controller actually needs, offering a better compromise than explicit future-image prediction or coarse latent-action codes.
- What it does not solve: the learned condition space remains implicit, difficult to interpret, and not obviously sufficient for longer-horizon planning beyond action generation.

### PERSIST / Beyond Pixel Histories (2026)
- Positioning: interactive world model with a persistent latent 3D world-frame plus explicit camera-query interface.
- What it gets right: replaces pixel-history memory with state-like geometric memory, making revisitation, off-screen persistence, and geometry-aware editing part of the representation rather than an emergent hope.
- What it does not solve: currently depends on privileged simulator-side 3D state/camera supervision and does not yet show the harder real-world learning problem.

### WorldStereo (2026)
- Positioning: camera-guided VDM augmented with global geometric memory and stereo-style retrieved correspondence memory for reconstructible generation.
- What it gets right: splits memory by function—coarse structure versus fine detail—and ties consistency to downstream 3D reconstruction rather than only perceptual video scores.
- What it does not solve: this is better understood as geometry-aware controllable generation than as a full interactive world model with persistent latent state or action-grounded dynamics.

### CityGenAgent (2026)
- Positioning: hierarchical procedural 3D city generation via executable block and building programs.
- What it gets right: the intermediate structure is real, editable, and aligned with different abstraction levels of the task rather than being prompt-only pseudo-planning.
- What it does not solve: much of the reward/evaluation stack depends on LLM judging and handcrafted priors, so claims about robust spatial reasoning should be treated cautiously.

### VGGT-World (2026)
- Positioning: world modeling as autoregressive prediction in frozen geometry-foundation feature space rather than video latent space.
- What it gets right: makes geometry the predictive state itself, which is a cleaner and more transferable representational commitment than bolting geometry losses onto RGB generation.
- What it does not solve: still closer to observational geometry forecasting than to an action-conditioned world model for intervention and control.

### Edit-As-Act (2026)
- Positioning: 3D scene editing as goal-regressive planning over executable symbolic predicates and edit actions.
- What it gets right: the intermediate structure directly governs what edits are allowed, what remains unchanged, and how physical plausibility is checked.
- What it does not solve: domain scope is still narrow, with a hand-designed symbolic language and relatively small benchmark.

### MosaicMem (2026)
- Positioning: patch-level hybrid spatial memory for controllable video rollouts under revisits and camera motion.
- What it gets right: chooses an intermediate memory unit that is selective, editable, and geometrically localizable without forcing everything into a brittle explicit 3D cache.
- What it does not solve: remains a memory/interface advance inside a video-generation stack, not a strong explicit-state model of action-grounded dynamics.

### EgoSim (2026)
- Positioning: egocentric world simulation built around an updateable 3D scene state rather than static scene assumptions or pure video continuation.
- What it gets right: persistence is implemented at the representation level, so multi-stage interaction has an explicit place to live besides frame history.
- What it does not solve: it is still unclear how physically faithful and reusable the learned state really is beyond visually consistent interaction generation.

### ActionParty (2026)
- Positioning: multi-subject video world model with persistent per-subject latent state for explicit action binding.
- What it gets right: treats action-to-entity assignment as a first-class architectural problem instead of assuming prompts or shared controls will implicitly preserve identity.
- What it does not solve: the subject state is still a soft latent in 2D game worlds, so the path to explicit object-level 3D state and embodied interaction remains open.

### LPWM (2026)
- Positioning: self-supervised object-centric world model where latent particles, masks, boxes, and keypoints form the predictive state.
- What it gets right: decomposition is not just interpretable packaging; it is the thing the dynamics model actually rolls forward and conditions on.
- What it does not solve: it is still unclear how stable the discovered objects remain under severe occlusion, contact-rich interactions, and open-world clutter.

### Points-to-3D (2026)
- Positioning: latent 3D generation anchored by observed point-cloud structure instead of pure-noise structural initialization.
- What it gets right: makes prior geometry a hard part of the latent interface, so controllability comes from preserving known structure and only sampling missing regions.
- What it does not solve: this is powerful constrained completion, but not yet a broader account of compositional 3D reasoning or uncertainty-aware structure generation.

### PhysGen (2026)
- Positioning: physics-guided 3D generation through joint shape-and-physics latents plus alternating latent refinement.
- What it gets right: uses physics to perturb the generative trajectory itself rather than scoring samples after generation is complete.
- What it does not solve: the mechanism is promising but currently demonstrated in favorable engineering-design settings with relatively explicit physical objectives.

### LeWorldModel (2026)
- Positioning: compact JEPA-style latent world model trained end-to-end from pixels with a simple anti-collapse regularizer.
- What it gets right: treats predictive-state learning and planning efficiency as first-class design goals instead of defaulting to huge frozen visual backbones or pixel-generation objectives.
- What it does not solve: a stable Gaussianized latent is not automatically a structured or compositional state, and real scaling beyond moderate offline control tasks remains to be shown.

### Geometric Priors via VSA (2026)
- Positioning: world modeling with explicit algebraic latent transitions implemented through vector-symbolic binding.
- What it gets right: the transition rule is structured, composable, and interpretable in a literal sense rather than metaphorical “modularity.”
- What it does not solve: evidence is still confined to a toy discrete environment, so the scaling story to realistic perception and stochastic dynamics is unresolved.

### PRISM-WM (2025)
- Positioning: planning-oriented world model that decomposes hybrid dynamics into mode-specialized transition experts.
- What it gets right: puts structure exactly where monolithic latent dynamics fail most, at contact- or event-driven regime changes that punish long-horizon planning.
- What it does not solve: expert specialization may remain implicit and hard to interpret, and the scaling path to perception-heavy robotics is still open.

### VEGA-3D / Generation Models Know Space (2026)
- Positioning: 3D understanding by borrowing intermediate geometric priors from large pretrained video generators.
- What it gets right: asks where useful geometric information actually lives inside generative backbones and supports that with a multi-view consistency analysis.
- What it does not solve: despite the “latent world simulator” framing, the method is still better understood as feature fusion for downstream understanding than as a structured world model with explicit state or controllable dynamics.

### Temporal Straightening (2026)
- Positioning: latent planning via curvature-regularized representation learning.
- What it gets right: makes a concrete claim that representation quality should be judged by optimization geometry, not just semantic richness or prediction accuracy.
- What it does not solve: improved local latent geometry is not the same thing as explicit state abstraction, uncertainty handling, or robust long-horizon world modeling.

### DWMR / Discrete World Models via Regularization (2026)
- Positioning: unsupervised Boolean world-model learning through structural regularization instead of decoder-centric training.
- What it gets right: treats discreteness, bit independence, and sparse action-local transitions as properties to optimize directly rather than probe after training.
- What it does not solve: current evidence appears strongest on small combinatorial environments, so the path to realistic perceptual world models is still unclear.

### RelaxFlow (2026)
- Positioning: amodal 3D generation with asymmetric control over observed versus unobserved structure.
- What it gets right: recognizes that controllability should be stronger where evidence is known and softer where the model must complete ambiguous geometry.
- What it does not solve: this is better viewed as a carefully designed conditioning interface for constrained completion than as a broad structured 3D world model.

## Working heuristics for future scouting
Prefer papers that do at least two of the following:
- make the intermediate structure executable or constraining,
- verify high-level structure against low-level dynamics or outcomes,
- localize errors by module or interface,
- show recombination under changed tasks, mechanisms, or boundaries,
- improve data efficiency or robustness because of the structure, not just alongside it.

Be skeptical of papers that claim:
- “compositional” but only rewrite prompts,
- “symbolic” but only use labels as auxiliary outputs,
- “world model” without planning utility or counterfactual leverage,
- “modular” when all communication is hidden inside soft uninterpretable latents.

## Why this topic matters
This is a useful lens for evaluating whether structure is real. It also connects several of the user’s interests: controllable generation, world models, neurosymbolic reasoning, embodied planning, and reusable representations.
