---
title: コンテンツ転送ツールの概要
description: コンテンツ転送ツールの概要
exl-id: 4715937e-4c4c-4680-af15-016db4fe7db9
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '858'
ht-degree: 99%

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

コンテンツ転送には、次の 2 つの段階が伴います。

1. **抽出**：抽出とは、ソース AEM インスタンスから、*移行セット*&#x200B;と呼ばれる一時領域にコンテンツを抽出することです。*移行セット*&#x200B;は、アドビが提供するクラウドストレージ領域で、ソース AEM インスタンスと AEM as a Cloud Service インスタンスの間で転送されるコンテンツを一時的に保存するためのものです。

   詳しくは、[コンテンツ転送の抽出プロセス](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#extraction-process)を参照してください。

>[!NOTE]
>
> 抽出段階の一環として、ユーザマッピングツールを実行することをお勧めします。詳しくは、[ユーザーマッピングツールの使用](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=ja#cloud-migration)を参照してください。

1. **インジェスト**：インジェストとは、*移行セット*&#x200B;からターゲット Cloud Service インスタンスにコンテンツを取り込むことです。

   詳しくは、[コンテンツ転送のインジェストプロセス](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#ingestion-process)を参照してください。

*移行セット*&#x200B;には次の特性があります。

* コンテンツ転送時に一度に作成および維持管理できる移行セットは最大 10 個です。
* 各移行セットには、一意の名前を付ける必要があります。
* 移行セットが 30 日以上非アクティブになっている場合は、自動的に削除されます。
* 移行セットは、作成すると常に特定の環境に関連付けられます。同じ環境のオーサーまたはパブリッシュインスタンスにのみ取り込むことができます。


コンテンツ転送ツールには、差分コンテンツ追加をサポートする機能があります。差分追加では、前回のコンテンツ転送アクティビティ以降に加えられた変更のみを転送できます。

>[!NOTE]
>
>最初のコンテンツ転送の後は、差分コンテンツ追加を頻繁に行って、Cloud Service での運用を開始する前に行う最後の差分コンテンツ転送に必要なコンテンツ凍結期間を短縮することをお勧めします。

抽出段階で既存の移行セットに&#x200B;***追加***&#x200B;するには、*上書き*&#x200B;オプションを無効にする必要があります。詳しくは、[追加抽出](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#top-up-extraction-process)を参照してください。

インジェストフェーズで現在のコンテンツの上に差分コンテンツを適用するには、*ワイプ*&#x200B;オプションを無効にする必要があります。詳しくは、[追加インジェスト](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#top-up-ingestion-process)を参照してください。


## ガイドラインとベストプラクティス {#best-practices}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_guidelines"
>title="ガイドラインとベストプラクティス"
>abstract="リビジョンクリーンアップタスク、ディスク容量に関する考慮事項など、コンテンツ転送ツールを使用する際のガイドラインとベストプラクティスを確認します。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=ja#pre-reqs" text="コンテンツ転送ツール使用時の重要な考慮事項"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=ja#important-considerations" text="ユーザーマッピングツール使用時の重要な考慮事項"

コンテンツ転送ツールを使用する際には、以下のガイドラインとベストプラクティスに従ってください。

* [リビジョンのクリーンアップ](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html)と[データストアの整合性チェック](https://helpx.adobe.com/jp/experience-manager/kb/How-to-run-a-datastore-consistency-check-via-oak-run-AEM.html)を&#x200B;**ソースリポジトリー**&#x200B;で実行して、潜在的な問題を特定し、リポジトリーのサイズを小さくすることをお勧めします。

* AEM as a Cloud Service オーサーのコンテンツ配信ネットワーク（CDN）に IP のホワイトリストが設定されている場合は、ソース環境と AEM as a Cloud Service 環境が相互に通信できるように、ソース環境の IP も許可リストに追加する必要があります。

* インジェスト段階では、*ワイプ*&#x200B;モードを有効にしてインジェストを実行することをお勧めします。このモードでは、ターゲット AEM as a Cloud Service 環境内の既存のリポジトリー（オーサーまたはパブリッシュ）が完全に削除された後、移行セットのデータで更新されます。このモードは、現在のコンテンツの上に移行セットが適用される非ワイプモードより、はるかに高速です。

* コンテンツ転送アクティビティが完了したら、Cloud Service 環境でコンテンツが正常にレンダリングされるように、Cloud Service 環境で正しいプロジェクト構造を使用する必要があります。

* コンテンツ転送ツールを実行する前に、ソース AEM インスタンスの `crx-quickstart` サブディレクトリに十分なディスク領域があることを確認する必要があります。これは、コンテンツ転送ツールによってリポジトリーのローカルコピーが作成され、後で移行セットにアップロードされるためです。必要な空きディスク容量を計算する一般的な式は次のとおりです。
   `data store size + node store size * 1.5`

   * *data store size*：実際のデータストアのサイズが大きい場合でも、コンテンツ転送ツールは 64 GB を使用します。
   * *node store size*：セグメントストアディレクトリのサイズまたは MongoDB データベースのサイズ。
したがって、セグメントストアのサイズが 20 GB の場合、必要な空きディスク容量は 94 GB になります。

* コンテンツ追加をサポートするには、コンテンツ転送アクティビティ全体を通して移行セットを維持管理する必要があります。コンテンツ転送アクティビティで一度に作成および維持管理できる移行セットは最大 10 個なので、コンテンツリポジトリーを適宜分割して、移行セットが不足しないようにすることをお勧めします。