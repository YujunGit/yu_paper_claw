# Lifting Traces to Logic: Programmatic Skill Induction with Neuro-Symbolic Learning for Long-Horizon Agentic Tasks

## Basic info

* Title: Lifting Traces to Logic: Programmatic Skill Induction with Neuro-Symbolic Learning for Long-Horizon Agentic Tasks
* Authors: Jie-Jing Shao, Haiyan Yin, Yueming Lyu, Xingrui Yu, Lan-Zhe Guo, Ivor W. Tsang, James T. Kwok, Yu-Feng Li
* Year: 2026
* Venue / source: arXiv / ICML 2026
* Link: https://arxiv.org/abs/2605.01293
* Date surfaced: 2026-05-06
* Why selected in one sentence: It is one of the few recent “agentic + neuro-symbolic” papers where the central mechanism is at least an explicit state-dependent program rather than branding alone.

## Quick verdict

**Useful**

I would not overhype this one. The paper uses some fashionable language, and the evaluation domains are still relatively stylized. Still, it has a real core idea: skills should not just compress successful traces into parameterized scripts; they should compile conditional logic, control flow, and variable binding that can adapt when the environment changes.

## One-paragraph overview

The paper proposes **Neuro-Symbolic Skill Induction (NSI)** for long-horizon agent tasks. Instead of storing reusable behavior as linear action scripts, NSI lifts interaction traces into graph-structured workflows with explicit symbolic predicates, branching conditions, loops, and dynamic variable binding. Neural perception is used to ground raw observations into a symbolic state, and a symbolic interpreter executes the resulting skill graph. The framework also includes an online refinement loop that grafts successful recovery trajectories back into the skill graph when execution fails.

## Key questions this summary must address

### 1. What problem is the paper trying to solve?
It tries to solve the brittleness of script-like skill induction for long-horizon agents. Linear trace reuse works poorly when the environment deviates from the original trajectory and the agent needs to know when to branch, rebind variables, or recover.

### 2. What is the method?
The method induces a neuro-symbolic skill representation consisting of invocation parameters, a neural grounding module, and a symbolic execution graph. The graph contains invented data-operation nodes, control nodes, and action nodes that together encode state-dependent workflows rather than fixed scripts.

### 3. What is the method motivation?
The motivation is that successful experience should be compiled into reusable execution logic, not just replayable action order. If a skill omits the conditions under which each action is appropriate, it will fail as soon as the environment differs in topology or object arrangement.

### 4. What data does it use?
From the accessible text, the main experiments are on **ALFWorld**, **WebShop**, and **TextCraft**. TextCraft includes recursive crafting tasks; the accessible text mentions **200 recursive tasks**. ALFWorld evaluation includes **134 test instances across six task types**.

### 5. How is it evaluated?
The paper evaluates long-horizon task success against programmatic-agent baselines, using success rate and domain-specific metrics such as WebShop score. It also analyzes skill structure and skill efficiency, including average atomic steps executed per skill invocation.

### 6. What are the main results?
The paper claims consistent gains over baseline programmatic agents across ALFWorld, WebShop, and TextCraft, plus better skill efficiency. The most interesting reported pattern is not just higher success but stronger reuse from more structured skill graphs. I did not fully verify the full result tables.

### 7. What is actually novel?
The novelty is not “agents learn skills.” The stronger contribution is defining a skill as a **logic-grounded workflow** with explicit symbolic execution semantics, variable binding, and branch structure, then updating that workflow through online repair.

### 8. What are the strengths?
- It earns the neuro-symbolic label better than many recent papers.
- The distinction between trace scripts and state-dependent logic is important.
- Skill repair through grafting recovery trajectories back into the graph is a useful idea.
- The representation is at least somewhat interpretable and executable.

### 9. What are the weaknesses, limitations, or red flags?
- The paper still lives in text-heavy and relatively structured domains.
- Symbol grounding quality may become the real bottleneck in noisier embodied settings.
- There is some risk that the graph formalism helps mainly because the tasks already reward symbolic decomposition.
- The “agentic” framing is louder than the strongest actual contribution.

### 10. What challenges or open problems remain?
A core open problem is whether this representation survives in richer partially observed worlds with ambiguous perception, continuous control, and messy object identity. Another is how much of the graph invention can remain stable under scaling.

### 11. What future work naturally follows?
- Apply the same logic-grounded skill induction to embodied or tool-rich settings with stronger perception noise.
- Learn better predicate grounding rather than assuming relatively clean symbolic state updates.
- Combine symbolic skill graphs with learned world models for look-ahead evaluation.
- Study when graph complexity helps versus overfits.

### 12. Why does this matter for my work?
It matters because it draws a sharp line between decorative modularity and executable modularity. If a reusable skill or abstraction cannot encode the conditions under which it should fire, it is not much of an abstraction.

### 13. What ideas are steal-worthy?
- Compile reusable skills as conditional workflows, not only scripts.
- Separate perception-to-symbol grounding from symbolic execution logic.
- Treat failures as opportunities to graft recovery structure back into the skill graph.
- Ask whether a claimed abstraction actually encodes **when** and **why**, not just **what next**.

### 14. Final decision
**Read selectively.** Worth reading for the representation and framing, but I would stay skeptical about how far the results transfer beyond the current domains.

---

## Confidence / access note

This note is based on the arXiv abstract and substantial arXiv HTML text, including the introduction, representation section, and benchmark descriptions. I did not do a full PDF-level audit of every table, ablation, or implementation detail.