---
title: "Mencius: Building Efficient Replicated State Machines for WANs"
date: 2022-07-26T11:39:00+04:00
draft: false
tags: [paxos]
---
- [Problem](#problem)
- [Solution](#solution)
- [Contributions](#contributions)
- [Discussion of Evaluations](#discussion-of-evaluations)
- [Notes](#notes)
- [References](#references)
## Problem

Paxos relies on a single leader to choose the request sequence which is a bottleneck limiting the throughput(*Computational bottleneck at the leader)*. Moreover, having a single leader leads to an unbalanced communication pattern limiting the full utilization of bandwidth(*Unbalanced communication pattern*). The leader always learn and commits the value it proposed, but it takes time for non-leader nodes to learn the committed value resulting in *higher learning latency for non-leader servers*.

Other multi-leader solutions as Fast Paxos and CoReFP suffer from lower throughput under high load since they have more complex messaging.

## Solution

**Mencius** is proposed as a multi-leader state machine replication protocol deriving from Paxos. Its design is aimed at high throughput under high client load and low latency under low client load. 

The basic approach is to divide the protocol instances among the servers. Like, if we have 3 servers acting in the system, server 0 will lead 0,3,6,…; server 1 will lead 1,4,7..; and server 2 will lead 2,5,8… This partitioning will amortize the load among servers equally and increase the throughput when the system is CPU-bound. When the workload is network-bound, this scheme fully utilizes the available network bandwidth. Latency is also reduced, since clients can use a local server for their requests.

## Contributions

3 types of messages are used:

- **Suggest:** the coordinator suggests a request *v* by sending *PROPOSE* messages in round *r*. *PROPOSE* messages are called *SUGGEST* messages.
- **Skip:** the coordinator skips its turn by sending *PROPOSE* messages that propose *no-op* in round *r.*
- **Revoke:**  **when suspecting that the coordinator has failed, some server will eventually arise as the new leader and revoke the right of the coordinator to propose.

Each server maintains its next simple consensus sequence number, and updates after sending suggest message. Slow servers skip their turns, not to make fast severs wait for them. When a server suspected to be failed, its range will be revoked. 

Commutative requests can be committed out of order to increase the concurrency.

## Discussion of Evaluations

- Mencius achieve higher throughput under both CPU-bound and network-bound workload. It also fully utilizes available bandwidth and adapts to bandwidth changes.
- Mencius temporarily stalls when any of the server fails, but Paxos stalls only when the leader fails. The throughput of Mencius declines in case of failed server, but in case of Paxos it doesn’t change since all available bandwidth isn’t used.
- As the number of participant servers increases the throughput of Mencius is increased, but the throughput of Paxos is decreased.
- Mencius has lower latency, moreover its out-of-order commit further decreases latency.

## Notes

Explore the DETER testbed to see whether we can use it or not. 

T. Benzel, R. Braden, D. Kim, et al. Design, deployment, and use
of the DETER testbed. In Proceedings of the DETER Community
Workshop on Cyber-Security and Test., Aug 2007.

## References

[](https://www.usenix.org/legacy/events/osdi08/tech/full_papers/mao/mao.pdf)