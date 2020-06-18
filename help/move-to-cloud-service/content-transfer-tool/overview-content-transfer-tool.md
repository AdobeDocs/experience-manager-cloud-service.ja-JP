---
title: コンテンツ転送ツールの概要
description: コンテンツ転送ツールの概要
translation-type: tm+mt
source-git-commit: 7648adc4b1d9c5849363beb4162de2f42eac7cfd
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 69%

---


# 概要 {#overview-content-transfer-tool}

コンテンツ転送ツールは、アドビが開発したツールで、既存のコンテンツをソース AEM インスタンス（オンプレミスまたは AMS）からターゲット AEM as a Cloud Service インスタンスに移動するためのものです。

プリンシパル（ユーザーやグループ）も自動的に転送されます。

コンテンツ転送には、次の 2 つの段階が伴います。

1. **抽出**：抽出とは、ソース AEM インスタンスから、*移行セット*&#x200B;と呼ばれる一時領域にコンテンツを抽出することです。*移行セット*&#x200B;は、アドビが提供するクラウドストレージ領域で、ソース AEM インスタンスと AEM as a Cloud Service インスタンスの間で転送されるコンテンツを一時的に保存するためのものです。

   詳しくは、[コンテンツ転送の抽出プロセス](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#extraction-process)を参照してください。

2. **インジェスト**：インジェストとは、*移行セット*&#x200B;からターゲット Cloud Service インスタンスにコンテンツを取り込むことです。

   詳しくは、[コンテンツ転送のインジェストプロセス](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#ingestion-process)を参照してください。

*移行セット*&#x200B;には次の特性があります。

* コンテンツ転送時に一度に作成および維持管理できる移行セットは最大 4 つです。
* 各移行セットには、一意の名前を付ける必要があります。
* 移行セットが 30 日以上非アクティブになっている場合は、自動的に削除されます。
* 移行セットは、作成すると常に特定の環境に関連付けられます。同じ環境のオーサーまたはパブリッシュインスタンスにのみ取り込むことができます。

コンテンツ転送ツールには、差分コンテンツ追加をサポートする機能があります。差分追加では、前回のコンテンツ転送アクティビティ以降に加えられた変更のみを転送できます。

>[!NOTE]
> 最初のコンテンツ転送の後は、差分コンテンツ追加を頻繁におこなって、Cloud Service での運用を開始する前におこなう最後の差分コンテンツ転送に必要なコンテンツ凍結期間を短縮することをお勧めします。

抽出段階で既存の移行セットに&#x200B;***追加***&#x200B;するには、*上書き*&#x200B;オプションを無効にする必要があります。詳しくは、[追加抽出](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#top-up-extraction-process)を参照してください。

インジェストフェーズで現在のコンテンツの上に差分コンテンツを適用するには、*ワイプ*&#x200B;オプションを無効にする必要があります。詳しくは、[追加インジェスト](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#top-up-ingestion-process)を参照してください。


## ガイドラインとベストプラクティス {#best-practices}

コンテンツ転送ツールを使用する際には、以下のガイドラインとベストプラクティスに従ってください。

* リビジョンのクリーンアップ [と](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/deploying/revision-cleanup.html) データストアの整合性チェックを [](https://helpx.adobe.com/experience-manager/kb/How-to-run-a-datastore-consistency-check-via-oak-run-AEM.html)**** ソースリポジトリで実行して、潜在的な問題を特定し、リポジトリのサイズを小さくすることをお勧めします。

* AEM Cloud Author Content Network(CDN)の設定でIPのホワイトリストが設定されている場合は、ソース環境とAEM Cloud環境が相互に通信できるように、ソース環境IPも許可リストに追加する必要があります。

* インジェスト段階では、*ワイプ*&#x200B;モードを有効にしてインジェストを実行することをお勧めします。このモードでは、ターゲット AEM as a Cloud Service 環境内の既存のリポジトリ（オーサーまたはパブリッシュ）が完全に削除された後、移行セットのデータで更新されます。このモードは、現在のコンテンツの上に移行セットが適用される非ワイプモードより、はるかに高速です。

* コンテンツ転送アクティビティが完了したら、Cloud Service 環境でコンテンツが正常にレンダリングされるように、Cloud Service 環境で正しいプロジェクト構造を使用する必要があります。

* コンテンツ転送ツールを実行する前に、ソースAEMインスタンスの `crx-quickstart` サブディレクトリに十分なディスク領域があることを確認する必要があります。 これは、コンテンツ転送ツールによってリポジトリのローカルコピーが作成され、後で移行セットにアップロードされるためです。
必要な空きディスク容量を計算する一般的な式は次のとおりです。
   `data store size + node store size * 1.5`

   * *data store size*: 実際のデータストアのサイズが大きい場合でも、コンテンツ転送ツールは64 GBを使用します。
   * *ノードストアのサイズ*: セグメントストアディレクトリのサイズまたはMongoDBデータベースのサイズ。
したがって、セグメントストアのサイズが20 GBの場合、必要な空きディスク容量は94 GBになります。