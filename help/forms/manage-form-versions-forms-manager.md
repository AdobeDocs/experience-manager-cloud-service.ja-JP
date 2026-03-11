---
title: Forms Manager でフォームのバージョンを管理する
description: Forms Manager UI で、アダプティブForms、フォームフラグメント、テーマ、その他のアセットのバージョンを作成および管理する方法について説明します。
feature: Adaptive Forms, Core Components, Foundation Components
role: User, Developer, Admin
badgeSaas: label="AEM Forms" type="Positive" tooltip="AEM Formsに適用）。"
exl-id: cd2c6e15-99a6-4b4e-bfd1-8291a2001ebe
source-git-commit: 89b0f2a8ca9d2f60365a5c3962b0b4e826f79b3e
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 7%

---

# Forms Manager UI での Form Assets バージョンの管理

<span class="preview"> この機能は、早期アクセスプログラムを通じて利用できます。 アクセスを要求するには、公式アドレスから [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) にメールを送信してください。</span>

Forms Manager で、フォームアセットのバージョン管理がサポートされるようになりました。 Forms Manager UI を使用して、バージョンの作成、バージョン履歴の表示、以前のバージョンのアセットの復元を行うことができます。

## サポートされているアセットタイプ {#supported-asset-types}

次のアセットタイプのバージョンを作成および管理できます。

| アセットタイプ | 説明 |
|---|---|
| アダプティブForms（コアコンポーネント） | コアコンポーネントを使用して作成されたアダプティブForms |
| アダプティブForms（基盤コンポーネント） | 基盤コンポーネントを使用して構築されたアダプティブForms |
| フォームフラグメント | 複数のフォームで共有される再利用可能なフォームセクション |
| テーマ | アダプティブFormsに適用される表示スタイルの定義 |
| XDP テンプレート | XFA ベースのフォームテンプレート |
| バイナリアセット | フォーム DAM リポジトリに格納されているその他のファイル |

## バージョンを作成 {#create-version-forms-manager}

フォームアセットのバージョンを作成するには：

1. **[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL Forms]**／**[!UICONTROL フォームとドキュメント]**&#x200B;に移動します。
1. フォームまたはアセットを選択します。
1. 左側のパネルで「**[!UICONTROL タイムライン]**」を選択します。
1. タイムラインツールバーの **[!UICONTROL バージョンとして保存]** をクリックします。
   ![ バージョンとして保存 ](/help/forms/assets/create-version.png)
1. 変更を説明する **[!UICONTROL ラベル]** とオプションの **[!UICONTROL コメント]** を入力します。
1. 「**[!UICONTROL 作成]**」をクリックします。
   ![ バージョン 2 として保存 ](/help/forms/assets/create-version1.png)

タイムラインパネルに、バージョンが、ラベル、コメント、タイムスタンプと共に表示されます。

## アップロード中のアセットのバージョン設定 {#version-on-upload}

既存のアセットと同じ名前のアセットをアップロードすると、Forms Manager で **ファイルアップロード** ダイアログが表示され、更新するアセットが一覧表示されます。 ダイアログには、アセット名、セクション、パスが表示されます。

同じ名前のアセットが既に存在する場合は、既存のアセットがアップロードに置き換えられ、新しいバージョンが自動的に作成されます。 作成したバージョンはタイムラインで表示できます。

![ バージョン付きアップロードを示すファイルアップロードダイアログ ](/help/forms/assets/version-upload.png)

## バージョン履歴の表示 {#view-version-history}

アセットのバージョン履歴を表示するには：

1. Forms Manager でアセットを選択します。
1. 左側のパネルで「**[!UICONTROL タイムライン]**」を選択します。
   ![ バージョン履歴 ](/help/forms/assets/version-history.png)

タイムラインには、すべてのバージョンエントリとアクティビティイベントが表示されます。 各エントリには、ラベル、コメント、作成者およびタイムスタンプが表示されます。

## 以前のバージョンを復元 {#restore-version}

以前のバージョンにアセットを復元するには：

1. Forms Manager でアセットを選択します。
1. 左側のパネルで「**[!UICONTROL タイムライン]**」を選択します。
1. 復元するバージョンを選択します。
1. 「**[!UICONTROL このバージョンに戻る]**」をクリックします。
   ![ バージョンを復帰 ](/help/forms/assets/revert-version.png)

>[!NOTE]
>
>画像を以前のバージョンに戻すことはできません。 アダプティブForms、フォームフラグメント、テーマ、XDP テンプレートなど、他のすべてのアセットタイプでは、バージョンの復元がサポートされています。

## 関連トピック {#see-also}

* [アダプティブフォームのバージョン管理、レビュー、コメント](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md)
* [フォームおよび関連アセットの読み込みと書き出し](/help/forms/import-export-forms-templates.md)
* [フォームの公開と非公開](/help/forms/publishing-unpublishing-forms.md)
