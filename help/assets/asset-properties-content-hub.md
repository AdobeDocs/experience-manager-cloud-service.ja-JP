---
title: ' [!DNL the Content Hub] でのアセットとそのプロパティのプレビュー'
description: ' [!DNL Content Hub] でアセットとプロパティをプレビューする方法について説明します。'
role: User
exl-id: a85af980-4c51-4d30-9fad-afd16370e9db
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '710'
ht-degree: 96%

---

# コンテンツハブでのアセットとそのプロパティのプレビュー {#asset-properties}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup>Dynamic Media Prime<a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM AssetsUltimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM AssetsとEdge Delivery Servicesの統合 </b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup><a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI 拡張機能 </b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Dynamic Media Prime</i></sup>Ultimateの新 <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b> 能 </b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>検索のベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>メタデータのベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>コンテンツハブ</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>OpenAPI 機能を備えた Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 開発者向けドキュメント</b></a>
        </td>
    </tr>
</table>

![メタデータバナー画像](assets/metadata-banner-image.png)

>[!AVAILABILITY]
>
>コンテンツハブガイドを PDF 形式で利用できるようになりました。ガイド全体をダウンロードし、Adobe Acrobat AI アシスタントを使用して質問に答えてください。
>
>[!BADGE コンテンツハブガイドの PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

[!DNL The Content Hub] を使用すると、効率的なアセット配布に重要なアセットに関する情報を表示できます。アセットに使用可能なすべてのデータのコレクションです。

アセットプレビューとそのプロパティの表示は、アセットをより細かく分類でき、デジタル情報量が大きくなるにつれ便利です。数百個のファイルをファイル名、サムネールおよびメモリだけに基づいて管理することは可能です。ただし、この手法は、関係者の数や管理するアセットの数が増えると、拡張性が低くなります。さらに、以下の理由からデジタルアセットの価値が大きくなります。

* アクセスが容易になる - システムやユーザーが簡単に見つけることができます。
* 操作が容易になる - アセットのビジュアルと関連情報に関する完全な情報が得られるので、より迅速かつ信頼性の高い方法で操作できます。
* 完全 - アセットは、より多くの情報とコンテキストを保持します。

## 前提条件 {#prerequisites}

[コンテンツハブユーザー](deploy-content-hub.md#onboard-content-hub-users)は、この記事で説明されているアクションを実行できます。

## アセットとそのプロパティのプレビュー {#properties-ui}

アセットを使用、共有またはダウンロードする前に、より詳細に表示できます。プレビュー機能を使用すると、画像だけでなく、サポートされているその他のアセットタイプも表示できます。アセットを表示できるだけでなく、詳細な情報を表示したり、その他のアクションを実行したりできます。アセットの情報を表示するには、アセットに移動するか、アセットを[検索](search-assets.md)してから、アセットをクリックしてプロパティを開きます。次の図は、アセットのプロパティページで使用できるフィールドを示しています。

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

[!DNL Content Hub] は、基になる [!DNL Assets] リポジトリがサポートするすべてのアセットタイプと形式をサポートします。次の表に、アセットを視覚的にプレビューする追加サポートを提供する [!DNL the Content Hub] の主なファイル形式を示します。

<table> 
    <tbody>
     <tr>
      <th><strong>ファイルタイプ</strong></th>
      <th><strong>サポートされる形式</strong></th>
     </tr>
     <tr>
      <td>画像</td>
      <td>
        <ul>
            <li>[!UICONTROL JPEG]</li> 
            <li>[!UICONTROL PNG]</li> 
            <li>[!UICONTROL SVG]</li>
        </ul>
      </td>
     </tr>
     <tr>
      <td>ビデオ</td>
      <td>
        <ul>
            <li>[!UICONTROL Quicktime]</li>  
            <li>[!UICONTROL MP4]</li> 
        </ul>
      </td>
     </tr>
      <tr>
      <td>ドキュメント</td>
      <td>
        <ul>
            <li>[!UICONTROL txt]（プレーン）</li>  
            <li>[!UICONTROL Doc/Docx]</li> 
            <li>[!UICONTROL XML]</li>
        </ul>
      </td>
     </tr>
     <tr>
      <td>メディアを印刷</td>
      <td>
        <ul>
            <li>[!UICONTROL PDF]</li>  
        </ul>
      </td>
     </tr>  
    </tbody>
   </table>

### 派生プロパティ {#derived-properties}

[!DNL Content Hub] に表示されるアセットの一部のプロパティは、アセットが [!DNL Assets] にアップロードされ、[!DNL Content Hub] での使用が承認された際に、自動的に派生または生成されます。その一部の一覧を以下に示します。

* **サイズ：**&#x200B;サイズは、基になるリポジトリに保存されているアセットバイナリのサイズを表します。

<!--* **Tags:** Tags help you categorize assets that can be browsed and searched more efficiently. Tagging helps in propagating the appropriate taxonomy to other users and workflows. -->

* **スマートタグ：**&#x200B;[!DNL The Content Hub] は、Adobe Sensei のスマートコンテンツサービスを使用して、タグベースの構造の認識アルゴリズムを使用してアセットのトレーニングを行います。その後、このコンテンツインテリジェンスを使用して、アセットの個々のセットに関連性の高いタグが適用されます。スマートタグを使用すると、関連性の高いアセットをすばやく見つけるうえで役に立つので、プロジェクトのコンテンツベロシティ（コンテンツ創出の速度）が向上します。スマートタグは、画像に含まれないアセット情報の例です。デフォルトで、[!DNL Experience Manager Assets] はアセットにスマートタグを自動的に適用します。

* **カラータグ：**&#x200B;[カラータグ](#https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/color-tag-images.html?lang=ja)は、アドビの Sensei AI 機能を用いてアセット内で自動識別されるカラーを使用して、アセットを認識するのに役立ちます。

* アップロード日

* アップロード実行者

* 最終変更日

* 最終変更者

コンテンツハブにアセットを追加する際に指定するプロパティもあります。詳しくは、[コンテンツハブへのブランド承認済みアセットの追加](upload-brand-approved-assets.md)を参照してください。これらのプロパティは、アセットプロパティページにも表示されます。

また、管理者は、次の各アセットに表示されるプロパティを設定することもできます。

* アセットプレビュー UI の場合：詳しくは、[コンテンツハブユーザーインターフェイスの設定](configure-content-hub-ui-options.md#configure-asset-details-content-hub)を参照してください。
* 検索結果またはコレクションのアセットカードの場合：詳しくは、[コンテンツハブユーザーインターフェイスの設定](configure-content-hub-ui-options.md#asset-card)を参照してください。

<!--

### Date range {#date-range} 

The date range allows you to select dates you want to see the assets. You can customize date range by choosing the start and end dates. 

-->
