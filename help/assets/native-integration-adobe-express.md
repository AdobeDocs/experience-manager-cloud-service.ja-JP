---
title: AEM AssetsとAdobe Expressのネイティブ統合
description: AEM AssetsとAdobe Expressのネイティブ統合により、Adobe Expressのユーザーインターフェイス内から、AEM Assetsに保存されているアセットに直接アクセスできます。
exl-id: d43e4451-da2a-444d-9aa4-4282130ee44f
source-git-commit: 69d890eaae30468db89b9aff975a2a421f53fcff
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 25%

---

# Adobe Expressとのネイティブ統合 {#native-integration-adobe-express}

AEM Assets は Adobe Express とネイティブに統合されているので、Adobe Express ユーザーインターフェイス内から AEM Assets に保存されているアセットに直接アクセスできます。AEM Assets で管理されているコンテンツを Express キャンバスに配置し、新しいコンテンツや編集したコンテンツを AEM Assets リポジトリに保存できます。この統合には、次のような主なメリットがあります。

* AEMで新しいアセットを編集および保存することで、コンテンツの再利用を促進しました。

* 新しいアセットを作成したり、既存のアセットの新しいバージョンを作成したりする全体的な時間と労力を削減します。

## 前提条件 {#prerequisites}

Adobe ExpressおよびAEM Assets内の 1 つ以上の環境にアクセスするための権限。 環境は、Assets as a Cloud Service または Assets Essentials 内の任意のリポジトリでも構いません。


## Adobe Express エディターでの AEM Assets の使用 {#use-aem-assets-in-express}

Adobe ExpressエディターでAEM Assetsの使用を開始するには、次の手順を実行します。

1. Adobe Express web アプリケーションを開きます。

2. 新しいテンプレートまたはプロジェクトを読み込むか、アセットを作成して、新しい空のキャンバスを開きます。

3. クリック **[!UICONTROL アセット]** 左側のナビゲーションウィンドウで使用できます。 Adobe Expressには、アクセス権のあるリポジトリのリストと、ルートレベルで使用可能なアセットおよびフォルダーのリストが表示されます。

4. リポジトリーのアセットを参照または検索して、キャンバスにドラッグ&amp;ドロップします。 使用可能な様々なフィルター（ファイルタイプ、MIME タイプ、ディメンションなど）を使用してアセットをフィルタリングできます。

   >[!NOTE]
   >
   >ディメンションによるフィルターがビデオに適用されない。

   ![Assets アドオンからアセットを含める](assets/adobe-express-native-integration.png)


## AEM Assets での Adobe Express プロジェクトの保存 {#save-express-projects-in-assets}

Express キャンバスに適切な変更を組み込んだ後、AEM Assets リポジトリに保存できます。

1. クリック **[!UICONTROL 共有]** を開きます **[!UICONTROL 共有]** ダイアログ。

   ![AEM でのアセットの保存](assets/adobe-express-share.png)

2. 右側のペインの「ストレージ」セクションから、次の項目を選択します。 **AEM Assets**. Adobe Expressにはアップロードダイアログが表示されます。
3. アセットの名前と形式を指定します。キャンバスのコンテンツは、PNG、JPEG、PDF、MP4、MP4+PNG、MP4+JPEG形式で保存できます。 形式は、アセットに基づいて自動的に調整されます。

   >[!NOTE]
   >
   >「現在のページ」を選択すると、ファイルが保存先フォルダーに保存されます。 「すべてのページ」を選択すると、すべての非PDFファイルの新しいフォルダが作成され、PDFファイルが 1 つのファイルとして保存先フォルダに保存されます。

4. の下のテキスト領域をクリックします **宛先フォルダー** をクリックして場所を選択し、アセットを保存します。

   ![AEM でのアセットの保存](/help/assets/assets/page-selection-and-destination-folder.png)

5. オプション：アップロードに使用するキャンペーンメタデータを **プロジェクト名またはキャンペーン名** フィールド。 既存の名前を使用することも、新しい名前を作成することもできます。 アップロードに複数のプロジェクト名またはキャンペーン名を定義できます。 名前を登録するには、名前を入力して Enter キーを押します。
ベストプラクティスとして、Adobeでは残りのフィールドに値を指定し、アップロードしたアセットの検索エクスペリエンスを強化することをお勧めします。

6. 同様に、の値を定義します **[!UICONTROL キーワード]** および **[!UICONTROL チャネル]** フィールド。

7. 「**[!UICONTROL アップロード]**」をクリックして、AEM Assets にアセットをアップロードします。




## 制限事項 {#limitations}

1. 読み込みと書き出しでサポートされるビデオファイルのタイプは MP4 です。

2. MP4 ビデオの読み込みの場合：

   a）サポートされている最大ファイルサイズは 200 MB です。 この制限を超えると、アラートメッセージが表示されます。
b）サポートされている最大解像度は 3840 X 3840 ピクセルです。
c）背景が透明なビデオ（アルファチャンネル）はサポートされていません。

3. MP4 ビデオの書き出しの場合：

   a）サポートされている最大ファイルサイズは 200 MB です。 この制限を超えると、次の画像に示すように、アラートメッセージに回避策の提案が表示されます
   ![アラートと回避策](/help/assets/assets/alert-with-workaround.png).
