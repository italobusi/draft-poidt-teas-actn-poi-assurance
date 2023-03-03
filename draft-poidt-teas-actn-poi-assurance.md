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

[EDITORS NOTE: Replace RFC YYYY with the RFC number of draft-ietf-teas-actn-poi-applicability once it has been published.]

   Existing IETF protocols and data models are identified for each
   multi-layer (packet over optical) service assurance scenario with a specific focus on
   the MPI (Multi-Domain Service Coordinator to Provisioning Network
   Controllers Interface)in the ACTN architecture.

--- middle

# Introduction

TODO Introduction

   Multi-layer and multi-domain service scenarios, based on the reference
   network described in section 2 of {{!I-D.draft-ietf-teas-actn-poi-applicability}} and very relevant for Service
   Providers, are described in sections {{optical-network}}, {{router-port}} and {{router-node}}.

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
{: #fig-ref-architecture
title="Reference Network (copy of Figure 1 of {{!I-D.draft-ietf-teas-actn-poi-applicability}})"
artwork-name="reference-architecture.txt"}

{: #yang}

# YANG Data Models for the MPIs

TODO YANG Data Models

{: #optical-network}

# Optical Network Failure and Performance Degradation

{: #optical-fault}

## Fault Detection

{: #optical-degradation}

## Performance Monitoring

{: #optical-protection}

## Protection Switching

{: #optical-maintenance}

## Maintenance

{: #router-port}

# Failure of a router port

{: #router-node}

# Failure of a router node

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
