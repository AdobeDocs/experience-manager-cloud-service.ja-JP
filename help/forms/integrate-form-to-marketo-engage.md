---
title: Marketo EngageとAEM Formsを統合する方法
description: Marketo Engage インスタンスをAEM Formsと統合する方法について説明します。
keywords: Marketo インスタンスとフォームの接続方法、フォームをMarketoに接続、フォームをMarketo Engageと統合、アダプティブフォームをMarketo インスタンスと統合します。
feature: Adaptive Forms, Form Data Model
role: User, Developer
exl-id: 74cd25f9-1ee1-4f3f-8e02-8714071e7c86
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 9%

---

# Marketo Engage の AEM Forms への統合

<span class="preview">機能は、早期導入プログラムで利用できます。早期導入プログラムに参加し、機能へのアクセスをリクエストするには、公式のメール ID で aem-forms-ea@adobe.com までメールを送信してください。</span>

AEM Formsと [Adobe Marketo Engage](https://experienceleague.adobe.com/en/docs/marketo/using/home) の統合により、Marketo Engageの機能を活用して、キャプチャされたデータからビジネスロジックを作成し、スマートキャンペーンやメールの自動処理などのワークフローを自動化できます。 設定されたフォームは、キャプチャされたデータをMarketo Engageに送信して処理できます。

## Marketo Engageと Forms を統合するメリット

AEM フォームをAdobe Marketo Engageに接続する利点は次のとおりです。

* **統合のシンプル化**：フォームをMarketo Engageに接続すると、別のフォームデータモデルを作成する必要がなくなります。 統合プロセスは簡単で使いやすいです。
* **自動データ取得**：フォーム送信を自動的に取得してMarketoに保存するのに役立ち、手動でのデータ入力を排除し、エラーを減らします。

* **リード管理**：フォーム送信をマーケティングデータベースに直接統合することでリード管理プロセスを合理化し、リードの追跡と育成を向上させます。

* **キャンペーンのパフォーマンスの向上**：フォームデータを使用してマーケティングキャンペーンを分析および最適化し、全体的なパフォーマンスと投資回収率（ROI）を向上させます。

* **分析とレポート**:Marketo内のMunchkinなどの堅牢な分析およびレポートツールにアクセスして、フォームとキャンペーンの効果を測定するのに役立ちます。

* **フォローアップの自動化**：フォームの送信によってトリガーされるフォローアップメールとワークフローを自動化し、リードとのタイムリーな通信を確保するのに役立ちます。

## 代替フォームソリューションよりもAEM Formsを使用する主なメリット

次の表に、他の代替フォームソリューションよりもAEM Formsを選択するいくつかの理由の概要を示します。

| **機能** | **AEM Forms** | **その他のフォームソリューション** |
|-------------------------------------|----------------------------------------------------------------------|-----------------------------------------------------------|
| **カスタマイズ** | では、特定のカスタム関数の追加、フォームアクションの調整、フィールドの動作の変更を行って、フォームのインタラクションや複雑なワークフローを強化することができます | カスタマイズのサポートなし |
| **ルールエディター** | では、ロジックおよび条件を追加するためのビルトインルールエディターをサポートしています。 | ルールエディターはサポートされていません |
| **レイアウトオプション** | 複数のレイアウトオプションをサポート | 制限付きレイアウトオプション |
| **事前入力サービス** | フォームデータを自動入力する事前入力サービスを提供します。 | 事前入力サービスはありません |
| **サイトへの埋め込み** | iFrame を使用して Sites に埋め込むことができる | iFrame を使用している Sites に埋め込めない |
| **Sites との統合の容易さ** | 他に学習は必要ありません。AEM Formsは Sites と同じスキルを使用します。 | 追加の学習が必要になる場合があります |
| **データの送信** | は様々なプラットフォームにデータを送信でき、SharePointへの接続、OneDrive への接続、Salesforceへの接続など、複数のコネクタを提供します。 | Salesforceなど、制限付きのコネクタにデータを送信できる |

## Marketo Engageと Forms の統合に関する考慮事項

Marketo EngageとAEM Formsの統合に関する考慮事項

* AEMは、様々なMarketo データベースのうち、人物（リード）データベースのみをサポートしています。
* Marketoでは、ユーザー定義オブジェクトとして [10 個のカスタムオブジェクトの作成 &#x200B;](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/marketo-custom-objects/add-marketo-custom-object-fields) を使用して、リードの標準フィールドを超えて専用のデータを保存し、独自のビジネスニーズをサポートできます。
* AEMがカスタムオブジェクトにアクセスできるのは、リードデータベースに関連付けられている場合のみです

## Marketo Engageと Forms の統合の前提条件

Marketo EngageをAEM Formsと接続するための前提条件を以下に示します。

* 有効なAdobe Marketo Engage ライセンス
* [&#x200B; クライアント ID とクライアント秘密鍵を取得 &#x200B;](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/additional-integrations/create-a-custom-service-for-use-with-rest-api) してクラウド設定を作成するためのMarketo Engageの作業用インスタンス。

## AEM Forms（アダプティブForms）をMarketo Engageに接続するクラウドサービス設定を作成します

![ワークフロー](/help/forms/assets/workflow-marketo-1.png)

>[!VIDEO](https://video.tv.adobe.com/v/3442865/engage-marketo-aem-forms-aem)

<span>このビデオは、コアコンポーネントのみに適用されます。UE／基盤コンポーネントについて詳しくは、記事を参照してください。</span>

クラウド設定によって、Experience Manager インスタンスをAdobe Marketo Engage インスタンスに接続します。 Marketo Engage クラウド設定を作成するには、以下の手順を実行します。

1. **ツール**/**クラウドサービス**/**Marketo Engage** に移動します。

   ![Marketo Engage](/help/forms/assets/marketo-engage.png)

1. 設定をホストするフォルダーを開き、「**作成**」をクリックします。 **Marketo Engage設定を作成** ウィンドウが表示されます。

   >[!NOTE]
   >
   > また、[&#x200B; クラウドサービス設定用フォルダーを設定する &#x200B;](/help/forms/configure-data-sources.md#configure-folder-for-cloud-service-configurations) こともできます。

1. サービスに接続するための設定と資格情報の **タイトル** を指定します。 認証資格情報は、Adobe Marketo Engage ダッシュボードから取得できます。

   * **クライアント ID** および **クライアントシークレット** は、**管理者**/**統合**/**LaunchPoint** でカスタムサービスを選択し、「**詳細を表示** をクリックして使用できます。
   * **ID URL** は、**管理者**/**統合**/**Web サービス** で、「**REST API**」セクションの **ID** として使用できます。

1. **接続** をクリックします。  接続に成功した場合、`Authentication Successful` のメッセージが表示されます。
1. **[!UICONTROL 作成]** をクリックして、クラウド設定を保存します。

![Marketo Engage クラウド設定 &#x200B;](/help/forms/assets/marketo-engage-cloud-configuration.png)

これで、作成されたクラウドサービス設定を使用して、Marketo Engage データソースをアダプティブフォームに接続できます。

## 次の手順

Adobe Marketo EngageをAEM Formsと統合するためのクラウドサービス設定を作成しました。 これで、以下を統合できます。

* [Marketo Engageを使用した新しいアダプティブフォーム](/help/forms/integrate-adaptive-form-with-marketo-engage.md)
* [Marketo Engageを使用した既存のアダプティブフォーム](/help/forms/use-marketo-engage-data-source-in-form.md)

## 関連記事

{{af-submit-action}}

## 関連トピック

{{marketo-engage-see-also}}
