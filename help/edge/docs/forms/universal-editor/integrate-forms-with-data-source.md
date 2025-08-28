---
title: ユニバーサルエディターでフォームのフォームデータモデル（FDM）を統合する方法
description: フォームデータモデル（FDM）に基づいた Edge Delivery Services 用のフォームの作成方法について説明します。FDM でデータモデルオブジェクトのサンプルデータを生成し、編集します。
feature: Edge Delivery Services, Form Data Model
role: Admin, User
exl-id: 9ce51223-57d0-47d8-8868-84b37d4e8e3e
source-git-commit: cfff846e594b39aa38ffbd3ef80cce1a72749245
workflow-type: ht
source-wordcount: '716'
ht-degree: 100%

---


# フォームとフォームデータモデル（FDM）の統合

FDM を使用してフォームをバックエンドデータソースに接続し、データ連結、検証、送信のワークフローを有効にします。

## 前提条件

FDM をフォームに統合する前に、次の手順を完了します。

1. **[データソースを設定](/help/forms/configure-data-sources.md)**：バックエンド接続を設定します
2. **[フォームデータモデルを作成](/help/forms/create-form-data-models.md)**：データ構造とサービスを定義します
3. **[データモデルオブジェクトを設定](/help/forms/work-with-form-data-model.md)**：データ関係をマッピングします

## 考慮事項

ユニバーサルエディターインターフェイスの「**データソース**」アイコンや、右側のプロパティパネルの&#x200B;**連結参照**&#x200B;プロパティが表示されない場合は、**Extension Manager** で&#x200B;**データソース**&#x200B;拡張機能を有効にします。

![フォーム統合に有効にできるデータソース拡張機能など、使用できる拡張機能を示すユニバーサルエディター Extension Manager インターフェイスのスクリーンショット](/help/edge/docs/forms/universal-editor/assets/extension-manager.png)

ユニバーサルエディターで拡張機能を有効または無効にする方法については、[Extension Manager 機能のハイライト](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)の記事を参照してください。

## フォームタイプの選択

ユニバーサルエディターは、次の 2 つのフォーム作成アプローチをサポートします。

| 項目 | スキーマベースのフォーム | スキーマベース以外のフォーム |
|--------|-------------------|----------------------|
| **設定の複雑さ** | シンプル（自動連結） | 手動（フィールド単位の連結） |
| **ユースケース** | データ構造が定義された新しいフォーム | 既存のフォームまたは柔軟な要件 |
| **データソース** | 作成時に必須 | 後で追加可能 |
| **連結** | 自動フィールド連結 | フィールドごとの手動連結 |

![ユニバーサルエディターのフォームのタイプ](/help/edge/docs/forms/universal-editor/assets/form-types.png){width="50%" align="center" height="50%"}

## スキーマベースのフォーム

スキーマベースのフォームでは、データソースを自動的に設定し、フォームフィールドをデータに連結します。このアプローチは、データ構造が明確に定義された新しいフォームに最適です。

### スキーマベースのフォームの作成

1. **フォームコンソールにアクセス**
   - [!DNL Experience Manager Forms] オーサーインスタンスにログインします
   - **[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL Forms]**／**[!UICONTROL フォームとドキュメント]**&#x200B;に移動します

2. **フォーム作成を開始**
   - **[!UICONTROL 作成]**／**[!UICONTROL アダプティブフォーム]**&#x200B;を選択します
   - Edge Delivery Services テンプレートを選択します
   - 有効な場合は、「**[!UICONTROL 作成]**」をクリックします

   ![Edge Delivery Services テンプレート](/help/edge/assets/create-eds-forms.png)

3. **データモデルを設定**
   - 「**データ**」タブに移動します
   - 複数のデータソースの場合は「**フォームデータモデル（FDM）**」を選択し、単一のバックエンドシステムの場合は「**JSON スキーマ**」を選択します
   - 作成した FDM（例：ペットのフォームデータモデル）を選択します

   ![フォームデータモデルを選択](/help/edge/docs/forms/universal-editor/assets/select-petstore-form-data-model.png)

4. **フォーム設定を完了**
   - **名前**&#x200B;と&#x200B;**タイトル**&#x200B;を入力します
   - **GitHub URL** を指定します（例：`https://github.com/wkndforms/edsforms`）
   - 「**[!UICONTROL 作成]**」をクリックします。

   ![スキーマベースのフォームを作成](/help/edge/docs/forms/universal-editor/assets/create-schema-based-form.png)

### スキーマベースのフォームの検証

フォームは、事前設定済みのデータ連結を使用してユニバーサルエディターで開きます。

![事前入力されたフォームフィールドを持つスキーマベースのフォームと、使用可能なデータソース要素を表示するコンテンツブラウザーを示すユニバーサルエディターのスクリーンショット](/help/edge/docs/forms/universal-editor/assets/schema-based-form-in-ue.png)

![自動データ連結](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding.png)

## スキーマベース以外のフォーム

スキーマ以外のフォームでは、データソース設定とフィールド連結を手動で行う必要があります。 このアプローチは、既存のフォームや複雑な要件に対して柔軟性を提供します。

### スキーマベース以外のフォームの作成

1. **フォームプロパティにアクセス**
   - [!DNL Experience Manager Forms] オーサーインスタンスにログインします
   - **[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL Forms]**／**[!UICONTROL フォームとドキュメント]**&#x200B;に移動します
   - フォームを選択し、「**[!UICONTROL プロパティ]**」をクリックします

   ![フォームのプロパティを開く](/help/edge/docs/forms/universal-editor/assets/non-schema-based-edit-properties.png)

2. **フォームモデルを設定**
   - 「**フォームモデル**」タブを開きます
   - **選択元**&#x200B;ドロップダウンから「**フォームデータモデル（FDM）**」を選択します
   - リストから FDM を選択します

   ![「フォームモデル」タブを選択](/help/edge/docs/forms/universal-editor/assets/select-form-model.png)

   ![FDM を選択](/help/edge/docs/forms/universal-editor/assets/select-fdm.png)

3. **設定を確認**
   - 警告ダイアログで「**OK**」をクリックします
   - 「**[!UICONTROL 保存して閉じる]**」をクリックします。

   ![フォームモデルウィザード](/help/edge/docs/forms/universal-editor/assets/form-model-wizard.png)

### データ要素の追加

1. **フォームを編集用に開く**
   - ユニバーサルエディターでフォームが開きます

   ![スキーマベース以外のフォームオーサリング](/help/edge/docs/forms/universal-editor/assets/non-schema-form-authoring.png)

2. **データソース要素にアクセス**
   - **[!UICONTROL コンテンツブラウザー]**&#x200B;の「**[!UICONTROL データソース]**」タブに移動します
   - FDM から使用可能なデータ要素を表示します

   ![フォームデータソース](/help/edge/docs/forms/universal-editor/assets/non-schema-data-source.png)

3. **フォームに要素を追加**
   - データ要素を選択し、「**[!UICONTROL 追加]**」をクリックします
   - または、要素をドラッグ＆ドロップしてフォームを作成します

   ![データ要素の追加](/help/edge/docs/forms/universal-editor/assets/non-schema-add-data-element.png)

   ![「データソース」タブからフォーム構造にデータ要素をドラッグ＆ドロップしてスキーマ以外のフォームを作成しているユニバーサルエディターを示すスクリーンショット](/help/edge/docs/forms/universal-editor/assets/non-schema-form.png)

### 手動データ連結の追加

既存のフォームフィールドの場合は、**バインド参照**&#x200B;プロパティを使用してデータ連結を追加します。

1. **フィールドのプロパティを開く**
   - 連結用のフォームフィールドを選択します
   - プロパティパネルを開きます

2. **連結参照を設定**
   - **連結参照**&#x200B;プロパティに移動します
   - **参照**&#x200B;アイコンをクリックします

   ![フォームフィールドのデータ連結を手動で追加](/help/edge/docs/forms/universal-editor/assets/non-schema-add-data-binding.png)

3. **データ要素を選択**
   - **連結参照を選択**&#x200B;ウィザードでデータソースツリーから選択します
   - 目的のデータ要素を選択し、「**選択**」をクリックします

   ![データ連結参照を選択](/help/edge/docs/forms/universal-editor/assets/select-bind-reference.png)

   ![データ要素を選択](/help/edge/docs/forms/universal-editor/assets/select-data-element.png)

4. **連結を検証**
   - これで、フォームフィールドがデータ要素に連結されます
   - 連結が&#x200B;**連結参照**&#x200B;プロパティに表示されます

   ![自動データ連結](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding.png)

## 統合の検証

統合が完了したら、次の手順を実行します。

1. **データ連結をテスト**：フォームフィールドに正しいデータが表示されていることを検証します
2. **送信を検証**：データが設定されたソースに保存されていることを確認します
3. **エラー処理を確認**：無効なデータシナリオでテストします

## 次の手順

[送信アクション](/help/edge/docs/forms/universal-editor/submit-action.md)を設定して、フォームワークフローを完了します。
