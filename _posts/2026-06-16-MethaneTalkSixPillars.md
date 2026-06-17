---
layout: post
title: Why I Gave a Methane Talk at an AI Conference — and the Six Pillars It Was Really About
---

<figure style="text-align: center;">
  <img src="/images/methane-talk/upperbound-2026-talk.jpg" alt="Steve Liang presenting on stage at Upper Bound 2026 in Edmonton" width="900">
  <figcaption style="font-size: 0.9em; color: gray;">Presenting <em>Automating the Path to Near-Zero Methane Emissions with Agentic AI</em> at Upper Bound 2026, Edmonton.</figcaption>
</figure>

Last month at [Upperbound](https://www.upperbound.ai/) 2026 — Canada's fastest-growing AI conference, hosted by Amii (the Alberta Machine Intelligence Institute) in Edmonton — I gave a talk titled *"Automating the Path to Near-Zero Methane Emissions with Agentic AI."* A reasonable reading of the title would suggest methane was the focal point. It was — but not the only one.

Net zero was the wedge. The payload was six architectural pillars I argued an AI agentic operating system needs in order to run complex physical operations — a framework to evaluate any solution claiming to do this kind of work. Methane is one of the cleanest test cases I know: high-stakes, regulated, measurable, multi-sensor, spatial, and with an unambiguous economic incentive to fix. But the same six pillars apply just as well to energy, mining, rail, ports, utilities, waste management, and similar domains where AI has to act on infrastructure rather than on tokens.

A full reference architecture — the kind you could hand to an engineering team and say "build to this" — is the topic of a follow-up post I owe myself. What I shared at Upperbound, and what I'll share here, are the six required foundational components: what each one solves, and what breaks when any one is missing.

This post is for the people in the audience who came up to me afterwards asking: *we want to build something like this — what do we actually need?* Here's what we need.

## The agent conversation is missing a continent

In 2026, the public conversation about AI agents is dominated by coding agents and chatbots. Coding copilots. Research agents. Customer support. These are real, valuable, and growing fast. They share one structural property: the world they observe and act in is text.

Physical operations are a different country. The agent has to reason about physical infrastructure with regulatory consequences, heterogeneous multi-sensor inputs with deployment-dependent uncertainty, geographic context spanning kilometers and centimeters, time-bounded events that may take hours or months to unfold, and feedback loops where a wrong action shows up in real emissions, real safety incidents, and decisions that can't be undone. The primitives that work in a browser break down here — not because LLMs aren't capable, but because they're being asked to operate without the scaffolding that physical operations require.

Here are the six pillars I shared on stage. In my experience, all six are necessary for an agentic OS that has to operate in the physical world — and the same list works as a framework for evaluating any solution that claims to do this.

## 1. Semantic grounding — ontologies, not prompts

LLM-based agents struggle with ambiguous terminology, inconsistent schemas, missing context, implicit relationships, unit confusion, operational semantics, and domain-specific meaning. Anyone who has tried to point an LLM at a real-world, messy industrial dataset with poor or missing metadata knows this is not a list of edge cases. The output is unpredictable, untraceable, and unauditable — and in any regulated industry, that's disqualifying.

The fix is not better prompts. The fix is an ontology that constrains, contextualizes, and aligns the agent's reasoning. *Standards-grounded data foundations* — open standards like OGC/ISO 19156 Observations & Measurements, ISO 19157 Data Quality, W3C SOSA/SSN, and OGC EmissionML — give an agent a shared vocabulary in which "methane emission rate of 5.2 kg/h estimated by a pole-mounted OGI camera observing the emission source — a thief hatch on Tank 204 — with phenomenon time starting 2026-04-18 at 14:23 UTC and result available at 14:35 UTC" is no longer eight guesses but a single, validated, cross-referenced statement in the operational knowledge graph. Without this pillar, every downstream pillar compounds the same semantic drift.

This is the pillar that distinguishes a reliable agent from an impressive demo.

## 2. Spatial primitives — beyond lat/lon

Agents that live in the physical world need stable spatial context, hierarchical reasoning across scales, locality-aware decision making, neighborhood semantics, containment and proximity reasoning, multi-resolution spatial memory, and globally consistent spatial partitioning.

Lat/lon alone gives you none of these. Lat/lon is an angular coordinate system on a curved reference surface — built for *point identification*, not for *spatial analysis*. It's continuous (no intrinsic cells to aggregate or neighbor on), hierarchically flat (no parent or child), and locally distorted (a degree of longitude is one thing at the equator and a very different thing near the poles). For any analytic operation, lat/lon needs additional structure imposed on top.

Classical GIS offers three families to impose that structure: **field-based** representations (rasters, continuous surfaces), **object-based** representations (vector features), and **grid-based** representations (DGGS like [rHEALPix](https://www.tandfonline.com/doi/full/10.1080/17538947.2025.2607210), plus related systems like H3 and S2). None is universally best — the right choice depends on the operation. Continuous phenomena like methane plumes want fields. Discrete assets like wells and pipelines want objects. Multi-scale aggregation, global indexing, and consistent neighborhood reasoning want grids.

One strong example for the grid cluster — and the one closest to my own work — is a Discrete Global Grid System: a hierarchical, globally consistent tessellation of the Earth into addressable cells at every resolution. Cell `R7-3194-22` means the same thing to every agent anywhere, contains a well-defined set of child cells, and supports proximity, adjacency, and containment queries in constant time. For the operations DGGS suits, it's as foundational to space as UTC is to time.

The deeper point is that physical-world agents need *some* explicit spatial primitive richer than lat/lon — chosen deliberately, sometimes more than one, for the operation at hand. Most agent frameworks ship without any spatial primitive at all. That's the gap.

## 3. Observations and events — the right unit of reasoning

Raw sensor data is a stream of timestamps and numbers. That alone isn't enough. The right unit of reasoning is an *event* — a release of methane from a specific source feature over a defined time interval, witnessed by multiple observation types that each carry their own provenance and uncertainty.

This reflects the classical ontological distinction between continuants (assets that persist through time—wells, tanks, pipelines) and occurrents (processes and events that unfold through time—emissions, repairs, inspections, deliveries). Conflating the two leads to a provenance error: the act of observing an emission is not the same as the act of emitting. Keeping those activities distinct is essential for attribution, quantification, and mitigation.

The [OGC Emissions Event Modeling Language (EmissionML)](https://github.com/opengeospatial/EmissionML) is one concrete example: an EmissionEvent is a 6-tuple of (t_start, t_end, source feature, substance, quantity, observations), and multiple heterogeneous observations — satellite, flyover, optical gas imaging, continuous monitoring, SCADA, field logs — are all linked back to the same event as evidence. This is the abstraction the agent's memory, prediction, and action all run on top of.

## 4. Multi-agent decomposition — operations are not monoliths

A single large LLM cannot run the operations of a methane program, a port, or a plant. The actual operation decomposes into roles — a coordinator that translates goals into sub-tasks, inspectors that detect, planners that schedule, repair crews that act, reconcilers that integrate, regulators that audit. The agentic OS has to mirror that decomposition.

Each agent gets a bounded scope, a defined set of tools, a memory of past actions and outcomes, and a goal it's accountable for. They communicate through the shared semantic and spatial pillars above — not through ad-hoc JSON blobs. Our GeoLLAMA architecture is one realization: a Site Coordinator agent translates an operator's intent, dispatches Inspection Crew agents (drone, aircraft, truck), routes detections to a Repair Crew, and feeds outcomes back into a Reconciler that updates the operation's emissions inventory.

Convergent evidence, from a domain as different as biomedicine: a peer-reviewed multi-agent system for scientific hypothesis generation, published in *Nature* in 2026, lands on the same shape — a coordinator agent orchestrating specialized worker agents (generation, critique, ranking, refinement) over an asynchronous task queue, with persistent shared state across the team.[^1] Different industry, identical architecture. The pattern isn't a methane-specific quirk; it's where multi-agent systems land when the work doesn't fit one model.

One detail from the same work is worth holding onto. Their critic agent — the one whose job was to find flaws in a proposed hypothesis — was given its own independent access to external search tools, separate from the agent that generated the hypothesis. Strip that access away and the critic starts hallucinating novelty — approving as new something already published. In their ablations, grounding the critic in independent search was one of the changes that visibly improved reliability.[^3]

The lesson plausibly translates. The critic in a physical-operations OS — whatever you call it: a planner's reviewer, a dispatch validator, a regulatory checker — shouldn't share context with the planner it's reviewing. It needs an independent read of the operational record (digital twin, standards vocabulary, historical event log) through tools the planner does not have. The co-scientist result suggests why: without that independence, a critic tends to drift toward confirming the planner's confidence rather than catching its errors.

This pattern — coordinator-plus-specialists with adversarially-grounded critics, sharing a typed event substrate — is, I'd argue, where physical-operations agent systems tend to converge. The evidence base is still thin (one methane architecture, one biomedical system from a different field), but the convergence across two domains that share so little is what makes me think it's structural rather than incidental.

## 5. The AI Gym — digital twins as the training environment

Real-world phenomenon data (observations and events) are the fuel for these agents, but it's slow, expensive, and unscalable. You cannot wait a year for a real methane event to test a new dispatch policy. You cannot let an inexperienced repair-planning agent practice on a live plant.

The answer is the same one aviation figured out fifty years ago: simulate. Digital Twins are the sparring partners — high-fidelity, physics-grounded simulation environments where AI agents fail safely, learn fast, and generate synthetic data to enrich real-world observations. A site coordinator agent can dispatch ten thousand simulated field crews against a year of simulated weather and emissions before its first real deployment.

Practice is one use. The deeper function of the Gym is *ranking* — choosing which candidate plan is worth touching reality with at all. In the same biomedical hypothesis system above, the agents proposed roughly thirty candidate ideas, ran a tournament of pairwise debates between them with an Elo score updated after each round, and only the top three candidates went on to expensive wet-lab validation.[^4] The cheap, fast ranking happened entirely in-system; the expensive real-world test was reserved for the finalists.

The same logic carries straight into a physical-operations OS. The Coordinator proposes ten dispatch policies for next quarter — different sensor cadences, different crew assignments, different deferred-repair thresholds. The Gym simulates each one against a year of stochastic weather and emissions in the digital twin, runs pairwise debates between the resulting outcomes with an explicit scoring rubric (cost, emission reduction, regulatory margin, crew burden), and only the top one or two reach the real fleet. The Gym is the LDAR backtest, the dispatch tournament, and the policy A/B harness all in one. Without it, every policy decision is implicitly betting on its first deployment.

The catch is that building good digital twins is itself a bottleneck. AI helps here too — generating, calibrating, and refining twins from real sensor data — and the result is a flywheel: better twins train better agents, better agents help build better twins, faster than either could move alone. I called this the *AI Gym* in [an earlier post](https://liangsteve.github.io/AIGym/); twelve months on, it's looking less like a metaphor and more like a system design principle.

## 6. Closed-loop self-improvement — the operation has to learn

The final pillar is the loop that ties it all together. Borrowing the AI Canvas from Agrawal, Gans, and Goldfarb's *Prediction Machines*, an agentic OS for physical operations looks like:

> **Observations and Context** → **Prediction** (the agent's reasoning) → **Operational Actions** → **Outcome** → **Learning** → back into Prediction, with **Human Judgement** governing throughout.

<figure style="text-align: center;">
  <img src="/images/methane-talk/closed-loop-canvas.svg" alt="The closed loop: Observations & Context feed Prediction; Prediction drives Operational Actions, which produce an Outcome, which produces Learning that updates the agent's skills and standing instructions and feeds back into the next Prediction — the whole cycle governed by Human Judgement." width="900">
  <figcaption style="font-size: 0.9em; color: gray;">The closed loop, adapted from the AI Canvas in Agrawal, Gans &amp; Goldfarb's <em>Prediction Machines</em>: outcomes drive learning that updates the agents' standing instructions — not their weights — and human judgement governs the whole cycle.</figcaption>
</figure>

The outcome from a real action — a repair completed, an emission averted, a regulatory threshold met or missed — flows back as a learning signal. And the learning doesn't have to mean retraining a model. The faster, cheaper surface is the agents' own standing instructions. Boris Cherny, who built Anthropic's Claude Code, describes how an organization's operating knowledge gets captured not in model weights but in *skills* the agents read — at Anthropic, onboarding a new engineer dropped from weeks to two days, because the answer to "how do I query the database" became a skill the agent already knew.[^5] The same move appears in a field entirely unlike it: a multi-agent system for biomedical hypothesis generation used a meta-review agent to distill recurring patterns from a tournament of candidate outputs and fold them into the next iteration's system prompts — no weight updates, no reinforcement-learning pipeline.[^2] For a physical-operations OS the same surface is available: post-action critique from the Reconciler folds back into the Coordinator's standing instructions for the next dispatch. The OS gets better at planning before any underlying model gets better at anything.

Over months, the operation literally gets better at running itself — and the human's role shifts with it, from authoring each decision to tending the loop that authors them. Cherny describes the same shift in software: "I don't prompt Claude anymore. I have loops that are the ones prompting Claude and figuring out what to do. My job is to write loops."[^5] In a methane program the equivalent operator stops writing each dispatch and instead maintains the loop around it — the objectives, the scoring rubric, the human-judgement gates. This is what "agentic" actually buys you: not autonomy for its own sake, but a system that compounds its own competence.

Without this loop, you have a clever assistant. With it, you have an operating system.

## The shift these six pillars unlock

The visible payoff of all six pillars running together isn't a smarter model or a slicker dashboard — it's a different *decision cadence*. The methane industry currently runs on annual inspection-and-repair plans, and most regulated industrial sectors run on annual-cadence equivalents of their own: a consultant is hired, operator intent is translated into a simulator's input format, the simulator runs, the results are translated back into a narrative, and an inspection-and-repair program is locked in for the next twelve months. The consultant's job, stripped of its ceremony, is *translation* — and the cost of that translation is what gates the frequency of every operational decision downstream.

Replace the human translator with an LLM agent that knows the simulator's schema, speaks the operator's vocabulary, and shares the same standards-grounded event substrate as the operations data, and the cadence shifts by orders of magnitude. Annual inspection-and-repair plans become weekly operational policies. The simulator that was previously a once-a-year deliverable becomes an overnight tool the operator runs against this morning's measurements. Strip out any one of the pillars and the system regresses — to a chatbot over a spreadsheet, or to a faster consultant. Keep all six and the planning artifact stops being a deliverable and starts being a *living policy*.

When I find the time, I'll come back to what this transformation looks like in practice — what an operator's week looks like on the new cadence, why the *consulting layer* (not the simulator) is the part that gets restructured, what humans actually do in the agentic era, and what generalizes to water, mining, ports, and rail — in a follow-up post. In the meantime, if any of these threads is of interest, feel free to [connect with me on LinkedIn](https://www.linkedin.com/in/steve-liang-198b44/) — I'd be glad to compare notes.

## What these six pillars are not

Worth being explicit about, because every one of these confusions has come up in conversation:

- It is **not a chatbot** for emissions data. A natural-language interface is the last mile, not the system.
- It is **not a single AI model**, however large. The six pillars each need their own implementation; the magic is in the integration.
- It is **not a forecasting tool**. Forecasting is one prediction the agents make. Acting on the forecast is the other half.
- It is **not specific to methane**. Methane is where we've proved it because the data, the regulations, and the economics line up. The pillars themselves are domain-neutral.
- It is **not a feature** you can bolt onto an existing analytics platform. These are foundational pillars. Treat them as features and you'll end up with a dashboard that hallucinates.
- It is **not, yet, a full reference architecture**. It's the framework — necessary ingredients and an evaluation lens. The reference architecture that maps every pillar to concrete components, interfaces, and data contracts is the next piece of writing I owe.

## What I want builders to take away

If you're building agentic AI for any complex physical operation — emissions, energy, water, manufacturing, logistics, utilities, urban systems — these six pillars are the minimum checklist. None of them are research projects anymore. The open standards exist (OGC, ISO, W3C). The spatial primitives are mature. The event ontologies are being standardized in working groups I and others chair. The multi-agent patterns have settled. Digital twins are commodity. The closed loop is engineering, not magic.

What's hard is *integrating all six*, in production, against the real heterogeneity of a real industry. That's the work. It's the work we've been doing at SensorUp for years, and it's the work I expect will define the next decade of AI in the physical economy — long after the coding-agent gold rush has moved on.

Net zero is the wedge. The six pillars are the payload — a framework to use today. A full reference architecture is the post I owe you next. In the meantime: what complex physical operation are you trying to automate — and which of these six pillars is missing from your stack?

## References

[^1]: Gottweis, J. et al. (2026). Accelerating scientific discovery with Co-Scientist. *Nature.* https://doi.org/10.1038/s41586-026-10644-y — see the Methods section for the Supervisor agent orchestrating Generation, Reflection, Ranking, Evolution, Proximity, and Meta-review specialized workers over an asynchronous task queue.

[^2]: Gottweis et al. (2026), op. cit. — see the description of the Meta-review agent, which synthesizes recurring patterns from a tournament of candidate hypotheses and propagates feedback by appending to other agents' system prompts in the next iteration. The paper describes this as "feedback propagation and learning without back-propagation techniques."

[^3]: Gottweis et al. (2026), op. cit. — see the agent ablation analyses (Methods and Supplementary Note 3). The paper reports that granting the Reflection agent access to external search tools "effectively prevented the hallucination of seemingly novel but implausible hypotheses." The Reflection agent's stated role is "simulating the role of a scientific peer reviewer, critically examining the correctness, quality, and novelty of the generated hypotheses."

[^4]: Gottweis et al. (2026), op. cit. — see the description of the Ranking agent, which "employs and orchestrates an Elo-based tournament" using "pairwise comparisons, facilitated by simulated scientific debates," and the wet-lab validation flow in which only the top-ranked candidates were selected for in vitro experiments (e.g., "Thirty top-ranked drug candidate hypotheses were shared with expert oncologists" before AML cell-line testing).

[^5]: Cherny, B. (2026). *Claude Code & the Future of Engineering*, Acquired Unplugged (presented by WorkOS). https://www.youtube.com/watch?v=RkQQ7WEor7w — Cherny, who built and leads Anthropic's Claude Code, describes the shift to writing "loops" rather than prompts (≈11:45); onboarding time at Anthropic dropping from weeks to two days because operational knowledge is captured as reusable *skills* the model reads (≈9:55–10:13); and organizational principles documents that "the model can use… in the form of skills" (≈24:55).
