---
title: コンテンツ転送ツールの概要
description: コンテンツ転送ツールの概要
exl-id: 4715937e-4c4c-4680-af15-016db4fe7db9
source-git-commit: f9becda129472f669a4d4511fc158e49be5d34d7
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 75%

---

# 概要 {#overview-content-transfer-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_overview"
>title="概要"
>abstract="コンテンツ転送ツールは、アドビが開発したツールで、既存のコンテンツをソース AEM インスタンス（オンプレミスまたは AMS）からターゲット AEM as a Cloud Service インスタンスに移動するためのものです。プリンシパル（ユーザーやグループ）も自動的に転送されます。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=ja#extraction-process" text="抽出プロセス"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=ja#ingestion-process" text="取り込みプロセス"

コンテンツ転送ツールは、アドビが開発したツールで、既存のコンテンツをソース AEM インスタンス（オンプレミスまたは AMS）からターゲット AEM as a Cloud Service インスタンスに移動するためのものです。

プリンシパル（ユーザーやグループ）も自動的に転送されます。

## コンテンツ転送ツールのフェーズ {#phases-content-transfer-tool}

コンテンツ転送には、次の 2 つの段階が伴います。

1. **抽出**：抽出とは、ソース AEM インスタンスから、*移行セット*&#x200B;と呼ばれる一時領域にコンテンツを抽出することです。*移行セット*&#x200B;は、アドビが提供するクラウドストレージ領域で、ソース AEM インスタンスと AEM as a Cloud Service インスタンスの間で転送されるコンテンツを一時的に保存するためのものです。

   詳しくは、[コンテンツ転送の抽出プロセス](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/extracting-content.html)を参照してください。

   >[!NOTE]
   > 抽出段階の一環として、ユーザマッピングツールを実行することをお勧めします。詳しくは、[ ユーザーマッピングツールの使用 ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/user-mapping-tool/using-user-mapping-tool.html) を参照してください。

1. **インジェスト**：インジェストとは、*移行セット*&#x200B;からターゲット Cloud Service インスタンスにコンテンツを取り込むことです。

   詳しくは、[ コンテンツ転送のインジェストプロセス ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/ingesting-content.html) を参照してください。

## 移行セットの属性 {#attributes-migration-set}

移行セットには次の特性があります。

* コンテンツ転送時に一度に作成および維持管理できる移行セットは最大 10 個です。
* 各移行セットには、一意の名前を付ける必要があります。
* 移行セットが 30 日以上非アクティブになっている場合は、自動的に削除されます。
* 移行セットは、作成すると常に特定の環境に関連付けられます。同じ環境のオーサーまたはパブリッシュインスタンスにのみ取り込むことができます。


コンテンツ転送ツールには、差分コンテンツ追加をサポートする機能があります。差分追加では、前回のコンテンツ転送アクティビティ以降に加えられた変更のみを転送できます。

>[!NOTE]
>最初のコンテンツ転送の後は、差分コンテンツ追加を頻繁に行って、Cloud Service での運用を開始する前に行う最後の差分コンテンツ転送に必要なコンテンツ凍結期間を短縮することをお勧めします。

抽出段階で既存の移行セットに&#x200B;***追加***&#x200B;するには、*上書き*&#x200B;オプションを無効にする必要があります。詳しくは、[追加抽出](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/extracting-content.html?lang=en#top-up-extraction-process)を参照してください。

インジェストフェーズで現在のコンテンツの上に差分コンテンツを適用するには、*ワイプ*&#x200B;オプションを無効にする必要があります。詳しくは、[追加インジェスト](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/ingesting-content.html?lang=en#top-up-ingestion-process)を参照してください。

## 次の手順 {#whats-next}

コンテンツ転送ツールの概要と、このツールを使用して既存のコンテンツをソースAEMインスタンス（オンプレミスまたは AMS）からターゲットAEM Cloud Serviceインスタンスに移動する方法を学習したら、[ コンテンツ転送ツールの前提条件 ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=en) を確認する必要があります。

