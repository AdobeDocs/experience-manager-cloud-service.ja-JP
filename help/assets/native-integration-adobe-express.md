---
title: AEM Assets と Adobe Express とのネイティブ統合
description: AEM Assets と Adobe Express とのネイティブ統合を使用すると、Adobe Express ユーザーインターフェイス内から AEM Assets に保存されているアセットに直接アクセスできます。
exl-id: d43e4451-da2a-444d-9aa4-4282130ee44f
feature: Collaboration
role: User
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '681'
ht-degree: 95%

---

# Adobe Express とのネイティブ統合 {#native-integration-adobe-express}

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

AEM Assets は Adobe Express とネイティブに統合されているので、Adobe Express ユーザーインターフェイス内から AEM Assets に保存されているアセットに直接アクセスできます。AEM Assets で管理されているコンテンツを Express キャンバスに配置し、新しいコンテンツや編集したコンテンツを AEM Assets リポジトリに保存できます。この統合には、次のような主なメリットがあります。

* AEM での新しいアセットの編集と保存による、コンテンツ再利用の増加。

* 新しいアセットの作成や、既存のアセットの新しいバージョンの作成にかかる全体的な時間と労力の削減。

## 前提条件 {#prerequisites}

AEM Assets 内の Adobe Express と 1 つ以上の環境にアクセスする権限。環境は、Assets as a Cloud Service または Assets Essentials 内の任意のリポジトリでも構いません。


## Adobe Express エディターでの AEM Assets の使用 {#use-aem-assets-in-express}

Adobe Express エディターで AEM Assets の使用を開始するには、次の手順を実行します。

1. Adobe Express web アプリケーションを開きます。

2. 新しいテンプレートまたはプロジェクトを読み込むか、アセットを作成して、新しい空のキャンバスを開きます。

3. 左側のナビゲーションパネルで「**[!UICONTROL アセット]**」をクリックします。Adobe Express には、アクセス権が付与されたリポジトリのリストとルートレベルで使用可能なアセットおよびフォルダーのリストが表示されます。

4. リポジトリのアセットを参照または検索し、キャンバスにドラッグ＆ドロップします。ファイルタイプ、MIME タイプ、ディメンションなど、使用可能な様々なフィルターを使用してアセットをフィルタリングできます。

   >[!NOTE]
   >
   >ディメンションによるフィルターは、ビデオには適用されません。

   ![Assets アドオンからアセットを含める](assets/adobe-express-native-integration.png)


## AEM Assets での Adobe Express プロジェクトの保存 {#save-express-projects-in-assets}

Express キャンバスに適切な変更を組み込んだ後、AEM Assets リポジトリに保存できます。

1. 「**[!UICONTROL 共有]**」をクリックして、**[!UICONTROL 共有]**&#x200B;ダイアログを開きます。

   ![AEM でのアセットの保存](assets/adobe-express-share.png)

2. 右側のパネルの「ストレージ」セクションから、「**AEM Assets**」を選択します。Adobe Express にアップロードダイアログが表示されます。
3. 「**現在のページ**」または「**すべてのページ**」を選択します。書き出すアセットの名前と形式を指定します。キャンバスのコンテンツは、PNG、JPEG、PDF、MP4、MP4+PNG、または MP4+JPEG 形式で書き出すことができます。形式は、キャンバスページのアセットに基づいて自動的に調整されます。
「**現在のページ**」を選択すると、現在のページのアセットが宛先フォルダーに保存されます。「**すべてのページ**」を選択し、書き出す形式が PDF でない場合、すべてのキャンバスページは、宛先フォルダー内の新しいフォルダーに個別のファイルとして保存されます。書き出す形式が PDF の場合、すべてのキャンバスページが 1 つの PDF ファイルとして宛先フォルダーに保存されます。

4. **宛先フォルダー**&#x200B;の下にあるフォルダーアイコンをクリックして場所を選択し、アセットを保存します。

   ![AEM でのアセットの保存](/help/assets/assets/page-selection-and-destination-folder.svg)

5. オプション：「**プロジェクトまたはキャンペーン名**」フィールドを使用して、アップロード用のキャンペーンメタデータを追加できます。既存の名前を使用するか、新しい名前を作成できます。アップロードには、複数のプロジェクト名またはキャンペーン名を定義できます。名前を登録するには、名前を入力して Enter キーを押すだけです。
ベストプラクティスとして、アドビでは、アップロードしたアセットの検索エクスペリエンスを強化すると共に、残りのフィールドに値を指定することをお勧めします。

6. 同様に、「**[!UICONTROL キーワード]**」フィールドと「**[!UICONTROL チャネル]**」フィールドの値を定義します。

7. 「**[!UICONTROL アップロード]**」をクリックして、AEM Assets にアセットをアップロードします。

## 制限事項 {#limitations}

1. 読み込みと書き出しの場合、サポートされるビデオファイルのタイプは MP4 です。

2. MP4 ビデオの読み込みの場合：

   1. サポートされる最大ファイルサイズは 200 MB です。この制限を超えると、アラートメッセージが表示されます。
   2. サポートされる最大解像度は 3840 X 3840 ピクセルです。
   3. 透明な背景（アルファチャンネル）のビデオはサポートされません。

3. MP4 ビデオの書き出しの場合：

   1. サポートされる最大ファイルサイズは 200 MB です。この制限を超えると、ビデオを 200 MB 以下にトリミングするか、ダウンロード後に AEM Assets の宛先フォルダーに手動でアップロードすることを提案するアラートが表示されます。



