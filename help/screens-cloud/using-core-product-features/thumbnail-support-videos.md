---
title: Screens as a Cloud Service でのビデオのサムネールサポート
description: このページでは、Screens as a Cloud Service にビデオのサムネールサポートを追加する方法について説明します。
index: true
exl-id: 7b15d7cc-f089-4008-9039-5f48343a0f20
source-git-commit: f5af37bf39ecd5a964a8c94a731111c561c2934e
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 30%

---

# ビデオのサムネールサポート {#thumbnail-support-videos}

## はじめに {#introduction}

コンテンツ作成者は、画像をプレースホルダーとして使用し、コンテンツの再生とターゲティングを適切にテストし、実際のビデオが適切なチームで最終処理されるように、ビデオのサムネールを定義できます。 その画像は、ビデオの再生に失敗した場合でも使用できます。

ビデオコンポーネントにサムネール画像のサポートを追加すると、お客様はチャネルに有効なコンポーネントを実際のコンテンツと共に適切に追加し、ビデオが配信される前にターゲット設定を実行できます。

>[!NOTE]
>サムネール画像は、ビデオコンポーネントに設定されている場合、プレーヤーでビデオの再生に失敗した場合に再生されます。 このワークフローを使用すると、完全にスキップする代わりに、目的のメッセージを（コンテンツを再生して）オーディエンスに配信できます。

サムネールのサポートでは、次の操作を実行できます。

* ビデオがまだ準備できていない場合や、プレーヤーに大きなアセットをダウンロードしてテストする必要がない場合に、チャネルエクスペリエンスを準備する

* デバイスで再生の問題が発生した場合に備えて、フォールバックメカニズムを設定する

## ビデオでのサムネールの使用 {#using-thumbnails}

>[!IMPORTANT]
>**前提条件**
>ビデオにサムネールを使用する方法を学ぶ前に、Screens as a Cloud Serviceプロジェクトでチャネルのビデオレンディションを作成する方法を必ず学んでください。 詳しくは、 [Screens でのビデオレンディションの作成as a Cloud Service](/help/screens-cloud/configuring/creating-screens-video-renditions-cloud-service.md).

ビデオでサムネールを使用するには、次の手順に従います。

1. 既存の Screens チャネルに移動するか、チャネルを作成します。

   >[!NOTE]
   >チャネルを作成しチャネルにコンテンツを追加する方法については、[Screens as a Cloud Service でのチャネルの作成と管理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/create-content/creating-channels-screens-cloud.html?lang=en)を参照してください。

1. チャネルを選択します。アクションバーで、 **編集** をクリックしてエディターを開きます。


   ![アクションバーの「編集」ボタン](/help/screens-cloud/using-core-product-features/assets/thumbnail-1.png)

1. 既存のビデオコンポーネントを追加または編集します（下図を参照）。

   ![ビデオアセットのハイライト表示画像。](/help/screens-cloud/using-core-product-features/assets/thumbnail-2.png)

1. 既存のビデオコンポーネントを追加または編集します（下図を参照）。

1. ビデオを選択し、設定 (*レンチ*) アイコンをクリックして、ビデオのプロパティを開きます。

   ![設定アイコンを向く矢印付きの選択済みビデオアセット画像（レンチ形式で表示）。 をクリックします。](/help/screens-cloud/using-core-product-features/assets/thumbnail-3.png)

1. この **ビデオ** ダイアログボックスが開き、表示できます **サムネール** ドロップゾーン。

   ![ビデオアセットの画像と「サムネール」ドロップボックスを表示するビデオダイアログボックス](/help/screens-cloud/using-core-product-features/assets/thumbnail-4.png)

1. アセットピッカーから **サムネール** ドロップゾーンとクリック **完了**.

   ![ビデオダイアログボックスの後ろに表示されるアセットの画像ピッカーで、「サムネール」ドロップボックスに画像アセットが表示されます。](/help/screens-cloud/using-core-product-features/assets/thumbnail-5.png)

1. **プレビュー**&#x200B;をクリックします。

1. コンポーネントでビデオが設定されている場合、ビデオが再生されます。 設定されていない場合は、サムネールが設定され、サムネールが再生されます。 それ以外の場合、コンポーネントは設定されていないと見なされ、スキップされます。

## ビデオでサムネールを使用する際にサポートされているユースケース {#understand-use-case}

ビデオ内のサムネールでは、次のユースケースをサポートしています。

* 設定がないビデオコンポーネントはスキップされます。

* サムネールのみが設定されたビデオコンポーネントがサムネールを再生します。

* ビデオコンポーネント（ビデオのレンディションが正しい場合）とサムネールが両方ともビデオを再生します。

* ビデオセットを持つビデオコンポーネントは、再生エラーが発生した場合はサムネールを再生し、サムネールが設定されていない場合は次の項目までスキップします。
