---
title: コードリファクタリングツール用 Unified Experience
description: コードリファクタリングツール用の統合エクスペリエンスについて説明します。
exl-id: daee0e2d-1e2b-41a3-acab-fc59142d0e05
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 37%

---

# コードリファクタリングツール用 Unified Experience {#unified-experience}

Adobeは、Adobe Experience Manager（AEM）as a Cloud Service環境との互換性を保つために必要な、コードリファクタリングタスクの一部を自動化するツールを開発しました。 様々なコードリファクタリングツールのインストールとセットアップに関連する複雑さを軽減するために、Adobeでは、コードとリポジトリを操作するツールを統合するプラグインを開発しました。

## メリット {#benefits}

Unified Experience プラグインには次のようなメリットがあります。

* ソースコードで機能するツールを 1 つの `node.js` アプリケーションに統合し、`aio-cli ` プラグインとして公開して、ユーザーに対して一貫性のあるユーザーエクスペリエンスを提供する。

* 1 つのコマンドですべてのツールを実行できる一方、必要に応じて特定のツールを柔軟に実行することもできます。

* エクスペリエンスの一貫性を維持しながら、新しいツールの追加を簡素化します。

## プラグインについて {#understanding-plugin}

`aio-cli-plugin-aem-cloud-service-migration` プラグインは、次の 2 つの主要な部分で構成されています。

* **ユーザーインターフェイス**

   * `aio-cli` 1 つ以上のコードリファクタリングツールを実行するコマンド（ツールを連結して順番に実行する）。
   * 必要な入力パラメーターを取り込む `config.yaml`

* **基礎となるコードリファクタリングツールスイート**

  コードリファクタリングツールは、次の方法で機能を実行します。

   * お客様のコードの各セクションをスキャンし、コードを操作して（ベストプラクティスのコード実装に基づいて）、検証およびデプロイ可能な出力を生成します。

   * 実行中に実行された操作を記録するサマリレポートを生成する。

## 入手方法 {#availability}

参照： [Git リソース：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) の使用方法と、GitHub でオープンソース化されているこのプラグインコードへの投稿方法について説明します。

>[!NOTE]
>現在、このプラグインは AEM Dispatcher Converter および Repository Modenizer と統合されています。
