**SHAP (Shapely Additive Explanations)** is a game theoretic approach to explain the output of any machine learning model. It connects optimal credit allocation with local explainations using classic Shapley values from game theory and their related extensions.

Explaining Machine Learning Models with Shapely values. Shapely values are widely used approach from cooperative game theory. SHAP quantifies the importance of each feature in making predictions

An _**individual prediction**_ can be explained by assuming that each feature value of the instance is a player in a game where the prediction is the payout. Shapely values tells us how to fairly distribute the payout among the features.

$$
f(x) = E[f[X]] + sum(SHAP values)
$$

The output of SHAP is the dataset with same dimensions as that on which model was orginially trained. SHAP values reveals intersting insight into how the input variables are impacting the predictions of the machine learning model, both at the level of individual instances and across the population as whole.

SHAP can be applied to any machine learning model as a post hoc interpretation technique- i.e. it is applied after model training, and is agnostic towards the algorithm itself. That said , it is particularly efficient to compute SHAP for tree based models, such as random forests and gradient boosted trees.

Caution should be exercised when deriving insights from SHAP analysis. It is important not to become over-invested in conclusions that certain feature values _**cause**_ certain outcomes unless the experiment has been conducted within a causal framework (this is rarely the case). SHAP only tells you what the model is doing within context of the data on which it has been trained. it doesnt necessarily reveal the true relationship between variables and outcomes in the real world. Decision-makers are often tempted to view features in SHAP analyses as dials that can be manipulated to engineer specific outcomes.

> The _**game**_ is the prediction task for a single instance of the dataset. The _**gain**_ is the actual prediction for this instance minus the average prediction for all instances. The _**players**_ are the features values of the instance that collaborate to receive the gain(=predict a certain value).

Consider an example of linear regression. While coefficients are great for telling us what will happen when we change the value of an input feature, by themselves they are not a great way to measure the importance of a feature. This is because value of each coefficient depends upon the scale of input feature.

> if for example we were to measure the age of home in minutes instead of years, then the coefficient of the HouseAge feature would become $0.0115 /(360*24*60)$

This means the magnitude of a coefficient is not necessarily a good measure of a feature's importance in a linear model.

One of the most fundamental properties of SHAP values is they always sum up to difference between game outcome when all players are present and game outcome when no players are present. For machine learning models what this means is that SHAP values of all the input features will always sum up to the difference between baseline(exptected)model output and current model output for the prediction being explained.

_**The Shapley value is the average marginal contribution of a feature value across all possible coalitions.**_

Consider the problem of predicting house prices from the four features. `park-nearby`, `area-50`, `floor-2nd`, `cat-banned`. Let's evaluate the contribution of `cat-banned` feature value when it is added to coalition of `park-nearby` and `area-50`.  We simulate that only `park-nearyby`, `area-50`, and `cat-banned` are in a coalition by randomly drawing another apartment from the data and using its value for the floor feature. The floor `floor-2nd` was replaced by `floor-1st`. Then we predict the price of the apartment with this contribution ($310,000$). In a second step we remove `cat-banned` from the coalition by replacing it with random value of the cat allowed/banned feature from the randomly drawn apartment. In the example it was `cat-allowed`, but it could have been `cat-banned` again. We predict the apartment price for coalition of `park-nearby` and `area-50` ($320,000$). The contribution of `cat-banned` was $310,000$ - $320,000$ = $-10,000$. This estimate depends upon the values of the randomly drawn apartment that served as a "donor" for the cat and floor feature values. We will get better esitmates if we repeat this sampling step  and average the contributions.

**Procedure to get the Shapely value** For each of the coalitions we compute the predicted apartment price with and without the feature value `cat-banned` and take the difference to get the marginal contribution. The Shapely value is the (weighted) average of marginal contributions. We replace the feature values of features that are not in coalition with random feature values from the apartment dataset to get a prediction from the machine learning model.

One possible solution to keep the computation time manageable is to compute contributions for only a few samples of the possible coalitions.

We replace the feature values of features that are not in coalition with random feature values from the apartment dataset to get prediction from the machine learning model.

## Interpretability Using Shap
### Local Interpretability: explaining individual contribtutions
Explaining predictions for individual instances of the data is referred to as local interpretability.

#### Waterfall Plots
- Input variables are ranked from top to bottom by how much impact they have on the model's prediction for this example from the data.
- The shap values quantifies the amount and direction in which each variable impacts the predicted house price.
- SHAP values show in red arrows corresponds to input variables that push the model towards predicting higher price, whereas those in blue push the model towards a lower price.
- The final prediction is sum of base value + sum of shap value.
- The base value is same for all instances in the data.For regression problem it is the mean value of the target variable and for classification problem it is the probability of the positive class.

#### Force Plots

### Global Interpretability Understanding drivers for prediction across the population
#### Bar Plots