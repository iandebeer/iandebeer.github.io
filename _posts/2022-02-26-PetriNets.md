---
layout: single
title:  "Petri Nets as a model for Describing Decentralized Applications (dApps)"
date:   2022-02-26 14:17:38 +0200
categories: web3 blockchain 
---

## Proposal

The core question that I am pursuing in this proposal is: How do you develop Decentralised Applications? 

Formally, a Petri Net is a state transition graph that maps Places (circles) to Transitions (rectangles) and Transitions to Places via Arcs (arrows).
It is well suited for describing the flow of discrete concurrent processes.

Petri Nets are more concise than other process flow descriptions (like UML or BPMN) in that they have an exact mathematical definition of their execution semantics, with a well-developed mathematical theory for process analysis. Bounded Petri Nets exhibits Categorical Semantics in the way that **concatenable processes as strict Monoidal categories** model Net computations [[1]](#1) [[2]](#2)

Because of its Markov property - states depend only on the current marking -  Stochastic Petri Nets are also used for validating and testing the Liveness, Boundedness and Reachability of distributed networks.

1. A business analyst should  create a dApp Protocol by joining Places (States) and Transitions with Arcs
2. Configuration of a specific instance of a dApp can be programmatically created or be informed by the UI connecting to the headless dApp through a GRPC/HTTP API
3. Smart Contract templates will allow reuse and create a possible market place of tested Contracts
4. Validation of dApp can be done in terms of Liveness, Boundedness and Reachability
5. Design patterns can be be implemented by a Petri Net:

![alt text](/assets/images/place_transitions.png "Arcs")

## As applied to the ErgPlatform

I believe we require a way to compose dApps from Ergo Boxes - Wallets, Smart Contracts and Transactions, much like Functional Programming allows you to compose applications from pure functions.


