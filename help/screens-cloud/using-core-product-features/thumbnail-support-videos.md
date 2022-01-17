---
title: Screens as a Cloud Service でのビデオのサムネールサポート
description: このページでは、Screens as a Cloud Service にビデオのサムネールサポートを追加する方法について説明します。
index: true
exl-id: 7b15d7cc-f089-4008-9039-5f48343a0f20
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: ht
source-wordcount: '494'
ht-degree: 100%

---

# ビデオのサムネールサポート {#thumbnail-support-videos}

## はじめに {#introduction}

コンテンツ作成者は、ビデオのサムネールを定義して、その画像をプレースホルダーとして使用できるようにし、実際のビデオを該当チームが仕上げている間に、コンテンツの再生とターゲティングを適切にテストすることができます。その画像は、ビデオの再生に失敗した場合でも使用できます。

ビデオコンポーネントにサムネール画像のサポートを追加すると、ユーザーは実際のコンテンツと共に有効なコンポーネントをチャネルに適切に追加し、ビデオが実際に配信される前にターゲティング設定を実行できます。

>[!NOTE]
>サムネール画像は、ビデオコンポーネントに設定されている場合、プレーヤーでビデオの再生が失敗した場合に再生されます。これにより、コンテンツを完全にスキップするのではなく、（コンテンツを再生して）適切なメッセージをオーディエンスに配信できます。

サムネールのサポートにより、次のことが可能になります。

* ビデオがまだ準備できていない場合や、プレーヤーに大きなアセットをダウンロードしてテストする必要がない場合に、チャネルエクスペリエンスを準備する

* デバイスで再生の問題が発生した場合に備えて、フォールバックメカニズムを設定する

## ビデオでのサムネールの使用 {#using-thumbnails}

>[!IMPORTANT]
>**前提条件**
>ビデオにサムネールを使用する方法を学ぶ前に、Screens as a Cloud Service プロジェクトでチャネルのビデオレンディションを作成する方法を必ず学んでください。詳しくは、[こちら](/help/screens-cloud/configuring/creating-screens-video-renditions-cloud-service.md)を参照してください。

ビデオでサムネールを使用するには、次の手順に従います。

1. 既存の Screens チャネルに移動するか、新しいチャネルを作成します。

   >[!NOTE]
   >チャネルを作成しチャネルにコンテンツを追加する方法については、[Screens as a Cloud Service でのチャネルの作成と管理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/create-content/creating-channels-screens-cloud.html?lang=ja)を参照してください。

1. チャネルを選択し、アクションバーの「**編集**」をクリックして、エディターを開きます。

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-1.png)

1. 既存のビデオコンポーネントを追加または編集します（下図を参照）。

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-2.png)

1. ビデオを選択し、*レンチ*&#x200B;アイコンをクリックして、ビデオのプロパティを開きます。

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-3.png)

1. **ビデオ**&#x200B;ダイアログボックスが開き、**サムネール**&#x200B;ドロップゾーンが表示されます。

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-4.png)

1. アセットピッカーから&#x200B;**サムネール**&#x200B;ドロップゾーンに画像をドラッグ＆ドロップし、「**完了**」をクリックします。

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-5.png)

1. 「**プレビュー**」をクリックします。

1. コンポーネントにビデオが設定されている場合は、ビデオが再生されます。ビデオが設定されておらず、サムネールが設定されている場合は、サムネールが再生されます。それ以外の場合、コンポーネントは未設定と見なされ、スキップされます。

## ビデオでサムネールを使用する際にサポートされているユースケース {#understand-use-case}

ビデオ内のサムネールでは、次のユースケースをサポートしています。

* 何も設定されていないビデオコンポーネントはスキップされます。

* サムネールのみ設定されているビデオコンポーネントでは、サムネールを再生します。

* ビデオ（正しいレンディションがあるもの）とサムネールの両方が設定されているビデオコンポーネントでは、ビデオを再生します。

* ビデオが設定されているビデオコンポーネントでは、再生エラーが発生した場合はサムネールを再生し、サムネールが設定されていない場合は次の項目までスキップします。
