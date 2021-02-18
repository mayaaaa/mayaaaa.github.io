---
layout: post
title: Deep Multimodal Fusion by Channel Exchanging 
tags: [NeurIPS20]
---

## [PDF](https://papers.nips.cc/paper/2020/file/339a18def9898dd60a634b2ad8fbbd58-Paper.pdf)

**イントロ**
- 深層学習を用いたmultimodal fusionがsemantic, segmentation, action recognition, VQAなどの分野でメジャーになっている
- 既存手法はaggregationベースのものとalignmentベースのもの二種類に分けられる
  - Aggregationベースの手法はaveraging, concatenationを用いて複数のモーダルを入力とするサブネットワークを一つのネットワークにまとめる
  - Alignmentベースの手法はモーダルごとのネットワークについて一部を共通化するような制約をかける
- Aggregationベースの手法は個々のモーダルの特性を十分に捉えることができない
- Alignmentベースの手法はしばしばfusionの齟齬を起こす
- サブネットワーク間のチャンネルを動的に交換するChannel-Exchanging-Network (CEN)を提案
  - Pruning等で用いられる``smaller-norm-less-informative''の仮定に基づく手法
  - チャンネルごとにBatch-Normalization (BN)のscaling factor $$\gamma$$を導入しこれが0に近い場合そのチャンネルを他のモーダルの平均で置き換える
- 提案手法のCENはBNレイヤー以外の全てのサブネットワークパラメータをモーダル間で共有することができる
  - サブネットワークを独立に学習する手法と畳み込みパラメータを共有する手法を提案
- RGB-Dデータのsemantic segmentation, 画像翻訳の二つのタスクにおいて提案手法の性能を評価 

**提案手法**
- 

