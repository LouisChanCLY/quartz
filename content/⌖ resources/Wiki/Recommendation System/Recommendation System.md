---
tag: todo
date: 2022-07-19
---

## Metadata
- Association:
- Domain: [[Domain Root - Data Science]]

## Recommendation System

Recommendation systems try to rank items according to their relevance with other items, i.e. similarities & [[Correlation]]. A more relevant item will have a higher score than a less relevant one. There are generally two approaches in implementing the system: content-based vs collaborative filtering.
#todo ==apparently there is a third option by combining both==

### [[Collaborative Filtering Recommendation System]]

This is a design with user perception & experience as the centrepiece of the system. Rankings will be determined solely on what other users prefer.

**Assumptions:** Historical data is all we need to make recommendations; Existing user base is statistically similar to new users; Trends are not important; Historical data is large and high quality enough for any inference

**Example:** let’s say a lot of users like coffee, tea, milk tea, and coffee with milk tea. At the same time, I like coffee, tea and milk tea as well. When I ask a Collaborative Filtering System what should I try next, it will suggest coffee with milk tea over coke.

### [[Content-based Recommendation System]]

The intuition is simple — the more similar the content, the higher the ranking. In cases where we are recommending contents for users, we would infer that action movie lovers should like Avengers if other action movies lovers like it too. The difference this has from collaborative filtering is that we are including the [[Latent Labels]] of users & products as part of the recommendation process.

**Assumptions:** Meta-labels have predictive power on whether something should be recommended.

**Example:** For example, although both Assasin’s Creed and Captain America are classified as action movies, user’s preferences on gaming (meta-label of a user) may come into play on how likely they would like Assasin’s Creed.