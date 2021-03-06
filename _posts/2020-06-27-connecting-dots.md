---
layout: post
title: "Connecting the Dots: Multivariate Time Series Forecasting with Graph Neural Networks"
tags: [KDD20]
---

<!--more-->

[PDF](https://dl.acm.org/doi/10.1145/3394486.3403118)

**イントロ**
- センサーの広がりによって気温, 価格, 交通速度, 電気利用料など様々な変化が記録できるようになっている
- 複数のドメインで取得された時系列は複数の時系列として表すことができる
- これらは互いに関連している
- 多変量時系列モデルは変数間の依存性を仮定している
  - 例えばVARやGPは変数間の関係に線形性を仮定している
  - LSTNetやTPA-LSTMなど深層学習ベースの手法は変数同士のペアワイズな関係を明示的にモデル化することができない $$\rightarrow$$ 説明性が低い
- 多変量時系列をグラフという観点から見直す
  - 変数=ノード, 変数間の関係=隠れたエッジ
- 時空間GCNを適用したいが, いくつか課題がある
  1. グラフ構造が未知
  2. もし既知だとしてもそれが最適でないという発想がない (学習しない)
- 課題 iに対しては新しいグラフ学習レイヤーを提案する
- グラフ構造を含めた全パラメータ学習をできるフレームワークを構築することで課題 iiに対応する

**提案手法**
- 提案手法はgraph learning layer, $$m$$つのgraph convolutionモジュール, $$m$$つのtemporal convolutionモジュールからなる
- Graph learning layerでは時系列間の関係を表す隣接行列を学習する
  - コスト削減のためサンプリング手法を使い, ノードのサブ集合間の関係のみを考慮する
  - ノードのembeddingを学習しそれらの非線形変換の内積で隣接行列をモデル化 
  - 隣接行列の値のうちトップ k以外は0にする

**実験**
- マルチステップ予測とシングルステップ予測の二つのタスクについて四つのベンチマークデータを使って精度評価
- 既存手法はシングルステップ予測にはAR, GP, LSTNet等を, マルチステップ予測にはGCNベースの手法を中心に用いる
- 図6にケーススタディの結果
  - 図6aは隣接行列をfixした時の時系列 (55番目のノードとその近隣ノード3つ), 図6bは隣接行列を学習した結果
  - 図6cはそれらのノードの場所を地図上に可視化したもの (緑が学習で推定した近隣ノード, 黄色が事前に定義された近隣ノード)
  - 図6cを見ると事前に定義した近隣ノードは55番目のノードに地理的に近い場所にあるのに対し学習された近隣ノードは地理的には遠いが同じ道路上にある
  - そのため図6aでは4つのノードの時系列が同時に変化しているのに対し図6bでは時差付きの相関が見られる
  - 学習した図6bの方が実際の異常時の道路状況をよく捉えている


