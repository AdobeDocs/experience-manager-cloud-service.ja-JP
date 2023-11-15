---
title: AEM forms で参照用のテーマとテンプレートを取得する方法を教えてください。
description: AEM Formsには、フォームをすばやく作成できるように、サンプルのアダプティブフォームテーマ、テンプレート、フォームデータモデルが用意されています。
exl-id: 81588759-22da-4123-92fe-5ca97e97f1e4
source-git-commit: 046ffed13569ca3f9c104fb4525d28361873277a
workflow-type: tm+mt
source-wordcount: '868'
ht-degree: 88%

---

# 参照テーマ、テンプレート、フォームデータモデル {#reference-themes-templates-and-data-models}


| 適用先 | 記事リンク |
| -------- | ---------------------------- |
| コアコンポーネントに基づくアダプティブフォーム | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html) |
| 基盤コンポーネントに基づくアダプティブフォーム | この記事 |

<span class="preview"> Adobeでは、最新の拡張可能なデータキャプチャを使用することをお勧めします [コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja) 対象： [新しいアダプティブFormsの作成](/help/forms/creating-adaptive-form-core-components.md) または [AEM SitesページへのアダプティブFormsの追加](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). これらのコンポーネントは、アダプティブFormsの作成における大幅な進歩を表し、印象的なユーザーエクスペリエンスを実現します。 この記事では、基盤コンポーネントを使用してアダプティブFormsを作成する古い方法について説明します。 </span>

AEM Forms as a Cloud Service には、アダプティブフォームの作成をすぐに開始するのに役立つ、複数の参照テーマ、テンプレート、フォームデータモデルが用意されています。[ソフトウェア配布ポータルからリファレンスコンテンツパッケージ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip)をダウンロードし、[パッケージマネージャー](/help/implementing/developing/tools/package-manager.md)を使用して、[リファレンスコンテンツパッケージ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip)を実稼働、開発、ローカル開発環境にインストールして、これらの参照アセットをお使いの環境に取りこむことができます。

参照コンテンツパッケージに含まれるテーマ、テンプレート、フォームデータモデルは次のとおりです。


| テーマ | テンプレート | フォームデータモデル |
---------|----------|---------
| Canvas 3.0 | 基本 | Microsoft Dynamics 365 |
| Tranquil | 空白 | Salesforce |
| Urbane |   |  |
| Ultramarine |  |  |
| Beryl |  |  |
| ヘルスケア |  |   |
| FSI |   |   |

## リファレンステーマ {#reference-themes}

[テーマ](/help/forms/themes.md)を使用すると、CSS に関する深い知識がなくてもフォームのスタイルを設定できます。[参照コンテンツパッケージ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip)をインストールすることで、次のテーマを入手できます。

* Beryl
* Canvas 3.0
* Tranquil
* Urbane
* Ultramarine
* ヘルスケア
* FSI（金融サービス＆保険）

各テーマには、独自のエレガントなスタイルが含まれていて、ユーザー向けの使いやすいアダプティブフォームの作成に使用できます。パネル、テキストボックス、数値ボックス、ラジオボタン、表、スイッチなど、セレクター用の独自のスタイル設定が含まれています。これらのテーマ内のスタイルは、要件に基づいたものです。例えば、あるシナリオで、クリーンなフォントを含む最小限のテーマが必要だとします。Liberty テーマなら、その外観を実現できます。

![リファレンステーマ](assets/ref-themes.png)

このパッケージに含まれるテーマはレスポンシブで、これらのテーマ内のスタイルはモバイルおよびデスクトップ表示用として定義されています。様々なデバイス上の最新ブラウザーのほとんどは、これらのテーマのいずれかが適用されたフォームを問題なくレンダリングできます。

パッケージのインストールについて詳しくは、[パッケージの作業方法](/help/implementing/developing/tools/package-manager.md)を参照してください。

## Beryl {#beryl}

Beryl テーマでは、背景画像、透明度、大きくてフラットなアイコンの使用が強調されます。以下のスクリーンショットで、Beryl テーマの外観と、フォームのスタイル設定がどのように拡張されるかを確認できます。

![Beryl テーマ](assets/beryl.png)

## Canvas 3.0 {#canvas}

Canvas 3.0 はアダプティブフォームのデフォルトのテーマで、基本色、透明度、フラットアイコンの使用が強調されます。以下のスクリーンショットでは、Canvas 3.0 のテーマがどのように表示されるのかを確認できます。

![Beryl テーマ](assets/canvas.png)


## Tranquil {#tranquil}

Tranquil テーマは、Tranquil カラースキームの明るいシェーディングと暗いシェーディングを提供して、フォームの様々なコンポーネントを強調します。例えば、ラジオボタン、パネル、タブが、様々なシェーディングの緑色になります。

![Tranquil テーマ](assets/tranquil.png)


## Urbane {#urbane}

Urbane テーマは、フォームの最小限の機能的外観を強調します。Urbane テーマをフォームに適用すると、コンポーネントはフラットになります。パネルには細いアウトラインが付けられ、モダンな外観を作成します。

![Urbane テーマ](assets/urbane.png)


## Ultramarine {#ultramarine}

Ultramarine テーマは、濃い青色のシェーディングを使用して、タブ、パネル、テキストボックス、ボタンなどのコンポーネントを強調します。

![Ultramarine テーマ](assets/ultramarine.png)

## ヘルスケア {#healthcare}

Healthcare テーマは、濃い緑色のシェードを使用して、タブ、パネル、テキストボックス、ボタンなどのコンポーネントを強調します。

![FSI テーマ](assets/healthcare.png)


## FSI（金融サービス＆保険）

FSI テーマは、フォームの最小限の機能的外観を強調します。FSI テーマをフォームに適用すると、パネルコンポーネントが黄色になります。

![FSI テーマ](assets/fsi.png)

## 参照テンプレート {#reference-templates}


[テンプレート](/help/forms/themes.md)を使用すると、フォームの初期フォーム構造、コンテンツ、アクションを定義できます。[参照コンテンツパッケージ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip)をインストールすると、次のテンプレートを取得できます。

* 基本
* 空白

基本テンプレートを使用すると、登録フォームを素早く作成できます。また、アダプティブフォームの基盤コンポーネントの機能をプレビューする場合にも使用できます。データをセクションごとに表示するウィザードレイアウトが提供されます。空のキャンバス上からアダプティブフォームの作成を開始するには、空のテンプレートを使用します。


## 参照フォームデータモデル {#reference-models}

アダプティブフォームは Microsoft Dynamics 365 サーバーや Salesforce サーバーと連携し、ビジネスワークフローを実現できるようになります。次に例を示します。

* アダプティブフォームの送信時に、データを Microsoft Dynamics 365 および Salesforce に書き込む。
* フォームデータモデル内で定義されているカスタムエンティティを使用して、データを Microsoft Dynamics 365 および Salesforce に書き込む（またはその逆の動作）。
* Microsoft Dynamics 365 および Salesforce サーバーに対してデータのクエリを実行し、アダプティブフォームに事前設定する。
* Microsoft Dynamics 365 および Salesforce サーバーからデータを読み取る。

[参照コンテンツパッケージ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip)をインストールすると、次のフォームデータモデルを取得できます。

* Microsoft® Dynamics 365
* Salesforce

これらのモデルの使用方法については、[Microsoft Dynamics 365 および Salesforce クラウドサービスの設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-msdynamics-salesforce.html?lang=ja#configure-dynamics-cloud-service)を参照してください。


## 関連トピック {#see-also}

{{see-also}}