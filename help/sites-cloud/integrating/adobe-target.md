---
title: Adobe Target との統合
description: 'Adobe Target との統合 '
translation-type: tm+mt
source-git-commit: bffc335fdafe6bf12a66bcd2f7aacf029fce567e
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 98%

---


# Adobe Target との統合{#integrating-with-adobe-target}

Adobe Marketing Cloud に含まれている [Adobe Target](http://www.adobe.com/jp/solutions/testing-targeting/testandtarget.html) を使用すると、あらゆるチャネルにわたってターゲット設定と測定をおこない、コンテンツの関連性を高めることができます。Adobe Target はマーケター向けのツールで、オンラインテストを設計および実行し、その場で（行動に基づいた）オーディエンスセグメントを作成し、コンテンツとオンラインエクスペリエンスのターゲット設定を自動化するために使用されます。AEM as a Cloud Service では Adobe Target Standard に使用されているターゲット設定ワークフローが採用されています。Target を使用すると、AEM as a Cloud Service のターゲット設定の編集環境に慣れ親しむことができます。

AEM Sites を Adobe Target に統合して、ページ内のコンテンツを次のようにパーソナライズできます。

* コンテンツのターゲティングを実装する。
* Target のオーディエンスを使用してパーソナライズされたエクスペリエンスを作成する。
* 訪問者がページとやり取りをおこなったときにコンテキストデータを Target に送信する。
* コンバージョン率を追跡する。

>[!NOTE]
>
>既存の Target アカウントを持たない Adobe Experience Manager as a Cloud Service ユーザーは、Experience Cloud 用の Target Foundation パックへのアクセスをリクエストできます。この Foundation パックでは、Target の使用量が制限されます。


Target に統合するには、次のタスクを実行します。

* [前提条件のタスクを実行する](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/target-requirements.html)：Adobe Target に登録して AEM オーサーインスタンスの特定の側面を設定します。Adobe Target アカウントには、**承認者**&#x200B;レベル以上の権限が必要です。さらに、ユーザーがアクセスできないように、パブリッシュノードのアクティビティ設定を保護する必要があります。

* Launch by Adobe は、Target 機能（JS ライブラリ）を備えた AEM サイトを実装するための事実上の標準ツールになっています。したがって、AEM as a Cloud Service を Launch や Adobe Target と統合すると、連携が強化されます（以下のリンクを参照）。

   * [Adobe I/O を使用した Adobe Target との統合](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/integration-ims-adobe-io.html)
   * [Launch by Adobe の統合](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/integrations/adobe-launch-integration-tutorial-understand.html)
   * [Adobe I/O を使用した AEM と Adobe Launch の統合](https://helpx.adobe.com/jp/experience-manager/using/aem_launch_adobeio_integration.html)
   * [AEM と Launch by Adobe、Analytics、Target の統合について](https://helpx.adobe.com/jp/experience-manager/kt/integration/using/aem-launch-integration-tutorial-understand.html)

>[!NOTE]
>
>Launch by Adobe の IMS 設定（技術アカウント）は、AEM as a Cloud Service に事前に設定されています。ユーザーはこの設定を作成する必要はありません。

1. [アクティビティを設定する](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/activitylib.html)：アクティビティを Target のクラウド設定に関連付けます。

>[!CAUTION]
>
>AEM as a Cloud Service では、AEM から Adobe Target にオファーとアクティビティを同期するレプリケーションエージェントは、デフォルトで無効になっています。レプリケーションエージェントを再度有効にする必要がある場合は、[アドビサポートチーム](https://helpx.adobe.com/jp/contact/enterprise-support.ec.html#experience-manager)にお問い合わせください。

>[!NOTE]
>
>カスタムプロキシ設定で Target を使用している場合、AEM には 3.x API を使用する機能と 4.x API を使用する機能があるので、両方の HTTP クライアントプロキシを設定する必要があります。
>
>* 3.x は [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient) のように設定します。
>* 4.x は [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator) のように設定します。

>



>[!CAUTION]
>
>権限のないユーザーがアクセスできないように、パブリッシュインスタンスでアクティビティ設定ノード **cq:ActivitySettings** を保護する必要があります。アクティビティ設定ノードには、Adobe Target へのアクティビティの同期を処理するサービスのみがアクセスできるようにしてください。
>
>詳しくは、[Adobe Target との統合の前提条件](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/target-requirements.html#securing-the-activity-settings-node)を参照してください。

統合が完了したら、訪問者データを Adobe Target に送信する[ターゲットコンテンツを作成](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/content-targeting-touch.html)できます。コンテンツのターゲティングを有効にするには、ページのコンポーネントに固有のコードが必要です（[ターゲットコンテンツの作成](https://docs.adobe.com/content/help/en/experience-manager-65/developing/personlization/target.html)を参照）。

>[!NOTE]
>
>AEM オーサーインスタンスでコンポーネントをターゲット設定すると、そのコンポーネントが、キャンペーンの登録、オファーの設定、Adobe Target セグメントの取得（設定されている場合）をおこなうために、Adobe Target に対して一連のサーバー側呼び出しを実行します。AEM Publish から Adobe Target にサーバー側呼び出しは作成されません。

## 背景情報ソース {#background-information-sources}

AEM as a Cloud Service と Adobe Target を統合するには、Adobe Target、AEM アクティビティの管理、AEM オーディエンスの管理に関する知識が必要です。以下を十分理解している必要があります。

* Adobe Target（[Adobe Target のドキュメント](https://docs.adobe.com/content/help/en/target/using/target-home.html)を参照）
* AEM アクティビティコンソール（[アクティビティの管理](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/activitylib.html)を参照）
* AEM オーディエンス（[オーディエンスの管理](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/managing-audiences.html)を参照）

>[!NOTE]
>
>Adobe Target を操作するときのキャンペーン内で許可されるアーティファクトの最大数は次のとおりです。
>
>* 場所：50
>* エクスペリエンス：2,000
>* 指標：50
>* レポートのセグメント：50

>


