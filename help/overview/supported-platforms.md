---
title: サポートされているクライアントプラットフォーム
description: AEM を使用したコンテンツのオーサリングと、Adobe Experience Manager as a Cloud Service を使用して公開されたサイトへのアクセスでサポートされているブラウザーについて説明します。
topic-tags: platform
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
exl-id: 7ddd0a75-621a-4499-91d1-7b3408a68269
source-git-commit: d53bfe103ff8e40c8221805a2d66faf3c5cd3823
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 99%

---

# サポートされているクライアントプラットフォーム {#supported-platforms}

AEM を使用したコンテンツのオーサリングと、Adobe Experience Manager as a Cloud Service を使用して公開されたサイトへのアクセスでサポートされているブラウザーについて説明します。

>[!TIP]
>
>このドキュメントでは、AEM as a Cloud Service でサポートされるクライアントプラットフォームについて説明します。AEM プロジェクト開発のためのビルド環境について詳しくは、[ビルド環境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md)のドキュメントを参照してください。

## サポートレベル {#support-levels}

アドビでは、AEM クライアントプラットフォームに対して次のレベルのサポートを定義しています。

| サポートレベル | 説明 |
|---|---|
| A：サポート対象 | アドビはこの構成への完全なサポートと保守を提供します。この構成は、アドビの品質保証プロセスでカバーされます。 |
| R：制限サポート | サポートでは、プロジェクトの設定を使用するために、アドビへの正式なリクエストが必要です。アドビによる確認が完了すると、アドビでは、限定的なサポートプログラムの範囲内で完全なサポートを提供します。詳しくは、アドビカスタマーケアにお問い合わせください。 |
| Z：サポート対象外 | この設定はサポートされていません。アドビは、この設定が動作するかどうかに関する一切の表明をせず、この設定をサポートしません。 |

## コンテンツのオーサリングでサポートされているブラウザー {#authoring}

AEM のユーザーインターフェイスは、ノートブック、デスクトップコンピューター、タブレット（Apple iPad や Microsoft Surface など）の大きめの画面向けに最適化されています。携帯電話のフォームファクターは、オーサリングのユースケースではサポートされていません。

Adobe Experience Manager のユーザーインターフェイスは、[オーサリング方法](/help/edge/overview.md#authoring-method)に応じて、次のクライアントプラットフォームで使用できます。

* [ユニバーサルエディター](/help/sites-cloud/authoring/universal-editor/authoring.md)
* [ページエディター](/help/sites-cloud/authoring/page-editor/introduction.md)
* [サイドキック](/help/edge/docs/sidekick.md)を使用した[ドキュメントベースのオーサリング](/help/edge/docs/authoring.md)

すべてのブラウザーは、デフォルトのプラグインとアドオンのセットを使用してテストされます。

| ブラウザー | ユニバーサルエディターのサポートレベル | ページエディターのサポートレベル | サイドキックのサポートレベル |
|---|---|---|---|
| Google Chrome（エバーグリーン） | A：サポート対象 | A：サポート対象 | A：サポート対象 |
| Microsoft Edge（エバーグリーン） | A：サポート対象 | A：サポート対象 | Z：サポート対象外 |
| Mozilla Firefox（エバーグリーン） | A：サポート対象 | A：サポート対象 | Z：サポート対象外 |
| Mozilla Firefox 最新 ESR [1] | A：サポート対象 | A：サポート対象 | Z：サポート対象外 |
| macOS の Safari（エバーグリーン） | A：サポート対象 | A：サポート対象 | Z：サポート対象外 |
| iPadOS の Safari （エバーグリーン） | Z：サポート対象外 | A：サポート対象 | Z：サポート対象外 |

1. Firefox の拡張サポートリリース（[詳しくは mozilla.org を参照してください](https://www.mozilla.org/ja-JP/firefox/enterprise/)）

>[!NOTE]
>
>**リリースサイクルの短いブラウザーのサポート：**
>
>Firefox、Chrome、Edge の各リリースは、定期的にアップデートされます。アドビは、これらのブラウザーの今後のバージョンに対して、上記のサポートレベルを維持するよう尽力します。

## Web サイトでサポートされているブラウザー {#websites}

AEM でレンダリングされる web サイトのブラウザーサポートは、AEM ページテンプレート、ブロック、デザイン、コンポーネント出力の実装によって異なります。したがって、プロジェクトを実装する開発者は、最終的にサイトの互換性を制御できるようになります。

AEM の[プロジェクトボイラープレート](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md#create-github-project)、[コアコンポーネント](/help/implementing/developing/components/overview.md#aem-core-components)、[WKND サンプルサイト](/help/implementing/developing/introduction/develop-wknd-tutorial.md)はすべて、最新のブラウザーすべてと互換性があります。
