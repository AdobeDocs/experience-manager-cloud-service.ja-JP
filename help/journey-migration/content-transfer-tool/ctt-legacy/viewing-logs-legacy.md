---
title: コンテンツ転送ツールにおける移行セットのログの表示（レガシー）
description: コンテンツ転送ツールにおける移行セットのログの表示
hide: true
hidefromtoc: true
exl-id: 01c8afd3-c594-4a41-b905-8c3a2d74db6f
source-git-commit: 22bbf15e33ab3d5608dc01ed293bb04b07cb6c8c
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 100%

---

# 移行セットのログの表示（レガシー） {#view-logs-content-transfer-tool}

各ステップ（抽出と取り込み）が完了したら、ログを確認してエラーを探します。エラーが発生した場合は、報告された問題を解決するかアドビサポートに連絡して、即座に対処してください。

## ログを表示する手順 {#viewing-logs}

既存の移行セットのログを&#x200B;*概要*&#x200B;ページから表示できます。次の手順に従います。

1. *概要*&#x200B;ページに移動し、ログを表示する移行セットを選択し、アクションバーの「**ログを表示**」をクリックします。

   ![画像](/help/journey-migration/content-transfer-tool/assets/view-log1.png)

1. **ログ**&#x200B;ダイアログボックスが表示されます。「**抽出ログ**」をクリックすると、ログが新しいタブに表示されます。

   ![画像](/help/journey-migration/content-transfer-tool/assets/view-log2.png)
または、

   *概要*&#x200B;画面から移行セットのログを直接表示することもできます。移行セットを選択し、「**抽出**」フィールド内のステータスをクリックします。下図の場合は、「**完了**」をクリックすると、ログが新しいタブに表示されます。

   ![画像](/help/journey-migration/content-transfer-tool/assets/view-log3.png)

1. ユーザーインターフェイスを使用せずにログの末尾を表示するには、ソース AEM 環境に SSH で接続し、`crx-quickstart/cloud-migration/extraction-XXXXX/output.log file`で tail コマンドを実行します。
