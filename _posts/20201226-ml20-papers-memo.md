---
layout: post
title: NeurIPS 2020 Papers サーベイメモ
tags: [NeurIPS20]
---

## Links
[NeurIPS 2020 Proceedings](https://papers.nips.cc/paper/2020)
[ICDM 2020 Proceedings](http://proceedings.mlr.press/v119/)


---
## Adapting Neural Networks for the Estimation of Treatment Effects 
### [PDF](https://papers.nips.cc/paper/2019/file/8fb5f8be2aa9d6c64a04e3ab9f63feee-Paper.pdf)
**イントロ**
- 観測データからの因果効果の推定を考える
- ランダム化比較試験 (RCT)が高いあるいはできない場合でも観測データが使える
- 因果推論においては交絡因子に配慮する必要がある
- 対処法の一つは共変量に関する情報を集めること
- 共変量が全ての交絡因子を含む場合, 因果効果が推定できる
- このあと観測されていない交絡因子がないという設定で議論する
- 出力 $$Y$$ (回復するか否か)に対する交絡因子 $$T$$ (投薬)の効果を共変量 X (疾患重症度や社会経済的地位)を考慮して推定する
- 因果推論にニューラルネットを用いる
- 因果効果の推定は二段階で行う
  - 初めにconditional outcomeと傾向スコアを用いてモデルをfitさせる
  - その後フィットさせたモデルを後段の推定器に入力する
- 因果推論の質を上げるためにニューラルネットをどうアレンジするかが鍵

---
## Performative Prediction
### [PDF](https://arxiv.org/abs/2002.06673)
**イントロ**
- 予測結果を意思決定のサポートに使う場合, 予測結果が行動変容を招き予測対象に影響を及ぼすことがある
- 例えばローン応募者の破産リスクを銀行が見積もりそれらを公開すると対象の破産リスクが高まる
- 遂行性は至る所に存在する
  - 交通予測は交通パターンに影響する, 犯罪の場所予測は警備配置に影響する, 株価の予測は売買を決める
- 遂行性を無視した場合, 分布の変化を招く
- 実用上は分布の変化に対応するために予測モデルを学習し直すアプローチが考えられる
- 再学習はいたちごっこになるため望ましくない
- 予測が誘発した分布に対してモデルが最適になるような平衡点が望ましい
- こういった平衡は再学習の安定点と一致する
- いくつか疑問が生じる
  - 安定点はどこにあるのか? どう効率的に探すのか? 再学習の収束条件は? どのような場合に安定点がよい予測精度を持つか? 
- statistical decision theory, causal reasoning, and game theoryのコンセプトを結びつけ performative predictionを定式化する


--- 
## Interpretable Sequence Learning for COVID-19 Forecasting [NeurIPS 20]
### [PDF](https://papers.nips.cc/paper/2020/file/d9dbc51dc534921589adf460c85cd824-Paper.pdf)
**イントロ**
- COVID-19の予測は様々なシーンで役立つ
- 予測にはmobility indicesなど様々なリソースを利用できる
- 予測には通常時系列予測手法が使われるが, パンデミックの予測にあたっては以下の課題がある
  - 感染症に関する事前知識を用い効きそうなデータを利用する必要がある
  - データの生成過程が非定常 (政府の方針や個人の予防行動に左右される)
  - 様々なデータソースがあり, それらの因果的効果は未知
  - ほとんどの感染が記録されていないため, 問題は識別不可能
  - データソースはノイズ多い
  - 精度以上に説明性が必要
- SIRやSEIRなどの区画モデルが感染症予測に使われている
- これらのモデルは区画 (Susceptible <感受性保持者>, Infectious <感染者>など)ごとの人数をモデル化し区画間の遷移を微分方程式で記述する
- 区画モデルは7つの短所がある
  - (i) パラメータが少ないため表現力が不足している
  - (ii) 微分方程式のレートが一定で
  - (iii) 共変量がない
  - (iv) well-mixedの仮定 
  - (v) 時間・空間をまたいだ情報共有ができていない
  - (vi) 識別可能でない
- 本研究の貢献
  - 記録されていないケースと病院のリソースを考慮できる形にSEIRモデルを拡張
  - 病気の広がりは時間変化する (例えば移動量が減ると拡散も減る)~
    このような現象を捉えるため時変する共変量を用いる <- 未来の情報は適当な予測モデルで外挿 (今回はXGBoostを使用) 
  - 部分的な観測からのマスク付き教師あり学習, partial teacher-forcing, 正則化, 場所間の情報共有を用いた学習メカニズムを提案

**提案手法**
- 単なる<感染者> <回復者>ではなく<記録された感染者> <記録されていない感染者>などのカテゴリを作り, これらを加えてSEIRモデルを書き直す
- 次世代行列を使って基本再生産数は(1)式で書き下せる
- 各タイムステップにおける共変量 $$cov(vi,t)$$に非線形変換をかけモデルの入力として使用
- 共変量の未来の値は適当な予測モデルで外挿 (今回はXGBoostを使用) 
- (2)式のw, cは場所間で共有されたパラメータ, $$b_i$$が場所ごとのパラメータ
  - 場所ごとの共変量の違いを$$b_i$$で吸収してしまう可能性があるので, $$b_i$$に正則化をかける
  - この正則化を外すとモデルの性能が落ちることが実験で確かめられている
- 目的関数は(3)式で定義されている
  - $L(\cdot)$は予測値と実測値の誤差
  - $$q(\cdot)$$は時間減衰関数 (減衰パラメータはハイパラとして扱う) <- 直近のデータを重視
- 基本再生産数の正則化を追加 <- 生産数が適度な幅に収まるように
- 予測結果に基づいて予測を繰り返すため, 伝搬誤差が生じる <- これを緩和するためteacher forcingを適用
  - Teacher forcingはモデルの入力として予測したい正解データを使うものだが, 評価時に正解データが使えないという問題がある
  - 入力として予測値と正解データをランダムに使うPartial teacher forcingを提案
  - どっちを使うかを表すバイナリ νはハイパラとして扱う
- アメリカ合衆国におけるCOVID-19データを使用 (死者数, 入院数, ICUベッド数など)
- 4つの州における死者数の予測結果を図3に示す
  - 全てのケースで実際の死者数の推移をうまく捉えることができている
- モデルの説明性について
  - 提案モデルは各区画を明示的にモデル化しているのでそれぞれの遷移を捉えることができる
  - encoderとして説明可能なモデルを使っているので各共変量の影響を把握することができる
    - 図3は共変量の重みの学習結果
    - interventionに関する共変量については重みのピークが数日後にくる
    - mobility indexは重みが正, public interventionの重みは負になっている
    - 社会福祉を受けている家庭の数, 60歳以上の人口率が死亡率と正の相関


---
## Benchmarking Deep Learning Interpretability in Time Series Predictions [NeurIPS 20]
### [PDF](https://papers.nips.cc/paper/2020/file/47a3893cc405396a5c30d91320572d6d-Paper.pdf)
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

---
## Deep Relational Topic Modeling via Graph Poisson Gamma Belief Network [NeurIPS 20]
### [PDF](https://papers.nips.cc/paper/2020/file/45c166d697d65080d54501403b433256-Paper.pdf)
**イントロ**
- グラフ関連のタスク (リンク予測など)では予測の不確実性をモデル化するのが重要
- グラフのモデル化に広く使われるモデルとして潜在空間におけるnodeとedgeの関係を考慮するもの (relational topic model)がある
- RTMは浅いネットワークを使っているので表現力に限界がある
- LDAの代わりに多層のネットワークを使って意味的な関係性を表現する手法が流行っているが, RTMには適用されていない
- 別の発展としてVAEをグラフに応用したVGAEがある
- これらを組み合わせたモデルを提案

**提案手法**
- ベースラインはGraph Poisson factorモデル
  - 文章 ($$K_0$$の単語のセット) $$x_i$$の系列 (N個)を入力とする
  - トピック$$\Psi$$と$$\theta_i$$に分解
  - ディリクレ分布を$$\Psi$$のpriorとして使う
  - $$\theta_i$$のpriorはgamma分布
- Graph Poisson gamma belief network (GPGBN)はTつの隠れ層を使ってこのモデルを拡張したもの
  - $$\theta_i$$が一つ上の層の$$\Psi$$と$$\theta_i$$の内積から生成されるという仮定
  - GPGBNは全てのパラメータの事後分布を解析的に解ける
- GPGBN (decoder)と2つのワイブル分布ベースグラフ推論モデル (decoder)を組み合わせる 
- 二つのワイブルグラフAEができる

**実験**
- 6つのベンチマークデータを使用
- 


---
## Multi-task Causal Learning with Gaussian Processes [NeurIPS 20] 
### [PDF](https://papers.nips.cc/paper/2020/file/45c166d697d65080d54501403b433256-Paper.pdf)
**イントロ**
- 意思決定において介入実験が重要
- 図1のように収穫量 $$Y$$は肥料 $$X$$, 異なる時刻における虫の率 $$Z=\{Z_1,Z_2,Z_3\}$$で決まる
- 実験を繰り返すことでintervention functionを学習する
- ナイーブにはintervention functionを各々モデル化することができる
- しかしこのアプローチは実験ごとの出力間の相関を考慮できない
- intervention functionは相関している
  - 例えばintervention set $${X, Z_1}$$について実験をした場合, $$X$$もしくは $${X, Z_1, Z_2, Z_3}$$を変化させた場合の情報も得られる
- 因果推論とマルチタスクラーニングを組み合わせたフレームワークを提案
- 確率的因果推論では実験が難しい時にd分離を使って介入効果の推定をする
- d分離では各々のintervention functionを独立に扱う
- Multi-task GPは出力同士の相関をモデル化するのに使われる

**提案手法**
- 確率的構造方程式モデルでは内生変数 $$v$$, 外生変数 $$u$$, (決定的)関数 $$f$$, 外生変数の分布 $$p(u)$$の4つの変数がある
- 関数$$f$$と分布$$p(u)$$から分布$$p(v)$$が決まる
- intervention functionsをTと置く

---
## CaSPR: Learning Canonical Spatiotemporal Point Cloud Representations
## [PDF](https://papers.nips.cc/paper/2020/file/9de6d14fff9806d4bcd1ef555be766cd-Paper.pdf)
**イントロ**
- 時空間的に変化する幾何オブジェクトの再構成が重要
- staticな三次元の観測や時変するpoint cloudから物体の形を学習する手法が提案されている
- しかし時間的な連続性, ロバスト性, カテゴリレベルの一般化ができていない
- 時空間の変化をencodeするオブジェクトの表現を学習する手法を提案
  - depth sensorsやLIDARで観測されたpoint cloudは時間・空間的にスパース
- 時空間の表現として望ましい性質は時空間の連続的な変化を捉えられること, 非規則的なサンプリングパターンにロバスト, 
カテゴリー内の見たことないオブジェクトや観測されていない時間への一般化

**提案手法**
- 連続時空間表現
  - TPointNet++によるembedding zを$$z_{ST}$$と$$z_{dyn}$$の二つに分割して使う
  - $$z_{dyn}$$をLatent ODEの初期値$$z_0$$として使う
  - ODEを解くことで$$z_0$$を時刻 $$T$$まで時間発展させ, $$z_T$$における連続的表現をはく 
  - $$Z_{ST}$$と$$Z_T$$の積$$z$$で時空間的な変化を表す
- 時空間生成モデル
  - 点群の生成には数々の手法が提案されているが, 4Dの時空間点群にはそぐわない
  - そこでContinuous Normalizing Flows (CNF)を使う
   - 観測されていないデータをサンプルできる
  - JJFORDの実装を使用 ()
  - 時刻 $$t=0,...,T$$までLatent ODEで3Dシェープの系列を生成する
  - Gaussianから変数 ykをサンプルしそれをztの条件付きflow $$g_{\beta}(y_k|z_t)$$に渡す


---
## Temporal Spike Sequence Learning via Backpropagation for Deep Spiking Neural Networks 
### [PDF](https://papers.nips.cc/paper/2020/file/8bdb5058376143fa358981954e7626b8-Paper.pdf)
**イントロ**
- 脳の活動にインスパイアされたSpiking Neural Networks (SNN)が注目を集めている
- バックプロパゲーション (BP)を用いた SNNの学習方法が多数提案されている
- しかし二つの課題がある
  - 離散のスパイクイベントが微分できないため誤差の正確な伝搬が難しい
  - 性能を上げるのにタイムステップ数が必要
- TSSL-BPは誤差伝搬を inter-neuron, intra-neuronの二種類の依存関係に分解する
- 


---
## Modeling Continuous Stochastic Processes with Dynamic Normalizing Flows [NeurIPS 20]
### [PDF](https://papers.nips.cc/paper/2020/file/58c54802a9fb9526cd0923353a34a7ae-Paper.pdf)

---
## Deep Multimodal Fusion by Channel Exchanging 
### [PDF](https://papers.nips.cc/paper/2020/file/339a18def9898dd60a634b2ad8fbbd58-Paper.pdf)

--- 
## A shooting formulation of deep learning 
### [PDF](https://proceedings.neurips.cc/paper/2020/file/89562dccfeb1d0394b9ae7e09544dc70-Paper.pdf)

--- 
## Teaching a GAN What Not to Learn
### [PDF](https://papers.nips.cc/paper/2020/hash/29405e2a4c22866a205f557559c7fa4b-Abstract.html)

---
## Learning to Extrapolate Knowledge: Transductive Few-shot Out-of-Graph Link Prediction
### [PDF](https://papers.nips.cc/paper/2020/hash/0663a4ddceacb40b095eda264a85f15c-Abstract.html)

---
## Implicit Neural Representations with Periodic Activation Functions 
### [PDF](https://papers.nips.cc/paper/2020/hash/53c04118df112c13a8c34b38343b9c10-Abstract.html)

---
## Non-reversible Gaussian processes for identifying latent dynamical structure in neural data
### [PDF](https://papers.nips.cc/paper/2020/hash/6d79e030371e47e6231337805a7a2685-Abstract.html)



