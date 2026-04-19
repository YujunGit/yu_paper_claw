# "Just in Time" World Modeling Supports Human Planning and Reasoning

## Basic info

* Title: "Just in Time" World Modeling Supports Human Planning and Reasoning
* Authors: Tony Chen, Sam Cheyette, Kelsey Allen, Joshua Tenenbaum, Kevin Smith
* Year: 2026
* Venue / source: arXiv
* Link: https://arxiv.org/abs/2601.14514
* Date surfaced: 2026-04-19
* Why selected in one sentence: It offers a concrete algorithmic account of building reduced world representations online, which is a better conceptual lens than assuming agents should simulate everything all at once.

## Quick verdict

**Highly relevant**

This is not the most directly applicable engineering paper today, but it may be the most conceptually useful one. The core claim, that useful simulation depends on constructing only the currently needed world representation and revising it online, is exactly the sort of framing that transfers well to structured planning and adaptive world models. The obvious caveat is that the paper appears to sit closer to cognitive modeling than scalable machine learning systems, so transfer to modern learned agents is interpretive rather than immediate.

## One-paragraph overview

The paper studies how humans might perform simulation-based reasoning without maintaining a complete detailed model of the environment. Its answer is a just-in-time process: simulation, visual search, and representation building are interleaved, so the current reasoning trajectory determines what parts of the world need to be encoded next. Instead of assuming the agent first constructs a full internal scene representation and then plans, the model says representation itself is an online, demand-driven process. The main contribution is therefore a procedural theory of selective world-model construction, not a new neural architecture.

## Key questions this summary must address

### 1. What problem is the paper trying to solve?
It addresses a basic tension in simulation-based reasoning: rich environments contain too much detail for exhaustive internal modeling, yet planning still needs useful predictive structure. The paper asks how a limited agent can decide what to represent and when.

### 2. What is the method?
The method is a just-in-time framework that tightly interleaves three processes: simulation, visual search, and representation modification. Simulation points to what matters next, visual search detects task-relevant objects or relations, and the representation is updated only as needed for future simulation.

### 3. What is the method motivation?
The motivation is strong. Full-scene internal simulation is usually unnecessary and likely unrealistic. Efficient reasoning should build partial state only when the active plan or prediction requires it.

### 4. What data does it use?
From the abstract, the empirical support comes from a grid-world planning task and a physical reasoning task. I cannot verify the exact datasets, subject counts, or task setups without the full paper.

### 5. How is it evaluated?
It is evaluated by comparing the model against alternative accounts across multiple behavioral measures in those tasks.

### 6. What are the main results?
The paper reports strong empirical support for the just-in-time account over alternatives. The interesting result is not raw accuracy but that limited selective encoding can still yield high-utility predictions.

### 7. What is actually novel?
The novelty is the explicit process view of world-model construction. Many systems treat representation as a fixed precursor to planning. This paper instead makes representation growth part of planning itself.

### 8. What are the strengths?
- Excellent conceptual framing.
- Treats representation cost as a first-class problem rather than hiding it.
- Gives a plausible algorithmic account of selective abstraction.
- Potentially useful for thinking about memory, perception, and planning as one loop rather than separate modules.

### 9. What are the weaknesses, limitations, or red flags?
- It is not clear how directly the framework maps onto modern large learned agents.
- Cognitive-model tasks may be too small or structured to establish engineering scalability.
- The abstract does not tell me how sensitive the account is to task design choices.
- There is a risk of over-translating a human cognitive result into ML architecture advice without enough evidence.

### 10. What challenges or open problems remain?
The big open problem is how to operationalize just-in-time representation building in large-scale learned systems. Another is determining which queries or reasoning contexts should trigger state expansion versus relying on a compressed current abstraction.

### 11. What future work naturally follows?
- Build learned agents that expand state only when planning uncertainty or ambiguity demands it.
- Study whether active perception can be directed by current imagined rollouts.
- Connect selective representation growth to memory budgeting and tool use.
- Compare demand-driven state construction against fixed latent world models in embodied tasks.

### 12. Why does this matter for my work?
It matters because it suggests a better question than “how can a model predict more future frames?” The more useful question may be “what minimal world state needs to exist right now to support the next planning computation?” That is a much stronger lens for scalable structured world models.

### 13. What ideas are steal-worthy?
- Treat representation construction as an online planning subroutine.
- Couple simulation with active search for missing state.
- Expand state only when the current reasoning trace reveals a gap.
- Evaluate world models partly by representational economy, not only predictive fidelity.

### 14. Final decision
**Worth reading for framing even if not for direct implementation.** I would use it to sharpen how you talk about selective abstraction, memory, and planning interfaces.

---

## Confidence / access note

This note is based on the arXiv abstract and metadata only. I could verify the core framing and task types, but not the full behavioral analysis, alternative models, or the exact formalism used in the paper.
