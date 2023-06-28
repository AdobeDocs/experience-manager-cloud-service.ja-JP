---
title: Adobe Target との統合
description: Adobe Target との統合
exl-id: 2b4cf35e-2b75-4303-8d09-f6644ad99274
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 66%

---

# Adobe Target との統合{#integrating-with-adobe-target}

Adobe Experience Cloud [Adobe Target](https://business.adobe.com/products/target/adobe-target.html) を使用すると、すべてのチャネルにわたってターゲティングと測定をおこない、コンテンツの関連性を高めることができます。 Adobe Target はマーケター向けのツールで、オンラインテストを設計および実行し、その場で（行動に基づいた）オーディエンスセグメントを作成し、コンテンツとオンラインエクスペリエンスのターゲット設定を自動化するために使用されます。AEM as a Cloud Service では Adobe Target Standard に使用されているターゲット設定ワークフローが採用されています。Target を使用する場合は、AEM as a Cloud Serviceのターゲティング編集環境に慣れています。

AEMサイトをAdobe Targetと統合して、ページ内のコンテンツを次のようにパーソナライズできます。

* コンテンツのターゲティングを実装します。
* Target のオーディエンスを使用してパーソナライズされたエクスペリエンスを作成する。
* 訪問者がページとやり取りを行ったときにコンテキストデータを Target に送信する。
* コンバージョン率を追跡します。

>[!NOTE]
>
>既存の Target アカウントを持たないお客様は、Experience Cloud用の Target Foundation パックへのアクセスをリクエストできます。 この Foundation パックでは、Target の使用量が制限されます。


Target に統合するには、次のタスクを実行します。

* [前提条件のタスクを実行する](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/target-requirements.html?lang=ja)：Adobe Target に登録して AEM オーサーインスタンスの特定の側面を設定します。Adobe Target アカウントには、**承認者**&#x200B;レベル以上の権限が必要です。さらに、ユーザーがアクセスできないように、パブリッシュノードのアクティビティ設定を保護する必要があります。

* Experience Platform Launch は、Target 機能（JS ライブラリ）を備えた AEM サイトを実装するための事実上の標準ツールになっています。したがって、AEM as a Cloud Service を Launch や Adobe Target と統合すると、連携が強化されます（以下のリンクを参照）。

   * [Adobe I/O を使用した Adobe Target との統合](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/integration-target-ims.html)
   * [Experience Platform Launch の統合](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-data-collection-tags/overview.html?lang=ja)
   * [Adobe I/Oを通じてAEMとAdobeLaunch を統合する](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-data-collection-tags/overview.html?lang=en)
   * [AEM と Experience Platform Launch、Analytics、Target の統合について](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-data-collection-tags/overview.html?lang=ja)

>[!NOTE]
>
>Experience Platform Launch の IMS 設定（技術アカウント）は、AEM as a Cloud Service に事前に設定されています。ユーザーはこの設定を作成する必要はありません。

1. [アクティビティを設定する](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/activitylib.html?lang=ja)：アクティビティを Target のクラウド設定に関連付けます。

>[!CAUTION]
>
>AEM as a Cloud Service では、AEM から Adobe Target にオファーとアクティビティを同期するレプリケーションエージェントは、デフォルトで無効になっています。に連絡する [Adobeサポート](https://experienceleague.adobe.com/?support-solution=General&amp;lang=ja#support) レプリケーションエージェントを再度有効にする必要がある場合は、チーム。

>[!NOTE]
>
>Target をカスタムプロキシ設定で使用している場合、AEMの一部の機能は 3.x API を使用し、他の一部の機能は 4.x API を使用するので、両方の HTTP クライアントプロキシを設定する必要があります。
>
>* 3.x は [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient) のように設定します。
>* 4.x は [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator) のように設定します。
>

>[!CAUTION]
>
>アクティビティ設定ノードの保護 **cq:ActivitySettings** 通常のユーザーがアクセスできないように、パブリッシュインスタンス上で実行します。 アクティビティ設定ノードには、Adobe Target へのアクティビティの同期を処理するサービスのみがアクセスできるようにしてください。
>
>詳しくは、 [Adobe Targetとの統合の前提条件](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/target-requirements.html?lang=ja#securing-the-activity-settings-node) を参照してください。

統合が完了したら、訪問者データを Adobe Target に送信する[ターゲットコンテンツを作成](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/content-targeting-touch.html?lang=ja)できます。コンテンツのターゲティングを有効にするには、ページコンポーネントに特定のコードが必要です。 （[ターゲットコンテンツの作成](https://experienceleague.adobe.com/docs/experience-manager-65/developing/personlization/target.html?lang=ja)を参照）。

>[!NOTE]
>
>AEM オーサーインスタンスでコンポーネントをターゲット設定すると、そのコンポーネントが、キャンペーンの登録、オファーの設定、Adobe Target セグメントの取得（設定されている場合）を行うために、Adobe Target に対して一連のサーバー側呼び出しを実行します。AEM パブリッシュから Adobe Target にサーバー側呼び出しは作成されません。

## 背景情報ソース {#background-information-sources}

AEM as a Cloud Service と Adobe Target を統合するには、Adobe Target、AEM アクティビティの管理、AEM オーディエンスの管理に関する知識が必要です。以下を十分理解している必要があります。

* Adobe Target（[Adobe Target のドキュメント](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=ja)を参照）
* AEM アクティビティコンソール（[アクティビティの管理](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/activitylib.html?lang=ja)を参照）。
* AEM Audiences( [オーディエンスの管理](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/managing-audiences.html?lang=ja)) をクリックします。

>[!NOTE]
>
>Adobe Targetを操作する場合、1 つのキャンペーンで許可されるアーティファクトの最大数は次のとおりです。
>
>* 50 の場所
>* 2,000 個のエクスペリエンス
>* 50 個の指標
>* 50 個のレポートセグメント
