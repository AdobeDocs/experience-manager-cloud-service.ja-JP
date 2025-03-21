---
title: Creative Cloud 統合のコンテンツ自動処理
description: Creative Cloud 統合を使用したアセットバリエーションの生成
contentOwner: AG
feature: Upload, Asset Processing, Publishing, Asset Compute Microservices
role: User, Admin
exl-id: 4cff355e-d12c-44c7-b519-4cc37f49e396
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 96%

---

# [!DNL Adobe Creative Cloud] 統合を使用したアセットバリエーションの生成 {#content-automation}

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

コンテンツ自動処理アドオンは、[!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] API と [!DNL Adobe Creative Cloud] API を統合して、大規模なアセットをクリエイティブに処理します。[!DNL Experience Manager] では、クラウドベースの[アセットマイクロサービス](/help/assets/asset-microservices-overview.md)を利用して、[!DNL Adobe Creative Cloud] 機能を使用し、アセットの作成とメディアの処理を自動化します。

[!DNL Adobe Photoshop] と [!DNL Adobe Lightroom] のアセットを編集する場合、[!DNL Experience Manager Assets] からアセットをダウンロードして編集して、再度アップロードする必要はありません。[!DNL Experience Manager] で処理プロファイルを作成および設定し、そのプロファイルをフォルダーに適用して、そのフォルダーにアセットをアップロードします。アップロードしたアセットは、処理プロファイルに基づいて再処理され、これらのアセットのバリエーションが得られます。一貫した手間のかからない一括処理により、手作業が不要になるのでコンテンツの作成速度が向上し、しかも優れたクリエイティブスキルを必要としません。また、開発者とパートナーは、これらの API に直接アクセスしてアセットマイクロサービスを拡張し、カスタムロジックを組み込むこともできます。

ユーザーは、処理プロファイルを作成して、アセットに対する次のクリエイティブな操作を自動化できます。

* **自動トーン**：人工知能を利用して画像の内容を分析し、画像の固有の属性に基づいて光と色の補正をインテリジェントに行います。

* **自動アップライト**：人工知能を利用して、画像の内容を分析し画像のゆがみを修正します。例えば、平らな水平面を作成する場合などです。

  ![自動トーン](/help/assets/assets/content-automation-autotone.png)

  *図：ゆがんだ画像の改善に役立つ自動トーンと自動補正*

* **Lightroom プリセット**：カスタムのプリセットを使用して、ユーザー定義の外観を画像に適用し、一貫した外観を実現します。

  ![Lightroom プリセット](/help/assets/assets/content-automation-lrpresets.png)

  *図：多くの画像に対して一貫した方法で画質を改善する Adobe Lightroom プリセット*

* **画像カットアウト**：人工知能を利用して、1 つのコマンドで、目立つオブジェクトを囲む選択範囲を作成し、その背景を削除します。

  ![写真からの画像の切り取りと背景の削除](/help/assets/assets/content-automation-backgroundremove.png)

* **画像マスク**：人工知能を利用して、1 つのコマンドで、目立つオブジェクトを囲むマスクを作成します。

  ![AI を使用した画像のマスク](/help/assets/assets/content-automation-mask.png)

* **Photoshop のアクション**：一連の [!DNL Adobe Photoshop] タスクをファイルまたはファイル群に適用します。

  ![Photoshop のアクション](/help/assets/assets/content-automation-psactions.png)

* **スマートオブジェクト置換**：PSD ファイル内で適用されたすべてのエフェクトと調整を維持しながら画像を入れ替えることができるので、大規模なパーソナライゼーションを実行できます。

  ![オブジェクトのスマートな置換](/help/assets/assets/content-automation-objectreplace.png)

## AEM as a Cloud Service プログラムのコンテンツ自動化の有効化 {#enable-content-automation}

Cloud Manager を使用して AEM as a Cloud Service プログラムのコンテンツ自動化アドオンを有効にするには：

1. アカウント担当者に連絡して、コンテンツ自動化アドオンのライセンスを取得します。
1. Cloud Manager にアクセスし、組織セレクターを使用して所属先の組織に切り替えます。
1. 「**[!UICONTROL プログラムを追加]**」をクリックし、プログラム名を指定します。
1. 「**[!UICONTROL 続行]**」をクリックします。
1. 「**[!UICONTROL アセット]**」を展開し、「**[!UICONTROL コンテンツ自動化]**」を選択します。
1. 「**[!UICONTROL 作成]**」をクリックします。
1. パイプラインを実行して、[変更内容を Cloud Manager にデプロイ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html?lang=ja)します。

Cloud Manager の既存の AEM as a Cloud Service プログラムにコンテンツ自動化アドオンを追加する必要がある場合：

1. プログラムカードで「...」をクリックします。

1. 「**[!UICONTROL プログラムを編集]**」を選択したあと、「**[!UICONTROL ソリューションとアドオン]**」タブを選択します。

1. 「**[!UICONTROL アセット]**」を展開し、「**[!UICONTROL コンテンツ自動化]**」を選択します。
1. 「**[!UICONTROL 更新]**」をクリックします。
1. パイプラインを実行して、[変更内容を Cloud Manager にデプロイ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html?lang=ja)します。

## 処理プロファイルを使用したクリエイティブアセットの一括編集 {#process-assets}

処理プロファイルを使用してバリエーションを自動的に作成するには、次の手順に従います。

1. **[!UICONTROL ツール]**／**[!UICONTROL アセット]**／**[!UICONTROL 処理プロファイル]**&#x200B;に移動します。

1. 「**[!UICONTROL 作成]**」を選択し、「**[!UICONTROL 名前]**」を指定します。

1. 「**[!UICONTROL クリエイティブ]**」タブを選択し、出力フォルダーを指定したあと、「**[!UICONTROL 新規追加]**」を選択してクリエイティブ設定を追加します。

1. 「**[!UICONTROL レンディション名]**」（出力名）と「**[!UICONTROL 拡張子]**」（ファイルタイプ）を指定し、「**[!UICONTROL 画質]**」（出力パラメーター）を選択し、MIME タイプの「**[!UICONTROL 次を含む]**」および「**[!UICONTROL 除外]**」リスト（入力アセットフィルター）を選択したあと、必要なクリエイティブ操作を選択します。

   ![[!UICONTROL クリエイティブ]タブ：[!UICONTROL 処理プロファイル]](assets/creative-processing-profile.png)

1. 一部の操作には、追加のパラメーター（アセット）が必要です。必要に応じて、これらの追加パラメーターの値を指定します。

1. 同じ処理プロファイルの一部として、さらにクリエイティブ操作を追加するか、プロファイルを保存します。

1. 処理プロファイルをフォルダーに適用します。フォルダーの&#x200B;**[!UICONTROL プロパティ]**&#x200B;ページで、「**[!UICONTROL アセット処理]**」を選択し、適用する処理プロファイルを選択します。

処理プロファイルを DAM フォルダーに適用すると、このフォルダーにアップロードされたアセットやこのフォルダーで更新されたすべてのアセットで、標準の処理に加えて、定義済みの操作が実行されます。サブフォルダーは、親フォルダーに適用されたプロファイルと同じプロファイルを継承します。ユーザーは、この継承をオーバーライドできます。

既存のアセットを処理するには、アセットを選択し、「**[!UICONTROL 再処理]**」オプションを選択したあと、必要な処理プロファイルを選択します。

## ヒントと制限事項 {#limitations-best-practices}

* [!DNL Experience Manager] では、アセット処理を環境ごとに 1 分あたり 300 リクエストまでに制限し、組織ごとに 1 分あたり 700 リクエストまでに制限しています。
* [!DNL Adobe Photoshop] API 操作のファイルサイズは 4 GB までに制限され、[!DNL Adobe Lightroom] 操作では 1 GB までに制限されています。

**関連情報**

* [アセットを翻訳](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [AEM Assets as a Cloud Service でサポートされているファイル形式](file-format-support.md)
* [アセットを検索](search-assets.md)
* [接続されたアセット](use-assets-across-connected-assets-instances.md)
* [アセットレポート](asset-reports.md)
* [メタデータスキーマ](metadata-schemas.md)
* [アセットをダウンロード](download-assets-from-aem.md)
* [メタデータを管理](manage-metadata.md)
* [検索ファセット](search-facets.md)
* [コレクションを管理](manage-collections.md)
* [メタデータの一括読み込み](metadata-import-export.md)
* [AEM および Dynamic Media へのアセットの公開](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [処理プロファイルを介したアセットマイクロサービスの設定と使用](/help/assets/asset-microservices-configure-and-use.md)
>* [ [!DNL Experience Manager] との統合： [!DNL Creative Cloud]](/help/assets/aem-cc-integration-best-practices.md)
>* [アセットマイクロサービスを使用したアセットの取り込みと処理：概要](/help/assets/asset-microservices-overview.md)
