---
layout: post
title:  "Prior sensitivity in BETS"
date:   2024-11-02 18:06:47 +0200 
categories: BETS Bayesian phylogenetics prior sensitivity BEAST
---

By Sebastian Duchene

Our recent preprint, _Assessing the effect of model specification and prior sensitivity on Bayesian tests of temporal signal_ ([Tay et al. 2024][manuscript-link]), has been recently accepted! We have updated the latest version in [_bioR$\chi$iv_][manuscript-link]. My PhD student, [John Tay][john-site] and I led this work in collaboration with [Arthur Kocher][arthur-site]. 

In this post, I will summarise the key findings, explain the implications for future studies, and suggest strategies to improve the assessment of temporal signal.

## Motivation
This study build on previous work, where we developed [BETS, Bayesian Evaluation of Temporal Signal (Duchene et al. 2020)][bets-paper] ([click here for a tutorial][bets-tutorial]). The goal of BETS is to determine whether incorporating sampling times improves that statistical fit of the full Bayesian phylogenetic model. Sampling times are a valuable source of information for calibrating the molecular clock, and thus understanding whether they can be reliably used is of great interest, particularly for recently evolving outbreaks or analyses involving ancient DNA.

The current study was motivated by our observations that the prior in Bayesian phylogenetics can impact model selection using Bayes factors and marginal likelihoods, even when it does not impact the posterior ([Tay et al. 2023][episodic-paper]). BETS treats the question of temporal signal as a model selection problem, and it uses Bayes factors and marginal likelihoods, such we thought it was important to assess its sensitivity to the choice of the prior. 

## Our results

## Implications for future studies




## References
John H Tay, Arthur Kocher, Sebastian Duchene, **Assessing the effect of model specification and prior sensitivity on Bayesian tests of temporal signal**
bioRxiv 2024.08.12.607579; doi: [https://doi.org/10.1101/2024.08.12.607579][manuscript-link]

Sebastian Duchene, Philippe Lemey, Tanja Stadler, Simon Y W Ho, David A Duchene, Vijaykrishna Dhanasekaran, Guy Baele, **Bayesian Evaluation of Temporal Signal in Measurably Evolving Populations**, Molecular Biology and Evolution, Volume 37, Issue 11, November 2020, Pages 3363–3379, [https://doi.org/10.1093/molbev/msaa163][bets-paper]


[arthur-site]: [https://scholar.google.com.au/citations?hl=en&user=wiunwsMAAAAJ]
[john-site]: https://scholar.google.com.au/citations?user=tj_0skYAAAAJ&hl=en&oi=ao
[bets-tutorial]: https://beast.community/bets_tutorial
[bets-paper]: https://academic.oup.com/mbe/article/37/11/3363/5867920 
[manuscript-link]: https://www.biorxiv.org/content/10.1101/2024.08.12.607579v2
[episodic-paper]: https://academic.oup.com/mbe/article/40/10/msad212/7280106?login=false