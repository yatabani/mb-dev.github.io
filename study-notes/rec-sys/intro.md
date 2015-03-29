---
tags: ['study-notes', 'recsys']
---

# Recommender Systems - Intro
[https://www.coursera.org/learn/recommender-systems/](https://www.coursera.org/learn/recommender-systems/)

## Description
Recommender systems have changed the way people find products, information, and even other people. They study patterns of behavior to know what someone will prefer from among a collection of things he has never experienced. The technology behind recommender systems has evolved over the past 20 years into a rich collection of tools that enable the practitioner or researcher to develop effective recommenders. We will study the most important of those tools, including how they work, how to use them, how to evaluate them, and their strengths and weaknesses in practice.

The algorithms we will study include content-based filtering, user-user collaborative filtering, item-item collaborative filtering, dimensionality reduction, and interactive critique-based recommenders. We will also explore the design space for recommender systems, including designing recommender interfaces and the backends that support them, and the surrounding social issues such as identity, privacy, and manipulation. The approach will be hands-on, with a total of seven assignments that involve hands-on activities.

## Automated Collaborative Filtering
- ACF for Usenet News - user rate items, user are correlated with other users, Nearest Neighbor Approach.
- GroupLens project
- MovieLens - K-nearest Neighbor User-User.
  - Pair wise correlation - how much two users agree with each other.
- User User Collaborative filtering.

## Taxonomy
- Domain: What is being recommended? news articles, bundles, sequence (playlists), new items (new movies), previous items (groceries you bought before).
- Purpose: Sales (buy more items), information (educating the user), community. Examples:  [ReferralWeb](http://www.cs.rochester.edu/users/faculty/kautz/referralweb/index.html)
- Context: What is the user doing at the time of the recommendation? Shopping, Listening to music (do not want to get popup recommendations), Hanging out with other people (may make group recommendation), level of attention, level of interruption.
- Who's Opinion: Experts, ordinary people? [wine.com - expert recommendation](http://www.wine.com/), [Phoaks - ordinary people](http://www.sigchi.org/chi97/proceedings/paper/lgt.htm)
- Personalization Level: Generic / Non Personalized (everyone gets the same one), by demographic (male vs. female, ages), ephemeral (matches current activity), persistent (match long term preferences). [Landsend - non personalized](http://www.landsend.com/), [Brooks Brother - personalized by a service](http://www.brooksbrothers.com/), [CDNow - ephemeral - Album Advisor](http://en.wikipedia.org/wiki/CDNow)
- Privacy & Trust - who knows what about me? how can I deny some of the preferences, would the recommender system not leak information about me, is the recommendations honest (bias by operator, vulnerability to manipulation).
- Interface: What output do we give? predictions, recommendations, filtering, organic vs. explicit. How we get feedback? explicit vs. implicit.
- Recommendation Algorithms: Non personalized, content based (information filtering, knowledge based), collaborative filtering (user-user, item-item, dimension reduction), others.

Data Model:

- User, User Attributes <- Ratings -> Item, Item Attributes

- Non Personalized Summary Stats:
  - Best sellers, most popular, trending (zagat restaurant ratings, billboard music ranking)
  - Rating table is a matrix, user x items and values 1-5.
- Content Based Filtering:
  - Knowledge based filtering
  - Personalized news feeds
  - Artist or Genre music feed
- Linking them together:
  - When rating movies - the attributes are going to be ranked instead of item themselves.
  - User - user: find neighborhood with similar rating and use that for recommendations
  - Item - item: precompute similarity among items via rating and use that for recommendation
