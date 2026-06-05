---
title: 実稼動プログラムの作成
description: Cloud Manager を使用して、ライブトラフィックをホストする独自の実稼動プログラムを作成する方法について説明します。
exl-id: 4ccefb80-de77-4998-8a9d-e68d29772bb4
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: 4ae77b2c9cff253749578127827a12e8483aaf7f
workflow-type: tm+mt
source-wordcount: '1720'
ht-degree: 55%

---


# 実稼動プログラムの作成 {#create-production-program}

実稼動プログラムは、Adobe Experience Manager（AEM）と Cloud Manager に精通し、ライブトラフィックの処理にコードをデプロイすることを目的として、コードの記述、ビルド、テストを行う準備ができているユーザーを対象としています。

プログラムタイプについて詳しくは、[プログラムとプログラムタイプについて](program-types.md)のドキュメントを参照してください。

## 実稼動プログラムの作成 {#create}

組織の使用権限によって、プログラムの追加時に使用できる追加の実稼動プログラムオプションが決まります。
[追加の実稼動プログラムのオプション &#x200B;](#options)を参照してください。

**実稼動プログラムを作成するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールの右上隅付近にある「**プログラムを追加**」をクリックします。

   ![Cloud Manager ランディングページ](assets/log-in.png)

1. *プログラムを作成*&#x200B;ウィザードの&#x200B;**プログラム名**&#x200B;テキストフィールドに、プログラムの名前を入力します。

1. **プログラムの目的**&#x200B;の下で、![地球のアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Globe_18_N.svg)「**実稼動用に設定**」を選択します。

   ![プログラムの作成ウィザード](assets/create-production-program.png)

1. （オプション）ウィザードダイアログボックスの右下隅で、次のいずれかの操作を行います。

   * 画像ファイルを ![画像アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Image_18_N.svg) **プログラム画像を追加**&#x200B;ターゲットにドラッグ＆ドロップします。
   * ![画像アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Image_18_N.svg)「**プログラム画像を追加**」をクリックし、ファイルブラウザーから画像を選択します。
   * ![削除アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_DeleteOutline_18_N.svg) をクリックして、追加した画像を削除します。

1. 「**続行**」をクリックします。

1. 「**セキュリティ**」タブで、使用するセキュリティオプションを選択します。 [&#x200B; セキュリティ &#x200B;](#security)を参照してください。

   実稼動用に設定ウィザード ![&#128279;](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/create-production-program-security-tab.png)の「 セキュリティ」タブ

1. 「**続行**」をクリックします。

1. **ソリューションとアドオン**&#x200B;リストボックスで、プログラムに含める 1 つ以上のソリューションを選択します。

   * 利用可能なさまざまなソリューションに対して1つ以上のプログラムが必要かどうかわからない場合は、最も関心のあるプログラムを選択してください。 後で[プログラムを編集](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)することで、追加のソリューションをアクティブ化することができます。 プログラム設定の推奨事項について詳しくは、[実稼動プログラムの概要ドキュメント](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md)を参照してください。
   * プログラムを作成するには、1 つ以上のソリューションを選択する必要があります。 例えば、デジタルエクスペリエンスを最適化する完全に管理された CDN ソリューションとして **Edge Delivery Services** を選択できます。 [Edge Delivery Servicesを使用したCloud Manager プロジェクトの配信について](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md)を参照してください。

   * ソリューション名の左側にある ![山形サイズ 300 アイコン](https://spectrum.adobe.com/static/icons/ui_18/ChevronSize300.svg) をクリックして、オプションのアドオンを表示します。<!-- such as the **Commerce** add-on option under **Sites**. -->

<!--   ![Select add-ons](assets/setup-prod-commerce.png) -->

    >[!NOTE]
    >
    > プログラムでEdge Delivery Servicesを配信に使用している場合、パブリッシュ層は必要ない場合があります。 柔軟なパブリッシュ階層機能（Beta）を使用すると、「ソリューションとアドオン」タブでパブリッシュ階層をプロビジョニングするかどうかを設定できます。 [Flexible Publish Tier （Beta） ] （/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#flexible-publish-tier）を参照してください。
    
    ![ ソリューションを選択] （/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/create-production-program-solutions.png） 

1. 「**続行**」をクリックします。

1. 「**配信タイプ**」タブでは、前の手順で選択したソリューションとアドオンに基づいて事前入力されていることに注意してください。 **AEM パブリッシュ**&#x200B;を選択した場合は、後でオンデマンドでプロビジョニングできます。

   ![配信タイプ タブ &#x200B;](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/create-production-program-delivery-type.png)


   <!-- * If you selected the **[Enable Enhanced Security](#security)** option, you can select only as many solutions for which HIPAA entitlements are available. -->

1. 「**続行**」をクリックします。

1. 必要な権限がある場合は、「**SLA**」タブは、**`Set up for production`** ダイアログで 2 番目か 3 番目のタブとして表示されます。 [SLA](#sla)を参照してください。

   ![SLA オプション](assets/create-production-program-sla.png)

   Sites および Forms は、標準の 99.9％のサービスレベル契約（SLA）を提供しています。

1. 「**続行**」をクリックします。

1. 「**公開日**」タブで、実稼動プログラムを公開する予定の日付を入力します。

   ![運用開始予定日の定義](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/create-production-program-go-live-date.png)

   * この日付はいつでも編集できます。
   * この日付は、情報として役に立ち、[**プログラムの概要**&#x200B;ページ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#program-overview)で運用開始ウィジェットをトリガーします。 この機能は、AEM as a Cloud Service のベストプラクティスへのタイムリーな製品内リンクを提供して、スムーズな運用開始エクスペリエンスをサポートします。

1. 「**作成**」をクリックします。 Cloud Manager によってプログラムが作成され、ランディングページに表示され、選択できるようになります。

   ![Cloud Manager の概要](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/create-production-program-my-programs.png)


## その他の実稼動プログラムオプション {#options}

組織で使用可能な使用権限に応じて、実稼動プログラムの作成時に次の追加オプションを使用できます。

### セキュリティ {#security}

必要な使用資格がある場合は、「**セキュリティ**」タブが **`Set up for production`** ダイアログボックスの最初のタブとして表示されます。

![セキュリティオプション](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/create-production-program-security-tab.png)

「**セキュリティ**」タブには、実稼動プログラム用の **HIPAA** か **WAF-DDOS 保護**&#x200B;のどちらか一方または両方をアクティブにするオプションが表示されます。

アドビの HIPAA 準拠の WAF-DDOS（web アプリケーションファイアウォール - 分散型サービス拒否）により、脆弱性から保護するための多層アプローチの一環としてクラウドベースのセキュリティが促進されます。

* **HIPAA** – このオプションを使用すると、AdobeのHIPAA対応ソリューションの実装が有効になります。
   * Adobe Experience Manager as a Cloud Service[&#128279;](/help/compliance/hipaa/hipaa-readiness.md)および[AdobeのHIPAA対応ソリューション実装](https://www.adobe.com/trust/compliance/hipaa-hds/hipaa-ready.html)のHIPAA対応の詳細について説明します。
   * プログラムの作成後に HIPAA を有効または無効にすることはできません。
* **WAF-DDOS Protection** – このオプションを使用すると、ルールを通じてWeb Application Firewallを有効にして、アプリケーションを保護できます。
   * 有効化されると、WAF-DDOS 保護は、[実稼動以外のパイプライン](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)で設定できます。
   * リポジトリでトラフィックフィルタールールを管理し、適切にデプロイする方法について詳しくは、[WAF ルールを含むトラフィックフィルタールール](/help/security/traffic-filter-rules-including-waf.md)を参照してください。
* **顧客管理キー** – このオプションを使用すると、プログラムのCMK （顧客管理キー）がアクティブ化され、Azure Blob StorageおよびMongoDBに保存されているデータに独自の暗号化キーを指定できます。

  >[!IMPORTANT]
  >
  >プログラム作成後にCMKを有効または無効にすることはできません。

   * CMKは、Cloud Service プログラムでのみ使用できます。 サンドボックスプログラムでは有効にできません。
   * プログラム内では、CMKはステージング環境と実稼動環境のみをカバーします。
   * プログラムでCMKを有効にした後、CMKを無効にすることはできません。
   * CMKを有効にした後、Experience Hubで暗号化キーを設定します。
AEM as a Cloud Service[&#128279;](/help/security/customer-managed-keys.md)のCustomer Managed Keys Setupを参照してください。
   * CMKが有効になっている場合、プログラム概要ページには、プログラムでCMKがアクティブであることを示すロックアイコンが表示されます。このアイコンは、プログラム内の個々の環境に対するCMKのアクティベーションステータスを反映していません。
     ![CMKがプログラムでアクティブであることを示すロックアイコン &#x200B;](/help/implementing/cloud-manager/release-notes/assets/cmk-status-on-program-card.png)
CMK ライセンスの使用状況は、ライセンスダッシュボードに表示されます。組織が購入したCMK クレジットの数と、それを使用しているプログラムの数を表示するには、[&#x200B; ライセンスダッシュボード &#x200B;](/help/implementing/cloud-manager/license-dashboard.md)を参照してください。
     ![&#x200B; ライセンスダッシュボードで使用可能な顧客管理キーの数を表示](/help/implementing/cloud-manager/release-notes/assets/cmk-license-dashboard.png)

### 柔軟な公開層（Beta） {#flexible-publish-tier}

>[!NOTE]
>
>ここで説明する柔軟なパブリッシュ層はBetaにあります。 Betaに参加するには、[grp-beta_xwalk-publish_config@adobe.com](mailto:grp-beta_xwalk-publish_config@adobe.com)にAdobeの組織IDとプログラム IDをメールで送信してください。

組織で柔軟なパブリッシュ層機能が有効になっている場合は、プログラムの環境にパブリッシュ層が必要かどうかを設定できます。 このオプションは、**実稼動用に設定** ダイアログボックスの「**配信タイプ**」タブ（[&#x200B; プログラム作成中](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)）に表示されます。

実稼動用に設定ウィザードの「![配信タイプ」タブ &#x200B;](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/create-production-program-delivery-type.png)

**プログラムを編集** ダイアログボックスにも表示されます（[&#x200B; プログラムを編集](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)する場合）。

![配信タイプのオプションが表示されたプログラムダイアログボックスを編集](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/edit-program-delivery-type.png)

すべてのアーキテクチャにパブリッシュ層が必要なわけではありません。 次の表に、パブリッシュ層を必要とするアーキテクチャとそうでないアーキテクチャを示します。

| アーキテクチャ | パブリッシュ層 |
| --- | --- |
| 従来型AEM Sites | 必須 |
| ヘッドレス/API ファースト | 必須 |
| Edge Delivery Services | 不要 |

必要な場合にのみパブリッシュ層を有効にすることで、次のことが可能になります。

* 環境をより迅速にプロビジョニング：
* インフラの簡素化。
* 不要なコンポーネントの削減：

**仕組み**
組織でフレキシブル公開階層機能が有効になっている場合：

* Cloud Managerは、プログラム内のすべての新しい環境をデフォルトで&#x200B;**オーサー層のみ**&#x200B;でプロビジョニングします。 ユーザーインターフェイスに表示される情報メッセージは、この動作を確認します。
* プログラムの作成中に&#x200B;**AEM パブリッシュ**&#x200B;を選択すると、パブリッシュ層がアクティブ化され、*新しい環境*&#x200B;でプロビジョニングされます。
* プログラムを編集して、後でパブリッシュ層をアクティブ化することもできます。 [プログラムの編集](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)を参照してください。

>[!NOTE]
>
>プログラムでコンテンツ配信にEdge Delivery Servicesを、コンテンツ作成にAEM オーサーを使用する場合、パブリッシュ層は必要ありません。 コンテンツはEdge Deliveryを通じて配信され、AEM パブリッシュ層を通過しません。 AEM オーサリング機能（Beta）を使用したEdge Delivery Servicesについてを参照してください。

### SLA {#sla}

必要な権限がある場合は、「**SLA**」タブは、**`Set up for production`** ダイアログで 2 番目か 3 番目のタブとして表示されます。

![SLA オプション](assets/create-production-program-sla.png)

Sites および Forms は、標準の 99.9％のサービスレベル契約（SLA）を提供しています。 「**99.99％のサービスレベル契約**」オプションは、Sites、Forms、Edge Delivery Services または 3 つすべてに関して、本番環境で 99.99％の最小稼動時間を保証します。

99.99％の SLA には、可用性の向上や待ち時間の短縮を含むメリットがあります。

Sites と Forms のプログラムの場合、99.99％の SLA では、プログラムの本番環境に[追加の公開地域](/help/implementing/cloud-manager/manage-environments.md#multiple-regions)を適用する必要があります。 [要件](#sla-requirements)が満たされたときに99.99% SLAをアクティブ化するには、[&#x200B; フルスタックパイプライン &#x200B;](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)を実行します。

Edge Delivery Services の場合、プログラムで 99.99％の SLA ライセンスを設定する以外に要件は&#x200B;*ありません*。

#### 99.99％の SLA の要件 {#sla-requirements}

必要な使用権限に加えて、Sites または Forms プログラムの 99.99％の SLA を使用するには、次の追加要件があります。

* 99.99％の SLA をプログラムに適用する際に、組織は 99.99％の SLA と追加の公開地域の使用権限を使用できる必要があります。
* Cloud Manager では、99.99％の SLA をプログラムに適用する前に、未使用の[追加の公開地域](/help/implementing/cloud-manager/manage-environments.md#multiple-regions)の使用権限が使用できることを確認します。
* プログラムを編集する際、1 つ以上の追加の公開地域がある本番環境が既に含まれている場合、Cloud Manager では 99.99％の SLA 使用権限が使用可能かどうかのみを確認します。
* 99.99% SLAとレポートをアクティブ化するには、[実稼動/ステージ環境](/help/implementing/cloud-manager/manage-environments.md#adding-environments)を作成し、実稼動/ステージ環境に少なくとも1つのパブリッシュリージョンを追加する必要があります。
   * [高度なネットワーク](/help/security/configuring-advanced-networking.md)を使用している場合は、地域に障害が発生した場合でも接続を維持できるように、[新しい環境への複数の公開地域の追加](/help/implementing/cloud-manager/manage-environments.md#adding-regions)ドキュメントで推奨事項を必ず確認してください。
* 99.99％の SLA プログラムには、常に 1 つ以上の公開地域を含める必要があります。 ユーザーは、最後に残っている追加の公開地域をプログラムから削除することは許可されていません。
* Sites または Forms ソリューションが有効になっている実稼動プログラムでは、99.99％の SLA がサポートされます。
* 99.99％の SLA は、[フルスタックパイプライン](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)を実行してアクティベートするか、プログラム編集時にアクティベート解除します。

## プログラムへのアクセス {#accessing}

1. ランディングページにプログラムカードが表示されたら、![その他アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックして、使用可能なメニューオプションを表示します。

   ![プログラムの概要](assets/program-overview.png)

1. 「**プログラムの概要**」を選択して、Cloud Manager の&#x200B;**概要**&#x200B;ページに移動します。

1. 概要ページにあるメインのコールトゥアクションカードのガイドに従って、環境、実稼動以外のパイプライン、そして最終的に実稼動パイプラインを作成できます。

   ![プログラムの概要](assets/set-up-prod5.png)

>[!TIP]
>
>Cloud Managerの操作方法と&#x200B;**マイプログラム** コンソールの理解については、[Cloud Manager UI](/help/implementing/cloud-manager/navigation.md)の操作を参照してください。

>[!NOTE]
>
>[サンドボックスプログラム](introduction-sandbox-programs.md#auto-creation)とは異なり、実稼動プログラムでは、Cloud Manager の適切な役割を持つユーザーがセルフサービス UI を使用してプロジェクトを作成し環境を追加する必要があります。


