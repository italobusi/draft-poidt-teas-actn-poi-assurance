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

This document extends the analysis of the applicability of Abstraction and Control of TE Networks (ACTN) architecture to Packet Optical Integration (POI), provided in RFC YYYY, to cover multi-layer service assurance scenarios, for end-to-end customer L2VPN or L3VPN connectivity services setup over underlying transport optical paths, with specific Service Level Agreement (SLA) requirements.

EDITORS NOTE: Replace RFC YYYY with the RFC number of draft-ietf-teas-actn-poi-applicability once it has been published.

   Existing IETF protocols and data models are identified for each
   multi-layer (packet over optical) service assurance scenario with a specific focus on
   the MPI (Multi-Domain Service Coordinator to Provisioning Network
   Controllers Interface) in the ACTN architecture.

--- middle

# Introduction

TODO Complete the Introduction

   Multi-layer and multi-domain service assurance scenarios, based on the reference
   network described in section 2 of {{!I-D.ietf-teas-actn-poi-applicability}} and very relevant for Service
   Providers, are described in sections {{fault}}, {{performance}} and {{resiliency}}.

This document is focusing on service assurance for end-to-end L2VPN or L3VPN connectivity services setup over underlying transport optical paths that requires multi-layer coordination

   For each scenario, existing IETF YANG data models,
   identified in section {{yang}}, are analyzed with a particular
   focus on the MPI in the ACTN architecture.

   For each multi-layer scenario, the document analyzes how to use the
   interfaces and data models of the ACTN architecture.

   A summary of the gaps identified in this analysis is provided in
   {{conclusions}}.

   Understanding the level of standardization and the possible gaps will
   help assess the feasibility of integration between packet and optical
   DWDM domains (and optionally OTN layer) from an end-to-end multi-vendor
   service assurance perspective.

# Conventions and Definitions

## Terminology

TODO Terminology

{: #ref-architecture}

# Reference Network Architecture

This document analyses several scenarios for service assurance in Packet and
   Optical Integration (POI) in which ACTN hierarchy is deployed to
   control a multi-layer and multi-domain network with two optical
   domains and two packet domains, as shown in Figure 1 of {{!I-D.ietf-teas-actn-poi-applicability}}, which is copied in {{fig-ref-architecture}} below.

~~~~ ascii-art
{::include figures/reference-architecture.txt}
~~~~
{: #fig-ref-architecture title="Reference Network (copy of Figure 1 of RFC YYYY)"
artwork-name="reference-architecture.txt"}

EDITORS NOTE: Replace RFC YYYY with the RFC number of {{!I-D.ietf-teas-actn-poi-applicability}} once it has been published.

In general, service assurance involves fault detection and localization; performance monitoring as well as re-routing (protection).

Two cases will be considered:

1. using grey interfaces on routers' ports, as outlined in {{!I-D.ietf-teas-actn-poi-applicability}}

2. using colored optical interfaces on routers' ports, as outlined in {{?I-D.mix-teas-actn-poi-extension}}

NOTE: It is not fully clear how much commonalities there are in service assurance for these two cases. This draft will start addressing both cases. At a later stage it will be assessed whether it is worthwhile keeping everything in a single draft or to split into two drafts.

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
through the same mechanisms described in {{!I-D.ietf-teas-actn-poi-applicability}}.

TO DO - Complete the description of the pre-requisites of MDSC in the cases discussed.

The following list summarizes the main assumptions about how MDSC can handle the service assurance cases described in this document. Most of them have been already described in {{!I-D.ietf-teas-actn-poi-applicability}}

1. MDSC has acquired all the topology and status information of both the IP and optical layers.

2. MDSC is fully aware of any multi-layer connections between the IP and the optical layers. It is also
aware of the multi-domain interconnection links between different IP domains.

3. MDSC is aware of any topology or resource utilization change obtained in real time through coordination with the O/P-PNCs. This applies in the case of a fault or a maintenance activity involving either the IP or the DWDM layer.

4. MDSC coordinates the IP and DWDM protections and, as a result, the re-routing of traffic at both the IP and DWDM layer.

5. Before planned maintenance operation at the DWDM layer, MDSC instructs the P-PNC to move the affected IP traffic to an other link in an hitless way. This is done before the event takes place. MDSC also coordinates with P-PNC to revert
back the traffic on the original path when the maintenance event is concluded.

6. When the O-PNC detects a degradation of optical performance (e.g. BER PRE-FEC values threshold crossing over
a certain period of time), it alerts the MDSC so that the MDSC relates the warning to an IP link.

7. MDSC distinguishes between IP and Optical failures. For example, in the case of the failure of an IP port of a router,
the IP traffic may be switched to a stand-by port, reusing the same ROADM optical resources (lambda, optical path) and keeping the end-to-end IP connection. If a remote IP node fails, then a re-route of optical resources takes place together with a switch of the local IP port in order to establish a new connection with a different IP node used for protection.

## Reference Network

TODO Add text from PR #10

{: #yang}

# YANG Data Models for the MPIs

TODO YANG Data Models

Initial set of YANG models that are potentially in the scope of this analysis:

- ietf-alarms defined in {{!RFC8632}}

- ietf-performance-monitoring defined in {{!I-D.yu-performance-monitoring-yang}}

{: #fault}
[]: # (Comment by Paolo - The following is a new section)

{: #pre-reqs}

# Pre-requirements for multi-layer coordination

The coordination of both the IP and the optical layer in the cases discussed in {{optical-network}} and {{edge}}
requires the MDSC to be aware of some network capabilities and to exchange the corresponding information with
both the P-PNC and the O-PNC.
To achieve maximum flexibility, a network operator may enable or disable these capabilities. 
Once the network operator has configured the capabilities described in this section, the MDSC exchanges
the relevant configuration with the PNCs present in the network before the use cases described in in {{optical-network}} and {{edge}}
take place.

The list of parameters that the MDSC may need to communicate to the PNCs includes:
- IP service reversion: on/off
- Optical service reversion: on/off   
- Hold-off time: time in ms (0 for immediate fast re-routing)
- Wait time before reversion: time in s
- Recovery method used in the optical layer: protection/restoration

{: #ref-network}

## Reference Network  

The following network topology will be considered to analyze and discuss the scenarios in in {{optical-network}} and {{edge}}.

~~~~ ascii-art
{::include figures/reference-network.txt}
~~~~
{: #fig-ref-network title="Reference Network"
artwork-name="reference-network.txt"}

EDITORS NOTE: Need to translate the picture into Ascii art!!!.

The network consists of three Points of Presence (POPs) geographically distributed. 
It is assumed that every POP hosts a Router (R1, R2, and R3 respectively) connected to a ROADM (ROADM1, ROADM2, and ROADM3).
All the routers connect to their co-located ROADMs with two Ethernet links (e.g. 100GE) for redundancy. 
In their normal operations, the routers may employ any local policy for traffic steering. For the scope of this document,
it is assumed that the path that R1 uses to steer the IP traffic to R2 goes from port P1 of R1 to port P1 of R2
(thus going through port P1 of R1, ports P1 and P3 of ROADM1, ports P3 and P1 of ROADM2, port P1 of R2).
R1 uses port P2 to steer the traffic to R3 instead.
Two distinct paths are configured on the link between R1 and R3. The first one carries the IP services that are
steered by R3 to any destinations with the exception of R2. The second path is a detour path chosen by R1 as a backup
path to reach R2 if a failure occurs in the primary path (across ROADM1 and ROADM2). 
The detour path also includes a second leg from R3 to R2. The detour path from R1 to R2, then includes: port P2 of R1, ports 
P2 and P4 or ROADM1, ports P3 and P1 of ROADM3, ports P1 and P2 of R3, ports P2 and P4 of ROADM3, ports P4 and P2 of ROADM2,
and port P2 of R2.
The connection between ROADM1 and ROADM2 is based on two fibers, each carrying one or more lambdas. 
For the scope of this document, it is assumed that some coordination mechanisms are employed at the optical layer so that
when a failure happens on the upper fiber (connecting port P3 of ROADM1 to port P3 of ROADM2), an optical backup path
is activated onto the lower fiber (P5 to P5). 
The mechanisms are assumed to be coordinated by O-PNC and MDSC, even if other methods may be also
considered (e.g. G-MPLS based). Further details are given in the use cases described in sections {{optical-network}} and {{edge}}.

{: #ref-hitless-reversion}

## Multi-layer hitless reversion

In some cases, the mechanisms employed by the optical layer to revert to the original setup may cause disruption 
at the IP layer, if proper coordination is not enabled. As this may cause traffic loss, if the optical reversion 
is requested by the network operator, multi-layer coordination under the supervision of the MDSC is necessary.
The effect of multi-layer coordination is to bring the whole network, i.e. both the IP and the optical layers, 
back to their initial configuration after the recovery from a failure. In particular, the process described in this section
relys on the hitless switching capability of the IP layer. 
Depending on the specific configuration, the procedure can be enabled at the end of the use cases described in sections {{optical-network}} and {{edge}}.
The decision whether to apply it or not has to be evaluated by the network operator considering different factors, 
including the relative complexity of the process and the effects of its steps on the live traffic. 

To move back to the initial network configuration the MDSC has to follow a sequence of steps:
- Force the IP layer to switch the traffic flow(s) on another path, e.g. an alternative/backup path
- Trigger the optical layer to coordinate the reversion to the initial setup, e.g. disable an optical backup path 
and enable connectivity on the previously used primary path
- Force again the IP layer to switch back to the original path.
The actions on the IP layer are handled so that the IP traffic is switched only after the interface queues are emptied, 
guaranteeing a hitless switching.
The mimics of the steps requested is shown in the next figure.

~~~~ ascii-art
{::include figures/hitless-multi-layer-reversion.txt}
~~~~
{: #fig-ref-architecture title="hitless multi-layer reversion"
artwork-name="hitless-multi-layer-reversion.txt"}

Figure 5.2 Diagram for hitless multi-layer reversion

The steps illustrated in the previous figure are detailed here:
1. ROADM1 detects the optical signal is up again on the previously broken fiber and notifies O-PNC
2. O-PNC notifies MDSC of the fiber up event
3. MDSC requires P-PNC to move the affected IP service(s) to an alternative/backup path (this path may vary according to the scenarios explained later). Being a hitless switch, it is necessary to avoid loss of service
4. P-PNC signals R1 to switch the IP service(s) to the alternative/backup path
5. R1 switches the service(s) to the alternative/backup path and notifies P-PNC
6. P-PNC confirms the switch to MDSC
7. MDSC instructs O-PNC to disable the optical protection path (which may vary according to the scenarios detailed later) and activate again the optical primary path
8. O-PNC instructs both ROADM1 and ROADM2 to disable the optical protection path and activate the primary one
9. ROADM1 and ROADM2 acknowledge to O-PNC
10. O-PNC acknowledges to MDSC
11. MDSC requires P-PNC to revert the IP service(s) back to the primary path
12. P-PNC signals R1 to switch the IP service(s) to primary path
13. R1 switches and acknowledges to P-PNC
14. P-PNC acknowledges to MDSC.

{: #optical-network}

# Multi-layer Fault Management

{: #optical-fault}

## Optical Network Failures

This use case is characterized by a fault happening on the upper fiber connecting ROAMD1 and ROADM2 
(port P3 to port P3 as depicted in {{fig-ref-network}}), affecting the IP traffic between R1 and R2.
As a result, the MDSC and the domain controllers cooperate to find a backup path for the IP traffic.
If the optical layer does not employ any mechanisms, the case is typically solved through the Fast Rerouting
Mechanisms (FRR) enabled by the IP/MPLS control plane. With reference to figure {{fig-ref-network}}, this corresponds
to using the combination of the two detour paths R1-R3 and R3-R2.
For the scope of this document, the assumption is instead that the optical layer supports its own mechansims that have
to interact with the IP layer. Two sub-cases are possible:
1. The optical layer supports restoration
2. The optical layer supports protection.

{: #restoration}

### Optical restoration

As restoration typically sets an alternative path on the fly based on the availability of sufficient optical resources,
the time taken by the process to create an optical backup tends to be longer than the time taken by the IP/MPLS FRR process.
As a result, the interaction between the two layers follows the mimics shown in the next figure.

~~~~ ascii-art
{::include figures/restoration.txt}
~~~~
{: #fig-fault-restoration title="Fault detection with optical restoration"
artwork-name="restoration.txt"}

More in details:
1a. The fault on the optical path (e.g. fiber cut, loss of signal, etc.) is detected by ROADM1 and notified to O-PNC
2a. O-PNC notifies the fault to MDSC
1b. R1 detects loss of end-to-end connectivity (e.g. 3 missed BFD messages) and notifies P-PNC. This step takes place almost simultaneously to 1a.
2b. P-PNC notifies the issue to MDSC
3.  R1 starts a fast reroute process to enable a backup path at the IP/MPLS layer, using the already established detour through R3
4.  R1 notifies P-PNC of the IP service switch through the alternate path (R1-R3 and R3-R2)
5.  P-PNC notifies MDSC of the switch
6.  ROADM1 and ROADM2 enable the restoration process. Based on the mechanism adopted, there may be intecaction between them
7.  Both ROADM1 and ROADM2 notify O-PNC of the availability of an optical backup path
8.  O-PNC notifies MDSC of the availability of an optical backup path
9.  R1 detects again end-to-end connectivity through the initial path R1-R2 and, if configured to do so, revert the service
10. R1 notifies P-PNC of the switch to the initial path
11. P-PNC notifies the switch to MDSC.

As noted in step 6., the restoration process may require an exchange of messages between ROADM1 and ROADM2.
This is not detailed in the present document as it is assumed that the relevant signaling is handled through O-PNC.

In step 9., R1 detects again control traffic from R2. The decision whether to revert the service on the initial path
is local, e.g. it depends on the configuration made by the network operator.
Often, the IP equipment is configured to operate the reversion automatically, but there are cases where the network
operator may prefer differently.

At the end of the process, multi-layer hitless reversion may take place, again based on the configuration adopted by the 
network operator. If multi-layer hitless reversion is adopted, then the process described in {{: #ref-hitless-reversion}}
takes place.

{: #protection}

### Optical protection

Differently from the previous case, here optical protection is considered. This duration of this process is comparable
with IP/MPLS FRR, as it is pre-computed. As a consequence, when multi-layer coordination is enabled it is preferrable
to hold-off FRR on R1 and wait that optical protection is completed.
The process is shown in the next figure.

~~~~ ascii-art
{::include figures/protection.txt}
~~~~
{: #fig-fault-protection title="Fault detection with optical protection"
artwork-name="protection.txt"}

The detailed process includes the following steps:
1a. The fault on the optical path (e.g. fiber cut, loss of signal, etc.) is detected by ROADM1 and notified to O-PNC
2a. O-PNC notifies the fault to MDSC
1b. R1 detects loss of end-to-end connectivity (e.g. 3 missed BFD messages) and notifies P-PNC. This step takes place almost simultaneously to 1a.
2b. P-PNC notifies the issue to MDSC [Editor's note: is this step necessary?]
3.  R1 is configured to hold the FRR process, thus it waits for the corresponding value set by the hold-off time parameter
4.  Optical protection is started by ROADM1, potentially involving an exchange of messages with O-PNC and ROADM2
5.  Both ROADM1 and ROADM2 notify O-PNC of the availability of an optical backup path
6.  O-PNC notifies MDSC of the availability of an optical backup path
7.  R1 detects again end-to-end connectivity with R2 and resumes normal IP traffic steering.

As in the previous use case, when the failure is fixed the network operator may desire to bring the service back
to the original configuration. If this is the case, multi-layer hitless reversion, as described
in {{: #ref-hitless-reversion}}, takes place to move the service back to the initial network setup.

{: #edge-fault}

## Cross-layer Link Failures

TODO Describe the mechanisms to detect when the failure occurs on a router port connected with the optical domain: see for example the fault scenarios in https://github.com/italobusi/draft-poidt-teas-actn-poi-assurance/files/10885907/2023.03.draft-poidt-teas-poi-assurance.pptx (slide 5)

{: #router-fault}

## Router Node Failures

TODO Describe the mechanisms to detect when the failure occurs on a node connected with the optical domain: see for example the fault scenarios in https://github.com/italobusi/draft-poidt-teas-actn-poi-assurance/files/10885907/2023.03.draft-poidt-teas-poi-assurance.pptx (slide 6)

{: #performance}

# Multi-layer Performance Management

TODO Describe performance monitoring and performance degradation detection performed by the O-PNC and how this information is reported to the MDSC: see for example the degradation scenario in https://github.com/italobusi/draft-poidt-teas-actn-poi-assurance/files/10885907/2023.03.draft-poidt-teas-poi-assurance.pptx (slide 7)

{: #resiliency}

# Multi-layer Resiliency

{: #optical-resiliency}

## Optical Network Failures

Failures in the optical domain can be recovered by packet-based protection mechanisms as described in {{!I-D.ietf-teas-actn-poi-applicability}}.

TODO Describe how the MDSC coordinates the protection switching mechanisms at the IP layer (e.g., FRR) and at optical layer, including the reversion when the failure is repaired: see for example the protection switching scenario in https://github.com/italobusi/draft-poidt-teas-actn-poi-assurance/files/10885907/2023.03.draft-poidt-teas-poi-assurance.pptx (slide 3)

{: #optical-maintenance}

## Optical Network Maintenance

TODO Describe how the MDSC initiates protection switching at the IP layer (e.g., FRR) and at optical layer at the beginning of a maintenance window, including the reversion after the maintenance operations are completed: see for example the maintenance scenario in https://github.com/italobusi/draft-poidt-teas-actn-poi-assurance/files/10885907/2023.03.draft-poidt-teas-poi-assurance.pptx (slide 4)

{: #edge-resiliency}

## Cross-layer Link Failures

TODO Describe the mechanisms to protect the traffic  when the failure occurs on a router port connected with the optical domain: see for example the protection scenarios in https://github.com/italobusi/draft-poidt-teas-actn-poi-assurance/files/10885907/2023.03.draft-poidt-teas-poi-assurance.pptx (slide 5)

{: #ref-hitless-reversion}

## Multi-layer hitless reversion

{: #router-resiliency}

## Router Node Failures

TODO Describe the mechanisms to protect the traffic  when the failure occurs on a router node connected with the optical domain: see for example the protection scenarios in https://github.com/italobusi/draft-poidt-teas-actn-poi-assurance/files/10885907/2023.03.draft-poidt-teas-poi-assurance.pptx (slide 6)

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
