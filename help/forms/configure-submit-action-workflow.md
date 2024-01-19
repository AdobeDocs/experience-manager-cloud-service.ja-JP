---
Title: How to integrate AEM workflow with an Adaptive Form?
Description: Explore the process of automated workflow initiation with AEM Forms Submit Action.
keywords: AEMワークフロー、アダプティブフォームとAEMワークフローの統合、AEMワークフローの起動送信アクション
feature: Adaptive Forms, Core Components
source-git-commit: 95af49839d206f67ac02116730229f5b0531c5bb
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 59%

---


# AEMアダプティブフォームとAEMワークフローの統合：ビジネスプロセスの合理化

The **[!UICONTROL AEM Workflow を起動]** 送信アクションは、アダプティブフォームをAEMワークフローに関連付けます。 フォームが送信されると、関連するワークフローがオーサーインスタンスで自動的に起動します。データファイル、添付ファイル、レコードのドキュメントは、ワークフローのペイロードの場所または変数に保存できます。 ワークフローが外部データストレージ用にマークされ、外部データストレージ用に設定されている場合、変数オプションのみを使用できます。ワークフローモデルで使用できる変数のリストから選択できます。ワークフローの作成時ではなく、後の段階で外部データストレージの対象としてワークフローがマークされている場合は、必要な変数設定が適切に行われていることを確認します。

>[!NOTE]
>
>  方法を学ぶ [ワークフローモデルの作成](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=ja#extending-aem) ：ユーザーがワークフローを開始したときに実行される一連の手順を定義します。 ワークフローを一時的なものにするか、複数のリソースを使用するかなど、モデルのプロパティを定義することもできます。

AEM as a Cloud Serviceには、フォーム送信を処理するための標準の様々な送信アクションが用意されています。 これらのオプションについて詳しくは、 [アダプティブフォーム送信アクション](/help/forms/configure-submit-actions-core-components.md)  記事。

## メリット

AEMワークフローを Adaptive Formsと統合する利点の一部を次に示します。

* AEMワークフロー統合を使用すると、フォーム送信に関わる複雑なビジネスプロセスを自動化できます。
* AEM Workflow は条件ロジックをサポートしているので、フォームデータや外部要因に基づいて動的に判断を下すことができます。
* AEMワークフローでは、定義済みのルールと条件に基づいてタスクをルーティングし、タスクが適切な個人またはグループに割り当てられるようにします。

<!--
## Prerequisites

Before using the **[!UICONTROL Invoke an AEM Workflow]** Submit Action configure the following for the **[!UICONTROL AEM DS settings service]** configuration: 

* **[!UICONTROL Processing Server URL]**: The Processing Server is the server where the Forms or AEM Workflow is triggered. This can be same as the URL of the AEM author instance or another server.

* **[!UICONTROL Processing Server User Name]**: Workflow user's username

* **[!UICONTROL Processing Server Password]**: Workflow user's password -->

## AEM Workflow と Adaptive Formsの統合 {#steps-to-integrate-workflow-with-af}

で自動処理を設定するには [AEM Workflow](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=ja#extending-aem) アダプティブフォームの場合は、次の手順を実行します。

1. コンテンツブラウザーを開き、アダプティブフォームの&#x200B;**[!UICONTROL ガイドコンテナ]**&#x200B;コンポーネントを選択します。
1. ガイドコンテナプロパティ ![ガイドプロパティ](/help/forms/assets/configure-icon.svg) アイコンをクリックします。アダプティブフォームコンテナダイアログボックスが開きます。
1. 「**[!UICONTROL 送信]**」タブをクリックします。
1. 次から： **[!UICONTROL 送信アクション]** ドロップダウンリストで、「 **[!UICONTROL AEM Workflow を起動]** .
   ![電子メールを送信のアクション設定](/help/forms/assets/configure-invoke-aem-workflow.png)

1. 次の中からワークフローモデルを選択： **[!UICONTROL ワークフローモデル]** 」ドロップダウンリストから選択できます。
1. 次の中からオプションを選択します。 **[!UICONTROL 次を使用してデータファイルを保存]** 」ドロップダウンリストから選択できます。

   **データファイル**：アダプティブフォームに送信されたデータを含みます。「**[!UICONTROL データファイルパス]**」オプションを使用して、ファイル名とペイロードを基準とするファイルのパスを指定できます。例えば、`/addresschange/data.xml` パスは、`addresschange` という名前のフォルダーを作成し、ペイロードを基準に配置します。フォルダー階層を作成せずに、`data.xml` のみを指定して、送信されたデータのみを送信することもできます。ワークフローが外部データストレージ用にマークされている場合は、「変数」オプションを使用し、ワークフローモデルで使用可能な変数のリストから変数を選択します。

1. 次の中からオプションを選択します。 **[!UICONTROL 次を使用して添付ファイルを保存]** 」ドロップダウンリストから選択できます。

   **添付ファイル**：「**[!UICONTROL 添付ファイルのパス]**」オプションを使用して、アダプティブフォームにアップロードされた添付ファイルの保存先となるフォルダー名を指定できます。フォルダーがペイロードを基準に作成されます。ワークフローが外部データストレージ用にマークされている場合は、「変数」オプションを使用し、ワークフローモデルで使用可能な変数のリストから変数を選択します。

1. 次の中からオプションを選択します。 **[!UICONTROL を使用したレコードのドキュメント]** 」ドロップダウンリストから選択できます。

   **レコードのドキュメント**：アダプティブフォーム用に生成されたレコードのドキュメントを含みます。「**[!UICONTROL レコードのドキュメントパス]**」オプションを使用して、レコードのドキュメントファイル名と、ペイロードを基準にファイルのパスを指定できます。例えば、`/addresschange/DoR.pdf` パスは、ペイロードを基準に `addresschange` という名前のフォルダーを作成し、ペイロードを基準に `DoR.pdf` を配置します。`DoR.pdf` のみを指定して、フォルダー階層を作成せずに、レコードのドキュメントのみを保存することもできます。ワークフローが外部データストレージ用にマークされている場合は、「変数」オプションを使用し、ワークフローモデルで使用可能な変数のリストから変数を選択します。
1. 「**[!UICONTROL 完了]**」をクリックします。

>[!NOTE]
>
> 詳細情報： [Forms中心のAEMワークフロー — ビジネスプロセスを自動化するためのステップリファレンス](/help/forms/aem-forms-workflow-step-reference.md).

<!--
## Best Practices

* When configuring the **[!UICONTROL Invoke an AEM Workflow]** Submit Action, select the appropriate workflow model that aligns with the desired business process.
* In case, the workflow involves external data storage, be sure to configure the workflow accordingly. It is recommended to set up variables appropriately and in accordance with any external storage requirements. -->

## 関連記事

{{af-submit-action}}