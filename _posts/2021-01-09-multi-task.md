---
layout: post
title: Multi-task Causal Learning with Gaussian Processes 
tags: [NeurIPS20]
---

### [PDF](https://papers.nips.cc/paper/2020/file/45c166d697d65080d54501403b433256-Paper.pdf)
**イントロ**
- 意思決定において介入実験が重要
- 図1のように収穫量 $$Y$$は肥料 $$X$$, 異なる時刻における虫の率 $$Z=\{Z_1,Z_2,Z_3\}$$で決まる
- 実験を繰り返すことでintervention functionを学習する
- ナイーブにはintervention functionを各々モデル化することができる
- しかしこのアプローチは実験ごとの出力間の相関を考慮できない
- intervention functionは相関している
  - 例えばintervention set $${X, Z_1}$$について実験をした場合, $$X$$もしくは $${X, Z_1, Z_2, Z_3}$$を変化させた場合の情報も得られる
- 因果推論とマルチタスクラーニングを組み合わせたフレームワークを提案
- 確率的因果推論では実験が難しい時にd分離を使って介入効果の推定をする
- d分離では各々のintervention functionを独立に扱う
- Multi-task GPは出力同士の相関をモデル化するのに使われる

**提案手法**
- 確率的構造方程式モデルでは内生変数 $$v$$, 外生変数 $$u$$, (決定的)関数 $$f$$, 外生変数の分布 $$p(u)$$の4つの変数がある
- 関数$$f$$と分布$$p(u)$$から分布$$p(v)$$が決まる
- intervention functionsをTと置く

