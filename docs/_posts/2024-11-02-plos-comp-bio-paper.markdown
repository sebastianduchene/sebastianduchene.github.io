---
layout: post
title:  "Prior sensitivity in BETS"
date:   2024-11-02 18:06:47 +0200 
categories: BETS Bayesian phylogenetics prior sensitivity BEAST Research
---

By Sebastian Duchene

Our recent paper, _Assessing the effect of model specification and prior sensitivity on Bayesian tests of temporal signal_ ([Tay et al. 2024][manuscript-link]), has been recently accepted! We have updated the latest version in [PLoS Computational Biology][manuscript-link]. My PhD student, [John Tay][john-site] and I led this work in collaboration with [Arthur Kocher][arthur-site]. 

In this post, I will summarise the key findings, explain the implications for future studies, and suggest strategies to improve the assessment of temporal signal.

## Motivation
Temporal signal refers to the situation where the window of time over which sequences data have been collected is enough to calculate the evolutionary rate. In the presence of a perfect molecular clock wee expect molecular substitutions to accumulate roughly linearly over time, such that samples collected more recently have more substitutions than those collected earlier. Temporal signal is typically inspected using a root-to-tip regression (Figs 1). [Leo Featherstone][leo-site], who completed his PhD with me recently, developed a tool called Clockor2 for this purpose (see [Featherstone et al. 2023][clockor2-paper] and the link to software [here][clockor2-link]).

![image](https://github.com/sebastianduchene/sebastianduchene.github.io/blob/main/docs/assets/images/rtt1.png?raw=true)
**Fig 1** Root to tip regression conducted in TempEst based on tree in Fig 2.

This study built on previous work where we developed [BETS, Bayesian Evaluation of Temporal Signal (Duchene et al. 2020)][bets-paper] ([click here for a tutorial][bets-tutorial]). The goal of BETS is to determine whether incorporating sampling times improves that statistical fit of the full Bayesian phylogenetic model. Sampling times are a valuable source of information for calibrating the molecular clock, and thus understanding whether they can be reliably used is of great interest, particularly for recently evolving outbreaks or analyses involving ancient DNA.

The current study was motivated by our observations that the prior in Bayesian phylogenetics can impact model selection using Bayes factors and marginal likelihoods, even when it does not impact the posterior ([Tay et al. 2023][episodic-paper]). BETS treats the question of temporal signal as a model selection problem, and it uses Bayes factors and marginal likelihoods, and thus we thought it was important to assess its sensitivity to the choice of the prior. 

## Our results
We conducted simulation experiments and analyses of several empirical data sets of pathogens, some involving ancient samples. Empirical data are always interesting because they violate the assumptions of the models in many ways, but it is often difficult to pinpoint problems in our methods because we do not know the ground truth and we will often ignore all the ways they will violate the assumptions of the model. For these reasons I will focus on our simulation results. In summary:

1. BETS is very good at detecting temporal signal when it is indeed present (low type II error or low false negative rate).
2. When temporal signal is not present, Bayesian phylogenetic analyses tend to make phylogenetic trees implausibly old (I am talking many orders of magnitude) and incorrectly favour temporal signal (high type I error or high false positive rate). For an example, see Fig2 below.
3. The problem of incorrect detection of temporal signal can be mitigated by using a tree prior that does penalises trees that are implausibly old.

![image](https://github.com/sebastianduchene/sebastianduchene.github.io/blob/main/docs/assets/images/tree_distortion.png?raw=true)
**Fig 2** Tree extension in data with no temporal signal. The true tree is simulated under a strict molecular clock (SC) and under no temporal signal (isochronous), shown here on the left. The inclusion of sampling times (SC heterochronous) results in a tree that is 500 times older than the truth. A similar, but more extreme situation occurs when we analyse the data under a relaxed molecular clock (UCLD here, for uncorrelated log-normally distributed).

The reason for why phylogenetic trees inferred for data sets with not temporal signal are so old is probably a means of compensating for the likelihood penalty of including sampling times that should not be there. In a very old tree, the sampling window corresponds to a very small proportion of the total timescale, so that the trees with and without sampling times can indeed have very similiar likelihoods (Fig 3).

![image](https://github.com/sebastianduchene/sebastianduchene.github.io/blob/main/docs/assets/images/tree_likelihoods.png?raw=true)
**Fig 3** Tree likelihoods for different analysis treatments. The *y*-axis is the phylogenetic likelihood (probability of the sequence data given the model) and the *x* axis is the height of the root-node. The data were generated with no temporal signal, so the correct model is the isochronous. Note that including sampling times (heterochronous) results in much older trees with similar likelihoods as those with no dates. In contrast, when we impose a hard bound on the age of the root, the likelihood is much lower (purple symbols).

## Implications for future studies
Sampling form the prior (also known as prior predictive simulations) should become standard practice with Bayesian models. Doing so allows us to understand how the different parameters and their priors are interacting and ultimately what is the marginal prior on parameters of interest. Here, we did not use explicit priors on the ages of nodes, but the population size of the coalescent process, which we use as tree prior, implicitly places prior distributions on the ages of nodes. A prior that makes unreasonable assumptions can result in an implausible posterior and the impact in model selection is not trivial. Here we recommend verifying the prior on the age of the root, and on the molecular clock rate, both fundamental parameters for understanding temporal signal. 

Please read the paper for more details on how to set up analyses with no sampling times correctly and other aspects about prior predictive simulations, such as parameter nonidentifiability.



## References
Sebastian Duchene, Philippe Lemey, Tanja Stadler, Simon Y W Ho, David A Duchene, Vijaykrishna Dhanasekaran, Guy Baele, **Bayesian Evaluation of Temporal Signal in Measurably Evolving Populations**, Molecular Biology and Evolution, Volume 37, Issue 11, November 2020, Pages 3363–3379. doi: [https://doi.org/10.1093/molbev/msaa163][bets-paper]

Leo A Featherstone, Andrew Rambaut, Sebastian Duchene, Wytamma Wirth, **Clockor2: Inferring Global and Local Strict Molecular Clocks Using Root-to-Tip Regression**, Systematic Biology, Volume 73, Issue 3, May 2024, Pages 623–628, doi: [https://doi.org/10.1093/sysbio/syae003]

John H Tay, Arthur Kocher, Sebastian Duchene, **Assessing the effect of model specification and prior sensitivity on Bayesian tests of temporal signal**
PLoS Comput Biol 20(11): e1012371. doi: [https://doi.org/10.1101/2024.08.12.607579]




[leo-site]: https://scholar.google.com.au/citations?user=yC7e4MUAAAAJ&hl=en&oi=ao
[arthur-site]: https://scholar.google.com.au/citations?hl=en&user=wiunwsMAAAAJ
[john-site]: https://scholar.google.com.au/citations?user=tj_0skYAAAAJ&hl=en&oi=ao
[bets-tutorial]: https://beast.community/bets_tutorial
[bets-paper]: https://academic.oup.com/mbe/article/37/11/3363/5867920 
[manuscript-link]: https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1012371
[episodic-paper]: https://academic.oup.com/mbe/article/40/10/msad212/7280106?login=false
[clockor2-link]: https://clockor2.github.io/
[clockor2-paper]: https://academic.oup.com/sysbio/article/73/3/623/7609804
