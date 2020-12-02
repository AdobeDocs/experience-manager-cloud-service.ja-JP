---
title: Adobe Experience Manager as a Cloud Service のオーバーレイ
description: AEM as a Cloud Service は、オーバーレイという原理を利用して、開発者がコンソールおよびその他の機能を拡張し、カスタマイズできるようにします
translation-type: tm+mt
source-git-commit: 8028682f19ba6ba7db6b60a2e5e5f5843f7ac11f
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 100%

---


# AEM as a Cloud Service でのオーバーレイ{#overlays-in-aem}

Adobe Experience Manager as a Cloud Service では、オーバーレイの原則を使用して、コンソールやその他の機能（ページオーサリングなど）の拡張やカスタマイズが可能です。

<!--
Adobe Experience Manager as a Cloud Service uses the principle of overlays to allow you to extend and customize the [consoles](/help/sites-developing/customizing-consoles-touch.md) and other functionality (for example, [page authoring](/help/sites-developing/customizing-page-authoring-touch.md)).
-->

オーバーレイは様々なコンテキストで使用される用語です。このコンテキスト（AEM as a Cloud Service の拡張）では、オーバーレイとは、「事前定義済みの機能に対して独自の定義を強制的に付加する（標準の機能をカスタマイズする）こと」を表します。

標準インスタンスでは、定義済みの機能は `/libs` に保持され、（リソースを解決する[検索パス](#search-paths)を使用して）`/apps` ブランチの下にオーバーレイ（カスタマイズ）を定義することをお勧めします。

* タッチ対応 UI は [Granite](https://helpx.adobe.com/jp/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) 関連のオーバーレイを使用します。

   * 方法

      * `/apps` の下に適切な `/libs` 構造を再構築します。

         1:1 コピーは不要です。[Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md) は、必要な元の定義を相互参照するのに使用されるからです。Sling Resource Merger は、差分メカニズムによってリソースにアクセスおよびマージするためのサービスを提供します。

      * 変更は `/apps` 以下でおこないます。
   * メリット

      * `/libs` 以下の変更に対する堅牢性が高まります。
      * 実際に必要な項目のみを再定義できます。


<!-- Still links to reference material in 6.5 -->

>[!CAUTION]
>
>[Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md) および関連する手法は、[Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) と併用する場合に限り使用できます。つまり、オーバーレイをスケルトン構造で作成する方法は、標準のタッチ操作対応 UI でのみ使用できます。

オーバーレイは、コンソールの設定、サイドパネル内にあるアセットブラウザーへの選択カテゴリの作成（ページのオーサリング時に使用）など、多くの変更において推奨される方法です。オーバーレイは、次の理由で必要になります。

<!--
Overlays are the recommended method for many changes, such as [configuring your consoles](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console) or [creating your selection category to the asset browser in the side panel](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser) (used when authoring pages). They are required as:
-->

* `/libs` ブランチ&#x200B;**で変更をおこなうことは&#x200B;***できません*。
このブランチは、インスタンスにアップグレードが適用されるたびに変更される可能性が高く、その際に変更内容が失われる場合があるからです。

* オーバーレイにより、変更を 1 箇所に集中させることができます。そのため、必要に応じて変更の追跡、移行、バックアップ、デバッグを実行しやすくなります。

## 検索パス {#search-paths}

AEM は、検索パスを使用してリソースを検索し、（デフォルトでは）最初に `/apps` ブランチを検索し、次に `/libs` ブランチを検索します。このメカニズムにより、`/apps` のオーバーレイ（およびそこに定義されているカスタマイズ）が優先されることになります。

オーバーレイの場合、配信されるリソースは、取得されたリソースとプロパティの集合体で、OSGi 設定で定義されている検索パスに応じます。

<!--
## Example of Usage {#example-of-usage}

Some examples are covered when:

* [Customizing the Consoles](/help/sites-developing/customizing-consoles-touch.md)
* [Customizing Page Authoring](/help/sites-developing/customizing-page-authoring-touch.md)
-->