---
title: Content Transformer の概要
description: Content Transformer の概要
source-git-commit: 55eedd342f048e19bad5c6fbfdd16a468ff1f4f9
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 4%

---

# 概要 {#overview-ct}

コンテンツトランスフォーマー (CT) は、Adobeが開発したツールで、 [ベストプラクティスアナライザー (BPA)](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md) 現在のAEM実装 ( オンプレミスまたはManaged Services) からAEM as a Cloud Serviceにコンテンツを移行する前に。

Content Transformer は、次に該当する問題の解決に役立ちます [BPA パターンカテゴリ](https://experienceleague.adobe.com/docs/experience-manager-pattern-detection/table-of-contents/aso.html?lang=ja) （以下の表を参照）移動や削除などの一括アクションを実行できるようにします。 これにより、時間を大幅に短縮し、移行プロジェクトに関連する複雑さを軽減できます。

## コンテンツ変換サービスでカバーされるパターンカテゴリと推奨ソリューション {#pattern-categories-and-benefits}

| パターンコード | 疑いのタイプ/サブタイプ | コンテンツをAEM as a Cloud Serviceに移行する前の潜在的な修正 |
|--------------|--------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| ACV | missing.jcrcontent <br> missing.original.rendition <br> metadata.descendants.violation | これらのアセットを別の場所に移動するか、削除して、AEM as a Cloud Serviceに移行されないようにします。 |
| CAV | content.area.violation | パスを一時的に移動 `/etc/packages/content-transformation/paths` AEM as a Cloud Serviceに移行されないようにするために使用します。 |
| DOPI | deprecated.ordered.index | 非推奨のインデックスを削除します。 |
| OAUI | non.migrated.oauth.users | これらのユーザーを削除して、AEM as a Cloud Serviceに移行されないようにします。 |
| PCX | page.complexity.medium <br> page.complexity.high | ページ/子を削除するか、別の場所に移動して、AEM as a Cloud Serviceに移行されないようにします。 |
| REP | forward.replication <br> reverse.replication <br> standard.replication.agent.modification <br> custom.replication.agent.detection | 新しく作成したレプリケーションエージェントを削除します。 <br> または <br> 変更または追加したプロパティを削除します。 |
| URS | clientlibs.location <br> file.location <br> node.location <br> workflow.location | 移行中の問題を回避するには、正しい場所に移動してください。 |
| URS | node.size | ノードを一時的に次の場所に移動`/etc/packages/content-transformation/paths` AEM as a Cloud Serviceに移行されないようにするために使用します。 |

## Content Transformer が提供するメリット {#benefits}

Content Transformer には次のような利点があります。

* フェイルセーフ：パッケージは、問題を修正するためにリポジトリを変更するたびに、Content Transformer によって作成されます。 必要に応じて、パッケージをインストールして前の状態に戻すことができます。
* 使いやすさ：Content Transformer は、コンテンツ転送ツールに統合され、直感的なシンプルなユーザーインターフェイスを備えています。
* 時間を節約：1 つのパターンカテゴリに該当するコンテンツの問題が多数ある場合、Content Transformer を使用して、数回クリックするだけですべての問題を解決できます。
