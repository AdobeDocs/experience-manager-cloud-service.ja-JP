---
title: 実稼動プログラムの作成
description: Cloud Manager を使用して、ライブトラフィックをホストする独自の実稼動プログラムを作成する方法について説明します。
exl-id: 4ccefb80-de77-4998-8a9d-e68d29772bb4
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: cb9707e4f53e32ed6e5aec244b1ef2240fcf376c
workflow-type: tm+mt
source-wordcount: '1098'
ht-degree: 79%

---


# 実稼動プログラムの作成 {#create-production-program}

実稼動プログラムは、Adobe Experience Manager（AEM）とCloud Managerに精通し、コードを記述、ビルド、テストする準備が整い、ライブトラフィックを処理するためにコードをデプロイすることを目標とするユーザー向けです。

プログラムタイプについて詳しくは、[プログラムとプログラムタイプについて](program-types.md)のドキュメントを参照してください。

## 実稼動プログラムの作成 {#create}

組織の使用権限によっては、プログラムを追加する際に追加の実稼動プログラムオプションが表示される場合があります。
[ その他の実稼動プログラムオプション ](#options) を参照してください。

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

1. **ソリューションとアドオン**&#x200B;リストボックスで、プログラムに含めるソリューションを 1 つ以上選択します。

   * 利用可能な様々なソリューションに対して 1 つ以上のプログラムが必要かどうかが不明な場合は、最も興味のあるプログラムを選択します。後で[プログラムを編集](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)することで、追加のソリューションをアクティブ化することができます。プログラム設定の推奨事項について詳しくは、[実稼動プログラムの概要ドキュメント](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md)を参照してください。
   * プログラムを作成するには、少なくとも 1 つのソリューションが必要です。
   * デジタルエクスペリエンスを最適化する完全に管理された CDN ソリューションの場合は、**Edge Delivery Services** を選択します。詳しくは、[Edge Delivery Services を使用した Cloud Manager プロジェクトの配信について](#edge-overview)を参照してください。
   * 「**[セキュリティの強化を有効にする](#security)**」オプションを選択した場合は、HIPAA 資格が使用可能なソリューションのみを選択できます。

     ![ソリューションの選択](/help/implementing/cloud-manager/assets/add-production-program-with-edge.png)

   * ソリューション名の左にある ![山形サイズ 300 アイコン](https://spectrum.adobe.com/static/icons/ui_18/ChevronSize300.svg) をクリックすると、オプションのアドオンが表示されます（**Sites** の下の「**Commerce**」アドオンオプションなど）。

   ![アドオンを選択](assets/setup-prod-commerce.png)

1. ソリューションとアドオンの選択が完了したら、「**続行**」をクリックします。

1. 「**開始日**」タブで、実稼動プログラムの運用開始予定日を入力します。

   ![運用開始予定日の定義](assets/set-up-go-live.png)

   * この日付はいつでも編集できます。
   * この日付は、情報として役に立ち、[**プログラムの概要**&#x200B;ページ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#program-overview)で運用開始ウィジェットをトリガーします。この機能は、AEM as a Cloud Service のベストプラクティスへのタイムリーな製品内リンクを提供して、スムーズな運用開始エクスペリエンスをサポートします。

1. 「**作成**」をクリックします。Cloud Manager によってプログラムが作成され、ランディングページに表示され、選択できるようになります。

   ![Cloud Manager の概要](assets/navigate-cm.png)

## その他の実稼動プログラムオプション {#options}

組織で使用できる使用権限によっては、実稼動プログラムの作成時に次の追加オプションを使用できる場合があります。

### セキュリティ {#security}

必要な使用資格がある場合は、「**セキュリティ**」タブが **`Set up for production`** ダイアログボックスの最初のタブとして表示されます。

![セキュリティオプション](assets/create-production-program-security.png)

「**セキュリティ**」タブには、実稼動プログラム用の **HIPAA** か **WAF-DDOS 保護**&#x200B;のどちらか一方または両方をアクティブにするオプションが表示されます。

アドビの HIPAA 準拠の WAF-DDOS（web アプリケーションファイアウォール - 分散型サービス拒否）により、脆弱性から保護するための多層アプローチの一環としてクラウドベースのセキュリティが促進されます。

* **HIPAA** - このオプションは、アドビの HIPPA 対応ソリューションの実装を有効にします。
   * アドビの HIPAA 対応ソリューションの実装について詳しくは、[こちら](https://www.adobe.com/jp/trust/compliance/hipaa-ready.html)を参照してください。
   * プログラムの作成後に HIPAA を有効または無効にすることはできません。
* **WAF-DDOS 保護** - このオプションは、ルールを介して web アプリケーションファイアウォールを有効にし、アプリケーションを保護します。
   * 有効化されると、WAF-DDOS 保護は、[実稼動以外のパイプライン](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)で設定できます。
   * リポジトリでトラフィックフィルタールールを管理し、適切にデプロイする方法について詳しくは、[WAF ルールを含むトラフィックフィルタールール](/help/security/traffic-filter-rules-including-waf.md)を参照してください。

### SLA {#sla}

必要な権限がある場合は、「**SLA**」タブは、**`Set up for production`** ダイアログで 2 番目か 3 番目のタブとして表示されます。

![SLA オプション](assets/create-production-program-sla.png)

Sites とFormsでは、99.9% の標準service level agreement（SLA）を提供しています。 「**99.99% Service level agreement**」オプションは、Sites、Forms、Edge Delivery Services、その他の 3 つの環境のいずれについても、実稼動環境の最小アップタイムを 99.99% 保証します。

99.99% SLAは、可用性の向上や待ち時間の短縮などのメリットを提供します。

Sites とFormsのプログラムの場合、99.99% のSLAをプログラムの実稼動環境に適用するには、[ 追加の公開地域 ](/help/implementing/cloud-manager/manage-environments.md#multiple-regions) が必要です。 99.99％の SLA を有効にする[要件](#sla-requirements)が満たされたら、[フルスタックパイプライン](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)を実行してアクティベートする必要があります。

Edge Delivery Servicesの場合、プログラムで 99.99% のSLA ライセンスを設定する以外に *要件はありません*。

#### 99.99％の SLA の要件 {#sla-requirements}

必要な使用権限に加えて、99.99%SLAを Sites またはForms プログラムに使用する場合、次の追加要件があります。

* 99.99％の SLA をプログラムに適用する際に、組織は 99.99％の SLA と追加の公開地域の使用権限を使用できる必要があります。
* Cloud Manager では、99.99％の SLA をプログラムに適用する前に、未使用の[追加の公開地域](/help/implementing/cloud-manager/manage-environments.md#multiple-regions)の使用権限が使用できることを確認します。
* プログラムを編集する際、1 つ以上の追加の公開地域がある実稼動環境が既に含まれている場合、Cloud Manager では 99.99％の SLA 使用権限が使用可能かどうかのみを確認します。
* 99.99％の SLA とレポートのアクティベーションの場合は、[実稼動環境／ステージ環境](/help/implementing/cloud-manager/manage-environments.md#adding-environments)が作成され、1 つ以上の追加の公開地域が実稼動環境／ステージ環境に適用されている必要があります。
   * [高度なネットワーク](/help/security/configuring-advanced-networking.md)を使用している場合は、地域に障害が発生した場合でも接続を維持できるように、[新しい環境への複数の公開地域の追加](/help/implementing/cloud-manager/manage-environments.md#adding-regions)ドキュメントで推奨事項を必ず確認してください。
* 99.99% SLA プログラムには、常に 1 つ以上の公開地域を含める必要があります。 ユーザーは、最後に残っている追加公開地域をプログラムから削除することはできません。
* 99.99% SLAは、Sites またはForms ソリューションが有効になっている実稼動プログラムでサポートされています。
* 99.99％の SLA は、[フルスタックパイプライン](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)を実行してアクティベートするか、プログラム編集時にアクティベート解除します。

## プログラムへのアクセス {#accessing}

1. ランディングページにプログラムカードが表示されたら、![その他アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックして、使用可能なメニューオプションを表示します。

   ![プログラムの概要](assets/program-overview.png)

1. 「**プログラムの概要**」を選択して、Cloud Manager の&#x200B;**概要**&#x200B;ページに移動します。

1. 概要ページにあるメインのコールトゥアクションカードのガイドに従って、環境、実稼動以外のパイプライン、そして最終的に実稼動パイプラインを作成できます。

   ![プログラムの概要](assets/set-up-prod5.png)

>[!TIP]
>
>Cloud Manager の操作方法と&#x200B;**マイプログラム**&#x200B;コンソールについて詳しくは、[Cloud Manager UI の操作](/help/implementing/cloud-manager/navigation.md)を参照してください。

>[!NOTE]
>
>[サンドボックスプログラム](introduction-sandbox-programs.md#auto-creation)とは異なり、実稼動プログラムでは、Cloud Manager の適切な役割を持つユーザーがセルフサービス UI を使用してプロジェクトを作成し環境を追加する必要があります。


