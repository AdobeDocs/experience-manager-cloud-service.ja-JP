---
title: コンテンツ転送ツールでの移行セットのログの表示
description: コンテンツ転送ツールでの移行セットのログの表示
source-git-commit: bcbf4e4ba1330bef9f2c8c473419903e40ac0e58
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 89%

---


# 移行セットのログの表示 {#view-logs-content-transfer-tool}


>[!CONTEXTUALHELP]
>id="aemcloud_ctt_logs"
>title="ログの表示"
>abstract="取得の抽出が完了したら、エラーや警告がないかログを確認します。エラーが発生した場合は、報告された問題を解決するかアドビサポートに連絡して、即座に対処してください。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=ja#troubleshooting" text="トラブルシューティング"
>additional-url="https://helpx.adobe.com/ca/enterprise/admin-guide.html/ca/enterprise/using/support-for-experience-cloud.ug.html" text="アドビサポートのご案内"

各ステップ（抽出と取り込み）が完了したら、ログを確認してエラーを探します。エラーが発生した場合は、報告された問題を解決するかアドビサポートに連絡して、即座に対処してください。

## ログの表示手順 {#viewing-logs}

既存の移行セットのログを&#x200B;*概要*&#x200B;ページから表示できます。それには、次の手順に従います。

1. *概要*&#x200B;ページに移動し、ログを表示する移行セットを選択し、アクションバーの「**ログを表示**」をクリックします。

   ![画像](/help/journey-migration/content-transfer-tool/assets/view-log1.png)

1. **ログ**&#x200B;ダイアログボックスが表示されます。「**抽出ログ**」をクリックすると、ログが新しいタブに表示されます。

   ![画像](/help/journey-migration/content-transfer-tool/assets/view-log2.png)
または、

   *概要*&#x200B;画面から移行セットのログを直接表示することもできます。移行セットを選択し、「**抽出**」フィールド内のステータスをクリックします。下図の場合は、「**完了**」をクリックすると、ログが新しいタブに表示されます。

   ![画像](/help/journey-migration/content-transfer-tool/assets/view-log3.png)

1. ユーザーインターフェイスを使用せずにログの末尾を表示するには、ソース AEM 環境に SSH で接続し、`crx-quickstart/cloud-migration/extraction-XXXXX/output.log file`で tail コマンドを実行します。
