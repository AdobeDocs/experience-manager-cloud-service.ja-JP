---
title: コードリファクタリングツールの統合エクスペリエンス
description: コードリファクタリングツールの統合エクスペリエンス
translation-type: tm+mt
source-git-commit: d6fa0d8bb7d5e251e51a3e4ffd93d6aaa1c7980c
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 1%

---


# コードリファクタリングツールの統合エクスペリエンス {#unified-experience}

Cloud ServiceとしてAEMとの互換性が必要なコードリファクタリングタスクの一部を自動化するツールを開発しました。 様々なコードリファクタリングツールのインストールと設定に伴う複雑さを軽減するため、コードおよびリポジトリで動作するツールを統合するプラグインを開発しました。

## メリット {#benefits}

Unified Experienceプラグインには次のような利点があります。

* ソースコードで機能するツールを1つのアプリケーションに統合し、プラグインとして公開して、ユーザーに対して一貫性のあるユーザーエクスペリエンス `node.js``aio-cli ` を提供します。

* 1つのコマンドですべてのツールを実行できると同時に、必要に応じて特定のツールを実行できる柔軟性も提供します。

* エクスペリエンスの一貫性を維持しながら、新しいツールの追加を簡略化する拡張機能を提供します。

## プラグインについて {#understanding-plugin}

プラグインは、次の2つの主要な部分で構成されています。 `aio-cli-plugin-aem-cloud-service-migration`

* **ユーザーインターフェイス**

   * `aio-cli` 1つ以上のコードリファクタリングツールを実行するコマンド（ツールを連結して順番に実行する）。
   * `config.yaml` は、必要な入力パラメーターを取り込みます。

* **基礎となるコードリファクタリングツールスイート**

   コードリファクタリングツールは、次の方法で機能を実行します。

   * お客様のコードの各セクションをスキャンし、（コードの実装に基づくベストプラクティスに基づく）コードを操作して出力を生成し、検証して導入できます。

   * 実行中に実行された操作を記録するサマリレポートを生成する。

## 入手方法 {#availability}

詳しくは、 [Gitリソースを参照してください。aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) ：使用方法と、GitHubでオープンソースのこのプラグインコードに貢献する方法を確認します。

>[!NOTE]
>現在、プラグインに統合されているのは、Dispatcher Converterのみです。
