---
title: Migration Utility Tool/AEM基盤コンポーネントに基づいてアダプティブ Formsをコアコンポーネントベースのフォームに変換する最新のツール
description: Migration Utility/AEM Modernize Toolsをインストールして使用し、基盤コンポーネントに基づくアダプティブ Formsをコアコンポーネントベースのフォームに変換する方法を説明します。
Keywords: Migration Utility Tool, Convert Adaptive Forms based on Foundation Components to Core Component based forms, Convert Foundation forms to Core Components forms, Using Modernizer Tool to convert Foundation Components to Core Components in forms.
role: User, Developer, Admin
features: core components
hide: true
badgeSaas: label="AEM Forms" type="Positive" tooltip="AEM Formsに適用）。"
exl-id: ee71a576-96a7-4c81-b3a3-1d678f010cba
feature: Adaptive Forms, Core Components
source-git-commit: 77f7d21eed1322de768ee07e3518638f60e3ae40
workflow-type: tm+mt
source-wordcount: '1109'
ht-degree: 11%

---

# はじめに

<span class="preview">この機能は、アーリーアダプタープログラムで利用できます。 早期導入プログラムに登録し、機能へのアクセスをリクエストするには、公式メール ID から aem-forms-ea@adobe.com にメールを送信してください。</span>

Forms Conversion Utilityは、[AEM Modernize Tool](https://opensource.adobe.com/aem-modernize-tools/) スイートの一部であり、従来の基盤コンポーネントで構築されたアダプティブ Formsを、コアコンポーネントでサポートされる最新の機能を活用したフォームに簡単に変換するのに役立ちます。

## AEM Modernize Toolsとは何ですか？

[AEM Modernize Tools](https://opensource.adobe.com/aem-modernize-tools/)とは、Adobe Experience Manager （AEM） プロジェクトの最新化または更新プロセスを促進するために設計された一連のユーティリティまたはソフトウェア アプリケーションを指します。 これらのツールは通常、AEM内の古いコンポーネントまたは機能を、より新しい、より効率的で、サポートされている代替品に変換するのに役立ちます。 Forms変換ユーティリティは、AEM Modernize Toolsの下にインストールされ、基盤コンポーネントに基づくアダプティブ Formsをコアコンポーネントベースのフォームに変換します。

Forms変換ユーティリティは、古い基盤コンポーネントに基づくアダプティブ Formsを、新しいコアコンポーネントベースのフォームに変換します。 このコンバージョンプロセスにより、最新の標準や機能に即したフォームが作成され、AEM内でのパフォーマンス、互換性、メンテナンスの容易性が向上する可能性があります。

![AEM Modernize Tools](/help/forms/assets/aem-modernize-tools.png)

>[!NOTE]
> 
>AEM Modernize ToolsをローカルのAEM設定にインストールすることをお勧めします。 基盤コンポーネントに基づくアダプティブ Formsを、コアコンポーネントベースのフォームに移行します。 フォームとそのアセットをダウンロードします。 次に、フォームとそのアセットを必要な環境にアップロードします。

## AEM Modernize Toolsの使用中の考慮事項 {#considerations}

* コンバージョンが成功すると、フォームに適用されたすべてのルールが削除されます。 ルールは自動的には移行されません。 これらのルールを手動で再作成し、変換されたフォームに適用する必要があります。
* 元のフォームで使用されている翻訳設定は引き継がれません。 変換したフォームの翻訳を再構成します。
* 基盤コンポーネント上に構築されたフォームにスクリプトまたはカスタム関数ルールが含まれている場合は、コアコンポーネントに基づいて、変換されたフォームにこれらのルールを書き換える必要があります。
* 次のOOTB基盤コンポーネントは、コアコンポーネントではまだサポートされていないため、変換されたフォームで削除されます。

   * Adobe Sign ブロック
   * グラフ
   * ファイル添付リスト
   * 脚注プレースホルダー
   * 画像選択
   * 「次へ」ボタン
   * 前へボタン
   * 手書き署名
   * 概要ステップ
   * ツールバー

## AEM Modernize Toolsを使用するための前提条件

* [AEM Forms](/help/forms/setup-local-development-environment.md)のローカル開発環境を設定します。
* お使いの AEM Cloud Service 環境でアダプティブフォームコアコンポーネントを有効にするには、最新版をインストールします。
* [!DNL forms-users] グループへのユーザーの追加。 [!DNL forms-users] グループのメンバーには、アダプティブフォームを作成する権限があります。
* 次の役割を持つユーザーには、AEM環境内にAEM Modernize Toolsをインストールする権限があります。

   * 開発者の役割
   * 管理者の役割

フォーム固有のユーザーグループの詳細なリストについては、[ グループと権限](forms-groups-privileges-tasks.md)を参照してください。

## AEM Modernize Toolsのインストールと設定

AEM Modernize Toolsをインストールして設定するには：

1. [AEM Modernize ToolsをローカルのAEM Forms環境にインストール](#install-aem-modernize-Tools)
1. [ローカルのAEM Forms環境でAEM Modernize Toolsを有効にする](#enable-aem-modernize-Tools)

### AEM Modernize ToolsをローカルのAEM Forms環境にインストール {#install-aem-modernize-Tools}

次の手順を実行して、AEM Modernize ToolsをローカルのAEM Forms環境にインストールします。

1. コマンドプロンプトまたはターミナルを開きます。
1. ローカルのAEM オーサーサービスを開始します。 例えば、から次のコードを実行して、ローカルのAEM オーサーインスタンスを起動します。

   `java -jar aem-author-p4502.jar`

1. ローカルシステムで[AEM Modernize Tool](https://github.com/adobe/forms-modernizer) リポジトリを複製します。

   ```Shell
   git clone [Path of Git repository of AEM Modernize Tool]
   ```

   コマンドを正常に実行すると、コンピューターでAEM Modernize Tool リポジトリのローカルコピーが利用可能になります。

1. ローカル システムの`[AEM Modernize Tool Repository]`に移動します。
1. 次のコマンドを実行します。

   ```Shell
       mvn clean install 
   ```

![ インストールに成功した画像](/help/forms/assets/aem-modernize-install-steps.png)

インストールが正常に完了すると、AEM Modernize Toolsがお客様の環境で使用できるようになります。

![AEM Migration Utility Toolを有効にする](/help/forms/assets/enable-aem-modernizer-tools.png)


### ローカルのAEM Forms環境でAEM Modernize Toolsを有効にする{#enable-aem-modernize-Tools}

AEM環境でAEM Modernize Toolsを有効にして使用するには、基盤コンポーネントをコアコンポーネントに移行するためのルールをマッピングすることが重要です。

1. オーサーインスタンスにログインします。
1. `http://[host]:[port]/system/console/configMgr` に移動します。
1. `AEM Modernize Tools - Component Rewrite Rule Service`を検索して編集します。
1. `Component Rule Paths`を`/apps/forms-modernizer/rules`として追加します。
1. 「**保存**」をクリックして、変更を保存します。

![AEM Modernize Component Rule](/help/forms/assets/aem-modernize-tools-component-rule.png)

## フォーム変換ユーティリティを実行して、基盤コンポーネント ベースのフォームをコアコンポーネント ベースのフォームに変換します

1. **[!UICONTROL ツール/AEM Modernize Tools/Forms Conversion]**&#x200B;に移動します。

   ![AEM Modernize Toolsを選択](/help/forms/assets/aem-modernize-tools-select-form.png)

1. 「**[!UICONTROL Forms コンバージョン]**」オプションを選択します。

   ![Forms コンバージョンオプションを選択](/help/forms/assets/aem-modernize-forms-conversion.png)

1. 「**作成**」をクリックして、新しいジョブを作成します。

   ![AEM Modernize Tools Create Job](/help/forms/assets/aem-modernize-tools-create-job.png)

1. **[!UICONTROL ジョブ名]**&#x200B;を指定します。
1. 「**[!UICONTROL フォーム]**」タブでは、次のいずれかのオプションを選択できます。

   * **なし**：フォームの変換を開始する前に、基盤コンポーネント ベースのフォームのコピーを作成しない場合は、このオプションを選択します。
   * **復元**：フォームの変換を開始する前の状態にフォームを復元するオプションを選択します。
   * **ターゲットにコピー**: フォームの変換を開始する前に、基盤コンポーネント ベースのフォームのコピーを作成するオプションを選択します。

   この場合、「**ターゲットにコピー**」オプションが選択されています。 「**ターゲットにコピー**」オプションが選択されている場合、**[!UICONTROL Source Path]**&#x200B;および&#x200B;**[!UICONTROL Target Path]** オプションが表示されます。

1. **[!UICONTROL Source パス]**&#x200B;に`source folder`名を指定します。
1. **[!UICONTROL ターゲットパス]**&#x200B;に`target folder`名を指定します。
1. 「**[!UICONTROL 次へ]**」を選択します。
1. 「**[!UICONTROL Formsを追加]**」をクリックします。 `source folder`のすべてのフォームが画面に表示されます。
1. 基盤コンポーネントに基づくアダプティブ Formsを選択して、コアコンポーネントベースのフォームに変換します。 複数のフォームを選択することもできます。

   ![AEM Modernize Tools Select Form](/help/forms/assets/aem-modernize-tools-select-form.png)

1. 「**[!UICONTROL 選択]**」をクリックします。
1. 「**[!UICONTROL ジョブをスケジュール]**」をクリックして、変換プロセスを開始します。
1. 「**[!UICONTROL ページを変換]**」ダイアログボックスで「**[!UICONTROL ページを変換]**」をクリックします。

   ![AEM Modernize Tools Convert Pages](/help/forms/assets/aem-modernize-tools-convert-form.png)

   プロセスのステータスが`success`に変更されたとき。 `target folder`に移動して、変換されたフォームを表示します。

   ![AEM Modernize Tools Success](/help/forms/assets/aem-modernize-tools-success.png)

1. アダプティブフォームを選択し、> **[!UICONTROL プロパティ]**&#x200B;を選択します。 フォームプロパティページが開きます。

   ![AEM Modernize Tools Destination Folder](/help/forms/assets/aem-modernize-tools-destination-folder.png)

1. **[!UICONTROL 保存して閉じる]**を選択し、変換したフォームのプロパティを再度保存します。
   ![AEM Modernize Tools アダプティブフォームのプロパティ ](/help/forms/assets/aem-modernize-tools-af-properties.png)

基盤コンポーネント上に構築されたアダプティブフォームが、コアコンポーネント上に構築されたアダプティブフォームに変換されます。

## ベストプラクティス {#best-practices}

* 基盤コンポーネント ベースのフォームを使用していることを確認します。使用可能な[ コアコンポーネント ](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/introduction#available-components-a-breakdown-by-component-type)を持つコンポーネントのみを使用してください。 同等のコアコンポーネントを持たない基盤コンポーネントを使用する場合、基盤コンポーネントは変換されません。 その結果、フォームのオーサリング中に正しく機能しません
* 基盤コンポーネントをコアコンポーネントに変換するルールがXMLでフォーマットされていることを確認します。
