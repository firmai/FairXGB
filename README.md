# FairXGB
Fair eXplainable Gradient Boosting Method that combines XGBMs and fairdata. This work heavily rely on work by H20.ai. 

By combining interpretable models, post-hoc explanations, discrimination testing, and data input and output adjustments with accessible software tools, this project aims to provide a template workflow for important ML applications that require high accuracy and interpretability and that mitigate risks of discrimination. Do not get put off by the lingo, everything is intuitive and would make sense as you work through this protocol. 

This manuscript outlines a viable approach for training and evaluating machine learning (ML) systems for high-stakes, human-centered, or regulated applications using common Python programming tools.

For maximum transparency and the potential generation of personalized adverse action notices, the constrained models are analyzed using post-hoc explanation techniques using global and local Shapley feature importance.

For now the benefit of partial dependence (PD) and individual conditional expectation (ICE) are somewhat disputed. The only additional information they provide is to veerify the montononicity constraint.

The constrained model predictions are also tested for disparate impact (DI) and other types of discrimination using measures with long-standing legal precedents, adverse impact ratio (AIR), marginal effect (ME), and standardized mean difference (SMD), along with straightforward group fairness measures. A functionality has been created to automate this step, to allow a broad spectrum of metrics. 

Post-hoc - correlations become more important with enforced montononicity constraints (mc). Which makes the correlation corrector all the more viable. 



Light G-Boost Encoding

First, I would like to briefly present Light-GBM (Light Gradient Boosting).
What is Gradient Boosting?

It is a boosting algorithm in which the loss is minimized using Gradient Descent method. And, by boosting we mean combining a set of weak learners to form a strong rule. It is an iterative process.
Why is it Light?

Light GBM is a fast, distributed, high-performance gradient boosting framework. Unlike other boosting algorithms it splits the trees leafwise and not level wise. LGBM runs very fast, hence the word “Light”.


Categorical feature support:

LightGBM can use categorical feature directly (without one-hot or label encoding). It has a unique way to deal with categorical variables. For our purposes one-hot encoding is a ncessity.

LGBM applies Fisher’s method to find the optimal split over categories.

We often represent categorical variables with one-hot encoding, but the optimal solution is to split on a categorical feature by partitioning its categories into 2 subsets.
If the feature has k categories, there are 2^(k-1)-1 possible partitions. Then we need to find the optimal partition.

LightGBM implements Exclusive Feature Bundling (EFB) technique, which is based on research by (D. Fisher, 1958) to find the optimal split over categories.

