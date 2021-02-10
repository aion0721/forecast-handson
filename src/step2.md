# Step2.データの準備・インポート

## データドメイン

Forecast は予めいくつかのデータセットが定義されています。
例えば、小売の需要予測であったり、EC2 キャパシティの予測であったりしますが、そのどれにも対応しない場合は、Custom ドメインというものを指定することになります。

多くの場合、AWS が予め提供してくれているデータセットではないことが多いので、Custom を指定することになりますが、その場合はきちんとソースとなるデータを整形してあげる必要があります。

##  データの準備

インポートするデータは、以下の通りのカラムになっている必要があります。

| timestamp | target_varlue |        item_id |
| --------: | ------------: | -------------: |
| 2020-1-16 |             1 | positive_count |
| 2020-1-17 |             0 | positive_count |

詳細を説明すると以下の通りになります。
PCR 検査数の推移を見たいため、item_id は一つですが、複数の項目の予測を立てたい場合はこれが複数になります。（例えば、複数商品の予測を立てたい場合、等）

1. タイムスタンプ：日付（yyyy-m-d 方式）
1. 項目値
1. 項目ラベル

今回、PCR 検査数については以下からデータをダウンロードしてきています。また、私の方で整形もしていますので、気になる方はソースデータとアップロードされているデータでどういう風に加工されているか確認してみてください。（そんなに難しくないです。）

- 加工前

![inputData1](/images/step2/inputData1.png)

- 加工後

![inputData2](/images/step2/inputData2.png)

- データソース

  - [オープンデータ｜厚生労働省](https://www.mhlw.go.jp/stf/covid-19/open-data.html)

また、今回は時間も限られているため件数も少なくしています。本来ここはサンプルデータ数が多ければ多い方が正答率が上がると考えられれているので、可能な限りたくさんサンプルは用意しましょう。

### データの種類

Forecst では、以下の三つのデータを扱うことになりますが、それぞれ理解しておいてください。

- TARGET_TIME_SERIES:ターゲット時系列

  - 実際に予測したい項目を指定するもの。
  - 今回は、PCR 検査陽性数

- RELATED_TIME_SERIES:関連する時系列

  - 予測したい項目に影響があると思われる項目を指定するもの。
  - 今回の例は、例えば市中の人数とかがイメージになると思います。

- ITEM_METADATA:項目メタデータ

  - 予測したい項目に対しての特徴（メタデータ）をまとめたもの。
  - 今回の例では難しいですが、例えば製品をイメージにとると、品質、色、大きさ、グレード等が挙げられます。
  - これを指定することによって、過去のデータがないもの（例えば新商品の売上予測）等を行うことができます。

## データセット作成

それでは早速マネージメントコンソールからやってみましょう。

予測を行うにあたって、一つのデータのまとまりのことをデータセットグループと呼んでいますがこれを作るところから始めます。

あと最初に謝っておきますが、みてわかると思う部分は特に解説はしません。（そのための画像多めのハンズオンなので）
もちろんわかりづらい部分は補足しますが、それでも理解しきれない部分は個別で連絡してください。（問い合わせが多い場合は本資料をアップデートします。）

- データセットグループを作成

  ![createDG](/images/step2/createDG.png)

  - もしかすると、以下のような画面かもしれません。

    ![createDGAlter](/images/step2/createDGAlter.png)

- データセットグループを定義

  - DatasetGroupName:Covid19-Forecast<strong>\_Name</strong>
  - ForecastingDomain: Custom

  ![createDGDetail](/images/step2/createDGDetail.png)

:::tip Dataset Group Name
同じ環境を利用しますので、必ず末尾に<strong>\_名前</strong>をつけてください。
:::

- データセットグループを定義

  - DatasetName: pcr_positive
  - Frequency of Data: 1 Day

  ![DGConfig1](/images/step2/DGConfig1.png)

  - Schema:

    1. timestamp:timestamp:**yyyy-MM-dd**
    1. target_value:float
    1. item_id:string

  ![DGConfig2](/images/step2/DGConfig2.png)

  - DatasetImportDetails

    - DatasetImportName: pcr_positive_count
    - SelectTimeZone: Do not use time zone
    - DataLocation: \<S3:Bucket>:Filename
    - IAMRole: 予め作ってあるので、選択できるやつを選択してください。

  ![DGConfig3](/images/step2/DGConfig3.png)

::: tip データセットグループ

データセットという言葉がゲシュタルト崩壊を起こしそうで非常にわかりづらいですが、以下のような考え方だとまだわかるかなと。

- DatasetGroup:予測の名前、タイトル
- Dataset(TARGET_TIME_SERIES):予測したい対象の名称
- DatasetName:インポートするファイル名、等

:::

- ここまで実施するとデータのインポートが始まります。おそらく、15 分ぐらいかと思いますので、お待ちください。

インポートが完了すると、以下の表示になると思います。わかりやすいですね。

また、関連する時系列や項目メタデータについても同様にボタンがありますのでここから登録することができます。

![ImportData](/images/step2/ImportData.png)
