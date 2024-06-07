---
title: コードリファクタリングツール用 Unified Experience
description: コードリファクタリングツール用 Unified Experience について説明します。
exl-id: daee0e2d-1e2b-41a3-acab-fc59142d0e05
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: ht
source-wordcount: '266'
ht-degree: 100%

---

# コードリファクタリングツール用 Unified Experience {#unified-experience}

アドビでは、Adobe Experience Manager（AEM）as a Cloud Service との互換性が必要なコードリファクタリングタスクの一部を自動化するツールを開発しました。様々なコードリファクタリングツールのインストールと設定に伴う複雑さを軽減するため、アドビではコードとリポジトリで動作するツールを統合するプラグインを開発しました。

## メリット {#benefits}

Unified Experience プラグインには次のようなメリットがあります。

* ソースコードで機能するツールを 1 つの `node.js` アプリケーションに統合し、`aio-cli ` プラグインとして公開して、ユーザーに対して一貫性のあるユーザーエクスペリエンスを提供する。

* 1 つのコマンドですべてのツールを実行すると同時に、必要に応じて特定のツールを実行する柔軟性も提供する。

* エクスペリエンスの一貫性を維持しながら、新しいツールの追加を簡略化する。

## プラグインについて {#understanding-plugin}

`aio-cli-plugin-aem-cloud-service-migration` プラグインは、次の 2 つの主要な部分で構成されています。

* **ユーザーインターフェイス**

   * 1 つ以上のコードリファクタリングツールを実行する `aio-cli` コマンド（ツールを連結して順番に実行する）。
   * 必要な入力パラメーターを取り込む `config.yaml`

* **基礎となるコードリファクタリングツールスイート**

  コードリファクタリングツールは、次の方法で機能を実行します。

   * 顧客のコードの各セクションをスキャンし、（ベストプラクティスのコード実装に基づいて）コードを操作して出力を生成し、検証してデプロイする。

   * 実行中に行われた操作を記録する概要レポートを生成する。

## 入手方法 {#availability}

使用方法および GitHub でオープンソースになっているこのプラグインコードに貢献する方法について詳しくは、[Git リソース：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) を参照してください。

>[!NOTE]
>現在、このプラグインは AEM Dispatcher Converter および Repository Modenizer と統合されています。
