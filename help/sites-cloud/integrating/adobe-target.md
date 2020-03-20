---
title: Adobe Target との統合
description: 'Adobe Target との統合 '
translation-type: tm+mt
source-git-commit: 5a7f2d603952b2c5f92363888efedb482d8efea3

---


# Adobe Target との統合{#integrating-with-adobe-target}

Adobe Marketing Cloud に含まれている [Adobe Target](http://www.adobe.com/solutions/testing-targeting/testandtarget.html) を使用すると、あらゆるチャネルにわたってターゲット設定と測定を行い、コンテンツの関連性を高めることができます。Adobe Target はマーケター向けのツールで、オンラインテストを設計および実行し、その場で（行動に基づいた）オーディエンスセグメントを作成し、コンテンツとオンラインエクスペリエンスのターゲット設定を自動化するために使用されます。クラウドサービスとしてのAEMでは、Adobe Target Standardで使用されるターゲット設定ワークフローが採用されています。 Targetを使用する場合は、AEMのクラウドサービスとしてのターゲット設定の編集環境について理解している必要があります。

AEM サイトを Adobe Target に統合して、ページ内のコンテンツを次のようにパーソナライズできます。

* コンテンツのターゲティングを実装する。
* Target オーディエンスを使用してパーソナライズされたエクスペリエンスを作成する。
* 訪問者がページとやり取りをおこなったときにコンテキストデータを Target に送信する。
* コンバージョン率を追跡する。

>[!NOTE]
>
>既存のTargetアカウントを持っていないクラウドサービスのお客様は、Adobe Experience Managerを使用して、Experience Cloud用Target Foundation Packへのアクセスをリクエストできます。  Foundation Packでは、Targetのボリュームの使用が制限されています。


Target に統合するには、次のタスクを実行します。

* [前提条件のタスクを実行する](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/target-requirements.html)：Adobe Target に登録して AEM オーサーインスタンスの特定の側面を設定します。Your Adobe Target account must have **approver** level permissions at a minimum. さらに、ユーザーがアクセスできないように、パブリッシュノードのアクティビティ設定を保護する必要があります。

* アドビによる起動は、AEMサイトにTarget機能（JSライブラリ）を実装するデファクトのツールです。 したがって、AEMをクラウドサービスとしてLaunchと統合し、Adobe Targetを入手できます（以下のリンクを参照）。

   * [Adobe I/Oを使用したAdobe Targetとの統合](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/integration-ims-adobe-io.html)
   * [Integrate Launch by Adobe](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/integrations/adobe-launch-integration-tutorial-understand.html)
   * [Adobe I/Oを使用したAEMとAdobe Launchの統合](https://helpx.adobe.com/experience-manager/using/aem_launch_adobeio_integration.html)
   * [Adobe、Analytics、およびTargetによるAEMのLaunchとの統合について](https://helpx.adobe.com/experience-manager/kt/integration/using/aem-launch-integration-tutorial-understand.html)

>[!NOTE]
>
>アドビが起動するIMS設定（技術アカウント）は、AEMでクラウドサービスとして事前に設定されています。 ユーザーは、この設定を作成する必要はありません。

1. [アクティビティを設定する](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/activitylib.html)：アクティビティを Target のクラウド設定に関連付けます。

>[!CAUTION]
>
>「AEMをクラウドサービスとして使用する場合、AEMからAdobe Targetにオファーとアクティビティを同期するレプリケーションエージェントは、デフォルトで無効になっています。 複製エージェントを再 [度有効にする必要がある場合は](https://helpx.adobe.com/contact/enterprise-support.ec.html#target) 、アドビサポートにお問い合わせください。」

>[!NOTE]
>
>カスタムプロキシ設定で Target を使用している場合、AEM には 3.x API を使用する機能と 4.x API を使用する機能があるので、両方の HTTP クライアントプロキシを設定する必要があります。
>
>* 3.x is configured with [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x は [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator) のように設定します。
>



>[!CAUTION]
>
>権限のないユーザーがアクセスできないように、パブリッシュインスタンスでアクティビティ設定ノード **cq:ActivitySettings** を保護する必要があります。アクティビティ設定ノードには、Adobe Target へのアクティビティの同期を処理するサービスのみがアクセスできるようにしてください。
>
>詳しくは、[Adobe Target との統合の前提条件](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/target-requirements.html#securing-the-activity-settings-node)を参照してください。

When the integration is complete, you can [author targeted content](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/content-targeting-touch.html) that sends visitor data to Adobe Target. ページコンポーネントでは、コンテンツのターゲット設定を有効にするために特定のコードが必要です。 (See [Developing for Targeted Content](https://docs.adobe.com/content/help/en/experience-manager-65/developing/personlization/target.html).

>[!NOTE]
>
>AEM オーサーインスタンスでコンポーネントをターゲット設定すると、そのコンポーネントが、キャンペーンの登録、オファーの設定、Adobe Target セグメントの取得（設定されている場合）をおこなうために、Adobe Target に対して一連のサーバー側呼び出しを実行します。AEM Publish から Adobe Target にサーバー側呼び出しは作成されません。

## 背景情報ソース {#background-information-sources}

AEMをクラウドサービスとしてAdobe Targetと統合するには、Adobe Target、AEM Activities管理およびAEM Audiences管理に関する知識が必要です。 次の情報に精通している必要があります。

* Adobe Target (See the [Adobe Target documentation](https://marketing.adobe.com/resources/help/en_US/target/)).
* AEM Activities console (See [Managing Activities](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/activitylib.html).
* AEM Audiences (See [Managing Audiences](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/managing-audiences.html).

>[!NOTE]
>
>Adobe Target を操作するときのキャンペーン内で許可されるアーティファクトの最大数は次のとおりです。
>
>* 場所：50
>* エクスペリエンス：2,000
>* 指標：50
>* レポートのセグメント：50
>


