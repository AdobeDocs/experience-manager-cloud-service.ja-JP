---
title: Edge 配信サービスの使用
description: AEM as a Cloud ServiceをEdge Delivery Servicesと共に使用する方法を説明します。
feature: Edge Delivery Services
exl-id: 41999302-b4c9-4f5a-b659-6e7398a3c4f4
source-git-commit: 5197a53b8aa763d7e1b2b2ce9097ee2bc8521dfa
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 14%

---


# Edge 配信サービスの使用 {#usingedge}

Edge Delivery Servicesを使用すると、作成者がコンテンツをすばやく更新および公開でき、新しいサイトを迅速に起動できる、迅速な開発環境を作成できます。 そのため、同じ web サイト上で複数のコンテンツソースを操作でき、選択したソースに関係なく、シームレスに公開を効率化できます。したがって、編集からインターネット上のコンテンツが表示されるまでに、数秒しかかかりません。

## 適切なツールの検索 {#right-tool}

Edge Delivery Servicesはコンテンツソースから切り離されており、異なるコンテンツソースからコンテンツを取り込むことができます。

![エッジ配信のコンテンツソース](assets/content-sources.png)

複数のコンテンツソースから取り込むと、ユーザーは極めて柔軟に取り込むことができます。 Adobeは、プロジェクトに最適なコンテンツソースを選択するのに役立つガイダンスを提供します。

コンテンツソースが事前に定義されている場合や、柔軟でない場合があります ( 例えば、プロジェクトで SharePoint やGoogle Drive を使用できない場合など )。 しかし、多くの場合、ツールは事前に定められておらず、ツールの選択は黒と白ではありません。

Adobeの導きの原理はシンプルさです。 ドキュメントベースのオーサリングから始め、必要に応じて複雑さを増やします。 ツールの変更が必要な場合、AEMEdge Delivery Servicesの統合では、コンテンツの移行について説明します。

![コンテンツソースの柔軟性](assets/content-source-flexiblity.png)

## オーサリング {#authoring-edge}

Edge Delivery Servicesを使用すると、オーサリングが簡単で、高速で、柔軟です。 ユニバーサルエディターを使用して、AEMでのドキュメントベースのオーサリングまたはオーサリングを使用してオーサリングを選択できます。

ドキュメントを参照してください [Edge Delivery Services用コンテンツのオーサリング](authoring.md) を参照してください。

## 公開 {#publishing-edge}

Edge Delivery Servicesを使用すれば、コンテンツソースに関係なく、コンテンツの公開がシームレスに行われます。

ドキュメントを参照してください [Edge Delivery Services用コンテンツの公開](publishing.md) を参照してください。

## 開発 {#developing-edge}

Edge Delivery Servicesは、ブロックの概念に基づいています。 AEMには、事前定義済みのブロックの包括的なライブラリが付属しており、プロジェクトのニーズに合わせて拡張できます。 Edge Delivery Servicesプロジェクトのコードは GitHub で管理されます。

ドキュメントを参照してください [Edge Delivery Services向け開発](developing.md) を参照してください。

## 既存のAEMプロジェクト {#existing-projects}

Edge Delivery Servicesの恩恵を受けるために、新しいAEMプロジェクトを待つ必要はありません。 Edge Delivery Servicesを既存のAEMプロジェクトに統合して、そのパフォーマンスの向上をすぐに活用できます。

ドキュメントを参照してください [既存のAEMプロジェクトでのEdge Delivery Servicesの使用](existing-projects.md) を参照してください。
