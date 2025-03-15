---
title: Adobe Experience Manager as a Cloud Service の Cloud Manager 2025.3.0 のリリースノート
description: AEM as a Cloud Service の Cloud Manager 2025.3.0 のリリースについて説明します。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 5983c8579dd8606bc8bedfe6fa2a3838493452cd
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 31%

---

# Adobe Experience Manager as a Cloud Service の Cloud Manager 2025.3.0 のリリースノート {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.03.0+Release -->

AEM（Adobe Experience Manager）as a Cloud Service の Cloud Manager 2025.3.0 のリリースについて説明します。


[Adobe Experience Manager as a Cloud Service の最新のリリースノート](/help/release-notes/release-notes-cloud/release-notes-current.md)も参照してください。

## リリース日 {#release-date}

AEM as a Cloud Service の Cloud Manager 2025.3.0 のリリース日は 2025年3月13日木曜日（PT）です。

次回のリリース予定は 2025年4月10日木曜日（PT）です。

## 新機能 {#what-is-new}

* **複数のパイプラインの実行**

  パイプライン ページに複数のパイプラインを同時に実行する機能が導入されました。 ユーザーは、1 つ以上 10 以下のパイプラインを選択する必要があります。 パイプライン ページの右上隅付近にある「**選択した実行（x）**」をクリックします。 モーダルダイアログボックスが表示され、開始できないパイプラインが一覧表示されます。 **実行** をクリックして、有効なすべてのパイプラインを開始します。

  ![ 選択したパイプラインを実行ダイアログボックス ](/help/implementing/cloud-manager/release-notes/assets/run-selected-pipelines.png)

* **Node.js バージョンのサポートが拡張されました**

  フロントエンドビルド環境で、次の `Node.js` バージョンがサポートされるようになりました。

   * 23
   * 22
   * 20

  [ フロントエンドパイプラインを使用したサイトの開発 ](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md#node-versions) も参照してください。<!-- CMGR-65307 -->

<!--
## Early adoption program {#early-adoption}

Be a part of Cloud Manager's early adoption program and have a chance to test upcoming features. -->


## バグ修正

* Cloud Managerの「高度なネットワーク設定」アップデートの **（UI）修正**

  「利用可能な更新 **通知が存在する場合に** 高度なネットワーク設定」の更新が行えなかったまれな問題が解決されました。 以前は、更新中の競合を防ぐために、Cloud Managerによって、高度なネットワーク設定などの設定変更がロックされていました。 保留中の更新を手動でトリガーして、必要な変更を制限なく適用できるようになりました。<!-- CMGR-65913 and CMGR-65788 -->

* **（UI） IP許可リストの更新が「更新中」ステータスでスタックする問題を修正**

  ある環境でアクティブなドメイン設定が重複していたことが原因で、Cloud Managerの IP 許可リストの更新が「更新中」ステータスのままになる、まれな問題が解決されました。 以前は、IP許可リストを更新する際に無限の処理遅延が発生し、必要なネットワークアクセスの調整が妨げられていました。 この修正により、IP 許可リストの更新が停止することなく正常に完了できるようになりました。<!-- CMGR-65786 -->




<!-- ## Known issues {#known-issues} -->
