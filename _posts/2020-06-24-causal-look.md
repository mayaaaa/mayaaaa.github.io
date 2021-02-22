---
layout: post
title: A causal look at statistical definitions of discrimination
tags: [KDD20]
---

<!--more-->

[PDF](https://dl.acm.org/doi/pdf/10.1145/3394486.3403130)

**イントロ**
- 心理テスト, 教育テストにおいてはフェアな分類器の基準として「予測の同等性 (predictive parity)」がスタンダードになっている
- 同様にerror rate balance, equalized oddsなどもフェアネスの基準として用いられる
- 本稿ではpredictive parityとerror rate balanceを因果の視点から分析する 
- 本研究ではフェアネスを考慮していない一般的な分類器は通常predictive parityの条件を満たさないことを示す
- 一方で一般的な分類器はerror rate balanceを満たしうる
- これらを証明するため, 本稿では分類器をデータ生成過程として理解し直し因果ダイアグラムとして表現する
  - 因果推論においては, データ生成過程についての仮定はobserved data causal diagramと呼ばれる因果ダイアグラムで表される
  - 機械学習の分類器の予測をデータ生成過程の出力として理解することでこの過程を因果ダイアグラムとして解釈し, prediction causal diagramと呼ぶ
- 因果ダイアグラムによって判断される独立性の基準を用いて以下を示す
  - (i) 出力がd分離の場合にデータ生成過程がerror rate balanceを達成できること  
  - (ii) グループによってベースレートが異なりかつデータが完全分離でない場合, predictive parityを達成できないこと 
- ちなみに(ii)の基準はデータの構造によらず成り立つ
- 人工データを用いて上記を実験的に検証した
- さらにCOMPASデータを分析し直し, predictive parityの欠如に関する証拠を挙げた

**提案手法**
- 特徴量をX, 出力をY, 差別に関連する変数 (属性など)をAとする
- Predictive parityは$$\text{PPVa} = P(Y_{ts}=1|A_{ts}=a,Yˆ{ts}=1)$$と定義することができる
- $$M$$をモデル, $$R$$を予測器とすると分類器のダイアグラムは図1のように描ける
- 特徴量Aを入れると図2のように描ける
- 図3はメジャーな分類器に対応する因果ダイアグラムのリスト
- predictive parityに関する証明
  - $$Y_{ts}$$と$$A_{ts}$$が独立でないならPPV0$$\neq$$PPV1であることを図3の因果ダイアグラムのリスト各々について示す
  - $$Y_{ts}$$は全ての因果ダイアグラムにおいて$$Y_{ts}$$を$$A_{ts}$$からd分離しない
  - 従って(1)式より結果 (ii)が証明できる
- FPR (false positive rate)とFNR (false negative rate)に関する証明
  - $$Y_{ts}$$はいくつかの因果ダイアグラムで$$Y_{ts}$$を$$A_{ts}$$からd分離する
  - これらのダイアグラムに対応する分類器においては error rate balanceが満たされる

**実験**
- 人工データを使った実験を行い上記の結果を実例で説明する
  - $$Y_{ts}$$が$$A_{ts}$$を\hat{Y}tsからd分離するようなダイアグラム (分類器)としないような分類器を二つ用意しそれらのダイアグラムに基づいて人工データを生成する
  - 生成した人工データに対して (i) Bayes classifierを学習し (ii) PPVなどの指標を計算し (iii) ベースレートの差を記録する
  - 図3を見ると, d分離するダイアグラム (Model 1)ではFPR1−FPR0が無視できるほど小さいのに対し, d分離しないダイアグラム (Model 2)ではそうなっていない
  - この結果は前章で導いた結果と一致する
- COMPASデータの再検証
  - COMPASデータは人種に関するpredictive parityが満たされている例として使われてきた
  - しかしこの前提は前章で導いた結果と矛盾する
  - 図8に各々の人種ごとのPPVaを示す
  - エラーバーがかぶっていないところを見るとこのデータはpredictive parityを満たしていない
  - 統計が足りていないのにも関わらずpredictive parityの検証をしてしまった可能性
