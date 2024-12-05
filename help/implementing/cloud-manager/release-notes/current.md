---
title: Adobe Experience Manager as a Cloud Service の Cloud Manager 2024.12.0 のリリースノート
description: AEM as a Cloud Service の Cloud Manager 2024.12.0 のリリースについて説明します。
feature: Release Information
role: Admin
source-git-commit: ea1aa471a4fcb2ace6e4079715ac88af2d296e18
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Adobe Experience Manager as a Cloud ServiceのCloud Manager 2024.12.0 のリリースノート {#release-notes}

AEM（Adobe Experience Manager）as a Cloud Service の Cloud Manager 2024.12.0 のリリースについて説明します。

>[!NOTE]
>
>詳しくは、[Adobe Experience Manager as a Cloud Service の最新のリリースノート](/help/release-notes/release-notes-cloud/release-notes-current.md)を参照してください。

## リリース日 {#release-date}

AEM as a Cloud ServiceのCloud Manager 2024.12.0 のリリース日は 2024 年 12 月 5 日（木）です。

次回の予定リリースは 2024 年 1 月（PT）です。

## 新機能 {#what-is-new}

* **Java 21 サポート：** お客様は、オプションで Java 17 または Java 21 を使用してビルドできるようになり、パフォーマンスの向上と新しい言語機能を利用できます。 Maven プロジェクトの説明や特定のライブラリバージョンの更新を含む設定手順については、[ ビルド環境 ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md) を参照してください。 ビルドバージョンが Java 17 または Java 21 に設定されている場合、ランタイムのデフォルトは Java 21 になります。

  2025 年 2 月以降、サンドボックスと開発環境は、ビルドバージョン（Java 8、11、17、21）に関係なく、Java 21 ランタイムにアップグレードされます。 実稼動環境は、2025 年 4 月のアップグレードに続きます。

* **レコードタイプ：** AEM Cloud Managerの CDN 設定を使用してドメインの運用開始準備を改善するために、レコードタイプのサポートが追加されました。 CNAME レコードタイプまたは Fastly の IP を表す A レコードタイプを追加して、ドメインのルーティングを簡素化することで、運用を開始するオプションが追加されました。 この機能強化により、Fastly でのドメイン設定を CNAME レコードのみに依存するという制限がなくなります。

  [ カスタムドメイン名の追加 ](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) を参照してください。<!-- CMGR-63076 -->

* **Edge Delivery サイトへの複数のドメインの追加：** apex ドメインと non-apex ドメインの両方を含む複数のドメインを、AEM Cloud ManagerのEdge Delivery サイト（EDS）に追加できるようになりました。 この機能強化により、複数のドメインを EDS オリジンに関連付ける機能を制限していた以前の制限が解決されました。 この更新により、ドメイン設定を柔軟に管理できるようになり、複雑なドメイン設定を含むサイトの運用開始プロセスが簡素化されます。<!-- CMGR-63007 -->

* **高度なフィルタリングオプション：** AEM Cloud Managerのパイプライン実行ページと SSL 証明書ページに高度なフィルタリングオプションが導入されました。 複数の条件でフィルタリングできるようになりました。関連データにすばやくアクセスでき、デプロイメントの効率が向上します。<!-- CMGR-26263 -->

   * **パイプラインアクティビティフィルタリング：** パイプラインアクティビティのフィルタリングが含まれます。これにより、特定のパイプラインアクティビティの検索結果を絞り込むことができます。 使用可能なフィルターには、パイプライン、アクション、ステータスが含まれます。
     ![ パイプラインアクティビティフィルタリング ](/help/implementing/cloud-manager/assets/filters-pipeline.png)


   * **SSL 証明書フィルタリング：** SSL 証明書フィルタリングが含まれ、特定の証明書の検索結果を絞り込むことができます。 使用可能なフィルターには、SSL 証明書の名前、所有権、ステータスが含まれます。
     ![SSL 証明書フィルタリング ](/help/implementing/cloud-manager/assets/filters-ssl-certificates.png)

## 早期導入プログラム {#early-adoption}

Cloud Manager の早期導入プログラムに参加すると、今後の機能をテストする機会を得ることができます。

### 独自の Git の導入 - GitLab と Bitbucket をサポートするようになりました {#gitlab-bitbucket}

<!-- BOTH CS & AMS -->

**独自の Git を取り込む** 機能が拡張され、GitLab や Bitbucket などの外部リポジトリがサポートされるようになりました。 この新しいサポートは、プライベートおよびエンタープライズ GitHub リポジトリに対する既存のサポートに追加されます。これらの新しいリポジトリを追加すると、パイプラインに直接リンクすることもできます。これらのリポジトリは、パブリッククラウドプラットフォーム上や、プライベートクラウドまたはインフラストラクチャ内でホストできます。また、この統合により、Adobe リポジトリと常にコード同期を行う必要がなくなり、プルリクエストをメイン分岐に結合する前に検証できるようになります。

外部リポジトリ（GitHub でホストされているリポジトリを除く）と **Git の変更時** に設定された **デプロイメントトリガー** を使用したパイプラインが自動的に開始されるようになりました。

[Cloud Manager でのプライベートリポジトリの追加](/help/implementing/cloud-manager/managing-code/external-repositories.md)を参照してください。

![リポジトリを追加ダイアログボックス](/help/implementing/cloud-manager/release-notes/assets/repositories-add-release-notes.png)

>[!NOTE]
>
>現在、標準のプルリクエストコード品質チェックは、GitHub でホストされるリポジトリ専用ですが、この機能を他の Git ベンダーに拡張する更新が進行中です。

この新機能をテストしてフィードバックを共有することに興味がある場合は、Adobe ID に関連付けられたメールアドレスから [Grp-CloudManager_BYOG@adobe.com](mailto:Grp-CloudManager_BYOG@adobe.com) にメールを送信します。使用する Git プラットフォームと、プライベート／パブリックまたはエンタープライズリポジトリ構造のいずれを使用するかを必ず含めてください。

## バグ修正

* AEM Cloud Managerでアクティブなドメインマッピングが設定されたドメインが削除されるのを防ぐためのセーフガードが追加されました。 このようなドメインを削除しようとすると、ドメインの削除を続行する前にドメインマッピングを削除するよう指示するエラーメッセージが表示されるようになりました。 このワークフローは、ドメインの整合性を確保し、誤った設定を防ぎます。<!-- CMGR-63033 -->
* まれに、それぞれのケースに関連付けられているステータスが正しくないため、ユーザーがドメイン名を追加したり、SSL 証明書を更新したりできませんでした。<!-- CMGR-62816 -->


<!-- ## Known issues {#known-issues} -->