---
title: コードリファクタリングツール用 Unified Experience
description: コードリファクタリングツール用の Unified Experience の詳細。
exl-id: daee0e2d-1e2b-41a3-acab-fc59142d0e05
source-git-commit: 78ead5f15c2613d9c3bed3025b43423a66805c59
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 38%

---

# コードリファクタリングツール用 Unified Experience {#unified-experience}

Adobeは、Adobe Experience Manager(AEM)as a Cloud Serviceとの互換性が必要なコードリファクタリングタスクの一部を自動化するツールを開発しました。 様々なコードリファクタリングツールのインストールと設定に伴う複雑さを軽減するために、Adobeでは、コードとリポジトリで動作するツールを統合するプラグインを開発しました。

## メリット {#benefits}

Unified Experience プラグインには次のようなメリットがあります。

* ソースコードで機能するツールを 1 つの `node.js` アプリケーションに統合し、`aio-cli ` プラグインとして公開して、ユーザーに対して一貫性のあるユーザーエクスペリエンスを提供する。

* 1 つのコマンドを使用してすべてのツールを実行し、必要に応じて特定のツールを柔軟に実行できます。

* エクスペリエンスの一貫性を維持しながら、新しいツールの追加を簡素化します。

## プラグインについて {#understanding-plugin}

`aio-cli-plugin-aem-cloud-service-migration` プラグインは、次の 2 つの主要な部分で構成されています。

* **ユーザーインターフェイス**

   * `aio-cli` 1 つ以上のコードリファクタリングツールを実行するコマンド（ツールを連結して順番に実行する方法）
   * 必要な入力パラメーターを取り込む `config.yaml`

* **基礎となるコードリファクタリングツールスイート**

  コードリファクタリングツールは、次の方法で機能を実行します。

   * 顧客のコードの各セクションをスキャンし、（コードの実装に基づくベストプラクティスに基づく）コードを操作して出力を生成し、検証して導入する。

   * 実行中に実行された操作を記録するサマリレポートを生成する。

## 入手方法 {#availability}

詳しくは、 [Git リソース：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) 使用方法や、GitHub でオープンソースになっているこのプラグインコードに貢献する方法について説明します。

>[!NOTE]
>現在、このプラグインは AEM Dispatcher Converter および Repository Modenizer と統合されています。
