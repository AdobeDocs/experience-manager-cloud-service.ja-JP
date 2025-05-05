---
title: Cloud Manager での Git の使用
description: Cloud Manager の Git リポジトリを使用する方法と、オンプレミスで顧客管理された独自の Git リポジトリを Cloud Manager と統合する方法について説明します。
exl-id: 57e71b8a-4546-4d7f-825c-a1637d08e608
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 80206fc1396896fe45e2c959c78a0bf30eba71c5
workflow-type: ht
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

>[!VIDEO](https://video.tv.adobe.com/v/31425?captions=jpn)

このビデオシリーズで概要を説明する手順と命名規則は、Cloud Manager で顧客管理の Git リポジトリを使用する際のベストプラクティスです。ここで説明されている規則とワークフローは、個々のユースケースに調整してください。

## 初期同期 {#initial-sync}

このビデオでは、顧客が管理する Git リポジトリを Cloud Manager の Git リポジトリと同期するための最初の手順を説明します。

>[!VIDEO](https://video.tv.adobe.com/v/31424/?quality=12&captions=jpn)

## 基本分岐戦略 {#branching-strategy}

このビデオでは、基本的な分岐戦略について説明します。

>[!VIDEO](https://video.tv.adobe.com/v/31423/?quality=12&captions=jpn)

## 機能分岐の開発 {#feature-development}

機能分岐は、非実稼動パイプラインでコードの品質と検証テストを行うために、顧客が管理する Git リポジトリ内でコード変更を隔離したり、Cloud Manager の Git リポジトリと同期したりするのに使用します。

>[!VIDEO](https://video.tv.adobe.com/v/31422/?quality=12&captions=jpn)

## 実稼動のデプロイメント {#production-deployment}

顧客管理 Git リポジトリで実稼動版リリースのコードを準備し、Cloud Manager の Git リポジトリと同期して、ステージ環境と実稼動環境にデプロイします。

>[!VIDEO](https://video.tv.adobe.com/v/31421/?quality=12&captions=jpn)

## リリースタグの同期 {#sync-tags}

Cloud Manager の Git リポジトリのリリースタグを、顧客が管理する Git リポジトリと同期させて、ステージング環境と実稼動環境にデプロイされたコードを把握できるようにします。

>[!VIDEO](https://video.tv.adobe.com/v/31420/?quality=12&captions=jpn)

## その他のリソース {#additional-resources}

* [GitHub リソース](https://docs.github.com/ja/get-started/getting-started-with-git/set-up-git)
* [Atlassian Git チュートリアル](https://www.atlassian.com/git/tutorials/what-is-version-control)
* [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)
