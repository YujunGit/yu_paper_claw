# Occupancy Reward Shaping: Improving Credit Assignment for Offline Goal-Conditioned Reinforcement Learning

## Basic info

* Title: Occupancy Reward Shaping: Improving Credit Assignment for Offline Goal-Conditioned Reinforcement Learning
* Authors: Aravind Venugopal, Jiayu Chen, Xudong Wu, Chongyi Zheng, Benjamin Eysenbach, Jeff Schneider
* Year: 2026
* Venue / source: arXiv, ICLR 2026
* Link: https://arxiv.org/abs/2604.20627
* Date surfaced: 2026-04-23
* Why selected in one sentence: It gives a concrete mechanism for extracting long-horizon goal geometry from a world model and turning it into a policy-invariant shaping signal.

## Quick verdict

**Must read**

This is the strongest paper in today’s batch because it uses world models for something sharper than generic latent planning or rollout. The core idea is to learn an occupancy measure over future states, recover geometry from it using optimal transport and flow matching, and convert that into reward shaping that preserves the optimal policy. That is conceptually reusable well beyond the specific offline goal-conditioned RL setting. The main caution is that I only inspected the abstract, metadata, and accessible HTML sections rather than the full paper line by line.

## One-paragraph overview

The paper targets sparse-reward offline goal-conditioned RL, where long delays between action and consequence make credit assignment hard. Instead of learning local temporal distances or graph search heuristics over replay data, the authors learn a generative model of the occupancy measure, meaning the distribution of future states reachable from a state-action pair. They argue that this occupancy model implicitly contains the geometry of long-horizon goal reachability, then use optimal transport and the velocity field of a flow-matched model to extract a scalar shaping reward. The result is a denser learning signal that is claimed to preserve the original optimal policy while materially improving performance on long-horizon locomotion, manipulation, and Tokamak control tasks.

## Key questions this summary must address

### 1. What problem is the paper trying to solve?
It addresses the central credit-assignment problem in offline goal-conditioned RL under sparse rewards. When rewards only appear at goal completion, learning from static data becomes brittle because it is hard to tell which earlier states and actions were meaningfully moving toward the goal.

### 2. What is the method?
The method learns an occupancy model over future states, apparently with flow matching, then extracts a goal-reaching reward from the geometry encoded in that model. The shaping reward is derived using optimal transport ideas and is designed to be policy-invariant in the potential-based sense, so the shaped problem should preserve the original optimum.

### 3. What is the method motivation?
The motivation is good. Many prior methods estimate only local temporal distance and then compose that local signal through graphs or heuristics, which can accumulate error. If the world model already captures the long-horizon occupancy distribution, then using that richer object directly for reward shaping is cleaner than pretending local distances are enough.

### 4. What data does it use?
From the accessible sections, evaluation includes 13 long-horizon locomotion and manipulation tasks from OGBench, plus 3 real-world Tokamak control tasks. I did not verify the full training-data construction, task splits, or environment-specific preprocessing from the full PDF.

### 5. How is it evaluated?
It is evaluated mainly by goal-reaching success or relative success rate against prior offline GCRL baselines. The paper also emphasizes comparison to sparse-reward base algorithms and prior state-of-the-art shaping or graph-based methods.

### 6. What are the main results?
The headline claim is a 2.2x improvement over the sparse-reward base algorithm, plus 24% to 248% improvements over prior methods across 13 OGBench tasks. The paper also claims successful gains on 3 Tokamak control tasks, which matters because it suggests the method is not tied only to toy navigation-style benchmarks.

### 7. What is actually novel?
The novel part is not just reward shaping, nor just occupancy modeling. The more interesting contribution is the argument that world-model occupancy structure encodes a recoverable geometry of long-horizon reachability, and that this geometry can be converted into a shaping reward without changing the optimal policy.

### 8. What are the strengths?
- Strong conceptual bridge between generative world models and reward design.
- Uses structure for a concrete downstream purpose rather than vague representation quality claims.
- The policy-invariance claim matters because many shaping methods quietly change the objective.
- The method looks transferable to other settings where long-horizon reachability matters more than one-step prediction accuracy.
- Real-world Tokamak evaluation is a serious plus if the setup is credible.

### 9. What are the weaknesses, limitations, or red flags?
- The method may depend heavily on occupancy-model quality, which could become difficult in highly multimodal or partially observed domains.
- The strongest theoretical story may rely on assumptions that become weaker in practical finite-data settings.
- Flow-matching occupancy learning plus optimal-transport extraction could be expensive or brittle relative to simpler baselines.
- I have not yet checked the ablations carefully enough to know whether the main gains come from the geometry extraction itself or from overall model capacity and training quality.

### 10. What challenges or open problems remain?
A big open question is whether this works when observations are heavily aliased, object-centric state is latent, or action consequences depend on hidden variables. Another is whether the occupancy geometry remains useful when the task distribution is broad enough that a single shaping scalar may compress away important mode structure.

### 11. What future work naturally follows?
- Extend the method to partially observed or belief-state settings.
- Use structured or object-centric occupancy models rather than flat state occupancy.
- Test whether the extracted geometry can guide planning, subgoal discovery, or exploration, not just reward shaping.
- Study whether similar extraction works for action-condition spaces or latent skill spaces.

### 12. Why does this matter for my work?
It matters because it treats a world model as a source of reusable long-horizon structure, not just a simulator or feature encoder. If you care about structured generation, planning, or reusable abstractions, this is a strong example of deriving a task-facing signal from model geometry.

### 13. What ideas are steal-worthy?
- Learn occupancy-style future distributions and derive geometry from them instead of only decoding rollouts.
- Use explicit structure to change the learning signal, not only the planner input.
- Treat optimal-transport geometry as a lens on long-horizon reachability.
- Demand policy-preserving structure when adding dense auxiliary signals.

### 14. Final decision
**Read first today.** Even if the empirical gains shrink under close inspection, the conceptual move is genuinely useful and more reusable than most world-model papers.

---

## Confidence / access note

This note is based on the abstract, arXiv metadata, and accessible HTML sections. I verified the high-level framing, method ingredients, benchmark names, and headline claims, but I did not do a full PDF-level audit of proofs, ablations, or failure cases.