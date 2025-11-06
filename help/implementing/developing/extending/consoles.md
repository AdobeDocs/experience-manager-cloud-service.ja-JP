---
title: コンソールのカスタマイズ
description: オーサーインスタンスのコンソールをカスタマイズするために AEM が提供する様々なオプションについて説明します。
exl-id: 832f9a86-07c4-4229-a0dc-8ad50a8195b0
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 96%

---

# コンソールのカスタマイズ {#customizing-consoles}

AEM は、オーサリングインスタンスのコンソール（および[ページオーサリング機能](/help/implementing/developing/extending/page-authoring.md)）をカスタマイズするオプションを提供します。

## Clientlibs {#clientlibs}

Clientlibs を使用すると、デフォルトの実装を拡張して新しい機能を提供しながら、標準の関数、オブジェクトおよびメソッドを再利用できます。Clientlibs をカスタマイズする場合、独自の clientlib を `/apps.` 下に作成できます。例えば、カスタムコンポーネントに必要なコードを保持できます。

詳しくは、[AEM as a Cloud Service でのクライアントサイドライブラリの使用](/help/implementing/developing/introduction/clientlibs.md)を参照してください。

## オーバーレイ {#overlays}

オーバーレイはノード定義に基づいており、`/libs` 下にある標準の機能に、`/apps` 下にあるカスタマイズした独自機能を重ねることができます。:1Sling Resource Merger[ は継承を許可しているので、オーバーレイを作成するときに、オリジナルの 1](/help/implementing/developing/introduction/sling-resource-merger.md) コピーは必要ありません。

オーバーレイを様々な方法で使用して AEM コンソールを拡張できます。次の節では、いくつかの例を示します。

詳しくは、[Adobe Experience Manager as a Cloud Service のオーバーレイ](/help/implementing/developing/introduction/overlays.md)を参照してください。

>[!TIP]
>
>オーサリングエクスペリエンスをカスタマイズするオプションについて詳しくは、[ページオーサリングのカスタマイズ](/help/implementing/developing/extending/page-authoring.md)を参照してください。

## コンソールのデフォルト表示のカスタマイズ {#customizing-the-default-view-for-a-console}

コンソールのデフォルト表示（列、カード、リスト）を次のようにカスタマイズできます。

* 次の場所で必要なエントリをオーバーレイすることで、ビューを並べ替えることができます。

   * `/libs/wcm/core/content/sites/jcr:content/views`

   * 最初のエントリがデフォルトです。

   * 使用可能なノードは、使用可能な表示オプションに関連付けられます。

      * `column`
      * `card`
      * `list`

* 例えば、次のようにリスト用のオーバーレイです。

   * `/apps/wcm/core/content/sites/jcr:content/views/list`

   * 次のプロパティを定義します。

      * **名前**：`sling:orderBefore`
      * **型**：`String`
      * **値**：`column`

### ツールバーへの新しいアクションの追加 {#add-a-new-action-to-the-toolbar}

独自のコンポーネントを構築し、対応するカスタムアクションのクライアントライブラリを含めることができます。

* 例えば、**ソーシャルメディアに昇格**&#x200B;アクションを次のように作成します。

   * `/apps/wcm/core/clientlibs/sites/js/socialmedia.js`

   * このアクションを独自コンソールのツールバー項目に関連付けることができます。

   * `/apps/<yourProject>/admin/ext/launches`

   * 選択モードの例：

   * `content/jcr:content/body/content/header/items/selection/items/socialmedia`

### 特定のグループに対するツールバーアクションの制限 {#restrict-a-toolbar-action-to-a-specific-group}

カスタムのレンダリング条件を使用して、標準のアクションをオーバーレイし、レンダリング前に満たす必要のある特定の条件を課すことができます。

例えば、コンポーネントを作成して、グループに従ってレンダリング条件を制御する場合があります。

* `/apps/myapp/components/renderconditions/group`

これらを Sites コンソールの「**サイトを作成**」アクションに適用するには、次の手順に従います。

* `/libs/wcm/core/content/sites`

1. オーバーレイを作成します。

   * `/apps/wcm/core/content/sites`

1. アクションのレンダリング条件を次のように追加します。

   * `jcr:content/body/content/header/items/default/items/create/items/createsite/rendercondition`

このノードのプロパティを使用して、特定のアクションを実行できる `groups`（`administrators` など）を定義できます。

### リスト表示での列のカスタマイズ {#customizing-columns-in-list-view}

リスト表示で列をカスタマイズするには、次の手順に従います。

1. 使用可能な列のリストをオーバーレイします。

   * ノードの場合：

     `/apps/wcm/core/content/common/availablecolumns`

1. 新しい列を追加するか、既存の列を削除します。

追加データを挿入する場合は、`pageInfoProviderType` プロパティを持つ [PageInforProvider](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/PageInfoProvider.html) を記述する必要があります。

>[!NOTE]
>
>この機能は、テキストフィールドの列に対して最適化されています。他のデータタイプの場合は、`/apps` で `cq/gui/components/siteadmin/admin/listview/columns/analyticscolumnrenderer` をオーバーレイできます。

### リソースのフィルタリング {#filtering-resources}

コンソールを使用する場合、ユーザーはページ、コンポーネントまたはアセットなどのリソースから選択する必要があります。作成者が項目を選択する必要があるリストの形式をとることができます。

リストを適切なサイズに保ち、使用事例にも関連するように、フィルターをカスタム述語の形式で実装できます。詳しくは、[ページオーサリングのカスタマイズ](/help/implementing/developing/extending/page-authoring.md#filtering-resources)を参照してください。
