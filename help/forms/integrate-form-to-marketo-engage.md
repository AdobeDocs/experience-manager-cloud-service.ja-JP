---
Title: How to Integrate Marketo Engage with AEM Forms?
Description: Learn how to integrate your Marketo Engage instance with AEM Forms.
Keywords: How to connect a Marketo instance with form? , Connect a form to Marketo, Integrate a form with Marketo Engage, Integrate an Adaptive Form with a Marketo instance.
Feature: Adaptive Forms, Form Data Model
Role: User, Developer
source-git-commit: 681c194f997ab66f93beedad4eea273614e6797d
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 6%

---


# Marketo EngageとAEM Formsの統合

<span class="preview">機能は、早期導入プログラムで利用できます。早期導入プログラムに参加し、機能へのアクセスをリクエストするには、公式のメール ID で aem-forms-ea@adobe.com までメールを送信してください。</span>

AEM Formsと [Adobe Marketo Engage](https://experienceleague.adobe.com/en/docs/marketo/using/home) の統合により、Marketo Engageの機能を活用して、キャプチャされたデータからビジネスロジックを作成し、スマートキャンペーンやメールの自動処理などのワークフローを自動化できます。 設定されたフォームは、キャプチャされたデータをMarketo Engageに送信して処理できます。

## Marketo Engageとフォームを統合する利点

AEM フォームをAdobe Marketo Engageに接続する利点は次のとおりです。

* **統合のシンプル化**：フォームとMarketo Engageを接続すると、別のフォームデータモデルを作成する必要がなくなります。 統合プロセスは簡単で使いやすいです。
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

## Marketo Engageとフォームの統合に関する考慮事項

Marketo EngageとAEM Formsの統合時の考慮事項：

* AEMは、様々なMarketo データベースのうち、人物（リード）データベースのみをサポートしています。
* Marketoでは、ユーザー定義オブジェクトとして [10 個のカスタムオブジェクトの作成 ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/marketo-custom-objects/add-marketo-custom-object-fields) を使用して、リードの標準フィールドを超えて専用のデータを保存し、独自のビジネスニーズをサポートできます。
* AEMがカスタムオブジェクトにアクセスできるのは、リードデータベースに関連付けられている場合のみです

## Marketo Engageとフォームの統合の前提条件

Marketo EngageとAEM Formsを接続するための前提条件を以下に示します。

* 有効なAdobe Marketo Engage ライセンス
* クラウド設定を作成するための [ クライアント ID およびクライアント秘密鍵を取得 ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/additional-integrations/create-a-custom-service-for-use-with-rest-api)Marketo Engageの作業用インスタンス。

## AEM Forms（アダプティブForms）をMarketo Engageと接続するためのクラウドサービス設定を作成します

![ワークフロー](/help/forms/assets/workflow-marketo-1.png)

クラウド設定は、Experience ManagerインスタンスをAdobe Marketo Engage インスタンスに接続します。 Marketo Engageのクラウド設定を作成するには、以下の手順を実行します。

1. **ツール** / **Cloud Service** / **Marketo Engage** に移動します。

   ![Marketo Engage](/help/forms/assets/marketo-engage.png)

1. 設定をホストするフォルダーを開き、「**作成**」をクリックします。 **Marketo Engage設定を作成** ウィンドウが表示されます。

   >[!NOTE]
   >
   > また、[ クラウドサービス設定用フォルダーを設定する ](/help/forms/configure-data-sources.md#configure-folder-for-cloud-service-configurations) こともできます。

1. サービスに接続するための設定と資格情報の **タイトル** を指定します。 認証資格情報は、Adobe Marketo Engage ダッシュボードから取得できます。
   * **クライアント ID** および **クライアントシークレット** は、**管理者**/**統合**/**LaunchPoint** でカスタムサービスを選択し、「**詳細を表示** をクリックして使用できます。
   * **ID URL** は、**管理者**/**統合**/**Web サービス** で、「**REST API**」セクションの **ID** として使用できます。

1. **接続** をクリックします。  接続に成功した場合、`Authentication Successful` のメッセージが表示されます。
1. **[!UICONTROL 作成]** をクリックして、クラウド設定を保存します。

![Marketo Engage クラウド構成 ](/help/forms/assets/marketo-engage-cloud-configuration.png)

これで、作成されたクラウドサービス設定を使用して、Marketo Engageデータソースをアダプティブフォームに接続できます。

## 次の手順

Adobe Marketo EngageをAEM Formsと統合するためのクラウドサービス設定を作成しました。 これで、以下を統合できます。
* [Marketo Engageを持つ新しいアダプティブフォーム](/help/forms/integrate-adaptive-form-with-marketo-engage.md)
* [Marketo Engageを使用した既存のアダプティブフォーム](/help/forms/use-marketo-engage-data-source-in-form.md)

## 関連記事

{{af-submit-action}}

## 関連トピック

{{marketo-engage-see-also}}



