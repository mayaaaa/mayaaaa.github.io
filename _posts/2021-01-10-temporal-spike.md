---
layout: post
title: Temporal Spike Sequence Learning via Backpropagation for Deep Spiking Neural Networks 
tags: [NeurIPS20]
---

### [PDF](https://papers.nips.cc/paper/2020/file/8bdb5058376143fa358981954e7626b8-Paper.pdf)
**イントロ**
- 脳の活動にインスパイアされたSpiking Neural Networks (SNN)が注目を集めている
- バックプロパゲーション (BP)を用いた SNNの学習方法が多数提案されている
- しかし二つの課題がある
  - 離散のスパイクイベントが微分できないため誤差の正確な伝搬が難しい
  - 性能を上げるのにタイムステップ数が必要
- TSSL-BPは誤差伝搬を inter-neuron, intra-neuronの二種類の依存関係に分解する


