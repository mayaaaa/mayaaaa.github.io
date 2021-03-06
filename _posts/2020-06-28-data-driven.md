---
layout: post
title: A Data Driven Graph Generative Model for Temporal Interaction Networks
tags: [KDD20]
---

<!--more-->

[PDF](https://dl.acm.org/doi/10.1145/3394486.3403082)

**イントロ**
- グラフの生成は重要なタスク
- 伝統的なグラフ生成モデルは特定の構造を仮定したもの
- 最近は深層生成モデルが使われている
- しかしこれらの手法はstaticなネットワークのために設計されたもの
- 実際のネットワークは本質的にdynamicであり, 時刻情報付きのシステムログの集合として保存されている
- 時変ネットワークのモデル化には時刻情報を丸めてグラフのスナップショットとしてモデル化する手法が取られる
- この手法の欠点は適切な時間粒度が不確実なこと
- 粒度が細かすぎるとスナップショットの数が増え計算コストがかかる
- 粗すぎると時間に関する情報が失われる可能性がある
- 本研究では以下のリサーチクエスチョンに取り組む
  - (Q1) 時間情報付きのエッジの系列をそのままモデル化できるか?
  - (Q2) グラフの構造と時間的特徴を保持したend-to-endの深層学習モデルを構築できるか?
- TagGenという手法を提案する
  - 時間的・構造的特徴を入力データから取得するためのランダムウォークサンプリングを提案
  - その上にbi-level self-attentionメカニズムを載っけた
  - さらにネットワークのcontextを生成する (ノード・エッジの削除・追加を行う)スキームを構築した

**提案手法**
- 提案手法は4つのステージからなる
  1. Sampling ランダムウォークでグラフから系列を抽出
  2. Generation ノード・エッジの削除・追加に対応する操作を定義し, 人工的な系列を生成
  3. Discrimination 生成されたグラフが入力と似た構造になっていることを補償するため, discriminatorモデルを適用
  4. Assembling ここまでの操作で生成されたランダムウォーク系列から時刻ごとの相互作用の頻度 (エッジ数)に基づきグラフを構築する

**実験**
- 7つのネットワーク時系列データを使って実験
- 6つのグラフ測度を考慮し生成されたデータと入力データの差を各測度ごとにMAPEで比較
- 図7に6つのグラフ測度それぞれについての誤差をプロット
  - 提案手法は全てのデータ, 全ての測度で既存手法より小さい誤差
- 図8はBITCOINデータにおけるタイムステップごとの測度の変化をプロットし実測と比較したもの
  - 提案手法は実際のカーブにうまくフィットしている 
- SOデータを用いてデータ拡張の設定においてanomaly detectionとリンク予測の精度を評価
  - データ拡張の設定において比較手法を上回る精度 
