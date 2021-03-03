---
layout: post
title: "Neural Datalog Through Time: Informed Temporal Modeling via Logical Specification"
tags: [ICML20]
---

<!--more-->

[PDF](http://proceedings.mlr.press/v119/mei20a.html)

[Video](https://icml.cc/virtual/2020/poster/6481)

**タスク**
- データベースが時間とともにどのように変化するかをモデル化
  - ここではオブジェクトの性質あるいはオブジェクト同士の関係を表すデータベースを想定する
    - 例えばイブはリンゴが好き, アダムはリンゴが好き, イブとアダムは関係がある etc 
  - データベースは事実 (fact)の群からなり各々のfactが潜在空間に埋め込まれている
  - このようなデータベースはイベントが起きる度に更新される
    - 新しいfactが観測されるとそれに基づいて他のfactの潜在ベクトルが変化する場合がある
- どのfactがどのfactに影響を与えるか事前知識を持っているケースを考えこれを利用してデータベースの時間発展を記述する

**既存手法**
- イベント系列の予測には確率生成モデルが, 一定間隔で観測された系列にはマルコフモデル, LSTM等が用いられる 
- これらのモデル化ではイベント $$e_i$$が観測されるごとに潜在状態 $${\bf s}_i$$が $${\bf s}_{i+1}$$に更新される
- 次のイベント $$e_{i+1}$$の分布は $${\bf s}_{i+1}$$に基づいて決まる
- イベントの種類が膨大な場合, あるいはイベントの種類が少ない場合, イベントと潜在状態の関係を学習するのが困難

**提案手法**
- どのfactがどのfactに影響しうるかを記述するため, Datalogというデータベース言語を用いる
  - 関連のある情報同士を予めリンクで結び, 関連情報への高速なアクセスを可能にするグラフデータベースが複数存在する
  - 一階述語論理を記述できる演算データベース言語としてDatalogが提案されている 
  - 例えば"イブとアダムがリンゴを好きならイブとアダムは関係がある"という命題を表す場合Datalogでは
    $$\require{color}
   \texttt{compatible(eve,adam)} {\color{orange}\text{ :- }} \texttt{likes(eve,apples)}, \texttt{likes(adam,apples)}$$
  - Factには好きか嫌いかといった二値以上の情報も含まれる (論文中では青文字で記述)
    $${\color{blue}\texttt{rel(eve,adam)}} {\color{orange}\text{ :- }} {\color{blue}\texttt{opinion(eve,apples)}}, {\color{blue}\texttt{opinion(adam,apples)}}$$
- Factとfactの関係を表す式をruleと呼ぶ
- Ruleの種類としてdeductive rule, triggering ruleの二種類を定義
  - Deductive ruleは"if"を表し以下の形式で記述される  
    $$\texttt{new fact}{\color{orange}\text{ :- }}\texttt{old fact}_1,\texttt{old fact}_2$$
    - データベースの中に既に $$\texttt{old fact}_1$$, $$\texttt{old fact}_2$$が含まれていた場合に $$\texttt{new fact}$$はデータベースに追加される
  - Triggering ruleは"when"を表し以下の形式で記述される
    $$\texttt{new fact}{\color{green}\text{ <- }}\texttt{event},\texttt{old fact}_1,\texttt{old fact}_2$$
    - データベースの中に既に $$\texttt{old fact}_1$$, $$\texttt{old fact}_2$$が含まれておりかつ $$\texttt{event}$$が起きた時に 
     $$\texttt{new fact}$$をデータベースに追加
    - 同じ仕組みで $$\texttt{new fact}$$をデータベースから削除することもできる
- 各々のfact (例えば$$\texttt{eve}$$と$$\texttt{adam}$$の関係)について潜在ベクトル $$[\![\texttt{rel(eve,adam)}]\!]$$が存在する 
  - 関係性がない場合は $$[\![\texttt{rel(eve,adam)}]\!]=\texttt{NULL}$$
- 潜在ベクトルはこれまで起きたイベントの影響で時間とともに更新されていく
  - 例えば$$\texttt{eve}$$と$$\texttt{adam}$$の $$\texttt{apple}$$に関する意見 $$\texttt{opinion(eve,apple)}$$,  $$\texttt{opinion(adam,apple)}$$が観測されたとする
  - このような場合, これらの意見の潜在ベクトル $$[\texttt{opinion(eve,apple)}]$$, $$[\texttt{opinion(adam,apple)}]$$を変換し結合することで
    $$\texttt{eve}$$と$$\texttt{adam}$$の関係を表す潜在ベクトル $$[\![\texttt{rel(eve,adam)}]\!]$$を更新する
  - $$\texttt{eve}$$と$$\texttt{adam}$$が他のトピックについても意見を持っている場合 (例えば$$\texttt{politics(eve,apple)}$$,$$\texttt{politics(adam,apple)}$$など), 
   これらの意見の潜在ベクトル $$[\texttt{politics(eve,apple)}]$$,  $$[\texttt{politics(adam,apple)}]$$の寄与も足し込む
  - その際non-linear poolingを使用
- 潜在ベクトルの連続的な時間変化を記述するためneural Hawkes processを使用
  - Neural Hawkes processはLSTMとHawkes過程を組み合わせたモデルであり, イベントが起きる度にLSTMの潜在状態を更新する
  - インテンシティはLSTMの潜在状態と時刻 $$t$$に依存
- あるイベントが起きたらデータベースにfactが追加される
- それに伴い, そのfactのインテンシティ $$\lambda_{e}(t)$$と対応するLSTMを作成
  - LSTMの潜在状態が各々のfactの潜在ベクトルに対応
  - LSTMの各タイムステップで上記の計算を行いruleに基づいて潜在状態を更新
- 最尤推定でモデルのパラメータを最適化 
  - 目的関数として各々のfact (イベントの種類)についてのインテンシティの対数尤度を全てのfactについて足し上げたもの

**実験**
- IPTV, RoboCupという2つのデータセットを使用
- IPTVは1000人のユーザ $$\texttt{U}$$のテレビ視聴 $$\texttt{P}$$履歴
  - テレビ番組は各々 $$\texttt{action}, \texttt{comedy}, \texttt{romance}$$等のタグを持つ 
  - この関係は $$\texttt{has_tag}(\texttt{P},\texttt{T})$$で表される
  - この関係式を用いて以下のルールを定義する
    1. 各々のタグの潜在ベクトルは関連するプログラム $$\texttt{P}$$の潜在ベクトルに影響する
    2. 番組視聴履歴に基づいて時間とともにタグの意味が変わる
  - さらに番組が公開される前は視聴できないためこれを表す倫理式を使用
- RoboCupはロボットによるサッカーの試合
  - サッカーについてのルールを考慮
  - 例えばプレイヤー $$\texttt{P}$$が $$\texttt{Q}$$にパスをした場合 
    - $$\texttt{P}$$はボールを持っていないはず $$\texttt{!has_ball(P)}$$
    - $$\texttt{Q}$$がボールを持っているはず $$\texttt{has_ball(Q)}$$
- イベント予測精度について負の対数尤度, 予測時刻と観測時刻のRMSE, イベントの種類予測の誤差率で評価
- 3つの評価指標で既存手法を上回る精度 (図2)


