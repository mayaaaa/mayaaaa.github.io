---
layout: post
title: Interpretable Sequence Learning for COVID-19 Forecasting 
tags: [NeurIPS20]
---

<!--more-->

[PDF](https://papers.nips.cc/paper/2020/file/d9dbc51dc534921589adf460c85cd824-Paper.pdf)

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
  1. パラメータが少ないため表現力が不足している
  2. 微分方程式のレートが一定で
  3. 共変量がない
  4. well-mixedの仮定 
  5. 時間・空間をまたいだ情報共有ができていない
  6. 識別可能でない
- 本研究の貢献
  - 記録されていないケースと病院のリソースを考慮できる形にSEIRモデルを拡張
  - 病気の広がりは時間変化する (例えば移動量が減ると拡散も減る)~
    このような現象を捉えるため時変する共変量を用いる $$\leftarrow$$ 未来の情報は適当な予測モデルで外挿 (今回はXGBoostを使用) 
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
  - $$L(\cdot)$$は予測値と実測値の誤差
  - $$q(\cdot)$$は時間減衰関数 (減衰パラメータはハイパラとして扱う) $$\leftarrow$$ 直近のデータを重視
- 基本再生産数の正則化を追加 $$\leftarrow$$ 生産数が適度な幅に収まるように
- 予測結果に基づいて予測を繰り返すため, 伝搬誤差が生じる $$\leftarrow$$ これを緩和するためteacher forcingを適用
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


