---
title: Screens as aCloud Serviceでのビデオのサムネールのサポート
description: ここでは、ビデオのサムネールサポートをCloud ServiceとしてScreensに追加する方法について説明します。
hide: true
index: false
source-git-commit: bd1efae4453e2c3a73eb962c4e6b4b4b9ba064d2
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 0%

---


# ビデオのサムネールのサポート {#thumbnail-support-videos}

## はじめに {#introduction}

コンテンツ作成者は、ビデオのサムネールを定義して、画像をプレースホルダーとして使用し、コンテンツの再生とターゲティングを適切にテストしながら、実際のビデオを適切なチームで確定できます。 ビデオの再生に失敗した場合にも、画像を使用できます。

ビデオコンポーネントにサムネール画像のサポートを追加すると、お客様は実際のコンテンツと共にチャネルに有効なコンポーネントを適切に追加し、ビデオが実際に配信される前にターゲティング設定を実行できます。

>[!NOTE]
>サムネール画像は、ビデオコンポーネントに設定されている場合、プレーヤーでビデオの再生が失敗した場合に再生されます。 これにより、完全にスキップするのではなく、（コンテンツを再生して）目的のメッセージをオーディエンスに配信できます。

サムネールのサポートでは、次のことが可能です。

* ビデオの準備が整っていない場合や、プレーヤー上で大きなアセットのダウンロードをテストしたくない場合に、チャネルエクスペリエンスを準備します

* デバイスで再生の問題が発生した場合に備えて、フォールバックメカニズムを設定します。

## ビデオでのサムネールの使用 {#using-thumbnails}

ビデオでサムネールを使用するには、以下の手順に従います。

1. 既存のScreensチャネルに移動するか、新しいチャネルを作成します。

   >[!NOTE]
   >チャネルを作成し、チャネルにコンテンツを追加する方法については、「[ScreensでのCloud Serviceとしてのチャネルの作成と管理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/create-content/creating-channels-screens-cloud.html?lang=en)」を参照してください。

1. チャネルを選択し、アクションバーの「**編集**」をクリックして、エディターを開きます。

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-1.png)

1. 次の図に示すように、既存のビデオコンポーネントを追加または編集します。

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-2.png)

1. ビデオを選択し、*レンチ*&#x200B;アイコンをクリックして、ビデオのプロパティを開きます。

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-3.png)

1. **ビデオ**&#x200B;ダイアログボックスが開き、**サムネール**&#x200B;のドロップゾーンが表示されます。

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-4.png)

1. アセットピッカーからサムネール&#x200B;**ドロップゾーンに画像をドラッグ&amp;ドロップし、「**&#x200B;完了&#x200B;**」をクリックします。**

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-5.png)

1. 「**プレビュー**」をクリックします。

1. コンポーネントにビデオが設定されている場合、ビデオが再生されます。 そうでない場合、サムネールが設定され、サムネールが再生されます。 それ以外の場合、コンポーネントは設定されていないと見なされ、スキップされます。

## ビデオでサムネールを使用する際にサポートされるユースケース {#understand-use-case}

ビデオでサムネールを使用する際は、次の使用例を参照してください。

次の要素を含むビデオコンポーネント

* *設定は* 何もスキップされません

* *サムネールのみがサ* ムネールを再生します

* *ビデオとサムネールの両方が* ビデオを再生します。

* *ビデオは再* 生エラーが発生した場合はサムネールを再生し、サムネールが設定されていない場合は次の項目にスキップします。
