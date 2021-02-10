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
- 

