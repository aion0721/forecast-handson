# Step5.付録

## InputData を増やした場合

今回は学習時間を短縮するために 60 件ぐらいの比較的少なめなデータ実施しましたが、長期間での結果を参考程度に記載しておきます。

- InputData: 300 件ぐらい
- 所要時間： （概算）
  - Import: 30 min
  - Train: 120 min
  - Predict: 45 min

![Reuslt](/images/step5/Result.png)

## 関連する時系列を追加した場合

コロナウイルスの特性的に気温が関係しているんじゃないかと思いまして、自分で気温を RELATED_TIME_SERIES に設定してみました。
（今でこそ、SupplementalyFeatures にて内部的には勝手に処理されていると思うのですが、当時はその機能がなかったため、自分で登録しています。

- データソース

  - [気象庁｜過去の気象データ検索](https://www.data.jma.go.jp/obd/stats/etrn/index.php)

    - 正直これの修正がとてもとても大変でした・・・

- 結果

  以下です。

  ![Tempereture](/images/step5/Temperature.png)

  これ、見た目はすごく単純（気温をデータとして入れていない前回の結果の方が統計的に特徴が出ているのに対し、この結果は特徴としては短調）なんですが、結果的には、こちらの方が実績に則していたりします。

  （正直、気温を入れたことによってアルゴリズムが変わって特徴が変わっただけだとは思うのですが、逆にいうとアルゴリズムが変化したことによって、これだけ差が出てくるんだなと実感しました。）

## TrainPredictor 詳細

訓練結果についてはより詳細な結果を確認することができます。そのうち主要項目をみてみましょう。

確認方法は先ほどのナビゲーションの Predictor からもいけますし、ダッシュボードの ViewPredictor でもいけます。

- Predictor OverView : Winning autoML algorithm
  ここで、採用されたアルゴリズムを確認することができます。

  ![Predictor1](/images/step5/Predictor1.png)

- AlgorithmMetrics : アルゴリズム評価

  ここでは、学習に対しての評価を確認することができます。詳細は
  [予測精度の評価](https://docs.aws.amazon.com/ja_jp/forecast/latest/dg/metrics.html)

  ![Predictor2](/images/step5/Predictor2.png)

## やってみた感想

やってみた感想はいかがでしたでしょうか。SaaS ならではのメリットもあり、相当簡単に機械学習による予測ができたんじゃないかなと思います。

ただし、SaaS だから、という癖みたいなものもあり（特にインプットデータ加工等）この辺りは上手に慣れていくしかないのかなと思います。

また、これの何がいいかというと、純粋に業務知識だけある人が機械学習をやろうと思ったときに、AI の知識やコーディング知識が不要で実施ができるというところが大きいと思います。

簡易的な予測としては充足していると思いますので、パパッと確認してみたい時など、ユースケースに応じて使い分けていけるととてもいいんじゃないかなと思います。