---
title: Edge Delivery サイト用のプッシュ無効化の設定
description: 効率的なコンテンツ更新とキャッシュコントロールを確保するために、Edge Delivery サイトのプッシュ無効化を設定する方法について説明します。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
exl-id: 7cded93c-325c-4a4b-8644-e6a2379d5179
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 100%

---

# プッシュ無効化の設定

プッシュ無効化により、作成者によるコンテンツ更新は、公開時に管理対象コンテンツ配信ネットワーク（CDN）から自動的に削除されます。これにより、最新のコンテンツのみが提供されるようになります。

システムは、特定の URL とキャッシュタグまたはキーに基づいてコンテンツをクリアし、古いバージョンがパージされるようにします。

プッシュ無効化を有効にするには、プロジェクトの設定ファイルに特定のプロパティを追加する必要があります。例えば、SharePoint 内の `.helix/config.xlsx` という名前の Microsoft Excel ワークブックや、Google Drive 内の `.helix/config` という名前の Google Sheets などです。

次の設定プロパティは、実稼動ホストの名前と CDN 管理のタイプを定義します。

| キー | 値 | コメント |
| --- | --- | --- |
| `cdn.prod.host` | `<Production Host>` | 実稼動サイトのホスト名。例えば、`www.example.com` のように指定します。 |
| `cdn.prod.type` | 管理対象 |   |

設定シートに変更を行ったら、ユーザーは [Sidekick ツール](https://www.aem.live/docs/sidekick)を使用して変更をプレビューし、アクティブ化して更新を適用する必要があります。

また、[Cloud Manager の Edge Delivery の TODO リストについて](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md#ed-todo-list)も参照してください。
