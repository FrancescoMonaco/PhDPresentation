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
     Some hash indices are data adaptive and don't need to 

- <span v-mark.red="2"> Problem</span>:
     They are usually slower than the non-adaptive ones

- <span v-mark.red="3"> Solution </span>:
    We implement a coreset predictor

---
transition: fade
---

# Test

---
transition: fade
layout: center
---

# <span class="leit-title">ThanKs foR youR AttentioN</span>