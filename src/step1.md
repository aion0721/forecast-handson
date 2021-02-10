# Step1.概要

## 軽く概要

ガッツリ概要は前述の通り、社内資料を参照してください。

簡単にいうと、AmazonForecast とは（以下、Forecast）、SaaS で機械学習をお手軽に実施するサービスです。
（Forecast 以外にも GCP で AutoMLTables や、Azure から AzureMachineLearning 等も出ていますので、この分野は後発かと。）

ただし、AWS はやっぱり流通がメインになっているので、その辺りの学習データ等は他社と比較しても強いのではないかなぁと思ったりします。（あくまで感想です。）

## 今回のレギュレーション

すでにお伝えしている通り、過去の PCR 検査数の推移から今後の予測を立てる、というのを例にとって、Forecast を学んでいこうと思います。

## ハンズオンの前提

ハンズオンの前提としては社内クラウド環境を利用することとしますので、ログイン情報等は確認しておいてください。

また、その場でも記載しますが、供用の環境となりますので、くれぐれも遣り過ぎはご注意ください。

## 流れ

Forecast は以下の流れで進んでいきます。

1. データインポート
1. 学習
1. 予測

これについては、Forecast のダッシュボード表記が非常にわかりやすいので先んじてみてみましょう。

![Dashboard](/images/step1/Dashboard.png)

これの通りに進んでいけばいいので、非常にわかりやすく直感的です。

## 参考リンク

- AWS

  - [AmazonForecast](https://aws.amazon.com/jp/forecast/)

- GCP

  - [AutoMLTables](https://cloud.google.com/automl-tables/?hl=ja)

- Azure

  - [AzureMachineLearning](https://azure.microsoft.com/ja-jp/services/machine-learning/)

::: tip Azure machine learning
ちなみに、AzureMachineLearning については、以前社内で過去に調査しておりますので、そちらも合わせて参照いただければと思います。
（当時の評価は、データのソースを確保できないから厳しいね、って感じでした。）
:::
