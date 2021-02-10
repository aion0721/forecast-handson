# Step4.予測

さて、無事に学習が完了したら最後の予測を確認してみましょう。

## Console

まずはコンソール上で確認してみましょう。

![Forecast](/images/step4/Forecast.png)

- CreateForecast

  - ForecastName: Forecast1
  - Predictor: Train1
  - ForecastType: (入力なし)

![ForecastDetail1](/images/step4/ForecastDetail1.png)

これにて予測作成完了です。 この処理はそんなに時間はかかりません。(30 分ぐらい)

続いて、予測結果の出力をしてみましょう。

- LookupForecast

予測結果の出力は Lookup から実施します。

- Forecast: Forecast1
- StartDate: 2021-01-25(実体の値と少し被せた方が傾向が見えてわかりやすいです。)
- EndDate: 2021-02-20(前述の通り、InputData が少ないため、20 個程度しか予測できません。)

![ForecastDetail2](/images/step4/ForecastDetail2.png)

- 結果については以下です。

![Result](/images/step4/Result.png)

なんとも言えない感じになりましたが、予測の範囲内には入っているような気がします。

## CSVExpoprt

次に CSV でもエクスポートしてみましょう。
といってもコンソールで見れる情報が並べられるだけなので、さらにこのデータを加工したい、というの思いがなければコンソールで充分かなとは思います。

- Forecasts List

  作成した予測結果を確認するときは、左のナビゲーションバーからアクセスします。(Forecasts ってやつです。)

  わかりづらくしているとしか思えませんが、ナビゲーションからしかアクセスできません。（あんまり利用ケースないからなのかなとは思いますが。）

  ![Navi](/images/step4/Navi.png)

  Export したい予測を選択して、右上の CreateForecastExport をクリックすれば Export できます。

  ![ForecastsList](/images/step4/ForecastsList.png)

  正直、ウィザードに沿っていけばできるので解説は割愛します。（手抜き）

  Export は S3 になりますので、適宜 Export した結果は適宜拾っていただければと思います。
