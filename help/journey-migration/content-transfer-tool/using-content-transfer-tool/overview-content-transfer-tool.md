---
title: コンテンツトランスファーツールの概要
description: コンテンツトランスファーツールを使用して、オンプレミスの AEM インスタンスから AEM as a Cloud Service にコンテンツを転送する方法について説明します。
exl-id: cfc0366a-2139-4d9d-b5bc-0b65bef4013c
feature: Migration
role: Admin
source-git-commit: e73933acc3ff23d1456f03b288f2f842a6289ace
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 100%

---


# 概要 {#overview-content-transfer-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_overview"
>title="概要"
>abstract="コンテンツトランスファーツールは、アドビが開発したツールで、ソース AEM インスタンス（オンプレミスまたは AMS）からターゲット AEM Cloud Service インスタンスへの既存のコンテンツの移行を開始するために使用できます。 グループも自動的に転送されます。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=ja" text="ガイドラインとベストプラクティス"

コンテンツトランスファーツールは、アドビが開発したツールで、ソース AEM インスタンス（オンプレミスまたは AMS）からターゲット AEM Cloud Service インスタンスへの既存のコンテンツの移行を開始するために使用できます。

グループも自動的に転送されます。詳しくは、[グループの移行](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md)を参照してください。

コンテンツトランスファーツールは、コンテンツ転送プロセスを Cloud Acceleration Manager と統合します。これにより、ユーザーは次の利点をすべて活用できます。

* セルフサービス方式で、移行セットを 1 回抽出し、同時に複数の環境に取り込めます。
* 読み込み状態、ガードレール、エラー処理の改善により、ユーザーエクスペリエンスが向上しました。
* 取り込みログは永続化され、常にトラブルシューティングに使用することができます。
* 検証およびプリンシパル移行レポートを検証に使用することができます。

## コンテンツトランスファーツールの諸段階 {#phases-content-transfer-tool}

コンテンツ転送には、次の 2 つの段階が伴います。

1. **抽出**：抽出とは、ソース AEM インスタンスから、*移行セット*&#x200B;と呼ばれる一時領域にコンテンツを抽出することです。*移行セット*&#x200B;は、アドビが提供するクラウドストレージ領域で、ソース AEM インスタンスと AEM as a Cloud Service インスタンスの間で転送されるコンテンツを一時的に保存するためのものです。

   詳しくは、[コンテンツ転送の抽出プロセス](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md)を参照してください。

1. **インジェスト**：インジェストとは、*移行セット*&#x200B;からターゲット Cloud Service インスタンスにコンテンツを取り込むことです。

   詳しくは、[コンテンツ転送の取り込みプロセス](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md)を参照してください。

## 移行セットの属性 {#attributes-migration-set}

移行セットには次の特性があります。

* 新しいバージョンでは、Cloud Acceleration Manager で作成したプロジェクト内に最大 10 の移行セットを作成できます。
* 各移行セットには、一意の名前を付ける必要があります。

コンテンツトランスファーツールには、差分コンテンツ追加をサポートする機能があります。差分追加では、前回のコンテンツ転送アクティビティ以降に加えられた変更のみを転送できます。

>[!NOTE]
>最初のコンテンツ転送の後は、差分コンテンツ追加を頻繁に行って、Cloud Service での運用を開始する前に行う最後の差分コンテンツ転送に必要なコンテンツ凍結期間を短縮することをお勧めします。

抽出段階で既存の移行セットに&#x200B;***追加***&#x200B;するには、*上書き*&#x200B;オプションを無効にする必要があります。詳しくは、[追加抽出](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process)を参照してください。

インジェストフェーズで現在のコンテンツの上に差分コンテンツを適用するには、*ワイプ*&#x200B;オプションを無効にする必要があります。詳しくは、[追加取り込み](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process)を参照してください。

## 移行セットの有効期限 {#migration-set-expiry}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_migrationset_expiry"
>title="移行セットの有効期限"
>abstract="移行セットの有効期限について説明します。"

非アクティブな状態がおよそ 45 日間続くと、すべての移行セットは最終的に期限切れになります。プロジェクトカードおよび移行ジョブテーブルの行に一定期間インジケーターが表示された後、移行セットは期限切れになり、そのデータは使用できなくなります。有効期限は、次の操作を移行セットに対して行うことで簡単に延長できます。

* 説明の編集
* 抽出キーの取得
* 抽出の実行
* 取り込みの実行

移行セット行で移行セットの有効期限を監視できます。移行セットの有効期限が近づいていることを示す便利な視覚的インジケーターが、プロジェクトのカードにも追加されました。

![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam29.png)

## 次の手順 {#whats-next}

コンテンツトランスファーツールとその概要を理解したら、[コンテンツトランスファーツールの前提条件](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/prerequisites-content-transfer-tool.md)を確認する必要があります。概要では、このツールを使用してソース AEM インスタンス（オンプレミスまたは AMS）からターゲット AEM Cloud Service インスタンスに既存のコンテンツを移行できることを説明しました。
