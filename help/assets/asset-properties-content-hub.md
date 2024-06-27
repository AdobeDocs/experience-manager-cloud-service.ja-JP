---
title: のアセットプロパティ [!DNL the Content Hub]
description: でアセットプロパティを表示および管理する方法を説明します [!DNL Content Hub]
role: User
source-git-commit: e590c34c177e6b45b6a52370caa88da54b61ebc0
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 12%

---


# Content Hubでのアセットプロパティの管理 {#asset-properties}

![メタデータバナー画像](assets/metadata-banner-image.png)

[!DNL The Content Hub] では、効率的なアセット配布にとって重要なアセットに関する情報を表示できます。 アセットに使用可能なすべてのデータのコレクションです。

アセットプロパティを表示すると、アセットをより詳細に分類するのに役立ち、デジタル情報量が多くなるにつれてさらに役に立ちます。 数百個のファイルをファイル名、サムネールおよびメモリだけに基づいて管理することは可能です。ただし、関与する人数が多く、管理されるアセットの数が増える場合、このアプローチは拡張性に欠けます。 さらに、デジタルアセットの価値は、アセットが次のように増大します。

* アクセスが容易になる - システムやユーザーが簡単に見つけることができます。
* 管理が容易 – 同じプロパティのセットを持つアセットを簡単に見つけて、変更を適用できます。
* 完了 – アセットには、より多くの情報とコンテキストが含まれます。

## アセットのプロパティの表示 {#properties-ui}

アセットを使用、共有またはダウンロードする前に、より詳細に表示できます。プレビュー機能を使用すると、画像だけでなく、サポートされているその他のアセットタイプも表示できます。 アセットを表示できるだけでなく、詳細情報を表示したり、その他のアクションを実行したりできます。 アセットの情報を表示するには、アセットに移動するか、 [検索](search-assets.md) アセットをクリックしてプロパティを開きます。 次の図は、アセットのプロパティページで使用できるフィールドを示しています。

![アセット UI のプロパティ](assets/properties-ui.png)

* **回答：** アセットのタイトル
* **B:** ズームインまたはズームアウトして、アセットをより近くにズームまたはプレビューする割合
* **C:** 前に選択したパーセンテージへのズームを取り消す
* **D:** 前または次のアセットに進む
* **E:** Assets数
* **F:** アセットのダウンロード
* **G:** を使用したアセットの編集 [!DNL Adobe Express]
* **H:** アセットの情報の折りたたみまたはプレビュー
* **I:** アセットの共有
* **J:** アセットを追加： [!DNL Collection]
* **K:** プレビュー画面を閉じる
* **L:** タイトル、形式、サイズ、解像度、タグ、カラータグ、スマートタグを含む、アセットの情報。

## サポートされるファイル形式 {#supported-formats}

次の表に、でサポートされるファイル形式を示します [!DNL the Content Hub]:

<table> 
    <tbody>
     <tr>
      <th><strong>ファイルタイプ</strong></th>
      <th><strong>サポートされるファイル形式</strong></th>
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
            <li>[!UICONTROL txt] （プレーン）</li>  
            <li>[!UICONTROL Doc/Docx]</li> 
            <li>[!UICONTROL XML]</li>
        </ul>
      </td>
     </tr>
     <tr>
      <td>印刷メディア</td>
      <td>
        <ul>
            <li>[!UICONTROL PDF]</li>  
        </ul>
      </td>
     </tr>  
    </tbody>
   </table>

### アセットのアップロード後の派生プロパティ {#derived-properties}

アセットをアップロードすると、Content Hubによって、自動生成されるプロパティがいくつか派生します。 その一部を次に示します。

* **サイズ：** サイズは、アセットの論理値をディメンションごとに示します。 これにより、アセットがリポジトリ内で取得しているスペースが明確になります。 [!DNL The Content Hub] は最大 2GB のアセットをサポートします。

<!--* **Tags:** Tags help you categorize assets that can be browsed and searched more efficiently. Tagging helps in propagating the appropriate taxonomy to other users and workflows. -->

* **スマートタグ：** [!DNL The Content Hub] は、Adobe Senseiのスマートコンテンツサービスを使用して、タグベースの構造上の認識アルゴリズムを使用してアセットのトレーニングを行います。 その後、このコンテンツインテリジェンスを使用して、アセットの個々のセットに関連性の高いタグが適用されます。スマートタグを使用すると、関連するアセットをすばやく見つけることができるので、プロジェクトのコンテンツベロシティ（コンテンツ創出の速度）が向上します。 スマートタグは、画像に含まれないアセット情報の例です。 [!DNL The Content Hub] は、デフォルトでスマートタグをアセットに自動的に適用します。

* **カラータグ：** [カラータグ](#https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/color-tag-images.html?lang=en) は、AdobeのSensei AI 機能を使用してアセット内で自動的に識別されるカラーを使用して、アセットを認識するのに役立ちます。

* アップロード日

* アップロード実行者

* 最終変更日

* 最終変更者

Content Hubにアセットを追加する際に指定するプロパティもあります。 詳しくは、を参照してください [ブランド承認済みアセットのContent Hubへの追加](upload-brand-approved-assets.md). これらのプロパティは、アセットプロパティページにも表示されます。

管理者は、各アセットに表示されるプロパティを設定することもできます。 詳しくは、を参照してください [Content Hub ユーザーインターフェイスの設定](configure-content-hub-ui-options.md#configure-asset-details-content-hub).

<!--

### Date range {#date-range} 

The date range allows you to select dates you want to see the assets. You can customize date range by choosing the start and end dates. 

-->

