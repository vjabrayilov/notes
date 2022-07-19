---
title: "StoppablePaxos"
date: 2022-07-19T10:17:24+04:00
draft: false
tags: [consensus, paxos]
---
## Summary
Stoppable state machines are used to implement reconfiguration, simply a reconfigurable state machine consists of several stoppable state machines. To switch between the configurations, one is stopped and the other is started.

The same variables are used and the same messages are exchanged in case of Stoppable Paxos. It acts as ordinary Paxos till the *stp* command found to be chosen in some instance *i*. The leader will perform *Phase2a* actions for instances which are numbered *less than i*, but it will stop performing the same for instances *greater than i*. Simply, leader try to get *stp* chosen and does nothing for higher-numbered instances. 

