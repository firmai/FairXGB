# FairXGB
Fair eXplainable Gradient Boosting Method that combines XGBMs and fairdata. This work heavily rely on work by H20.ai. 

By combining interpretable models, post-hoc explanations, discrimination testing, and data input and output adjustments with accessible software tools, this project aims to provide a template workflow for important ML applications that require high accuracy and interpretability and that mitigate risks of discrimination. Do not get put off by the lingo, everything is intuitive and would make sense as you work through this protocol. 

This manuscript outlines a viable approach for training and evaluating machine learning (ML) systems for high-stakes, human-centered, or regulated applications using common Python programming tools.

For maximum transparency and the potential generation of personalized adverse action notices, the constrained models are analyzed using post-hoc explanation techniques using global and local Shapley feature importance.

For now the benefit of partial dependence (PD) and individual conditional expectation (ICE) are somewhat disputed. The only additional information they provide is to veerify the montononicity constraint.

The constrained model predictions are also tested for disparate impact (DI) and other types of discrimination using measures with long-standing legal precedents, adverse impact ratio (AIR), marginal effect (ME), and standardized mean difference (SMD), along with straightforward group fairness measures. A functionality has been created to automate this step, to allow a broad spectrum of metrics. 

Post-hoc - correlations become more important with enforced montononicity constraints. Which makes the correlation corrector all the more viable. 


