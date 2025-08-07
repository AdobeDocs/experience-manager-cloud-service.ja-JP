---
Title: How to integrate AEM workflow with an Adaptive Form?
Description: Explore the process of automated workflow initiation with AEM Forms Submit Action.
keywords: AEM ワークフロー、アダプティブフォームと AEM ワークフローの統合、「AEM ワークフローの起動」送信アクション
feature: Adaptive Forms, Core Components
exl-id: b7788e3d-acd8-4867-b232-f9767cf6b2f5
role: User, Developer
source-git-commit: dc9fc0c7d886d976f9b0b9daa955f98402341527
workflow-type: tm+mt
source-wordcount: '1413'
ht-degree: 89%

---

# AEM アダプティブフォームと AEM ワークフローの統合：ビジネスプロセスの合理化

「**[!UICONTROL AEM ワークフローを起動]**」送信アクションは、アダプティブフォームを AEM ワークフローと関連付けます。フォームが送信されると、関連するワークフローがオーサーインスタンスで自動的に起動します。データファイル、添付ファイル、レコードのドキュメントは、ワークフローのペイロードの場所または変数に保存できます。ワークフローが外部データストレージ用にマークされ、外部データストレージ用に設定されている場合、変数オプションのみを使用できます。ワークフローモデルで使用できる変数のリストから選択できます。ワークフローの作成時ではなく、後の段階で外部データストレージの対象としてワークフローがマークされている場合は、必要な変数設定が適切に行われていることを確認します。

>[!NOTE]
>
>  ユーザーがワークフローを開始したときに実行される一連のステップを定義する[ワークフローモデルを作成する](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=ja#extending-aem)方法について説明します。ワークフローを一時的なものにするか、複数のリソースを使用するかなど、モデルのプロパティを定義することもできます。

AEM as a Cloud Service では、フォーム送信を処理するための様々な送信アクションが標準で提供されます。これらのオプションについて詳しくは、[アダプティブフォーム送信アクション](/help/forms/configure-submit-actions-core-components.md)の記事をご覧ください。

## メリット

AEM ワークフローをアダプティブフォームと統合するいくつかの利点を次に示します。

* AEM ワークフロー統合を使用すると、フォーム送信に関わる複雑なビジネスプロセスを自動化できます。
* AEM Workflow は条件ロジックをサポートしているので、フォームデータや外部要因に基づいて動的に判断を下すことができます。
* AEM ワークフローでは、定義済みのルールと条件に基づいてタスクをルーティングし、タスクが適切な個人またはグループに割り当てられるようにします。

<!--
## Prerequisites

Before using the **[!UICONTROL Invoke an AEM Workflow]** Submit Action configure the following for the **[!UICONTROL AEM DS settings service]** configuration: 

* **[!UICONTROL Processing Server URL]**: The Processing Server is the server where the Forms or AEM Workflow is triggered. This can be same as the URL of the AEM author instance or another server.

* **[!UICONTROL Processing Server User Name]**: Workflow user's username

* **[!UICONTROL Processing Server Password]**: Workflow user's password -->

## AEM ワークフローとアダプティブフォームを統合する {#steps-to-integrate-workflow-with-af}

>[!BEGINTABS]

>[!TAB 基盤コンポーネント]

基盤コンポーネントに基づくアダプティブフォームに対して [AEM ワークフロー ](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=ja#extending-aem) を使用して自動プロセスを設定するには、次の手順を実行します。

1. 編集用にアダプティブフォームを開き、アダプティブフォームのコンテナプロパティの「**[!UICONTROL 送信]**」セクションに移動します。
1. **[!UICONTROL 送信アクション]** ドロップダウンリストから、**送信アクション** を **[!UICONTROL AEM ワークフローの呼び出し]** として選択します。
1. 「**[!UICONTROL ワークフローモデル]**」ドロップダウンリストからワークフローモデルを選択します。
1. 「**&#x200B;** を使用してデータファイルを保存」ドロップダウンリストからオプションを選択します。

   **データファイル**：アダプティブフォームに送信されたデータを含みます。「**[!UICONTROL データファイルパス]**」オプションを使用して、ファイル名とペイロードを基準とするファイルのパスを指定できます。例えば、`/addresschange/data.xml` パスは、`addresschange` という名前のフォルダーを作成し、ペイロードを基準に配置します。フォルダー階層を作成せずに、`data.xml` のみを指定して、送信されたデータのみを送信することもできます。ワークフローが外部データストレージ用にマークされている場合は、「変数」オプションを使用し、ワークフローモデルで使用可能な変数のリストから変数を選択します。

   ![invoke-workflow-fc](/help/forms/assets/invoke-workflow-fc.png)

1. 「**&#x200B;** を使用して添付ファイルを保存」ドロップダウンリストからオプションを選択します。

   **添付ファイル**：「**[!UICONTROL 添付ファイルのパス]**」オプションを使用して、アダプティブフォームにアップロードされた添付ファイルの保存先となるフォルダー名を指定できます。フォルダーがペイロードを基準に作成されます。ワークフローが外部データストレージ用にマークされている場合は、「変数」オプションを使用し、ワークフローモデルで使用可能な変数のリストから変数を選択します。

1. 「**&#x200B;** を使用したレコードのドキュメント」ドロップダウンリストからオプションを選択します。

   **レコードのドキュメント**：アダプティブフォーム用に生成されたレコードのドキュメントを含みます。「**[!UICONTROL レコードのドキュメントパス]**」オプションを使用して、レコードのドキュメントファイル名と、ペイロードを基準にファイルのパスを指定できます。例えば、`/addresschange/DoR.pdf` パスは、ペイロードを基準に `addresschange` という名前のフォルダーを作成し、ペイロードを基準に `DoR.pdf` を配置します。`DoR.pdf` のみを指定して、フォルダー階層を作成せずに、レコードのドキュメントのみを保存することもできます。ワークフローが外部データストレージ用にマークされている場合は、「変数」オプションを使用し、ワークフローモデルで使用可能な変数のリストから変数を選択します。
1. 「**[!UICONTROL 完了]**」をクリックします。

   >[!NOTE]
   >
   > 詳しくは、[Forms 中心の AEM ワークフロー - ステップリファレンスを使用して、ビジネスプロセスを自動化](/help/forms/aem-forms-workflow-step-reference.md)を参照してください。

>[!TAB コアコンポーネント]

コアコンポーネントに基づくアダプティブフォームに対して [AEM ワークフロー ](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=ja#extending-aem) を使用して自動プロセスを設定するには、次の手順を実行します。

1. コンテンツブラウザーを開き、アダプティブフォームの&#x200B;**[!UICONTROL ガイドコンテナ]**&#x200B;コンポーネントを選択します。
1. ガイドコンテナプロパティ ![ガイドプロパティ](/help/forms/assets/configure-icon.svg) アイコンをクリックします。 アダプティブフォームコンテナダイアログボックスが開きます。
1. 「**[!UICONTROL 送信]**」タブをクリックします。
1. **[!UICONTROL 送信アクション]**&#x200B;ドロップダウンリストから「**[!UICONTROL AEM ワークフローを起動]**」を選択します。

   ![「メールを送信」のアクション設定](/help/forms/assets/configure-invoke-aem-workflow.png)

1. 「**[!UICONTROL ワークフローモデル]**」ドロップダウンリストからワークフローモデルを選択します。
1. 「**&#x200B;** を使用してデータファイルを保存」ドロップダウンリストからオプションを選択します。

   **データファイル**：アダプティブフォームに送信されたデータを含みます。「**[!UICONTROL データファイルパス]**」オプションを使用して、ファイル名とペイロードを基準とするファイルのパスを指定できます。例えば、`/addresschange/data.xml` パスは、`addresschange` という名前のフォルダーを作成し、ペイロードを基準に配置します。フォルダー階層を作成せずに、`data.xml` のみを指定して、送信されたデータのみを送信することもできます。ワークフローが外部データストレージ用にマークされている場合は、「変数」オプションを使用し、ワークフローモデルで使用可能な変数のリストから変数を選択します。

1. 「**&#x200B;** を使用して添付ファイルを保存」ドロップダウンリストからオプションを選択します。

   **添付ファイル**：「**[!UICONTROL 添付ファイルのパス]**」オプションを使用して、アダプティブフォームにアップロードされた添付ファイルの保存先となるフォルダー名を指定できます。フォルダーがペイロードを基準に作成されます。ワークフローが外部データストレージ用にマークされている場合は、「変数」オプションを使用し、ワークフローモデルで使用可能な変数のリストから変数を選択します。

1. 「**&#x200B;** を使用したレコードのドキュメント」ドロップダウンリストからオプションを選択します。

   **レコードのドキュメント**：アダプティブフォーム用に生成されたレコードのドキュメントを含みます。「**[!UICONTROL レコードのドキュメントパス]**」オプションを使用して、レコードのドキュメントファイル名と、ペイロードを基準にファイルのパスを指定できます。例えば、`/addresschange/DoR.pdf` パスは、ペイロードを基準に `addresschange` という名前のフォルダーを作成し、ペイロードを基準に `DoR.pdf` を配置します。`DoR.pdf` のみを指定して、フォルダー階層を作成せずに、レコードのドキュメントのみを保存することもできます。ワークフローが外部データストレージ用にマークされている場合は、「変数」オプションを使用し、ワークフローモデルで使用可能な変数のリストから変数を選択します。
1. 「**[!UICONTROL 完了]**」をクリックします。

   >[!NOTE]
   >
   > 詳しくは、[Forms 中心の AEM ワークフロー - ステップリファレンスを使用して、ビジネスプロセスを自動化](/help/forms/aem-forms-workflow-step-reference.md)を参照してください。

>[!TAB ユニバーサルエディター]

ユニバーサルエディターで作成されたアダプティブフォームの [0&rbrace;AEM ワークフロー &rbrace; で自動プロセスを設定するには、次の手順を実行します。](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=ja#extending-aem)

1. アダプティブフォームを編集用に開きます。
1. エディターで **フォームプロパティを編集** 拡張機能をクリックします。
**フォームのプロパティ** ダイアログが表示されます。

   >[!NOTE]
   >
   > * ユニバーサルエディターインターフェイスに **フォームプロパティを編集** アイコンが表示されない場合は、Extension Managerで **フォームプロパティを編集** 拡張機能を有効にします。
   > * ユニバーサルエディターで拡張機能を有効または無効にする方法については [&#128279;](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)Extension Manager機能のハイライト &rbrace; の記事を参照してください。

1. 「**送信**」タブをクリックし、「**[!UICONTROL AEM ワークフローの呼び出し]**」送信アクションを選択します。


   ![「メールを送信」のアクション設定](/help/forms/assets/invoke-service-ue.png)

1. 「**[!UICONTROL ワークフローモデル]**」ドロップダウンリストからワークフローモデルを選択します。
1. 「**&#x200B;** を使用してデータファイルを保存」ドロップダウンリストからオプションを選択します。

   **データファイル**：アダプティブフォームに送信されたデータを含みます。「**[!UICONTROL データファイルパス]**」オプションを使用して、ファイル名とペイロードを基準とするファイルのパスを指定できます。例えば、`/addresschange/data.xml` パスは、`addresschange` という名前のフォルダーを作成し、ペイロードを基準に配置します。フォルダー階層を作成せずに、`data.xml` のみを指定して、送信されたデータのみを送信することもできます。ワークフローが外部データストレージ用にマークされている場合は、「変数」オプションを使用し、ワークフローモデルで使用可能な変数のリストから変数を選択します。

1. 「**&#x200B;** を使用して添付ファイルを保存」ドロップダウンリストからオプションを選択します。

   **添付ファイル**：「**[!UICONTROL 添付ファイルのパス]**」オプションを使用して、アダプティブフォームにアップロードされた添付ファイルの保存先となるフォルダー名を指定できます。フォルダーがペイロードを基準に作成されます。ワークフローが外部データストレージ用にマークされている場合は、「変数」オプションを使用し、ワークフローモデルで使用可能な変数のリストから変数を選択します。

1. 「**&#x200B;** を使用したレコードのドキュメント」ドロップダウンリストからオプションを選択します。

   **レコードのドキュメント**：アダプティブフォーム用に生成されたレコードのドキュメントを含みます。「**[!UICONTROL レコードのドキュメントパス]**」オプションを使用して、レコードのドキュメントファイル名と、ペイロードを基準にファイルのパスを指定できます。例えば、`/addresschange/DoR.pdf` パスは、ペイロードを基準に `addresschange` という名前のフォルダーを作成し、ペイロードを基準に `DoR.pdf` を配置します。`DoR.pdf` のみを指定して、フォルダー階層を作成せずに、レコードのドキュメントのみを保存することもできます。ワークフローが外部データストレージ用にマークされている場合は、「変数」オプションを使用し、ワークフローモデルで使用可能な変数のリストから変数を選択します。
1. 「**[!UICONTROL 完了]**」をクリックします。

   >[!NOTE]
   >
   > 詳しくは、[Forms 中心の AEM ワークフロー - ステップリファレンスを使用して、ビジネスプロセスを自動化](/help/forms/aem-forms-workflow-step-reference.md)を参照してください。

>[!ENDTABS]

<!--
## Best Practices

* When configuring the **[!UICONTROL Invoke an AEM Workflow]** Submit Action, select the appropriate workflow model that aligns with the desired business process.
* In case, the workflow involves external data storage, be sure to configure the workflow accordingly. It is recommended to set up variables appropriately and in accordance with any external storage requirements. -->

## 関連記事

{{af-submit-action}}
