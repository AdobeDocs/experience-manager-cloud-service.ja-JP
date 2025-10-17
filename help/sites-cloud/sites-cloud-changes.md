---
title: AEM Cloud Service の AEM Sites の主な変更点
description: AEM Sites as a Cloud Service を使用して作成および管理する方法と、AEM Cloud Service の AEM Sites に対する重要な変更点について説明します。
exl-id: 60b1aec4-75a0-459f-bf77-8d8c1af757ce
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 3761019b42ddc4b3a6cc904afe91b47eb3d99ac6
workflow-type: ht
source-wordcount: '526'
ht-degree: 100%

---


# AEM Sites as a Cloud Service の主な変更点 {#notable-changes}

AEM Sites as a Cloud Service は、クラウドネイティブな AEM as a Cloud Service プラットフォームの一部として、エクスペリエンス管理機能を提供します。AEM Sites as a Cloud Service には、AEM as a Cloud Service の主なメリット（クラウドネイティブの拡張性、稼動時間、最新状態の維持など）に加え、Sites 固有の変更や追加もいくつか含まれています。

>[!NOTE]
>このドキュメントでは、AEM Sites の主な変更点について重点的に説明します。AEM as a Cloud Service およびその他のモジュールに関する一般的な変更点については、以下を参照してください。
>
>* [Adobe Experience Manager as a Cloud Service の概要](/help/overview/introduction.md)
>* [AEM as a Cloud Service の概要 - 新機能と相違点](/help/overview/what-is-new-and-different.md)
>* Adobe Experience Manager as a Cloud Service の[アーキテクチャ](/help/overview/architecture.md)
>* [AEM as a Cloud Service の主な変更点（リリースノート）](/help/release-notes/aem-cloud-changes.md)
>* [AEM Assets as a Cloud Service の主な変更点](/help/assets/assets-cloud-changes.md)
>* [AEM Assets as a Cloud Service の概要](/help/assets/overview.md)
>* [Adobe Experience Manager as a Cloud Service のチュートリアル](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html?lang=ja)

AEM Sites as a Cloud Service の変更点と追加機能は次のとおりです。

* [非同期ページ操作](#asynchronous-page-operations)
* [新しい参照サイトおよびチュートリアル](#new-reference-site-and-tutorial)

## 非同期ページ操作 {#asynchronous-page-operations}

AEM Cloud Service では、従来 UI をブロックしていた操作は、バックグラウンドで実行される小さなタスクに分解されました。

* ページの移動
* ページのロールアウト

<!--
The initiator of such actions can check their status in a new UI at `/mnt/overlay/dam/gui/content/asyncjobs.html`.
-->

非同期ジョブのステータスは、[バックグラウンド操作ダッシュボード](/help/operations/asynchronous-jobs.md)で表示できます。

>[!NOTE]
>
>この新機能を利用するためにシステムのユーザーに必要な変更はありません。ここでは、以前のオンプレミスバージョンの AEM から動作が変更された点としてのみ記載しておきます。

## 新しい参照サイトおよびチュートリアル {#new-reference-site-and-tutorial}

[WKND](https://wknd.site/)（新しい AEM の参照用サイト）が更新および公開されました。このサイトには、AEM で web サイトを構築するためのベストプラクティスや、AEM で使用可能な機能、コンポーネント、デプロイメントモデルの包括的なセットが反映されています。新しい参照サイトと[付属のチュートリアル](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=ja)では、プロジェクトの設定、コアコンポーネント、編集可能なテンプレート、クライアントライブラリ、Adobe Experience Manager Sites を使用したコンポーネント開発などの基本的なトピックについて説明します。

これまで、AEM と共にデフォルトで We.Retail がインストールされていました（実稼動モードで開始した場合を除く）。AEM as a Cloud Service では、参照サイトはデフォルトではインストールされません。 代わりに、更新された WKND 参照サイトコードを含んだ [Git リポジトリー](https://github.com/adobe/aem-guides-wknd/)および[付属のチュートリアル](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=ja)が提供されます。

## 実行時に使用できない機能 {#capabilities-not-available-at-runtime}

AEM as a Cloud Service は常に有効で、常に最新の状態に保たれています。それを実現するには、不変コンテンツと可変コンテンツで AEM リポジトリーを分離し、実行時に不変コンテンツにアクセスできないようにする必要があります。可変コンテンツと不変コンテンツについて詳しくは、[リポジトリの可変領域と不変領域](/help/implementing/developing/introduction/aem-project-content-package-structure.md#mutable-vs-immutable)を参照してください。

実行時には不変コンテンツにアクセスできないので、AEM Sites の次の操作は実行時に使用できません。

* i18n 辞書の翻訳
* AEM Sites ページエディターの開発者モード

これらの機能を、AEM as a Cloud Service のローカルのスタンドアロン開発者インスタンスを通じて使用し、AEM as a Cloud Service の Git リポジトリー内のコンテンツやコードを更新することはできますが、ホストされたランタイムインスタンスでは使用できません。
