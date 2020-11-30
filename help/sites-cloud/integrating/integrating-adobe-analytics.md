---
title: Adobe Analytics との統合
description: 'Adobe Analytics との統合 '
translation-type: tm+mt
source-git-commit: 76db5314369ca0f854482586d5c96474014a47af
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 100%

---


# Adobe Analytics との統合{#integrating-with-adobe-analytics}

Adobe Analytics と AEM as a Cloud Service の統合により、Web ページのアクティビティを追跡できます。統合には次の要件が必要です。

* AEM as a Cloud Service で Analytics 設定を作成するためのタッチ UI を使用できること
* [Adobe Launch](#analytics-launch) の拡張機能として Adobe Analytics を追加し、設定できることAdobe Launch について詳しくは、[このページ](https://docs.adobe.com/content/help/ja-JP/launch/using/intro/get-started/quick-start.html)を参照してください。

旧バージョンの AEM と比較して、フレームワークのサポートは、AEM as a Cloud Service の Analytics 設定では提供されません。代わりに、AEM サイトに Analytics 機能（JS ライブラリ）を実装するデファクトツールである Adobe Launch によって実行されます。Adobe Launch では、Adobe Analytics の拡張を設定できるプロパティが作成され、Adobe Analytics にデータを送信するルールが作成されます。Adobe Launch は、SiteCatalyst が提供する解析のタスクに代わるものです。

>[!NOTE]
>
>既存の Analytics アカウントを持たない Adobe Experience Manager as a Cloud Service ユーザーは、Experience Cloud 用の Analytics Foundation パックへのアクセスをリクエストできます。この Foundation パックでは、Analytics の使用量が制限されます。

## Adobe Analytics 設定の作成 {#analytics-configuration}

1. **ツール**／**クラウドサービス**&#x200B;に移動します。
2. 「**Adobe Analytics**」を選択します。
   ![Adobe Analytics ウィンドウ](assets/analytics_screen2.png " Adobe Analytics ウィンドウ")
3. 「**作成**」ボタンを選択します。
4. 詳細（以下を参照）を入力し、「**接続**」をクリックします。

### 設定パラメーター {#configuration-parameters}

Adobe Analytics 設定ウインドウで表示される設定フィールドは次のとおりです。

![設定パラメーター](assets/properties_field1.png "設定パラメーター")

| プロパティ | 説明 |
|---|---|
| 会社 | Adobe Analytics ログイン会社情報 |
| ユーザー名 | Adobe Analytics API ユーザー |
| パスワード | 認証に使用される Adobe Analytics パスワード |
| データセンター | アカウントが関連付けられている Adobe Analytics データセンター（サンノゼやロンドンなどのサーバー） |
| セグメント | 現在のレポートスイートで定義されている Analytics セグメントを使用するオプション。Analytics レポートは、セグメントに基づいてフィルタリングされます。詳細は、[このページ](https://docs.adobe.com/content/help/ja-JP/analytics/components/segmentation/seg-overview.html)を参照してください。 |
| レポートスイート | データを送信し、レポートを取り込むリポジトリ。レポートスイートでは、選択した Web サイト、Web サイト群、または Web サイトページのサブセットに関する完全な独立したレポートが定義されます。単一のレポートスイートから取得したレポートを表示し、必要に応じて、いつでも設定でこのフィールドを編集できます。 |

### サイトへの設定の追加 {#add-configuration}

タッチ操作対応 UI 設定をサイトに適用するには、**サイト**&#x200B;に移動して、**任意のサイトページを選択**&#x200B;し、**プロパティ**／**詳細**／**設定**&#x200B;で、設定するテナントを選択します。

## Adobe Launch を使用した AEM Sites と Adobe Analytics の統合 {#analytics-launch}

Adobe Analytics は、Launch プロパティで拡張機能として追加できます。マッピングの実行と、Adobe Analytics に対して POST 呼び出しをおこなうルールを定義できます。

* 基本的なサイトに対して Analytics の拡張機能を Launch で設定する方法については、[このビデオ](https://docs.adobe.com/content/help/ja-JP/analytics-learn/tutorials/implementation/via-adobe-launch/basic-configuration-of-the-analytics-launch-extension.html)をご覧ください。

* ルールを作成して Adobe Analytics にデータを送信する方法の詳細については、[このページ](https://docs.adobe.com/content/help/ja-JP/core-services-learn/implementing-in-websites-with-launch/implement-solutions/analytics.html)を参照してください。

>[!NOTE]
>
>既存の（レガシー）フレームワークは引き続き機能しますが、タッチ操作対応 UI では設定できません。Launch で変数マッピング設定を再構築することをお勧めします。

>[!NOTE]
>
>Launch の IMS 設定（技術アカウント）は、AEM as a Cloud Service に事前に設定されています。ユーザーはこの設定を作成する必要はありません。
