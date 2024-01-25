---
title: 実稼動プログラムの作成
description: Cloud Manager を使用して、ライブトラフィックをホストする独自の実稼動プログラムを作成する方法について説明します。
exl-id: 4ccefb80-de77-4998-8a9d-e68d29772bb4
source-git-commit: a25f1c674534792353cb9b34d4f88a5e32230bc1
workflow-type: tm+mt
source-wordcount: '1047'
ht-degree: 46%

---


# 実稼動プログラムの作成 {#create-production-program}

実稼動プログラムの対象ユーザーは、AEM と Cloud Manager に精通し、ライブトラフィックをホストするためにコードをデプロイする目的でコードの作成、ビルドおよびテストを開始する準備が整っているユーザーです。

プログラムの種類について詳しくは、[プログラムとプログラムの種類について](program-types.md)のドキュメントを参照してください。

## 実稼動プログラムの作成 {#create}

実稼動プログラムを作成するには、次の手順に従います。 お客様の組織の使用権限に応じて、 [その他のオプション](#options) プログラムを追加する際に使用します。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. 次の日： **[マイプログラム](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#my-programs)** 画面、タップまたはクリック **プログラムの追加** をクリックします。

   ![Cloud Manager ランディングページ](assets/log-in.png)

1. プログラムを作成ウィザードで「**実稼動用に設定**」を選択して、実稼動プログラムを作成し、プログラム名を指定します。

   ![プログラム作成ウィザード](assets/create-production-program.png)

1. オプションとして、画像ファイルを&#x200B;**プログラム画像を追加**&#x200B;のターゲットにドラッグ＆ドロップするか、ファイルブラウザーからクリックして画像を選択することで、プログラムに画像を追加できます。「**続行**」を選択します。

1. 「**ソリューションとアドオン**」タブで、プログラムに含めるソリューションを選択します。

   * 利用可能な様々なソリューションに対して 1 つ以上のプログラムが必要かどうかが不明な場合は、最も興味のあるプログラムを選択します。後で[プログラムを編集](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)することで、追加のソリューションをアクティブ化することができます。プログラム設定の推奨事項について詳しくは、[実稼動プログラムの概要ドキュメント](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md)を参照してください。
   * プログラムを作成するには、少なくとも 1 つのソリューションが必要です。
   * 次を選択した場合、 **[拡張セキュリティの有効化](#security)** 」オプションを使用する場合、HIPAA 使用権限を持つソリューションを選択できる数に制限はありません。

   ![ソリューションを選択](assets/setup-prod-select.png)

1. ソリューション名の前の山形記号をクリックすると、オプションのアドオンが表示されます。例えば、**Sites** で **Commerce** アドオンオプションを選択できます。

   ![アドオンを選択](assets/setup-prod-commerce.png)

1. ソリューションやアドオンを選択してから、「**続行**」をクリックします。

1. 「**開始日**」タブで、実稼動プログラムの運用開始予定日を入力します。

   ![運用開始予定日の定義](assets/setup-go-live.png)

   * この日付はいつでも編集できます。
   * この日付は、情報提供のみを目的とし、Go Live ウィジェットを [**プログラムの概要** ページ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#program-overview) AEMas a Cloud Serviceのベストプラクティスドキュメントへの製品内リンクをタイムリーに提供し、Go Live の成功とスムーズな運用を実現するジャーニーに合わせます。

1. 「**作成**」をクリックします。

プログラムが Cloud Manager により作成され、ランディングページに表示されて選択可能になります。

![Cloud Manager の概要](assets/navigate-cm.png)

## その他の実稼動プログラムオプション {#options}

組織が使用できる使用権限に応じて、実稼働用プログラムの作成時に追加のオプションを使用できる場合があります。

### セキュリティ {#security}

必要な権限がある場合は、 **セキュリティ** タブが **実稼動用に設定** ダイアログ。

The **セキュリティ** 「 」タブには、アクティブにするオプションが表示されます **HIPAA** および/または **WAF-DDOS 保護** 実稼動プログラム用に作成されます。

Adobeの HIPAA 準拠と Web アプリケーションファイアウォール (WAF) は、脆弱性から保護するための多層アプローチの一環として、クラウドベースのセキュリティを促進します。

* **HIPAA**  — このオプションは、Adobeの HIPPA 対応ソリューションの実装を有効にします。
   * アドビの HIPAA 対応ソリューションの実装について詳しくは、[こちら](https://www.adobe.com/go/hipaa-ready)を参照してください。
   * プログラムの作成後に HIPAA を有効または無効にすることはできません。
* **WAF-DDOS 保護**  — このオプションは、ルールを介した Web アプリケーションファイアウォールで、アプリケーションを保護することを有効にします。
   * 有効化すると、WAF-DDOS 保護は、[実稼動以外のパイプライン](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)で設定できます。
   * リポジトリでフィックフィルタールールを管理し、適切にデプロイする方法については、[WAF ルールを含むトラフィックフィルタールール](/help/security/traffic-filter-rules-including-waf.md)を参照してください。

![セキュリティオプション](assets/create-production-program-security.png)

### SLA {#sla}

必要な権限がある場合は、 **SLA** タブは、 **実稼動用に設定** ダイアログ。

AEM Sitesは、標準の 99.9%のサービスレベル契約 (SLA) を提供しています。 The **99.99%のサービスレベル契約** 「 」オプションを使用すると、実稼動環境の 99.99%の最小稼動時間の割合が有効になります。

99.99%の SLA は、可用性の向上や待ち時間の短縮を含むメリットを提供し、 [追加の公開領域](/help/implementing/cloud-manager/manage-environments.md#multiple-regions) をプログラムの実稼動環境に適用します。

![SLA オプション](assets/create-production-program-sla.png)

1 回 [要件](#sla-requirements) 99.99%の SLA を有効にするには、 [フルスタックパイプライン](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) 有効化するために。

#### SLA 99.99%の要件 {#sla-requirements}

99.99%の SLA には、必要な権限以外にも、使用に関する追加の要件があります。

* 99.99%の SLA をプログラムに適用する際には、SLA 99.99%と追加の発行地域の使用権限の両方を組織が利用できる必要があります。
* 99.99%の SLA をプログラムに適用するために、Cloud Manager は、未使用であることを確認します [追加の公開領域](/help/implementing/cloud-manager/manage-environments.md#multiple-regions) 使用権限も使用でき、プログラムに適用できます。
* プログラムの編集時に、少なくとも 1 つの追加の公開地域がある実稼動環境が既に含まれている場合、Cloud Manager は SLA の 99.99%の権限が使用可能かどうかのみを確認します。
* 99.99%の SLA とレポートをアクティブにするには、 [実稼働/ステージ環境](/help/implementing/cloud-manager/manage-environments.md#adding-environments) が作成され、実稼動/ステージング環境に少なくとも 1 つの追加の公開領域が適用されている必要があります。
   * を使用する場合 [高度なネットワーク、](/help/security/configuring-advanced-networking.md) 必ず [新しい環境への複数のパブリッシュ領域の追加](/help/implementing/cloud-manager/manage-environments.md#adding-regions) 地域で障害が発生した場合に接続を維持するための推奨事項のドキュメントです。
* 99.99% SLA プログラムには、1 つ以上の追加の発行地域を残す必要があります。 99.99%の SLA プログラムから最後の追加の公開領域を削除することは許可されていません。
* 99.99%の SLA は、Sites ソリューションが有効になっている実稼動プログラムでサポートされています。
* 次を実行する必要があります： [フルスタックパイプライン](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) 99.99%の SLA をアクティブ化（または、プログラムの編集時に非アクティブ化）するため。

## プログラムへのアクセス {#accessing}

1. ランディングページにプログラムカードが表示されたら、省略記号（...）ボタンを選択して、使用可能なメニューオプションを表示します。

   ![プログラムの概要](assets/program-overview.png)

1. 「**プログラムの概要**」を選択して、Cloud Manager の&#x200B;**概要**&#x200B;ページに移動します。

1. 概要ページのメインコールトゥアクションカードのガイドに従って、環境、実稼動以外のパイプライン、そして最終的に実稼動パイプラインを作成できます。

   ![プログラムの概要](assets/set-up-prod5.png)

別のプログラムに切り替えたり、概要ページに戻って別のプログラムを作成したりする必要がある場合は、いつでも画面の左上のプログラム名をクリックして「**移動先**」オプションを表示します。

![](assets/create-program-a1.png) に移動します。

>[!NOTE]
>
>[サンドボックスプログラム](introduction-sandbox-programs.md#auto-creation)とは異なり、実稼動プログラムでは、Cloud Manager の適切な役割を持つユーザーがセルフサービス UI を使用してプロジェクトを作成し環境を追加する必要があります。
