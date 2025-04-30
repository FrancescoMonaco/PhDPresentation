---
# You can also start simply with 'default'
theme: default
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://cover.sli.dev
# some information about your slides (markdown enabled)
title: Enriching Mining Algorithms with Hash Oracles
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

- We want to use hash oracles

---
transition: fade
---

# Algorithms with Predictions
What is the plan?

- We want to use hash oracles
- We want to expand in the offline setting

---
transition: fade
---

# Algorithms with Predictions
A coreset predictor for hash indices

- <span v-mark.orange="1"> Setting</span>:
    Hash indices are used for tasks like clustering, recommender systems

    Some hash indices, like PUFFINN*, are data adaptive and don't need to have their parameter tuned to the task, so they are preferred .

- <span v-mark.red="2"> Problem</span>:
     Data adaptive hash indices are usually slower than the non-adaptive ones during the search operation, we would like to keep the data adaptive property while making it competitive with carefully tuned non-adaptive hash indices.

- <span v-mark.green="3"> Solution </span>:
    We implement a coreset predictor that drives the search of the hash index. Saving time during the search operation.


###### *([Aumüller et al., 2020](https://arxiv.org/abs/1906.12211))
---
transition: fade
---

# Algorithms with Predictions
A coreset predictor for hash indices

---
transition: fade
---

# Algorithms with Predictions
A Bloom filter predictor for approximate triangle counting

- <span v-mark.orange="1"> Setting</span>:
    Triangle counting is a fundamental task in graph mining, with applications in social network analysis and bioinformatics.

    The task is to count the number of times a certain pattern appears.

- <span v-mark.red="2"> Problem</span>:
    Current predictors are trained one time and their performaces degrade over time due to the dynamic nature of the data. We want to use an oracle that can detect the shifts in the data distribution and adapt to them.

- <span v-mark.green="3"> Solution </span>:
    We implement a sensitive Bloom filter that with constant time operations can update itself to the new data distribution. This allows us to obtain accurate predictions.

---
transition: fade
---

# Algorithms with Predictions
A Bloom filter predictor for approximate triangle counting

---
transition: fade
layout: center
---

# <span class="leit-title">ThanKs foR <br> yOuR AttenTion</span>