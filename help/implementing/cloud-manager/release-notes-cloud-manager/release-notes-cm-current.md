---
title: AEM as a Cloud Service Release 2021.8.0 Cloud Manager のリリースノート
description: AEM as a Cloud Service Release 2021.8.0 Cloud Manager のリリースノート
feature: リリース情報
exl-id: 42cc9cab-6e66-4976-a3b1-ecb9dbaaabf4
source-git-commit: 05cd993df7293691a0f8b91e9bde278ec7b7af69
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Adobe Experience Manager as a Cloud Service 2021.8.0 の Cloud Manager のリリースノート {#release-notes}

このページでは、AEM as a Cloud Service Release 2021.8.0 Cloud Manager のリリースノートの概要を説明しています。

>[!NOTE]
>Adobe Experience Manager as a Cloud Service の最新のリリースノートを参照するには、[こちら](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=ja)をクリックしてください。

## リリース日 {#release-date}

AEM as aCloud Service2021.8.0のCloud Managerのリリース日は2021年8月12日です。
次回のリリースは2021年9月9日に予定されています。

### 新機能 {#what-is-new}

* Cloud Serviceのお客様は、Cloud Managerでサービスレベル契約(SLA)レポートを表示できるようになりました。 これは今後数ヶ月間徐々に利用可能になる予定です。

* IndexTypeと`IndexDamAssetLucene`品質ルールの種類と重大度が変更されました。 現在は、これらは&#x200B;*サーバー性*&#x200B;のブロッカーのバグです。

* 非同期およびtikaの設定をカバーする新しいOakインデックス品質ルールが導入されました。

* プログラムごとの最大SSL証明書数を50に増やします。

* ユーザーがCloud Manager UIを使用して複数のリポジトリを作成および管理できるセルフサービス機能。

* SonarQubeがGitの履歴データを不必要に読み取っていた問題を修正しました。 大規模なコードベースでは、これにより、不要なビルドパフォーマンスの低下が生じる可能性があります。

* パイプラインごとにMaven依存関係キャッシュを無効にするAPIが追加されました。

* Cloud Manager で使用される AEM プロジェクトアーキタイプのバージョンが 28 に更新されました。

### バグ修正 {#bug-fixes}

* 最新のリリースが現在のリリースより少ない場合は、「利用可能な更新」ステータスが表示されない。

* 名前が非常に長い新しい組織で、最初のオンボーディングが失敗していました。

* 何らかの理由でパイプラインが2回トリガーされた場合、*はパイプライン実行ステータス*&#x200B;を更新できませんでしたが、実行の1つが失敗することがあります。


