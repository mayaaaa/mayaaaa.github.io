---
layout: post
title: A Framework for Recommending Accurate and Diverse Items Using Bayesian Graph Convolutional Neural Networks 
tags: [KDD2020]
---

### [PDF](https://dl.acm.org/doi/pdf/10.1145/3394486.3403254)
**イントロ**
- オンラインショッピング, ビデオ視聴, ニュース行動などオンライン上の消費行動がポピュラーに
- このような消費行動を予測するための推薦手法は userとitemのembedding, それらの間の非線形な関係を捉えるものが提案されている
- しかし, 既存の推薦手法には三つの大きな課題がある
  - スパース性: ユーザとアイテムの相互作用が少ない場合, よい表現を学習できない
  - 不確実性: 既存手法はデータを不確実性がないものとして扱っている
  - 多様性: 既存のtop-N推薦手法はtop-Nのアイテムそれぞれのみにフォーカスしており, トップN個のアイテムの多様性を見過ごしている
- GCNはスパースなデータやコールドスタート問題に対処できるということが知られている
- ただし不確実性や多様性を考慮することはできない
- Bayesian Graph Neural Networks (BGNNs)に基づきnode-copyingを用いた新たな手法を提案
- node-copyingモデルは観測グラフに似ているが十分な多様性を含む
- 提案手法はスケーラブルで不確実性に対処できる

