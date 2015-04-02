---
tags: ['study-notes', 'recsys']
---

# Recommender Systems - Non-Personalized Recommenders
[https://www.coursera.org/learn/recommender-systems/](https://www.coursera.org/learn/recommender-systems/)


### Example
- Zagat Guide. Each restaurant comes with four scores.
  - Formula: Each customer gives score 1-3, round(MEAN(ratings)*10)
- Other examples: Cruises, TripAdvisor, Billboard, Movie charts
- Average can be misleading: To find Zagat/Billboard useful, one needs to have similar taste to popular opinion.
- Average lack context - ketchup might be the most popular sauce, but not on a sundae.

### People who X also Y
- Start simple - (X and Y) / X
- The banana challenge - some products are very popular.
- Better: ((X and Y) / X) / ((!X and Y) / !X)
- Association Rule mining has a lift:
  P(X and Y) / (P(X) * P(Y))

## Issues
- Self selection bias - people who don't like some restaurants - don't go there, and they drop from the average.
- Some people don't like fine dining yet they still participate in ratings.
- It can work well for travel, books etc.
