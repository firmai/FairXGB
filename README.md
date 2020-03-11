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

Fitting a model and having a high accuracy is great, but is usually not enough. Quite often, we also want a model to be simple and interpretable. An example of such an interpretable model is a linear regression, for which the fitted coefficient of a variable means holding other variables as fixed, how the response variable changes with respect to the predictor. For a linear regression, this relationship is also monotonic: the fitted coefficient is either positive or negative.

Beyond Linear Models

It is possible, at least approximately, to force the model monotonicity constraint in a non-linear model as well. For a tree-based model, if for each split of a particular variable we require the right daughter node’s average value to be higher than the left daughter node (otherwise the split will not be made), then approximately this predictor’s relationship with the dependent variable is monotonically increasing; and vise versa.


We can also check the relationship between the feature (median income) and the dependent variable (median house value)- This in a nutshell is partial dependence. 

Can you rerun a model and it will give you similar results.  This is not always the case for deeplearning methods. 


XNN - Explainable NN might perform, better on often does on large tabular data sets, but the interpretability is still somehwat hidden. When it does outperform on smaller datasets, it is probabably due to This is at least partially due to the preprocessing required to
present directly comparable post-hoc explainability results and to use neural networks and TensorFlow,
e.g., numerical encoding of categorical features and missing values. This preprocessing appears to
hamstring some of the tree-based models’ inherent capabilities.

You will have to instroduce your own interactions if you want them to exists - Of course, the monotonicity constraints themselves could have dampened the effects of
non-monotonic interactions under gMGBM, even if they did exist in the training data (e.g., LTV ratio
and the no introductory rate period flag, see Figure 6). This rigidity could also have played a role
in the performance differences between gMGBM(X) and gXNN(X) in the mortgage data not observed
for the simulated data, wherein strong interactions appeared to be between features with the same

Interesting -  it has a name  High system complexity is sometimes considered a mitigating influence as well [60]. This is
sometimes known as the transparency paradox in data privacy and security, and it likely applies to
ML security as well, especially in the context of interpretable ML models and post-hoc explanation
(see The AI Transparency Paradox).) Practitioners should of course consider the discussed interpretable
modeling, post-hoc explanation, and discrimination testing approaches as at least partial remedies to
the black-box and discrimination issues in ML. However, they should also consider that explanations
can ease model stealing, data extraction, and membership inference attacks, and that explanations
can mask ML discrimination.


The US HMDA law, originally enacted in 1975, requires many financial institutions that originate
mortgage products to provide certain loan-level data about many types of mortgage-related products
on an annual basis. This information is first provided to the CFPB, which subsequently releases some
of the data to the public. Regulators often use HMDA data to, “... show whether lenders are serving
the housing needs of their communities; they give public officials information that helps them make
decisions and policies; and they shed light on lending patterns that could be discriminatory” (see
Mortgage data (HMDA)). In addition to regulatory use, public advocacy groups use these data for
similar purposes, and the lenders themselves use the data to benchmark their community outreach
relative to their peers. The publicly available data that the CFPB releases includes information such as
the lender, the type of loan, loan amount, LTV ratio, DTI ratio, and other important financial descriptors.
The data also include information on each borrower and co-borrower’s race, ethnicity, gender, and
age. Because the data includes information on these protected class characteristics, certain measures
that can be indicative of discrimination in lending can be calculated directly using the HDMA data.
Ultimately, the HMDA data represent the most comprehensive source of data on highly-regulated
Information 2020, 11, 137 20 of 32
mortgage lending that is publicly available, which makes it an ideal dataset to use for the types of
analyses set forth in Sections 2 and 3.






