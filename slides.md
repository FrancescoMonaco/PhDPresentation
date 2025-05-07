---
# You can also start simply with 'default'
theme: default
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://cover.sli.dev
# some information about your slides (markdown enabled)
title: Enriching Similarity Search Algorithms with Oracles
titleTemplate: '%s'
author: 'Francesco Pio Monaco'
info: |
  PhDProject
# apply unocss classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
# open graph
# seoMeta:
#  ogImage: https://cover.sli.dev

---
<style>
@font-face {
  font-family: 'BPdots';
  src: url('/fonts/BPdotsUnicasePlus.otf') format('opentype');
  font-display: swap;
}

.leit-title {
  font-family: 'BPdots', sans-serif;
  font-size: 3rem;
  letter-spacing: 0.05em;
}
</style>
# <span class="leit-title">Enriching Similarity Search Algorithms with Oracles</span>

<div class="absolute bottom-10">
  <span class="font-700">
    Francesco Pio Monaco, May 2025
  </span>
</div>

---
transition: fade
---

# The Setting

<br>

- Similarity search is a fundamental task where we want to find the most similar elements in a collection of elements.
<br>

- In particular, we are interested in the Near Neighbor Search (ANNS) problem.

   - Given a set of elements and a query, we want to find the elements in the set <span v-mark.green = "1">that are closest</span> to the query.
   - This procedure is used in many applications like time series analysis, Minimum Spanning Tree, recommender systems.

---
transition: fade
---

# The Problem
A continuos increase in the volume of data

<br>

 - Many similarity search algorithms scale with super linear behaviors.

 - We need to find efficient techniques to deal with this data.

 - We want to have theoretical guarantees on the performance of our algorithms and the quality of the results.

---
transition: fade
---

# A Recent Development
Algorithms with Predictions

<br>

- Algorithms with predictions is a new framework to design algorithms that use a <span v-mark.yellow="1">predictor</span> to improve their performance.

- They keep the theoretical guarantees of the original algorithm while improving their performance in the <span v-mark.yellow="2">average case</span>.

- The predictors are usually neural models <span v-mark.red="3">trained</span> on data that is similar to the one used in the algorithm.
---
transition: fade
---

# Algorithms with Predictions
The current challenges

<br>

- Neural predictors need to be trained using specific techniques (e.g., conformal predictions, calibrated predictions) and need lots of data to reach theoretical guarantees on the predictions.

- We can use hash structures to obtain deployable and robust predictors.


---
transition: fade
---

# Algorithms with Predictions
What is the plan?
<br>

- We want to integrate hash structures in the algorithms with predictions framework.

    - We obtain robust predictors that are easy to initialize and deploy.
    - We address the challenges posed by high-dimensional data in ANNS.
<br>
---
transition: fade
---

# Algorithms with Predictions
What is the plan?
<br>

- We want to integrate hash structures in the algorithms with predictions framework.

    - We obtain robust predictors that are easy to initialize and deploy.
    - We address the challenges posed by high-dimensional data in ANNS.
<br>

- We expand in the offline setting.

    - The algorithm with predictions framework started for streaming data.
    - In the last months some works showed that it is beneficial also in the offline one.


---
transition: fade
---

# Algorithms with Predictions
A predictor for hash indices

<br>

- <span v-mark.orange="1"> Setting</span>:
    Hash indices, structures to answer Approximate Near Neighbor Queries, are used for many downstream tasks like clustering, recommender systems or pattern matching.

    Some hash indices, like PUFFINN*, are data adaptive and don't need have a set of parameters to tune.

- <span v-mark.red="2"> Problem</span>:
     Data adaptive hash indices are usually slower than the non-adaptive ones during the search operation, we would like to keep the data adaptive property while making it competitive with carefully hash indices.

- <span v-mark.green="3"> Solution</span>:
    We implement a predictor based on clusters and coresets that drives the search of the hash index. Saving time during the search operation.

<br>

###### *([Aumüller et al., 2020](https://arxiv.org/abs/1906.12211))
---
transition: fade
---

# Algorithms with Predictions
A predictor for hash indices

<HashTreeAnimation />

---
transition: fade
---

# Algorithms with Predictions
A Bloom filter predictor for distance approximations

<br>

- <span v-mark.orange="1"> Setting</span>:
    Computing distances between elements is fundamental in tasks of similarity search.

- <span v-mark.red="2"> Problem</span>:
    Computing distances is expensive, especially in high dimensional spaces. We want to approximate the distance between two elements using a small subset of their dimensions.
    Current methods to approximate distances have known problems on robustness.

- <span v-mark.green="3"> Solution</span>:
    We implement a sensitive Bloom filter to select the most relevant dimensions to be used in the distance approximation. We use the filter rapresentation to estimate the remaining dimensions.

---
transition: fade
---

# Algorithms with Predictions
A Bloom filter predictor for distance approximations

<Bloom />

---
transition: fade
---

# Algorithms with Predictions
A predictor for hash ensembles

<br>

- <span v-mark.orange="1"> Setting</span>:
     Ensembles are a family of algorithms that use multiple models to improve the performance. They are used in many neural tasks. Extremely useful to deal with data drift.

- <span v-mark.blue="2"> Idea</span>:
    We want to extend the idea of ensembles to the hash setting. We want to use multiple hash indices to improve the performance of the search.

- <span v-mark.green="3"> Solution</span>:
    We implement an ensembles of hash indices, indices will complement each other on different data distributions. A predictor will be used to select the best hash index for the current data distribution.

---
transition: fade
---

# Algorithms with Predictions
A predictor for hash ensembles

<Ensemble />

---
transition: fade
layout: center
---

# <span class="leit-title">ThanKs foR <br> yOuR AttenTion</span>

---
transition: fade
---

# Extra
A Computer Vision application

- A CNN is used conjunctly with an LSTM to create a textual despcription of the people in a video stream.

- To reverse search in a video from a textual description a hash index is used to find the matching frames.

- The description creates a textual embedding, ANN search finds the closest frames in the hash index, the frames are then retrieved and the CNN is used to find the people in the frames.

<br>

###### *([Yuenyoung et al., 2022](https://www.mdpi.com/2504-2289/6/4/136))

---
transition: fade
---

# Extra
An industry application

- A hash index is used to cluster behaviours of a set of sensors in an incinerator.

- A dictionary of behaviours helps the recognition of anomalies.

- The project was carried out in collaboration with beanTech IT.

<img src="/images/multidim_shap_profile.png" style="width:auto; height:65%;" />

