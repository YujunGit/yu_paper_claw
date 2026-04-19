# Do LLMs Build Spatial World Models? Evidence from Grid-World Maze Tasks

## Basic info

* Title: Do LLMs Build Spatial World Models? Evidence from Grid-World Maze Tasks
* Authors: Weijiang Li, Yilin Zhu, Rajarshi Das, Parijat Dube
* Year: 2026
* Venue / source: arXiv
* Link: https://arxiv.org/abs/2604.10690
* Date surfaced: 2026-04-19
* Why selected in one sentence: It is a useful anti-hype paper that tests whether apparent spatial reasoning really reflects stable internal world-model construction.

## Quick verdict

**Useful**

I would not treat this as a definitive verdict on world modeling in language models, but it is still worth keeping. Its value is mostly diagnostic and rhetorical: it shows that seemingly competent maze reasoning can collapse under a representation change, which is exactly what you would expect if models are exploiting format-specific shortcuts rather than maintaining a robust spatial state. The main limitation is that maze tasks are controlled but narrow, so broad claims should be made carefully.

## One-paragraph overview

The paper studies whether contemporary language models genuinely build internal spatial world models by evaluating them on maze tasks that require multi-step spatial reasoning. It compares performance across different input representations, including tokenized adjacency encodings and visual grid formats, and also probes whether models accumulate stable spatial knowledge across related questions. The central finding is that performance is highly representation-dependent and does not seem to reflect a durable cumulative internal map. So the paper is less about building a new model and more about stress-testing a common assumption.

## Key questions this summary must address

### 1. What problem is the paper trying to solve?
It asks whether strong task performance by LLMs in planning-like settings actually implies the presence of a robust internal spatial world model.

### 2. What is the method?
The method is a controlled evaluation suite built around maze solving, sequential proximity questions, and compositional distance comparisons across multiple LLMs and multiple input formats.

### 3. What is the method motivation?
The motivation is good. Many claims about LLM planning quietly assume that good outputs reflect stable internal structured state. That assumption deserves direct testing.

### 4. What data does it use?
From the abstract, it uses grid-world maze tasks in multiple representational formats rather than a naturalistic embodied dataset.

### 5. How is it evaluated?
It evaluates maze-solving accuracy and related spatial reasoning probes across Gemini-2.5-Flash, GPT-5-mini, Claude-Haiku-4.5, and DeepSeek-Chat, with chain-of-thought prompting and different task encodings.

### 6. What are the main results?
The abstract reports a large performance gap between tokenized adjacency formats and visual grid formats, plus failures to maintain cumulative spatial knowledge across related questions. The authors interpret this as evidence against robust spatial world-model construction.

### 7. What is actually novel?
The novelty is mainly evaluative. The paper contributes a targeted diagnostic lens on the difference between apparent reasoning competence and actual stable spatial abstraction.

### 8. What are the strengths?
- Good corrective pressure against vague capability claims.
- Uses representation changes as a meaningful stress test.
- Separates one-shot task success from cumulative state maintenance.
- Likely useful as a citation when arguing for explicit structured state rather than trusting implicit sequence reasoning.

### 9. What are the weaknesses, limitations, or red flags?
- Maze tasks are narrow and may underrepresent what richer multimodal systems can do.
- The paper risks overgeneralizing from a controlled spatial domain.
- Prompting and formatting details can dominate outcomes in these evaluations.
- It diagnoses failure but does not propose a remedy.

### 10. What challenges or open problems remain?
A key open problem is building evaluations that can distinguish robust latent world-model construction from brittle task-specific reasoning across more realistic environments. Another is testing multimodal and embodied systems, not only text-first LLMs.

### 11. What future work naturally follows?
- Extend the same diagnostic logic to embodied and multimodal agents.
- Test whether external memory or explicit map construction closes the gap.
- Compare implicit LLM reasoning with explicit symbolic or object-centric state trackers.
- Build harder transfer tasks where representation format changes but underlying spatial logic stays the same.

### 12. Why does this matter for my work?
It matters because it is a clean citation against hand-wavy claims that sequence models automatically learn robust spatial world representations. If your work argues for explicit abstraction, memory, or structured state, this paper helps justify why those additions may be necessary.

### 13. What ideas are steal-worthy?
- Use representation shifts as a test of whether a model learned the right latent structure.
- Probe cumulative state maintenance, not only final-answer accuracy.
- Separate apparent reasoning fluency from durable world-state construction.
- Treat evaluative skepticism as part of method design, not an afterthought.

### 14. Final decision
**Save as a citation and skepticism check, not as a method blueprint.** Useful for framing, limited for direct algorithmic inspiration.

---

## Confidence / access note

This note is based on the arXiv abstract and metadata only. I could verify the evaluation framing and headline results, but not the exact task construction, prompt settings, statistical analysis, or whether the conclusions are fully supported across all reported variants.
