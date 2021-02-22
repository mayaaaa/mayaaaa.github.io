---
layout: post
title: Community Interaction and Conflict on the Web
tag: [WWW18]
---

<!--more-->

[PDF](https://arxiv.org/pdf/1803.03697.pdf)

[Code and Data](https://snap.stanford.edu/conflict/)

**イントロ**
- 時変グラフにおけるpath failureをあてる
  - グラフとして道路ネットワーク, 通信網などを想定
  - path failure = 道路ネットワークにおける経路の混雑, 通信網における (ハードウェアの故障などによる)通信経路の断絶
- グラフ構造だけでなくノードに載っている情報も使う
  - 例) 道路ネットワークにおける traffic density
- ダイナミックに時変するノード情報とグラフ構造をモデル化するため, Long Short-Term Memory R-GCN (LRGCN)を提案
- ある時刻におけるグラフのスナップショット内での関係 (iner-time relation)と時間的に隣接するグラフ同士の関係 (intra-time relation)の双方を考慮

**提案手法**
- グラフ上の長さ mのpath 
  path <img src="https://latex.codecogs.com/svg.latex?\Large&space;\{v_1,v_2,...,v_m\}" />が時刻 tにおいてfailureかavailableかを判定する
  - v_jはノードID
- グラフ上の任意の pathについて, Mつ前から現在までの時刻における pathの系列から Fタイムステップ後までに当該 pathがfailureしたかどうかをあてる
  - pathの系列を入力とする0/1の分類タスク 
  - 損失関数はクロスエントロピー
- ノード間の相関, グラフ構造の時間変化, ノードの時間変化 を考慮するため, GCN + LSTMモデルを用いてグラフの系列から各時刻におけるノードの潜在ベクトルを抽出
- 各々のpathをノードの潜在ベクトルの系列で書き換え, LSTMをかける
- LSTMの出力にさらに attentionをかけて pathの特徴量を抽出 -> 損失関数につっこむ 


