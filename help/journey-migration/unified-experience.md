---
title: コードリファクタリングツール用 Unified Experience
description: コードリファクタリングツール用の Unified Experience の詳細。
exl-id: daee0e2d-1e2b-41a3-acab-fc59142d0e05
source-git-commit: 8c73805b6ed1b7a03c65b4d21a4252c1412a5742
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 87%

---

# コードリファクタリングツール用 Unified Experience {#unified-experience}

AEM as a Cloud Service との互換性が必要なコードリファクタリングタスクの一部を自動化するツールを開発しました。様々なコードリファクタリングツールのインストールと設定に伴う複雑さを軽減するため、コードおよびリポジトリーで動作するツールを統合するプラグインを開発しました。

## メリット {#benefits}

Unified Experience プラグインには次のようなメリットがあります。

* ソースコードで機能するツールを 1 つの `node.js` アプリケーションに統合し、`aio-cli ` プラグインとして公開して、ユーザーに対して一貫性のあるユーザーエクスペリエンスを提供する。

* 1 つのコマンドですべてのツールを実行できると同時に、必要に応じて特定のツールを実行できる柔軟性も提供する。

* エクスペリエンスの一貫性を維持しながら、新しいツールの追加を簡略化する拡張機能を提供する。

## プラグインについて {#understanding-plugin}

`aio-cli-plugin-aem-cloud-service-migration` プラグインは、次の 2 つの主要な部分で構成されています。

* **ユーザーインターフェイス**

   * 1 つ以上のコードリファクタリングツールを実行する `aio-cli` コマンド（ツールを連結して順番に実行する）
   * 必要な入力パラメーターを取り込む `config.yaml`

* **基礎となるコードリファクタリングツールスイート**

  コードリファクタリングツールは、次の方法で機能を実行します。

   * 顧客コードの各セクションをスキャンし、（コードの実装に基づくベストプラクティスに基づく）コードを操作して出力を生成し、検証して導入する。

   * 実行中に実行された操作を記録するサマリレポートを生成する。

## 入手方法 {#availability}

詳しくは、 [Git リソース：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) の使用方法と、GitHub でオープンソースになっているこのプラグインコードに貢献する方法について説明します。

>[!NOTE]
>現在、このプラグインは AEM Dispatcher Converter および Repository Modenizer と統合されています。
