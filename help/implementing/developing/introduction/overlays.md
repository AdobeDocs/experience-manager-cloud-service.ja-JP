---
title: Adobe Experience Manager as a Cloud Service のオーバーレイ
description: AEM as a Cloud Service は、オーバーレイという原理を利用して、開発者がコンソールおよびその他の機能を拡張し、カスタマイズできるようにします
exl-id: 24bdb1a9-6d77-43c7-a75e-28e6e0fd7608
source-git-commit: d361ddc9a50a543cd1d5f260c09920c5a9d6d675
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 31%

---

# AEM as a Cloud Service でのオーバーレイ {#overlays-in-aem}

Adobe Experience Manager as a Cloud Service では、オーバーレイの原則を使用して、コンソールやその他の機能（ページオーサリングなど）の拡張やカスタマイズが可能です。

オーバーレイは様々なコンテキストで使用される用語です。このコンテキストでは、AEMas a Cloud Serviceを拡張すると、オーバーレイとは、事前定義された機能を使用し、それに対して独自の定義を適用して標準の機能をカスタマイズすることです。

標準インスタンスでは、事前定義された機能は `/libs` オーバーレイ（カスタマイズ）は、 `/apps` ブランチ ( [検索パス](#search-paths) を参照 )。

* タッチ操作対応 UI では、 [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)-related overlays:

   * 方法

      * `/apps` の下に適切な `/libs` 構造を再構築します。

        この再構築では、1:1 コピーは必要ありません。 [Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md) は、必要な元の定義を相互参照するために使用されます。 Sling Resource Merger は、差分（差分）メカニズムを使用してリソースにアクセスし、マージするためのサービスを提供します。

      * の下 `/apps`、変更を加えます。

   * メリット

      * `/libs` 以下の変更に対する堅牢性が高まります。
      * 必要な項目のみを再定義できます。

>[!CAUTION]
>
>[Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md) および関連する手法は、[Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) と併用する場合に限り使用できます。このルールでは、スケルトン構造を持つオーバーレイの作成は、タッチ操作対応の標準的なユーザーインターフェイスに対してのみ適しているということを意味します。

多くの変更では、オーバーレイを使用することをお勧めします。 例えば、コンソールの設定や、サイドパネルのアセットブラウザーへの選択カテゴリの作成（ページのオーサリング時に使用）をおこないます。 次のように必要です。

* **内 `/libs` 分岐 *しない* 変更を加える**
このブランチは、インスタンスにアップグレードが適用されるたびに変更される可能性が高いので、加えた変更が失われる場合があります。

* 変更を 1 か所に集中させるので、必要に応じて、変更の追跡、移行、バックアップ、デバッグを容易におこなえます。

## 検索パス {#search-paths}

AEMは、検索パスを使用してリソースを検索し、最初に（デフォルトでは）を検索します。 `/apps` 分岐してから `/libs` 分岐。 このメカニズムは、 `/apps` （およびそこで定義されたカスタマイズ）が優先されます。

オーバーレイの場合、配信されるリソースは、取得されたリソースとプロパティの集合体で、OSGi 設定で定義されている検索パスに応じます。
