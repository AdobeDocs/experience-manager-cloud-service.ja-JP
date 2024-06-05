---
title: コンテンツ変換サービスの概要
description: コンテンツ変換サービスを使用して BPA で報告される、コンテンツ関連の問題を検出および修正する方法について説明します。
exl-id: aa3397ff-3dd6-4c67-9064-cb9b19bf1c73
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 100%

---

# 概要 {#overview-ct}

コンテンツ変換サービス（CT）は、アドビが開発したツールです。現在の AEM 実装（オンプレミスまたは Managed Services）から AEM as a Cloud Service にコンテンツを移行する前に、[ベストプラクティスアナライザー（BPA）](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md)によって報告されたコンテンツに関連する問題を自動的に検出および修正するために使用できます。

コンテンツ変換サービスは、移動や削除などの一括アクションを実行できるようにすることで、次の [BPA パターンカテゴリ](https://experienceleague.adobe.com/docs/experience-manager-pattern-detection/table-of-contents/aso.html?lang=ja)（以下の表に参照）に該当する問題の解決に役立ちます。これにより、時間を大幅に短縮し、移行プロジェクトに関連する複雑さを軽減できます。

## コンテンツ変換サービスでカバーされるパターンカテゴリと推奨ソリューション {#pattern-categories-and-benefits}

| パターンコード | 疑いのタイプ／サブタイプ | コンテンツを AEM as a Cloud Service に移行する前の潜在的な修正 |
|--------------|--------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| ACV | missing.jcrcontent <br> missing.original.rendition <br> metadata.descendants.violation | これらのアセットを別の場所に移動するか、または削除して AEM as a Cloud Service に移行されないようにします。 |
| CAV | content.area.violation | パスを一時的に `/etc/packages/content-transformation/paths` に移動して、AEM as a Cloud Service に移行されないようにします。 |
| DOPI | deprecated.ordered.index | 非推奨のインデックスを削除します。 |
| OAUI | non.migrated.oauth.users | これらのユーザーを削除して、AEM as a Cloud Service に移行されないようにします。 |
| PCX | page.complexity.medium <br> page.complexity.high | ページ／子を削除するか、または別の場所に移動して AEM as a Cloud Service に移行されないようにします。 |
| REP | forward.replication <br> reverse.replication <br> standard.replication.agent.modification <br> custom.replication.agent.detection | 作成したレプリケーションエージェントを削除します。<br> または <br> 変更または追加したプロパティを削除します。 |
| URS | clientlibs.location <br> file.location <br> node.location <br> workflow.location | 正しい場所に移動して、移行中の問題を回避します。 |
| URS | node.size | ノードを一時的に `/etc/packages/content-transformation/paths` に移動し、AEM as a Cloud Service に移行されないようにします。 |

## コンテンツ変換サービスが提供するメリット {#benefits}

コンテンツ変換サービスには次のようなメリットがあります。

* フェイルセーフ：問題を修正しようとリポジトリを変更するたびに、コンテンツ変換サービスによってパッケージが作成されます。必要に応じて、パッケージをインストールして前の状態に戻すことができます。
* 使いやすさ：コンテンツ変換サービスは、コンテンツ転送ツールに統合され、直感的なシンプルなユーザーインターフェイスを備えています。
* 時間を節約：1 つのパターンカテゴリに分類されるコンテンツの問題が多数ある場合、コンテンツ変換サービスを使用すると、数回クリックするだけですべての問題を解決できます。
