---
layout: post
title: KDD 2019 Papers Memo
tags: [KDD2019]
---

## Links
[KDD 2019 Accepted Papers](https://www.kdd.org/kdd2019/accepted-papers)  
[KDD 2019 Papers with ArXiv Links](https://leenashekhar.github.io/2019-06-25-KDD-2019-papers/) 

---
## PerDREP: Personalized Drug Eﬀectiveness Prediction from Longitudinal Observational Data  
### [PDF](https://astro.temple.edu/~tua87106/kdd19.pdf)
 

---
## Deep Landscape Forecasting for Real-time Bidding Advertising
### [PDF](https://arxiv.org/pdf/1905.03028.pdf)


---
## TUBE: Embedding Behavior Outcomes for Predicting Success
### [PDF](https://dl.acm.org/authorize?N689598)
**イントロ**
- タスク：ある試行が成功するか否かの予測
  - 例) 論文がKDDに通るか否か？
- 例えば次の論文がKDDに通るかどうかを考える
  - トピックは "social media"
  - 筆頭著者は stanfordの学生
  - 最終著者は Jure
  - 問題設定はツイートの人気度の予測
- オンライン上の学術データが利用可能になっている
- 本研究では goalに対する planの成功度を予測する
- 学術論文以外のドメインにも適用可能な手法を構築する
- 3つの課題がある
  - planと goalの低次元特徴量を抽出する必要がある
  - planはベクトル場上で評価すべき. ネットワーク構造に基づく測度は使えない
  - 失敗 (negative sample)は観測されない
- 上記の課題を解決する新たな手法 (TUBE)を提案する
- アイデアはベクトル場を新しい方法で扱うこと
  - TUBEはベクトル場上で意思決定を navigateする
  - 例) 原点から始まって context items (第一著者, 問題設定)を追加 -> 星印のゴールにたどり着くために必要な context items (コラボレーター, キーワード)を追加 (図1の緑の線)
- 成功は点ではなく半直線で定義される
  - planの達成レベルを評価することができる (つまり余裕で成功したのかぎりぎりだったのか) 
- Context itemsと planの embeddingを同時に学習する
  - Positive examples (論文の記録)が "1"の効果を持っているとする
  - Word embeddingでよく使われる negative samplingを使う
    - Negative examplesを生成しそれらが小さな効果を持っているとする 


**提案手法**
- Context itemsを p={c_1,c_2,...,c_n}と定義
- 各々の context itemsを embeddingしてベクトル和を取り plan pを得る
- 成功を表す半直線を定義
- その近くに plan pがあるほど成功度 εも高いとみなす
- 成功度 εをtanh関数を使って 0から1の値に変換 (0が失敗, 1が成功)
- KL divergenceを最小化する embeddingを学習

**実験**
- 人工データを用いた実験
  - kつのスキルがあると仮定 
    - 例) k=3ならスキル "a", スキル "b", スキル "c"がある
  - 各 context item (キャラなど)が最大 mのスキルポイントを持っていると仮定
    - 例) m=3の場合, スキル "a"が2ポイント, スキル "b"が1ポイントなど -> この場合 contextを c_aabと書く
  - Goalを達成するために badgeを稼がなきゃいけない設定
  - 各々の badgeは スキルに対応. バッチを一つ稼ぐために xポイント要るとする.  
  - Goalを bedgeの組み合わせとする 
    - 例) Aが二つ, Bが一つ欲しい = Goalは "AAB" 
- 実データ (データマイニング分野の論文データで実験)



---
## Dynamic Modeling and Forecasting of Time-evolving Data Streams
### [PDF](https://dl.acm.org/authorize?N688475)

**イントロ**
- タスク：特定のパターン ("regimes")の連続からなる多次元時系列データのモデル化
  - 例) 運動時のセンシングデータなら jogging/cooling down/resting
  - 例) Human motionデータなら rotating/walking など 
- (i) パターン抽出 (ii) パターン間の関係を推定 (iii) l_s タイムステップ後の時系列予測 する問題に取り組む
- 非線形微分方程式でパターン間の遷移を記述するモデルを提案
  - 遷移の仕方が事変する
- Markov chainや Bayesian networkなど離散的な時間遷移をモデル化する手法と異なり, 連続的な時間遷移を捉えているところがポイント 

**提案手法**
- 背後の潜在状態 s(t)を仮定
- 遷移を


---
## Learning Dynamic Context Graphs for Predicting Social Events  
### [PDF](https://yue-ning.github.io/docs/KDD19-dengA.pdf)

**イントロ**
- 大規模でかつノイズの多いデータからソーシャルイベントを予測する
- 先行研究ではイベントの先駆けとなる指標 (precursors)を検出し予測に用いる手法が提案されている 
- 先行研究の課題
  - 大規模データにおいては precursorの検出が難しくなり, 予測精度が落ちる
  - 過去のイベント同士の関係を考慮していない
- 上記課題を解決するため, ダイナミックGCN手法を提案
  - 過去のイベント系列を表すグラフネットワークをGCNでエンコード
  - entitiesと actionsからなるグラフを生成

**提案手法**
- 各々の regimeを記述する関数 s(t)を導入
- s(t)を常微分方程式でモデル化
  - 初期値 v^{in}を導入
  - v^{out}を導入し, s(t)が v^{out}にある程度近づいたら次の状態に遷移すると仮定


---
## Modeling Extreme Events in Time Series Prediction 
### [PDF](http://staff.ustc.edu.cn/~hexn/papers/kdd19-timeseries.pdf)

**イントロ**
- 時系列のモデル化・予測は重要なタスク
- 既存手法は古くは ARMA, 最近のだとDNNが主流
- しかし時系列に Extreme event (少数のイレギュラーなイベント)が含まれる場合, 
  (a) レギュラーなイベントのみにフィットするようパラメータが学習される (図1aのように thresholdができる) (b) オーバーフィッティングする 等の問題が起こる (図1b)
- DNNの予測精度を上げるため, Extreme eventを考慮する新たな手法を提案
  - 新たな損失関数を提案
  - メモリネットワークを用いて過去の Extreme eventsを記憶する仕組みを導入

**提案手法**
- 入力 x_tと出力 y_tのペアからなる長さ Tの時系列をモデル化
  - 損失関数として二乗誤差を仮定
- 各タイムステップごとに "Extreme event"かどうかを表すラベル v_tを導入
- y_tの従う分布として heavy-tailedを仮定 
- 各々のタイムステップ tごとに windowの系列を M個ランダムに抽出 
  - windowは長さ Δの連続した時系列
- 各々の window w_jをGRUに入力して特徴ベクトル s_jを1つ出力
- 各々の windowに対して window終端の直後のタイムステップで extreme eventがあったかどうか (q_j)を判定する memory networkを学習 
- それとは別に時刻 tまでの時系列を GRUに突っ込んで中間状態 h_tを学習し, h_tを線形変換して特徴ベクトル <img src="https://latex.codecogs.com/svg.latex?\Large&space;\tilde{o}_t" />を得る
-  <img src="https://latex.codecogs.com/svg.latex?\Large&space;\tilde{o}_t" />は extreme eventか否かの情報を含まないので s_jと組み合わせる方法を考える
  - h_tと s_jの内積でアテンション a_tjを算出 
  - <img src="https://latex.codecogs.com/svg.latex?\Large&space;\tilde{o}_t" />と<img src="https://latex.codecogs.com/svg.latex?\Large&space;u_t\sum_{j=1}^M a_{tj}\cdot q_j" />の重み付け和で新たな特徴ベクトル o_tを出力
  - u_tはタイムステップ tの後にextreme eventがあったかどうかを表す
- o_tと y_tの二乗誤差を最小化するようなNNのパラメータを推定
- Extreme Value Theory (EVT)に従って u_tを使って損失誤算のペナルティ項を設計 
- 二乗誤差 + EVTに基づくペナルティで損失関数を定義
 

---
## dEFEND: Explainable Fake News Detection 
### [PDF](http://arxiv.org/abs/1905.03994)

**イントロ**
- SNSにおける fake newsの拡散が問題になっている
  - 2016年米大統領選における "Pizzagate"など 
- SNS上の fake news検出にあたってはいくつかの課題がある
  - わざとミスリードを誘うような書き方がされている
  - SNSデータは大規模でかつノイズが多い
- 最近は fake news検出のためにユーザの反応 (コメントなど)を使う手法が提案されている
- 既存手法は検出のみにフォーカスしたもので, なぜそのニュースが fakeと見なされたのか説明するものではない
- ニュースの内容とユーザのコメントから説明を得るアプローチを提案する
  - ジャーナリストによるファクトチェックは手間と時間がかかる
  - ユーザのコメントは fake newsかどうかを説明するための重要な手がかりになりうる
- 提案手法は(1) ニュースの内容をエンコードするパーツ (2) ユーザのコメントをエンコードするパーツ 
  (3) (1)-(2)の出力に attentionをかけるパーツ (ニュースの内容とコメントの相関を捉え, 本文とコメントから説明可能な top-Kを取ってくる)
  の3つのパーツからなる 

**提案手法**
- Nつの文章からなるニュース記事とそれに紐づいたコメントから
  - fakeか否かの分類問題を解く
  - 文章とコメントの説明可能性をランキングにしたリストを出力 
- (1) ニュースの内容をエンコード: 各文章の単語系列をGRUに入力
- (2) ユーザのコメントをエンコード: 各コメントの単語系列をGRUに入力
- 上記手順でニュースの各文章, 各コメントごとの特徴ベクトルを得る
- (3) 各特徴ベクトルをNNでマッピングしアテンションを出力
- アテンションを重みとして特徴ベクトルの重み付け和を取り, concatinate -> 非線形変換でラベルを出力
- 損失関数はクロスエントロピー

**実験**
- ベンチマークのFakeNewsNetデータを使う
  - データはTwitterユーザのコメントを含む
- 説明性については既存手法の HANにアテンション構造を追加して拡張しベースラインとした
- ClaimBusterを用いて作成したランキングをGround truthとして使用し map@kで比較


---
## 


---
## Predicting Path Failure In Time-Evolving Graphs
### [PDF](http://arxiv.org/abs/1905.03994)

**イントロ**
- 時変グラフにおけるpath failureをあてる
  - グラフとして道路ネットワーク, 通信網などを想定
  - path failure = 道路ネットワークにおける経路の混雑, 通信網における (ハードウェアの故障などによる)通信経路の断絶
- グラフ構造だけでなくノードに載っている情報も使う
  - 例) 道路ネットワークにおける traffic density
- ダイナミックに時変するノード情報とグラフ構造をモデル化するため, Long Short-Term Memory R-GCN (LRGCN)を提案
- ある時刻におけるグラフのスナップショット内での関係 (iner-time relation)と時間的に隣接するグラフ同士の関係 (intra-time relation)の双方を考慮

**提案手法**
- グラフ上の長さ mのpath 
  path <img src="https://latex.codecogs.com/svg.latex?\Large&space;\{v_1,v_2,...,v_m\}" />が時刻 tにおいてfailureかavailableかを判定する
  - v_jはノードID
- グラフ上の任意の pathについて, Mつ前から現在までの時刻における pathの系列から Fタイムステップ後までに当該 pathがfailureしたかどうかをあてる
  - pathの系列を入力とする0/1の分類タスク 
  - 損失関数はクロスエントロピー
- ノード間の相関, グラフ構造の時間変化, ノードの時間変化 を考慮するため, GCN + LSTMモデルを用いてグラフの系列から各時刻におけるノードの潜在ベクトルを抽出
- 各々のpathをノードの潜在ベクトルの系列で書き換え, LSTMをかける
- LSTMの出力にさらに attentionをかけて pathの特徴量を抽出 -> 損失関数につっこむ 


---
## Beyond Personalization: Social Content Recommendation for Creator Equality and Consumer Satisfaction
### [PDF](https://arxiv.org/abs/1905.11900)

**イントロ**
- タスクはSNSにおけるコンテンツ (文章)の推薦
- コンテンツ間の類似度を用いる手法 (Content-based), や協調フィルタリング (CF)がある
- CFに基づく既存手法は Matthew's Effects ("The Rich Get Richer")をもたらす
  - Creatorの公平性は考慮していない
- Creatorの公平性を考慮する研究もいくつかある (例) ゲーム理論に基づくアプローチなど
- ただしこれらのアプローチはユーザの満足度を下げる可能性がある (図1)
- Creatorの公平性とF1スコアの比較 (図1)
  - 最新のCF -> ジニ係数高 (Creatorの公平性が低い)
  - Content-based手法 -> ジニ係数低 (Creatorの公平性が高い)
- ユーザ満足度とCratorの公平性の双方を考慮する手法を提案 
- Content-based手法にユーザの嗜好を入れるため, ユーザごとのパラメータを導入
- さらに各ユーザの友人の情報を使ってスパースデータに対処
  - n-hop目までの友人の情報を使う
  - 探索に時間がかかるのでMonte Carlo Tree Search (MCTS)を使う 

**提案手法**
- 文章中の各単語をword embedding -> CNNをかけて文章ごとの潜在ベクトルを抽出
- 文章の潜在ベクトルとユーザの潜在ベクトルで各ユーザの word-level representationを定義
- ユーザ uが文章 dをクリックする確率 <img src="https://latex.codecogs.com/svg.latex?\Large&space;p=\mathcal{F}(u,d)" />をユーザ uとその友人のword-level representaionを入力とする関数でモデル化 
- 友人を探索するために MCTSを使う


---
## SurfCon: Synonym Discovery on Privacy-Aware Clinical Data
### [PDF](https://arxiv.org/abs/1906.09285)

**イントロ**
- 医療文章は治療の意思決定を行う上で重要な情報を含む
- 医療文章からの類義語 (synonym)の発見は重要なタスクである 
  - 例えば医師が過去のカルテから "vitamin C"という単語を検索する時, "c vitamin", "vit c", "ascorbic acid"などの同義語や
    スペルミスを含む単語 ("viatmin c")も queryとして使えると嬉しい
- 医療分野においては患者のプライバシーを尊守する必要があり, 一つ一つの医療文章を入手できるケースは稀である
- 単語の共起回数を記録したデータのみが利用可能になっている
- 本研究では医療単語とそれらの共起グラフが与えられた下で各単語の類義語をあてるタスクに取り組む
- ストレートなアプローチは単語を写像して Knowledge graph (KB)を作ること
- しかしKBは限られた同義語しかカバーしていないことが知られている
- 最近の研究では Wikipediaや PubMedなど大規模なコーパスから同義語を抽出する研究がある
- しかしこれらは一つ一つの文章が得られることを前提としており, プライバシー保護が重要な医療分野にはそぐわない
- 限られた情報から同義語を抽出するため, 2種類の情報を活用する
  - 単語の表記の類似性   
    - 先行研究では文字間の類似性を使う方法が提案されている
    - しかし (1) 字面が似ていても意味が違う (2) 意味が同じでも字面が違う ケースはカバーできない
  - 単語の共起性  
    - 共起グラフの embedding手法が提案されている
    - しかしノイズの乗ったデータには対処できない
    - また, 共起グラフに含まれない単語 (Out-of-Vocabulary; OOV)も検索クエリとして使用される
- 本研究では上述の課題を解決する新たなモデルを提案する
- 提案法は surface form (字面)の encoding component, context matching componentの二つのパーツからなる
- context matching componentでは surface form encodingベクトルを入力として各単語の意味を推定する
  - その際, 生の単語ではなく surface form encodingベクトルを用いることで OOVに対処できる

**提案手法**
- Surface form encoding
  - クエリ qと類義語の候補 cが与えられた下でそれらの文字系列 x_q, c_qと単語系列 w_q, w_cを写像するencodersを定義する
  - encodersの出力をconcatしてさらに非線型変換を噛ませ, クエリ qと類義語 cの特徴ベクトル s_q, c_qを得る
  - 学習した特徴ベクトルに基づき, それらを入力とする関数で字面の類似度 (surface score)を定義する
- Context matching
  - 単語 u_iのコンテキストで単語 u_jが出現する確率を潜在ベクトル <img src="https://latex.codecogs.com/svg.latex?\Large&space;\nu_{u_j}" />と
    surface form encoding componentで学習した <img src="https://latex.codecogs.com/svg.latex?\Large&space;s_{u_i}" />の内積でモデル化する
  - 共起グラフをうまく説明するように各単語ごとの潜在ベクトル <img src="https://latex.codecogs.com/svg.latex?\Large&space;\nu_{u_j}" />を学習する
    - 損失関数はクロスエントロピー 
    - 単語数が多い場合計算量がかかるので negative samplingを使う
  - 学習済みモデルを使えば各単語 tに字面が似ている単語 (top-K)を得ることができる
  - クエリ qの類似単語のtop-K <img src="https://latex.codecogs.com/svg.latex?\Large&space;\{v_q^i\}_{i=1}^{K}" />と
    類義語の候補単語 cの類似単語のtop-K <img src="https://latex.codecogs.com/svg.latex?\Large&space;\{v_c^j\}_{j=1}^{K}" />について, 
    各組み合わせを入力として取るニューラルネットワークを学習し, 出力の重みづけ和をクエリ単語 qの意味とする
  - 同じ手順で候補単語 cの意味を学習し, 学習した2つの単語の特徴ベクトルを入力とする関数で意味の類似度 (context score)を定義する
- 単語の類似度は surface scoreとcontext scoreの和で決まる
- 損失関数としてクロスエントロピーを用い, ListNetで残りのパラメータを最適化

---
## Coupled Variational Recurrent Collaborative Filtering 
### [PDF](https://arxiv.org/abs/1906.04386)

**イントロ**
- タスクは推薦
- 推薦の文脈において深層学習を使う手法が多数提案されている
- しかしこれらの深層学習に基づく手法はUncertaintyを考慮しない   (決定論的アプローチであり, point estimationを出力する) 
    - 観測誤差が乗ったデータを扱う場合や未観測のinteractionを予測する場合等に問題になる
- Deep Bayesian Learning (DBE)ベースの推薦手法を提案
- DBEを適用する際に以下が問題になる
    - User/item fatureが時間とともに激しく変化する
    - 高頻度なストリームデータなので直近のデータを参考にモデルをアップデートする必要がある
    - DBLは一般的に計算コストが高く, User/item数が多い場合にスケールしない

**提案手法**
- i番目のノードと j番目のノードのinteraction <img src="https://latex.codecogs.com/svg.latex?\Large&space;x_{ij}" />が i番目のノードの 特徴量 v_iと
  j番目のノードの 特徴量 v_jを用いて平均 <img src="https://latex.codecogs.com/svg.latex?\Large&space;f_1(u_i,v_j)" />, 
  分散 <img src="https://latex.codecogs.com/svg.latex?\Large&space;f_2(u_i,v_j,\sigma_{i,j,T})" />のガウス分布に従うと仮定
  - <img src="https://latex.codecogs.com/svg.latex?\Large&space;f_1(\cdot)" />, <img src="https://latex.codecogs.com/svg.latex?\Large&space;f_2(\cdot)" />はニューラルネット
- User/itemの特徴量は 定常な項 (u)と dynamicな項 (Δu)に分けられる 
  - ある時刻 Tにおける user特徴量はその時刻 Tにおける Δuと定常項 u^sの和で書ける
  - 定常項は平均 0のガウス分布から生成される
  - ある時刻 Tにおける Δuは一つ前の時刻 T-1における Δuを用いて 
  平均 <img src="https://latex.codecogs.com/svg.latex?\Large&space;f_4(\Delta u_i^{T+1},\Delta \tau^{T})" />, 
  分散 <img src="https://latex.codecogs.com/svg.latex?\Large&space;f_3(\Delta u_i^{T+1},\Delta \tau^{T})" />のガウス分布に従うと仮定
  - <img src="https://latex.codecogs.com/svg.latex?\Large&space;f_3(\cdot)" />, <img src="https://latex.codecogs.com/svg.latex?\Large&space;f_4(\cdot)" />はニューラルネット
- 学習時は全ての時刻 tにおける user/item行列の事後分布を推定
  - 推論にはSequential Monte Carlo (SMC), 変文推論などを用いることができる
  - 今回はUser/item数が多い場合を想定し, 計算コストの少ない変分推論を用いた


---
## Fast and Accurate Anomaly Detection in Dynamic Graphs with a Two-Pronged Approach 
### [PDF](https://minjiyoon.xyz/ANRank.pdf)

**イントロ**
- コンピュータのネットワークやSNSを含む Network-based systemは様々な攻撃の対象にされている
  - マシンへのDDOS攻撃
  - SNSにおいてはスパムによる "Follow"や "Like"などが攻撃と見なせる 
- このような攻撃を検知するタスクに取り組む
- 既存手法の多くは staticなネットワークを仮定している
- いくつかの手法は dynamicなネットワークをモデル化する
- しかしこれらの手法は精度と速度という観点で問題がある
- 本研究では2つのタスクに取り組む
  - エッジの有無についての anomalyを検出 (Structural anomalies; AnomalyS) ← 図2(a)
  - エッジの重みについての anomalyを検出 (Edge weight anomalies; AnomalyW) ← 図2(b)
- nodeの写像を行うための手法は色々ある
- 本研究では node scoresの変化 (1階微分と2階微分)に焦点をあてる
- 上述の二つのタスクそれぞれについて適当なnode scoreの算出方法 (関数)を定義する
- 定義した関数の微分を anomaly度を測る metricとする

**提案手法**
- PageRankの拡張を提案
- 提案手法は node scoreの1階微分が large change, 2階微分が abrupt changeを表しているという直感に基づく
- node scoreの1階微分, 2階微分をトラッキングすることで anomaliesを検出する
- 二つのタスクを定義
  1. AnomalyS (エッジの有無についての anomaly検出)  
     - 例1) spammerがたくさんのユーザに一気にメールを送る→これまでつながっていなかったノード間に新しいエッジが張られる   
     - 例2) マシン上のデータを盗む場合, 対象マシンに秘密裏にエッジを貼る方法がとられる  
     %- とあるノード uがエッジの張り先を Δm変更した場合, 「ネットワーク構造が Δm変化した」と呼ぶ 
  2. AnomalyW (エッジの重みについての anomaly検出) 
     - エッジの重み ∝ エッジの生成回数
     - 例1) 攻撃対象のIPの portsをスキャンする時, 攻撃者は何度も攻撃対象のノード (IP)に繋ぐ
     - 例2) ボットが何度も同じ文章を投稿する (user-keywordのグラフのエッジの重みが対応)
- AnomalyS, AnomalyW検出用のNode score関数を設計
- どちらも関数の設計方法は変わらず, PageRankに基づいて node scoreの時間発展をモデル化 ($4.2)
- 上述のモデルに基づいて node scoreの1階微分, 2階微分を導出
- それらをconcatinateしたものをanomaly scoreとして使用
 
**実験**
- DARPAデータを用いて2つの既存手法と比較を行い, 精度でも計算時間でも既存手法より良い性能を示すことを確かめた 
- AnomalySとAnomalyWを同時に扱うアプローチが有効であることを定性的に示した


---
## Fates of Microscopic Social Ecosystems: Keep Alive or Dead? 
### [PDF](http://www.calvinzang.com/file/2019KDD-Li-SocialEcosystemFate.pdf)

**イントロ**
- Social networkの維持はSNSサービス提供者にとって重要な課題
- SNSのfates (alive, activeまたはdead)を予測するタスクに取り組む
- fates = ユーザのアクティビティの活発度
- 先行研究はsocial ecosystemのアクティビティをマクロなレベルで分析するものが主流
  - ユーザごとの違い, ユーザ同士のinteractionを考慮していない 
- 最近は別の文脈でネットワーク構造を考慮した手法も提案されている
- しかしデータが入手しにくいことから, microscopic social ecosystem (実験ではmicroscopic social ecosystemsとして各ユーザのego-networkを想定)のfatesについての研究はあまりされてこなかった
- 本研究ではまずWeChatデータ (5,500 microscopic social ecosystems with 75,027 users)を分析し以下の特性を洗い出した  
  - ユーザの役割 ("species")が明らかでない
  - 異なる役割を持つユーザが異なるscosystemから異なる影響を受ける
  - 各々のecosystemの最終状態は異なるパターンを示す
- これらの特性を考慮した新しいモデル "SocialFate"を提案
  - まず各ユーザの役割 ("species")を定義する
  - 次にspeciesとネットワーク構造, species同士のinteractionを考慮してモデルを構築する

**基礎分析** 
- WeChatデータを分析することで3つのcomplexitiesを発見した
  1. Uncertain species types (Figure 1-a)
    - 写真をアップロードする行為 = produce, 友人がアップロードした写真に likeもしくはコメントする行為 = consumptionとして
        ユーザごとのproductionの度合い (production score)を定義 ← 式(1) 
    - production scoreの高低によってユーザを producer/dealer/consumerの3つのタイプ ("species")に分ける
  2. Complex interaction networks (Figure 1-c)
    - 異なる終状態 (alive/active/dead)のecosystemは各speciesの割合が異なる  
      activeなecosystemは producerが多く, deadは consumerが多い
  3. Complex final states (Figure 1-b)
    - 先ほど定義した producer/dealer/consumerの3つのタイプの割合から social ecosystemの終状態を4つに分類した 

**提案手法**
- Lotka-Volterra modelをベース
- ユーザ数 N × speciesの種類 K の大きさの行列 Xを導入
  - Xの (n,k)番目の要素 <img src="https://latex.codecogs.com/svg.latex?\Large&space;X_{(n,k)}" />はユーザ nがspecies kに属す確率を示す
- 各speciesに固有の変化を表す項 f(・)と他のspeciesとのinteractionを表す項 g(・)で Xの時間変化 (dX/dt)をモデル化
- ユーザ間の関係を表すadjacency matrix Mと species同士の関係を表す matrix Aを導入し, X(t), M, Aを用いたgraph convolutionで g(・)をモデル化
- 提案手法はLotka-Volterra modelをspecial caseとして含む ($4.2の後半で証明)
- MLEでパラメータを学習
  - Xの推定値と実際の Xとの差異を小さくするようにパラメータを学習

**所感**
- タスクの新規性推し
- 実験が充実 
  - fatesをあてるという本来のタスクだけでなくSNSを活性化するための介入まで踏み込んでシミュレーションをしている
  - AとMを変化させた時に未来の Xがどう変化するか？というシミュレーション
- モデル化がリーズナブルでおもしろい. しかし応用上の意味がどれほどあるのかは不明.  
  fatesをあてるだけならLotka-Volterra modelに基づく仮定は必ずしも必要でない


---
## Predicting Embedding Trajectories for Temporal Interaction Networks 
### [PDF](https://cs.stanford.edu/~srijan/pubs/jodie-kdd2019.pdf) [Web](http://snap.stanford.edu/jodie/) 

**イントロ**
- 時刻付きUser-item (product)行列のモデル化
- Embedding手法が広く用いられる
- しかし既存手法には以下の課題がある
  1. Userが actionを取った時のみユーザの潜在ベクトルが変化するという仮定を置いている
  2. User/itemの潜在ベクトルは時変しない項と時変する項からなる
  3. 予測時に全 Itemをなめす必要がある -> Item数が多い場合に時間がかかる
  4. 学習を1度だけ行い, その後は潜在ベクトルの更新をしない
- RNNに基づき上記の課題を解決する手法を提案する
- 提案手法は Userと Itemのinteractionが起こる度に潜在ベクトルを更新する
  - Userの潜在ベクトルの更新時には interactした Itemの潜在ベクトルを用いる (逆も然り)
- User/Itemの潜在ベクトルの時間発展をモデル化 
  - 時間と共に線形に変遷するという仮定を置いている 

**提案手法**
- User/Itemの潜在ベクトルの変遷をRNNでモデル化
- User × Item行列を走査するのではなく, 未来の時刻において各ユーザが選ぶアイテムを直接あてるアプローチを考える 
  - 時刻 tにアイテム iとinteractしたユーザ uが時刻 t+Δにアイテム jとinteractするとする  
    t+Δの直前にユーザ uがどのアイテムとinteractするか？をあてたい
  - 時刻 t+Δにおけるアイテムのembeddingベクトル <img src="https://latex.codecogs.com/svg.latex?\Large&space;\tilde{j}(t+\Delta)" />を導入し
    時刻 t+Δにおけるユーザの潜在ベクトルとアイテムの潜在ベクトルの重み付き和でモデル化 
  - <img src="https://latex.codecogs.com/svg.latex?\Large&space;\tilde{j}" />の推定値と実測値の二乗誤差を目的関数とする


**実験**
- 実験時は "User state change prediction"と題してdrop-outの予測をしている ($4.2) 
  - 各手法を用いて学習したUser feature (論文中では "User trajectory")を入力としてロディスティック回帰でdrop-outしたか否かの0/1を当てるタスク 


