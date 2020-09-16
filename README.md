# Charter Proposal for an IAM side meeting, Version 0.3

## Background

Data delivery between endpoints depends on backward signaling such as acknowledgements(ACK) for transport control. Acknowledgement mechanism is a common module for various transport protocols such as TCP and QUIC. In order to meet the diversified needs of heterogeneous network environment and a diverse set of applications, the frequency of ACKs should be dynamically adjusted in a network where the overhead of ACKs is non-negligible (e.g., limited available backward path capacity or when a radio-resource management system has to track channel usage, or both). However, changing acknowledgement mechanism may have side effects on the original ACK-clocking algorithms on end hosts.

On the other hand, robustness of changes to protocols relies heavily on extensive unit and end-to-end testing. Not as memory-constrained as the kernel and not limited by the kernel API, the user-space development allows for extensive logging and debugging, opening oppotunities for newly proposed acknowledgement mechanism. High deployment velocity allows deploying various on-demand acknowledgement mechanisms with further modifications to the whole protocol stack. 

## IAM

IAM (Internet Acknowledgement Mechanism) attempts to revisit the backward signaling of the transport protocol, seeking the optimal acknowledgement mechanism where the ACKs are exactly required by the transport. Basically, the trigger conditions of ACKs and the information carried in ACKs will be specified according to network environment and applications. Also, IAM will focus on the definition of the division of labor between sender and receiver, allowing the overhead of ACKs and the efficiency of ACK-clocking algorithms (e.g., round-trip timing, loss recovery, and congestion control) to meet the transport requirements. 

Interaction with proxy-based solution such as TCP splitting is out of scope. Multiple-path backward signaling will not be specifically addressed and is left for future consideration.

The functions to be considered by IAM include:

* When to send ACKs: An ACK can be triggered by receiving data from the forward path in the unit of number of packets or bytes (condition 1), or be triggered by a timer at the receiver (condition 2). Initially, IAM will specify the number of packets or bytes and the time interval to be counted for each acknowledgement mechanism, and seek the optimal combination between the above two conditions and other event-based trigger conditions (e.g., packet loss, parameter update, and zero window notification). Also, the selection between negative ACK (NACK/NAK) and positive ACK will be included in order to speed up recovery when loss event occurs.

* What to carry in ACKs: In some cases (e.g., LTE), enlarging the size of ACKs will increase the backward traffic volume, cancelling out the benefit of reducing ACK frequency. However, the overhead introduced by increasing the size of ACK rather than increasing the number of ACKs can be negligible in other cases (e.g., WLAN). IAM will answer the question that what information should be carried in ACKs, and why it is necessary. In addition, ACK packet encapsulation and its extension to the legacy TCP/QUIC will be specified. In order to improve space utilization, mechanisms on information compression/decompression in ACKs will also be included. 

* Interaction with other protocol modules:
  
  * Interaction with transport state monitoring: Per-packet acknowledgement achieves ideal transport state monitoring. The initial focus will be on round-trip timing under varying ACK frequency. But a receiver-based estimation framework of transport state, which acts as input of the protocol's ACK-clocking algorithms, will be included in order to reduce the estimation biases introduced by changing ACK frequency.

  * Interaction with loss detection and recovery: The delay from a packet loss to the packet recovery is crucial to packet reassembling, and thus impacts transport performance. IAM will focus on timely loss detection on lossy forward path and robust feedback on bidirectionally lossy path.

  * Interaction with congestion control: Lowering ACK frequency results in burstiness. And probe of transport state requires modifications to the protocol stack. IAM will give the principle of modification to various types of congestion control algorithms.   

  * Interaction with flow control: Send window update requires ACKs to update the receive window. Lowering ACK frequency probably delays acknowledging packet receipts and reporting  receive window, resulting in feedback lags and wasting opportunity of sending data. IAM will probe into the ACK mechanism to remove this side effects.

* Test cases for evaluating IAM proposals: Performance evaluation of various ACK mechanisms and their corresponding advancements on protocol design can be conducted in a controlled environment. The test cases for evaluation will cover basic usage scenarios and will be described using a common structure, which allows for additional test cases to be added to those described herein to accommodate other transport requirements.  

## Relationship to Other WGs and RGs

IAM will actively consult ICCRG for congestion control issues, and coordinate its progress with the TCPM and QUIC working groups to ensure that we are fulfilling the needs of these constituencies.

## Milestones

A "problems and opportunities" document will be adopted as the basis of this work. Then an IAM specification will be adopted as the main deliverable.

