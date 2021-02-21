---
layout: post
title: Non-reversible Gaussian processes for identifying latent dynamical structure in neural data
tags: [NeurIPS20]
---

### [PDF](https://papers.nips.cc/paper/2020/hash/6d79e030371e47e6231337805a7a2685-Abstract.html)
**イントロ**
- 高次元の神経作用は低次元の潜在状態の時間変化で記述することができる
- 既存手法は2つのカテゴリに分けられる
- 1つ目は潜在状態の時間発展をマルコフモデルで記述する手法
  - 線形力学系, 確率的深層学習, 遷移行列のノンパラ推定を含む
  - これらの手法は学習に時間がかかる
- 2つ目は潜在状態を直接確率過程でモデル化する手法
  - 主成分分析をガウス過程に拡張したGaussian-process factor analysis (GPFA)など
  - 観測値と潜在変数との非線形な関係を捉える
  - GPベースの手法は効率的な学習が可能&uncertaintyを解析的に計算できる
  - ただしスムーズな状態の変化しか記述できない

**提案手法**
- $$N$$次元の観測データ $${\bf y}(t)$$が $$T$$つの時刻 $$t$$ごとに与えられている
- GPFAでは観測データが$$M$$次元の潜在状態の軌跡から生成されていると仮定
  - 各々の軌跡をGPで記述
  - 潜在状態の独立性を仮定
  - 潜在状態間の関係を捉えることができない
-  

