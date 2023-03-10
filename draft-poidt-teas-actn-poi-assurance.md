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
  -
    name: Paolo Volpato
    org: Huawei Technologies
    email: paolo.volpato@huawei.com
  -
    name: Prasenjit Manna
    org: Cisco
    email: prmanna@cisco.com

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

In general, assurance involves detection and localization of link failures and performance degradation as well as re-routing (protection).

Two cases will be considered:
1. using grey interfaces on routers' ports, as outlined in {{!I-D.ietf-teas-actn-poi-applicability}}
2. using colored optical interfaces on routers' ports, as outlined in {{?I-D.mix-teas-actn-poi-extension}}

NOTE: It is not fully clear how much commonalities there are in service assurance for these two cases. This draft will start addressing both cases and assess at a later stage whether it is worthwhile keeping everything in a single draft or to split into two drafts.

The MDSC is responsible for coordinating the whole multi-domain, multi-layer (packet and optical) network. MDSC interacts with different Provisioning Network Controllers (O/P-PNCs) through the MPI interface.
The MPI interface presents an abstracted topology to MDSC, hiding the technology-specific aspects of the network and the topology details (depending on the policy chosen regarding the level of abstraction supported).

Following the assumptions of section 2.1.2 of {{I-D.ietf-teas-actn-poi-applicability}}, this document analyses scenarios where
the MDSC uses the partial summarization approach to coordinate multi-domain/multi-layer path computation.

In this approach, the MDSC has complete visibility of the TE topology of the packet network domains and an abstracted
view of the TE topology of the optical network domains.
That means the MDSC has the capability of performing multi-domain/single-layer path computation for the packet layer. The MDSC needs to delegate the O-PNCs to perform local path computation within their respective domains.
It uses the information received by the O-PNCs and its TE topology view of the multi-domain packet layer to perform multi-layer/multi-domain path computation.

P-PNCs are responsible for setting up the TE paths between any two PEs or BRs in their respective controlled domains,
as requested by MDSC, and providing topology information to the MDSC.

O-PNCs are responsible to provide to the MDSC an abstract TE topology view of their underlying optical network resources.
They perform single-domain local path computation, when requested by the MDSC. They also perform optical tunnel setup, when requested by the MDSC.

No GMPLS-UNI interaction between IP and Optical equipment is considered.
This is also the assumption followed in this document: the MDSC performs the function of multi-layer/multi-domain path computation
through the same mechanisms described in (I-D.ietf-teas-actn-poi-applicability) even if that is applied to the maintenance and protection cases described in the next sections.

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
