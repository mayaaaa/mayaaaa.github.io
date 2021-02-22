---
layout: post
title: Benchmarking Deep Learning Interpretability in Time Series Predictions 
tags: [NeurIPS20]
---

<!--more-->

[PDF](https://papers.nips.cc/paper/2020/file/47a3893cc405396a5c30d91320572d6d-Paper.pdf)

**イントロ**
- 説明可能なモデルは多数提案されているが, 説明性の評価は正解がないため難しい
- 特に時系列データだとこれが問題になる
  - 画像や文章のようにsaliency mapやattentionを使った可視化ができない
- 特徴量の一部を隠して予測精度がどれぐらい落ちるか確認する
- 実験を通して以下を確認した
  - 画像に対しては有効なsaliency map手法が時系列においてはその限りでない
  - saliency mapは各々のタイムステップにおいて重要な特徴量とそうでないものを見分けられない
    - あるタイムステップで一つの特徴量が重要と見做されるとそれ以外の特徴量 
  - モデルの構造がsaliency mapの出力に大きく影響する
- 重要な特徴量を正解として含む人工データを生成し評価に使用
- saliency map手法の後段で使える手法を提案 
  - タイムステップごとにtime-relevance scoreを計算する
  - time-relevance scoreがある一定値を超えていたら各特徴量ごとにfeature-relevance scoreを計算する
  - 最終的なscoreをtime-relevance scoreとfeature-relevance scoreの積でモデル化

**提案手法**
- Modification-based evaluation metricsには二つの問題がある
  - 特徴量のランキングが重要度を表すという仮定を置いている~
  -> 特徴量をひとつづく抜く代わりに一定の割合づつ抜く方法を取る
  - 特徴量を削除することでテストデータの分布が変わるためテストデータと訓練データのi.i.dが破れる
  -> 人工データと元データの分布に基づくマスクを使っているのでi.i.dの仮定を破らない
- 説明性の評価にはAUR, AUPを使った
  - 異なる劣化 (精度の低下)レベルにおけるprecisionとrecallの値を用いてcurveを描く
- 時間・特徴量ドメインが融合している場合は既存のsaliency map手法ではうまくいかない
  - 図8(a)は画像向けのsaliency map手法を多変量時系列に適用した結果
    - CNNはうまくいっているがTCNは各タイムステップにおける特徴量の重要度を捉えられていない
  - 図8(b)は多変量を二変量と一変量に変換した場合の結果

**所感**
- 提案手法はかなりシンプル, モチベーションを語る章で提案手法の限界を示した&評価方法をデザインしたのが貢献

