---
title: 実稼動プログラムの作成
description: Cloud Manager を使用して、ライブトラフィックをホストする独自の実稼動プログラムを作成する方法について説明します。
exl-id: 4ccefb80-de77-4998-8a9d-e68d29772bb4
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 6a3d2d484bde20586b329010cdfe156570e736f5
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 34%

---


# 実稼動プログラムの作成 {#create-production-program}

実稼動プログラムは、AEMとCloud Managerに精通し、コードの記述、ビルド、テストを行う準備が整い、ライブトラフィックを処理するためにコードをデプロイすることを目標とするユーザー向けです。

プログラムの種類について詳しくは、ドキュメント [ プログラムとプログラムの種類について ](program-types.md) を参照してください。

## 実稼動プログラムの作成 {#create}

組織の使用権限によっては、プログラムを追加する際に [ 追加のオプション ](#options) が表示される場合があります。

**実稼動プログラムを作成するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)** コンソールの右上隅付近にある「**プログラムを追加**」をクリックします。

   ![Cloud Manager ランディングページ](assets/log-in.png)

1. *プログラムを作成しましょう* ウィザードの **プログラム名** テキストフィールドに、プログラムの名前を入力します。

1. **プログラムの目的** の下で、**`Set up for production`** を選択します。

   ![プログラム作成ウィザード](assets/create-production-program.png)

1. （オプション）ウィザードダイアログボックスの右下隅で、次のいずれかの操作を行います。

   * 画像ファイルを **プログラム画像を追加** ターゲットにドラッグ&amp;ドロップします。
   * **プログラム画像を追加** をクリックし、ファイルブラウザーから画像を選択します。
   * 追加した画像を削除するには、ごみ箱アイコンをクリックします。

1. 「**続行**」をクリックします。

1. **ソリューションとアドオン** リストボックスで、プログラムに含める 1 つ以上のソリューションを選択します。

   * 利用可能な様々なソリューションに対して 1 つ以上のプログラムが必要かどうかが不明な場合は、最も興味のあるプログラムを選択します。後で[プログラムを編集](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)することで、追加のソリューションをアクティブ化することができます。プログラム設定の推奨事項について詳しくは、[実稼動プログラムの概要ドキュメント](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md)を参照してください。
   * プログラムを作成するには、少なくとも 1 つのソリューションが必要です。
   * デジタルエクスペリエンスを最適化する完全に管理された CDN ソリューションには **0}Edge Deliver Services} を選択します。**[Edge Delivery Servicesを使用したCloud Manager プロジェクト配信について ](#edge-overview) を参照してください。
   * 「**[セキュリティの強化を有効にする](#security)**」オプションを選択した場合は、HIPAA 資格が使用可能なソリューションのみを選択できます。

   ![ソリューションを選択](/help/implementing/cloud-manager/assets/add-production-program-with-edge.png)

1. ソリューション名の左側にある山形アイコンをクリックすると、オプションのアドオンが表示されます。例えば、「**Sites** の下にある **Commerce** アドオンオプションなどです。

   ![アドオンを選択](assets/setup-prod-commerce.png)

1. ソリューションやアドオンを選択してから、「**続行**」をクリックします。

1. 「**開始日**」タブで、実稼動プログラムの運用開始予定日を入力します。

   ![運用開始予定日の定義](assets/set-up-go-live.png)

   * この日付はいつでも編集できます。
   * この日付は、情報提供の目的と、[**プログラムの概要** ページ ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#program-overview) の運用開始ウィジェットをトリガーします。 この機能は、AEM as a Cloud Serviceのベストプラクティスへのタイムリーな製品内リンクを提供し、スムーズな運用開始エクスペリエンスをサポートします。

1. 「**作成**」をクリックします。Cloud Managerがプログラムを作成し、ランディングページに表示して選択します。

![Cloud Manager の概要](assets/navigate-cm.png)

## その他の実稼動プログラムオプション {#options}

組織が使用できる使用権限に応じて、実稼動用プログラムの作成時に追加のオプションを使用できる場合があります。

### セキュリティ {#security}

必要な権限がある場合は、「**`Set up for production`** 定」ダイアログボックスの最初のタブとして「**セキュリティ**」タブが表示されます。

![セキュリティオプション](assets/create-production-program-security.png)

「**セキュリティ**」タブでは、実稼動プログラムに対して **HIPAA** または **WAF-DDOS 保護**、あるいはその両方をアクティブ化するオプションが提供されます。

AdobeHIPAA 準拠のWAF-DDOS （Web Application Firewall - Distributed Denial of Service）により、脆弱性から保護するための多層アプローチの一部としてクラウドベースのセキュリティが促進されます。

* **HIPAA** - このオプションは、アドビの HIPPA 対応ソリューションの実装を有効にします。
   * アドビの HIPAA 対応ソリューションの実装について詳しくは、[こちら](https://www.adobe.com/trust/compliance/hipaa-ready.html)を参照してください。
   * プログラムの作成後に HIPAA を有効または無効にすることはできません。
* **WAF-DDOS 対策** – このオプションを使用すると、アプリケーションを保護する規則によって Web アプリケーション ファイアウォールが有効になります。
   * アクティブ化した後は、（実稼動以外のパイプライン [ を設定することで、WAF-DDOS 対策を設定でき ](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) す。
   * リポジトリにトラフィックフィルタールールを管理して適切にデプロイする方法については、[WAF ルールを含むトラフィックフィルタールール ](/help/security/traffic-filter-rules-including-waf.md) を参照してください。

### SLA {#sla}

必要な権限がある場合、「**SLA**」タブが「**`Set up for production`**」ダイアログボックスの 2 番目または 3 番目のタブとして表示されます。

![SLA オプション](assets/create-production-program-sla.png)

AEM Sites および Forms は、標準の 99.9％のサービスレベル契約（SLA）を提供しています。「**99.99％のサービスレベル契約**」オプションを使用すると、Sites や Forms の実稼動環境で 99.99％の最小稼動時間の割合が有効になります。

99.99％の SLA には、可用性の向上や待ち時間の短縮を含むメリットがあり、プログラムの実稼動環境に[追加の公開地域](/help/implementing/cloud-manager/manage-environments.md#multiple-regions)を適用する必要があります。

99.99% のSLAを有効にするための [ 要件 ](#sla-requirements) が満たされたら、[ フルスタックパイプライン ](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) を実行して有効にする必要があります。

#### 99.99％の SLA の要件 {#sla-requirements}

99.99％の SLA には、必要な使用権限以外にも、使用に関する追加の要件があります。

* 99.99% SLAをプログラムに適用する際には、99.99% のSLAと、追加の公開地域の使用権限が必要です。
* Cloud Managerは、99.99% のSLAをプログラムに適用する前に、未使用の [ 追加の公開地域 ](/help/implementing/cloud-manager/manage-environments.md#multiple-regions) 使用権があることを確認します。
* プログラムを編集する際、1 つ以上の追加の公開地域がある実稼動環境が既に含まれている場合、Cloud Manager では 99.99％の SLA 使用権限が使用可能かどうかのみを確認します。
* 99.99% のSLAとレポートをアクティベートするには、[ 実稼働/ステージング環境 ](/help/implementing/cloud-manager/manage-environments.md#adding-environments) が作成され、実稼働/ステージング環境に少なくとも 1 つの追加のパブリッシュリージョンが適用されている必要があります。
   * [ 高度なネットワーク ](/help/security/configuring-advanced-networking.md) を使用している場合は、[Adding Multiple Publish Regions to a New Environment](/help/implementing/cloud-manager/manage-environments.md#adding-regions) のドキュメントを参照して、地域的な障害が発生した場合でも接続が維持されるように、推奨事項を確認してください。
* 99.99％の SLA プログラムに 1 つ以上の追加の公開地域が維持する必要があります。ユーザーは、99.99％の SLA プログラムから最後の追加の公開地域を削除することは許可されていません。
* Sites または Forms ソリューションが有効になっている実稼動プログラムでは、99.99％の SLA がサポートされます。
* [ フルスタックパイプライン ](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) を実行してアクティブ化するか、プログラム編集時に 99.99% のSLAを非アクティブ化します。

## プログラムへのアクセス {#accessing}

1. ランディングページにプログラムカードが表示されたら、省略記号（...）ボタンを選択して、使用可能なメニューオプションを表示します。

   ![プログラムの概要](assets/program-overview.png)

1. 「**プログラムの概要**」を選択して、Cloud Manager の&#x200B;**概要**&#x200B;ページに移動します。

1. 概要ページのメインコールトゥアクションカードのガイドに従って、環境、実稼動以外のパイプライン、最後に実稼動パイプラインを作成できます。

   ![プログラムの概要](assets/set-up-prod5.png)

>[!TIP]
>
>Cloud Managerのナビゲーション方法と ](/help/implementing/cloud-manager/navigation.md) マイプログラム **コンソールについて詳しくは、[Cloud Manager UI の操作** を参照してください。

>[!NOTE]
>
>[ サンドボックスプログラム ](introduction-sandbox-programs.md#auto-creation) とは異なり、実稼動プログラムでは、Cloud Managerの適切な役割を持つユーザーがセルフサービス UI を使用してプロジェクトを作成し環境を追加する必要があります。


