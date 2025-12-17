---
title: 管理ビューでの AI 生成メタデータによるコンテンツ検出の強化
description: 管理ビューで AI 生成メタデータを使用してコンテンツの検出を強化する方法を説明します
feature: Smart Tags,Tagging
role: Admin,User
source-git-commit: 3f44e74488fc73c406fefb6decc41782859d029b
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 76%

---


# AI で生成されたメタデータによるコンテンツ検出の強化 {#ai-smart-tags}

| UI | 記事リンク |
| -------- | ---------------------------- |
| アセットビュー | [ここをクリックしてください](/help/assets/ai-generated-metadata-assets-view.md) |
| 管理ビュー | この記事 |

AI は、手動の入力に依存するのではなく、デジタルアセットに説明的なタグを自動的に割り当てます。これらの AI で生成されたタグは、メタデータの品質を向上させ、アセットの検索、分類および推奨を容易にします。このアプローチでは、手動でのタグ付けが不要なために効率が向上するだけでなく、大量のデジタルコンテンツ間の一貫性とスケーラビリティも確保できます。例えば、アセットが画像の場合、AI はアセット内のオブジェクト、シーン、感情、さらにはブランドロゴを識別し、「夕日」、「ビーチ」、「休暇」、「笑顔」など、関連するタグを生成できます。 AI が生成するコンテンツは、セマンティック検索とレキシカル検索の両方の技術を活用することで、アセットの検索精度を向上させることができます。詳しくは、[Assets の検索](search-assets.md)を参照してください。<!--If the asset is a document, AI reads and interprets the text to assign meaningful keywords that summarize its content—such as "climate change," "policy," or "renewable energy.-->

![拡張スマートタグ](assets/enhanced-smart-tags1.png)

## AI で生成されたメタデータを有効にする方法 {#enable-ai-generated-metadata}

AI で生成されたメタデータを有効にするには：

* AEM のリリースバージョン `20626` 以上が必要です。

## AI で生成されたタイトルの設定 {#configure-ai-generated-titles}

AEM では、アセットの参照ページのカード表示またはリスト表示でのアセットタイトルの表示を設定できます。自分で定義したアセットタイトル、AI を使用して生成されたタイトルを表示するか、アセットに既存のタイトルがない場合にのみ AI が生成されたタイトルを使用するかを選択できます。

AI で生成されたタイトルを設定するには：

1. **[!UICONTROL ツール/Assets/Assets設定/スマートタグ拡張機能の設定]** に移動します。

1. 次のいずれかのオプションを選択します。

   * **DC タイトルを表示（デフォルト）**：アセットプロパティで使用可能な「**[!UICONTROL タイトル]**」フィールドにタイトルを指定して、カード表示またはリスト表示で表示します。アセットタイトルが定義されていない場合、AEM Assets にはファイル名が表示されます。

   * **AI で生成されたタイトルを表示**：AI で生成されたタイトルを表示し、アセットプロパティで指定したタイトルを無視します。AI で生成されたタイトルがアセットに使用できない場合、AEM Assets にはそのプロパティで使用できるデフォルトのアセットタイトルが表示されます。

   * **DC タイトルが存在しない場合にのみ AI で生成されたタイトルを表示**：AEM Assets には、アセットにアセットタイトルが定義されていない場合にのみ AI で生成されたタイトルが表示されます。

     ![AI で生成されたタイトルの設定](assets/configure-title-ai-generated.png)

## AI で生成されたメタデータの使用 {#using-ai-generated-smart-tags}

<!--[!NOTE]
>
>The enhanced smart tags capability is available only for the newly uploaded assets.
-->

拡張スマートタグ機能を使用するには、次の手順を実行します。

1. [!DNL Experience Manager] インターフェイスで、目的のフォルダーに移動し、「**[!UICONTROL Assets を追加]**」をクリックします。<!--Alternatively, to update enhanced smart tags in an existing content, click **[!UICONTROL reprocess]**.-->互換性のある画像ファイル形式は、`png`、`jpg`、`jpeg`、`psd`、`tiff`、`gif`、`webp`、`crw`、`cr2`、`3fr`、`nef`、`arw` および `bmp` です。

1. 新しくアップロードされたアセットが処理されるまで待ちます。完了したら、「アセットプロパティ」に移動します。

1. **[!UICONTROL AI 生成]**&#x200B;タブに移動します。[!DNL Experience Manager] バージョンに互換性がないか更新されていない場合、このタブは表示されません。次のフィールドがあります。

   * **[!UICONTROL 生成されたタイトル]：**&#x200B;このタイトルは、アップロードされたアセットの中核となるアイデアを捉えた明確で簡潔な見出しとなり、一目でわかりやすくなります。アセットを追加する際に、（`dc:title` で）タイトルを指定すると、アセットの参照ビューに表示されます。空白のままにすると、AIによって生成されたタイトルが自動的に割り当てられます。
   * **[!UICONTROL 生成された説明]：**&#x200B;説明には、アセットの内容に関する簡潔でわかりやすい概要が記載されており、ユーザーや検索モジュールがその関連性をすばやく把握できるようにします。
   * **[!UICONTROL 生成されたキーワード]：**&#x200B;キーワードは、アセットの主なテーマを表すターゲット用語で、タグ付けやコンテンツのフィルタリングに役立ちます。

1. [オプション]：関連するタグが欠落していると思われる場合は、追加のタグを追加するか、独自のタグを作成できます。これを行うには、「**[!UICONTROL 生成されたキーワード]**」フィールドにタグを入力し、「**[!UICONTROL 保存]**」をクリックします。

## AI で生成されたメタデータを無効にする {#disable-ai-generated-metadata}

AI で生成されたメタデータをAEM as a Cloud Service環境に対して無効にするか、フォルダーレベルで無効にすることができます。

AEM as a Cloud Service環境で AI 生成メタデータを無効にするには：

1. **[!UICONTROL ツール/Assets/Assets設定/スマートタグ拡張機能の設定]** に移動します。

1. 「**[!UICONTROL スマートタグ拡張機能を無効にする]**」を選択します。

1. **[!UICONTROL 保存]** をクリックします。

AI で生成されたメタデータは、AEM Assetsにアップロードする新しいアセットやフォルダーでは無効になります。 AI によって生成されたメタデータフィールドを持つ既存のアセットまたはフォルダーには、引き続きこれらのフィールドが表示されます。

### フォルダーの AI 生成メタデータを無効にする {#disable-ai-generated-metadata-folder-level}

AI で生成されたメタデータをフォルダーレベルで無効にするには：

1. フォルダーを選択し、「**[!UICONTROL プロパティ]**」をクリックします。

1. 「**[!UICONTROL アセット処理]**」タブを選択します。

1. 「**[!UICONTROL 画像のスマートタグ機能の強化]**」セクションで、ドロップダウンメニューから **[!UICONTROL 無効]** を選択します。

1. **[!UICONTROL 保存して閉じる]** をクリックして、選択したフォルダーの AI 生成メタデータを無効にします。