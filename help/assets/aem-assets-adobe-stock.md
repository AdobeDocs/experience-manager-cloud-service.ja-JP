---
title: AEM Assets での Adobe Stock デジタルアセットの使用
description: Adobe Experience Manager で Adobe Stock アセットを検索、取得、ライセンス、管理します。ライセンスされたアセットをその他の Adobe Experience Manager アセットとして扱います。
contentOwner: AG
translation-type: tm+mt
source-git-commit: b0436c74389ad0b3892d1258d993c00aa470c3ab
workflow-type: tm+mt
source-wordcount: '1132'
ht-degree: 97%

---


# AEM Assets での Adobe Stock アセットの使用 {#use-adobe-stock-assets-in-aem-assets}

Adobe Stock エンタープライズプランと AEM Assets を統合すると、AEM の強力なアセット管理機能を使用して、ライセンスが必要なアセットをクリエイティブプロジェクトやマーケティングプロジェクトに幅広く活用できます。

Adobe Stock サービスは、あらゆるクリエイティブプロジェクトに使用できる、適切にキュレーションされ、著作権使用料が不要で質の高い何百万点もの写真、ベクター、イラスト、ビデオ、テンプレートおよび 3D アセットを提供します。AEM に保存されている Adobe Stock アセットの検出、プレビューおよびライセンスの取得を、AEM Workspace 内からすばやく実行できます。

## AEM と Adobe Stock の統合 {#integrate-aem-and-adobe-stock}

AEM と Adobe Stock の間でやり取りができるようにするには、AEM 内で IMS 設定と Adobe Stock 設定を作成します。

>[!NOTE]
>
>統合は、組織の AEM 管理者と Admin Console 管理者のみ実行できます。統合の実行には管理者権限が必要です。

### IMS 設定の作成 {#create-an-ims-configuration}

1. AEM のロゴをクリックします。**[!UICONTROL ツール]**／**[!UICONTROL セキュリティ]**／**[!UICONTROL Adobe IMS 設定]**&#x200B;に移動します。「**[!UICONTROL 作成]**」をクリックし、**[!UICONTROL クラウドソリューション]**／**[!UICONTROL Adobe Stock]** を選択します。
1. 既存の証明書を再使用するか、「**[!UICONTROL 新しい証明書を作成]**」を選択します。
1. 「**[!UICONTROL 証明書を作成]**」をクリックします。証明書を作成したら、公開鍵をダウンロードします。「**[!UICONTROL 次へ]**」をクリックします。
1. 「**[!UICONTROL タイトル]**」、「**[!UICONTROL 認証サーバー]**」、「**[!UICONTROL API キー]**」、「**[!UICONTROL クライアントの秘密鍵]**」および「**[!UICONTROL ペイロード]**」の各フィールドに適切な値を指定します。See [JWT authentication quick start](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md), for detailed information to fetch these values from Adobe Developer Console.
1. ダウンロードし追加た公開鍵をAdobe Developer Consoleサービスアカウントにダウンロードします。

<!--
TBD: Update this instance when AIO updates their documentation publish URL.
-->

### AEM での Adobe Stock 設定の作成 {#create-adobe-stock-configuration-in-aem}

1. AEM ユーザーインターフェイスで、**[!UICONTROL ツール]**／**[!UICONTROL クラウドサービス]**／**[!UICONTROL Adobe Stock]** に移動します。
1. 「**[!UICONTROL 作成]**」をクリックして設定を作成し、その設定を既存の IMS 設定に関連付けます。環境パラメーターとして「`PROD`」を選択します。
1. 「**[!UICONTROL ライセンスが必要なアセットのパス]**」フィールドの場所をそのまま残します。この場所を Adobe Stock アセットを保存する場所に変更しないでください。
1. すべての必須プロパティを追加して作成を完了します。「**[!UICONTROL 保存して閉じる]**」をクリックします。
1. アセットのライセンスを取得できる AEM ユーザーまたはグループを追加します。

>[!NOTE]
>
>複数の Adobe Stock 設定がある場合は、AEM ユーザーインターフェイスで AEM のロゴをクリックして、[!UICONTROL ユーザーの環境設定]パネルで目的の設定を選択します。

## AEM での Adobe Stock アセットの使用と管理 {#usemanage}

この機能を使用すると、AEM Assets で Adobe Stock アセットを操作できます。AEM のユーザーインターフェイス内から Adobe Stock アセットを検索し、必要なアセットのライセンスを取得できます。

AEM 内で Adobe Stock アセットのライセンスを取得すると、そのアセットを通常のアセットと同様に使用および管理できます。ユーザーは AEM 内でアセットの検索およびプレビュー、アセットのコピーおよび公開、Brand Portal でのアセットの共有、AEM デスクトップアプリケーション経由でのアセットのアクセスおよび使用をおこなうことができます。

<!--  ![Search for Adobe Stock assets and filter results from your AEM workspace](assets/adobe-stock-search-results-workspace.png)
*Figure: Search for Adobe Stock assets and filter results from your AEM workspace* -->

**A.** 指定された Adobe Stock ID のアセットと類似しているアセットを検索します。**B.** 選択した形状や向きと一致するアセットを検索します。**C.** サポートされているアセットタイプのいずれかを検索します。**D.** フィルターウィンドウを開く／折りたたみます。**E.** 選択したアセットのライセンスを取得して AEM に保存します。**F.** アセットを透かし付きで AEM に保存します。**G.** 選択したアセットと類似したアセットを Adobe Stock Web サイトで調べます。**H.** 選択したアセットを Adobe Stock Web サイトに表示します。**I.** 検索結果から選択したアセットの数。**J.** カード表示とリスト表示を切り替えます。

### アセットの検索 {#find-assets}

AEM と Adobe Stock の両方でアセットを検索できます。検索場所を Adobe Stock に限定しない場合は、AEM と Adobe Stock からの検索結果が表示されます。

* Adobe Stock アセットを検索するには、**[!UICONTROL ナビゲーション]**／**[!UICONTROL アセット]**／**[!UICONTROL Adobe Stock を検索]**&#x200B;をクリックします。

* Adobe Stock と AEM Assets をまたいでアセットを検索するには、検索アイコン ![検索アイコン](assets/do-not-localize/search_icon.png) をクリックします。

また、Adobe Stock アセットを選択するには、検索バーに「`Location: Adobe Stock`」と入力します。AEM は、検索されたアセットに対する高度なフィルタリング機能を備えており、サポートされているアセットのタイプや画像の向き、ライセンスの状態などのフィルターを使用して、必要なアセットをすばやく見つけることができます。

>[!NOTE]
>
>Adobe Stock から検索されたアセットは AEM に表示されるだけです。[アセットを保存](/help/assets/aem-assets-adobe-stock.md#saveassets)するか、[アセットのライセンスを付与された](/help/assets/aem-assets-adobe-stock.md#licenseassets)後でないと、Adobe Stock アセットを取得して AEM リポジトリに保存することはできません。既に AEM に保存されているアセットが表示され、参照やアクセスが簡単にできるようにハイライトされます。また、これらのアセットは、ソースが Adobe Stock であることを示すいくつかの追加メタデータとともに保存されます。

![AEM の検索フィルターと、検索結果内でハイライトされている Adobe Stock アセット](assets/aem-search-filters2.jpg)*図：AEM の検索フィルターと、検索結果内でハイライトされている Adobe Stock アセット*

### 必要なアセットの保存と表示 {#saveassets}

AEM に保存するアセットを選択します。上部ツールバーの「保存」をクリックし、アセットの名前と保存場所を指定します。ライセンスが不要なアセットはローカルに透かし付きで保存されます。

アセットの検索を次回実行すると、保存済みのアセットは、AEM Assets で使用可能であることを示すバッジ付きでハイライトされます。

>[!NOTE]
>
>最近追加されたアセットには、ライセンスが許諾されていることを示すバッジではなく、新しいアセットであることを示すバッジが表示されます。

### アセットのライセンス取得 {#licenseassets}

Adobe Stock エンタープライズプランの割り当てを使用することで、Adobe Stock アセットのライセンスを取得できます。ライセンスを許諾されたアセットは透かしなしで保存され、AEM Assets で検索することも使用することも可能になります。

![Adobe Stock アセットのライセンスを取得してアセットを AEM Assets に保存するためのダイアログ](assets/aem-stock_licenseandsave.jpg)*図：Adobe Stock アセットのライセンスを取得してアセットを AEM Assets に保存するためのダイアログ*

### メタデータおよびアセットプロパティへのアクセス {#access-metadata-and-asset-properties}

メタデータ（AEM に保存されているアセットの Adobe Stock メタデータプロパティを含む）にアクセスしてプレビューし、アセットの&#x200B;**[!UICONTROL ライセンス参照]**&#x200B;を追加できます。ただし、ライセンス参照の更新は AEM と Adobe Stock Web サイトの間で同期されません。

ユーザーは、ライセンスを許諾されたアセットとライセンスを許諾されていないアセットの両方を表示できます。

![保存されているアセットのメタデータとライセンス参照の表示およびアクセス](assets/metadata_properties.jpg)*図：保存されているアセットのメタデータとライセンス参照の表示およびアクセス*

## 既知の制限事項 {#known-limitations}

### 編集用画像であることを示す警告が表示されない

画像のライセンスを取得する際に、画像が編集用であるかどうかを確認できません。管理者は誤用を防ぐために、Admin Console から編集用アセットへのアクセスをオフにできます。

### 間違ったライセンスタイプが表示される

アセットに関して、AEM に間違ったライセンスタイプが表示されることがあります。Adobe Stock Web サイトにログインすると、ライセンスタイプを確認できます。

### 参照フィールドとメタデータが同期しない

ライセンス参照フィールドを更新すると、ライセンス参照情報が AEM には反映されますが、Adobe Stock Web サイトには反映されません。同様に、Adobe Stock Web サイトで参照フィールドを更新すると、更新情報が AEM には反映されません。

## 関連リソース {#related-resources}

[AEM Assets での Adobe Stock アセットの使用について説明するビデオチュートリアル](https://helpx.adobe.com/jp/experience-manager/kt/assets/using/stock-assets-feature-video-use.html)

[Adobe Stock エンタープライズプランのヘルプ](https://helpx.adobe.com/jp/enterprise/using/adobe-stock-enterprise.html)

[Adobe Stock の FAQ](https://helpx.adobe.com/jp/stock/faq.html)
