---
title: Forms Managerでのフォームのバージョン管理
description: Forms Manager UIで、アダプティブForms、フォームフラグメント、テーマ、その他のアセットのバージョンを作成および管理する方法について説明します。
feature: Adaptive Forms, Core Components, Foundation Components
role: User, Developer, Admin
badgeSaas: label="AEM Forms" type="Positive" tooltip="AEM Formsに適用）。"
exl-id: cd2c6e15-99a6-4b4e-bfd1-8291a2001ebe
source-git-commit: 08fe79147c81c0a5b319fef3ef7733b6053b399a
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 6%

---

# Forms Manager UIでのForm Assets バージョンの管理

Forms Managerで、フォームアセットのバージョン管理がサポートされるようになりました。 Forms Manager UIから、バージョンの作成、バージョン履歴の表示、以前のバージョンのアセットの復元を行うことができます。

## サポートされているアセットタイプ {#supported-asset-types}

次のアセットタイプのバージョンを作成および管理できます。

| アセットタイプ | 説明 |
|---|---|
| アダプティブ Forms（コアコンポーネント） | コアコンポーネントを使用して構築されたアダプティブForms |
| アダプティブ Forms（基盤コンポーネント） | 基盤コンポーネントを使用して構築されたアダプティブ Forms |
| フォームフラグメント | 複数のフォームで共有された再利用可能なフォームセクション |
| テーマ | アダプティブFormsに適用されるビジュアルスタイル定義 |
| XDP テンプレート | XFA ベースのフォームテンプレート |
| バイナリ資産 | Forms DAM リポジトリに保存されているその他のファイル |

## バージョンを作成します。 {#create-version-forms-manager}

フォームアセットのバージョンを作成するには：

1. **[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL Forms]**／**[!UICONTROL フォームとドキュメント]**&#x200B;に移動します。
1. フォームまたはアセットを選択します。
1. 左側のパネルで、**[!UICONTROL タイムライン]**&#x200B;を選択します。
1. タイムラインツールバーの「**[!UICONTROL バージョンとして保存]**」をクリックします。
   ![ バージョンとして保存](/help/forms/assets/create-version.png)
1. 変更を説明するには、**[!UICONTROL ラベル]**&#x200B;とオプションの&#x200B;**[!UICONTROL コメント]**&#x200B;を入力します。
1. 「**[!UICONTROL 作成]**」をクリックします。
   ![ バージョン 2](/help/forms/assets/create-version1.png)として保存

バージョンは、ラベル、コメント、タイムスタンプを含むタイムラインパネルに表示されます。

## アップロード時にアセットをバージョン化する {#version-on-upload}

既存のアセットと同じ名前のアセットをアップロードすると、Forms Managerは、更新するアセットを一覧表示する&#x200B;**ファイルアップロード** ダイアログを表示します。 ダイアログには、アセット名、セクション、パスが表示されます。

同じ名前のアセットが既に存在する場合、アップロードによって既存のアセットが置き換えられ、新しいバージョンが自動的に作成されます。 作成したバージョンはタイムラインで表示できます。

バージョン管理されたアップロードを示す![ ファイルアップロードダイアログ ](/help/forms/assets/version-upload.png)

## バージョン履歴を表示 {#view-version-history}

アセットのバージョン履歴を表示するには：

1. Forms Managerでアセットを選択します。
1. 左側のパネルで、**[!UICONTROL タイムライン]**を選択します。
   ![ バージョン履歴](/help/forms/assets/version-history.png)

タイムラインには、すべてのバージョンのエントリとアクティビティイベントが表示されます。 各エントリには、ラベル、コメント、作成者、タイムスタンプが表示されます。

## 以前のバージョンを復元 {#restore-version}

アセットを以前のバージョンに復元するには：

1. Forms Managerでアセットを選択します。
1. 左側のパネルで、**[!UICONTROL タイムライン]**&#x200B;を選択します。
1. 復元するバージョンを選択します。
1. 「**[!UICONTROL このバージョンに戻る]**」をクリックします。
   ![ バージョンを元に戻す](/help/forms/assets/revert-version.png)

>[!NOTE]
>
>画像を以前のバージョンに戻すことはできません。 アダプティブForms、フォームフラグメント、テーマ、XDP テンプレートなど、その他すべてのアセットタイプでバージョンの復元がサポートされます。

## 関連トピック {#see-also}

* [アダプティブフォームでのバージョン管理、レビュー、コメント](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md)
* [フォームと関連アセットの読み込みと書き出し](/help/forms/import-export-forms-templates.md)
* [フォームの公開と非公開](/help/forms/publishing-unpublishing-forms.md)
