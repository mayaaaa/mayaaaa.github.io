---
layout: post
title: Implicit Neural Representations with Periodic Activation Functions 
tags: [NeurIPS20]
---

### [PDF](https://papers.nips.cc/paper/2020/hash/53c04118df112c13a8c34b38343b9c10-Abstract.html)
**アブスト**
<!-- 
- 非明示的に定義された連続かつ微分可能なシグナルの表現をニューラルネットで記述する方法が出てきている
- しかし既存の非明示的な表現は詳細を捉えることができない
- また, 既存の手法は時間微分・空間微分を正確にモデル化することができない
- 本研究では周期的なactivation functionを用いる手法を提案
-->
- 画像, ビデオ, 音声等のシグナルのmapping $$\Phi$$をニューラルネットで記述する手法が提案されている
  - 例えば画像ピクセルの座標を入力したときに各ピクセルのRGB値を返す関数 $$\Phi$$をニューラルネットでモデル化
  - このような $$\Phi$$のパラメータを画像のimplicit representationと呼ぶ
- 提案手法はニューラルネット $$\Phi$$のactivation functionとしてRelu, tanh等の代わりにsin関数を使う
- sin関数の特徴はその微分が位相をずらしたcos関数で表せること
- この特徴を利用することでニューラルネットの出力そのものだけでなく入力 (画像の場合ピクセル座標)の1階微分, 2階微分についての学習もできるようになる 

