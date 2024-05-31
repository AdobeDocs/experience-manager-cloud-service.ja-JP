---
title: 基盤コンポーネントに基づくアダプティブFormsをコアコンポーネントベースのフォームに変換するための移行ユーティリティ
description: 移行ユーティリティをインストールして使用し、基盤コンポーネントに基づくアダプティブFormsをコアコンポーネントベースのフォームに変換する方法を説明します。
Keywords: Migration Utility tool, Convert Adaptive Forms based on foundation components to core component based forms, Convert Foundation forms to Core components forms, Using Modernizer tool to convert Foundation Components to Core components in forms.
role: User, Developer, Admin
features: core components
hide: true
hidefromtoc: true
source-git-commit: 494e90bd5822495f0619e8ebf55f373a26a3ffe6
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 6%

---


# はじめに

移行ユーティリティを使用して、基盤コンポーネントに基づくアダプティブFormsをコアコンポーネントベースのフォームに変換できます。 を使用できます [AEM Modernize ツール](https://opensource.adobe.com/aem-modernize-tools/) 移行ユーティリティツールとして使用します。 この [AEM Modernize ツール](https://opensource.adobe.com/aem-modernize-tools/) 基盤コンポーネントをベースとするアダプティブFormsを、サポートされている最新のコアコンポーネント機能に変換するためのユーティリティスイートを提供します。

## AEM Modernize Tools とは

[AEM Modernize ツール](https://opensource.adobe.com/aem-modernize-tools/) Adobe Experience Manager（AEM）プロジェクトの最新化または更新プロセスを容易にするために設計された一連のユーティリティまたはソフトウェアアプリケーションを指します。 これらのツールは、通常、AEM内の古いコンポーネントや機能を、より効率的でサポートされている新しい代替機能に変換する際に役立ちます。

AEM Modernize Tools は、古い基盤コンポーネントに基づくアダプティブFormsを、新しいコアコンポーネントベースのフォームに変換します。 この変換プロセスにより、フォームが最新の標準と機能に準拠するようになり、AEM環境のパフォーマンス、互換性、メンテナンスのしやすさが向上する可能性があります。

![AEM Modernize Tools](/help/forms/assets/aem-modernize-tools.png)

>[!NOTE]
> 
> ローカルのAEM設定にAEM Modernize Tools をインストールすることをお勧めします。 基盤ベースのフォームをコアコンポーネントベースのフォームに移行します。 フォームとそのアセットをダウンロードします。 次に、フォームとそのアセットを必要な環境にアップロードします。

## AEM Modernize Tools を使用するための前提条件

* [AEM Forms 用のローカル開発環境を設定](/help/forms/setup-local-development-environment.md)
* [お使いの環境でアダプティブ Forms コアコンポーネントを有効にします。](/help/forms/enable-adaptive-forms-core-components.md)

* にユーザーを追加 [!DNL forms-users] グループ。 [!DNL forms-users] グループのメンバーには、アダプティブフォームを作成する権限があります。

* 次の役割を持つユーザーは、AEM環境内にAEM Modernize Tools をインストールする権限を持っています。
   * 開発者の役割
   * 管理者の役割フォーム固有のユーザーグループの詳細なリストについては、次を参照してください。 [グループと権限](forms-groups-privileges-tasks.md).

## AEM Modernize Tools のインストールと設定

AEM Modernize Tools のインストールと設定の手順：

1. [ローカルのAEM Forms環境へのAEM Modernize Tools のインストール](#install-aem-modernize-tools)
2. [ローカルのAEM Forms環境に対してAEM Modernize Tools を有効にする](#enable-aem-modernize-tools)

### ローカルのAEM Forms環境へのAEM Modernize Tools のインストール {#install-aem-modernize-tools}

次の手順を実行して、ローカルのAEM Forms環境にAEM Modernize Tools をインストールします。

1. コマンドラインから次のコマンドを実行して、ローカル AEM オーサーサービスを開始します。

   `java -jar aem-author-p4502.jar`

   >[!NOTE]
   >
   > 管理者パスワードを `admin` として指定します。任意の管理者パスワードを使用できますが、ローカル開発にはデフォルトを使用して、再設定しなくてすむようにすることをお勧めします。

1. のクローン [AEM Modernize Tools](https://git.corp.adobe.com/livecycle/forms-modernizer/tree/convertForms) ローカルシステム内のリポジトリ。

   ```Shell
   git clone [Path of Git repository of AEM Modernize Tools]
   ```
   を [AEM Modernize Tools の Git リポジトリのパス] と、AEM Modernize Tools の対応する Git リポジトリの実際の URL を比較します。
コマンドを正常に実行すると、お使いのマシン上でAEM Modernize Tools リポジトリのローカルコピーが利用可能になります。

1. に移動します。`[AEM Modernize Tools Repository]`  ローカルシステム内。
1. 次のコマンドを実行します。

   ```Shell
       mvn clean install 
   ```
![インストールの成功イメージ](/help/forms/assets/aem-modernize-install-steps.png)

インストールが完了すると、AEM Modernize Tools を使用できるようになります。

![AEM Modernize Tools の有効化](/help/forms/assets/enable-aem-modernizer-tools.png)


### ローカルのAEM Forms環境に対してAEM Modernize Tools を有効にする{#enable-aem-modernize-tools}

AEM環境でAEM Modernize Tools を有効にして使用するには、基盤コンポーネントをコアコンポーネントに移行するためのルールをマッピングすることが重要です。

1. オーサーインスタンスにログインします。
1. `http://[host]:[port]/system/console/configMgr` に移動します。
1. を検索して編集します `AEM Modernize Tools - Component Rewrite Rule Service`.
1. を追加 `Component Rule Paths` as `/apps/forms-modernizer/rules`.
1. 「**保存**」をクリックして、変更を保存します。

![AEM Modernize コンポーネントルール](/help/forms/assets/aem-modernize-tools-component-rule.png)

## AEM Modernize Tools を実行して、基盤コンポーネントベースのフォームをコアコンポーネントベースのフォームに変換する

1. に移動 **[!UICONTROL ツール / AEM Modernize ツール / Forms変換]**.

   ![AEM Modernize Tools を選択します。](/help/forms/assets/aem-modernize-tools-select.png)

1. 「」を選択します **[!UICONTROL Forms変換]** オプション。

   ![「Forms変換」オプションを選択します](/help/forms/assets/aem-modernize-forms-conversion.png)

1. クリック **作成** 新規ジョブを作成します。

   ![AEM Modernize Tools ジョブを作成](/help/forms/assets/aem-modernize-tools-create-job.png)

1. を指定 **[!UICONTROL ジョブ名]**.
1. が含まれる **[!UICONTROL フォーム]** タブで、次のいずれかのオプションを選択できます。
   * **なし** ：フォームの処理が不要な場合は、このオプションを選択します。
   * **復元** ：最後の変換の前の状態にフォームを復元するには、このオプションを選択します。
   * **ターゲットにコピー**：変換を実行する前にフォームをコピーする場合は、このオプションを選択します。
ここでは、 **ターゲットにコピー** オプションが選択されています。 次の場合 **ターゲットにコピー** オプションを選択すると、 **[!UICONTROL ソースパス]** および **[!UICONTROL ターゲットパス]** オプションが表示されます。

1. を指定 `source folder` の名前 **[!UICONTROL ソースパス]**.
1. を指定 `target folder` の名前 **[!UICONTROL ターゲットパス]**.
1. 「**[!UICONTROL 次へ]**」を選択します。
1. クリックする **[!UICONTROL Formsを追加]**. 内のすべてのフォーム `source folder` 画面に表示されます。
1. 基盤コンポーネントに基づくフォームを選択し、コアコンポーネントに基づくフォームに変換します。 複数のフォームを選択することもできます。

   ![AEM Modernize Tools フォームを選択](/help/forms/assets/aem-modernize-tools-select-form.png)

1. クリック **[!UICONTROL を選択]**.
1. クリック **[!UICONTROL ジョブのスケジュール]** 変換処理を開始します。
1. クリック **[!UICONTROL 変換]** から **[!UICONTROL ページを変換]** ダイアログが表示されます。

   ![AEM Modernize Tools ページを変換](/help/forms/assets/aem-modernize-tools-convert-form.png)

   プロセスのステータスが「」に変更された場合 `success`. に移動します。 `target folder` 変換後のフォームを表示します。

   ![AEM Modernize Tools の成功](/help/forms/assets/aem-modernize-tools-success.png)

1. アダプティブフォームを選択し、/を選択します。 **[!UICONTROL プロパティ]**. フォームプロパティページが開きます。
   ![AEM Modernize Tools の宛先フォルダー](/help/forms/assets/aem-modernize-tools-destination-folder.png)

1. を選択 **[!UICONTROL 保存して閉じる]** 変換後のフォームのプロパティを再度保存します。
   ![AEM Modernize Tools アダプティブフォームのプロパティ](/help/forms/assets/aem-modernize-tools-af-properties.png)

これで、基盤コンポーネント上に構築されたアダプティブフォームが、コアコンポーネント上に構築されたアダプティブフォームに変換されることを確認できます。

## 移行ユーティリティ・ツール使用時の考慮事項 {#considerations}

* 基盤コンポーネント上で作成されたフォームにカスタム関数ルールが含まれている場合、コアコンポーネントに基づいて変換されたフォーム用にこれらのルールを書き換える必要があります。
* 変換されたフォームにはルールエディターのルールが含まれていないので、変換されたフォームのルールを書き換える必要があります。
* 変換されたフォームの翻訳ジョブを再作成する必要があります。

## ベストプラクティス {#best-practices}

* 基盤コンポーネント上に構築されたフォームには、コアコンポーネントベースのコンポーネントにあるコンポーネントのみが含まれます。
* ルールが XML 形式であることを確認します。


