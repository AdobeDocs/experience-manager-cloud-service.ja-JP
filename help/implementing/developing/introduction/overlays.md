---
title: Adobe Experience Manager as a Cloud Service のオーバーレイ
description: AEM as a Cloud Service は、オーバーレイという原理を利用して、開発者がコンソールおよびその他の機能を拡張し、カスタマイズできるようにします
exl-id: 24bdb1a9-6d77-43c7-a75e-28e6e0fd7608
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 93%

---

# AEM as a Cloud Service でのオーバーレイ {#overlays-in-aem}

Adobe Experience Manager as a Cloud Service では、オーバーレイの原則を使用して、コンソールやその他の機能（ページオーサリングなど）の拡張やカスタマイズが可能です。

オーバーレイは様々なコンテキストで使用される用語です。AEM as a Cloud Service を拡張するというこのコンテキストにおいて、オーバーレイとは、事前定義済みの機能に対して独自の定義を強制的に付加することで、標準の機能をカスタマイズすることを意味します。

標準インスタンスでは、定義済みの機能は `/libs` 下に保持され、（リソースを解決する[検索パス](#search-paths)を使用して）`/apps` 分岐の下にオーバーレイ（カスタマイズ）を定義することをお勧めします。

* タッチ対応ユーザーインターフェイスは [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) 関連のオーバーレイを使用します。

   * 方法

      * `/apps` の下に適切な `/libs` 構造を再構築します。

        この再構築では、必要な元の定義を相互参照するために :1Sling Resource Merger[&#x200B; が使用されるので、1](/help/implementing/developing/introduction/sling-resource-merger.md) コピーは必要ありません。 Sling Resource Merger は、差分メカニズムによってリソースにアクセスおよびマージするサービスを提供します。

      * `/apps` の下に、変更を加えます。

   * メリット

      * `/libs` 以下の変更に対する堅牢性が高まります。
      * 必須項目のみを再定義します。

>[!CAUTION]
>
>[Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md) および関連する手法は、[Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) と併用する場合に限り使用できます。このルールでは、スケルトン構造を持つオーバーレイの作成は、標準的なタッチ操作対応ユーザーインターフェイスに対してのみ適しているということを意味します。

オーバーレイは、変更が多い場合に推奨されるメソッドです。例えば、コンソールの設定またはサイドパネルのアセットブラウザーへの選択カテゴリの作成（ページのオーサリング時に使用）です。必要な理由は次のとおりです。

* **`/libs` 分岐で変更を加えることは&#x200B;*できません***
この分岐は、インスタンスにアップグレードが適用されるたびに変更される可能性が高く、その際に変更内容が失われる場合があるからです。

* オーバーレイにより、変更を 1 箇所に集中させることができるため、必要に応じて変更の追跡、移行、バックアップまたはデバッグを実行しやすくなります。

## 検索パス {#search-paths}

AEM は、検索パスを使用して、（デフォルトでは）最初に `/apps` 分岐、次に `/libs` 分岐の順に検索してリソースを見つけます。このメカニズムにより、`/apps` のオーバーレイ（およびそこに定義されているカスタマイズ）が優先されることになります。

オーバーレイの場合、配信されるリソースは、取得されたリソースとプロパティの集合体で、OSGi 設定で定義されている検索パスに応じます。
