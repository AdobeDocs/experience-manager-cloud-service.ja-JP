---
title: Cloud ServiceとしてのAdobe Experience Managerのオーバーレイ
description: Cloud ServiceとしてのAEMでは、オーバーレイの原則を使用して、コンソールやその他の機能を拡張およびカスタマイズできます
translation-type: tm+mt
source-git-commit: 8028682f19ba6ba7db6b60a2e5e5f5843f7ac11f
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 31%

---


# AEMのCloud Serviceとしてのオーバーレイ {#overlays-in-aem}

Cloud ServiceとしてのAdobe Experience Managerでは、オーバーレイの原則を使用して、コンソールやその他の機能（ページオーサリングなど）の拡張やカスタマイズが可能です。

<!--
Adobe Experience Manager as a Cloud Service uses the principle of overlays to allow you to extend and customize the [consoles](/help/sites-developing/customizing-consoles-touch.md) and other functionality (for example, [page authoring](/help/sites-developing/customizing-page-authoring-touch.md)).
-->

オーバーレイは様々なコンテキストで使用される用語です。このコンテキスト(AEMをCloud Serviceとして拡張する)では、オーバーレイとは、定義済みの機能を取り込み、それに独自の定義を付加する（標準機能をカスタマイズする）ことです。

標準インスタンスでは、定義済みの機能はに保持され `/libs` 、ブランチの下にオーバーレイ（カスタマイズ）を定義する(リソースを解決する `/apps` 検索パスを使用する [](#search-paths) )ことをお勧めします。

* タッチ対応UIは [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)関連のオーバーレイを使用します。

   * 方法

      * の下に適切な `/libs` 構造を再構築し `/apps`ます。

         1:1コピーは不要です。 [Sling Resource Marge](/help/implementing/developing/introduction/sling-resource-merger.md) は、必要な元の定義を相互参照するために使用されます。 Sling Resource Merger は、差分メカニズムによってリソースにアクセスおよびマージするためのサービスを提供します。

      * Make any changes under `/apps`.
   * メリット

      * More robust to changes under `/libs`.
      * 実際に必要な項目のみを再定義できます。


<!-- Still links to reference material in 6.5 -->

>[!CAUTION]
>
>[Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md) および関連する手法は、[Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)と併用する場合に限り使用できます。つまり、オーバーレイをスケルトン構造で作成する方法は、標準のタッチ操作対応 UI でのみ使用できます。

オーバーレイは、コンソールの設定、サイドパネル内にあるアセットブラウザーへの選択カテゴリの作成（ページのオーサリング時に使用）など、多くの変更において推奨される方法です。オーバーレイは、次の理由で必要になります。

<!--
Overlays are the recommended method for many changes, such as [configuring your consoles](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console) or [creating your selection category to the asset browser in the side panel](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser) (used when authoring pages). They are required as:
-->

* You ***must not *make changes in the`/libs`branch **Any changes you do make may be lost, because this branch is liable to changes whenever upgrades are applied to your instance.

* オーバーレイにより、変更を 1 箇所に集中させることができます。そのため、必要に応じて変更の追跡、移行、バックアップ、デバッグを実行しやすくなります。

## 検索パス {#search-paths}

AEMは、検索パスを使用してリソースを検索し、（デフォルトでは）最初にブランチを検索し、次に `/apps` ブランチを検索し `/libs` ます。 This mechanism means that your overlay in `/apps` (and the customizations defined there) will have priority.

オーバーレイの場合、リソースは、OSGi設定で定義された検索パスに応じて取得されるリソースとプロパティの集計です。

<!--
## Example of Usage {#example-of-usage}

Some examples are covered when:

* [Customizing the Consoles](/help/sites-developing/customizing-consoles-touch.md)
* [Customizing Page Authoring](/help/sites-developing/customizing-page-authoring-touch.md)
-->