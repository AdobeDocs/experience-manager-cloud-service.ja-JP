---
title: AEMでのEdge Delivery Servicesの使用
description: AEM as a Cloud Service を Edge 配信サービスで使用する方法について説明します。
feature: Edge Delivery Services
exl-id: 41999302-b4c9-4f5a-b659-6e7398a3c4f4
source-git-commit: e98ddd8169ffbd407fdd4ff713bda57f693abaf9
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 69%

---


# AEMでのEdge Delivery Servicesの使用 {#using-edge}

Edge Delivery Servicesはコンテンツソースから切り離され、様々なコンテンツソースからコンテンツを取り込むことができます。 つまり、選択したソースに関係なく、シームレスで合理化された公開で、同じ web サイト上で複数のコンテンツソースを操作できます。

Edge Delivery Servicesを使用すると、作成者がコンテンツをすばやく更新して公開したり、新しいサイトをすばやく開始したりできる、迅速な開発環境を構築できます。 編集からインターネット上でのコンテンツのライブ表示まで、数秒で完了します。

![Edge 配信のコンテンツソース](assets/content-sources.png)

複数のコンテンツソースからの取り込みにより、ユーザーには最大限の柔軟性が提供されます。アドビでは、プロジェクトに最適なコンテンツソースを選択するのに役立つガイダンスを提供します。

コンテンツソースが事前定義されている場合や、柔軟性がない場合があります（例: プロジェクトで Sharepoint や Google ドライブを使用できない）。ただし、多くの場合、ツールは事前に定められておらず、ツールの選択に明確な区別はありません。

アドビの指針はシンプルさです。ドキュメントベースのオーサリングから始めて、必要に応じて複雑さを増やす ツールの変更が必要な場合は、AEM の Edge 配信サービスの統合によってコンテンツの移行がカバーされます。

![コンテンツソースの柔軟性](assets/content-source-flexiblity.png)

## オーサリング {#authoring-edge}

Edge 配信サービスを使用すると、オーサリングが簡単、迅速、柔軟に行えます。ドキュメントベースのオーサリングを使用してオーサリングすることも、ユニバーサルエディターを使用したAEM ベースのオーサリングを使用してオーサリングすることもできます。

詳しくは、[Edge 配信サービス向けのコンテンツのオーサリング](/help/edge/aem-authoring/authoring.md)を参照してください。

## 公開 {#publishing-edge}

Edge 配信サービスを使用すると、コンテンツソースに関係なく、コンテンツの公開をシームレスに行えます。

詳しくは、[Edge 配信サービス向けのコンテンツの公開](/help/edge/aem-authoring/publishing.md)を参照してください。

## 開発 {#developing-edge}

Edge 配信サービスは、ブロックの概念に基づいています。AEM には、プロジェクトのニーズに合わせて拡張できる事前定義済みのブロックの包括的なライブラリが付属しています。Edge 配信サービスプロジェクトのコードは、GitHub で管理されます。

詳しくは、[Edge Delivery Services を使用した AEM オーサリングのための開発者用入門ガイド](/help/edge/aem-authoring/edge-dev-getting-started.md)ドキュメントを参照してください。

## 既存の AEM プロジェクト {#existing-projects}

新しい AEM プロジェクトで Edge 配信サービスのメリットを活用できるようになるまで待つ必要はありません。Edge 配信サービスは既存の AEM プロジェクトに統合できるので、パフォーマンスの向上をすぐに活用できます。

詳しくは、[既存の AEM プロジェクトでの Edge 配信サービスの使用](/help/edge/aem-authoring/existing-projects.md)を参照してください。
