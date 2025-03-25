---
title: SPA エディターの廃止
description: SPA Editor は引き続きAdobeでサポートされますが、SPA Editor がプロジェクトに対して非推奨になる意味と、今後のプロジェクトで使用できるオプションについて説明します。
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 7bff178eabdf7e0d89e7195be6ca109db19ee655
workflow-type: tm+mt
source-wordcount: '914'
ht-degree: 2%

---


# SPA エディターの廃止 {#spa-editor-deprecation}

SPA Editor は引き続きAdobeでサポートされますが、SPA Editor がプロジェクトに対して非推奨になる意味と、今後のプロジェクトで使用できるオプションについて説明します。

## 概要 {#summary}

Adobeは、AEM as a Cloud Serviceの [ リリース 2025.01](/help/release-notes/release-notes-cloud/2025/release-notes-2025-1-0.md#spa-editor) で SPA エディターを非推奨（廃止予定）としました。つまり、SDK にさらに機能強化や更新は行われません。 Adobeでは、AEMの最新のイノベーションを活用するために、新しいプロジェクトには [ ユニバーサルエディター ](/help/implementing/universal-editor/introduction.md) を使用することをお勧めします。

## 廃止の詳細 {#details}

SPA エディターの廃止 **すぐに削除するつもりはありません**。既存の実装がある場合は **ニーズを満たす限り、使用を継続できます。** ただし、廃止に伴い、以下の点にご注意ください。

* 今後、Adobeで対処する問題は、P1 と P2 の問題と、セキュリティの脆弱性のみです。
* SDK に対するその他の開発、機能強化または更新は行われません。

非推奨（廃止予定）は、次の SDK が機能フリーズになっていることを意味します。

* [AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype/)
* [AEM SPA プロジェクトコア ](https://github.com/adobe/aem-spa-project-core)
* [AEM SPA Page Model Manager](https://github.com/adobe/aem-spa-page-model-manager)
* [AEM SPA コンポーネントマッピング ](https://github.com/adobe/aem-spa-component-mapping)
* [AEM SPA React 編集可能コンポーネント](https://github.com/adobe/aem-react-editable-components)
   * [AEM React コアコンポーネント ](https://github.com/adobe/aem-react-core-wcm-components)
   * [AEM React コアコンポーネントベース ](https://github.com/adobe/aem-react-core-wcm-components-base)
   * [AEM React コアコンポーネント SPA](https://github.com/adobe/aem-react-core-wcm-components-spa)
   * [AEM React コアコンポーネント ](https://github.com/adobe/aem-react-core-wcm-components-examples) 例
* [AEM SPA Angular編集可能コンポーネント ](https://github.com/adobe/aem-angular-editable-components)
   * [AEM Angular コアコンポーネント ](https://github.com/adobe/aem-angular-core-wcm-components)
   * [AEM Angular コアコンポーネントベース ](https://github.com/adobe/aem-angular-core-wcm-components-base)
   * [AEM Angular コアコンポーネント SPA](https://github.com/adobe/aem-angular-core-wcm-components-spa)
   * [AEM Angular コアコンポーネントの例 ](https://github.com/adobe/aem-angular-core-wcm-components-examples)
* [AEM SPA Vue 編集可能コンポーネント ](https://github.com/mavicellc/aem-vue-editable-components)

## SPA エディターの代替手段 {#alternatives}

SPA エディターに最も適した代替手段は、プロジェクトのニーズに応じて異なります。

* **[ユニバーサルエディター](/help/edge/wysiwyg-authoring/authoring.md)** は、SPA エディターの代わりとなる最適なエディターです。
   * ユニバーサルエディターもビジュアルエディターで、SPA Editor のAdobeのエクスペリエンスをすべて取り入れて、分離された実装のために特別に設計されました。
   * ユニバーサルエディターも [AEM 6.5 用にリリース ](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/implementing/developing/headless/universal-editor/introduction) されており（AEM 6.5 のリリース 2024.11.05 を含む）、Cloud Services に加えて AMS とオンプレミスのユースケースをサポートしています。
* **[コンテンツフラグメントエディター](/help/assets/content-fragments/content-fragments-managing.md)** は、フォームベースのエディターを好むユーザーの代替手段です。
   * コンテンツフラグメントエディターは、コンテンツがページとしてではなく、コンテンツフラグメントとして構造化されている場合に最適です。

コンテンツフラグメントでコンテンツを構造化しても、ユニバーサルエディターがビジュアルエディターとして使用されなくなるわけではなく、両方のエディターを一緒に使用できます。

## ユニバーサルエディターへの移行 {#migrate-ue}

ユニバーサルエディターには多くの利点があり、移行は新規プロジェクトにとって優れたソリューションになります。

* **ビジュアル編集：** SPA エディターと同様に、作成者はプレビュー内でコンテンツを直接編集でき、変更が訪問者エクスペリエンスにどのように影響するかを即座に確認できます。
* **将来性の検証：AEMのロードマップでは** ユニバーサルエディターがビジュアルエディターとして優先されます。 それを採用することで、最新のイノベーションや機能強化にアクセスできます。
* **よりシンプルな統合：** ユニバーサルエディターを使用するためにAEM固有のSDKは必要ないため、テクニカルスタックのロックインが減ります。
* **独自のアプリを用意：** ユニバーサルエディターは、あらゆる web フレームワークやアーキテクチャをサポートしており、複雑なリファクタリングを必要とせずに導入できます。
* **拡張性：** ユニバーサルエディターは、GenAI、Workfrontなどとの統合を含む、堅牢な [ 拡張フレームワーク ](/help/implementing/universal-editor/extending.md) のメリットを受けます。

SPA エディターからユニバーサルエディターに直接移行するパスはありません。 これは、2 つの技術の基本的な違いによるものです。

* ユニバーサルエディターには、テンプレートエディター、スタイルシステム、レスポンシブグリッドなどの機能は再導入されません。
   * Edge Delivery Servicesまたはヘッドレスプロジェクトのリーンフロントエンド CSS および JS を使用して、これらのユースケースをより効率的に処理できるようになりました。
* ユニバーサルエディターはサービスとしてのエディターなので、実装者がコンポーネントダイアログに CSS または JS を挿入することはできません。
   * これにより、ページエディターからコンポーネントダイアログが自動変換されるのを防ぐことができます。
   * これは、カスタムウィジェット、フィールド検証、表示/非表示ルール、テンプレートベースのカスタマイズなど、ダイアログの多くの領域に影響します。

これらの技術的な違いを念頭に置いて、Adobeでは次の操作をお勧めします。

* サポートが継続されるので、既存の SPA エディターサイトをそのままの状態に保ちます。
* 新しいサイト、セクション、ページなど、すべての新しい開発にユニバーサルエディターを採用します。

ユニバーサルエディターには特定の SPA エディター機能を直接実装していませんが、ユニバーサルエディターの新しい柔軟性を使用して同じ問題を解決する新しい方法があることに注意してください。

## SPA エディターとユニバーサルエディターの比較 {#spa-vs-ue}

ユニバーサルエディターを使用すると、次の図に示すように、web アプリの実装者の自由度が大幅に向上します。

![ 比較されるユニバーサルエディターと SPA エディターアーキテクチャ ](assets/spa-editor-vs-ue.png)

|  | SPA エディター | ユニバーサルエディター |
|---|---|---|
| **テーマ設定** | アプリは、AEMのグリッド CSS を使用してレイアウトを実装する必要があります。 | アプリは、レイアウトに任意の最新の CSS 手法を使用できます。 |
| **レンダリング** | アプリは SPA エディターのルーティング構造に従う必要があります。 | ルールやパターンを意識することなく、自由にアプリを実装することができます。 |
| **SDK** | 実装では、SDKを緊密に統合する必要があります。 | オーサー層では、アプリは `corlib.js` を読み込み、HTML アノテーションを介してユニバーサルエディターに指示します。 |
| **フレームワーク** | アプリでは、サポートされているバージョンの React またはAngularを使用する必要があります。 | アプリは任意のフレームワークまたはアーキテクチャを使用できます。 |
| **ホスティング** | アプリはAEMのドメインでホストされている必要があります。 | アプリはどこでも完全に切り離してホストできます。 |
| **API** | アプリは、`model.json` API からコンテンツを取得する必要があります。 | アプリは、カスタムの API を含む任意の API を使用できます。 |
| **永続性** | SPA エディターでは、ビジュアル編集のためにページコンテンツのみをサポートしています。 | ユニバーサルエディターは、ページとコンテンツフラグメントのビジュアル編集をネイティブにサポートしています。 |
|  |  | ユニバーサルエディターを拡張して、同じ視覚的機能で外部コンテンツを編集できます。 |
|  | 開発者は、Sling モデルと `cq:Dialog` をAEMにデプロイする必要があります。 | 開発者はAEMの経験がほぼまたはまったくない必要があり、Java を記述する必要はありません。 |
