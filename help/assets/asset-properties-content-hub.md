---
title: ' [!DNL the Content Hub] でのアセットとそのプロパティのプレビュー'
description: ' [!DNL Content Hub] でアセットとプロパティをプレビューする方法について説明します。'
role: User
badgeSaas: label="AEM Assets" type="Positive" tooltip="AEM Assetsに適用）。"
exl-id: a85af980-4c51-4d30-9fad-afd16370e9db
source-git-commit: 230ca753bd5f3d5b26b30a962a526dc0edfc9bd4
workflow-type: tm+mt
source-wordcount: '1041'
ht-degree: 61%

---

# コンテンツハブでのアセットとそのプロパティのプレビュー {#asset-properties}

![メタデータバナー画像](assets/metadata-banner-image.png)

[!DNL The Content Hub] を使用すると、効率的なアセット配布に重要なアセットに関する情報を表示できます。 アセットに使用可能なすべてのデータのコレクションです。

アセットプレビューとそのプロパティの表示は、アセットをより細かく分類でき、デジタル情報量が大きくなるにつれ便利です。 数百個のファイルをファイル名、サムネールおよびメモリだけに基づいて管理することは可能です。 ただし、この手法は、関係者の数や管理するアセットの数が増えると、拡張性が低くなります。 さらに、以下の理由からデジタルアセットの価値が大きくなります。

* アクセスが容易になる - システムやユーザーが簡単に見つけることができます。
* 操作が容易になる - アセットのビジュアルと関連情報に関する完全な情報が得られるので、より迅速かつ信頼性の高い方法で操作できます。
* 完全 - アセットは、より多くの情報とコンテキストを保持します。

## 前提条件 {#prerequisites}

[コンテンツハブユーザー](deploy-content-hub.md#onboard-content-hub-users)は、この記事で説明されているアクションを実行できます。

## アセットとそのプロパティのプレビュー {#properties-ui}

アセットを使用、共有またはダウンロードする前に、より詳細に表示できます。 プレビュー機能を使用すると、画像だけでなく、サポートされているその他のアセットタイプも表示できます。 アセットを表示できるだけでなく、詳細な情報を表示したり、その他のアクションを実行したりできます。 アセットの情報を表示するには、アセットに移動するか、アセットを[検索](search-assets.md)してから、アセットをクリックしてプロパティを開きます。 次の図は、アセットのプロパティページで使用できるフィールドを示しています。

![アセット UI のプロパティ](assets/properties-ui.png)

* **A：**&#x200B;アセットのタイトル
* **B：**&#x200B;ズームインまたはズームアウトして、アセットをより詳細にズームまたはプレビューする割合
* **C：**&#x200B;前に選択した割合でズームを元に戻す
* **D：**&#x200B;前または次のアセットに進む
* **E：**&#x200B;アセットの数
* **F：**&#x200B;アセットのダウンロード
* **G：**&#x200B;[!DNL Adobe Express] を使用したアセットを編集
* **H：**&#x200B;アセットの情報を折りたたむまたはプレビュー
* **I：**&#x200B;アセットを共有
* **J：**&#x200B;[!DNL Collection] にアセットを追加
* **K：**&#x200B;プレビュー画面を閉じる
* **L：**&#x200B;タイトル、形式、サイズ、解像度、タグ、カラータグ、スマートタグを含むアセットの情報。

## サポートされるアセット形式 {#supported-formats}

[!DNL Content Hub] は、基になる [!DNL Assets] リポジトリがサポートするすべてのアセットタイプと形式をサポートします。 次の表に、アセットを視覚的にプレビューする追加サポートを提供する [!DNL the Content Hub] の主なファイル形式を示します。

<table> 
    <tbody>
     <tr>
      <th><strong>ファイルタイプ</strong></th>
      <th><strong>サポートされる形式</strong></th>
     </tr>
     <tr>
        <td rowspan="3"> 画像 </td>
    </tr>
    </tr>
    <tr>
        <td>[!UICONTROL JPEG]</td>
    </tr>
    <tr>
        <td>[!UICONTROL PNG]</td>
    </tr>
    <tr>
        <td rowspan="4"> ビデオ </td>
    </tr>
    </tr>
    <tr>
        <td>[!UICONTROL Quicktime]</td>
    </tr>
    <tr>
        <td>[!UICONTROL MP4]</td>
    </tr>
    <tr>
        <td>[!UICONTROL MPEG]</td>
    </tr>
    <tr>
        <td rowspan="4"> ドキュメント </td>
    </tr>
    </tr>
    <tr>
        <td>[!UICONTROL txt]（プレーン）</td>
    </tr>
    <tr>
        <td>[!UICONTROL Doc/Docx]</td>
    </tr>
    <tr>
        <td>[!UICONTROL XML]</td>
    </tr>
    <tr>
        <td rowspan="2"> メディアを印刷 </td>
    </tr>
    </tr>
    <tr>
        <td>[!UICONTROL PDF]</td>
    </tr>
    </tbody>
</table>

### 派生プロパティ {#derived-properties}

[!DNL Content Hub] に表示されるアセットの一部のプロパティは、アセットが [!DNL Assets] にアップロードされ、[!DNL Content Hub] での使用が承認された際に、自動的に派生または生成されます。 その一部の一覧を以下に示します。

* **サイズ：**&#x200B;サイズは、基になるリポジトリに保存されているアセットバイナリのサイズを表します。

<!--* **Tags:** Tags help you categorize assets that can be browsed and searched more efficiently. Tagging helps in propagating the appropriate taxonomy to other users and workflows. -->

* **スマートタグ：** [!DNL The Content Hub]は、Adobe AIのスマートコンテンツサービスを使用して、タグベースの構造に対する認識アルゴリズムを使用してアセットをトレーニングします。 その後、このコンテンツインテリジェンスを使用して、アセットの個々のセットに関連性の高いタグが適用されます。 スマートタグを使用すると、関連性の高いアセットをすばやく見つけるうえで役に立つので、プロジェクトのコンテンツベロシティ（コンテンツ創出の速度）が向上します。 スマートタグは、画像に含まれないアセット情報の例です。 デフォルトで、[!DNL Experience Manager Assets] はアセットにスマートタグを自動的に適用します。

* **カラータグ：** [&#x200B; カラータグ &#x200B;](#https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/color-tag-images.html?lang=en)を使用すると、AdobeのAI機能を使用して、アセット内で自動的に識別されるカラーを使用してアセットを識別できます。

* アップロード日

* アップロード実行者

* 最終変更日

* 最終変更者

コンテンツハブにアセットを追加する際に指定するプロパティもあります。 詳しくは、[コンテンツハブへのブランド承認済みアセットの追加](upload-brand-approved-assets.md)を参照してください。 これらのプロパティは、アセットプロパティページにも表示されます。

また、管理者は、次の各アセットに表示されるプロパティを設定することもできます。

* アセットプレビュー UI の場合：詳しくは、[コンテンツハブユーザーインターフェイスの設定](configure-content-hub-ui-options.md#configure-asset-details-content-hub)を参照してください。
* 検索結果またはコレクションのアセットカードの場合：詳しくは、[コンテンツハブユーザーインターフェイスの設定](configure-content-hub-ui-options.md#asset-card)を参照してください。

<!--

### Date range {#date-range} 

The date range allows you to select dates you want to see the assets. You can customize date range by choosing the start and end dates. 

-->

## よくある質問 {#faqs-asset-properties-content-hub}

### AEM Assets Content Hubでアセットとそのプロパティをプレビューする理由

AEM Assets Content Hubでアセットとそのプロパティをプレビューすると、アセットの詳細を詳細に確認できます。これは、効率的なアセットの配信と管理に不可欠です。 デジタル情報の増加に伴い、ファイル名やサムネールを使用するだけでは拡張性がなくなります。 詳細なプロパティを確認することで、アセットを分類し、アクセスを容易にし、行動を促進し、あらゆる顧客に情報を確実に提供できるようになります。

### AEM Assets Content Hubでアセットのプロパティを表示して操作するにはどうすればよいですか？

AEM Assets Content Hubでアセットのプロパティを表示するには、アセットに移動するか検索し、アセットをクリックしてプロパティページを開きます。 ここでは、プレビューのズームインまたはズームアウト、ズームの取り消し、前または次のアセットへの移動、アセットのダウンロード、Adobe Expressでの編集、コレクションへの追加、プレビューの閉じなどを行うことができます。 プロパティページには、タイトル、形式、サイズ、解像度、タグ、カラータグ、スマートタグなどの詳細情報が表示されます。

### AEM Assets Content Hubの派生プロパティとは何か、どのように生成されますか？

AEM Assets Content Hubの派生プロパティは、アセットがアップロードおよび承認されると自動的に生成されます。 例えば、アセットのサイズ、スマートタグ、カラータグなどがあります。 スマートタグ Adobe AIのスマートコンテンツサービスを使用して、関連するタグを自動的に認識および適用し、アセットの見つけやすさを向上させることができます。 また、カラータグもAIを活用して自動的に識別されるため、ユーザーは目立つ色でアセットを認識することができます。

### 管理者は、AEM Assets Content Hubに表示されるアセットプロパティをカスタマイズできますか？

はい。管理者は、AEM Assets Content Hubの各アセットに対して表示するプロパティを設定できます。 これは、アセットのプレビューユーザーインターフェイスと、検索結果やコレクション内のアセットカードの両方に対して実行でき、ユーザーが要件に基づいて最も関連性の高い情報を確認できるようにします。

### AEM Assets Content Hubでアセットをプレビューするためにサポートされているファイル形式は何ですか？

AEM Assets Content Hubでサポートされているファイル形式には、JPEGおよびPNGの画像、Quicktime、MP4、MPEGのビデオ、TXT、DOC/DOCX、XMLのドキュメント、PDFの印刷媒体などがあります。


**関連情報**

* [アセットを翻訳](/help/assets/translate-assets.md)
* [Assets HTTP API](/help/assets/mac-api-assets.md)
* [AEM Assets as a Cloud Service でサポートされているファイル形式](/help/assets/file-format-support.md)
* [アセットを検索](/help/assets/search-assets.md)
* [接続されたアセット](/help/assets/use-assets-across-connected-assets-instances.md)
* [アセットレポート](/help/assets/asset-reports.md)
* [メタデータスキーマ](/help/assets/metadata-schemas.md)
* [アセットをダウンロード](/help/assets/download-assets-from-aem.md)
* [メタデータを管理](/help/assets/manage-metadata.md)
* [Dynamic Media テンプレートの管理](/help/assets/dynamic-media/manage-dynamic-media-templates.md)
* [レポートの管理](/help/assets/manage-reports-assets-view.md)
* [検索ファセット](/help/assets/search-facets.md)
* [コレクションを管理](/help/assets/manage-collections.md)
* [メタデータの一括読み込み](/help/assets/metadata-import-export.md)
* [AEM および Dynamic Media へのアセットの公開](/help/assets/publish-assets-to-aem-and-dm.md)
