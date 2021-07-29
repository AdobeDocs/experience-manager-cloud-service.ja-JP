---
title: コンテンツの自動化によるCreative Cloud統合
description: アセットの統合を使用してCreative Cloudのバリエーションを生成
contentOwner: AG
feature: アップロード，アセット処理，公開，Asset computeマイクロサービス，ワークフロー
role: User,Admin
source-git-commit: 09aecfac8bab0377e9e777b80e7db986d7aa4914
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 0%

---


# [!DNL Adobe Creative Cloud]統合を使用してアセットのバリエーションを生成する {#content-automation}

コンテンツ自動化アドオンは、[!DNL Adobe Experience Manager Assets]を[!DNL Cloud Service]および[!DNL Adobe Creative Cloud] APIとして統合し、アセットを大規模に作成して処理します。 [!DNL Experience Manager] は、クラウドベースのアセ [ッ](/help/assets/asset-microservices-overview.md) トマイクロサービスを使用して、 [!DNL Adobe Creative Cloud] 機能を使用し、アセットの作成とメディア処理を自動化します。

[!DNL Adobe Photoshop]と[!DNL Adobe Lightroom]のアセットを編集する場合、[!DNL Experience Manager Assets]からアセットをダウンロードし、編集して、再度アップロードする必要はありません。 [!DNL Experience Manager]で処理プロファイルを作成して設定し、そのプロファイルをフォルダーに適用して、そのフォルダーにアセットをアップロードします。 アップロードしたアセットは、処理プロファイルに基づいて再処理され、これらのアセットのバリエーションを取得します。 一貫性が高く、容易な一括処理により、手作業を省き、優れたクリエイティブスキルを必要とせずに、コンテンツの速度を向上させます。 また、開発者とパートナーは、これらのAPIに直接アクセスしてアセットマイクロサービスを拡張し、カスタムロジックを含めることができます。

ユーザーは、処理プロファイルを作成して、アセットに対する次のクリエイティブ操作を自動化できます。

* **自動トーン**:人工知能を使用して画像の内容を分析し、画像の固有の属性に基づいて光と色の補正をインテリジェントに行います。

* **自動縦**:人工知能を使用して画像の内容を分析し、画像の歪んだ遠近法を修正します。たとえば、レベルの水平線を作成する場合などです。

   ![自動トーン](/help/assets/assets/content-automation-autotone.png)

   *図：自動トーンと自動ストレートは、歪んだ画像の改善に役立ちます。*

* **Lightroomプリセット**:ユーザー定義の外観を画像に適用し、カスタムで作成したプリセットを使用して一貫した外観を実現します。

   ![Lightroomプリセット](/help/assets/assets/content-automation-lrpresets.png)

   *図：AdobeLightroomプリセットを使用して、多くの画像に対して一貫した画質を提供します。*

* **画像の切り抜き**:人工知能を使用して、突き出たオブジェクトの周囲に選択範囲を作成し、1つのコマンドで背景を削除します。

   ![背景を削除し、写真から画像を切り取る](/help/assets/assets/content-automation-backgroundremove.png)

* **イメージマスク**:人工知能を使用して、1つのコマンドで突出オブジェクトの周囲にマスクを作成します。

   ![AIを使用した画像のマスク](/help/assets/assets/content-automation-mask.png)

* **Photoshopのアクション**:一連のタスクをフ [!DNL Adobe Photoshop] ァイルまたはファイルのバッチに適用します。

   ![Photoshopのアクション](/help/assets/assets/content-automation-psactions.png)

* **スマートオブジェクトの置換**:PSDファイル内で適用されたすべての効果と調整を維持しながら画像を入れ替えることで、パーソナライゼーションを大規模に実行します。

   ![オブジェクトをスマートに置換](/help/assets/assets/content-automation-objectreplace.png)

## 処理プロファイルを使用したクリエイティブアセットの一括編集 {#process-assets}

処理プロファイルを使用してバリエーションを自動的に作成するには、次の手順に従います。

1. [Adobeカスタマーケア](https://experienceleague.adobe.com/#support)に連絡して、ライセンスを受け取ります。

1. **[!UICONTROL ツール]** / **[!UICONTROL アセット]** / **[!UICONTROL 処理プロファイル]**&#x200B;に移動します。

1. 「**[!UICONTROL 作成]**」を選択し、「**[!UICONTROL 名前]**」を指定します。

1. 「**[!UICONTROL クリエイティブ]**」タブを選択し、出力フォルダーを指定して、「**[!UICONTROL 新規追加]**」を選択し、クリエイティブ設定を追加します。

1. 「**[!UICONTROL レンディション名]**」（または出力名）、「**[!UICONTROL 拡張子]**」（またはファイルタイプ）、「**[!UICONTROL 画質]**」（または出力パラメーター）、「**[!UICONTROL 次を含む]**」および「**[!UICONTROL MIMEタイプを除外]**」を選択し、必要なクリエイティブ操作。

   ![ 処理プロファイ [!UICONTROL ルの「作成」タブ]](assets/creative-processing-profile.png)

1. 一部の操作では、追加のパラメーター（アセット）が必要です。 必要に応じて、これらの追加のパラメーターの値を指定します。

1. 同じ処理プロファイルの一部として、さらにクリエイティブな操作を追加するか、プロファイルを保存します。

1. フォルダーに処理プロファイルを適用します。 フォルダーの&#x200B;**[!UICONTROL プロパティ]**&#x200B;ページで、「**[!UICONTROL アセット処理]**」を選択し、適用する処理プロファイルを選択します。

処理プロファイルをDAMフォルダーに適用すると、このフォルダーにアップロードまたは更新されたすべてのアセットで、標準の処理に加えて、定義済みの操作が実行されます。 サブフォルダーは、親フォルダーに適用されたのと同じプロファイルを継承します。 ユーザーは、この継承を上書きできます。

既存のアセットを処理するには、アセットを選択し、「**[!UICONTROL 再処理]**」オプションを選択して、必要な処理プロファイルを選択します。

## ヒントと制限事項 {#limitations-best-practices}

* [!DNL Experience Manager] では、アセット処理を環境あたり300個のリクエストに制限し、組織あたり700個のリクエストに制限します。
* [!DNL Adobe Photoshop] API操作の場合はファイルサイズは4 GBに制限され、[!DNL Adobe Lightroom]操作の場合は1 GBに制限されます。

>[!MORELIKETHIS]
>
>* [処理プロファイルを介したアセットマイクロサービスの設定と使用](/help/assets/asset-microservices-configure-and-use.md)を参照してください。
>* [ [!DNL Experience Manager]  [!DNL Creative Cloud]](/help/assets/aem-cc-integration-best-practices.md)との統合。
>* [アセットマイクロサービスを使用したアセットの取り込みと処理：概要](/help/assets/asset-microservices-overview.md)を示します。

