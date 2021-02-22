---
layout: post
title: Open Intent Extraction from Natural Language Interactions
tag: [WWW 2020] 
---

<!--more-->

**イントロ**
- 音声認識サービスにおいては人の発言の意図を理解するのが大事
- 既存手法ではマルチタスク分類手法を用いてユーザの意図を理解するものが多い (ラベル付きデータを使用)
- しかしこれらの手法は新たな意図のカテゴリに対処することができない
- また, 既存手法は入力テキストが一つの意図を表現していると仮定している
- 本稿はOPINEという手法を提案
  - 事前に意図のクラスを定義する必要がない
  - 複数の意図を検出できる
- ユーザの投稿や発話から未知の意図を検出するタスクを「Open Intent Discovery」と定義する
  - 例) カスタマーサポートへの投稿に優先順位をつける, メールや議事録のaction itemにスポットを当てる
  - 例えば "Please make a 10:30 sharp appointment for a haircut"は予約するという一つの意図,<br> 
    "I would like to reserve a seat and also if possible, request a special meal on my flight"はシート予約と食事リクエストの二つの意図が含まれる
- 最近の研究で似たような問題を解いているものもある
  - ただし意図そのものを検出することはできない
  - また, 二つ以上の意図は扱わない 
- 本研究ではOpen Intent Discovery問題をsequence taggingタスクとして解く
- LSTMの上にCRFを載せたニューラルモデルを提案
- 提案手法はドメインに関係なくユーザの意図を検出できる
- さらに提案モデルの低レイヤー部分の学習に adversarial trainingを使う
- この定式化によって, ラベルが十分でない時も効果的な cross-domain adaptationができる
- 意図理解のベンチマークデータは実世界のノイズと複雑性を捉えられてない
- 本研究ではStack Exchangeのデータを使う (意図はクラウドソーシングでアノテーション)

**提案手法**
- 意図をactionとobjectの二つで定義
  - "Please make a 10:30 sharp appointment for a haircut"のobjectはappointment, actionはmake
  - "I would like to reserve a seat and request a special meal on my flight"のobjectはseatとspecial meal, actionはreserveとrequest
- その上でOpen Intent DiscoveryをAction, Object, Noneの3つのタグを用いたsequence taggingタスクとして定式化
- シンプルなPOS taggerやOpenIE, SRLとは少し違う問題を解く
- まずCNNを用いて文字と単語のembeddingを行う
- また, ノイズに対処するためにadversarial trainingを使う
- CNNの上にattention mechanismをかませ, さらにattentionの出力をCRFの入力として使う
- CRFでAction, Object, Noneタグを予測したら最後に意味のあるフレーズに変換 <- 単語同士の近さを使って分類するシンプルな手法とMLPを使う手法を2つ提案

**所感**
- イントロの書き方うまい (open world $$\leftrightarrow$$ closed worldの説明など)
- タスクの新規性＆応用上の重要性とクラウドソーシングを使ってラベル付きデータを集めた点がBest paper受賞につながった?


