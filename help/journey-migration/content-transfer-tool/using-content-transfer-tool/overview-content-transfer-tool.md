---
title: コンテンツ転送ツールの概要
description: コンテンツ転送ツールの概要
exl-id: cfc0366a-2139-4d9d-b5bc-0b65bef4013c
source-git-commit: 3bf12642e94076a67010e4701715a54138a490ee
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 72%

---

# 概要 {#overview-content-transfer-tool}


>[!CONTEXTUALHELP]
>id="aemcloud_ctt_overview"
>title="概要"
>abstract="コンテンツ転送ツールは、アドビが開発したツールで、既存のコンテンツをソース AEM インスタンス（オンプレミスまたは AMS）からターゲット AEM as a Cloud Service インスタンスに移動するためのものです。プリンシパル（ユーザーやグループ）も自動的に転送されます。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=en" text="ガイドラインとベストプラクティス"

<!-- Alexandru: Old version of contextual help, keep for failover/debugging
>[!CONTEXTUALHELP]
>id="aemcloud_ctt_overview"
>title="Overview"
>abstract="Content Transfer Tool is a tool developed by Adobe that can be used to move existing content over from a source AEM instance (on-premise or AMS) to the target AEM Cloud Service instance. This tool also transfers principals (users or groups) automatically."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#extraction-process" text="Extraction Process"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#ingestion-process" text="Ingestion Process" -->

コンテンツ転送ツールは、アドビが開発したツールで、既存のコンテンツをソース AEM インスタンス（オンプレミスまたは AMS）からターゲット AEM as a Cloud Service インスタンスに移動するためのものです。

プリンシパル（ユーザーやグループ）も自動的に転送されます。

コンテンツ転送ツールの新しいバージョンが利用でき、コンテンツ転送プロセスと Cloud Acceleration Manager が統合されています。 次の利点をすべて活用するには、この新しいバージョンに切り替えることを強くお勧めします。

* 移行セットを 1 回抽出し、同時に複数の環境に取り込むセルフサービス方法
* 読み込み状態、ガードレール、エラー処理が改善され、ユーザーエクスペリエンスが向上しました。
* 取り込みログは保持され、常にトラブルシューティングに使用できます

新しいバージョン (v2.0.10) の使用を開始するには、以下を実行します。 <!-- update when version is available --> このツールでは、アーキテクチャが大きく変更されたので、古いバージョンのコンテンツ転送ツールをアンインストールする必要があります。

>[!NOTE]
>
> 移行が既に進行中の場合は、移行が完了するまで以前のバージョンの CTT を使用し続けることができます。 以前のバージョンの CTT に関連するドキュメントについては、 [レガシードキュメント](/help/journey-migration/content-transfer-tool/ctt-legacy/overview-content-transfer-tool-legacy.md).

## コンテンツ転送ツールの諸段階 {#phases-content-transfer-tool}

コンテンツ転送には、次の 2 つの段階が伴います。

1. **抽出**：抽出とは、ソース AEM インスタンスから、*移行セット*&#x200B;と呼ばれる一時領域にコンテンツを抽出することです。*移行セット*&#x200B;は、アドビが提供するクラウドストレージ領域で、ソース AEM インスタンスと AEM as a Cloud Service インスタンスの間で転送されるコンテンツを一時的に保存するためのものです。

   詳しくは、[コンテンツ転送の抽出プロセス](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/extracting-content.html?lang=ja)を参照してください。

   >[!NOTE]
   > 抽出段階の一環として、ユーザマッピングツールを実行することをお勧めします。詳しくは、[ユーザーマッピングツールの使用](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/user-mapping-tool/using-user-mapping-tool.html?lang=ja)を参照してください。

1. **インジェスト**：インジェストとは、*移行セット*&#x200B;からターゲット Cloud Service インスタンスにコンテンツを取り込むことです。

   詳しくは、[コンテンツ転送の取り込みプロセス](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/ingesting-content.html?lang=ja)を参照してください。

## 移行セットの属性 {#attributes-migration-set}

移行セットには次の特性があります。

* 新しいバージョンでは、Cloud Acceleration Manager で作成したプロジェクト内に最大 5 つの移行セットを作成できます。
* 各移行セットには、一意の名前を付ける必要があります。

コンテンツ転送ツールには、差分コンテンツ追加をサポートする機能があります。差分追加では、前回のコンテンツ転送アクティビティ以降に加えられた変更のみを転送できます。

>[!NOTE]
>最初のコンテンツ転送の後は、差分コンテンツ追加を頻繁に行って、Cloud Service での運用を開始する前に行う最後の差分コンテンツ転送に必要なコンテンツ凍結期間を短縮することをお勧めします。

抽出段階で既存の移行セットに&#x200B;***追加***&#x200B;するには、*上書き*&#x200B;オプションを無効にする必要があります。詳しくは、[追加抽出](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/extracting-content.html?lang=ja#top-up-extraction-process)を参照してください。

インジェストフェーズで現在のコンテンツの上に差分コンテンツを適用するには、*ワイプ*&#x200B;オプションを無効にする必要があります。詳しくは、[追加インジェスト](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/ingesting-content.html?lang=ja#top-up-ingestion-process)を参照してください。

## 次の手順 {#whats-next}

コンテンツ転送ツールとその概要を理解したら、[コンテンツ転送ツールの前提条件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=ja)を確認する必要があります。概要では、このツールを使用してソース AEM インスタンス（オンプレミスまたは AMS）からターゲット AEM Cloud Service インスタンスに既存のコンテンツを移行できることを説明しました。
