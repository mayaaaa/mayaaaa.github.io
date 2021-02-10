---
layout: post
title: Teaching a GAN What Not to Learn
tags: [NeurIPS2020]
---

### [PDF](https://papers.nips.cc/paper/2020/hash/29405e2a4c22866a205f557559c7fa4b-Abstract.html)
**イントロ**
- GAN (Generative adversarial networks)の学習はdivergenceの最小化に等しい
  - 最適なgeneratorは生成されたデータと真のデータの分布の違いを最小化するもの
  - 真のデータの分布を$$p_d$$, 生成したデータの分布 $$p_g$$とおく
- LSGANではdiscriminatorを回帰モデルとする
  - 生成されたデータにラベル a, 真のデータにラベル bを付与
  - Generatorはラベルcに分類されるようなデータを生成する
- LSGANにおいて最適なgeneratorは $$2p_d$$と $$p_d+p_g$$の Pearson-$\chi^2$ 誤差を最小化するようなものに相当
- Conditional GANはGANを教師ありに拡張したもの
  - Generatorとdiscriminator両方にクラスラベルを入力
- それ以外のアプローチとしてはデータを正負に分け識別するものがある
  - Metric learningやrepresentation learningではサンプル間の距離をニューラルネットの学習に使う
  - Contrastive lossはサンプル間の類似度を計算し似ているものには正のラベル, 似ていないものに負のラベルを付す
  - Triplet lossでは正のクラスからの距離を最小化&負のクラスからの距離を最大化するような学習を行う
- Complementary CGAN (CCGAN)は補完的なラベルがついているサンプルを学習する
- Generative positive-unlabelled learning (GenPU)は半教師ありGAN
  - 正もしくは負のラベルあり+ラベルなしデータを入力とし, 正のラベルなしデータを負のデータから区別することを目的とする
- 一般的なGANは適当なgenerator見つけるのをゴールとしているが, GCGANやGenPUの最終目的は適当なdiscriminatorを見つけること

![GSD1 phenotype](_site/assets/Rumi-GAN.png)

**提案手法**
- 本研究は詩人ルーミーの ``The art of knowing is knowing what to ignore''という言葉に動機づけられたもの
- 

