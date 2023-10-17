---
title: Cloud Manager での git の使用
description: Cloud Manager の Git リポジトリを使用する方法と、オンプレミスで顧客管理された独自の Git リポジトリを Cloud Manager と統合する方法について説明します。
exl-id: 57e71b8a-4546-4d7f-825c-a1637d08e608
source-git-commit: bceec9ea6858b1c4c042ecd96f13ae5cac1bbee5
workflow-type: ht
source-wordcount: '316'
ht-degree: 100%

---

# Cloud Manager での git の使用 {#git-integration}

Adobe Cloud Manager には、Cloud Manager の CI／CD パイプラインを使用したコードのデプロイに使用される単一の Git リポジトリがプロビジョニングされます。

Cloud Manager の Git リポジトリをそのまま使用することもできますが、顧客が管理する Git リポジトリを Cloud Manager と統合することもできます。

## Git 統合の概要 {#git-integration-overview}

このビデオシリーズでは、顧客が管理する Git リポジトリと Cloud Manager と統合する際の、次のようなユースケースをいくつかご紹介します。

* [初期同期](#initial-sync)
* [基本分岐戦略](#branching-strategy)
* [機能ブランチの開発](#feature-development)
* [実稼動のデプロイメント](#production-deployment)
* [リリースタグの同期](#sync-tags)

このビデオシリーズは、Git とソース管理に関する基本的な知識を前提としています。Git について詳しくは、以下の[その他のリソース](#additional-resources)を参照してください。

>[!VIDEO](https://video.tv.adobe.com/v/28710/)

このビデオシリーズで概要を説明する手順と命名規則は、Cloud Manager で顧客管理の Git リポジトリを使用する際のベストプラクティスです。ここで説明されている規則とワークフローは、個々のユースケースに調整してください。

## 初期同期 {#initial-sync}

このビデオでは、顧客が管理する Git リポジトリを Cloud Manager の Git リポジトリと同期するための最初の手順を説明します。

>[!VIDEO](https://video.tv.adobe.com/v/28711/?quality=12)

## 基本分岐戦略 {#branching-strategy}

このビデオでは、基本的な分岐戦略について説明します。

>[!VIDEO](https://video.tv.adobe.com/v/28712/?quality=12)

## 機能分岐の開発 {#feature-development}

機能分岐を使用して、顧客が管理する Git リポジトリ内のコード変更を分離し、Cloud Manager の Git リポジトリと同期して、コードの品質と検証テストに非実稼動パイプラインを使用します。

>[!VIDEO](https://video.tv.adobe.com/v/28723/?quality=12)

## 実稼動デプロイメント {#production-deployment}

顧客管理 Git リポジトリで実稼動版リリースのコードを準備し、Cloud Manager の Git リポジトリと同期して、ステージ環境と実稼動環境にデプロイします。

>[!VIDEO](https://video.tv.adobe.com/v/28724/?quality=12)

## リリースタグの同期 {#sync-tags}

Cloud Manager の Git リポジトリのリリースタグを、顧客が管理する Git リポジトリと同期させて、ステージング環境と実稼動環境にデプロイされたコードを把握できるようにします。

>[!VIDEO](https://video.tv.adobe.com/v/28725/?quality=12)

## その他のリソース {#additional-resources}

* [GitHub リソース](https://try.github.io)
* [Atlassian Git チュートリアル](https://www.atlassian.com/git/tutorials/what-is-version-control)
* [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)
