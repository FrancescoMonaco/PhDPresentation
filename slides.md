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
# <span class="leit-title">Enriching Mining Algorithms with Hash Oracles</span>

<div class="absolute bottom-10">
  <span class="font-700">
    Francesco Pio Monaco, May 2025
  </span>
</div>

---
transition: fade
---

# The Problem
A continuos increase in the volume of data

 - Many mining algorithms scale with super linear behaviors
 - We need to find efficient techniques to deal with this data
 - We want to have theoretical guarantees on the performance of our algorithms and the quality of the results

---
transition: fade
---

# A Recent Development
Algorithms with Predictions

---
transition: fade
---

# Algorithms with Predictions
Do they work?

---
transition: fade
---

# Algorithms with Predictions
What is the plan?

- We want to integrate hash structures in the algorithms with predictions framework.
    Their theoretical properties are suitable for our goal of obtaining theoretical guarantees.

---
transition: fade
---

# Algorithms with Predictions
What is the plan?

- We want to integrate hash structures in the algorithms with predictions framework.
    Their theoretical properties are suitable for our goal of obtaining theoretical guarantees.

- We want to expand in the offline setting


---
transition: fade
---

# Algorithms with Predictions
A predictor for hash indices

- <span v-mark.orange="1"> Setting</span>:
    Hash indices, structures to answer Approximate Near Neighbor Queries, are used for many downstream tasks like clustering, recommender systems or pattern matching.

    Some hash indices, like PUFFINN*, are data adaptive and don't need have a set of parameters to tune.

- <span v-mark.red="2"> Problem</span>:
     Data adaptive hash indices are usually slower than the non-adaptive ones during the search operation, we would like to keep the data adaptive property while making it competitive with carefully hash indices.

- <span v-mark.green="3"> Solution</span>:
    We implement a predictor based on clusters and coresets that drives the search of the hash index. Saving time during the search operation.


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

---
transition: fade
---

# Algorithms with Predictions
A predictor for hash ensembles
- <span v-mark.orange="1"> Setting</span>:
     Ensembles are a family of algorithms that use multiple models to improve the performance. They are used in many neural tasks.

- <span v-mark.blue="2"> Idea</span>:
    We want to extend the idea of ensembles to the hash setting. We want to use multiple hash indices to improve the performance of the search.

- <span v-mark.green="3"> Solution</span>:
    We implement an ensembles of hash indices, indices will complement each other on different data distributions. A predictor will be used to select the best hash index for the current data distribution.
  

---
transition: fade
layout: center
---

# <span class="leit-title">ThanKs foR <br> yOuR AttenTion</span>