# Charter Proposal for a AOD WG, Version 0.1

## Background

Data delivery between endpoints depends on backward signaling such as acknowledgements(ACK) for transport control. In order to meet the diversified needs of heterogeneous network environment and a diverse set of applications, the frequency of ACKs should be dynamically adjusted in a network where the overhead of ACKs is non-negligible (e.g., limited available backward path capacity or when a radio-resource management system has to track channel usage, or both). However, changing acknowledgement mechanism may have side effects on the original ACK-clocking algorithms on end hosts.

On the other hand, robustness of changes to protocols relies heavily on extensive unit and end-to-end testing. Not as memory-constrained as the kernel and not limited by the kernel API, the user-space development allows for extensive logging and debugging, opening oppotunities for newly proposed acknowledgement mechanism. High deployment velocity allows deploying various on-demand acknowledgement mechanisms with further modifications to the whole protocol stack. 

## AOD

AOD (Acknowledgement On Demand) attempts to revisit the backward signaling of the transport protocol, seeking the optimal acknowledgement mechanism where the ACKs are exactly required by the transport. Basically, the trigger conditions of ACKs and the information carried in ACKs will be specified according to network environment and applications, which allows the overhead of ACKs and the efficiency of ACK-clocking algorithms (e.g., round-trip timing, loss recovery, and congestion control) to meet the transport requirements.

Interaction with proxy-based solution such as TCP splitting is out of scope. Multiple-path backward signaling will not be specifically addressed and is left for future consideration.

The functions to be considered by AOD include:

* Trigger conditions of ACKs: An ACK can be triggered by receiving data from the forward path in the unit of number of packets or bytes, or be triggered by a timer at the receiver. AOD will specify the number of packets or bytes and the time interval to be counted for each acknowledgement mechanism, and also seek the optimal combination between the above two conditions and other event-based triggered conditions (e.g., packet loss, parameter update, and zero window notification).

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
