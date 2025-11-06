---
title: Cloud Manager での Git の使用
description: Cloud Manager の Git リポジトリを使用する方法と、オンプレミスで顧客管理された独自の Git リポジトリを Cloud Manager と統合する方法について説明します。
exl-id: 57e71b8a-4546-4d7f-825c-a1637d08e608
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 100%

---

# Cloud Manager での Git の使用 {#git-integration}

Adobe Cloud Manager には、Cloud Manager の CI／CD パイプラインを使用したコードのデプロイに使用される単一の Git リポジトリがプロビジョニングされます。

Cloud Manager の Git リポジトリをそのまま使用することもできますが、顧客が管理する Git リポジトリを Cloud Manager と統合することもできます。

## Git 統合の概要 {#git-integration-overview}

このビデオシリーズでは、顧客が管理する Git リポジトリと Cloud Manager と統合する際の、次のようなユースケースをいくつかご紹介します。

* [初期同期](#initial-sync)
* [基本分岐戦略](#branching-strategy)
* [機能分岐の開発](#feature-development)
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

機能分岐は、非実稼動パイプラインでコードの品質と検証テストを行うために、顧客が管理する Git リポジトリ内でコード変更を隔離したり、Cloud Manager の Git リポジトリと同期したりするのに使用します。

>[!VIDEO](https://video.tv.adobe.com/v/28723/?quality=12)

## 実稼動のデプロイメント {#production-deployment}

顧客管理 Git リポジトリで本番リリースのコードを準備し、Cloud Manager の Git リポジトリと同期して、ステージ環境と本番環境にデプロイします。

>[!VIDEO](https://video.tv.adobe.com/v/28724/?quality=12)

## リリースタグの同期 {#sync-tags}

Cloud Manager の Git リポジトリのリリースタグを、顧客が管理する Git リポジトリと同期させて、ステージング環境と本番環境にデプロイされたコードを把握できるようにします。

>[!VIDEO](https://video.tv.adobe.com/v/28725/?quality=12)

## その他のリソース {#additional-resources}

* [GitHub リソース](https://docs.github.com/ja/get-started/getting-started-with-git/set-up-git)
* [Atlassian Git チュートリアル](https://www.atlassian.com/git/tutorials/what-is-version-control)
* [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)
