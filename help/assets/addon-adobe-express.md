---
title: Adobe Express用AEM Assetsアドオン
description: AEM Assets add-on for AEM Assetsを使用すると、Adobe Expressユーザーインターフェイス内からAdobe Expressに保存されているアセットに直接アクセスできます。
exl-id: d43e4451-da2a-444d-9aa4-4282130ee44f
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 0%

---

# Adobe Express用AEM Assetsアドオン {#assets-addon-adobe-express}

AEM Assets add-on for AEM Assetsを使用すると、Adobe Expressユーザーインターフェイス内からAdobe Expressに保存されているアセットに直接アクセスできます。 AEM Assetsで管理するコンテンツを Express キャンバスに配置し、新しいコンテンツや編集したコンテンツをAEM Assetsリポジトリに保存できます。 このアドオンには、次の主なメリットがあります。

* AEMでの新しいアセットの編集と保存によるコンテンツの再利用の向上

* 新しいアセットを作成したり、既存のアセットの新しいバージョンを作成したりする際の全体的な時間と労力を削減

## 前提条件 {#prerequisites}

AEM Assets内のAdobe Expressと 1 つ以上の環境にアクセスする権限。 環境は、Assets 内の任意のリポジトリーまたはas a Cloud ServiceAssets Essentialsです。


## AEM AssetsアドオンをAdobe Expressに追加 {#access-assets-addon}

次の手順を実行して、AEM AssetsアドオンをAdobe Expressに追加します。

1. Adobe ExpressWeb アプリケーションを開きます。

1. 新しいテンプレートやプロジェクトを読み込むか、アセットを作成して、新しい空のキャンバスを開きます。

1. クリック **[!UICONTROL アドオン]** は、左側のナビゲーションペインで使用できます。

1. 指定 **[!UICONTROL AEM Assets]** 」で、 [!UICONTROL アドオン] 「 」セクションに移動して、「 AEM Assetsアドオン」をクリックします。

   ![AEM Assetsアドオン](assets/aem-assets-add-on.png)

1. 「**[!UICONTROL 追加]**」をクリックします。アドオンは、 **[!UICONTROL アドオン]** 」セクションに入力します。 もう一度アドオンをクリックすると、右側のナビゲーションウィンドウにコンテンツが表示されます。 アドオンには、アクセス権が付与されたリポジトリのリストと、ルートレベルで使用可能なアセットおよびフォルダーのリストが表示されます。

   検索バーを使用して、キャンバスで使用する必要があるアセットを検索します。

   ![AEM Assetsアドオンでのアセットの検索](assets/assets-add-on-browse-assets.png)

   A. AEM Assetsリポジトリを選択します。B.検索バーを使用してアセットを検索します。C.アセットを昇順または降順で並べ替えます。D.選択した場所で使用可能なアセットとフォルダー。 E. AEM Assetsに変更を保存します。



## Adobe ExpressエディターでのAEM Assetsの使用 {#use-aem-assets-in-express}

Adobe ExpressにAEM Assetsアドオンを追加した後、Express キャンバス内のAEM Assetsリポジトリに保存されている PNG 画像とJPEG画像を使用し始めることができます。 適切なフォルダーに移動し、アセットをクリックしてキャンバスに含めます。

![Assets アドオンのアセットを含める](assets/aem-assets-add-on-include-assets.png)


## AEM AssetsでのAdobe Expressプロジェクトの保存 {#save-express-projects-in-assets}

Express キャンバスに適切な変更を組み込んだ後、AEM Assetsリポジトリに保存できます。

1. クリック **[!UICONTROL 保存]** 開く **[!UICONTROL アップロード]** ダイアログ。
1. アセットの名前と形式を指定します。 キャンバスのコンテンツは、PNG 形式またはJPEG形式で保存できます。

1. の横にあるフォルダーアイコンをクリックします。 **[!UICONTROL 場所]** フィールドで、アセットを保存する場所に移動し、 **[!UICONTROL 選択]**. フォルダーの名前が **[!UICONTROL 場所]** フィールドに入力します。

1. クリック **[!UICONTROL アップロード]** をクリックして、AEM Assetsにアセットをアップロードします。

   ![AEMでのアセットの保存](assets/aem-assets-add-on-save.png)
