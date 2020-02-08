---
title: AEMクラウドサービスのAEMサイトに対する注目すべき変更
description: 'AEMクラウドサービスのAEMサイトに対する注目すべき変更 '
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# クラウドサービスとしてのAEMサイトに対する注目すべき変更 {#notable-changes}

クラウドサービスとしてのAEMサイトは、クラウドネイティブのAEMの一部として、クラウドサービスプラットフォームとしてエクスペリエンス管理機能を提供します。 クラウドサービスとしてのAEMの主なメリット（クラウドネイティブの拡張性、稼働時間、常に最新の状態など）に加え、クラウドサービスとしてのAEMサイトには、サイト固有の変更や追加が数多く含まれています。

>[!NOTE]
>このドキュメントでは、AEMサイトに対する注目すべき変更点について説明します。 クラウドでのAEMの一般的な変更点については、以下を参照してください。
>
>* [クラウドサービスとしてのAdobe Experience Manager(AEM)の主な変更点](/help/release-notes/aem-cloud-changes.md)


AEMサイトでのクラウドサービスとしての変更点と追加点は次のとおりです。

* [非同期ページ操作](#asynchronous-page-operations)
* [新しいリファレンスサイトとチュートリアル](#new-reference-site-and-tutorial)

## 非同期ページ操作 {#asynchronous-page-operations}

AEM cloudサービスでは、従来からUIをブロックしていた操作は、バックグラウンドで実行される小さなタスクに分類されています。

* ページの移動
* ロールアウトページ

このようなアクションの開始者は、の新しいUIでそのステータスを確認できま `/mnt/overlay/dam/gui/content/asyncjobs.html`す。

>[!NOTE]
>
>この新機能を利用するためにシステムのユーザーが必要とする変更はありません。 ここでは、以前のオンプレミスバージョンのAEMとの動作の変更についてだけ説明します。

## 新しいリファレンスサイトとチュートリアル {#new-reference-site-and-tutorial}

[新しいAEM](https://wknd.site/)リファレンスサイトWKNDが更新および公開され、AEMでWebサイトを構築するためのベストプラクティス、およびAEMで利用可能な機能、コンポーネント、デプロイメントモデルの包括的なセットが反映されました。 新しいリファレンスサイトと付属のチ [ュートリアルでは](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) 、プロジェクトの設定、コアコンポーネント、編集可能なテンプレート、クライアントライブラリ、Adobe Experience Manager Sitesを使用したコンポーネントの開発など、基本的なトピックについて説明します。

以前は、We.Retailは、デフォルトでAEMと共にインストールされていました（実稼働モードで開始した場合を除く）。  今後、リファレンスサイトはデフォルトでインストールされなくなります。  代わりに、 [gitレポートと](https://github.com/adobe/aem-guides-wknd/) 、更新 [](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) されたWKNDリファレンスサイトコードを含む付属のチュートリアルが提供されます。

## 実行時には使用できない機能 {#capabilities-not-available-at-runtime}

AEM as a Cloud Serviceは常にオンで、常に最新です。 これを行うには、不変コンテンツと可変コンテンツでAEMリポジトリを分離し、実行時に不変コンテンツにアクセスできないようにする必要があります。 可変コンテンツと不変コンテンツについて詳しくは、「リポジ [トリの可変領域と不変領域」を参照してください](/help/implementing/developing/introduction/aem-project-content-package-structure.md#mutable-vs-immutable)。

不変コンテンツに実行時にアクセスできないため、次のAEMサイト操作は実行時に使用できません。

* i18n辞書翻訳
* AEMサイトページエディターの開発者モード

これらの機能は、AEMのローカルのスタンドアロン開発者インスタンスをクラウドサービスとして使用し、AEM内のコンテンツやコードをクラウドサービスGITリポジトリとして更新するために使用できますが、ホストされたランタイムインスタンスでは使用できません。
