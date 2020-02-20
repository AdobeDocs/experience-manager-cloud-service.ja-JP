---
title: AEMでのデジタルアセットと画像の検索
description: AEM のフィルターパネルを使用した必要なアセットの検索方法と検索で表示されたアセットの使用方法を説明します。
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 7141e42f53c556c0ac21def6085182ef400f5a71

---


# AEM でのアセットの検索 {#search-assets-in-aem}

Experience Managerのアセット検出オプションを使用して、コンテンツの速度を向上させることができます。 標準搭載の機能とカスタム方法を使用すると、シームレスでインテリジェントな検索機能により、チームは市場投入までの時間を短縮できます。 アセットの検索は、デジタルアセット管理システムの利用の中核を成します。用途は、クリエイティブ担当者によるさらなる利用、ビジネスユーザーやマーケティング担当者によるアセットの堅牢な管理、DAM 管理者による管理などです。AEM Assetsのユーザーインターフェイスや他のアプリケーションやサーフェスを介して実行できる、シンプルな、高度な、カスタム検索は、これらの使用例を満たすのに役立ちます。

AEMは次の使用例をサポートしており、この記事では、これらの使用例の使用方法、概念、設定、制限、トラブルシューティングについて説明します。

| アセットの検索 | 設定と管理 | 検索結果の操作 |
|--- |--- |--- |
| [基本検索](#searchbasics) | [検索インデックス](#searchindex) | [結果の並べ替え](#sort) |
| [検索UIについて](#searchui) |  | [アセットのプロパティとメタデータの確認](#checkinfo) |
| [サーチクエリ](#searchsuggestions) | [必須メタデータ](#mandatorymetadata) | [ダウンロード](#download) |
| [検索結果と行動の把握](#searchbehavior) | [検索ファセットの変更](#searchfacets) | [バルクメタデータの更新](#metadataupdates) |
| [検索ランクと昇順](#searchrank) | [テキスト抽出](#extracttextupload) | [スマートコレクション](#collections) |
| [アドバンス検索：検索のフィルタリングと範囲](#scope) | [カスタム述語](#custompredicates) | [予期しない結果を把握し](#unexpectedresults) 、トラブルシュ [ーティング](#troubleshoot) |
| [他のソリューションおよびアプリから検索](#beyondomnisearch): <br />Asset Link [](#aal) Desktop app <br />[](#desktopapp)<br />     [Adobe stock画像](#adobestock)<br />     ダイナミ [ックメディアアセット](#dynamicmedia) |  |  |
| [アセットの選択/選択](#assetselector) |  |  |
| [制限事項](#tips) とヒ [ント](#limitations) |  |  |
| [図の例](#samples) |  |  |

AEM webインターフェイスの上部にあるOmnisearchフィールドを使用してアセットを検索します。 AEMのアセッ **[!UICONTROL ト]** / **[!UICONTROL ファイルに移動し、上部のバーの]** search_icon ![](assets/do-not-localize/search_icon.png) をクリックし、検索キーワードを入力して、Returnキーを押します。 または、キーワードショートカット(ス `/` ラッシュ)を使用してOmnisearchフィールドを開きます。 `Location:Assets` が事前に選択され、検索がDAMアセットに制限されています。 アドバンス検索を実行して、検索範囲を拡大または [制限できます](#scope)。

Use the **[!UICONTROL Filters]** panel to search for assets, folders, tags, and metadata. ファイルタイプ、ファイルサイズ、最終変更日、アセットのステータス、インサイトデータ、Adobe stockライセンスなど、様々なオプション（述部）に基づいて検索結果をフィルターできます。 You can customize the Filters panel and add/remove search predicates using [search facets](/help/assets/search-facets.md).

AEM検索機能は、コレクションの検索とコレクション内のアセットの検索をサポートします。 コレクション [の検索を参照してくださ](/help/assets/manage-collections.md)い。

## 検索インターフェイスの理解 {#searchui}

検索インターフェイスと使用可能なアクションについて理解してください。

![](assets/aem_search_results.png) アセット検索結果インターフェイス図&#x200B;**&#x200B;の構成要素アセット検索結果インターフェイスの一部について

**** A.検索をスマートコレクションとして保存します。 **** B.フィルター（述語）を使用して、検索結果を絞り込みます。 **C.検索結果に** 、ファイル、フォルダ、またはその両方を表示します。 **** D.「フィルター」をクリックして、左側のレールを開くか閉じます。 **** E.検索場所はDAMです。 ************ F.ユーザが提供する検索キーワード **Gを含むOmnisearchフィールド。すべての検索結果** Hを選択する場合は、チェックボックスをオンにします。検索結果 **Iの合計中に表示された検索結果数。検索** Jを閉じます。カード表示とリスト表示の切り替え

### 動的検索ファセット {#dynamicfacets}

検索ファセット内で予想される検索結果の数は動的に更新されますが、この数を使用して、検索結果ページから目的のアセットをより迅速に見つけることができます。検索フィルターを適用する前であっても、予想されるアセット数は更新されます。フィルターに対して予想されるアセット数を確認すると、検索結果をすばやく効率的にナビゲートすることができます。詳しくは、[AEM でのアセットの検索](/help/assets/search-assets.md)を参照してください。

![検索ファセットで検索結果をフィルタリングしない場合のアセット概数の表示](assets/asset_search_results_in_facets_filters.png)

検索ファセットで検索結果をフィルタリングしない場合のアセット概数の表示

## 入力時のサーチクエリ {#searchsuggestions}

キーワードの入力を開始すると、AEMは可能な検索キーワードまたは語句を提案します。 提案は、AEMのアセットに基づいて行われます。 AEMは、検索に役立つすべてのメタデータフィールドのインデックスを作成します。 検索の提案を行うために、システムは次のいくつかのメタデータフィールドの値を使用します。 検索の提案を行う場合は、以下のフィールドに適切なキーワードを入力することを検討してください。

* アセットタグ。 (マップ先 `jcr:content/metadata/cq:tags`)
* アセットのタイトル。 (マップ先 `jcr:content/metadata/dc:title`)
* アセットの説明。 (マップ先 `jcr:content/metadata/dc:description`)
* JCRリポジトリ内のタイトル。 この値は、アセットのタイトルにマップされる場合があります。 (マップ先 `jcr:content/jcr:title`)
* JCRリポジトリ内の説明。 この値は、アセットの説明にマップされる場合があります。 (マップ先 `jcr:content/jcr:description`)

## 検索結果と行動の把握 {#searchbehavior}

### 基本検索用語と検索結果 {#searchbasics}

キーワード検索はOmniSearchフィールドから実行できます。 キーワード検索は、大文字と小文字が区別されず、（人気のあるメタデータフィールド全体で）全文検索です。 複数のキーワードを使用する場合、は `AND` キーワード間のデフォルトの演算子です。 結果は、最も近い一致から順に、関連性の高い順に並べ替えられます。 複数のキーワードの場合、メタデータに両方のキーワードが含まれるアセットが、より関連性の高い結果になります。 メタデータ内では、スマートタグとして表示されるキーワードは、他のメタデータフィールドに表示されるキーワードよりも高いランク付けが行われます。

AEMでは、特定の検索用語により高い重みを付与できます。 また、特定の検索用語に対して、ターゲット設定されたいくつかのアセットのランクを上げることもできます。 AEM管理者は、以下の説明に従ってこれらの設定を行うことができます。

関連するアセットをすばやく見つけるために、リッチインターフェイスには、フィルタリング、並べ替え、選択のメカニズムが用意されています。 複数の条件に基づいて結果をフィルタリングし、様々なフィルターで検索したアセットの数を確認できます。 または、[Omnisearch]フィールドのクエリを変更して検索を再実行することもできます。 検索用語やフィルターを変更しても、その他のフィルターは適用されたままになり、検索のコンテキストが保持されます。

検索結果に予期しないアセットが表示される場合があります。 詳しくは、「予期しない結果」を [参照してくださ](#unexpectedresults)い。

AEMでは様々なファイル形式を検索でき、検索フィルターはビジネス要件に合わせてカスタマイズできます。 管理者に問い合わせて、DAMリポジトリで使用できる検索オプションと、ログインにどのような制限があるかを確認してください。

<!-- 
### Results with and without Enhanced Smart Tags {#withsmarttags}

By default, AEM search combines the search terms with an AND clause. For example, consider searching for keywords woman running. Only the assets with both woman and running keywords in the metadata appear in the search results by default. The same behavior is retained when special characters (periods, underscores, or dashes) are used with the keywords. The following search queries return the same results:

* `woman running`
* `woman.running`
* `woman-running`

However, the query `woman -running` returns assets without `running` in their metadata.
Using smart tags adds an extra `OR` clause to find any of the search terms as the applied smart tags. An asset tagged with either `woman` or `running` using Smart Tags also appear in such a search query. So the search results are a combination of,

* Assets with `woman` and `running` keywords in the metadata (default behavior).

* Assets smart tagged with either of the keywords (Smart Tags behavior).
-->

### 検索のランク付けと昇順 {#searchrank}

メタデータフィールド内のすべての検索用語に一致する検索結果が最初に表示され、スマートタグ内の検索用語のいずれかに一致する検索結果はその後に表示されます。上記の例の場合、検索結果が表示される順序はおおよそ次のようになります。

1. Matches of `woman running` in the various metadata fields.
1. Matches of `woman running` in smart tags.
1. Matches of `woman` or of `running` in smart tags.

特定のアセットに対するキーワードの有効性を高めることで、キーワードに基づいた検索を強化できます。つまり、特定のキーワードを昇格させた場合、それらのキーワードに基づいて検索すると、それらのキーワードの対象となる画像が検索結果の最上部に表示されます。

1. アセットユーザーインターフェイスから、アセットのプロパティページを開きます。 「詳細」 **[!UICONTROL をクリックし]** 、「検索キーワードを **[!UICONTROL 昇格」の「追加]** 」をク **[!UICONTROL リックまたはタップします]**。
1. 「**[!UICONTROL 昇格を検索]**」ボックスで、画像検索時の強化の対象となるキーワードを指定し、「**[!UICONTROL 追加]**」をクリックまたはタップします。同じ方法で複数のキーワードを指定できます。
1. 「**[!UICONTROL 保存して閉じる]**」をクリックまたはタップします。このキーワードに対して昇格したアセットが、上位の検索結果に表示されます。

ターゲットキーワードの検索結果で一部のアセットのランクを上げることで、この機能を活用できます。 以下のビデオの例を参照してください。 For detailed info, see [search in AEM](https://helpx.adobe.com/experience-manager/kt/help/assets/search-feature-video-use.html).

>[!VIDEO](https://video.tv.adobe.com/v/16766/?quality=6)

*検索結果のランク付け方法とランクへの影響を把握する。*

## 詳細検索 {#scope}

AEMは、検索したアセットに適用されるフィルターなど、様々な方法を提供し、目的のアセットをすばやく見つけられるようにします。 一般的に使用される方法のいくつかを以下に示します。 以下に、 [図示された例を](#samples) いくつか示します。

**ファイルまたはフォルダの検索**:検索結果には、ファイル、フォルダ、またはその両方が表示されます。 フィル **[!UICONTROL ター]** ・パネルから、適切なオプションを選択できます。 「検索イン [ターフェイス](#searchui)」を参照。

**フォルダー内のアセットの検索**:検索対象を特定のフォルダーに限定できます。 フィルター **[!UICONTROL パネルで]** 、フォルダーのパスを追加します。 一度に1つのフォルダーのみを選択できます。

![フィルターパネルにフォルダーパスを追加して、検索結果をフォルダーに制限する](assets/search_folder_select.gif)

フィルターパネルにフォルダーパスを追加して、検索結果をフォルダーに制限する

<!--
### Find similar images {#visualsearch}

To find images that are visually similar to a user-selected image, click **[!UICONTROL Find Similar]** option from the card view of an image or from the toolbar. AEM displays the smart tagged images from the DAM repository that are similar to a user-selected image. See [how to configure similarity search](#configvisualsearch).

![Find similar images using the option in the card view](assets/search_find_similar.png)
*Figure: Find similar images using the option in the card view*
-->

### Adobe stock画像 {#adobestock}

From within the AEM user interface, users can search [Adobe Stock assets](/help/assets/aem-assets-adobe-stock.md) and license the required assets. Omnisearchバ `Location: Adobe Stock` ーでを追加します。 また、フィルターパネルを使用して、ライセンス済みまたはライセンスされていないアセットをすべて検索したり、Adobe stockのファイル番号を使用して特定のアセットを検索したりすることもできます。

### ダイナミックメディアアセット {#dmassets}

フィルターパネルからダイナミックメディア/セットを選択し **[!UICONTROL て、ダイナミックメディア画像をフィルター]** するこ **[!UICONTROL とができます]** 。 画像セット、カルーセル、混在メディアセット、スピンセットなどのアセットをフィルタリングして表示します。

### メタデータフィールドでの特定の値を使用した検索 {#gqlsearch}

タイトル、説明、作成者など、特定のメタデータフィールドの正確な値に基づいてアセットを検索できます。 GQLの全文検索機能は、メタデータ値が検索クエリーと完全に一致するアセットのみを取得します。 プロパティの名前（作成者、タイトルなど）と値の大文字と小文字は区別されます。

| メタデータフィールド | ファセット値と使用方法 |
|---|---|
| タイトル | title:John |
| 作成者 | creator:John |
| 場所 | 場所：NA |
| 説明 | description:&quot;Sample Image&quot; |
| 作成ツール | creatortool:&quot;Adobe Photoshop CC 2015&quot; |
| 著作権の所有者 | copyrightowner:&quot;Adobe Systems&quot; |
| 貢献者 | contributor:John |
| 使用条件 | usageterms:&quot;CopyRights Reserved&quot; |
| 作成日 | created:YYYY-MM-DDTHH |
| 有効期限 | expires:YYYY-MM-DDTHH |
| オンタイム | ontime:YYYY-MM-DDTHH |
| オフタイム | offtime:YYYY-MM-DDTHH |
| 時間の範囲（有効期限、オンタイム、オフタイム） | facet field : lowerbound..upperbound |
| パス | /content/dam/&lt;folder name> |
| PDF タイトル | pdftitle:&quot;Adobe Document&quot; |
| 件名 | subject:&quot;Training&quot; |
| タグ | tags:&quot;Location And Travel&quot; |
| タイプ | type:&quot;image\png&quot; |
| 画像の幅 | width:lowerbound..upperbound |
| 画像の高さ | height:lowerbound..upperbound |
| 人 | person:John |

プロパティのパス、制限、サイズ、およびorderbyを他のプロパティとORすることはできません。

ユーザー生成プロパティのキーワードは、プロパティエディターにおけるフィールドラベルからスペースを削除して小文字で表記したものです。

複雑なクエリの検索形式の例：

* 複数のファセットフィールドを持つアセットをすべて表示する（例：タイトル = John Doe、作成ツール = Adobe Photoshop）： `title:"John Doe" creatortool : Adobe*`
* To display all assets when the facets value is not a single word but a sentence (for example: title=Scott Reynolds): `title:"Scott Reynolds"`
* To display assets with multiple values of a single property (for example: title=Scott Reynolds or John Doe): `title:"Scott Reynolds" OR "John Doe"`
* To display assets with property values starting with a specific string (for example: title is Scott Reynolds): `title:Scott*`
* To display assets with property values ending with a specific string (for example: title is Scott Reynolds): `title:*Reynolds`
* To display assets with a property value that contains a specific string (for example: title = Basel Meeting Room): `title:*Meeting*`
* To display assets that contain a particular string and have a specific property value (for example: search for string Adobe in assets having title=John Doe): `*Adobe* title:"John Doe"`

## 他のAEMサービスまたはインターフェイスからのアセットの検索 {#beyondomnisearch}

Adobe Experience Manager (AEM)は、DAMリポジトリを様々なAEMソリューションに接続し、デジタルアセットへの高速アクセスを提供し、クリエイティブワークフローを合理化します。 アセットの検出は、ブラウズまたは検索で始まります。 検索の動作は、さまざまなサーフェスやソリューションで大きく同じままです。 対象となるオーディエンス、使用例およびユーザーインターフェイスはAEMソリューションによって異なるので、検索方法は変わります。 個々のソリューションに関する具体的な方法については、以下のリンクを参照してください。 この記事では、一般に適用されるヒントと動作について説明します。

### Adobe Asset Linkパネルからのアセットの検索 {#aal}

クリエイティブプロフェッショナルは、Adobe Asset linkを使用して、サポート対象のAdobe Creative cloudアプリケーションから離れることなく、AEM Assetsに保存されたコンテンツにアクセスできるようになりました。 クリエイティブは、Creative cloudアプリケーションのアプリケーション内パネルを使用して、アセットの参照、検索、チェックアウトおよびチェックインをシームレスに行うことができます。Photoshop、IllustratorおよびInDesign。 また、アセットリンクを使用すると、視覚的に類似した結果を検索できます。 視覚検索の表示結果は、Adobe Senseiの機械学習アルゴリズムを利用して、美的に類似した画像を見つけやすくします。 詳しくは、 [Adobe Asset Linkを使用したアセットの検索](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink) &amp;参照を参照してください。

### AEMデスクトップアプリでのアセットの検索 {#desktopapp}

クリエイティブプロフェッショナルは、デスクトップアプリケーションを使用して、AEM Assetsをローカルデスクトップ（WinまたはMac）で簡単に検索および利用できるようにします。 クリエイティブは、Mac finderまたはWindowsエクスプローラーで目的のアセットを簡単に表示し、デスクトップアプリケーションで開いてローカルに変更し、AEMに保存し直し、新しいバージョンをリポジトリで作成します。 1つ以上のキーワード*と？を使用した基本検索がサポートされます。 ワイルドカード、およびAND演算子。 デスクトップ [アプリケーションでのアセットの参照、検索](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#browse-search-preview-assets) 、プレビューを参照してください。

### Search assets in Brand Portal {#brandportal}

基幹業務のユーザーおよびマーケターは、Brand portalを使用して、承認されたデジタルアセットを、社内の拡張チーム、パートナーおよびリセラーと効率的かつ安全に共有します。 See [search assets on Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/search-capabilities/brand-portal-searching.html).

### Adobe stock画像の検索 {#adobestock-1}

AEM のユーザーインターフェイス内から Adobe Stock アセットを検索し、必要なアセットのライセンスを取得できます。「Omnisearch」 `Location: Adobe Stock` フィールドにを追加します。 また、フィルターパネルを使 **[!UICONTROL 用して]** 、ライセンス済みまたはライセンスされていないすべてのアセットを検索したり、Adobe stockのファイル番号を使用して特定のアセットを検索したりすることもできます。 AEMでの [Adobe stock画像の管理を参照してください](/help/assets/aem-assets-adobe-stock.md#usemanage)。

### ダイナミックメディアアセットの検索 {#dynamicmedia}

フィルターパネルでダイナミックメディア **[!UICONTROL /セットを選択して、ダイナミッ]** クメディア画像をフィル **[!UICONTROL ターで]** きます **** 。 画像セット、カルーセル、混在メディアセット、スピンセットなどのアセットをフィルタリングして表示します。 Webページの作成時に、作成者はコンテンツファインダー内でセットを検索できます。 セットのフィルターは、ポップアップメニューで使用できます。

### Webページの作成時のコンテンツファインダーでのアセットの検索 {#contentfinder}

作成者は、コンテンツファインダーを使用してDAMリポジトリで関連アセットを検索し、作成したWebページでアセットを使用できます。

<!-- Authors can also use the Connected Assets functionality to search for assets that are available on a remote AEM deployment. Authors can then use these assets in web pages on a local AEM deployment. See [use remote assets](use-assets-across-connected-assets-instances.md#use-remote-assets).
-->

### コレクションの検索 {#collections}

AEM検索機能は、コレクションの検索とコレクション内のアセットの検索をサポートします。 コレクション [の検索を参照してくださ](/help/assets/manage-collections.md)い。

## Asset selector {#assetselector}

アセットセレクターを使用すると、DAMアセットを特別な方法で検索、フィルターおよび参照できます。 アセットセレクターは、で使用できま `https://[aem_server]:[port]/aem/assetpicker.html`す。 選択したアセットのメタデータは、アセットセレクターを使用して取得できます。 アセットタイプ（画像、ビデオ、テキスト）や選択モード（単一または複数の選択）など、サポートされているリクエストパラメーターを使用して、このファイルを起動できます。 これらのパラメーターは、特定の検索インスタンスのアセットセレクターのコンテキストを設定し、選択範囲全体を通じてそのまま残ります。

The asset selector uses the HTML5 `Window.postMessage` message to send data for the selected asset to the recipient. アセットセレクターは、Granite の基盤ピッカーのボキャブラリに基づいています。デフォルトでは、アセットセレクターは、参照モードで動作します。

次のリクエストパラメーターを URL で渡して、特定のコンテキストでアセットセレクターを起動できます。

| 名前 | 値 | 例 | 目的 |
|---|---|---|---|
| resource suffix (B) | URL のリソースサフィックスとしてのフォルダーパス：[https://localhost:4502/aem/assetpicker.html/&lt;フォルダーパス>](https://localhost:4502/aem/assetpicker.html) | To launch the asset selector with a particular folder selected, for example with the folder /content/dam/we-retail/en/activities, selected, the URL should be of the form: [https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images](https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images) | アセットセレクターの起動時に特定のフォルダーを選択する必要がある場合、そのフォルダーをリソースサフィックスとして渡します。 |
| mode | single、multiple | [https://localhost:4502/aem/assetpicker.html?mode=multiplehttps://localhost:4502/aem/assetpicker.html?mode=single](https://localhost:4502/aem/assetpicker.html?mode=multiplehttps://localhost:4502/aem/assetpicker.html?mode=single) | 複数モードでは、アセットセレクターを使用して、いくつかのアセットを同時に選択できます。 |
| mimetype | mimetype(s) (`/jcr:content/metadata/dc:format`) of an asset (wildcard also supported) | <ul><li>[https://localhost:4502/aem/assetpicker.html?mimetype=image/png](https://localhost:4502/aem/assetpicker.html?mimetype=image/png)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*png](https://localhost:4502/aem/assetpicker.html?mimetype=*png)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*presentation](https://localhost:4502/aem/assetpicker.html?mimetype=*presentation)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*presentation&amp;mimetype=*png](https://localhost:4502/aem/assetpicker.html?mimetype=*presentation&mimetype=*png)</li></ul> | MIME タイプに基づいてアセットをフィルタリングするために使用します |
| dialog | true、false | [https://localhost:4502/aem/assetpicker.html?dialog=true](https://localhost:4502/aem/assetpicker.html?dialog=true) | これらのパラメータを使用して、Granite Dialogとしてアセットセレクタを開きます。 このオプションは、Granite Path fieldからアセットセレクターを起動し、pickerSrc URLとして設定した場合にのみ適用できます。 |
| assettype (S) | images、documents、multimedia、archives | <ul><li>[https://localhost:4502/aem/assetpicker.html?assettype=images](https://localhost:4502/aem/assetpicker.html?assettype=images)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=documents](https://localhost:4502/aem/assetpicker.html?assettype=documents)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=multimedia](https://localhost:4502/aem/assetpicker.html?assettype=multimedia)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=archives](https://localhost:4502/aem/assetpicker.html?assettype=archives)</li></ul> | 渡された値に基づいてアセットタイプをフィルタリングするには、このオプションを使用します。 |
| root | &lt;folder_path> | [https://localhost:4502/aem/assetpicker.html?assettype=images&amp;root=/content/dam/we-retail/en/activities](https://localhost:4502/aem/assetpicker.html?assettype=images&root=/content/dam/we-retail/en/activities) | アセットセレクターのルートフォルダーを指定するには、このオプションを使用します。この場合、アセットセレクターを使用すると、ルートフォルダーの下の子アセット（直接／間接）のみを選択できます。 |

To access the asset selector interface, go to `https://[AEM server]:[port]/aem/assetpicker`. 目的のフォルダーに移動して、1 つまたは複数のアセットを選択します。または、「Omnisearch」ボックスから目的のアセットを検索し、必要に応じてフィルターを適用して、選択します。

![アセットピッカーでアセットを参照して選択します](assets/assetpicker.png)

アセットピッカーでアセットを参照して選択します

## 制限事項 {#limitations}

AEM Assetsの検索機能には、次の制限があります。

* 検索クエリの先頭にスペースを入れないでください。スペースを入力しないと、検索が機能しません。
* 検索結果からアセットのプロパティを選択し、検索をキャンセルした後も、AEMは検索語を引き続き表示する場合があります。(CQ-4273540)
* フォルダ、ファイル、フォルダを検索する場合、検索結果をどのパラメータでも並べ替えることはできません。
* Omnisearchバーで何も指定せずにReturnキーを押すと、AEMはファイルのみのリストを返し、フォルダーは返しません。 キーワードを使用せずに特定のフォルダーを検索した場合、AEMは結果を返しません。

視覚検索または類似性検索には、次の制限があります。

* ビジュアル検索は、より大きなリポジトリで最も効果的です。 良好な結果を得るために必要な画像の数は最小限ですが、一致する画像の数が少ないと、大きなリポジトリの一致ほど良くない場合があります。
* モデルを変更したり、AEMをトレーニングして類似の画像を見つけることはできません。 例えば、一部のアセットにスマートタグを追加または削除しても、モデルは変更されません。 アセットは、視覚的に類似した検索結果から除外されます。

## 検索のヒント {#tips}

* アセットのレビューステータスを監視する場合は、該当するオプションを使用して、承認されているアセットまたは承認待ちのアセットを検索します。
* 様々な Creative アプリから取得した使用状況の統計に基づいて、サポートされるアセットを検索するには、インサイトの述語を使用します。使用状況データは、使用状況スコア、インプレッション数、クリック数およびメディアチャネルの下にグループ化され、アセットがカテゴリとして表示されます。
* チェックボックスを使用して、すべての検索結果または選択範囲に対して操作するフィルター適用済みの検索結果を選択します。 現在のユーザービューに表示されているアセットの数に関係なく、検索されたすべてのアセットが選択されます。 例えば、選択したすべてのアセットをダウンロードしたり、選択したすべてのアセットのメタデータプロパティを一括して更新したり、選択したアセットをコレクションに追加したりできます。
* 必須メタデータを含まないアセットを検索するには、必須メタデータを参 [照してくださ](#mandatorymetadata)い。
* 検索では、すべてのメタデータフィールドが使用されます。 12の検索など、汎用検索は通常多くの結果を返します。 より良い結果を得るには、二重引用符（単一引用符ではなく）を使用するか、特殊文字のない単語に番号が連続していることを確認し *ます(shoe12*)。
* フルテキスト検索では、-、^などの演算子を使用できます。 これらの文字を文字列リテラルとして検索するには、検索式を二重引用符で囲みます。例えば、「Notebook - Beauty」の代わりに「Notebook - Beauty」を使用します。
* 検索結果が多すぎる場合は、目的のアセ [ットに対して](#scope) 、検索範囲をゼロインに制限します。 特定のファイルタイプ、特定の場所、特定のメタデータなど、目的のアセットの検索方法を理解している場合に最も効果的です。

* **タグ**:タグを使用すると、閲覧や検索が効率的に行えるアセットを分類できます。 タグ付けは、適切な分類を他のユーザーやワークフローに伝播するのに役立ちます。 AEMは、使用状況やトレーニングを活用してアセットのタグ付けを改善し続ける、アドビ先生の人工的にインテリジェントなサービスを使用して、アセットに自動的にタグ付けする方法を提供しています。 アカウントで機能が有効な場合、アセットを検索する際にスマートタグが組み込まれます。 組み込み検索機能と同時に機能します。 検索動 [作を参照](#searchbehavior)。 検索結果が表示される順序を最適化するために、選択した複数のア [セットの検索ランクを](#searchrank) 「上げる」ことができます。

* **インデックス**:インデックス付きのメタデータとアセットのみが検索結果に返されます。 適切な範囲とパフォーマンスを確保するために、適切なインデックスを作成し、ベストプラクティスに従ってください。 indexingを参 [照](#searchindex)。

## 検索の例 {#samples}

キーワードの周囲で二重引用符を使用して、ユーザーが指定した順序で完全に一致するフレーズを含むアセットを検索します。

![検索動作（引用符の有無）](assets/search_with_quotes.gif)

検索動作（引用符の有無）

**アスタリスクワイルドカードで検索**:検索範囲を広げるには、任意の数の文字に一致するように、検索語の前または後にアスタリスクを使用します。 例えば、アスタリスクなしでrunを検索しても、（メタデータに含まれる）単語のバリエーションを含むアセットは返されません。 アスタリスクは任意の数の文字を置き換えます。 例：

* `run` 実行済みキーワードのアセットを返す
* `run*` 実行、実行、暴走などのアセットを返します。
* `*run` は、outrun、rerunなどを返します。
* `*run*` 可能なすべての組み合わせを返します。

![例を使用したアセット検索でのアスタリスクワイルドカードの使用例](assets/search_with_asterisk_run.gif)

例を使用したアセット検索でのアスタリスクワイルドカードの使用例

**疑問符ワイルドカードで検索**:検索範囲を広げるには、1つ以上の「?」を使用します。 文字を使用して、正確な文字数に一致させます。 例えば、次の図では、

* `run???` クエリがどのアセットとも一致しません。

* `run????` queryは、4文字後の単 `running` 語に一致します `run`。

* `??run` queryは、2文字前の単 `rerun` 語に一致します `run`。

![例を使用したアセット検索での疑問符ワイルドカードの使用](assets/search_with_questionmark_run.gif)

例を使用したアセット検索での疑問符ワイルドカードの使用

**キーワードの除外**:ダッシュを使用して、キーワードを含まないアセットを検索します。 例えば、クエリー `running -shoe` は、を含むが含まないアセ `running`ットを返しま `shoe`す。 同様に、クエ `camp -night` リーは、を含むが含まないアセット `camp` を返しま `night`す。 クエリーは、 `camp-night` との両方を含むアセットを返すことに注意し `camp` てくださ `night`い。

![ダッシュを使用して、除外されたキーワード図を含まないアセットを検索](assets/search_dash_exclude_keyword.gif)*します。ダッシュを使用して、除外されたキーワードを含まないアセットを検索する*

<!--
## Configuration and administration tasks related to search functionality {#configadmin}

### Search index configurations {#searchindex}

Asset discovery relies on indexing of DAM contents, including the metadata. Faster and accurate asset discovery relies on optimized indexing and appropriate configurations. See [indexing](/help/operations/indexing.md).

### Sort on Name column {#sortbyname}

In list view, you can sort the search results just as you can sort assets in any folder. Sorting does not work on the `Name` column by default. To sort by the `Name` column, overlay `/libs/dam/gui/content/commons/availablecolumns` and change the value of sortable to `True`.

<!--
### Visual or similarity search {#configvisualsearch}

Visual search uses smart tagging and requires AEM 6.5.2.0 or later. After configuring smart tagging functionality, follow these steps.

1. In AEM CRXDE, in `/oak:index/lucene` node, add the following properties and values and save the changes.

    * `costPerEntry` property of type `Double` with the value `10`.

    * `costPerExecution` property of type `Double` with the value `2`.

    * `refresh` property of type `Boolean` with the value `true`.

   This configuration allows searches from the appropriate index.

1. To create Lucene index, in CRXDE, at `/oak:index/damAssetLucene/indexRules/dam:Asset/properties`, create node named `imageFeatures` of type `nt-unstructured`. In `imageFeatures` node,

    * Add `name` property of type `String` with the value `jcr:content/metadata/imageFeatures/haystack0`.

    * Add `nodeScopeIndex` property of type `Boolean` with the value of `true`.

    * Add `propertyIndex` property of type `Boolean` with the value of `true`.

    * Add `useInSimilarity` property of type `Boolean` with the value `true`.

   Save the changes.

1. Access `/oak:index/damAssetLucene/indexRules/dam:Asset/properties/predictedTags` and add `similarityTags` property of type `Boolean` with the value of `true`.
1. Apply Smart Tags to the assets in your AEM repository. See [how to configure smart tags](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/smart-tags-technical-video-setup.html).
1. In CRXDE, in `/oak-index/damAssetLucene` node, set the `reindex` property to `true`. Save the changes.
1. (Optional) If you have customized search form then copy the `/libs/settings/dam/search/facets/assets/jcr%3Acontent/items/similaritysearch` node to `/conf/global/settings/dam/search/facets/assets/jcr:content/items`. Save all the changes.

For related information, see [understand smart tags in AEM](https://helpx.adobe.com/experience-manager/kt/help/assets/smart-tags-feature-video-understand.html) and [how to manage smart tags](/help/assets/smart-tags.md).

-->
<!--

### Mandatory metadata {#mandatorymetadata}

Business users, administrators, or DAM librarians can define some metadata as mandatory metadata that is a must for the business processes to work. For various reasons, some assets may be missing this metadata, such as legacy assets or assets migrated in bulk. Assets with missing or invalid metadata are detected and reported based on the indexed metadata property. To configure it, see [mandatory metadata](/help/assets/metadata-schemas.md#defining-mandatory-metadata).

### Modify search facets {#searchfacets}

To improve the speed of discovery, AEM Assets offers search facets using which you can filter the search results. The Filters panel includes a few standard facets by default. Administrators can customize the Filters panel to modify the default facets using the in-built predicates. AEM provides a good collection of in-built predicates and an editor to customize the facets. See [search facets](/help/assets/search-facets.md).

### Extract text when uploading assets {#extracttextupload}

You can configure AEM to extract the text from the assets when users upload assets, such as PSD or PDF files. AEM indexes the extracted text and helps users search these assets based on the extracted text. See [upload assets](/help/assets/manage-digital-assets.md#uploading-assets).

<!-- Check with gklebus if this customization is possible in Cloud Service now

### Custom predicates to filter search results {#custompredicates}

Predicates are used to create facets. Administrators can customize the search facets in the Filters panel using pre-configured predicates. These predicates can be customized using overlays. See [create custom predicates](/help/assets/searchx.md).

You can search for digital assets based on one or more of the following properties. Filters that apply on some of these properties are available by default and some other filters can be custom-created to apply on the other properties.

| Search field | Search property values |
|---|---|
| MIME Types | Images, Documents, Multimedia, Archives, or Other. |
| Last Modified | Hour, Day, Week, Month, or Year. |
| File Size | Small, Medium, or Large. |
| Publish Status | Published or Unpublished. |
| Approved Status | Approved or Rejected. |
| Orientation | Horizontal, Vertical, or Square. |
| Style | Color, or Black & White. |
| Video Height | Specified as a minimum and maximum value. Value is stored in the metadata of video renditions only. |
| Video Width | Specified as a minimum and maximum value. Value is stored in the metadata of video renditions only. |
| Video Format | DVI, Flash, MPEG4, MPEG, OGG Theora, QuickTime, Windows Media. Value is stored in the metadata of the source video and any renditions. |
| Video Codec | x264. Value is stored in the metadata of video renditions only. |
| Video Bitrate | Specified as a minimum and maximum value. Value is stored in the metadata of video renditions only. |
| Audio Codec | Libvorbis, Lame MP3, AAC Encoding. Value is stored in the metadata of video renditions only. |
| Audio Bitrate | Specified as a minimum and maximum value. Value is stored in the metadata of video renditions only. |

-->

## アセット検索結果の操作 {#aftersearch}

条件に一致する検索済みアセットが表示されたら、これらの検索結果に対して次の一般的なタスクを実行するか、または次のアクションを実行できます。

* メタデータのプロパティとその他の情報を表示します。
* 1つ以上のアセットをダウンロードします。
* デスクトップアクションを使用して、デスクトップアプリでこれらのアセットを開きます。
* スマートコレクションを作成します。

### 検索結果の並べ替え {#sort}

検索結果を並べ替えると、必要なアセットをすばやく見つけることができます。 検索結果の並べ替えは、リストビューで機能し、フィルターパネルで「フ **[!UICONTROL [ァイル](#searchui)]**」を選択した場**[!UICONTROL &#x200B;合のみ&#x200B;]**行います。 AEM Assetsでは、サーバーサイドの並べ替えを使用して、フォルダー内のすべてのアセット（数量）や検索クエリの結果をすばやく並べ替えます。 サーバー側の並べ替えは、クライアント側の並べ替えよりも高速で正確な結果を提供します。

リストビューでは、任意のフォルダ内のアセットを並べ替えるのと同じように、検索結果を並べ替えることができます。 並べ替えは、「タイトル」、「ステータス」、「ディメンション」、「サイズ」、「評価」、「使用状況」、「変更日」、「発行日」、「ワークフロー」、「チェックアウト」の各列で行われます。

「名前列 [での並べ替えの設定」を参照してくださ](#sortbyname)い。 並べ替え機能の制限については、制限を参照して [ください](#limitations)。

### アセットの詳細情報の確認 {#checkinfo}

検索したアセットの詳細情報は、検索結果ページで確認できます。

アセットのすべてのメタデータを表示するには、アセットを選択し、ツールバーから **[!UICONTROL プロパティ]** をクリックします。

アセットに対するコメントまたはアセットのバージョン履歴を確認するには、アセットをクリックして大きいサイズのプレビューを開きます。 左側のレールでタイムラインを開き、「コメント」または「バ **[!UICONTROL ージョン]** 」を **[!UICONTROL 選択します]**。 また、コメントやバージョンなどのタイムラインアクティビティを時系列順に並べ替えることもできます。

![検索アセットのタイムラインエントリの並べ替え](assets/sort_timeline_search_results.gif)

検索アセットのタイムラインエントリの並べ替え

### 検索したアセットのダウンロード {#download}

フォルダから通常のアセットをダウンロードするのと同じように、検索したアセットとそのレンディションをダウンロードできます。 検索結果から1つ以上のアセットを選択し、ツールバーの「ダウ **[!UICONTROL ンロード]** 」をクリックします。

### メタデータプロパティの一括更新 {#metadataupdates}

複数のアセットの共通のメタデータフィールドに対して一括更新を行うことができます。 検索結果から、1つ以上のアセットを選択します。 ツールバ **[!UICONTROL ーで「プロパティ]** 」をクリックし、必要に応じてメタデータを更新します。 完了したら **[!UICONTROL 「保存して閉じる]** 」をクリックします。 更新されたフィールド内の既存のメタデータが上書きされます。

単一のフォルダーまたはコレクションで使用できるアセットの場合、メタデータを一括 [で更新する方が簡単です](/help/assets/manage-metadata.md#manage-assets-metadata)。 複数のフォルダーで使用できるアセットや共通の条件に一致するアセットの場合は、検索を使用してメタデータを一括更新する方が高速です。

### スマートコレクション {#collections-1}

コレクションは、異なる場所のアセットを含めることができる、順序付けられたアセットのセットです。コレクションには、これらのアセットへの参照のみが含まれます。 コレクションは次の2つのタイプで構成されます。

* アセット、フォルダーおよびその他のコレクションの静的参照リストです。
* 検索条件に基づいてコレクション内のアセットを入力する動的リスト（スマートコレクション）。

検索条件に基づいてスマートコレクションを作成できます。 フィルターパネ **[!UICONTROL ルで]** 「ファイル」を選 **[!UICONTROL 択し、「スマートコレクション]** を保存」をクリックします ****。 コレクション [の管理を参照してくださ](/help/assets/manage-collections.md)い。

## 予期しない検索結果 {#unexpectedresults}

**見つからないメタデータを検索**:必須のメタデータがないアセットを検索すると、AEMで有効なメタデータを持つアセットが表示される場合があります。 インデックス付きメタデータプロパティに基づいて、見つからないメタデータが検出され、報告されます。 アセットのメタデータが固定されていても、インデックスの再作成が行われるまで、メタデータが見つからないものとして引き続き表示されます。 必須メタデ [ータを参照してくださ](/help/assets/metadata-schemas.md#defining-mandatory-metadata)い。

**検索結果が多すぎます**:検索結果が多くなるのを防ぐために、検索結果を制限することを検討してください。 例えば、DAM内のアセットを検索するには、Omnisearchバーでを `Location:Assets` 選択します。 その他の検索フィルタについては、「検 [索範囲」を参照](#scope)。

<!-- Another reason to get more than expected search results can be use of smarts tags. See [search behavior with smart tags](#withsmarttags). 
-->

<!--
**Partially related or unrelated search results**: AEM may display seemingly partially related or unrelated assets, alongside the desired assets in the search results. If you enable Enhanced Smart Tags, the search behavior changes slightly. See how it changes [after smart tagging](#withsmarttags).
-->

**新しくアップロードされたアセットに対するオートコンプリートの提案はありません**。Omnisearchバーで検索キーワードを入力し始めると、最近アップロードされたアセットのメタデータ（タイトル、タグなど）を提案としてすぐに使用できなくなります。 AEM Assetsは、タイムアウト期間（デフォルトで1時間）が経過するまで待機してから、バックグラウンドジョブを実行し、新しくアップロードまたは更新されたすべてのアセットのメタデータのインデックスを作成し、そのメタデータを提案のリストに追加します。

**検索結果なし**:AEMで検索クエリの空白ページを表示する場合は、次の理由が考えられます。

* クエリに一致するアセットが存在しません。
* 検索クエリの前に空白を追加します。 これは既知の [制限です](#limitations)。

* サポートされていないメタデータフィールドに、検索するキーワードが含まれています。 すべてのメタデータフィールドが検索用と見なされるわけではありません。 「 [scope](#scope)」を参照。
* オンタイムとオフタイムはアセットに対して設定され、アセットのオフタイム中に検索が行われました。

**検索フィルタ/述語が使用できません**:フィルターの検索に必要なカスタマイズがユーザーインターフェイスで使用できない場合は、管理者に問い合わせて、カスタマイズがすべての作成者と使用している実稼働サーバーに実装されたかどうかを確認してください。 設定が正しくなかった可能性があります。

## 検索関連の問題のトラブルシューティング {#troubleshoot}

以下の問題と考えられる対策を参照してください。

* 必要な検索フィルター/述語が表示されない場合は、管理者に問い合わせてください。
* 視覚的に類似した画像を検索する場合、検索結果に期待した画像が表示されないことがあります。 そのようなアセットがインデックス付けされ、スマートタグ付けされているかどうかを確認します。
* 視覚的に類似した画像を検索する場合、検索結果には、一見無関係に見える画像が表示されることがあります。 AEMは、可能な限り多くの関連するアセットを表示します。 関連性の低い画像がある場合は結果に追加されますが、検索のランクは低くなります。 検索結果を下にスクロールすると、一致の質と検索されたアセットの関連性が低下します。
