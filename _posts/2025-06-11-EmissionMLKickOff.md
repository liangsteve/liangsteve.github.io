On June 11 2025, I chaired the kickoff meeting of the OGC Emission Event Modeling Language Standards Working Group, held in Mérida, Mexico. Below is a summary of the meeting, which is also published on the [SensorUp blog](https://www.sensorup.com/blog).

# OGC EmissionML Standard Working Group Kickoff Meeting Summary

On June 11, 2025, the [EmissionML Standard Working Group (SWG)](https://github.com/opengeospatial/EmissionML) officially launched during [the 132nd Open Geospatial Consortium (OGC) Technical Committee Meeting](https://events.ogc.org/132MemberMeeting#/?lang=en) held in Mérida, Mexico. Hosted by [CentroGeo](https://www.centrogeo.org.mx/), this kickoff marked an important milestone in establishing a structured, interoperable, and machine-readable foundation for modeling emission events across sectors and geographies.

## The Motivation Behind EmissionML

Today, emissions data is often scattered across disconnected formats—spreadsheets, PDFs, proprietary tools—with inconsistent terminology and minimal traceability. This fragmentation limits effective data reuse, hinders cross-platform integration, and complicates reporting obligations for regulators and operators alike. EmissionML seeks to address these challenges by offering a unified, extensible ontology and data model grounded in spatio-temporal principles.

Crucially, EmissionML is not a fixed reporting template, but a modeling language—a foundational framework that allows emission data to be expressed in a machine-readable, interoperable way. It provides a common vocabulary and structure for representing emission events, but leaves room for implementation flexibility to support diverse regulatory frameworks, domain-specific methods, and organizational reporting needs.

By defining emissions in terms of well-scoped events, EmissionML allows for consistent tracking, attribution, aggregation, and reconciliation, with explicit support for uncertainty and data provenance. The model can be adapted to describe methane from oil and gas operations, CO₂ from industrial sources, landfill emissions, or even synthetic test data from simulators—all while preserving semantic clarity and interoperability.

## Deliverables and Development Roadmap

The SWG will focus on developing a core ontology for emission events, along with domain-specific extensions such as MethaneML. Encodings in formats like JSON and CSV are planned, along with best practice guides to support uncertainty modeling, event reconciliation, and integration with existing monitoring and reporting systems. 

The group is targeting submission of the standard to [the OGC Architecture Board](https://www.ogc.org/our-committees/) by October 2025. A public review period will follow, after which the standard will be proposed for adoption as part of the ISO 19000 series through [ISO/TC 211](https://committee.iso.org/home/tc211).

## Leadership and Community Engagement

[Dr. Steve Liang](https://liangsteve.github.io), professor at the University of Calgary and CTO of [SensorUp](https://www.sensorup.com/), was elected Chair of the SWG. Ryan Ahola of [Natural Resources Canada](https://natural-resources.canada.ca/) was appointed Co-Chair. The working group will meet biweekly online, with in-person sessions scheduled during future OGC Technical Committee meetings in Boulder (October 2025), Philadelphia (March 2026), and either Japan or Portugal (June 2026), culminating with a global session in South Africa in October 2026.

The development process is fully open. One of the motions approved during the SWG kickoff meeting designated the [EmissionML GitHub repository](https://github.com/opengeospatial/EmissionML) as the central platform for documentation, version control, issue tracking, and community contributions.

## Use Cases Presented

Two early use cases were presented in the SWG meeting, and showcased how EmissionML could meet practical needs in emissions research and industrial applications.

[Dr. Erin Li](https://ca.linkedin.com/in/mingke-erin-li) presented a methane inventory methodology using Discrete Global Grid Systems (DGGS). She explained how DGGS offers uniform spatial resolution and simplifies the comparison of emission intensities across regions. Integrating DGGS identifiers and resolution metadata into EmissionML would enable scalable reporting and attribution at multiple levels of spatial granularity.

[Jingya Wang](https://ca.linkedin.com/in/jinya-wang-1902812a1), an MSc student from the University of Calgary, introduced GeoLLaMA, an agent-based simulation platform for Leak Detection and Repair (LDAR). She demonstrated how the current lack of standardization in emission input/output formats complicates simulation workflows and cross-tool validation. EmissionML, she argued, could serve as a common interface for simulation inputs, outputs, and result sharing.

## Modeling Framework and Core Concepts

Dr. Liang introduced the draft conceptual model for EmissionML. Each *EmissionEvent* is defined by a *StartEvent*, an *EndEvent*, an *EmissionQuantity* (such as rate, mass, or volume) determined by a *QuantificationDeterminationMethod*, and a *SourceFeature*, which may represent a site, facility, piece of equipment, or geographic region. The model also supports multiple ISO/OGC *Observations* — such as satellite, flyover, continuous monitoring, optical gas imaging, field logs, or even operational systems—linked to each event, along with an approach for selecting the best estimate based on methodological quality.

The design explicitly accounts for uncertainty in temporal, spatial, and quantitative dimensions. It also supports hierarchical spatial features (from component to basin level), integration with controlled vocabularies, and alignment with key standards such as [ISO 19157](https://www.iso.org/standard/78900.html) for data quality and [ISO/OGC 19156:2023](https://www.ogc.org/standards/om/) for observations, measurements, and samples.

## Community Discussion Highlights

Several experts offered feedback during the session. Tim Skone from the U.S. Department of Energy emphasized the importance of designing the model to accommodate sparse data and high uncertainty—common conditions in real-world emissions monitoring. Zachary Weller from GTI Veritas pointed to the need for disambiguation around terms like “source” and stressed the importance of supporting multiple spatial resolutions for both internal analysis and public disclosure.

The consensus was that EmissionML must support flexible, multi-resolution reporting and provide clear semantic definitions to enable adoption across regulatory, scientific, and commercial domains.

## Open Footprint Data Model and EmissionML

During the kickoff meeting, [AJ van de Voort](https://www.linkedin.com/in/arjen-van-de-voort-92190b3) from the [Open Footprint Forum](https://www.opengroup.org/openfootprint-forum) presented the [Open Footprint Data Model](https://blog.opengroup.org/2024/04/11/the-open-group-open-footprint-data-model-snapshot-is-now-released-and-available/), which focuses on providing standard data element definitions for the various areas that comprise an organization’s emissions footprint. AJ discussed how EmissionML and Open Footprint serve complementary purposes—Open Footprint provides high-level organizational accounting, while EmissionML offers fine-grained, spatio-temporal modeling of individual emission events. Together, the two standards can support a complete emissions data ecosystem from source-level detection to enterprise-level reporting.

## Upcoming SWG Outreach Activities

In the next quarter, the EmissionML SWG will engage in targeted outreach to broaden stakeholder involvement and gather feedback. Planned activities include participation in [the invitation-only Third United Nations High-Level Expert Group Meeting on Data and Frontier Technologies for the Planet](https://eo4society.esa.int/event/third-high-level-expert-group-meeting-on-big-data-2025/), as well as a presentation at [CH₄ Connections 2025](https://www.gti.energy/training-events/ch4-connections/)—a leading conference focused on methane emissions science, policy, and technology.

## Next Steps

With strong initial momentum, the SWG will continue refining the UML-based data model, aligning it with relevant OGC and ISO standards, and gathering additional input from regulators, certifiers, technology providers, and researchers.

An important guiding principle is that EmissionML is not prescriptive about what must be reported—it is descriptive about how emissions can be modeled. This distinction allows the standard to support both existing protocols (such as [OGMP 2.0](https://www.ogmpartnership.org/), [GTI Veritas](https://veritas.gti.energy/), and [MiQ](https://miq.org/)) and emerging use cases that require more flexible or higher-resolution representations. Whether used to document direct measurements, inferred quantities, or simulated outputs, EmissionML enables structured, traceable representation of emissions in a way that supports both transparency and reuse.

There are also plans to collaborate with international initiatives, such as the [CEOS](https://ceos.org/) efforts to standardize satellite-based methane data, and to onboard new use cases from sectors beyond oil and gas, such as agriculture, landfills, and transportation.

## Get Involved

Whether you work in emissions research, policy, regulation, software development, or operations, your input is essential to shaping this emerging standard. The SWG invites all interested parties to participate in the development process.

To get involved, visit the [EmissionML GitHub repository](https://github.com/opengeospatial/EmissionML) for access to meeting notes, draft models, and open issues. You can also contact SWG Chair Dr. Steve Liang (steve dot liang at ucalgary dot ca) to be added to the mailing list and receive meeting invitations.

EmissionML is more than a standard—it’s the foundation for explainable, machine-readable, and trustworthy emissions data.
