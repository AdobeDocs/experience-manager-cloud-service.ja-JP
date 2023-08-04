---
title: コンソールのカスタマイズ
description: オーサーインスタンスのコンソールをカスタマイズするためにAEMが提供する様々なオプションについて説明します。
source-git-commit: f159f0ef86c2b82da4e7308a0892b4947b6e43fb
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 10%

---


# コンソールのカスタマイズ {#customizing-consoles}

AEMには、コンソール ( および [ページオーサリング機能](/help/implementing/developing/extending/page-authoring.md)) を作成します。

## Clientlibs {#clientlibs}

clientlibs を使用すると、デフォルトの実装を拡張して新しい機能を提供し、標準の関数、オブジェクト、メソッドを再利用できます。 clientlibs を使用してカスタマイズする場合、独自の clientlib を `/apps.` 例えば、カスタムコンポーネントに必要なコードを保持できます。

clientlibs の詳細については、このドキュメントを参照してください。 [AEMでのクライアント側ライブラリの使用をas a Cloud Serviceします。](/help/implementing/developing/introduction/clientlibs.md)

## オーバーレイ {#overlays}

オーバーレイはノード定義に基づいており、 `/libs` カスタマイズされた機能を `/apps`. オーバーレイを作成する場合、元の 1 対 1 のコピーは不要です。 [Sling resource merger](/help/implementing/developing/introduction/sling-resource-merger.md) 継承を許可します。

オーバーレイは、様々な方法でAEMコンソールを拡張できます。 次の節では、いくつかの例を示します。

オーバーレイについて詳しくは、ドキュメントを参照してください。 [Adobe Experience Manager as a Cloud Serviceのオーバーレイ。](/help/implementing/developing/introduction/overlays.md)

>[!TIP]
>
>オーサリングエクスペリエンスをカスタマイズするオプションに興味がある場合は、ドキュメントを参照してください [ページオーサリングのカスタマイズ。](/help/implementing/developing/extending/page-authoring.md)

## コンソールのデフォルト表示のカスタマイズ {#customizing-the-default-view-for-a-console}

コンソールのデフォルトの表示（列、カード、リスト）をカスタマイズできます。

* 次の場所で必要なエントリをオーバーレイすることで、ビューを並べ替えることができます。

   * `/libs/wcm/core/content/sites/jcr:content/views`

   * 最初のエントリがデフォルトです。

   * 使用可能なノードは、使用可能な表示オプションに関連付けられます。

      * `column`
      * `card`
      * `list`

* 例えば、リストのオーバーレイでは、次のようになります。

   * `/apps/wcm/core/content/sites/jcr:content/views/list`

   * 次のプロパティを定義します。

      * **名前**：`sling:orderBefore`
      * **型**：`String`
      * **値**：`column`

### ツールバーに新しいアクションを追加する {#add-a-new-action-to-the-toolbar}

独自のコンポーネントを構築し、対応するカスタムアクション用のクライアントライブラリを含めることができます。

* 例えば、 **ソーシャルメディアに昇格** アクション：

   * `/apps/wcm/core/clientlibs/sites/js/socialmedia.js`

   * このアクションを独自コンソールのツールバー項目に関連付けることができます。

   * `/apps/<yourProject>/admin/ext/launches`

   * 選択モードの例：

   * `content/jcr:content/body/content/header/items/selection/items/socialmedia`

### 特定のグループにツールバーアクションを制限する {#restrict-a-toolbar-action-to-a-specific-group}

カスタムのレンダリング条件を使用して、標準のアクションをオーバーレイし、レンダリング前に満たす必要のある特定の条件を課すことができます。

例えば、コンポーネントを作成して、グループに従ってレンダリング条件を制御する場合があります。

* `/apps/myapp/components/renderconditions/group`

これらを **サイトを作成** サイトコンソールのアクション：

* `/libs/wcm/core/content/sites`

1. オーバーレイを作成します。

   * `/apps/wcm/core/content/sites`

1. 次に、アクションのレンダリング条件を追加します。

   * `jcr:content/body/content/header/items/default/items/create/items/createsite/rendercondition`

このノードのプロパティを使用して、特定のアクションを実行できる `groups`（`administrators` など）を定義できます。

### リスト表示の列のカスタマイズ {#customizing-columns-in-list-view}

リスト表示の列をカスタマイズするには：

1. 使用可能な列のリストをオーバーレイします。

   * ノードの場合：

     `/apps/wcm/core/content/common/availablecolumns`

1. 新しい列を追加するか、既存の列を削除します。

追加のデータを挿入する場合は、 [PageInfoProvider](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/PageInfoProvider.html) と `pageInfoProviderType` プロパティ。

>[!NOTE]
>
>この機能は、テキストフィールドの列に対して最適化されています。他のデータタイプの場合は、 `cq/gui/components/siteadmin/admin/listview/columns/analyticscolumnrenderer` in `/apps`.

### リソースのフィルタリング {#filtering-resources}

コンソールを使用する場合、多くの場合、ユーザーはページ、コンポーネント、アセットなどのリソースから選択する必要があります。 作成者が項目を選択する必要があるリストの形式をとることができます。

リストを適切なサイズに保ち、使用事例にも関連するように、カスタム述語の形式でフィルターを実装できます。 ドキュメントを参照してください[ページオーサリングのカスタマイズ](/help/implementing/developing/extending/page-authoring.md#filtering-resources) 」を参照してください。
