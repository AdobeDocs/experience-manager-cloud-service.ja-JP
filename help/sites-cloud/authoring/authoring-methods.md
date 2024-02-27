---
title: AEMでコンテンツをオーサリングする方法
description: AEMでコンテンツをオーサリングする様々な方法とその違いについて説明します。
feature: Authoring
source-git-commit: faac7c803a5145f4207154bfb3c9aa06274bbb86
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

---


# AEMでコンテンツをオーサリングする方法 {#authoring-methods}

AEMでコンテンツを作成する様々な方法、コンテンツの違い、およびコンテンツを重ね合わせて使用するタイミングについて説明します。

## AEM Authoring の柔軟性 {#authoring-flexibility}

AEM as a Cloud Serviceには、様々なタイプのコンテンツを編集するための様々なエディターが用意されており、様々なオーサリングの使用例をサポートしています。

* [AEM Page Editor](#page-editor)  — これは、AEMでコンテンツをオーサリングするための従来のエディターで、数千の Web サイトにわたって何千もの人々が試み、信頼できました。
* [AEM Content Fragment Editor](#cf-editor)  — ヘッドレスコンテンツを作成する場合に選択できるエディターです。
* [ユニバーサルエディター](#universal-editor)  — この最新の UI を使用すると、コンテンツに依存しない方法でAEMコンテンツを作成でき、Edge Delivery Servicesを活用するAEMプロジェクトの最初の選択肢です。
* [ドキュメントベースのオーサリング](#document-based) - Edge 配信サービスを使用する場合、Microsoft Word やGoogleドキュメントなど、従来のドキュメントとして、AEMコンソール以外のコンテンツを作成するように選択できます。

AEMの統合された拡張性のある特性により、これらのメソッドは、排他的に、またはプロジェクトのニーズに応じて、互いに組み合わせて使用できます。

使用可能なオーサリングオプションが不明な場合や、コンテンツのオーサリング用の新しいオプションを検討したい場合は、システム管理者またはプロジェクトマネージャーにお問い合わせください。

## AEM Page Editor {#page-editor}

これは、AEMでコンテンツをオーサリングするための従来のエディターで、数千の Web サイトで何千もの人々に対して試され、信頼されています。

![AEMページエディター](assets/authoring-methods-page-editor.png)

AEMのページエディターは、what-you-see-is-what-you-get(WYSIWYG) インターフェイスを使用してコンテンツをオーサリングするための統合環境を表示します。 定義済みのコンポーネントをドラッグ&amp;ドロップしてページを作成し、コンテンツをインプレースで編集します。

AEMページエディターの詳細については、ドキュメントを参照してください。 [AEM Page Editor。](/help/sites-cloud/authoring/page-editor/introduction.md)

## AEM Content Fragment Editor {#cf-editor}

AEMコンテンツフラグメントエディターは、ヘッドレスコンテンツを作成する際に選択するエディターです。

![AEM Content Fragment Editor](assets/authoring-methods-cf-editor.png)

AEMコンテンツフラグメントエディターは、ヘッドレス配信に最適な、構造化コンテンツを作成および管理するための明確なインターフェイスを提供します。

AEMコンテンツフラグメントエディターの詳細については、ドキュメントを参照してください。 [コンテンツフラグメントの管理](/help/sites-cloud/administering/content-fragments/managing.md) および [コンテンツフラグメントのオーサリング](/help/sites-cloud/administering/content-fragments/managing.md).

>[!NOTE]
>
>The *新規* AEM as a Cloud Service用にローカルで開発する場合は、この節で強調表示されているエディターは使用できません。
>
>The [*オリジナル* コンテンツフラグメントエディター](/help/assets/content-fragments/content-fragments-variations.md) はも利用できます。

## ユニバーサルエディター {#universal-editor}

ユニバーサルエディターは、コンテンツに依存しない方法でAEMコンテンツを作成できる最新の UI で、Edge Delivery Servicesを活用したAEMプロジェクトの最初の選択肢です。

![ユニバーサルエディター](assets/authoring-methods-ue.png)

ユニバーサルエディターはAEM内の Sites コンソールからアクセスしますが、AEMコンテンツだけでなく、適切に実装された外部コンテンツも作成できる、コンテンツに依存しない優れた柔軟性を備えています。

ユニバーサルエディターの詳細については、ドキュメントを参照してください [ユニバーサルエディターを使用したコンテンツのオーサリング。](/help/sites-cloud/authoring/universal-editor/authoring.md)

## ドキュメントベースのオーサリング {#document-based}

Edge 配信サービスを使用する場合、Microsoft Word やGoogle Docs などの従来のドキュメントとは全く別のドキュメントとして、コンテンツを作成することもできます。 [AEM **Sites** コンソール。](/help/sites-cloud/authoring/sites-console/introduction.md)

![ドキュメントベースのコンテンツの編集](assets/authoring-methods-document.jpg)

ドキュメントベースのオーサリングでは、作成者は既に知っているツールを使用でき、AEMEdge Delivery Servicesの速度とパフォーマンスのメリットを活用して、コンテンツを公開できます。 ドキュメントベースのオーサリングでは、AEMコンソールを使用する必要はありません。

ドキュメントベースのオーサリングについて詳しくは、ドキュメントを参照してください [Edge Delivery Services用コンテンツのオーサリング](/help/edge/authoring.md)
