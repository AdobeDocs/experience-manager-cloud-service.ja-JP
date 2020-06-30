---
title: Cloud ServiceとしてのAdobe Experience Managerのオーバーレイ
description: Cloud ServiceとしてのAEMでは、オーバーレイの原則を使用して、コンソールやその他の機能を拡張およびカスタマイズできます
translation-type: tm+mt
source-git-commit: 58440cb565039becd5b08333994b70f2ea77cc99
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 38%

---


# AEMのCloud Serviceとしてのオーバーレイ {#overlays-in-aem}

Cloud ServiceとしてのAdobe Experience Managerでは、オーバーレイの原則を使用して、コンソールやその他の機能（ページオーサリングなど）の拡張やカスタマイズが可能です。

<!--
Adobe Experience Manager as a Cloud Service uses the principle of overlays to allow you to extend and customize the [consoles](/help/sites-developing/customizing-consoles-touch.md) and other functionality (for example, [page authoring](/help/sites-developing/customizing-page-authoring-touch.md)).
-->

オーバーレイは様々なコンテキストで使用される用語です。このコンテキスト(AEMをCloud Serviceとして拡張する)では、オーバーレイとは、定義済みの機能を取り込み、それに独自の定義を付加する（標準機能をカスタマイズする）ことです。

In a standard instance the predefined functionality is held under `/libs` and it is recommended practice to define your overlay (customizations) under the `/apps` branch. AEM uses a search path to find a resource, searching first the `/apps` branch and then the `/libs` branch (the [search path can be configured](#configuring-the-search-paths)). このメカニズムにより、オーバーレイ（およびそこに定義されているカスタマイズ）が優先されることになります。

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

* You ***must not *make changes in the`/libs`branch **Any changes you do make may be lost, because this branch is liable to changes whenever you:

   * インスタンス上のアップグレード
   * ホットフィックスの適用
   * 機能パックのインストール

* オーバーレイにより、変更を 1 箇所に集中させることができます。そのため、必要に応じて変更の追跡、移行、バックアップ、デバッグを実行しやすくなります。

## 検索パスの設定 {#configuring-the-search-paths}

オーバーレイの場合、配信されるリソースは、取得されたリソースとプロパティの集合体で、定義可能な以下の検索パスに応じます。

* **OSGi 設定**&#x200B;で [Apache Sling Resource Resolver Factory](/help/implementing/deploying/configuring-osgi.md) 用に定義された、リソースの **Resolver Search Path**。

   * 検索パスの順序は、上から下の順で、それぞれの優先順位を示します。
   * In a standard installation the primary defaults are `/apps`, `/libs` - so the content of `/apps` has a higher priority than that of `/libs` (i.e. it *overlays* it).

* 2人のサービスユーザーは、スクリプトが保存されている場所へのJCR:READアクセス権が必要です。 これらのユーザーは、 components-search-service(com.day.cq.wcm.coreto access/cacheコンポーネントで使用)およびsling-scripting（org.apache.sling.servlets.resolverでサーブレットを検索するために使用）。
* 次の設定も、スクリプトの配置場所に応じて設定する必要があります（この例では/etc、/libs、または/appsの下）。

   ```
   PID = org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl
   resource.resolver.searchpath=["/etc","/apps","/libs"]
   resource.resolver.vanitypath.whitelist=["/etc/","/apps/","/libs/","/content/"]
   ```

* 最後に、サーブレットリゾルバーも設定する必要があります（この例では/etcも追加します）。

   ```
   PID = org.apache.sling.servlets.resolver.SlingServletResolver
   servletresolver.paths=["/bin/","/libs/","/apps/","/etc/","/system/","/index.servlet","/login.servlet","/services/"]
   ```

<!--
## Example of Usage {#example-of-usage}

Some examples are covered when:

* [Customizing the Consoles](/help/sites-developing/customizing-consoles-touch.md)
* [Customizing Page Authoring](/help/sites-developing/customizing-page-authoring-touch.md)
-->