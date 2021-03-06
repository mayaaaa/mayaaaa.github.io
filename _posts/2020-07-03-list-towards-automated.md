---
layout: post
title: Towards Automated Neural Interaction Discovering for Click-Through Rate Prediction
tags: [KDD20]
---

<!--more-->

**イントロ**
- クリック率の予測はリアルタイム入札, ウェブ広告, 検索エンジンの最適化などの応用で重要 
- 既存手法はexplicit featureとexplicit featureの相互作用をMLPで学習するものが多い
- 最近の研究ではダイアモンド構造を持ったMLPがトライアングル構造のものよりも有効だという結果が出ている 
- ニューラルネットワークのアーキテクチャを最適化するNeural Architecture Search (NAS)が発展している
- 相互作用を発見するためのNASの利用にはいくつか課題がある
  - CVタスクにおける画像特徴量と違ってクリック率の予測に使う特徴量は異種で高次元でスパースなものとデンスなものが混じっている
  - また, 既存のクリック率予測においては非構造化された探索空間が用いられている
  - さらにクリック率予測モデルの訓練には数十億以上のデータが使われる
  - 構造の異なるクリック率予測モデルでも精度はそこまで変わらないという報告がある -> NASで細かいモデルの違いを区別したい
- AutoCTRというモデルを提案
  - ランク学習を使う
  - サンプリングとハッシュサイズの削減で探索スピードを上げた

**提案手法**
- 2段階の階層構造を持った探索空間を構築しそれらをDAGでつなぐ
  - 内側の探索空間はユニット数などのハイパラ, ブロック間のつながりは外側の探索空間で探索する
  - 図1のように複数のブロックとブロック同士をつなぐワイヤで構成する
- ブロックを構築する際は機能性と複雑性を考慮する
- これらの要請を満たす3つのモデル (MLP, DP, FM)をブロックとして用いる
- ブロック以外には入力の選択 (デンス/スパース, 両方), ブロック同士のつながり, 各ブロックのハイパラを探索する
- 4つの要素を組み合わせを表すベクトルを用意
- 探索器は進化的アルゴリズムとランク学習を組み合わせたもの

**実験**
- Criteo, Avazu, KDD Cupの3つのベンチマークデータを使用
- 図4は探索したモデルの数に対するloglossの減り方
  - AutoCTRは探索の効率で既存手法を上回る
- 表3では一つのデータで探索したベストなモデルを他の二つのデータに転用して精度を評価した
  - 転移学習の設定においても提案手法は良い精度
- 図6は探索で見つけたベストなモデル
  - ダイアモンド構造のネットワークが推定されている -> これは先行研究の分析結果と一致 


