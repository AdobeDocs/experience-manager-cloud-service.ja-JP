---
title: AEM Repo ツール
description: AEM Repo ツールは、FTP に相当するコマンドラインを使用してローカルファイルシステムと AEM サーバーの間で JCR コンテンツを転送するためのシンプルなソリューションです。
exl-id: fb887ba3-e40b-4ab1-b142-0748c6d9f18e
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 100%

---

# AEM Repo ツール {#aem-repo-tool}

AEM Repo ツールは、FTP に相当するコマンドラインを使用してローカルファイルシステムと AEM サーバーの間で JCR コンテンツを転送するためのシンプルなソリューションです。AEM Repo ツールは、[Jackrabbit FileVault Maven プラグイン](https://jackrabbit.apache.org/filevault-package-maven-plugin)に似ていますが、より高速で依存関係が最小限であり、シンプルな bash スクリプトです。

このツールは、デベロッパーによるファイルの転送をシンプルにします。また、Eclipse および IntelliJ と統合して開発をより効率的にできます。

## 概要 {#overview}

ファイルシステム上の `jcr_root` FileVault 構造内の特定のパスの場合、AEM Repo ツールは、サブツリー全体に対する単一のフィルターを含むパッケージを作成し、それをサーバーにプッシュして（FTP の `put` と同じ）、サーバーから取得（`get`）または違いを比較（`status` および `diff`）します。

このツールは、複数のフィルターパスや FileVault の `filter.xml` をサポートしません。

>[!CAUTION]
>
>AEM Repo ツールは、指定したファイル全体またはディレクトリを常に上書きすることに注意してください。

## ダウンロードとドキュメント {#download-and-documentation}

[AEM Repo ツールは、このリンクの GitHub で利用できます](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo)。詳細なインストールおよび使用手順も用意されています。

AEM Repo ツールのソースをダウンロードする場合は、GitHub プロジェクト（次のリンク）を参照してください。

GitHub のコード

このページのコードは GitHub にあります

* [GitHub でツールのプロジェクトを開きます](https://github.com/Adobe-Marketing-Cloud/tools)
* プロジェクトを [ZIP ファイル](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)としてダウンロードします
