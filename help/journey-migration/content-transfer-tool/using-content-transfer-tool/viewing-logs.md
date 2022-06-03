---
title: コンテンツ転送ツールにおける移行セットのログの表示
description: コンテンツ転送ツールにおける移行セットのログの表示
exl-id: aed1ac83-a2fb-425e-aca4-39cd0bb42fd3
source-git-commit: 9a098eefbb730ae2930169cf7402ab4799043291
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 59%

---

# 移行セットのログの表示 {#view-logs-content-transfer-tool}


>[!CONTEXTUALHELP]
>id="aemcloud_ctt_logs"
>title="ログの表示"
>abstract="取得の抽出が完了したら、エラーや警告がないかログを確認します。エラーが発生した場合は、報告された問題を解決するかアドビサポートに連絡して、即座に対処してください。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=ja#troubleshooting" text="トラブルシューティング"
>additional-url="https://helpx.adobe.com/jp/enterprise/admin-guide.html/jp/enterprise/using/support-for-experience-cloud.ug.html" text="アドビサポートのご案内"

各ステップ（抽出と取り込み）が完了したら、ログを確認してエラーを探します。エラーが発生した場合は、報告された問題を解決するかアドビサポートに連絡して、即座に対処してください。

## ログを表示する手順 {#viewing-logs}

抽出ログを表示するには、ソースAdobe Experience Managerインスタンスに移動し、必要な移行セットを選択します。

次に、次の手順に従います。

1. 移行セットを選択し、 **ログを表示** をクリックします。 ログダイアログが表示されます。 クリック **抽出ログ** ログを新しいタブに表示します。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam25.png) \
   または、 **完了** ステータスを使用して、ログを新しいタブに表示できます。

1. ユーザーインターフェイスを使用せずにログの末尾を表示するには、ソース AEM 環境に SSH で接続し、`crx-quickstart/cloud-migration/extraction-XXXXX/output.log file`で tail コマンドを実行します。

1. 取り込みログを表示するには、Cloud Acceleration Manager の取り込みジョブリストに移動し、3 つのドット (**...**) をクリックします。 次の項目をクリックすると、 **ログをダウンロード** ログをダウンロードします。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam28.png)
