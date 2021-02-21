---
layout: post
title: "CaSPR: Learning Canonical Spatiotemporal Point Cloud Representations"
tags: [NeurIPS20]
---

<!--more-->

## [PDF](https://papers.nips.cc/paper/2020/file/9de6d14fff9806d4bcd1ef555be766cd-Paper.pdf)
**イントロ**
- 時空間的に変化する幾何オブジェクトの再構成が重要
- staticな三次元の観測や時変するpoint cloudから物体の形を学習する手法が提案されている
- しかし時間的な連続性, ロバスト性, カテゴリレベルの一般化ができていない
- 時空間の変化をencodeするオブジェクトの表現を学習する手法を提案
  - depth sensorsやLIDARで観測されたpoint cloudは時間・空間的にスパース
- 時空間の表現として望ましい性質は時空間の連続的な変化を捉えられること, 非規則的なサンプリングパターンにロバスト, 
カテゴリー内の見たことないオブジェクトや観測されていない時間への一般化

**提案手法**
- 連続時空間表現
  - TPointNet++によるembedding zを$$z_{ST}$$と$$z_{dyn}$$の二つに分割して使う
  - $$z_{dyn}$$をLatent ODEの初期値$$z_0$$として使う
  - ODEを解くことで$$z_0$$を時刻 $$T$$まで時間発展させ, $$z_T$$における連続的表現をはく 
  - $$Z_{ST}$$と$$Z_T$$の積$$z$$で時空間的な変化を表す
- 時空間生成モデル
  - 点群の生成には数々の手法が提案されているが, 4Dの時空間点群にはそぐわない
  - そこでContinuous Normalizing Flows (CNF)を使う
   - 観測されていないデータをサンプルできる
  - JJFORDの実装を使用 ()
  - 時刻 $$t=0,...,T$$までLatent ODEで3Dシェープの系列を生成する
  - Gaussianから変数 ykをサンプルしそれをztの条件付きflow $$g_{\beta}(y_k|z_t)$$に渡す
