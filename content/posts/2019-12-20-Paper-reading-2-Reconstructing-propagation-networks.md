+++
title = "Reconstructing propagation networks with natural diversity and identifying hidden sources"
date = "2019-12-20"
tags = [
    "notes"
]
+++


Some notes about a paper.
<!--more-->

[Source](https://www.nature.com/articles/ncomms5323)

## Summary
This paper aims to reconstruct the networks hosting the spreading process and identify the source of spreading using limited measurements. The ultimate goal in the study of complex systems is to devise practically implementable strategies to control the collective dynamics. 

A main purpose of this work is to identify the key individuals in the network to implement target control and to locate the source of infection to isolate it so as to prevent recurrent infection in the future. 

The framework in the paper is based on Compressed Sensing Theory (CST) .

They give details on 1) Reconstructing networks and infection and recovery rates, 2) locating the hidden source of propagation. 


## Challenging in terms of content
A great challenge is that the network structure and the nodal dynamics are often unknown but only limited measured time series are available. 

It (reconstruct the networks hosting the spreading process and identify the source of spreading using limited measurements) is especially challenging due to (1)  difficulty in predicting and monitoring mutations of deadly virus  and (2) absence of epidemic threshold in heterogeneous  networks.

Another significant challenge in reconstructing a spreading network lies in the nature of the available time series: they are polarized, despite stochastic spreading among nodes. 

if no immediate information about the diffusion is available, the tree-structure-based inference method is inapplicable, and the problem of network reconstruction and locating the source becomes extremely challenging, hindering control of diffusion and delivery of immunization. 




## Originality of the topic
Employ two prototypical models of epidemic spreading: classic susceptible- infected-susceptible (SIS) dynamics and contact processes (CPs), on both model and real-world (empirical) networks. 

## Innovative scientific elements
None.

## Aimed at building up a new line of research
Our approach opens up a new avenue towards fully addressing the inverse problem in complex stochastic systems in a highly efficient manner 

## Potential to make important contributions to science
The main accomplishment of this work is then the development of a scheme to implement the highly non-trivial transformation associated with the spreading dynamics in the paradigm of CST (compressed sensing theory )

## Effective in terms of proposed methodology
Authors provide a detailed table to show the effectivity of their method.

## International importance of the proposed research area
None.

## Constraints
This work raises a number of questions to further and perfect the theoretical and algorithmic development of reconstructing complex dynamical systems. 
* For example, if partial knowledge about the network structure is available, the information can be incorporated into our framework to further reduce the required data amount. 
* Moreover, for non-Markovian spreading processes, our current reconstruction framework may fail. This raises the need to develop new and more general approaches. 



## Others
Our approach *opens up a new avenue* towards fully addressing the inverse problem in complex stochastic systems in a highly efficient manner 

*Taken together*, our results provide strong credence to the proposition that complex networks can be fully decrypted from measurements, 

*The key to* success of our method *lies in* our development of a novel class of transformation, allowing the network inference problem to be converted to the problem of sparse signal reconstruction, which can then be solved by the standard compressed-sensing algorithm. 

*Without loss of generality*, we employ two prototypical models of epidemic spreading 

In this case, identifying the source of rumour is important, a problem that our framework *is capable of solving*. 


