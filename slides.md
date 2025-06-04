---
# You can also start simply with 'default'
theme: default
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://cover.sli.dev
# some information about your slides (markdown enabled)
title: Enriching Similarity Search Algorithms with Predictors
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
# <span class="leit-title">Enriching Similarity Search Algorithms with Predictors</span>

<div class="absolute bottom-10">
  <span class="font-700">
    Francesco Pio Monaco, June 2025
  </span>
</div>

---
transition: fade
---

# The Setting
A continuos increase in the volume of data

<br>

 - We want to analyze and extract information from large amounts of data.

 - We need to find efficient techniques to deal with this data.

 - Many mining algorithms scale with super linear time complexity.


---
transition: fade
---

# The Setting
Similarity Search

<br>

- Similarity search is a fundamental task where we want to find the most similar elements in a collection of elements.
<br>

- In particular, we are interested in the Approximate Near Neighbor Search (ANNS) problem.

   - Given a set of elements and a query, we want to find the elements in the set <span v-mark.green = "1">that are closest</span> to the query.
   - This procedure is used in applications like time series analysis to find common patterns, Minimum Spanning Tree to find the minimal edges, recommender systems to find similar elements to propose.


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

- Neural predictors need to be trained using specific techniques (e.g., <span v-mark.orange="1">conformal or calibrated predictions</span>) 

- Need lots of data to reach theoretical guarantees on the predictions.

- Not easy to deploy in real-world applications.

<br>

<span v-mark.circle.green="2">Idea</span>:

- We can use hash structures to obtain deployable and robust predictors.


---
transition: fade
---

# Goals of the project
What is the plan?
<br>

- We want to integrate hash structures in the algorithms with predictions framework.

    - We obtain robust predictors that are easy to initialize and deploy.
    - We address the challenges posed by high-dimensional data in ANNS.
    - We derive mechanisms that can be expandend in several downstream tasks.
<br>
---
transition: fade
---

# Goals of the project
What is the plan?
<br>

- We want to integrate hash structures in the algorithms with predictions framework.

    - We obtain robust predictors that are easy to initialize and deploy.
    - We address the challenges posed by high-dimensional data in ANNS.    
    - We derive mechanisms that can be expandend in several downstream tasks.

<br>

- We expand in the offline setting.

    - The algorithm with predictions framework started for streaming data.
    - In the last months some works showed that it is beneficial also in the offline one.


---
transition: fade
---

# A predictor for hash indices
Faster ANN search

<br>

- <span v-mark.orange="1"> Setting</span>:
    Hash indices, structures to answer Approximate Near Neighbor Queries, are used for many downstream tasks like clustering, recommender systems or pattern matching.

    Some hash indices, like PUFFINN*, are data adaptive and don't have a set of parameters to tune, making them more general.

- <span v-mark.red="2"> Problem</span>:
     Data adaptive hash indices are usually slower than the non-adaptive ones during the search operation, we would like to reduce search time.

- <span v-mark.green="3"> Solution</span>:
    We implement a predictor based on clusters and coresets that drives the search of the hash index. Saving time during the search operation.

<br>

###### *([Aumüller et al., 2020](https://arxiv.org/abs/1906.12211))
---
transition: fade
---

# A predictor for hash indices
Faster ANN search

<HashTreeAnimation />

---
transition: fade
---

# A Bloom filter predictor for distance approximations
Faster distance computations in ANN

<br>

- <span v-mark.orange="1"> Setting</span>:
    Computing distances between elements is fundamental in tasks of ANN.

- <span v-mark.red="2"> Problem</span>:
    Computing distances is expensive, especially in high dimensional spaces. We want to approximate the distance between elements using a small subset of their dimensions.
    Current methods to approximate distances have known problems on robustness.

- <span v-mark.green="3"> Solution</span>:
    We implement a sensitive Bloom filter predictor to select the most relevant dimensions and estimate the distance between elements. We expect it to be robust given the theoretical properties of the Bloom filter.

---
transition: fade
---

# A Bloom filter predictor for distance approximations
Faster distance computations in ANN

<Bloom />

---
transition: fade
---

# Some Results in the literature
How much can predictors help? An application to triangle counting in graphs

<img src="/images/tonic.png" style="width:auto; height:65%;" />

<br>

###### *([Boldrin, Vandin, 2024](https://arxiv.org/pdf/2409.15205))


---
transition: fade
---

# Some Results in the literature
How much can predictors help? An application to motif discovery in multivariate time series

<table class="w-full text-xs border-collapse border border-gray-300">
  <thead>
        <th class="border px-1 py-0.5">dataset</th>
        <th class="border px-1 py-0.5">n (length)</th>
        <th class="border px-1 py-0.5">D (dimensionality)</th>
  </thead>
    <tbody>
    <tr>
      <td class="border px-1 py-0.5">potentials</td>
      <td class="border px-1 py-0.5">2 500</td>
      <td class="border px-1 py-0.5">8</td>
    </tr>
    <tr>
      <td class="border px-1 py-0.5">evaporator</td>
      <td class="border px-1 py-0.5">7 000</td>
      <td class="border px-1 py-0.5">5</td>
    </tr>
    <tr>
      <td class="border px-1 py-0.5">RUTH</td>
      <td class="border px-1 py-0.5">14 859</td>
      <td class="border px-1 py-0.5">32</td>
    </tr>    
    <tr>
      <td class="border px-1 py-0.5">weather</td>
      <td class="border px-1 py-0.5">100 057</td>
      <td class="border px-1 py-0.5">8</td>
    </tr>    
    <tr>
      <td class="border px-1 py-0.5">whales</td>
      <td class="border px-1 py-0.5">450 001</td>
      <td class="border px-1 py-0.5">32</td>
    </tr>    
    <tr>
      <td class="border px-1 py-0.5">quake</td>
      <td class="border px-1 py-0.5">6 440 998</td>
      <td class="border px-1 py-0.5">32</td>
    </tr>    
    <tr>
      <td class="border px-1 py-0.5">el_load</td>
      <td class="border px-1 py-0.5">6 960 008</td>
      <td class="border px-1 py-0.5">10</td>
    </tr>    
    <tr>
      <td class="border px-1 py-0.5">LTMM</td>
      <td class="border px-1 py-0.5">25 132 289</td>
      <td class="border px-1 py-0.5">6</td>
    </tr>
    </tbody>
</table>

<br>

###### *([Ceccarello, Monaco, Silvestri, 2025](https://arxiv.org/pdf/2502.14446))

---
transition: fade
---

# Experimental Results
Time to find the top motif in seconds

<table class="w-full text-xs border-collapse border border-gray-300">
  <thead>
    <tr>
      <th class="border px-1 py-0.5">dataset</th>
      <th class="border px-1 py-0.5" colspan="2">LEIT-motifs</th>
      <th class="border px-1 py-0.5">MSTUMP</th>
      <th class="border px-1 py-0.5">EMD</th>
      <th class="border px-1 py-0.5">RP</th>
    </tr>
    <tr>
      <th></th>
      <th class="border px-1 py-0.5">Index build</th>
      <th class="border px-1 py-0.5">Total</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="border px-1 py-0.5">potentials</td>
      <td class="border px-1 py-0.5">0.11</td>
      <td class="border px-1 py-0.5 bg-green-100 text-black">0.51</td>
      <td class="border px-1 py-0.5">3.65</td>
      <td class="border px-1 py-0.5">4.80</td>
      <td class="border px-1 py-0.5">3.20</td>
    </tr>
    <tr>
      <td class="border px-1 py-0.5">evaporator</td>
      <td class="border px-1 py-0.5">0.16</td>
      <td class="border px-1 py-0.5 bg-green-100 text-black">0.55</td>
      <td class="border px-1 py-0.5">4.45</td>
      <td class="border px-1 py-0.5">12.95</td>
      <td class="border px-1 py-0.5">6.78</td>
    </tr>
    <tr>
      <td class="border px-1 py-0.5">RUTH</td>
      <td class="border px-1 py-0.5">2.91</td>
      <td class="border px-1 py-0.5 bg-green-100 text-black">8.10</td>
      <td class="border px-1 py-0.5">84.04</td>
      <td class="border px-1 py-0.5">1.5h</td>
      <td class="border px-1 py-0.5">2.3h</td>
    </tr>
    <tr>
      <td class="border px-1 py-0.5">weather</td>
      <td class="border px-1 py-0.5">15.04</td>
      <td class="border px-1 py-0.5 bg-green-100 text-black">33.37</td>
      <td class="border px-1 py-0.5">1035.73</td>
      <td class="border px-1 py-0.5">-</td>
      <td class="border px-1 py-0.5">1.2h</td>
    </tr>
    <tr>
      <td class="border px-1 py-0.5">whales</td>
      <td class="border px-1 py-0.5">60.67</td>
      <td class="border px-1 py-0.5 bg-green-100 text-black">2.2 h</td>
      <td class="border px-1 py-0.5">(2.7 days)</td>
      <td class="border px-1 py-0.5">-</td>
      <td class="border px-1 py-0.5">-</td>
    </tr>
    <tr>
      <td class="border px-1 py-0.5">quake</td>
      <td class="border px-1 py-0.5">175.3</td>
      <td class="border px-1 py-0.5 bg-green-100 text-black">3.6 h</td>
      <td class="border px-1 py-0.5">(7.2 days)</td>
      <td class="border px-1 py-0.5">-</td>
      <td class="border px-1 py-0.5">-</td>
    </tr>
    <tr>
      <td class="border px-1 py-0.5">el_load</td>
      <td class="border px-1 py-0.5">180.2</td>
      <td class="border px-1 py-0.5 bg-green-100 text-black">2.8 h</td>
      <td class="border px-1 py-0.5">(8.4 days)</td>
      <td class="border px-1 py-0.5">-</td>
      <td class="border px-1 py-0.5">-</td>
    </tr>
    <tr>
      <td class="border px-1 py-0.5">LTMM</td>
      <td class="border px-1 py-0.5">240.6</td>
      <td class="border px-1 py-0.5 bg-green-100 text-black">15.6 h</td>
      <td class="border px-1 py-0.5">(11.8 days)</td>
      <td class="border px-1 py-0.5">-</td>
      <td class="border px-1 py-0.5">-</td>
    </tr>
  </tbody>
</table>


---
transition: fade
---

# Extra
A Computer Vision application

- A CNN is used conjunctly with an LSTM to create a textual description of the people in a video stream.

- To reverse search in a video from a textual description a hash index is used to find the matching frames.

- The description creates a textual embedding, ANN search finds the closest frames in the hash index, the frames are then retrieved and the CNN is used to find the people in the frames.

<img src="/images/mdpi.png" style="width:auto; height:35%;" />

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


---
transition: fade
---

# A predictor for hash ensembles
Improving quality for drifting data

<br>

- <span v-mark.orange="1"> Setting</span>:
     Ensembles are a family of algorithms that use multiple models to improve the performance. They are used in many neural tasks. Extremely useful to deal with data drift.

- <span v-mark.blue="2"> Idea</span>:
    We want to extend the idea of ensembles to the hash setting. We want to use multiple hash indices to improve the performance of the search and support mixture data.

- <span v-mark.green="3"> Solution</span>:
    We implement an ensembles of hash indices, indices will complement each other on different data distributions. A predictor will be used to select the best hash index for the current data distribution.

---
transition: fade
---

# A predictor for hash ensembles
Improving quality for drifting data

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
Timeline

```mermaid {theme: 'forest'}
gantt
    title Year 1 Timeline
    dateFormat  YYYY-MM-DD
    axisFormat  %b %Y
    section PhD Activities
    Lessons                        :crit, 2025-11-01, 2026-07-31
    section Project Packages
    Predictor MST Algorithm        :done, mst_predictor, 2025-11-01, 2026-03-30
    Predictor ANN Queries          :active, ann_predictor, 2026-02-01, 2026-10-31
    section Subactivities
    Benchmarking                   :done, benchmark, 2025-11-01, 2026-01-31
    Paper Preparation                     :done, paper_prep, 2026-02-01, 2026-03-30
    Literature Review & Design     :active, review_design, 2026-02-01, 2026-07-31
    ANN Evaluation                 :active, ann_eval, 2026-08-01, 2026-10-31
    section Milestones/Deliverables
    Closure MST Paper              :milestone, mst_closure, 2026-05-01, 1d
    Framework for ANN Queries      :milestone, ann_framework, 2026-08-01, 1d
```

---
transition: fade
---

# Extra
Timeline

```mermaid {theme: 'forest'}
gantt
    title Year 2 Timeline
    dateFormat  YYYY-MM-DD
    axisFormat  %b %Y

    section PhD Activities
    Period Abroad                  :crit, abroad, 2027-02-01, 2027-10-20

    section Project Packages
    ANN Predictor                  :done, ann_predictor, 2026-11-01, 2027-01-31
    Distance Predictor             :active, dist_predictor, 2027-02-01, 2027-10-31

    section Subactivities
    Paper Preparation (ANN)        :done, ann_prep, 2026-11-01, 2027-01-31
    Literature Review & Development:active, dist_lit_dev, 2027-02-01, 2027-07-31
    Evaluation                     :active, dist_benchmark, 2027-08-01, 2027-09-25
    Paper Preparation              :active, paper_prep, 2027-09-01, 2027-11-30

    section Milestones/Deliverables
    ANN Paper Closure              :milestone, ann_closure, 2027-02-01, 1d
    Distance Framework             :milestone, dist_framework, 2027-08-01, 1d
```

---
transition: fade
---

# Extra
Timeline

```mermaid {theme: 'forest'}
gantt
    title Year 3 Timeline
    dateFormat  YYYY-MM-DD
    axisFormat  %b %Y
    section PhD Activities
    Thesis Preparation             :crit, thesis_prep, 2028-03-01, 2028-11-30
    section Project Packages
    Hash Ensemble Predictor        :active, hash_predictor, 2027-11-01, 2028-07-31
    section Subactivities
    Develop Hash Ensemble    :active, ensemble_dev, 2027-11-01, 2028-01-31
    Predictor for Ensamble       :active, predictor_dev, 2028-02-01, 2028-04-30
    Evaluation          :active, hash_eval, 2028-04-11, 2028-05-18
    Downstream Tasks    :active, down, 2028-05-13, 2028-08-01
    section Milestones/Deliverables
    Distance Paper Closure         :milestone, dist_closure, 2028-02-01, 1d
    Thesis Closure                 :milestone, thesis_closure, 2028-11-07, 1d
```
