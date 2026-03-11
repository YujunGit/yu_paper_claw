# yu_paper_claw

A curated research paper scouting repository.

This repo is updated daily to track, filter, and summarize research papers that are genuinely worth attention. The goal is **not** to collect paper confetti. The goal is to produce a small number of high-judgment notes that help with fast understanding, related-work positioning, method inspiration, and future research decisions.

## What happens here every day

Each day, the workflow aims to:

1. search for recent papers relevant to a method-centered research agenda,
2. filter aggressively instead of recommending everything adjacent,
3. rank the most worthwhile papers,
4. write concise daily digests,
5. produce structured, critical paper notes for selected papers,
6. update topic-level synthesis notes when useful,
7. commit and push the results to this repository.

The emphasis is on:
- methodological depth,
- transferable ideas,
- mechanism over hype,
- honest uncertainty,
- clean repository organization.

## Research interests behind the scouting

The scouting process prioritizes papers related to:
- generative models
- 3D / 4D generation
- world models
- compositional generation
- compositional reasoning
- physics-based or physics-informed models
- neurosymbolic models
- agentic systems
- neurosymbolic robotics
- representation learning

Papers are especially valued when they improve structure, controllability, interpretability, modularity, reasoning, planning, memory, tool use, reusable abstractions, or transfer.

## What this repo is **not**

This repo is **not**:
- a dump of every paper that sounds vaguely relevant,
- a hype feed,
- a benchmark-chasing list,
- a summary farm that rewrites abstracts without judgment.

Weak or shallow papers may be skipped entirely. On some days, the correct answer may be that nothing newly surfaced is strong enough.

## Repository structure

### `daily_papers/`
Daily digests.

These files usually contain:
- the date,
- the day’s theme,
- a ranked short list,
- which paper is most relevant,
- whether any paper matters for novelty, baselines, framing, or related work,
- links to detailed notes.

### `paper_notes/`
Detailed single-paper notes.

These follow a structured template and focus on questions like:
- what problem the paper is solving,
- what the method actually is,
- why the design makes sense or does not,
- what data and evaluation really support,
- what is genuinely novel,
- what is weak, fragile, or overclaimed,
- why the paper matters for future work.

### `related_work/`
Topic-level synthesis notes.

These files are for grouping papers into reusable research lenses, not just isolated summaries.

### `reading_queue/`
Optional prioritized reading lists for future follow-up.

## Writing style and judgment standard

The notes in this repo aim to be:
- direct,
- compact,
- critical,
- concrete,
- useful.

They intentionally avoid:
- generic praise,
- inflated novelty claims,
- blind trust in author framing,
- pretending certainty where evidence is thin.

## Daily operating principle

The default principle is simple:

> optimize for research judgment, not volume.

A good day is not “many papers.”
A good day is:
- a small number of the right papers,
- clearly understood,
- critically evaluated,
- written in a way that reduces future cognitive load.

## Automation note

This repository is maintained through a recurring daily workflow. The workflow is expected to run once per day, generate or update notes, and push changes when possible.

## Task spec

The detailed operating instructions for the scouting workflow live in:

- [`TASK.md`](./TASK.md)

That file defines the required summary format, quality bar, paper selection rules, and output conventions.
