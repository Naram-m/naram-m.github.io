---
title: Research Interests
type: page
date: 2026-09-09
toc: true
share: false
profile: false
show_breadcrumb: false
show_date: false
reading_time: true
---


My research lies at the intersection of online learning and network optimization. I develop algorithms that allocate resources before knowing future demands or operating conditions. I am interested in learning from this interaction, exploiting useful predictions, and providing rigorous guarantees when the environment behaves unexpectedly.

## Learning while the system runs

In online learning, an algorithm takes an action, observes feedback, and uses it to improve subsequent decisions. As Cesa-Bianchi emphasizes in his foreword to [Orabona's book][orabona], learning and evaluation are interleaved, complementing the familiar separation between training and testing. The framework allows us to study learning without assuming observations are independent samples from a fixed distribution.

The central performance measure is *regret*: the algorithm's accumulated cost relative to a specified benchmark, such as the best fixed decision chosen with hindsight. For caching, this could be the fixed collection of files that would have served users best. A suitable algorithm can make its average excess cost vanish over time, despite never seeing future requests. This possibility draws me to the field.

Several frameworks capture different aspects of this problem:

- **Online convex optimization (OCO)** uses convex costs and feasible sets to design efficient algorithms for sequential decisions. Applications include bandwidth allocation, portfolio selection, and updating prediction models as data arrive. [Orabona][orabona], [Hazan][hazan], and [Shalev-Shwartz][shalev] provide foundational treatments.
- **Bandits** capture limited feedback: a recommendation system observes responses to displayed items, but not the alternatives. Learning requires balancing exploration with exploiting promising choices. Stochastic bandits assume stable reward distributions; adversarial bandits allow reward sequences without that assumption. “Adversarial” describes the guarantee's scope, even without a malicious opponent. [Lattimore and Szepesvári][bandits] develop both settings.
- **Markov decision processes (MDPs)** incorporate lasting consequences: an action affects immediate rewards and future states, such as queue lengths or battery reserves. Learning in unknown MDPs connects exploration with long-term planning in reinforcement learning; see [Chapter 38 of Lattimore and Szepesvári][bandits].

The broader systems perspective of these frameworks is also considered in our [survey of pervasive AI](https://arxiv.org/abs/2105.01798), covering federated learning, distributed inference, and bandits under communication and computation constraints.

## Making useful predictions count

Now, consider a prediction of what happens next. A network operator might forecast demand using a machine learning model. Accurate forecasts could improve allocation, but their reliability may change precisely when good decisions matter most.

My [doctoral thesis][thesis], asks how algorithms can use **untrusted predictions while maintaining worst-case guarantees**. The objective combines robustness to inaccurate forecasts with gains when forecasts are informative. Optimism means adapting to prediction quality, which need not be known in advance. Regret bounds make this explicit: smaller prediction errors can yield substantially stronger guarantees.

Caching provides a concrete starting point: choosing files before requests arrive can reduce delays and network traffic. Our [TMC paper](https://doi.org/10.1109/TMC.2023.3317943) develops optimistic caching algorithms and learns which prediction sources are useful. Our [SIGMETRICS paper on discrete caching](https://arxiv.org/abs/2208.06414) establishes performance limits and develops algorithms for storing whole files, or more generally the online Knapsack problem. The guarantees improve with prediction accuracy while preserving worst-case regret rates.

The thesis then moves beyond a fixed benchmark. If demand changes, the best allocation can change with it. Through *dynamic regret*, I study performance against a moving sequence of decisions. Our [ICML work on optimism with history pruning](https://arxiv.org/abs/2505.22899) develops a guarantee for this more challenging settings.

Finally, I study systems with memory through *non-stochastic control*. As in an MDP, actions affect future states. Here, the underlying dynamics are linear, while disturbances and convex costs may be adversarial. Familiar linear-quadratic control specifies its cost model in advance. Here, costs arrive sequentially, and we compete with the best policy in a specified class, chosen in hindsight; see [Hazan and Singh's introduction to online control](https://www.cambridge.org/core/books/introduction-to-online-control/4EAE3F32A195899D073E496D2EDBD730). My thesis shows how forecasts over an extended horizon help account for the lasting effects of today's actions.

## When changing a decision has a cost

More recently, I have become interested in *smoothed online learning*, where an algorithm pays both for its decisions and for changing them. [*Smooth Handovers via Smoothed Online Learning*](https://ieeexplore.ieee.org/abstract/document/11044691) illustrates this tension in mobile networks: better connectivity must be balanced against handover costs. For AI inference, [Li and colleagues](https://arxiv.org/abs/2512.11131) use smoothed online convex optimization to study server/GPU provisioning with reconfiguration costs.

These examples motivate algorithms that balance responsiveness with stability. Our [recent AISTATS paper](https://proceedings.mlr.press/v300/mhaisen26a.html) studies how much an algorithm can moderate its updates while tracking a changing benchmark. We establish regimes where this is possible without sacrificing the optimal order of dynamic regret. My aim is to adapt to meaningful change while avoiding costly reactions to every fluctuation.

## Selected references and further reading

1. Francesco Orabona. [*Online Learning: A Modern Introduction Using Convex Optimization*][orabona]. 2026 manuscript.
2. Elad Hazan. [*Introduction to Online Convex Optimization*][hazan]. 2nd edition, MIT Press, 2022.
3. Shai Shalev-Shwartz. [*Online Learning and Online Convex Optimization*][shalev]. Foundations and Trends in Machine Learning, 4(2), 107–194, 2012.
4. Tor Lattimore and Csaba Szepesvári. [*Bandit Algorithms*][bandits]. Cambridge University Press, 2020. Free online edition.
5. Naram Mhaisen. [*Optimistic Learning with Applications to Caching Networks*][thesis]. PhD thesis, TU Delft, 2025.

[orabona]: https://arxiv.org/abs/1912.13213v10
[hazan]: https://mitpress.mit.edu/9780262046985/introduction-to-online-convex-optimization/
[shalev]: https://doi.org/10.1561/2200000018
[bandits]: https://tor-lattimore.com/downloads/book/book.pdf
[thesis]: https://doi.org/10.4233/uuid:68fd39be-e3d5-4b3a-a3e5-76c80b3121f0
