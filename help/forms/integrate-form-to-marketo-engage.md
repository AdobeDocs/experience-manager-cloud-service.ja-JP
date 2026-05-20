---
title: Marketo EngageとAEM Formsの統合方法？
description: Marketo Engage インスタンスをAEM Formsと統合する方法について説明します。
keywords: Marketo インスタンスをフォームに接続する方法 、Marketoへのフォームの接続、Marketo Engageとのフォームの統合、Marketo インスタンスとのアダプティブフォームの統合。
feature: Adaptive Forms, Form Data Model
role: User, Developer
badgeSaas: label="AEM Forms" type="Positive" tooltip="AEM Formsに適用）。"
exl-id: 74cd25f9-1ee1-4f3f-8e02-8714071e7c86
source-git-commit: 60fa6bd9f29e670acb2acf52a40266e699bb99d3
workflow-type: tm+mt
source-wordcount: '817'
ht-degree: 5%

---

# Marketo Engage の AEM Forms への統合

AEM Formsと[Adobe Marketo Engage](https://experienceleague.adobe.com/ja/docs/marketo/using/home)を統合することで、Marketo Engageの機能を活用して、取り込まれたデータからビジネスロジックを作成し、スマートキャンペーンやメールオートメーションなどのワークフローを自動化することができます。 設定されたフォームは、キャプチャしたデータをMarketo Engageに送信して処理できます。

## Marketo Engageとフォームを統合する利点

次に、AEM フォームをAdobe Marketo Engageに接続する利点をいくつか示します。

* **簡単な統合**: Marketo Engageとフォームを接続すると、別のフォームデータモデルを作成する必要がなくなります。 統合プロセスはシンプルでユーザーフレンドリーです。
* **自動データキャプチャ**: フォーム送信を自動的にキャプチャし、Marketoに保存することで、手作業によるデータ入力を排除し、エラーを減らすことができます。

* **リード管理**: フォーム送信をマーケティングデータベースに直接統合することで、リード管理プロセスを合理化し、リードの追跡と育成を強化できます。

* **キャンペーンパフォーマンスの向上**: フォームデータを使用してマーケティングキャンペーンを分析および最適化し、全体的なパフォーマンスと投資収益率（ROI）を向上させます。

* **分析とレポート**: Marketo内でMunchkinなどの強力な分析およびレポートツールにアクセスし、フォームやキャンペーンの効果を測定するのに役立ちます。

* **フォローアップの自動化**: フォーム送信によってトリガーされるフォローアップメールとワークフローを自動化し、リードとのタイムリーなコミュニケーションを確保するのに役立ちます。

## 代替フォームソリューションよりもAEM Formsを使用する主な利点

次の表は、他の代替フォームソリューションよりもAEM Formsを選択する理由をいくつか示しています。

| **機能** | **AEM Forms** | **その他のフォームソリューション** |
|-------------------------------------|----------------------------------------------------------------------|-----------------------------------------------------------|
| **カスタマイズ** | 特定のカスタム関数の追加、フォームアクションの調整、フィールドの動作の変更を行って、フォームのインタラクションや複雑なワークフローを強化できます | カスタマイズのサポートなし |
| **ルールエディター** | 組み込みのルールエディターをサポートして、ロジックと条件を追加します。 | ルールエディターのサポートなし |
| **レイアウトオプション** | 複数のレイアウトオプションをサポート | レイアウトオプションが限定的 |
| **事前入力サービス** | フォームデータを自動入力する事前入力サービスを提供します。 | 使用可能な事前入力サービスがありません |
| **Sitesに埋め込む** | iFrameを使用してSitesに埋め込むことができます | iFrameを使用してSitesに埋め込むことはできません |
| **サイトとの統合のしやすさ** | Adobe AEM Formsでは、Adobe Experience Manager Sitesと同じスキルを使用するため、それ以外の学習は不要です | 追加の学習が必要な場合があります |
| **データ送信** | 様々なプラットフォームにデータを送信でき、SharePointへの接続、OneDriveへの接続、Salesforceへの接続など、複数のコネクターを提供します。 | 限られたコネクタ（例：Salesforce）にデータを送信できます |

## Marketo Engageとフォームを統合する際の考慮事項

Marketo EngageとAEM Formsを統合する際の考慮事項：

* AEMは、様々なMarketo データベースの中のPeople （Leads） データベースのみをサポートします。
* Marketoでは、ユーザー定義オブジェクトとして10個のカスタムオブジェクト [&#128279;](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/marketo-custom-objects/add-marketo-custom-object-fields)を作成し、リードの標準フィールドを超える特殊なデータを保存して、独自のビジネスニーズをサポートすることができます。
* AEMがカスタムオブジェクトにアクセスできるのは、リードデータベースに関連付けられている場合のみです

## Marketo Engageとフォームを統合するための前提条件

Marketo EngageとAEM Formsを連携するための前提条件は次のとおりです。

* 有効なAdobe Marketo Engage ライセンス
* [へのMarketo Engageの作業中のインスタンスは、クラウド設定を作成するためにクライアント IDとクライアントシークレット &#x200B;](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/additional-integrations/create-a-custom-service-for-use-with-rest-api)を取得します。

## AEM Forms（アダプティブForms）とMarketo Engageを接続するためのクラウドサービス設定の作成

![ワークフロー](/help/forms/assets/workflow-marketo-1.png)

>[!VIDEO](https://video.tv.adobe.com/v/3442865/engage-marketo-aem-forms-aem)

<span>このビデオは、コアコンポーネントのみに適用されます。 UE／基盤コンポーネントについて詳しくは、記事を参照してください。</span>

Cloud設定は、Experience Manager インスタンスをAdobe Marketo Engage インスタンスに接続します。 Marketo Engage クラウド設定を作成するには、次の手順を実行します。

1. **ツール** > **Cloud Services** > **Marketo Engage**&#x200B;に移動します。

   ![Marketo Engage](/help/forms/assets/marketo-engage.png)

1. 設定をホストするフォルダーを開き、**作成**&#x200B;をクリックします。 「**Marketo Engage設定を作成**」ウィンドウが表示されます。

   >[!NOTE]
   >
   > また、[&#x200B; クラウドサービス設定のフォルダーを設定することもできます](/help/forms/configure-data-sources.md#configure-folder-for-cloud-service-configurations)。

1. サービスに接続する設定と資格情報の&#x200B;**タイトル**&#x200B;を指定します。 Adobe Marketo Engage ダッシュボードから認証情報を取得できます。

   * **クライアント ID**&#x200B;と&#x200B;**クライアントシークレット**&#x200B;は、**管理者** > **統合** > **LaunchPoint**&#x200B;で利用できます。カスタムサービスを選択し、**詳細を表示**&#x200B;をクリックします。
   * **ID URL**&#x200B;は、**REST API** セクションの&#x200B;**Admin** > **Integration** > **Web Services**&#x200B;で&#x200B;**Identity**&#x200B;として利用できます。

1. 「**接続**」をクリックします。  接続に成功した場合、`Authentication Successful` のメッセージが表示されます。
1. 「**[!UICONTROL 作成]**」をクリックして、クラウド設定を保存します。

![Marketo Engage Cloud Configuration](/help/forms/assets/marketo-engage-cloud-configuration.png)

これで、作成したクラウドサービス設定を使用して、Marketo Engage データソースをアダプティブフォームに接続できます。

## 次の手順

Adobe Marketo EngageとAEM Formsを統合するためのクラウドサービス設定が作成されました。 以下を統合できます。

* [Marketo Engageを使用した新しいアダプティブフォーム](/help/forms/integrate-adaptive-form-with-marketo-engage.md)
* [Marketo Engageを使用した既存のアダプティブフォーム](/help/forms/use-marketo-engage-data-source-in-form.md)

## 関連記事

{{af-submit-action}}

## 関連トピック

{{marketo-engage-see-also}}
