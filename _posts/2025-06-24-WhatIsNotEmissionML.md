# What EmissionML *Is Not* — and Why That Matters

As the chair of the OGC [EmissionML Standard Working Group](https://github.com/opengeospatial/EmissionML), I’ve had many conversations about what EmissionML is—and just as importantly, what it *isn’t*. It’s an initiative I’m deeply passionate about, and frankly, one that’s often misunderstood. So let’s clear the air.

Below are several common misconceptions I’ve encountered, along with clarifications to help position EmissionML accurately in the broader emissions ecosystem. Special thanks to DoE's Tim Skone and GTI Energy's Dr. Zach Weller for their valuable conversations that informed this post.

Table below is the summary. Details are below.

### Clarifying the Scope of EmissionML

| EmissionML *IS*                                         | EmissionML *IS NOT*                                |
|------------------------------------------------------------|--------------------------------------------------------|
| A standardized **data model and ontology**                 | Not a methane MMRV protocol (e.g., MiQ, Veritas, DoE)      |
| A foundation for **interoperable reporting formats**       | Not a fixed reporting format (e.g., CSV template, PDF)     |
| A semantic link between **observations** and **events**    | Not a raw sensor data format                               |
| An enabler for **AI-ready structured data**                | Not an AI/ML model                                         |
| A specification adopted by **software platforms**          | Not a software product or downloadable app                |
| Designed to support **data quality, provenance, and context** | Not a methodology for how to measure or quantify emissions         |

---

## EmissionML is NOT a methane MMRV protocol

This is a big one. EmissionML is designed to support and integrate with MMRV (Measurement, Monitoring, Reporting, and Verification) protocols like [MiQ](https://miq.org/), [DoE Greenhouse Gas Supply Chain Emissions MMRV Framework](https://www.energy.gov/fecm/greenhouse-gas-supply-chain-emissions-measurement-monitoring-reporting-verification-framework), [OGMP 2.0](https://www.ogmpartnership.org/), and [Veritas](https://veritas.gti.energy/protocols)—but it is not one of them.

MMRV protocols define the process of measurement, monitoring, reporting, and verification of emissions to ensure accurate, transparent, and accountable quantification for regulatory or voluntary frameworks.

EmissionML, in contrast, provides a standardized modeling language to represent:

- Emission events (when, where, how much)  
- Observations that observed those events  
- Data quality, including uncertainty  
- Provenance of the data used  

It’s the common vocabulary that allows different MMRV programs to share, compare, and interoperate without building custom data translators for every implementation.

---

## EmissionML is NOT a reporting format

This is a subtle but crucial distinction. A reporting format typically refers to a CSV template, PDF layout, or specific API schema for submitting emissions data. These are often rigid and built for specific organizational needs.

EmissionML is not that. It's a modeling language based on a formal ontology. It defines the fundamental concepts and relationships necessary to describe emission-related information.

Organizations and regulatory bodies can use EmissionML to design their own reporting formats—while ensuring interoperability with others. For instance, a government agency could say:

> “Our reporting format for methane emissions will be a CSV file structured based on the EmissionML ontology, with these specific optional fields marked as mandatory for our jurisdiction.”

EmissionML provides the building blocks—not the finished report.

---

## EmissionML is NOT an AI model

It’s easy to conflate structured data with AI. But EmissionML doesn’t analyze, predict, or learn. It’s not a model in the machine learning sense.

What EmissionML *does* is provide the structured, contextualized data that AI systems desperately need to function effectively. Without a common data foundation, AI models are forced to learn from messy, inconsistent inputs. EmissionML transforms that chaos into semantically rich, linked datasets that support:

- Emission source attribution and root cause analysis  
- Predictive analytics  
- Optimization and automated auditing  

In short: EmissionML is not the AI—it’s the **fuel** that powers it.

---

## EmissionML is NOT a software

You won’t find an “EmissionML app” to download. It’s not a tool or service—it’s a **standard**: an [Open Geospatial Consortium](https://ogc.org/) specification with requirement classes, schemas, and controlled vocabularies, and will be submitted to ISO to be considered as an official ISO standard.

However, EmissionML is intended to be widely implemented in software. Developers can use EmissionML to:

- Build data platforms that store and serve standardized emissions data  
- Create visualization and analysis tools that consume consistent data formats  
- Enable reporting tools that generate compliance-ready outputs  

Think of it like HTML—not a website, but the structure behind every interoperable page.

---

## EmissionML is NOT a sensor data format

While EmissionML deals with observational data from sensors, it doesn’t define raw sensor data formats from various sensing data providers.

Instead, EmissionML focuses on standardizing **observations**—the processed, meaningful outputs derived from raw sensor data—and relating those to the emission events they inform. EmissionML follows the ISO standard for observations ([OGC/ISO 19156:2023](https://www.ogc.org/standards/om/)). It allows you to describe:

- What was observed (e.g., the presence of emissions or the emission rates)  
- How it was observed (e.g., via OGI, satellites, Hi-Flow meters)  
- When and where the observation occurred  
- How that observation supports the emission event (e.g., volume/mass, confirming location, indicating start or end time)  

For example, EmissionML helps you represent:

> “The satellite was the first to detect the emission. OGI confirmed it originated from a thief hatch of a tank at Wellpad XYZ. A Hi-Flow meter quantified the rate. A field log confirmed the event ended.”

This **rich semantic linking** turns raw data into a traceable, machine-readable emission narrative.

---

## Final Thoughts

Understanding what EmissionML *is not* is essential to using it effectively. It is not a protocol, software, or AI—but rather a **data model and vocabulary** that underpins all of them. By clearly defining emission events, observations, and their context, EmissionML provides the semantic foundation needed for credible reporting, rigorous analysis, and scalable interoperability.

If you’re working on emissions data and want to avoid reinventing the wheel—or if you’re building the next generation of MMRV tools or AI systems—EmissionML is designed to help. Let me know how you’d like to contribute or collaborate.