---
title: Cloud Manager での Git の使用
description: Cloud Manager の Git リポジトリを使用する方法と、オンプレミスで顧客管理された独自の Git リポジトリを Cloud Manager と統合する方法について説明します。
exl-id: 57e71b8a-4546-4d7f-825c-a1637d08e608
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: 922d77a0d93657b338581b38b086219b9ebee8cc
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 57%

---

# Cloud Manager での Git の使用 {#git-integration}

Adobe Cloud Manager には、Cloud Manager の CI/CD パイプラインを使用したコードのデプロイに使用される単一の Git リポジトリがプロビジョニングされます。

Cloud ManagerのGit リポジトリを使用できますが、お客様が管理するGit リポジトリをCloud Managerと統合するオプションもあります。

## Git 統合の概要 {#git-integration-overview}

このビデオシリーズでは、お客様が管理するGit リポジトリをCloud Managerと統合する際に、次のようないくつかのユースケースについて説明します。

* [初期同期](#initial-sync)
* [基本分岐戦略](#branching-strategy)
* [機能分岐の開発](#feature-development)
* [実稼動のデプロイメント](#production-deployment)
* [リリースタグの同期](#sync-tags)

このビデオシリーズでは、Gitとソース制御管理に関する基本的な知識が必要です。 Git について詳しくは、[以下のその他のリソース](#additional-resources)を参照してください。

>[!VIDEO](https://video.tv.adobe.com/v/31425?captions=jpn)

このビデオシリーズで説明されている手順と命名規則は、Cloud Managerでユーザーが管理するGit リポジトリを操作するためのベストプラクティスを示しています。 ここで説明されている規則とワークフローは、個々のユースケースに調整してください。

## 初期同期 {#initial-sync}

このビデオでは、顧客が管理する Git リポジトリを Cloud Manager の Git リポジトリと同期するための最初の手順を説明します。

>[!VIDEO](https://video.tv.adobe.com/v/31424/?captions=jpn&quality=12)

## 基本分岐戦略 {#branching-strategy}

このビデオでは、基本的な分岐戦略について説明します。

>[!VIDEO](https://video.tv.adobe.com/v/31423/?captions=jpn&quality=12)

## 機能分岐の開発 {#feature-development}

機能分岐を使用して、顧客が管理する Git リポジトリ内のコード変更を分離し、Cloud Manager の Git リポジトリと同期して、コードの品質と検証テストに実稼動以外のパイプラインを使用します。

>[!VIDEO](https://video.tv.adobe.com/v/31422/?captions=jpn&quality=12)

## 実稼動デプロイメント {#production-deployment}

お客様が管理するGit リポジトリで実稼動リリース用のコードを準備し、Cloud ManagerのGit リポジトリと同期して、ステージング環境と実稼動環境にデプロイします。

>[!VIDEO](https://video.tv.adobe.com/v/31421/?captions=jpn&quality=12)

## リリースタグの同期 {#sync-tags}

ステージング環境と実稼動環境にデプロイされたコードを可視化するには、Cloud Manager Git リポジトリからリリースタグをお客様が管理するGit リポジトリに同期します。

>[!VIDEO](https://video.tv.adobe.com/v/31420/?captions=jpn&quality=12)

## その他のリソース {#additional-resources}

* [GitHubのリソース](https://docs.github.com/ja/get-started/getting-started-with-git/set-up-git)
* [Atlassian Git チュートリアル](https://www.atlassian.com/git/tutorials/what-is-version-control)
* [Git チートシート](https://education.github.com/git-cheat-sheet-education.pdf)
