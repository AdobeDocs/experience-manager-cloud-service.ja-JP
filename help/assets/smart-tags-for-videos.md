---
title: ビデオアセットのスマートタグ
description: Adobe Experience Manager では、 [!DNL Adobe Sensei] を使用して、状況に応じた説明的なスマートタグをビデオに自動的に追加します。
feature: Smart Tags,Tagging
role: Admin,User
exl-id: 87d0eea2-83a1-4cfa-a4a5-425d0e8abba6
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 100%

---

# ビデオアセットのスマートタグ {#video-smart-tags}

新しいコンテンツに対するニーズが高まる中で、人手による作業を減らしつつ、人を惹きつけるデジタルエクスペリエンスをすぐに届ける必要があります。[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] では、人工知能を使用したビデオアセットの自動タグ付けをサポートしています。ビデオの手動のタグ付けには時間がかかる場合があります。しかし、[!DNL Adobe Sensei] を活用したビデオスマートタグ付け機能では、人工知能モデルを使用してビデオコンテンツを分析し、ビデオアセットにタグを追加します。DAM ユーザーが顧客に豊富なエクスペリエンスを提供するまでの時間を短縮できます。Adobe の機械学習サービスは、ビデオに対して 2 組のタグを生成します。1 組は、そのビデオ内のオブジェクト、シーンおよび属性に対応し、もう 1 組は、飲む、走る、ジョギングするなどのアクションに対応します。

ビデオタグ付けは、[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] ではデフォルトで有効になっています。ただし、フォルダーの[ビデオのスマートタグをオプトアウト](#opt-out-video-smart-tagging)できます。新しいビデオをアップロードする場合や、既存のビデオを再処理する場合、ビデオは自動的にタグ付けされます。また、[!DNL Experience Manager] では、ビデオファイルのサムネールを作成し、メタデータを抽出します。スマートタグは、アセット[プロパティ](#confidence-score-video-tag)内で[!UICONTROL 信頼性スコア]の降順で表示されます。

## アップロードのビデオのスマートタグ {#smart-tag-assets-on-ingestion}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] に[ビデオアセットをアップロード](add-assets.md#upload-assets)すると、ビデオが処理されます。処理が完了したら、アセット[!UICONTROL プロパティ]ページの「[!UICONTROL 基本]」タブを参照してください。スマートタグは、ビデオの[!UICONTROL スマートタグ]に自動的に追加されます。アセットマイクロサービスは、[!DNL Adobe Sensei] を利用してこれらのスマートタグを作成します。

![スマートタグはビデオに追加され、アセットプロパティの「基本」タブに表示されます](assets/smart-tags-added-to-videos.png)

適用されたスマートタグは、[信頼性スコア](#confidence-score-video-tag)の降順で並べ替えられ、[!UICONTROL スマートタグ]内で、オブジェクトタグとアクションタグを組み合わせて表示されます。

>[!IMPORTANT]
>
>自動生成されたタグが、ブランドとその内容に適合するかどうか確認してください。

## DAM 内の既存のビデオのスマートタグ {#smart-tag-existing-videos}

DAM 内の既存のビデオアセットに対しては、スマートタグが自動的には付けられません。手動で[!UICONTROL アセットを再処理]して、スマートタグを生成する必要があります。

アセットリポジトリーに既に存在するビデオアセット、またはアセットのフォルダー（サブフォルダーも含む）にスマートタグを付けるには、次の手順に従います。

1. [!DNL Adobe Experience Manager] ロゴを選択し、[!UICONTROL ナビゲーション]ページからアセットを選択します。

1. 「[!UICONTROL ファイル]」をクリックまたはタップして、Assets のインターフェイスを表示します。

1. スマートタグを適用するフォルダーに移動します。

1. フォルダー全体または特定のビデオアセットを選択します。

1. [!UICONTROL アセットの再処理]アイコン![アセットの再処理アイコン](assets/do-not-localize/reprocess-assets-icon.png)を選択し、「[!UICONTROL 完全なプロセス]」オプションを選択します。

<!-- TBD: Limit size -->

![アセットの再処理を行い、DAM リポジトリー既存のするビデオにタグを追加する](assets/reprocess.gif)

プロセスが完了したら、フォルダー内の任意のビデオアセットの[!UICONTROL プロパティ]ページに移動します。自動的に追加されたタグは、「[!UICONTROL 基本]」タブの[!UICONTROL スマートタグ]セクションに表示されます。適用されたこれらのスマートタグは、[信頼性スコア](#confidence-score-video-tag)の降順で並べ替えられます。

## タグ付きビデオの検索 {#search-smart-tagged-videos}

自動生成されたスマートタグに基づいてビデオアセットを検索するには、[オムニサーチ](search-assets.md#search-assets-in-aem)を使用します。

1. 検索アイコン![検索アイコン](assets/do-not-localize/search_icon.png)を選択して、「オムニサーチ」フィールドを表示します。

1. ビデオに明示的に追加していないタグを「オムニサーチ」フィールドに指定します。

1. タグに基づいて検索します。

検索結果には、指定したタグに基づいてビデオアセットが表示されます。

検索結果は、メタデータ内の検索されたキーワードを含むビデオアセットと、検索されたキーワードでスマートタグ付けされたビデオアセットを組み合わせたものです。ただし、メタデータフィールド内のすべての検索語に一致する検索結果が最初に表示され、スマートタグ内の検索語のいずれかに一致する検索結果はその後に表示されます。詳しくは、「[スマートタグを使用した [!DNL Experience Manager] 検索結果について](smart-tags.md#understand-search)」を参照してください。

## ビデオスマートタグのモデレート {#moderate-video-smart-tags}

[!DNL Adobe Experience Manager] では、スマートタグをキュレーションして次の操作を行うことができます。

* ブランドビデオに割り当てられている不正確なタグを削除します。

* タグベースでビデオを検索する場合は、最も関連性の高いタグの検索結果にビデオが表示されるように調整します。したがって、関連のないビデオが検索結果に表示される可能性を排除します。

* タグに高いランクを割り当てて、ビデオに対する関連性を高めます。ビデオのタグのランクを高くすることで、タグに基づいて検索が実行されたときに、そのビデオが検索結果に表示される可能性が高くなります。

アセットのスマートタグをモデレートする方法について詳しくは、「[スマートタグの管理](smart-tags.md#manage-smart-tags-and-searches)」を参照してください。

![ビデオスマートタグのモデレート](assets/manage-video-smart-tags.png)

>[!NOTE]
>
>[スマートタグの管理](smart-tags.md#manage-smart-tags-and-searches)の手順を使用してモデレートされたタグは、アセットの再処理時に記憶されません。元のタグセットが再び表示されます。

## ビデオスマートタグのオプトアウト {#opt-out-video-smart-tagging}

ビデオの自動タグ付けは、サムネールの作成やメタデータの抽出など、他のアセット処理タスクと並行して実行されるので、時間がかかる場合があります。アセットの処理を迅速に行うために、アップロード時にフォルダーレベルでビデオのスマートタグのオプトアウトを行うことができます。

特定のフォルダーにアップロードされたアセットに対してビデオスマートタグオプトアウトを自動生成するには、次の手順に従います。

1. フォルダー[!UICONTROL プロパティ]の「[!UICONTROL アセット処理]」タブを開きます。

1. [!UICONTROL ビデオのスマートタグ]メニューでは、「[!UICONTROL 継承]」オプションがデフォルトで選択され、ビデオスマートタグが有効になっています。

   「[!UICONTROL 継承]」オプションが選択されている場合、継承されたフォルダーのパスは、「[!UICONTROL 有効化]」と「[!UICONTROL 無効化]」のどちらに設定されているかという情報と共に表示されます。

   ![ビデオスマートタグの無効化](assets/disable-video-tagging.png)

1. フォルダーにアップロードされたビデオのスマートタグを無効にするには、「[!UICONTROL 無効化]」を選択します。

>[!IMPORTANT]
>
>アップロード時にフォルダーのビデオのタグ付けをオプトアウトして、アップロード後にビデオにスマートタグを付けたい場合は、フォルダーの[!UICONTROL プロパティ]の「[!UICONTROL アセット処理]」タブから&#x200B;**[!UICONTROL ビデオのスマートタグを有効化]**&#x200B;し、「[[!UICONTROL アセットの再処理]」オプション](#smart-tag-existing-videos)を使用してスマートタグを追加します。

## 信頼スコア {#confidence-score-video-tag}

各ビデオアセットのタグが多いとインデックス作成に時間がかるので、[!DNL Adobe Experience Manager] はタグ数が多くなりすぎないように、信頼性の最小しきい値をオブジェクトとアクションスマートタグに適用します。アセットの検索結果は、信頼スコアに基づいてランク付けされます。これにより、通常、ビデオアセットに割り当てられたタグの検査で示唆される以上に、検索結果が向上します。不正確なタグは信頼スコアが低いことが多いため、アセットのスマートタグリストの最上位に表示されることはめったにありません。

[!DNL Adobe Experience Manager] のアクションタグとオブジェクトタグのデフォルトのしきい値は 0.7 です（0 から 1 の間の値が必要）。一部のビデオアセットが特定のタグでタグ付けされていない場合、予測されたタグに 70% 未満の信頼性があることをアルゴリズムは示しています。デフォルトのしきい値は、すべてのユーザーにとって常に最適であるとは限りません。したがって、OSGI 構成では信頼スコア値を変更できます。

[!DNL Cloud Manager] を介して [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] にデプロイされたプロジェクトに信頼スコア OSGI 構成を追加するには、以下を行います。

* [!DNL Adobe Experience Manager] プロジェクト（Archetype 24 以降は `ui.config`、それ以前は `ui.apps`）の `config.author` OSGi 構成には `com.adobe.cq.assetcompute.impl.senseisdk.SenseiSdkImpl.cfg.json` という名前の構成ファイルが含まれ、以下がそのコンテンツです。

```json
{
  "minVideoActionConfidenceScore":0.5,
  "minVideoObjectConfidenceScore":0.5,
}
```

>[!NOTE]
>
>手動タグには信頼性 100%（最大の信頼性）が割り当てられます。したがって、検索クエリに一致する手動タグを持つビデオアセットがある場合、それらは検索クエリに一致するスマートタグの前に表示されます。

## 制限事項 {#video-smart-tagging-limitations}

* 特定のビデオを使用して、ビデオにスマートタグを適用するサービスをトレーニングすることはできません。デフォルトの [!DNL Adobe Sensei] 設定で機能します。

* タグ付けの進行状況は表示されません。

* ファイルサイズが 300 MB 未満のビデオのみ自動的にタグ付けされます。[!DNL Adobe Sensei] サービスは、サイズが大きいビデオファイルをスキップします。

* [スマートタグ](/help/assets/smart-tags.md#smart-tags-supported-file-formats)で言及されているファイル形式とサポート対象コーデックのビデオのみタグ付けされます。

>[!MORELIKETHIS]
>
>* [スマートタグとアセット検索の管理](smart-tags.md#manage-smart-tags-and-searches)
>* [スマートタグサービスのトレーニングと画像のタグ付け](smart-tags.md)
