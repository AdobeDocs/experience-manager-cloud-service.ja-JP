---
title: コンテンツ転送ツールにおける移行セットのログの表示
description: コンテンツ転送ツールにおける移行セットのログの表示
exl-id: aed1ac83-a2fb-425e-aca4-39cd0bb42fd3
feature: Migration
role: Admin
source-git-commit: e1089810b3bf3db0cc440bb397e5549ade6eac37
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 100%

---

# 移行セットのログの表示 {#view-logs-content-transfer-tool}


>[!CONTEXTUALHELP]
>id="aemcloud_ctt_logs"
>title="ログの表示"
>abstract="取得の抽出が完了したら、エラーや警告がないかログを確認します。エラーが発生した場合は、報告された問題を解決するかアドビサポートに連絡して、即座に対処してください。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=ja#troubleshooting" text="トラブルシューティング"
>additional-url="https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html" text="アドビサポートのご案内"

各ステップ（抽出と取り込み）が完了したら、ログを確認してエラーを探します。エラーが発生した場合は、報告された問題を解決するかアドビサポートに連絡して、即座に対処してください。

## ログを表示する手順 {#viewing-logs}

### 抽出ログ

抽出ログを表示するには、ソース Adobe Experience Manager インスタンスに移動し、必要な移行セットを選択します。

次の手順に従います。

1. 移行セットを選択し、アクションバーから「**ログを表示**」をクリックします。ログダイアログが表示されます。「**抽出ログ**」をクリックすると、ログが新しいタブに表示されます。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/logs.png) \
   または、**完了**&#x200B;ステータスをクリックして、ログを新しいタブに表示します。

1. ユーザーインターフェイスを使用せずにログの末尾を表示するには、ソース AEM 環境に SSH で接続し、`crx-quickstart/cloud-migration/extraction-XXXXX/output.log file`で tail コマンドを実行します。

### 取り込みログ

取り込みログを表示するには、Cloud Acceleration Manager の取り込みジョブリストに移動し、必要な移行ジョブを見つけて 3 つのドット（**...**）をクリックします。「**ログをダウンロード**」をクリックしてログをダウンロードします。

![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam28.png)
