# Zero-to-CAD: Agentic Synthesis of Interpretable CAD Programs at Million-Scale Without Real Data

## Basic info

* Title: Zero-to-CAD: Agentic Synthesis of Interpretable CAD Programs at Million-Scale Without Real Data
* Authors: Mohammadmehdi Ataei, Farzaneh Askari, Kamal Rahimi Malekshan, Pradeep Kumar Jayaraman
* Year: 2026
* Venue / source: arXiv
* Link: https://arxiv.org/abs/2604.24479
* Date surfaced: 2026-04-28
* Why selected in one sentence: It treats editable CAD programs as the primary generated object and uses tool-grounded search to synthesize large-scale executable data instead of relying on scarce real construction histories.

## Quick verdict

**Must read**

This is one of the better recent examples of explicit structure earning its keep. The paper’s core value is not the word “agentic”; it is the combination of executable search, environment feedback, documentation lookup, and program validation to generate interpretable CAD procedures at scale. If the claims hold beyond the abstract, this is a meaningful dataset-and-interface paper for structured generation.

## One-paragraph overview

The paper starts from a real bottleneck in CAD learning: most large 3D datasets contain final geometry, not the construction history that makes models editable and intent-preserving. Zero-to-CAD addresses that gap by placing an LLM inside a CAD execution environment and turning synthesis into an iterative search loop. The model proposes CAD code, executes it, checks validity, consults tools and documentation, and revises until it produces executable construction sequences. That loop is then used to synthesize about one million readable CAD programs and a curated 100k subset, which in turn bootstraps a vision-language model that predicts editable programs from images.

## Key questions this summary must address

### 1. What problem is the paper trying to solve?
It tries to solve the lack of large-scale training data for editable, interpretable CAD generation. Existing 3D corpora usually preserve only final meshes or B-Reps, which are useful geometrically but throw away procedural intent.

### 2. What is the method?
The method frames CAD synthesis as tool-augmented agentic search. An LLM generates CAD construction code, executes it in a feedback-rich CAD environment, validates the result, uses documentation/tool lookup when needed, and iterates toward geometrically valid, operation-diverse programs. The resulting synthetic corpus is then used to train a model for image-to-editable-CAD reconstruction.

### 3. What is the method motivation?
The motivation is strong: if the target artifact is meant to be editable and interpretable, the training target should be executable procedural structure, not only endpoint geometry. The paper also recognizes that such data is scarce in the wild, so synthesis itself becomes the data-generation mechanism.

### 4. What data does it use?
According to the abstract, the main contribution is synthetic data: roughly one million executable CAD sequences plus a curated 100k subset chosen for geometric diversity. It also uses multi-view images for the downstream reconstruction demonstration.

### 5. How is it evaluated?
From the abstract, evaluation has two layers: (1) quality and diversity of the synthesized CAD programs, and (2) downstream reconstruction of editable CAD programs from images, compared against strong baselines including GPT-5.2. I do not yet have the full metric table from the paper body.

### 6. What are the main results?
The paper claims the synthetic data is good enough to fine-tune a vision-language model that outperforms strong baselines, including GPT-5.2, on editable CAD program reconstruction from multi-view images. The abstract also claims the synthetic corpus covers a broader operation vocabulary than sketch-extrude-heavy workflows.

### 7. What is actually novel?
The novelty is the combined recipe:
- treating CAD synthesis itself as a feedback-driven search problem,
- using tool execution and validation to keep the generated structure grounded,
- generating training data at scale without real construction-history corpora,
- using that synthetic corpus to bootstrap editable program prediction.
The strongest novelty is not a single architecture block; it is the executable data-generation loop.

### 8. What are the strengths?
- The decomposition is real: code generation is tied to execution and validation.
- The target representation is editable and interpretable by construction.
- It addresses a real data bottleneck instead of pretending it does not exist.
- The synthetic-data angle is potentially very transferable to other structured-generation domains.

### 9. What are the weaknesses, limitations, or red flags?
- “Agentic” can easily hide expensive trial-and-error; the cost profile matters.
- Synthetic data quality may be high enough for execution yet still encode narrow design priors.
- Beating GPT-5.2 on this task is interesting but not automatically a decisive scientific result unless evaluation is carefully normalized.
- The paper may still be more about scalable corpus generation than about a fundamentally new reconstruction model.

### 10. What challenges or open problems remain?
The big open question is whether synthetic executable programs capture realistic human design intent rather than only valid procedural traces. Another is whether the method scales to more ambiguous, underconstrained, or highly semantic design requests.

### 11. What future work naturally follows?
- quality-aware filtering of synthetic procedural corpora,
- uncertainty estimates for execution-valid but semantically dubious programs,
- transfer from CAD to other programmatic 3D or robotics domains,
- interactive editing and repair loops rather than one-shot reconstruction.

### 12. Why does this matter for my work?
It matters because it is a concrete example of making intermediate structure executable and learnable at scale. The transferable lesson is that when real structured supervision is scarce, one promising route is to synthesize it through validated interaction with the underlying environment rather than abandoning structured targets.

### 13. What ideas are steal-worthy?
- Use environment feedback to generate structured training targets.
- Treat editable procedures as first-class outputs rather than auxiliary explanations.
- Build synthetic corpora around execution validity, operation diversity, and interpretability.
- Separate “plausible-looking structure” from “actually executable structure.”

### 14. Final decision
**Read.** Even if some of the “agentic” framing is fashionable, the underlying mechanism and dataset strategy are strong enough to matter.

---

## Confidence / access note

This note is based on the arXiv abstract and metadata page only, not a full paper read. The high-level method appears clear, but detailed metrics, ablations, and failure cases still need verification from the full paper.
