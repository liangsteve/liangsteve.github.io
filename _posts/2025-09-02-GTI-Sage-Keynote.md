---
layout: post
title: Human's Role in the Age of AI, IoT, and Digital Twins
---

At [GTI](https://www.gti.energy/)’s [Statistics, Analytics, and GIS for Energy (SAGE) Conference](https://www.gti.energy/training-events/events-overview/sage/), I had the privilege of sharing a keynote on a theme that has shaped my career for more than two decades: how human judgment and meaning remain essential in an era dominated by AI, IoT, and digital twins.


## Sensors Are Everywhere — But Still Fragmented

When Mark Weiser wrote in 1991 in the famous paper ["The Computer for the 21st Century"](https://ics.uci.edu/~corps/phaseii/Weiser-Computer21stCentury-SciAm.pdf): “the most profound technologies are those that disappear,” he foresaw a future where technology blended seamlessly into our daily lives. Twenty years ago, I suggested the same about the sensor web.

Today, sensors are indeed everywhere—embedded in vehicles, factories, supply chains, and cities. Yet most IoT systems remain siloed. Each network and application operates in isolation, like a body whose eyes, ears, and hands never share information. The result is inefficiency, costly errors, and a lack of real-time visibility.

The true value of IoT is about the speed to mix-and-match different observations from heterogeneous systems for innovative applications. It follows the Metcalfe's Law, i.e., the value of the network grows quadratically with the number of nodes, since every new node can connect with all the others.. As a result, it is critical to reduce the unecessary frictions within your organization that preventing the use and reuse these IoT sensor observations. A typical friction and might be the biggest friction is the lack of a common ontology and standards to enable write-once-use-many-time. Today's reality is write many times and create a miantenance nightmare (hence the friction is not getting smaller, but getting bigger). 

This matters more than ever because, historically, humans consumed sensor data for situational awareness before taking action. The consequences of the inability to mix-and-match of different sensing systems is not shown clearly, because human is the bottleneck of processing sensor data. Today, with abundant AI it is possible to unlock the human bottleneck, and unleash new capabilities that make me deeply optimistic.

At the same time, new capabilities expose previously hidden frictions. The central challenge is the inability to consistently understand and reuse real-time observations. If ontologies remain inconsistent—or worse, entirely absent—across sensing systems, AI will only amplify those gaps, producing results that are unreliable, non-repeatable, and potentially very costly.

Today, with abundant AI, the bottleneck of consuming multiple sensing observations for decisions is removed, and it makes me deeply optimistic about the future. However, as repeated again and again in the history, new capabilities typically also reveals the existing frictions. ANd in this case it is the inabiility to understand and reuse real-time observations. And the inconsistent ontology of different sensor observations will only make the AI results even more inconsistent and not repeatable, and more room to make very big mistakes. 

![Figure 1. The Network Effect (Metcalfe’s Law)](https://www.reliantsproject.com/wp-content/uploads/2020/06/reliants_keyconcepts-07.png)

Figure 1. The Network Effect (Metcalfe’s Law). Connecting siloed IoT systems doesn’t just add value linearly; it multiplies it. Every new connection creates new possibilities for insight and action. Reference: https://www.reliantsproject.com/2020/06/14/concept-8-metcalfes-law-and-network-effects/


## From Observations to Events

Standards and APIs for sensor observations are essential. [OGC/ISO 19156](https://www.ogc.org/standards/om/) provided a global model for observations and measurements. But we must move beyond raw, snapshot-based observations toward spatio-temporal events.

Why? Because the signal-to-noise ratio of individual observations is low. The real value lies in extracting events from continuous data streams—and, more powerfully, in detecting complex events that emerge from multiple simple events across different sensing systems. Traditional GIS platforms, built around static “snapshots,” struggle to capture this dynamic reality. Spatio-temporal event modeling is therefore at the frontier of IoT-enabled GIS research.

This is why my research group and SensorUp are developing the [OGC Emission Event Modeling Language (EmissionML)](https://github.com/opengeospatial/EmissionML)—an event-based ontology for one highly specialized but critical domain: emissions. The same approach can apply to other spatio-temporal events such as pipeline spills, extended cargo dwell times, or equipment malfunctions.

In a sensor-everywhere world, the ability for both humans and AI to act on rich event information just-in-time will prevent accidents, eliminate delays, and reduce waste.

## AI as a Prediction Machine

At its core, AI is about prediction: turning the information you do have into the information you don’t. Predictions were once expensive; today they are affordable and everywhere.

When predictions become highly accurate, systems can act before we even ask. Imagine trucks dispatched before a service request, inspections launched before equipment fails, or firefighters warned before a flashover.

AI makes IoT data far more valuable because observations and events become the training fuel for predictive models. Together, IoT and AI enable processes that are just-in-time: no wait, no waste, no accidents.

Here is a great follow-up reading about about AI as prediction machines: https://www.predictionmachines.ai/


## Generative AI and the Rise of Agents

Generative AI extends the power of AI from prediction to creation. These models can generate structured outputs—text, images, simulations, even multimodal experiences. As NVIDIA’s Jensen Huang noted at CES 2025, tokens are no longer just words; they can be anything.

Generative AI itself is not new. Google Translate, for example, is a specialized generative AI built for a single purpose. What’s new in recent tools, such as large language models (LLMs), is general-purpose accessibility. Instead of requiring a new system for every problem, LLMs can be instructed to translate, draft marketing copy, write code, or perform millions of other tasks—without retraining, fine-tuning, or redeployment. This leap from specialist to generalist systems is not just technical—it’s economic. It dramatically lowers the cost of solving entirely new classes of problems.

And now, we stand at the next leap: AI agents. Agents don’t just generate; they act. They set goals, take actions, observe results, and adapt in real time. If IoT gave us eyes and ears everywhere, and predictive AI gave us foresight, then agents represent the hands that can act on our behalf—turning data into decisions, and decisions into actions.

Consider a few possibilities:
	•	Energy & Emissions: An agent detects a methane leak, estimates its impact, files a repair ticket, and dispatches a crew—before a human even checks a dashboard.
	•	Logistics: An agent continuously reroutes deliveries as traffic and demand shift, removing waste from the supply chain.

With agents comes both capability and vulnerability. If agents act on fragmented or inconsistent data, they can amplify mistakes as efficiently as they amplify insights. Without consistent standards and ontologies, we risk creating fast, powerful systems that are also unreliable and non-repeatable.

The promise of agents, then, is profound: autonomous systems that integrate observations, prediction, and action at machine speed. But to realize this promise safely, we must first ensure that the data foundation they build upon is consistent, trustworthy, and reusable.


## Digital Twins: The AI Gym

The limiting factor for AI has always been data—expensive to collect, slow to label, and difficult to scale. Digital twins transform this challenge. Like flight simulators for pilots, they provide a safe, virtual environment where AI can practice without the cost or risk of real-world mistakes.

By creating virtual representations of real systems, digital twins accelerate the AI learning cycle: they enable simulation of scenarios, testing of “what if” counterfactuals, and refinement of decisions before deployment. They don’t just speed up training—they expand what’s possible, allowing foresight into situations that cannot be tested safely or affordably in the physical world.

But digital twins also come with risks. If they are too costly to build, they become bottlenecks; if they are poorly designed, they can mislead AI with false confidence. Inconsistent standards can even turn digital twins into new data silos. The real breakthrough comes when AI itself helps generate, validate, and evolve digital twins—turning them from a bottleneck into a flywheel of continuous improvement.

Imagine a planetary-scale training ground—where digital twins, continuously updated with real-time sensor events, teach AI agents to shape the physical world responsibly. More about Digital Twin as the AI Gym in a previous blog post: https://liangsteve.github.io/AIGym/


## The Future of Work: What I Tell My Kids

I often frame these ideas for my two boys, ages 7 and 9, by asking: what does the future of work look like for them?

AI, IoT, and digital twins will automate countless tasks. But they cannot replace human judgment, purpose, and meaning. As Vinod Khosla has argued, liberating people from survival jobs could redefine what it means to be human—enabling us to pursue creativity, learning, and intellectual goals for their own sake.

In short: machines will predict and simulate, but humans must continue to judge and decide.

## Closing Thoughts

The trajectory is clear: sensors everywhere, predictions everywhere, and digital twins fueling the next generation of AI agents. The key question is not whether machines will replace us, but how we design systems where machines provide the predictions, and humans provide the meaning.

This is the balance we must strike—a future where technology amplifies our humanness rather than diminishes it.
