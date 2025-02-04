# Size-Curve-Problem
Size Curve Problem : Demand Estimation for Product Variants

Motivation : Retailers face a tricky problem when deciding how many units of each size to order for products like t-shirts (small, medium, large, extra-large, and so on).  Sales figures alone aren't a reliable guide to actual customer demand for a few key reasons.  First, if a particular size was out of stock at any point, the sales records will underestimate how many people actually wanted to buy it.  Second, what people want can change with the weather, the latest styles, or even where they live.  A sudden heatwave might boost demand for larger sizes of lightweight shirts, for example.  Finally, for a brand new product, there simply isn't enough sales history to accurately predict what sizes will be most popular.

Solution : To estimate true demand, we use Maximum Likelihood Estimation (MLE) to model the probability distribution of demand for each variant. The process involves the following steps:
1. Indexing Variants :
Each product variant (size) is assigned an index: S = 1, M = 2, L = 3, XL = 4
2. Pairwise Comparisons :
Instead of estimating demand for all sizes at once, we look at how each size compares to another when both were available at the same time.
3. Likelihood Function :
The likelihood function is a mathematical function that quantifies how well a given set of probabilities explains the observed data. In this case, we are interested in the demand probabilities.
We define p1, p2, p3, p4 as the demand probabilities for S, M, L, and XL (these sum to 1).
For each size (i,j) that are available at the same time, probability of selling i over variant j follows a Binomial Distribution. Why? The binomial distribution models the number of successful outcomes in a fixed number of trials, where each trial has two possible outcomes (success or failure) and a constant probability of success.
Binomial Function for this case would look like so:
$P(S_{i}|p)=\binom{n}{S_{i}}p_{i}^{S_{i}}p_{j}^{S_{j}}$
where:
$S_{i}$ = sales of size i,
$S_{j}$ = sales of size j,
$n = S_{i} + S_{j}$ Total sales when both sizes were available.
The likelihood function, as discussed above is represented as: $L(p)=\sum_{(i,j)\in \text{available pairs}}S_{i}\log p_{i}+S_{j}\log p_{j}$.
This function measures how well a set of probabilities explains the sales data. The goal is to find values of p1, p2, p3, p4 such that $L(p)$ is maximized.
4. Optimization : Gradient Descent
Since the likelihood function is complex, we use gradient descent, an optimization algorithm that iteratively adjusts the probabilities to maximize $L(p)$.
