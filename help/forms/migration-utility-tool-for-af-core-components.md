---
title: 移行ユーティリティツール/AEM基盤コンポーネントに基づくアダプティブFormsをコアコンポーネントベースのフォームに変換するためのツールを最新化します
description: 移行ユーティリティ/AEM Modernize Tools をインストールして使用し、基盤コンポーネントに基づくアダプティブFormsをコアコンポーネントベースのフォームに変換する方法を説明します。
Keywords: Migration Utility Tool, Convert Adaptive Forms based on Foundation Components to Core Component based forms, Convert Foundation forms to Core Components forms, Using Modernizer Tool to convert Foundation Components to Core Components in forms.
role: User, Developer, Admin
features: core components
hide: true
hidefromtoc: true
exl-id: ee71a576-96a7-4c81-b3a3-1d678f010cba
feature: Adaptive Forms, Core Components
source-git-commit: 92a5599ac94d5bf09311d34dd0287def46b14353
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 8%

---

# はじめに

<span class="preview"> この機能は、早期導入プログラムで利用できます。 早期導入プログラムに参加し、機能へのアクセスをリクエストするには、公式メール ID から aem-forms-ea@adobe.com にメールを送信してください。</span>

Forms変換ユーティリティは、[AEM Modernize Tool](https://opensource.adobe.com/aem-modernize-tools/) スイートの一部で、従来の基盤コンポーネントで構築されたアダプティブFormsを、サポートされている最新のコアコンポーネント機能を利用するフォームに簡単に変換するのに役立ちます。

## AEM Modernize Tools とは

[AEM Modernize Tools](https://opensource.adobe.com/aem-modernize-tools/) とは、Adobe Experience Manager（AEM）プロジェクトの最新化または更新プロセスを容易にするユーティリティまたはソフトウェアアプリケーションのセットを指します。 これらのツールは、通常、AEM内の古いコンポーネントや機能を、より効率的でサポートされている新しい代替機能に変換する際に役立ちます。 Forms変換ユーティリティは、AEM Modernize Tools の下にインストールされ、基盤コンポーネントに基づくアダプティブFormsをコアコンポーネントベースのフォームに変換します。

Forms変換ユーティリティは、古い基盤コンポーネントに基づくアダプティブFormsを、新しいコアコンポーネントベースのフォームに変換します。 この変換プロセスにより、フォームが最新の標準と機能に準拠するようになり、AEM環境のパフォーマンス、互換性、メンテナンスのしやすさが向上する可能性があります。

![AEM Modernize Tools](/help/forms/assets/aem-modernize-tools.png)

>[!NOTE]
> 
>ローカルのAEM設定にAEM Modernize Tools をインストールすることをお勧めします。 基盤コンポーネントに基づくアダプティブ Formsをコアコンポーネントベースのフォームに移行します。 フォームとそのアセットをダウンロードします。 次に、フォームとそのアセットを必要な環境にアップロードします。

## AEM Modernize Tools 使用時の考慮事項 {#considerations}

* 変換が成功すると、フォームに適用されているすべてのルールが削除されます。 ルールは自動的には移行されません。 これらのルールを手動で再作成し、変換後のフォームに適用する必要があります。
* 元のフォームで使用されていた翻訳設定は引き継がれません。 変換後のフォームの翻訳を再設定します。
* 基盤コンポーネント上で作成されたフォームにスクリプトまたはカスタム関数ルールが含まれている場合、コアコンポーネントに基づいて変換されたフォーム用にこれらを書き換える必要があります。
* 次の OOTB 基盤コンポーネントは、コアコンポーネントではまだサポートされていないので、変換された形式で削除されます。

   * Adobe Sign ブロック
   * グラフ
   * ファイル添付リスト
   * 脚注プレースホルダー
   * 画像選択
   * 次へボタン
   * 前へボタン
   * 手書き署名
   * 概要ステップ
   * ツールバー

## AEM Modernize Tools を使用するための前提条件

* [AEM Forms 用のローカル開発環境を設定](/help/forms/setup-local-development-environment.md)
* [お使いの環境でアダプティブ Forms コアコンポーネントを有効にします。](/help/forms/enable-adaptive-forms-core-components.md)
* [!DNL forms-users] グループにユーザーを追加します。 [!DNL forms-users] グループのメンバーには、アダプティブフォームを作成する権限があります。
* 次の役割を持つユーザーは、AEM環境内にAEM Modernize Tools をインストールする権限を持っています。

   * 開発者の役割
   * 管理者の役割

フォーム専用のユーザーグループの詳細なリストについては、[ グループと権限 ](forms-groups-privileges-tasks.md) を参照してください。

## AEM Modernize Tools のインストールと設定

AEM Modernize Tools をインストールして設定するには：

1. [ローカルのAEM Forms環境へのAEM Modernize Tools のインストール](#install-aem-modernize-Tools)
1. [ローカルのAEM Forms環境に対してAEM Modernize Tools を有効にする](#enable-aem-modernize-Tools)

### ローカルのAEM Forms環境へのAEM Modernize Tools のインストール {#install-aem-modernize-Tools}

次の手順を実行して、ローカルのAEM Forms環境にAEM Modernize Tools をインストールします。

1. コマンドプロンプトまたはターミナルを開きます。
1. ローカル AEM オーサーサービスを開始します。 例えば、から次のコードを実行して、ローカルのAEM オーサーインスタンスを開始します。

   `java -jar aem-author-p4502.jar`

1. ローカルシステムで [AEM Modernize Tool](https://github.com/adobe/forms-modernizer) リポジトリのクローンを作成します。

   ```Shell
   git clone [Path of Git repository of AEM Modernize Tool]
   ```

   コマンドを正常に実行すると、お使いのマシン上でAEM Modernize Tool リポジトリのローカルコピーが利用可能になります。

1. ローカルシステムの `[AEM Modernize Tool Repository]` に移動します。
1. 次のコマンドを実行します。

   ```Shell
       mvn clean install 
   ```

![ インストールイメージの成功 ](/help/forms/assets/aem-modernize-install-steps.png)

インストールが完了すると、AEM Modernize Tools を使用できるようになります。

![AEM移行ユーティリティツールを有効にする ](/help/forms/assets/enable-aem-modernizer-tools.png)


### ローカルのAEM Forms環境に対してAEM Modernize Tools を有効にする{#enable-aem-modernize-Tools}

AEM環境でAEM Modernize Tools を有効にして使用するには、基盤コンポーネントをコアコンポーネントに移行するためのルールをマッピングすることが重要です。

1. オーサーインスタンスにログインします。
1. `http://[host]:[port]/system/console/configMgr` に移動します。
1. `AEM Modernize Tools - Component Rewrite Rule Service` を検索して編集します。
1. `/apps/forms-modernizer/rules` のように `Component Rule Paths` を追加します。
1. 「**保存**」をクリックして、変更を保存します。

![AEM Modernize コンポーネントルール ](/help/forms/assets/aem-modernize-tools-component-rule.png)

## フォーム変換ユーティリティを実行して、基盤コンポーネントベースのフォームをコアコンポーネントベースのフォームに変換します

1. **[!UICONTROL ツール/AEM Modernize Tools/Forms変換]** に移動します。

   ![AEM Modernize Tools を選択してください ](/help/forms/assets/aem-modernize-tools-select-form.png)

1. 「**[!UICONTROL Formsコンバージョン]**」オプションを選択します。

   ![ 「Forms変換」オプションを選択 ](/help/forms/assets/aem-modernize-forms-conversion.png)

1. **作成** をクリックして、新しいジョブを作成します。

   ![AEM Modernize Tools Create Job](/help/forms/assets/aem-modernize-tools-create-job.png)

1. **[!UICONTROL ジョブ名]** を指定します。
1. 「**[!UICONTROL フォーム]**」タブでは、次のいずれかのオプションを選択できます。

   * **なし**：フォームの変換を開始する前に基盤コンポーネントベースのフォームのコピーを作成しない場合は、このオプションを選択します。
   * **復元**：フォームをフォーム変換を開始する前の状態に復元するには、このオプションを選択します。
   * **ターゲットにコピー**：フォームの変換を開始する前に基盤コンポーネントベースのフォームのコピーを作成する場合は、このオプションを選択します。

   ここでは、「**ターゲットにコピー** オプションが選択されています。 「**ターゲットにコピー**」オプションが選択されている場合、「**[!UICONTROL Sourceのパス]**」および「**[!UICONTROL ターゲットパス]**」オプションが表示されます。

1. `source folder`1}Source Path} に ]**名」を入力します。**[!UICONTROL 
1. **[!UICONTROL ターゲットパス]** で `target folder` 名を指定します。
1. 「**[!UICONTROL 次へ]**」を選択します。
1. **[!UICONTROL Formsを追加]** をクリックします。 `source folder` 内のすべてのフォームが画面に表示されます。
1. 基盤コンポーネントに基づくアダプティブFormsを選択して、コアコンポーネントベースのフォームに変換します。 複数のフォームを選択することもできます。

   ![AEM Modernize Tools Select Form](/help/forms/assets/aem-modernize-tools-select-form.png)

1. **[!UICONTROL 選択]** をクリックします。
1. 「**[!UICONTROL ジョブをスケジュール]**」をクリックして、変換プロセスを開始します。
1. **[!UICONTROL ページを変換]** ダイアログボックスで **[!UICONTROL 変換]** をクリックします。

   ![AEM Modernize Tools Convert Pages](/help/forms/assets/aem-modernize-tools-convert-form.png)

   プロセスのステータスが `success` に変更された場合。 `target folder` に移動して、変換されたフォームを表示します。

   ![AEM Modernize Tools Success](/help/forms/assets/aem-modernize-tools-success.png)

1. アダプティブフォームを選択し、/ **[!UICONTROL プロパティ]** を選択します。 フォームプロパティページが開きます。

   ![AEM Modernize Tools の宛先フォルダー ](/help/forms/assets/aem-modernize-tools-destination-folder.png)

1. **[!UICONTROL 保存して閉じる]** を選択して、変換されたフォームのプロパティを再度保存します。
   ![AEM Modernize Tools アダプティブフォームのプロパティ ](/help/forms/assets/aem-modernize-tools-af-properties.png)

これで、基盤コンポーネント上に構築されたアダプティブフォームが、コアコンポーネント上に構築されたアダプティブフォームに変換されることを確認できます。

## ベストプラクティス {#best-practices}

* 基盤コンポーネントベースのフォームは、同等の [ コアコンポーネント ](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/introduction#available-components-a-breakdown-by-component-type) を使用できるコンポーネントのみを使用します。 同等のコアコンポーネントを持たない基盤コンポーネントを使用する場合、基盤コンポーネントは変換されません。 その結果、フォームのオーサリング中に正しく機能しません
* 基盤コンポーネントをコアコンポーネントに変換するルールは、XML 形式で指定してください。
