---
title: ユニバーサルエディターでフォームのフォームデータモデル（FDM）を統合する方法
description: フォームデータモデル（FDM）に基づいてエッジ配信サービス用のフォームを作成する方法を説明します。 FDM でデータモデルオブジェクトのサンプルデータを生成し、編集します。
feature: Edge Delivery Services, Form Data Model
role: Admin, User
exl-id: 9ce51223-57d0-47d8-8868-84b37d4e8e3e
source-git-commit: cfff846e594b39aa38ffbd3ef80cce1a72749245
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 32%

---


# Formsとフォームデータモデル（FDM）の統合

FDM を使用してフォームをバックエンドのデータソースに接続し、データのバインド、検証、送信のワークフローを有効にします。

## 前提条件

FDM をフォームに統合する前に、次の手順を実行します。

1. **[Data Sourceの設定](/help/forms/configure-data-sources.md)**：バックエンド接続を設定する
2. **[フォームデータモデルの作成](/help/forms/create-form-data-models.md)**：データ構造とサービスを定義する
3. **[データモデルオブジェクトの設定](/help/forms/work-with-form-data-model.md)**：データ関係のマッピング

## 考慮事項

ユニバーサルエディターインターフェイスの「**データソース**」アイコンや、右側のプロパティパネルの&#x200B;**連結参照**&#x200B;プロパティが表示されない場合は、**Extension Manager** で&#x200B;**データソース**&#x200B;拡張機能を有効にします。

![フォーム統合に有効にできるデータソース拡張機能など、使用できる拡張機能を示すユニバーサルエディター Extension Manager インターフェイスのスクリーンショット](/help/edge/docs/forms/universal-editor/assets/extension-manager.png)

ユニバーサルエディターで拡張機能を有効または無効にする方法については、](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)Extension Manager 機能のハイライト[の記事を参照してください。

## フォームタイプを選択

ユニバーサルエディターは、次の 2 つのフォーム作成アプローチをサポートします。

| 項目 | スキーマベースのフォーム | スキーマベース以外のフォーム |
|--------|-------------------|----------------------|
| **セットアップの複雑さ** | シンプル（自動バインディング） | 手動（フィールド単位のバインディング） |
| **ユースケース** | データ構造が定義された新しいフォーム | 既存のフォームまたは柔軟な要件 |
| **データソース** | 作成時に必須 | 後で追加できます |
| **バインディング** | 自動フィールドバインディング | フィールドごとの手動バインディング |

![ユニバーサルエディターのフォームのタイプ](/help/edge/docs/forms/universal-editor/assets/form-types.png){width="50%" align="center" height="50%"}

## スキーマベースのフォーム

スキーマベースのフォームでは、データソースを自動的に設定し、フォームフィールドをデータにバインドします。 このアプローチは、明確に定義されたデータ構造を持つ新しいフォームに最適です。

### スキーマベースのフォームの作成

1. **Forms コンソールへのアクセス**
   - [!DNL Experience Manager Forms] オーサーインスタンスにログインします。
   - **[!UICONTROL Adobe Experience Manager]** / **[!UICONTROL Forms]** / **[!UICONTROL Formsとドキュメント]** に移動します

2. **フォームの作成を開始**
   - **[!UICONTROL 作成]**/**[!UICONTROL アダプティブForms]** を選択します。
   - Edge Delivery Services テンプレートを選択
   - 有効な場合は「**[!UICONTROL 作成]**」をクリックします

   ![Edge Delivery Services テンプレート](/help/edge/assets/create-eds-forms.png)

3. **データモデルの設定**
   - **データ** タブに移動します
   - 複数のデータソースの場合は **フォームデータモデル（FDM）** 単一のバックエンドシステムの場合は **JSON スキーマ** を選択します
   - 作成した FDM （ペットのフォームデータモデルなど）を選択する

   ![フォームデータモデルを選択](/help/edge/docs/forms/universal-editor/assets/select-petstore-form-data-model.png)

4. **フォーム設定の完了**
   - **名前** と **タイトル** を入力
   - **GitHub URL** を指定します（例：`https://github.com/wkndforms/edsforms`）
   - 「**[!UICONTROL 作成]**」をクリックします

   ![スキーマベースのフォームを作成](/help/edge/docs/forms/universal-editor/assets/create-schema-based-form.png)

### スキーマベースのフォームの検証

フォームがユニバーサルエディターで開き、事前設定済みのデータバインディングが表示されます。

![事前入力されたフォームフィールドを持つスキーマベースのフォームと、使用可能なデータソース要素を表示するコンテンツブラウザーを示すユニバーサルエディターのスクリーンショット](/help/edge/docs/forms/universal-editor/assets/schema-based-form-in-ue.png)

![自動データ連結](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding.png)

## スキーマベース以外のフォーム

非スキーマフォームの場合は、手動でのデータソース設定とフィールドバインディングが必要です。 このアプローチは、既存のフォームや複雑な要件に対して柔軟性を提供します。

### スキーマベース以外のフォームの作成

1. **フォームプロパティへのアクセス**
   - [!DNL Experience Manager Forms] オーサーインスタンスにログインします。
   - **[!UICONTROL Adobe Experience Manager]** / **[!UICONTROL Forms]** / **[!UICONTROL Formsとドキュメント]** に移動します
   - フォームを選択し、「**[!UICONTROL プロパティ]**」をクリックします

   ![フォームのプロパティを開く](/help/edge/docs/forms/universal-editor/assets/non-schema-based-edit-properties.png)

2. **フォームモデルの設定**
   - 「**フォームモデル**」タブを開きます。
   - **選択元** ドロップダウンから **フォームデータモデル（FDM）** を選択します
   - リストから FDM を選択します

   ![「フォームモデル」タブを選択](/help/edge/docs/forms/universal-editor/assets/select-form-model.png)

   ![FDM の選択](/help/edge/docs/forms/universal-editor/assets/select-fdm.png)

3. **設定の確認**
   - 警告ダイアログで **OK** をクリックします
   - 「**[!UICONTROL 保存して閉じる]**」をクリックします。

   ![フォームモデルウィザード](/help/edge/docs/forms/universal-editor/assets/form-model-wizard.png)

### データ要素の追加

1. **フォームを編集用に開く**
   - フォームがユニバーサルエディターで開きます

   ![スキーマベース以外のフォームオーサリング](/help/edge/docs/forms/universal-editor/assets/non-schema-form-authoring.png)

2. **Data Source要素へのアクセス**
   - **[!UICONTROL コンテンツブラウザー]** の「**[!UICONTROL データソース]**」タブに移動します。
   - FDM から使用可能なデータ要素を表示する

   ![フォームデータソース](/help/edge/docs/forms/universal-editor/assets/non-schema-data-source.png)

3. **フォームへの要素の追加**
   - データ要素を選択し、「**[!UICONTROL 追加]**」をクリックします
   - または、要素をドラッグ&amp;ドロップしてフォームを作成します

   ![データ要素の追加](/help/edge/docs/forms/universal-editor/assets/non-schema-add-data-element.png)

   ![「データソース」タブからフォーム構造にデータ要素をドラッグ＆ドロップしてスキーマ以外のフォームを作成しているユニバーサルエディターを示すスクリーンショット](/help/edge/docs/forms/universal-editor/assets/non-schema-form.png)

### 手動データバインディングを追加

既存のフォームフィールドの場合は、**連結参照** プロパティを使用してデータ連結を追加します。

1. **フィールドのプロパティを開く**
   - 連結するフォームフィールドを選択
   - プロパティパネルを開きます。

2. **バインド参照の設定**
   - **バインド参照** プロパティに移動します
   - **参照** アイコンをクリックします

   ![フォームフィールドのデータ連結を手動で追加](/help/edge/docs/forms/universal-editor/assets/non-schema-add-data-binding.png)

3. **データ要素の選択**
   - **バインド参照の選択** ウィザードのデータソースツリーからを選択します
   - 目的のデータ要素を選択し、「**選択**」をクリックします

   ![データ連結参照を選択](/help/edge/docs/forms/universal-editor/assets/select-bind-reference.png)

   ![データ要素を選択](/help/edge/docs/forms/universal-editor/assets/select-data-element.png)

4. **バインディングの検証**
   - これで、フォームフィールドがデータ要素にバインドされます
   - 連結が「連結参照 **プロパティーに表示され** す

   ![自動データ連結](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding.png)

## 統合の検証

統合が完了したら、次の手順を実行します。

1. **データ連結をテスト**：フォームフィールドに正しいデータが表示されることを確認します
2. **送信を検証**：設定されたソースへのデータ保存を確認する
3. **エラー処理を確認**：無効なデータシナリオを使用したテスト

## 次の手順

[ 送信アクション ](/help/edge/docs/forms/universal-editor/submit-action.md) を設定して、フォームワークフローを完了します。
