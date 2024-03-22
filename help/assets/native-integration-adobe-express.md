---
title: AEM AssetsとAdobe Expressのネイティブ統合
description: AEM AssetsのAdobe Expressとのネイティブ統合により、Adobe Assets のユーザーインターフェイス内からAEM Assetsに保存されたAdobe Expressに直接アクセスできます。
exl-id: d43e4451-da2a-444d-9aa4-4282130ee44f
source-git-commit: 8bbf9a2ba8f708a5a03d11bc0388d39b32d4c7b3
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 34%

---

# Adobe Expressとのネイティブ統合 {#native-integration-adobe-express}

AEM Assetsは、Adobe Expressとネイティブに統合され、Adobe Expressユーザーインターフェイス内からAEM Assetsに保存されたアセットに直接アクセスできます。 AEM Assets で管理されているコンテンツを Express キャンバスに配置し、新しいコンテンツや編集したコンテンツを AEM Assets リポジトリに保存できます。統合の主なメリットは次のとおりです。

* AEMでの新しいアセットの編集と保存により、コンテンツの再利用が促進されました。

* 新しいアセットを作成したり、既存のアセットの新しいバージョンを作成したりする際の、全体的な時間と労力を削減しました。

## 前提条件 {#prerequisites}

AEM Assets内のAdobe Expressと 1 つ以上の環境にアクセスする権限。 環境は、Assets as a Cloud Service または Assets Essentials 内の任意のリポジトリでも構いません。


## Adobe Express エディターでの AEM Assets の使用 {#use-aem-assets-in-express}

Adobe ExpressエディターでAEM Assetsの使用を開始するには、次の手順を実行します。

1. Adobe Express web アプリケーションを開きます。

1. 新しいテンプレートまたはプロジェクトを読み込むか、アセットを作成して、新しい空のキャンバスを開きます。

1. クリック **[!UICONTROL Assets]** は、左側のナビゲーションペインで使用できます。 Adobe Expressには、アクセス権が付与されたリポジトリーのリストと、ルートレベルで使用可能なアセットおよびフォルダーのリストが表示されます。

1. リポジトリー内のアセットを参照または検索して、キャンバスにドラッグ&amp;ドロップします。 使用可能な様々なフィルター（ファイルタイプ、MIME タイプ、ディメンションなど）を使用して、アセットをフィルタリングできます。

   ![Assets アドオンからアセットを含める](assets/adobe-express-native-integration.png)


## AEM Assets での Adobe Express プロジェクトの保存 {#save-express-projects-in-assets}

Express キャンバスに適切な変更を組み込んだ後、AEM Assets リポジトリに保存できます。

1. クリック **[!UICONTROL 共有]** 開く **[!UICONTROL 共有]** ダイアログ。

   ![AEM でのアセットの保存](assets/adobe-express-share.png)

1. 選択 **[!UICONTROL AEM Assets]** から **[!UICONTROL ストレージ]** セクションが右側のウィンドウに表示されます。 Adobe Expressにアップロードダイアログが表示されます。
1. アセットの名前と形式を指定します。キャンバスのコンテンツは、PNG 形式または JPEG 形式で保存できます。

1. 「**[!UICONTROL 場所]**」フィールドの横にあるフォルダーアイコンをクリックして、アセットを保存する必要がある場所に移動し、「**[!UICONTROL 選択]**」をクリックします。フォルダーの名前が「**[!UICONTROL 場所]**」フィールドに表示されます。

   ![AEM でのアセットの保存](assets/adobe-express-upload.png)

1. オプション： **[!UICONTROL プロジェクト名またはキャンペーン名]** フィールドに入力します。 既存の名前を使用するか、新しい名前を作成することができます。 アップロード用に複数のプロジェクト名またはキャンペーン名を定義できます。 名前を入力する際に、ダイアログボックス内の他の場所をクリックするか、 `,` （コンマ）キーを使用して名前を登録します。

   ベストプラクティスとして、Adobeは、残りのフィールドに値を指定すると共に、アップロードしたアセットの検索機能が強化されます。
1. 同様に、 **[!UICONTROL キーワード]** および **[!UICONTROL チャネル]** フィールド。

1. 「**[!UICONTROL アップロード]**」をクリックして、AEM Assets にアセットをアップロードします。




## 制限事項 {#limitations}

複数のリポジトリーのアセットを含むドキュメントを保存する際に、複数の Assets リポジトリーにアクセスできる一部のユーザーが発生する既知のバグがあります。
