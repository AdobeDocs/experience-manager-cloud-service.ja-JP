---
title: AEM as a Cloud Service Release 2021.8.0 Cloud Manager のリリースノート
description: AEM as a Cloud Service Release 2021.8.0 Cloud Manager のリリースノート
feature: Release Information
source-git-commit: 11910316836b33e886aeba84f89d1b2eebfe7de2
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 61%

---

# Adobe Experience Manager as a Cloud Service 2021.8.0 の Cloud Manager のリリースノート {#release-notes}

このページでは、AEM as a Cloud Service Release 2021.8.0 Cloud Manager のリリースノートの概要を説明しています。

>[!NOTE]
>Adobe Experience Manager as a Cloud Service の最新のリリースノートを参照するには、[こちら](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=ja)をクリックしてください。

## リリース日 {#release-date}

AEM as aCloud Service2021.8.0のCloud Managerのリリース日は2021年8月12日です。

### 新機能 {#what-is-new}

* Cloud Serviceのお客様は、Cloud Managerでサービスレベル契約(SLA)レポートを表示できるようになりました。 これは今後数ヶ月間徐々に利用可能になる予定です。
詳しくは、[SLAレポート](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sla-reporting.html)を参照してください。

* IndexTypeと`IndexDamAssetLucene`品質ルールの種類と重大度が変更されました。 現在は、これらは&#x200B;*サーバー性*&#x200B;のブロッカーのバグです。

* 非同期およびtikaの設定をカバーする新しいOakインデックス品質ルールが導入されました。

* プログラムごとの最大SSL証明書数を50に増やします。

* ユーザーが Cloud Manager UI を使用して複数のリポジトリを作成および管理できるセルフサービス機能。

* SonarQubeがGitの履歴データを不必要に読み取っていた問題を修正しました。 大規模なコードベースでは、これにより、ビルドパフォーマンスが不必要に低下することがありました。

* パイプラインごとに Maven 依存関係キャッシュを無効にする API が追加されました。

* Cloud Manager で使用される AEM プロジェクトアーキタイプのバージョンが 29 に更新されました。

### バグ修正 {#bug-fixes}

* 最新のリリースが現在のリリースより前の場合は、更新可能ステータスは表示されるべきではありません。

* 名前が非常に長い新しい組織で、最初のオンボーディングが失敗していました。

* 何らかの理由でパイプラインが 2 回トリガーされた場合、「*パイプライン実行ステータスを更新できませんでした*」エラーで、いずれかの実行が失敗します。
