---
tags: ['study-notes', 'ml']
---

# Machine Learning - Stanford
[https://www.coursera.org/course/ml](https://www.coursera.org/course/ml)

## Week 10 - Large Scale Machine Learning
- One of the best way to get ML is to use low bias algorithm and train in a lot of data

![Large data wins](http://i.imgur.com/z5qXQ3D.png)

- If m = 100,000,000, like the US census then and training a linear/logistic regression - this requires summing 100,000,000 times.
- We might want to just train on fewer examples, like 1,000. To verify that, use learning curves.
- This is called Batch gradient descent

### Stochastic Gradient Descent

![Stochastic Gradient Descent vs. Batch](http://i.imgur.com/QEsRIKl.png)

- Random shuffle to make it converge a bit better
- The algorithm improves the theta parameters with each iteration instead of only updating after going through all examples.

![Convergance](http://i.imgur.com/qXFG73W.png)

- It does not converge like the other gradient descent. It usually runs around the global minimum.
- The outer loop is repeat 1-10 times depends on the size of the data set. For 300,000,000 once might be enough.


### Mini batch gradient descent

[Mini Batch](http://i.imgur.com/hMl15Aj.png)

- Batch - use all m training example
- Stochastic - uses 1 example in each iteration while Mini batch uses b examples in each iteration. b = 2-100.
- When summing 10 examples, we can vectorize it. and it might be slower than just 1 example. But then there's another parameter - b has to be fiddled with.

### Convergence

![Convergence](http://i.imgur.com/grywkjw.png)

- In batch gradient descent we plotted the function on the number of iterations which will be slow for large data.
- Every 1,000 examples, avg the values and plot.

![Convergence](http://i.imgur.com/qvkHopg.png)

- top left: red is smaller learning rate
- top right: 1000 might give less smooth curve than 5,000.
- bottom left: Same as above, it might show that it's going down at 5,000
- bottom right: the algorithm is diverging - use smaller alpha.
- it's possible to lower alpha over time (alpha = const1/(iteration number + const2)), but with the cost of const1 and const2

### Online Learning

![Online Learning](http://i.imgur.com/TaEOPeP.png)

- useful to learn from continuous stream of data.
- get (x,y) pair for a visitor
- can adapt to change in user preference

![Online Learning 2](http://i.imgur.com/brNW92B.png)

- For each phone and - construct a feature.
- Estimate the probability that the user will click on the link
- Predicted CTR
- For each session, we will get 10 examples and the y value for that.
- Similar: which offers to show? which news to aggregate?

### Map reduce and data parallelism

![Map Reduce](http://i.imgur.com/MtxU9Rr.png)

- We assume we have 400 training set
- Four machines, each machine use a 1/4 of the data
- This is the same as the function above, just counting the sum on four machines.
- Can the algorithm be expressed as sums of training set? if so, map reduce can be candidate.
- Multi-core can also be used to split the training set.
- Caveat: some numerical libraries can automatically scale to multi-core.

### Application case study - OCR

![Photo OCR Problem](http://i.imgur.com/OpQvmzf.png)

- Example problem: How to capture text in images, to enable search
- Solution: Find regions where the text is, and then segment the characters and then run a classifier on each character
- A spelling correction might also be required
- Pipeline - all the steps required to solve ML problem. This is the example of the OCR pipeline.

![OCR Pipeline](http://i.imgur.com/LMCqvVc.png)

- The challenge is defining the pipeline, so that it's possible to split the team to work on different parts of the pipeline.

**Sliding windows**:

- To explain the algorithm we will use a pedestrian detection, that is simpler, since aspect ratio is similar.

![Sliding Windows](http://i.imgur.com/3JcPs6S.png)

- We'll step a rectangle around the image by (step size).
- Train a NN to classify the squares - In a typical system there might be 1000 examples. NN might classify it.

![Sliding Windows](http://i.imgur.com/lryMNIL.png)

- Run each rectangle through the classifier

- In detecting text in image, we will have patches of images that contains text and patches that do not contain text.
- Apply expansion operator to find chunks.
- Look at connected components. Ignore thin tall once.

![Sliding Windows](http://i.imgur.com/ExeksJF.png)

![Sliding Windows](http://i.imgur.com/dtKJiZ1.png)

- Detect if we have a mid point in the text. and if so, move the sliding window.

**Artificial Data**:
![4:16]()

- Provides easy way to get a lot of data.
- Example, it's possible to use all the fonts available on the computer, and paste them against random background.

![5:02]()
- Another idea - take example we have, and introduce distortions.
- Introduce only distortions that you might see in the real data.
- Before going on this route, ensure you have a low bias classifier.
- Ask: How much work would it to be to get 10x as much data as we have? if it's only a few days, it might be worth it.
- It's also possible to classify ourselves. Calculate how much time it would take.
- Also Mechanical Turk can be used to cloud source data labeling.

### Ceiling Analysis
What part of the pipeline to work next:

![Ceiling Analysis](http://i.imgur.com/cbZB1Y2l.png)

- The most valuable resource is the time of colleagues, so deciding which component is worth to invest time to improve.
- We can have some metric as example: "overall system": 72%
- We can manually feed the pipeline with correct results and see how much this improves the system.
- Suppose with perfect data for text detection - the system overall metric got to 89%
- For character segmentation we get to 90%
- For character recognition we get to 100%
- So we see that getting perfect text detection gets us only 1% improvement - not worth it, while investing time to improve other parts can give 10% improvement or more.
- Another example: Recognize image. We can recognize facial features. Do ceiling analysis to see which part to improve.
- There was a team that spent 1.5 years on background removal - and yet it did not make big improvement.
