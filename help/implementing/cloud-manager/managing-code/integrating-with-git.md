---
title: Cloud Manager での git の使用
description: Cloud Manager の Git リポジトリを使用する方法と、オンプレミスで顧客管理された独自の Git リポジトリを Cloud Manager と統合する方法について説明します。
exl-id: 57e71b8a-4546-4d7f-825c-a1637d08e608
source-git-commit: a9303c659730022b7417fc9082dedd26d7cbccca
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 47%

---

# Cloud Manager での git の使用 {#git-integration}

Adobe Cloud Manager には、Cloud Manager の CI／CD パイプラインを使用したコードのデプロイに使用される単一の Git リポジトリーがプロビジョニングされます。

Cloud Manager の Git リポジトリは、すぐに使用できますが、顧客が管理する Git リポジトリを Cloud Manager と統合することもできます。

## Git 統合の概要 {#git-integration-overview}

このビデオシリーズでは、顧客が管理する Git リポジトリを Cloud Manager と統合する際の使用例をいくつか紹介します。

* [初期同期](#initial-sync)
* [基本分岐戦略](#branching-strategy)
* [機能ブランチの開発](#feature-development)
* [実稼動のデプロイメント](#production-deployment)
* [リリースタグの同期](#sync-tags)

このビデオシリーズは、Git とソース管理に関する基本的な知識を前提としています。Git について詳しくは、以下の[その他のリソース](#additional-resources)を参照してください。

>[!VIDEO](https://video.tv.adobe.com/v/28710/)

このビデオシリーズで概要を説明する手順と命名規則は、Cloud Manager で顧客が管理する Git リポジトリを使用する際のベストプラクティスです。 表示される規則とワークフローは、個々の使用例に合わせて適合していることが予想されます。

## 初期同期 {#initial-sync}

このビデオでは、顧客が管理する Git リポジトリを Cloud Manager の Git リポジトリと同期するための最初の手順を説明します。

>[!VIDEO](https://video.tv.adobe.com/v/28711/?quality=12)

## 基本分岐戦略 {#branching-strategy}

このビデオでは、基本分岐戦略について説明します。

>[!VIDEO](https://video.tv.adobe.com/v/28712/?quality=12)

## 機能ブランチの開発 {#feature-development}

機能ブランチを使用して、顧客が管理する Git リポジトリー内のコード変更を分離し、Cloud Manager の Git リポジトリーと同期して、コードの品質と検証のテストに非実稼動パイプラインを使用します。

>[!VIDEO](https://video.tv.adobe.com/v/28723/?quality=12)

## 実稼動のデプロイメント {#production-deployment}

顧客管理 Git リポジトリーで実稼動版リリースのコードを準備し、Cloud Manager の Git リポジトリーと同期して、ステージ環境と実稼動環境にデプロイします。

>[!VIDEO](https://video.tv.adobe.com/v/28724/?quality=12)

## リリースタグの同期 {#sync-tags}

Cloud Manager の Git リポジトリのリリースタグを、顧客が管理する Git リポジトリに同期して、ステージング環境と実稼動環境にデプロイされたコードを明確に把握できるようにします。

>[!VIDEO](https://video.tv.adobe.com/v/28725/?quality=12)

## その他のリソース {#additional-resources}

* [GitHub リソース](https://try.github.io)
* [Atlassian Git チュートリアル](https://www.atlassian.com/git/tutorials/what-is-version-control)
* [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)
