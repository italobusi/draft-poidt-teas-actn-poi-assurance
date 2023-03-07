---
coding: utf-8

title: >
  Applicability of Abstraction and Control of Traffic Engineered Networks
  (ACTN) for Packet Optical Integration (POI) service assurance
abbrev: "ACTN POI Assurance"
category: info

docname: draft-poidt-teas-actn-poi-assurance-latest
submissiontype: IETF
v: 3
workgroup: TEAS WG

stand_alone: yes
pi: [toc, sortrefs, symrefs, comments]

author:
  -
    name: Italo Busi
    org: Huawei Technologies
    email: italo.busi@huawei.com
  -
    ins: J-F. Bouquier
    name: Jean-Francois Bouquier
    org: Vodafone
    email: jeff.bouquier@vodafone.com
  -
    name: Fabio Peruzzini
    org: TIM
    email: fabio.peruzzini@telecomitalia.it

normative:

informative:


--- abstract

This document extends the analysis of the applicability of Abstraction and Control of TE Networks (ACTN) architecture to Packet Optical Integration (POI), provided in RFC YYYY, to cover service assurance scenarios.

EDITORS NOTE: Replace RFC YYYY with the RFC number of \[I-D.ietf-teas-actn-poi-applicability] once it has been published.

   Existing IETF protocols and data models are identified for each
   multi-layer (packet over optical) service assurance scenario with a specific focus on
   the MPI (Multi-Domain Service Coordinator to Provisioning Network
   Controllers Interface)in the ACTN architecture.

--- middle

# Introduction

TODO Introduction

   Multi-layer and multi-domain service scenarios, based on the reference
   network described in section 2 of {{!I-D.draft-ietf-teas-actn-poi-applicability}} and very relevant for Service
   Providers, are described in sections {{optical-network}} and {{edge}}.

   For each scenario, existing IETF YANG data models,
   identified in section {{yang}}, are analyzed with a particular
   focus on the MPI in the ACTN architecture.

   For each multi-layer scenario, the document analyzes how to use the
   interfaces and data models of the ACTN architecture.

   A summary of the gaps identified in this analysis is provided in
   {{conclusions}}.

   Understanding the level of standardization and the possible gaps will
   help assess the feasibility of integration between packet and optical
   DWDM domains (and optionally OTN layer) in an end-to-end multi-vendor
   service assurance perspective.

# Conventions and Definitions

## Terminology

TODO Terminology

{: #ref-architecture}

# Reference Network Architecture

This document analyses several scenarios for service assurance in Packet and
   Optical Integration (POI) in which ACTN hierarchy is deployed to
   control a multi-layer and multi-domain network with two optical
   domains and two packet domains, as shown in Figure 1 of {{!I-D.draft-ietf-teas-actn-poi-applicability}}, which is copied in {{fig-ref-architecture}} below.

~~~~ ascii-art
{::include figures/reference-architecture.txt}
~~~~
{: #fig-ref-architecture title="Reference Network (copy of Figure 1 of RFC YYYY)"
artwork-name="reference-architecture.txt"}

EDITORS NOTE: Replace RFC YYYY with the RFC number of {{!I-D.ietf-teas-actn-poi-applicability}} once it has been published.

{: #yang}

# YANG Data Models for the MPIs

TODO YANG Data Models

Initial set of YANG models that are potentially in the scope of this analysis:
- ietf-alarms defined in {{!RFC8632}}
- ietf-performance-monitoring defined in {{!I-D.yu-performance-monitoring-yang}}

{: #optical-network}

# Optical Network Failure and Performance Degradation

{: #optical-fault}

## Fault Detection

TODO Describe fault detection performed by the O-PNC and how this information is reported to the MDSC: see for example the failure scenario in https://github.com/italobusi/draft-poidt-teas-actn-poi-assurance/files/10885907/2023.03.draft-poidt-teas-poi-assurance.pptx (slide 3)

{: #optical-degradation}

## Performance Monitoring

TODO Describe performance monitoring and performance degradation detection performed by the O-PNC and how this information is reported to the MDSC: see for example the degradation scenario in https://github.com/italobusi/draft-poidt-teas-actn-poi-assurance/files/10885907/2023.03.draft-poidt-teas-poi-assurance.pptx (slide 7)

{: #optical-protection}

## Protection Switching

TODO Describe how the MDSC coordinates the protection switching mechanisms at the IP layer (e.g., FRR) and at optical layer, including the reversion when the failure is repaired: see for example the protection switching scenario in https://github.com/italobusi/draft-poidt-teas-actn-poi-assurance/files/10885907/2023.03.draft-poidt-teas-poi-assurance.pptx (slide 3)

{: #optical-maintenance}

## Maintenance

TODO Describe how the MDSC initiates protection switching at the IP layer (e.g., FRR) and at optical layer at the beginning of a maintenance window, including the reversion after the maintenance operations are completed: see for example the maintenance scenario in https://github.com/italobusi/draft-poidt-teas-actn-poi-assurance/files/10885907/2023.03.draft-poidt-teas-poi-assurance.pptx (slide 4)

{: #edge}

# Failures between the IP and Optical edges

{: #edge-fault}

## Fault Detection

TODO Describe the mechanisms to detect when the failure occurs on a router port or on the router node connected with the optical domain: see for example the fault scenarios in https://github.com/italobusi/draft-poidt-teas-actn-poi-assurance/files/10885907/2023.03.draft-poidt-teas-poi-assurance.pptx (slide 5 and slide 6)

{: #edge-protection}

## Protection Switching

TODO Describe the mechanisms to protect the traffic  when the failure occurs on a router port or on the router node connected with the optical domain: see for example the protection scenarios in https://github.com/italobusi/draft-poidt-teas-actn-poi-assurance/files/10885907/2023.03.draft-poidt-teas-poi-assurance.pptx (slide 5 and slide 6)

{: #conclusions}

# Conclusions

This section will provide a summary of the analysis and of the gaps identified in this draft once the analysis is mature.

# Security Considerations

TODO Security

# IANA Considerations

This document has no IANA actions.


--- back

# Acknowledgments
{:numbered="false"}

TODO acknowledge.
