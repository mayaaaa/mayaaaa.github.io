---
layout: post
title: Learning to Extrapolate Knowledge: Transductive Few-shot Out-of-Graph Link Prediction 
tags: [NeurIPS2020]
---

### [PDF](https://proceedings.neurips.cc/paper/2020/file/0663a4ddceacb40b095eda264a85f15c-Paper.pdf)
**イントロ**
- 非ユークリッド空間においてグラフをあつかうGNN手法が多数存在する
- 近年はエッジのラベルや向きを考慮する relation-aware GNN手法が提案されている
- 関連して, FreebaseやWordNet等のナレッジグラフが注目を集めている
- ナレッジグラフは多数のtripletsから成るが, 一方で欠損が多いことでも知られている
- ナレッジグラフの補完 (いわゆるリンク予測)が界隈で重要なタスクになっている
- 実世界におけるリンク予測にはいくつか課題がある
  - ナレッジグラフは時間的に変化する
    - 一日に200程度のノードが新しく生成される
  - ナレッジグラフはロングテールの分布を持つ
    - ノードの大多数が少数のtripletを持つ
- 新しく生成されたノードに対するFew-Shot Out-of-Graph (OOG)リンク予測を行う
- そのためにOOGリンク予測のためのmeta-learning手法を提案
- 提案手法は二つのGNNを用意しメタ学習を行う
  - 一つ目のGNNは観測済みのノードと未観測のノード間のリンク予測 
  - 二つ目のGNNは未観測のノード同士のリンク予測を行う
  - Meta-learningの枠組みの中でシュミレーションを用いて未観測のノードを生成
  - 不確実性を考慮するため, 未観測のノードのembeddingについて分布の学習を行う
  - さらにlong-tail分布をモデル化するため転移学習を用いる
- FB15K-237, NELL-995, WN18RRという三つのナレッジグラフ, DeepDDI, BIOSNAP-subという二つのドラッグ間相互作用グラフを用いて実験

**提案手法**
- グラフをシミュレーションされた未観測ノードと本物の未観測ノードに分割
- シミュレーションした未観測ノードからのサンプリングでタスクを生成
- tripletsをサポートセット $$\mathcal{S}_i$$, クエリセット $$\mathcal{Q}_i$$

