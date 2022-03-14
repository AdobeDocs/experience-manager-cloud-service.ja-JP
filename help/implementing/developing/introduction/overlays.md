---
title: Adobe Experience Manager as a Cloud Service のオーバーレイ
description: AEM as a Cloud Service は、オーバーレイという原理を利用して、開発者がコンソールおよびその他の機能を拡張し、カスタマイズできるようにします
exl-id: 24bdb1a9-6d77-43c7-a75e-28e6e0fd7608
source-git-commit: ac760e782f80ee82a9b0604ef64721405fc44ee4
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 100%

---

# AEM as a Cloud Service でのオーバーレイ {#overlays-in-aem}

Adobe Experience Manager as a Cloud Service では、オーバーレイの原則を使用して、コンソールやその他の機能（ページオーサリングなど）の拡張やカスタマイズが可能です。

オーバーレイは様々なコンテキストで使用される用語です。このコンテキスト（AEM as a Cloud Service の拡張）では、オーバーレイとは、「事前定義済みの機能に対して独自の定義を強制的に付加する（標準の機能をカスタマイズする）こと」を表します。

標準インスタンスでは、定義済みの機能は `/libs` に保持され、（リソースを解決する[検索パス](#search-paths)を使用して）`/apps`ブランチの下にオーバーレイ（カスタマイズ）を定義することをお勧めします。

* タッチ対応 UI は [Granite](https://helpx.adobe.com/jp/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) 関連のオーバーレイを使用します。

   * 方法

      * `/apps` の下に適切な `/libs` 構造を再構築します。

         1:1 コピーは不要です。[Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md) は、必要な元の定義を相互参照するのに使用されるからです。Sling Resource Merger は、差分メカニズムによってリソースにアクセスおよびマージするためのサービスを提供します。

      * 変更は `/apps` 以下で行います。
   * メリット

      * `/libs` 以下の変更に対する堅牢性が高まります。
      * 実際に必要な項目のみを再定義できます。


>[!CAUTION]
>
>[Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md) および関連する手法は、[Granite](https://www.adobe.io/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) と併用する場合に限り使用できます。つまり、オーバーレイをスケルトン構造で作成する方法は、標準のタッチ操作対応 UI でのみ使用できます。

オーバーレイは、コンソールの設定、サイドパネル内にあるアセットブラウザーへの選択カテゴリの作成（ページのオーサリング時に使用）など、多くの変更において推奨される方法です。オーバーレイは、次の理由で必要になります。

* `/libs` ブランチ&#x200B;**で変更を行うことは&#x200B;***できません*。
このブランチは、インスタンスにアップグレードが適用されるたびに変更される可能性が高く、その際に変更内容が失われる場合があるからです。

* オーバーレイにより、変更を 1 箇所に集中させることができます。そのため、必要に応じて変更の追跡、移行、バックアップ、デバッグを実行しやすくなります。

## 検索パス {#search-paths}

AEM は、検索パスを使用してリソースを検索し、（デフォルトでは）最初に `/apps` ブランチを検索し、次に `/libs` ブランチを検索します。このメカニズムにより、`/apps` のオーバーレイ（およびそこに定義されているカスタマイズ）が優先されることになります。

オーバーレイの場合、配信されるリソースは、取得されたリソースとプロパティの集合体で、OSGi 設定で定義されている検索パスに応じます。
