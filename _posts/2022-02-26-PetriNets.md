---
layout: single
title:  "Petri Nets as a model for Describing Decentralized Applications (dApps)"
date:   2022-02-26 14:17:38 +0200
categories: web3 blockchain 
---

## Proposal

The core question that I am pursuing in this proposal is: How do you develop Decentralized Applications in a cost effective and resource effective manner?  

In category theory, a Petri net can be described as a directed bipartite graph with two types of nodes: places and transitions. The edges of the graph represent the flow of tokens between places and transitions.

A coloured Petri net is a variation of a Petri net in which the tokens are not just simple markers, but are instead labeled with a "colour" that represents some additional information about the token. For example, the colour could represent the type of a product being processed in a manufacturing system, or the state of a system being modeled.

In category theory, the places in a coloured Petri net can be thought of as objects, and the transitions can be thought of as morphisms between those objects. The flow of tokens between places and transitions can be thought of as the composition of morphisms. The colours of the tokens can be thought of as labels on the morphisms, representing additional structure or information about the flow of tokens.

Overall, a coloured Petri net can be seen as a way of modeling the flow of labeled tokens through a system, with the structure of the Petri net representing the relationships between the different places and transitions in the system.

Looking at it from a Functional Programming perspective, it looks like a case for composition of smart contracts as pure functions into higher order functions - dApps. Bounded Petri Nets exhibits Categorical Semantics in the way that **concatenable processes as strict Monoidal categories** model Net computations [[1]](#1) [[2]](#2)It is easy to see (if you are that way inclined) that Petri Nets form a Category of Petri. A _Coloured_ Petri Net is traversable using a state monad to step from an initial state to subsequent state.

In category theory, the colours of the transitions in a coloured Petri net can be represented by an additional layer of structure on the category, called a functor. This functor assigns to each transition in the category a colour in some fixed set of colours.

The objects in the category corresponding to a coloured Petri net are still the places in the net, and the morphisms are still the transitions. However, the transitions are now decorated with colours, which can be used to describe additional properties or constraints on their behavior.

For example, a coloured Petri net might be used to model a manufacturing process in which different types of resources (represented by different colours) are required for different types of operations (represented by the transitions). In this case, the functor representing the colours of the transitions could be used to enforce the requirement that certain transitions can only be performed if the necessary resources are available.

From the proposal perspective, Petri Nets are directed graphs consisting of Places(Stages), Transitions(Actions) and Arcs(Transaction). It models state-transitions of (concurrent) processes. I contend that there is a need to handle consecutive Smart Contract invocations (the dApp Protocol) within the context of a encapsulating state machine (FSM) as expressed by a Petri Net and executed by an off-chain dApp-container.

Because of it's Markov property - state transitions depend only on the currently available state.  In addition to main artifacts mentioned above, Petri Net execution relies on Markers and Tokens. The Marker indicates a requirement-gate that needs to be satisfied before the next transition can take place. For a given set of Tokens (current state) the PetriNet can be asked to step through to the next state (set of Tokens) as indicated by the Markers - guards - placed on the Arcs that join Places and Transitions.

![alt text](/assets/images/animate.gif "flow")

Stochastic Petri Nets are also used for validating and testing the Liveness, Boundedness and Reachability of distributed networks.

1. A business analyst should  create a dApp Protocol by joining Places (States) and Transitions with Arcs
2. Configuration of a specific instance of a dApp can be programmatically created or be informed by the UI connecting to the headless dApp through a GRPC/HTTP API
3. Smart Contract templates will allow reuse and create a possible market place of tested Contracts
4. Validation of dApp can be done in terms of Liveness, Boundedness and Reachability
5. Design patterns can be be implemented by a Petri Net:

![alt text](/assets/images/place_transitions.png "Arcs")

## As applied to the ErgPlatform

I believe we require a way to compose dApps from Ergo Boxes - Wallets, Smart Contracts and Transactions, much like Functional Programming allows you to compose applications from pure functions.

I wanted to test an intuition that the Categorical  (monoidal) aspects of Petri Nets lend itself to composing a dApp from the Boxes (Places) with guarding Contracts and  Transactions (Transitions).   I am basing this intuition on prior work I have done in creating an implementation of PetriNets (see https://github.com/iandebeer/castanet). It is a generalized implementation in Scala 3, developed with intent  to compose applications from Knative Services under Kubernetes.

As a starting point for ErgoHack, I used the "Heads or Tails Game" from the Ergoscript by Example repository (https://github.com/ergoplatform/ergoscript-by-example/blob/main/headsOrTails.md), to test the concept. I picked this example to render as a Petri Net because it has finite looping (5 plays) and forking and joining concepts. I want build this out so I can visualize this dApp, and then generalize the concept from there, to a point where one use it for dApp development by visualizing the stages, validating the flow, and running an instance of the dApp in the ErgoPlayground or through Appkit on the Ergo Blockchain.

I want to implement an Ergo-Castanet Client API over GRPC that will support:

```scala
val dAppID: String                = addDApp(flowSpec: org.ergoplatform.flow.spec.flowspec.FlowSpec)
val pngURL: URL                   = visualiseDApp(dAppID: String)
val animated_GIF_URL: URL         = validateDApp(dAppID: String ,markers: Seq(FlowMarkers)
val markerBitMap: Long            = excuteStepDApp(dAppID : String, markerBitMap: Long, transaction:ErgoTransaction)
```

Using the above API with the Head-or-Tails example I expect to visualize the dApp in the following Petri Net:

![Petri Net](/assets/images/Heads-Tails-Net.png)

 I created a project on GitHub: https://github.com/iandebeer/ergo-castanet.  The project depends on another open source project I published on GitHub https://github.com/iandebeer/castanet 
 I implemented a GRPC client/server using the Typelevel FS2-GRPC framework. The protobuf I pulled from https://github.com/ergoplatform/ergo-appkit/tree/develop/docs/design-contracts.

## As applied to the Cardano

## As applied to cross-chain dApp development
