---
layout: post
title: Identifying Sepsis Subphenotypes via Time-Aware Multi-Modal Auto-Encoder
tags: [KDD20]
---

<!--more-->

[PDF](https://dl.acm.org/doi/10.1145/3394486.3403129)

**イントロ**
- 敗血症 (感染症に起因する生命を脅かすような臓器障害)は死因の半数を占めている
- 介入に対する反応が個人で違うため敗血症の患者の扱いは難しい
- subphenotypeの同定が重要
- 図1は電子健康記録の例
  - 属性, 診断, バイタルサインの系列などからなる
- 既存手法は重要な変数を集約しそれに基づいて患者を分類
- これらの手法は (i) 時間性を無視している (ii) 欠損値に対処できない という課題がある
- 提案手法は Time-Aware Multi-modal auto-Encoder (TAME)でまず欠損を埋める
- その後dynamic time wrapping (DTW)で患者同士の時間的類似度を測る
- 最後にweighted k-meansで患者を分類する
- DACMIとMIMIC-IIIという二つのパブリックデータで実験
- 欠損値の補完とk-meansによる分類で患者の分類精度を上げることができた

**提案手法**
- TAMEは複数種類の変数 (属性, 診断, バイタルサイン)を入力に取りベクトルを出力する
  - 欠損を表すマスク ctを導入
  - 変数と観測間のtime gapを三角関数を使ってembedding
  - それぞれの変数に関する特徴量が得られたらconcatinate -> max-pooling -> 双方向LSTM
  - time gapに関する特徴量を変換しattentionをかける
  - 観測との二乗誤差を最小化するパラメータを学習
- 欠損値補完が終わったらDTWで時系列間の関連性を判断しk-meansでクラスタリング

**実験**
- DACMIとMIMIC-IIIという二つのパブリックデータを使用
- 欠損値補完の精度をRMSEで評価
  - 表1, 2は二つのデータにおける各々の変数の補完精度 
- 図4は患者のクラスタリングの結果
  - 正解ラベルがないためラベルなしのデータに適用できる指標 (Calinski-Harabasz IndexとDavis-Bouldin Index)を使った 

