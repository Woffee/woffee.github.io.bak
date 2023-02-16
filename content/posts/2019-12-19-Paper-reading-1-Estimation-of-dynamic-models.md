+++
title =  "Estimation of dynamic models with nonparametric simulated maximum likelihood"
date = "2019-12-19"
tags = [
    "notes"
]
+++


Some notes about a paper.
<!--more-->

[PDF](https://pages.wustl.edu/files/pages/imce/yshin/npsmle1.pdf)

## Summary
Authors propose an easy-to-implement simulated maximum likelihood estimator for dynamic models where no closed-form representation of the likelihood function is available.

For any given parameter value, conditioning on available past information, they draw N i.i.d. simulated observations from the model. They construct the likelihood and search over the parameter space to obtain a nonparametric simulated maximum likelihood estimator (NPSMLE). 

For the stationary case, they also analyze the impact of simulations on the bias and variance of the NPSMLE. NPSML can be used for estimating general classes of models, such as structural Markov decision processes and discretely-sampled diffusions.

For the classes of models that NPSML addresses, there are two categories of existing approaches. The first is based on moment matching, and includes simulated methods of moments,  indirect inference, and efficient methods of moments. The approaches in the second category approximate the likelihood function itself, and hence is more closely related to NPSML.

They prove that NPSMLE is consistent and asymptotically efficient. 

## Challenging in terms of content

* NPSML can be used for estimating general classes of models, but some of them may be dynamic programming problem. Hence does not typically have a closed-form representation.
* As for the estimation of continuous-time stochastic models with discretely sampled data, the transition densities are well-defined, but only in a few special cases can we derive closed-form expressions for them. 


## Originality of the topic
* The method can handle any simulable model without latent dynamics. 
* The method can be fully automated to yield full efficiency
* NPSML can handle nonstationary and time-inhomogeneous dynamics

Cons:
* only consider the cases where it is possible to simulate the dependent variable conditional on finitely-many past observations.

## Innovative scientific elements
* They investigate the performance of NPSML when applied to jump–diffusion models with particular attention to the impact of the number of simulations and bandwidth. Find that NPSML performs well even for a moderate number of simulations and that it is quite robust to the choice of bandwidth.
* They establish its asymptotic properties under fairly weak regularity conditions allowing for a wide range of different models. While other methods are designed only for specific classes of models.

## Aimed at building up a new line of research
I think this paper doesn’t build up a new line of research. Authors just propose an easy-to-implement simulated maximum likelihood estimator for dynamic models where no closed-form representation of the likelihood function is available.

## Potential to make important contributions to science
As said in Originality of the topic. This method has a strong applicability and can be used in more research scenarios.

## Effective in terms of proposed methodology
There exist many data-driven methods that guide the researcher in this regard such that their method can be fully automated to yield full efficiency

## International importance of the proposed research area
This point is not raised in the text. But I think such a widely applicable method will greatly promote research in related fields.

## Others
* At the practical level, when the model specification changes, only the part of the computer code that simulates observations needs to be modified, *leaving other parts* (e.g., kernel estimation of conditional density or numerical maximization of likelihood) unchanged.
* Extensions of our method that obtain full efficiency in the presence of latent dynamics are *worked out* in a companion paper (Brownlees et al., 2011), building on the main results obtained here.
* *The rest of the paper is organized as follows*. In the next section, we set up our framework to present the simulated conditional density and the associated NPSMLE.
* This method is applicable to general classes of models, and can be implemented *with ease*. 
* Find that NPSML performs well even for *a moderate number of* simulations and that it is quite robust to the choice of bandwidth.
