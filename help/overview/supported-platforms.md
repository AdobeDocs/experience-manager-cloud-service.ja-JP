---
title: サポートされているクライアントプラットフォーム
description: AEMを使用したコンテンツのオーサリングと、Adobe Experience Manager as a Cloud Serviceを使用して公開されたサイトへのアクセスでサポートされているブラウザーについて説明します。
topic-tags: platform
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
source-git-commit: 22d4e6b5f87221b2739cf1dd9d59b4652a014316
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 26%

---


# サポートされているクライアントプラットフォーム {#supported-platforms}

AEMを使用したコンテンツのオーサリングと、Adobe Experience Manager as a Cloud Serviceを使用して公開されたサイトへのアクセスでサポートされているブラウザーについて説明します。

>[!TIP]
>
>このドキュメントでは、AEM as a Cloud Serviceがサポートするクライアントプラットフォームについて説明します。 AEM プロジェクト開発のためのビルド環境について詳しくは、「ビルド環境 [ を参照してください。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md)

## サポートレベル {#support-levels}

Adobeは、AEM クライアントプラットフォームに対して次のレベルのサポートを定義します。

| サポートレベル | 説明 |
|---|---|
| A：サポート対象 | アドビはこの構成への完全なサポートと保守を提供します。この構成は、アドビの品質保証プロセスでカバーされます。 |
| R：制限サポート | サポートでは、プロジェクトで設定を使用するために、Adobeへの正式なリクエストが必要です。 Adobeによる確認が完了すると、Adobeは、制限されたサポートプログラム内で完全なサポートを提供します。 詳しくは、アドビカスタマーケアにお問い合わせください。 |
| Z：サポートされていません | この設定はサポートされていません。アドビは、この設定が動作するかどうかに関する一切の表明をせず、この設定をサポートしません。 |

## コンテンツのオーサリングでサポートされるブラウザー {#authoring}

AEMのユーザーインターフェイスは、ノートブック、デスクトップコンピューター、タブレットデバイス（Apple iPadやMicrosoft Surface など）で見つかる大きな画面に最適化されています。 電話のフォームファクターは、オーサリングのユースケースではサポートされていません。

Adobe Experience Manager ユーザーインターフェイスは、[ オーサリング方法 ](/help/edge/authoring-methods.md) に応じて、次のクライアントプラットフォームで機能します。

* [ユニバーサルエディター](/help/sites-cloud/authoring/universal-editor/authoring.md)
* [ページエディター](/help/sites-cloud/authoring/page-editor/introduction.md)
* [2}Sidekickを使用した ](/help/edge/docs/authoring.md) ドキュメントベースのオーサリング ](/help/edge/docs/sidekick.md)[

すべてのブラウザーは、デフォルトのプラグインとアドオンのセットを使用してテストされます。

| ブラウザー | ユニバーサルエディターのサポートレベル | ページエディターのサポートレベル | Sidekickのサポートレベル |
|---|---|---|---|
| GoogleChrome（エバーグリーン） | A：サポート対象 | A：サポート対象 | A：サポート対象 |
| Microsoft Edge（エバーグリーン） | A：サポート対象 | A：サポート対象 | Z：サポートされていません |
| Mozilla Firefox （エバーグリーン） | A：サポート対象 | A：サポート対象 | Z：サポートされていません |
| Mozilla Firefox 最新 ESR [1] | A：サポート対象 | A：サポート対象 | Z：サポートされていません |
| macOSの Safari （エバーグリーン） | A：サポート対象 | A：サポート対象 | Z：サポートされていません |
| iOS（エバーグリーン）の Safari [2] | Z：サポートされていません | A：サポート対象 | Z：サポートされていません |

1. Firefox の拡張サポートリリース（[mozilla.org について詳しくはこちらを参照 ](https://www.mozilla.org/en-US/firefox/enterprise/)）
1. Apple iPadのみをサポート

>[!NOTE]
>
>**リリースサイクルの短いブラウザーのサポート：**
>
>Firefox、Chrome、Edgeの各リリースは、定期的にアップデートされます。 Adobeは、これらのブラウザーの今後のバージョンに対して、上記のサポートレベルを維持することに全力を注いでいます。

## Web サイトでサポートされているブラウザー {#websites}

AEMでレンダリングされる web サイトのブラウザーサポートは、AEM ページテンプレート、ブロック、デザイン、コンポーネント出力の実装によって異なります。 したがって、プロジェクトを実装する開発者は、最終的にサイトの互換性を制御できます。

AEM[ プロジェクトボイラープレート ](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md#create-github-project)、[ コアコンポーネント ](/help/implementing/developing/components/overview.md#aem-core-components)、[WKND サンプルサイト ](/help/implementing/developing/introduction/develop-wknd-tutorial.md) はすべて、最新のすべてのブラウザーと互換性があります。
