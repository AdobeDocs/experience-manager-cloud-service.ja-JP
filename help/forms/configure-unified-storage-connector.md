---
title: AEM Forms 用の統合ストレージコネクタ（USC）の設定方法
description: AEM Forms 用の統合ストレージコネクタ（USC）の管理方法を説明します。統合ストレージコネクタ（USC）を使用して、AEM Forms を外部データストレージに接続します。
role: Admin, Developer, User
feature: Adaptive Forms, Workflow
exl-id: c93d0242-0c15-4d69-82a1-d6fcc7da4bae
source-git-commit: c17e4e70fa8cec176c908983230b03f2899bc1ca
workflow-type: ht
source-wordcount: '637'
ht-degree: 100%

---

# AEM Forms 用の統合ストレージコネクタ（USC）の管理 {#manage-unified-storage-connector}

統合ストレージコネクタ（USC）を使用すると、AEM Forms を外部データストレージに接続できます。

例えば、アダプティブフォームのフィールドに値を入力し、そのアダプティブフォームを AEM ワークフローに送信することができます。さらに、Microsoft Azure ストレージサーバーなどの外部ストレージにデータを保存するように AEM ワークフローを設定することもできます。AEM ワークフローと外部ストレージの間の接続を作成するには、統合ストレージコネクタ（USC）を使用します。

## AEM ワークフローと Microsoft Azure ストレージサーバーの接続 {#connect-workflows-with-azure}

Azure ストレージ設定を作成し、統合ストレージコネクタ（USC）を使用してその設定を参照します。そうすれば、データストレージを外部化して Azureストレージサーバーに接続するように AEM ワークフローモデルを設定することができます。

### [!DNL Azure] ストレージ設定の作成 {#create-azure-storage-configuration}

これらの手順を実行する前に、[!DNL Azure] ストレージアカウントと、[!DNL Azure] ストレージアカウントへのアクセスを許可するためのアクセスキーがあることを確認してください。

[!DNL Azure] ストレージ設定を作成するには、次の手順を実行します。

1. **[!UICONTROL ツール]**／**[!UICONTROL クラウドサービス]**／**[!UICONTROL Azure ストレージ]**&#x200B;に移動します。
1. 設定を作成するフォルダーを選択して、「**[!UICONTROL 作成]**」を選択します。
1. 「**[!UICONTROL タイトル]**」フィールドで設定のタイトルを指定します。
1. 「**[!UICONTROL Azure ストレージアカウント]**」フィールドで [!DNL Azure] ストレージアカウントの名前を指定します。
1. Azure ストレージアカウントにアクセスするためのキーを「**[!UICONTROL Azure アクセスキー]**」フィールドで指定し、「**[!UICONTROL 保存]**」を選択します。

### AEM ワークフロー用の統合ストレージコネクタ（USC）の設定 {#configure-unified-storage-connector-workflows}

AEM ワークフロー用の統合ストレージコネクタ（USC）を設定するには、次の手順を実行します。

1. **[!UICONTROL ツール]**／**[!UICONTROL Forms]**／**[!UICONTROL 統合ストレージコネクタ]**&#x200B;に移動します。

1. 「**[!UICONTROL ワークフロー]**」セクションで、「ストレージ」ドロップダウンリストから「**[!UICONTROL Azure]**」を選択します。
1. 「**[!UICONTROL ストレージ設定パス]**」フィールドで、[Azure ストレージ設定の設定パス](#create-azure-storage-configuration)を指定します。
1. 「**[!UICONTROL 公開]**」を選択してから、「**[!UICONTROL 保存]**」を選択して設定を保存します。

### 外部データストレージを使用するための AEM ワークフローモデルの設定 {#configure-workflow-external-data-storage}

外部データストレージを使用するように AEM ワークフローモデルを設定するには、次の手順を実行します。

1. **[!UICONTROL ツール]**／**[!UICONTROL ワークフロー]**／**[!UICONTROL モデル]**&#x200B;に移動します。
1. モデル名を選択し、「**[!UICONTROL 編集]**」をタップします。
1. 「ページ情報」アイコンを選択し、「**[!UICONTROL プロパティを開く]**」を選択します。
1. 「**[!UICONTROL ワークフローのデータストレージを具体化]**」を選択します。
1. 「**[!UICONTROL 保存して閉じる]**」を選択して、プロパティを保存します。

>[!NOTE]
>
>外部データストレージを使用するように AEM ワークフローモデルを設定する場合、「タスクを割り当て」ステップをドラフトとして保存するオプションと、「タスクを割り当て」ステップの履歴を取得するオプションは無効です。

### AEM ワークフローで外部データストレージを使用する場合のガイドライン {#guidelines-workflows-external-data-storage}

AEM ワークフローを使用し、Microsoft Azure ストレージサーバーなどの外部データストレージにデータを保存する場合のガイドラインを以下に示します。

* ワークフローモデルステップで入出力データファイルと添付ファイルを定義する際は、変数を使用してデータを格納します。「**[!UICONTROL ペイロードを基準とする]**」オプションと「**[!UICONTROL 絶対パスで利用可能]**」オプションを選択しないでください。**[!UICONTROL 外部データストレージを使用するように AEM ワークフローモデルを設定]**&#x200B;したら、「[ペイロードを基準とする](#configure-workflow-external-data-storage)」オプションと「**[!UICONTROL 絶対パスで利用可能]**」オプションは自動的には表示されません。

* アダプティブフォームを AEM ワークフローに送信する際は、変数を使用してデータファイルと添付ファイルを格納します。アダプティブフォームを AEM ワークフローに送信する際に、「**[!UICONTROL ペイロードを基準とする]**」オプションを選択しないでください。[外部データストレージを使用するように AEM ワークフローモデルを設定](#configure-workflow-external-data-storage)したら、「**[!UICONTROL ペイロードを基準とする]**」オプションは自動的には表示されません。

* ワークフローモデルでカスタム AEM ワークフローステップを使用して CRX DE リポジトリーにデータを保存しないでください。

* [外部データストレージ用に AEM ワークフローモデルを設定](#configure-workflow-external-data-storage)する場合、AEM インボックス内の作業項目が外部ストレージとしてマークされたワークフローに属しているとカスタム列の値は取得されないので、AEM インボックス用にカスタム列を作成しないでください。

>[!MORELIKETHIS]
>
>* [AEM Forms のデータソースを設定](/help/forms/configure-data-sources.md)
>* [AEM Forms の Azure ストレージを設定](/help/forms/configure-azure-storage.md)
>* [Microsoft Dynamics 365 の統合](/help/forms/configure-msdynamics.md)
>  [AEM Sites ページへのフォームポータルの追加](/help/forms/configure-forms-portal.md)
