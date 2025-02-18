---
title: AEM Sites と Edge Delivery Service
description: コンテンツ作成を高速化して 100％のパフォーマンスでサイトを配信することを目的とした、Edge Delivery Services が AEM Sites のオーサリングとパブリッシングの可能性を拡張する仕組みについて説明します。
solution: Experience Manager Sites
feature: Authoring
role: User
exl-id: 7747d6f7-18e4-4713-baea-bcfa94f54934
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: ht
source-wordcount: '618'
ht-degree: 100%

---

# AEM Sites と Edge Delivery Service {#sites-and-edge}

コンテンツ作成を高速化して 100％のパフォーマンスでサイトを配信することを目的とした、Edge Delivery Services が AEM Sites のオーサリングとパブリッシングの可能性を拡張する仕組みについて説明します。

## 概要 {#overview}

クラウドネイティブの AEM as a Cloud Service プラットフォームの一部として [AEM Sites as a Cloud Service が提供する能力と機能](/help/sites-cloud/sites-cloud-changes.md)のすべてに加えて、Edge Delivery Services は追加のオーサリングとパブリッシングの可能性を提供し、コンテンツ作成を高速化し、100％のパフォーマンスでサイトを配信します。

## Edge Delivery Services とは {#what-is-edge}

Edge Delivery Services は、オーサリングと開発が迅速で、影響力の大きいエクスペリエンスを提供することで、エンゲージメントとコンバージョンを促進する優れたエクスペリエンスを提供します。これは、作成者がサイトをすばやく更新および公開できて、新しいサイトが迅速にローンチされる高速開発環境を可能にする、構成可能なサービスセットです。Edge Delivery Services について詳しくは、[Edge Delivery Services の概要](/help/edge/overview.md)ドキュメントを参照してください。

Edge Delivery Services を AEM Sites as a Cloud Service と共に使用すると、プロジェクトで次のようなメリットが得られます。

* [新しい開発者エクスペリエンス](#developer-experience)
* [新しいパブリッシュ層](#publish-tier)
* [追加のオーサリングオプション](#authoring-options)

## 新しい開発者エクスペリエンス {#developer-experience}

Edge Delivery Services のコアとなる原理は&#x200B;*速度*&#x200B;です。これは、開発者のエクスペリエンスから始まります。開発者である場合：

* Git の基本を理解
* HTML、CSS、JavaScript の基本を理解

30 分以内に、Edge Delivery Services 用の独自のプロジェクトとコンポーネントをカスタマイズして使い始めることができます。まず、GitHub でボイラープレートプロジェクトのクローンを作成し、変更をコミットします。カスタマイズはすぐに反映されます。

Edge Delivery Services の開発について詳しくは、[はじめに - 開発者向けチュートリアル](https://www.aem.live/developer/tutorial)を参照してください。

## 新しいパブリッシュ層 {#publish-tier}

開発時間が大幅に短縮されるだけでなく、Edge Delivery Services は web サイトを超高速に作成します。

## 追加のオーサリングオプション {#authoring-options}

Edge Delivery Services は、新しいオーサリングオプションを提供することで、コンテンツ作成の速度も向上させます。

### ユニバーサルエディター {#universal-editor}

ユニバーサルエディターは、あらゆるコンテンツの作成に使用できるシームレスな、見たとおりに編集できる（WYSIWYG）オーサリングエクスペリエンスを提供します。

ユニバーサルエディターを使用したコンテンツのオーサリングについて詳しくは、[Edge Delivery Services 向けの WYSIWYG コンテンツのオーサリング](/help/edge/wysiwyg-authoring/authoring.md)ドキュメントを参照してください。

### ドキュメントベースのオーサリング {#document-authoring}

ドキュメントベースのオーサリングでは、誰もが知っているツールである Word や Google Docs を活用して、トレーニングなしで誰でもコンテンツを作成できます。これらのシンプルなツールを使用すると、Edge Delivery Services は Word ドキュメントへの変更をライブサイト上の更新されたコンテンツに即時に変換できます。

ドキュメントベースのオーサリングの使用について詳しくは、[コンテンツのオーサリングとパブリッシング](https://www.aem.live/docs/authoring)ドキュメントを参照してください。

## Edge の使用判断 {#decision}

アドビは、あらゆる規模のプロジェクトにおいて、お客様とその関係者が Edge Delivery Services から大きなメリットを得ていることを実感しています。このため、アドビでは、新しいプロジェクトの開始点として Edge Delivery Services を活用することをお勧めします。

また、サイトまたはページのサブセットを Edge Delivery にデプロイし、残りを現在のスタックに保持することもできます。これは、パフォーマンス、オーガニックトラフィック、顧客エンゲージメント、開発者、またはコンテンツの速度の改善が必要な場合に常に推奨されます。

Edge Delivery が適切かどうかわからない場合は、アドビ担当者にお問い合わせください。

### Edge Delivery とヘッドレスについて（#ヘッドレス）

Edge Delivery は、バックエンドから分離されたパフォーマンス重視のヘッドです。React SPA などのカスタムヘッドがある場合、アドビでは AEM ヘッドレス統合パターンをお勧めします。詳しくは、[AEM ヘッドレスドキュメント](/help/headless/introduction.md)を参照してください。

ただし、アドビでは通常、Edge Delivery をデフォルトのヘッドとして使用して、その速度とパフォーマンスを活用し、プロジェクトのヘッドレス部分（通常はビジネスアプリケーション）をヘッドレスアプローチ（React や SPA など）で統合することをお勧めします。
