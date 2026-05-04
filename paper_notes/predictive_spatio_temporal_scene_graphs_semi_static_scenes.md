# Predictive Spatio-Temporal Scene Graphs for Semi-Static Scenes

## Basic info

* Title: Predictive Spatio-Temporal Scene Graphs for Semi-Static Scenes
* Authors: Miguel Saavedra-Ruiz, Charlie Gauthier, Kumaraditya Gupta, Shima Shahfar, Kirsty Ellis, Steven Parkison, Liam Paull
* Year: 2026
* Venue / source: arXiv
* Link: https://arxiv.org/abs/2605.00121
* Date surfaced: 2026-05-04
* Why selected in one sentence: It gives open-vocabulary scene graphs a concrete temporal forecasting mechanism instead of leaving them as static semantic memory.

## Quick verdict

**Useful**

This is not the flashiest paper, but it is one of the cleaner structured-memory papers in the batch. The important move is attaching Bayesian persistence filters to graph relationships so object locations can be forecast over semi-static routines. The weakness is that the setting is fairly specialized: semi-static object routines are easier than rich interactive dynamics.

## One-paragraph overview

The paper asks how a robot should reason about environments that are neither fully static nor fully chaotic. In homes or labs, many objects move in recurring patterns: mugs migrate between cupboard, counter, and sink; doors open on schedules; rooms have routine occupancy. The authors extend persistence estimation with a switching prior and embed it in an open-vocabulary 3D scene graph, creating PredictiveGraphs. In this representation, graph nodes are objects and edges carry temporal belief updates about spatio-semantic relations, allowing the robot to answer not only where an object is now, but where it is likely to be later.

## Key questions this summary must address

### 1. What problem is the paper trying to solve?
Most semantic mapping systems reason about geometry and semantics but not future state. This paper targets the gap between static maps and real environments where objects change location in structured, repeated ways.

### 2. What is the method?
The method combines two pieces. First, Perpetua* extends a persistence estimator with Bayesian model selection and switching priors. Second, PredictiveGraphs inserts these temporal estimators into an open-vocabulary scene graph so object states and relations can be forecast across time.

### 3. What is the method motivation?
The motivation is solid. Robots operating over days or weeks need more than a present-tense map. They need lightweight temporal structure that can exploit routines without assuming everything is fully predictable.

### 4. What data does it use?
The paper evaluates both in simulation and in a real-world dataset gathered over three weeks with bi-hourly observations in a lab undergoing semi-static changes.

### 5. How is it evaluated?
It is evaluated on future-state prediction and dynamic navigation tasks, including robustness under distribution shift. The key test is whether the robot can better infer object locations as the map becomes stale.

### 6. What are the main results?
The paper reports better future-state prediction than baselines in both simulation and real-world settings, including in environments with structured changes over time. The long-duration real-world setup is one of the more convincing aspects.

### 7. What is actually novel?
The main novelty is integrating persistence estimation into an open-vocabulary scene graph so temporal forecasting happens at the object/relation level, not only at low-level occupancy or feature persistence.

### 8. What are the strengths?
- Good fit between representation and problem structure.
- Real long-term setting instead of a toy short-horizon demo.
- Open-vocabulary semantic mapping plus temporal forecasting is a useful combination.
- Helpful citation for persistent world-state arguments.

### 9. What are the weaknesses, limitations, or red flags?
- The dynamics are semi-static and routine-driven, not truly interaction-rich.
- Discrete “receptacle” assumptions may simplify the problem substantially.
- It is more about temporal memory and prediction than broader world-model planning.
- Scalability to cluttered multi-object causal dynamics is unclear.

### 10. What challenges or open problems remain?
How should this extend to environments where object motion is caused by agents, tasks, or contacts rather than routine patterns? Can the same framework represent uncertainty over relational changes at larger scale?

### 11. What future work naturally follows?
- Combine routine forecasting with action-conditioned prediction.
- Move beyond discrete receptacles toward richer relational state spaces.
- Use the predictive graph as a substrate for planning, not only retrieval/navigation.
- Test in messier homes or warehouses with more object interactions.

### 12. Why does this matter for my work?
It matters as a concrete example of temporal structure being attached to a semantic world representation. If you want explicit memory or persistent world state to be more than rhetoric, this is a useful reference.

### 13. What ideas are steal-worthy?
- Attach temporal forecasting to object relations rather than raw frames.
- Use structured priors to model routine world changes.
- Treat stale-map reasoning as a first-class benchmark.
- Build world representations that can answer future queries, not only present ones.

### 14. Final decision
**Worth keeping, but not first priority.** Good citation material and useful adjacent inspiration for persistent world-state design.

---

## Confidence / access note

This note is based on the arXiv abstract plus the arXiv HTML paper text for the introduction and problem framing. I did not fully inspect every quantitative comparison in the PDF.
