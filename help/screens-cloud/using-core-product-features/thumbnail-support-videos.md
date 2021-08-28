---
title: Screens as aCloud Serviceでのビデオのサムネールのサポート
description: ここでは、ビデオのサムネールサポートをCloud ServiceとしてScreensに追加する方法について説明します。
index: true
source-git-commit: cd06e409ec085fcc77fc7bb466169de3a14dba40
workflow-type: tm+mt
source-wordcount: '455'
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

ビデオ内のサムネールは、次の使用例をサポートしています。

* 何も設定されていないビデオコンポーネントはスキップされます。

* サムネールのみが設定されたビデオコンポーネントがサムネールを再生します。

* ビデオとサムネールの両方が設定されたビデオコンポーネントがビデオを再生します。

* ビデオセットを含むビデオコンポーネントは、再生エラーが発生した場合にサムネールを再生し、サムネールが設定されていない場合には次の項目にスキップします。
