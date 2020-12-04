---
title: メタデータの編集と追加
description: アセットのメタデータを編集する様々な方法（ [!DNL Experience Manager Assets] アセットのメタデータ）について説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 3207151a76c51637551907d15a34f1a6b7450d02
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 91%

---


# メタデータの編集と追加 {#how-to-edit-or-add-metadata}

メタデータは、検索可能なアセットに関する追加情報です。画像をアップロードすると自動的に抽出されます。既存のメタデータを編集したり、新しいメタデータプロパティを既存のフィールドに追加（例えば、メタデータフィールドが空白の場合など）したりすることができます。

会社には、制御された信頼性の高いメタデータの語彙が必要なので、[!DNL Experience Manager Assets]では、新しいメタデータプロパティをアドホックに追加できません。 作成者は、アセットの新しいメタデータフィールドを追加することはできませんが、開発者は追加できます。[アセットの新しいメタデータプロパティの作成](meta-edit.md#editing-metadata-schema)を参照してください。

## アセットのメタデータの編集 {#editing-metadata-for-an-asset}

メタデータを編集するには、次の手順に従います。

1. 次のいずれかの操作をおこないます。

   * Assets UI でアセットを選択し、ツールバーの「**[!UICONTROL プロパティを表示]**」アイコンをクリックまたはタップします。
   * アセットのサムネールから、「**[!UICONTROL プロパティを表示]**」クイックアクションを選択します。
   * アセットページから、ツールバーの「**[!UICONTROL プロパティを表示]**」をクリックまたはタップします。

   アセットページに、アセットのメタデータがすべて表示されます。このメタデータは、AEM Assets にアップロードされた（取り込まれた）ときに、自動的に抽出されたものです。

1. 様々なタブで必要に応じてメタデータを編集したら、ツールバーの「**[!UICONTROL 保存]**」をクリックまたはタップして、変更内容を保存します。「**[!UICONTROL 閉じる]**」をクリックまたはタップして、Assets Web インターフェイスに戻ります。

   >[!NOTE]
   >
   >テキストフィールドが空の場合、現在設定されているメタデータはありません。フィールドに値を入力して保存すると、そのメタデータプロパティを追加できます。

アセットのメタデータへの変更内容は、XMP データの一部として元のバイナリに書き戻されます。この操作は、AEM のメタデータ書き戻しワークフローで実行されます。既存のプロパティ（`dc:title` など）への変更は上書きされ、新しく作成されたプロパティ（`cq:tags` などのカスタムプロパティを含む）はスキーマとともに追加されます。

<!-- XMP write-back is supported and enabled for the platforms and file formats described in technical requirements. -->

## メタデータスキーマの編集 {#editing-metadata-schema}

メタデータスキーマの編集方法について詳しくは、[メタデータスキーマフォームの編集](metadata-schemas.md#edit-metadata-schema-forms)を参照してください。

## AEM 内でのカスタム名前空間の登録 {#registering-a-custom-namespace-within-aem}

AEM 内での独自の名前空間を追加できます。cq、jcr、sling など事前に定義された名前空間があるように、リポジトリメタデータと xml 処理用の名前空間を設定できます。

1. ノードタイプ管理ページ（*https://&lt;host>:&lt;port>/crx/explorer/nodetypes/index.jsp*）に移動します。
1. ページ上部の「**[!UICONTROL 名前空間]**」をクリックまたはタップします。ウィンドウに名前空間管理ページが表示されます。

1. 名前空間を追加するには、下部の「**[!UICONTROL 新規]**」をクリックまたはタップします。
1. XML 名前空間規則に従って、カスタム名前空間を指定（URI 形式の id と、その id に関連付けられているプレフィックスを指定）したら、「**[!UICONTROL 保存]**」をクリックまたはタップします。
