---
title: コンテンツフラグメントのプレビュー
description: 様々な方法でコンテンツフラグメントをプレビューする方法を説明します。
feature: Content Fragments
role: User, Developer, Architect
solution: Experience Manager Sites
source-git-commit: 42dbf6138920c4f733d7dc74dfc81504dee1e0ae
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 50%

---

# コンテンツフラグメントのプレビュー {#previewing-content-fragments}

コンテンツフラグメントは、ヘッドレス配信とページオーサリングの両方で使用できます。 フラグメントは書式設定のない唯一のコンテンツなので、レビューするのはより困難になる場合があります。 したがって、様々なシナリオでフラグメントをプレビューする複数の方法が提供されます。

コンテンツフラグメントに使用できる方法はいくつかあり、コンソールフラグメントコンソールおよびエディターからアクセスできます。 この節で説明するコンソールとエディターは、ヘッドレスコンテンツ配信用に開発されました（ただし、すべてのシナリオで使用できます）。

フラグメントをプレビューできます。

* [ プレビュー URL パターン ](#preview-url-pattern) の使用

* [ プレビューインスタンス ](#preview-instance) に公開したり、インスタンスから非公開にしたりする

<!--
* with a HTML template, using **[Preview]()** from the Content Fragments console
-->

>[!IMPORTANT]
>
>コンテンツフラグメントには、**コンテンツフラグメント**&#x200B;と **Assets** の 2 つのコンソールからアクセスできます。
>
>また、コンテンツフラグメントをオーサリングするエディターは 2 つあります。基本機能は同じですが、いくつか違いがあります。両方のエディターは、両方のコンソールからアクセスできます。
>
>この節では、**コンテンツフラグメント**&#x200B;コンソールと&#x200B;*新しい*&#x200B;コンテンツフラグメントエディターについて説明します。これらはヘッドレスコンテンツ配信用に開発されています（ただし、すべてのシナリオで使用できます）。
>
>詳しくは、次のセクションを参照してください。
>
>* [コンテンツフラグメントの管理](/help/assets/content-fragments/content-fragments-managing.md)のための **Assets** コンソールの使用
>* [*元の*&#x200B;コンテンツフラグメントエディター](/help/assets/content-fragments/content-fragments-variations.md)の使用
>* [ページオーサリング用のコンテンツフラグメント](/help/sites-cloud/authoring/fragments/content-fragments.md)の使用

## プレビュー URL パターン {#preview-url-pattern}

コンテンツフラグメントエディターは、編集内容を外部フロントエンドアプリケーションでプレビューするオプションを作成者に提供します。

この機能を使用するには、まず次の操作が必要です。

* IT チームと協力して、JSON 出力を使用してコンテンツフラグメントをレンダリングする外部フロントエンドアプリケーションを設定します。

* 外部フロントエンドアプリケーションが設定されると、**デフォルトのプレビュー URL パターン**&#x200B;は、[適切なコンテンツフラグメントモデルのプロパティ](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#model-properties)として定義される必要があります。

プレビュー URL は次のパターンに従います。

    `https://<preview_url>?param=${expression}`

使用できる式は次のとおりです。

* `${contentFragment.path}`
* `${contentFragment.model.path}`
* `${contentFragment.model.name}`
* `${contentFragment.variation}`
* `${contentFragment.id}`

URL を定義すると、エディターの上部のツールバーで「**[プレビュー](/help/sites-cloud/administering/content-fragments/authoring.md#preview-content-fragment)**」ボタンがアクティブになります。 このボタンを選択すると、（別のタブで）外部アプリケーションを起動して、コンテンツフラグメントをレンダリングできます。

## プレビューインスタンス {#preview-instance}

フラグメントは **公開** および **非公開** プレビューインスタンス（およびパブリッシュインスタンス）に公開できます。

フラグメントは、エディターまたはコンソールから公開できます。

以下を参照してください。

* [ フラグメントの公開とプレビュー ](/help/sites-cloud/administering/content-fragments/managing.md#publishing-and-previewing-a-fragment) を参照してください。

* [ フラグメントを非公開にする ](/help/sites-cloud/administering/content-fragments/managing.md#unpublishing-a-fragment) を参照してください。

<!--
## Preview based on a HTML Template {#preview-based-on-a-html-template}

The Content Fragment console provides a **Preview** option for every fragment.

The icon can be selected to open a dialog that represents the fragment based on a HTML template. You can use the default template, or develop and load your own.
-->
