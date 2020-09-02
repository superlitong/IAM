# Charter Proposal for a AOD WG, Version 0.1

## Background

ACK机制的多样化需求.
Data delivery between endpoints depends on backward signaling such as acknowledgements(ACK) for transport control.

At the same time, robustness of changes to protocols relies heavily on extensive unit and end-to-end testing. Not as memory-constrained as the kernel and not limited by the kernel API, the user-space development allows for extensive logging and debugging, opening oppotunities for newly proposed acknowledgement mechanism. High deployment velocity allows deploying various on-demand acknowledgement mechanisms with further modifications to the whole protocol stack. 

## AOD

AOD (Acknowledgement On Demand) attempts to revisit the backward signaling, seeking the optimal acknowledgement mechanism where the ACKs are exactly required by the transport. 

Goals and non-goals.

The functions to be considered by AOD include:

* Trigger conditions of ACKs:  

* Definitions of information carried in ACKs: 

* Interaction with round-trip timing:  

* Interaction with loss recovery:

* Interaction with congestion control:

AOD can be deployed in both  .

## Relationship to Other WGs and RGs

The working group will actively consult ICCRG for congestion control issues, and coordinate its progress with the TCPM and QUIC working groups to ensure that we are fulfilling the needs of these constituencies.

## Milestones

A "problems and opportunities" document will be adopted as the basis of this work. Then an AOD specification will be adopted as the main deliverable.

* AOD problems and opportunities, WG document adopted, January 2021
* AOD specification, WG document(s) adopted, February 2021
* AOD specification, PS to IESG, February 2022
