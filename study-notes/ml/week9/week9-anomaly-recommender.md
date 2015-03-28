# Coursera - Machine Learning - Week 9

## Anomaly Detection

### Problem Motivation
Manufacture of aircraft and measure features of the aircraft and found some features and the normal values for them. Suppose a new engine comes along and we want to know if it's working the same as the previous or not.

![Anomaly Detection Example](AnomalyDetectionExample.png)

If the X is outside the normal range, we assume it's an anomaly. Or we want to know if Xtext is anomalous.

**Formally:**

- Dataset: $ \{ x^{(1)}, x^{(2)},...,x^{(m)} \} $
- Is Xtest anomalous?
- Create a model for P(Xtest):<br>
If $ p(X_{test}) < \epsilon \rightarrow $ flag anomaly, otherse $  p(X_{test}) \ge \epsilon \rightarrow $ OK

Examples:

- Fraud detection
  - $X(i)$ = features of user $i$'s activities (forum posts, activities etc.)
  - Model $p(x)$ from data
  - Identify unusual users by checking which have $ p(x) < \epsilon $
- Manufacturing
- Monitoring computers in a data center
  - $X(i) = features of machine
  - X1 = memory use, x2 = number of disk access
  - X3 = CPU load
  - $ p(x) < \epsilon $ - machine has issues or about to go down

## Guassian (Normal) Distribution
Say $ x \in \mathbb{R} $, if $x$ is a distribution with mean $\mu$ and variance $\sigma^2$

![](GuassianDistribution1.png)

- $ x \sim \mathcal{N}(\mu,\sigma^2) $ - $\sim$ means distributed as.
- $ \mu $ - center of bell curve
- $ \sigma $ - the width of the curve or standard deviation
- $ \sigma^2 $ - called the variance
- $ \displaystyle p(x,\mu,\sigma^2) = \frac{1}{ \sigma \sqrt{2 \pi}} e^{\left(-\frac{{\left(\mu - x\right)}^{2}}{2 \, \sigma^{2}}\right)} $

![](GuassianDistribution2.png)

- The area under the curve always sums up to 1.

## Parameter estimation
- Dataset: $ \{ x^{(1)}, x^{(2)},...,x^{(m)} \}, X^{(i)} \in \mathbb{R} $
- And if I suspect they are guassian distribution - $ X \sim \mathcal{N}(\mu, \sigma^2) $
- I want to estimate the $\mu$ and $\sigma^2$
- $ \mu = \frac{1}{m} \sum_{i=1}^{m} X^{(i)} $
- $ \sigma^2 = \frac{1}{m} \sum_{i=1}^{m} (X^{(i)} - \mu)^2 $

## Algorithm - Density Estimation
- Training Set: $ \{ x^{(1)}, x^{(2)},...,x^{(m)} \}, X^{(i)} \in \mathbb{R} $
- We will assume that each $ x_i \sim \mathcal{N} $
- $ p(x) = \prod_{j=1}^{n} p(x_j,\mu_j,\sigma_j^2) $
- Also called Independent Assumption

**Process:**

- Choose features $X_i$ that you think might be indicative of anomalous features
- Fit parameters $ \mu_1,..\mu_n,\sigma_1^2..\sigma_n^2 $
  - $ \mu_j = \frac{1}{m} \sum_{i=1}^{m} X_j^{(i)} $
  - $ \sigma_j^2 = \frac{1}{m} \sum_{i=1}^{m} (X_j^{(i)} - \mu_j)^2 $
- Given a new example X, compute p(x):
  - $ p(x) = \prod_{j=1}^{n} p(x_j,\mu_j,\sigma_j^2) $
  - anomaly if $ p(x) < \sigma $
  - Or vectorized: $ \mu = \begin{bmatrix} \mu_1\\ \mu_2\\ .. \\ \mu_n \end{bmatrix} =   \frac{1}{m} \sum_{i=1}^{m} X^{(i)} $

## Example
![](AnomalyDetectionExample3.png)
- The probability of the two features can be plotted to be the cone above
- All the area below a certain height will be considered an anomaly

## Evaluation
- How do we evaluate which features to add? how do we evaluate the algorithm?
- Assume we have some labeled data, of anomalous and non anomalous examples (y=0 if normal, y=1 if anomalous).
- Training set: X(1)...X(m) - assume normal
- Cross validation $ (x_{cv}^1, y_{cv}^1),...,(x_{cv}^{m_{cv}}, y_{cv}^{m_{cv}}) $
- Test set $ (x_{test}^1, y_{test}^1),...,(x_{test}^{m_{test}}, y_{test}^{m_{test}}) $

An Example:

- 1000 good (normal) engines - most of them at least
- 20 flawed (anomalous) (2-50 typical amount of examples)
- Training Set: 6,000 good engines - use to fit p(x)
- CV: 2,000 good engines (y=0), 10 anomalous (y=1)
- Test: 2,000 good engines (y=0), 10 anomalous (y=1)
- 20%, 20% split
- Some people use the same engines in CV/Test, they are less recommended.

To evaluate:

- Fit the model $p(x)$ on the training set
- On CV/Test example x, predict: $
  y = \begin{cases}
    1, if p(x) < \epsilon \ (anomaly) \\
    0, if p(x) \ge \epsilon \ (normal)
  \end{cases}
$
- We will be predicting the accuracy. Our data is also skewed because we have a good data too.
- Possible evaluation metrics:
  - True positive, false positive, false negative, true negative
  - Precision/Recall
  - F-score
- Can also use cross validation set to choose the $ \epsilon $

## Anomaly Detection vs Supervised Learning
- Anomaly detection can be used when:
  - Very small number of anomalous (positive, y=1) examples (0-20)
  - Large number of normal (negative, y=0) example.
  - Many different types of anomalies, future anomalies may look nothing like the once we seen so far
  - Fraud detection, Manufacturing, monitoring machines
- Supervised learning:
  - Large number of positive and negative examples
  - Each positive examples for algorithm to get a sense of what positive examples are like, future positive examples likely to be similar to the training set.
  - For example with Spam, we have enough examples and that's why we think of it as supervised learning. Or Weather Prediction, Cancer classification, etc.

## What features to use?
- We modeled features using Gaussian distribution. So plot histogram of the data to ensure is a Gaussian (hist command). If it does not look Gaussian we might shift it to make it Gaussian. The algorithm will work regardless, but transforming the data a bit might make it better.

![](NonGuassianFeatures.png)

- or $ log (x_2 + c) $
- or $ x_4^{\frac{1}{3}} $
- (Lecture showing how to do it with Octave, playing with the powers of the X)

To come up with features:

![](ErrorAnalysisGuassian.png)

- Fit the model to the current features
- See anomalies that we fail to detect
- Figure out new features to help the system detect the anomalies. Make them stand out

Choose features that might take on unusually large of small values in the event of anomaly:

- x1 = memory use of computer, x2 = number of disk access, x3 = CPU load, x4 = network traffic
- we might create a new variable x5 = (cpu load) / (network traffic) to detect anomaly of high cpu without similar increase in traffic.

## Multivarate Guassian Distribution

![](MotivatingExampleMultiGuassian.png)

- Sometimes our normal features are not shaped exactly like a circle but have a more linear growth (the more CPU usage, the more memory usage) and the regular Gaussian might not manage to detect the failures.

![](GuassianDistributionFormula.png)

- The sigma on the equations is the covariance matrix and not summation symbol

![](GuassianDistributionExamples.png)

- shrinking sigma, the distribution is narrower and taller.
- if sigma gets bigger, the distribution is flatter

![](MultiGuassianExamples2.png)

- If only one of the variables on the matrix changes, we get a more ellipsis shape
- Can also modify the other diagonal in the covariance matrix to model negative or positive correlation between x and y.

## Algorithm

![](MultivariableDistributionAlgorithm.png)

1. Fit the model by setting $\mu$ and $\sigma$ above
2. Given a new example x, compute p(x) using formula above
3. Flag anomaly if $ p(x) < \epsilon $

This will correctly flag anomalies described before.

We can show that the regular distribution is where the sigma has zeros in the off diagonal area.

When to use each model?
- Original model: used more often, when x1, x2 can take unusual combination of values. To capture, create extra combination of values.
- Computationally cheaper, scales better to large n.
- OK even if m is small
- Multivariate Gaussian: automatically captures correlations between features.
- Calculate sigma matrix is more computationally expensive.
- Must have m>n or else E is non invertible. In practice, only if m is >> 10n
