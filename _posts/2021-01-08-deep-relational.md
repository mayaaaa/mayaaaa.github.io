---
layout: post
title: Deep Relational Topic Modeling via Graph Poisson Gamma Belief Network 
tags: [NeurIPS20]
---

### [PDF](https://proceedings.neurips.cc/paper/2020/hash/05ee45de8d877c3949760a94fa691533-Abstract.html)
**イントロ**
- グラフ関連のタスク (リンク予測など)では予測の不確実性をモデル化するのが重要
- グラフのモデル化に広く使われるモデルとして潜在空間におけるnodeとedgeの関係を考慮するもの (relational topic model)がある
- RTMは浅いネットワークを使っているので表現力に限界がある
- LDAの代わりに多層のネットワークを使って意味的な関係性を表現する手法が流行っているが, RTMには適用されていない
- 別の発展としてVAEをグラフに応用したVGAEがある
- これらを組み合わせたモデルを提案

**提案手法**
- ベースラインはGraph Poisson factorモデル
  - 文章 ($$K_0$$の単語のセット) $$x_i$$の系列 (N個)を入力とする
  - トピック$$\Psi$$と$$\theta_i$$に分解
  - ディリクレ分布を$$\Psi$$のpriorとして使う
  - $$\theta_i$$のpriorはgamma分布
- Graph Poisson gamma belief network (GPGBN)はTつの隠れ層を使ってこのモデルを拡張したもの
  - $$\theta_i$$が一つ上の層の$$\Psi$$と$$\theta_i$$の内積から生成されるという仮定
  - GPGBNは全てのパラメータの事後分布を解析的に解ける
- GPGBN (decoder)と2つのワイブル分布ベースグラフ推論モデル (decoder)を組み合わせる 
- 二つのワイブルグラフAEができる

**実験**
- 6つのベンチマークデータを使用


