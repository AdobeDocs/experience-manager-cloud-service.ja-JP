---
title: AI で生成されたメタデータを使用してコンテンツの検出を強化
description: AI で生成されたメタデータを使用してコンテンツの検出を強化する方法を説明します
source-git-commit: f83324be68bdab65e5c76ef336eb7e4a2e318dd1
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 94%

---


# AI で生成されたメタデータを使用してコンテンツの検出を強化 {#ai-smart-tags}

AI は、手動の入力に依存するのではなく、デジタルアセットに説明的なタグを自動的に割り当てます。これらの AI で生成されたタグは、メタデータの品質を向上させ、アセットの検索、分類および推奨を容易にします。このアプローチでは、手動でのタグ付けが不要なために効率が向上するだけでなく、大量のデジタルコンテンツ間の一貫性とスケーラビリティも確保できます。例えば、アセットが画像の場合、AI はアセット内のオブジェクト、シーン、感情、さらにはブランドロゴを識別し、「夕日」、「ビーチ」、「休暇」、「笑顔」など、関連するタグを生成できます。 AI が生成するコンテンツは、セマンティック検索とレキシカル検索の両方の技術を活用することで、アセットの検索精度を向上させることができます。詳しくは、[Assets の検索](search-assets-view.md)を参照してください。<!--If the asset is a document, AI reads and interprets the text to assign meaningful keywords that summarize its content—such as "climate change," "policy," or "renewable energy.-->

![AI で生成されたメタデータ](/help/assets/assets/enhanced-smart-tags.png)

## AI で生成されたメタデータを有効にする方法 {#enable-ai-generated-metadata}

AI で生成されたメタデータを有効にするには：

* AEM のリリースバージョン `20626` 以上が必要です。


## AI で生成されたメタデータの使用 {#using-ai-generated-smart-tags}

<!--[!NOTE]
>
>The enhanced smart tags capability is available only for the newly uploaded assets.
-->

拡張スマートタグ機能を使用するには、次の手順を実行します。

1. [!DNL Experience Manager] インターフェイスで、目的のフォルダーに移動し、「**[!UICONTROL Assets を追加]**」をクリックします。<!--Alternatively, to update enhanced smart tags in an existing content, click **[!UICONTROL reprocess]**.-->互換性のある画像ファイル形式は、`png`、`jpg`、`jpeg`、`psd`、`tiff`、`gif`、`webp`、`crw`、`cr2`、`3fr`、`nef`、`arw` および `bmp` です。

1. 新しくアップロードされたアセットが処理されるまで待ちます。完了したら、アセットの詳細に移動します。

1. 「**[!UICONTROL AI 生成]**」タブに移動します。[!DNL Experience Manager] のバージョンが非対応または更新されていない場合、このタブは表示されません。次のフィールドがあります。

   * **[!UICONTROL 生成されたタイトル]：**&#x200B;このタイトルは、アップロードされたアセットの中核となるアイデアを捉えた明確で簡潔な見出しとなり、一目でわかりやすくなります。アセットを追加する際に、（`dc:title` で）タイトルを指定すると、アセットの参照ビューに表示されます。空白のままにすると、AIによって生成されたタイトルが自動的に割り当てられます。
   * **[!UICONTROL 生成された説明]：**&#x200B;説明には、アセットの内容に関する簡潔でわかりやすい概要が記載されており、ユーザーや検索モジュールがその関連性をすばやく把握できるようにします。
   * **[!UICONTROL 生成されたキーワード]：**&#x200B;キーワードは、アセットの主なテーマを表すターゲット用語で、タグ付けやコンテンツのフィルタリングに役立ちます。

1. [オプション]：関連するタグが欠落していると思われる場合は、追加のタグを追加するか、独自のタグを作成できます。これを行うには、「**[!UICONTROL 生成されたキーワード]**」フィールドにタグを入力し、「**[!UICONTROL 保存]**」をクリックします。

AI で生成されたメタデータを無効にする方法について詳しくは、[AI で生成されたメタデータを無効にする](/help/assets/smart-tags.md#disable-ai-generated-metadata)を参照してください。
