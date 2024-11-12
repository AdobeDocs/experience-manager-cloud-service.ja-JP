---
title: プッシュの無効化の設定
description: 独自の実稼動 CDN を構築するためにプッシュ無効化を設定する方法について説明します。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: bb225fcb931c6e9014ab18e6efbb0620262bcd76
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 2%

---

# プッシュの無効化の設定

プッシュの無効化は、作成者が行ったコンテンツ更新が公開時に管理コンテンツ配信ネットワーク（CDN）から自動的に削除されるようにします。 これにより、最新のコンテンツのみが提供されるようになります。

システムは、特定の URL とキャッシュタグまたはキーに基づいてコンテンツをクリアし、古いバージョンがパージされるようにします。

プッシュの無効化を有効にするには、特定のプロパティをプロジェクトの設定ファイルに追加する必要があります。 例えば、SharePointの `.helix/config.xlsx` という名前のMicrosoft Excel ワークブックや、Google Drive のGoogle シート名 `.helix/config` などです。

次の設定プロパティは、実稼動ホストの名前と CDN 管理のタイプを定義します。

| キー | value | 件のコメント |
| --- | --- | --- |
| `cdn.prod.host` | `<Production Host>` | 本番サイトのホスト名。 例えば、`www.example.com` のように指定します。 |
| `cdn.prod.type` | managed |   |

構成シートに変更が加えられたら、[ 構成ツールを使用して構成シートをプレビューし、アクティブ化して ](/help/edge/docs/sidekick.md) 更新をSidekickする必要があります。

[Cloud ManagerのEdge Delivery Servicesの概要 ](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md#ed-todo-list) も参照してください。
