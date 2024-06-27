---
title: コンポーネントの作成
description: AEM コンポーネントを使用して、Web ページ上で使用できるコンテンツを保持、書式設定およびレンダリングします。このページでは、チャネルのオーサリングとコンポーネントのレンダリングについて説明します。
exl-id: a81e812e-29ed-45de-b2d0-1fb0a8c5ce1a
feature: Developing Screens
role: Admin, Developer
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: ht
source-wordcount: '284'
ht-degree: 100%

---

# コンポーネントの作成 {#creating-components}

AEM コンポーネントを使用して、web ページ上で使用できるコンテンツを保持、書式設定およびレンダリングします。

## チャネルのオーサリング {#authoring-channels}

チャネルは、一連のディスプレイに配信されるコンテンツの中心的なオブジェクトです。したがって、通常、コンテンツ作成者は、コンテンツを追加または変更するために、エディターでチャネルを開きます。チャネルは ***cq:Page*** なので、同じ従来の UX パターンに従って、チャネル上のコンポーネントを追加および変更します。

ただし、チャネル内のコンポーネントは通常フルスクリーンでレンダリングされるので、単一コンポーネントの編集や新しい順序の編成をおこなう際にオーサリングエクスペリエンスに影響を及ぼします。そのため、チャネルはコンポーネントの様々なビューをレンダリングするためにセレクターを使用します。オーサリング環境では、編集セレクターを使用して、カスタムチャネルのレンダリングをアクティベートします。

例：`http://localhost:4502/editor.html/content/screens/we-retail/channels/idle.edit.html](http://localhost:4502/editor.html/content/screens/we-retail/channels/idle.edit.html`

ユーザーは、編集時に URL にセレクターを追加する必要はありません。クライアント側のロジックがレイヤースイッチイベントをリッスンしており、チャネルに専用のリソースタイプ *screens/core/components/channel* がある場合にセレクターを追加します。

## コンポーネントのレンダリング {#rendering-components}

適切なオーサリングを有効にするために、コンポーネントでは次の 2 つのレンダリングを提供する必要があります。

| **コンポーネント** | **レンディション** |
|---|---|
| *my-component/my-component.html* | 実稼動レンダリング |
| *my-component/edit.html* | 小さいビューでのレンダリングの編集 |

組み込みのコンポーネントでは、次のクライアントライブラリのカテゴリが使用されます。

| **コンポーネント** | **クライアントライブラリ** |
|---|---|
| *cq.screens.components.edit* | オーサリング時に読み込む必要がある CSS および JS |
| *cq.screens.components.production* | チャネルの実行時に読み込む必要がある CSS および JS |
| *cq.screens.components* | 共有 CSS および JS |

>[!NOTE]
>
>カスタムコンポーネントを開発する場合は、[AEM Screens のサンプルコンポーネントテンプレート](https://github.com/Adobe-Marketing-Cloud/aem-screens-component-template)を使用してください。
