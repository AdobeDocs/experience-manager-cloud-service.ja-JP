---
title: Git との統合
description: Git との統合 - クラウドサービス
translation-type: tm+mt
source-git-commit: 23349f3350631f61f80b54b69104e5a19841272f
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 100%

---


# Git と Adobe Cloud Manager の統合 {#git-integration}

Adobe Cloud Manager には、Cloud Manager の CI/CD パイプラインを使用したコードのデプロイに使用される単一の Git リポジトリがプロビジョニングされます。お客様は、Cloud Manager の Git リポジトリをすぐに使用できます。オプションとして、オンプレミスまたは&#x200B;**顧客管理**&#x200B;の Git リポジトリを Cloud Manager と統合することもできます。

## Git 統合の概要  {#git-integration-overview}

>[!VIDEO](https://video.tv.adobe.com/v/28710/)

このビデオシリーズでは、顧客が管理する Git リポジトリと Cloud Manager の統合に関する使用例をいくつか紹介します。

* [初期同期](#initial-sync)
* [基本分岐戦略 ](#branching-strategy)
* [機能ブランチの開発](#feature-development)
* [実稼動のデプロイメント](#production-deployment)
* [リリースタグの同期](#sync-tags)

このビデオシリーズは、Git とソース管理に関する基本的な知識を前提としています。Git について詳しくは、以下の[その他のリソース](#additional-resources)を参照してください。

>[!NOTE]
>
>このビデオシリーズで概要を説明する手順と命名規則は、顧客管理 Git リポジトリと Cloud Manager を使用する際のベストプラクティスです。規則とワークフローは、個々の開発チームに合わせて調整してください。

## 初期同期 {#initial-sync}

顧客が管理する Git リポジトリを Cloud Manager の Git リポジトリと同期するための最初の手順。

>[!VIDEO](https://video.tv.adobe.com/v/28711/?quality=12)

## 基本分岐戦略 {#branching-strategy}

以下のビデオに従って、基本分岐戦略を学びます。

>[!VIDEO](https://video.tv.adobe.com/v/28712/?quality=12)

## 機能ブランチの開発 {#feature-development}

機能ブランチを使用して、顧客が管理する Git リポジトリ内のコード変更を分離し、Cloud Manager の Git リポジトリと同期して、コードの品質と検証のテストに非実稼動パイプラインを使用します。

>[!VIDEO](https://video.tv.adobe.com/v/28723/?quality=12)

## 実稼動のデプロイメント {#production-deployment}

顧客管理 Git リポジトリで実稼動版リリースのコードを準備し、Cloud Manager の Git リポジトリと同期して、ステージ環境と実稼動環境にデプロイします。

>[!VIDEO](https://video.tv.adobe.com/v/28724/?quality=12)

## リリースタグの同期 {#sync-tags}

Cloud Manager の Git リポジトリのリリースタグを、顧客管理 Git リポジトリと同期させて、ステージ環境と実稼動環境にデプロイされたコードを明確に把握できるようにします。

>[!VIDEO](https://video.tv.adobe.com/v/28725/?quality=12)

## その他のリソース {#additional-resources}

* [GitHub リソース](https://try.github.io)
* [Atlassian Git チュートリアル](https://www.atlassian.com/git/tutorials/what-is-version-control)
* [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)