---
title: AEM Repo ツール
description: AEM Repo ツールは、FTP に相当するコマンドラインを使用してローカルファイルシステムと AEM サーバーの間で JCR コンテンツを転送するためのシンプルなソリューションです。
translation-type: tm+mt
source-git-commit: c40d668cb6dcf5c3e2d09504b547457306a99c85
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 51%

---


# AEM Repo ツール {#aem-repo-tool}

AEM Repo ツールは、FTP に相当するコマンドラインを使用してローカルファイルシステムと AEM サーバーの間で JCR コンテンツを転送するためのシンプルなソリューションです。AEM Repo Toolは[Jackrabbit FileVault Mavenプラグイン](https://jackrabbit.apache.org/filevault-package-maven-plugin)に似ていますが、高速で依存性が最小限で、単純なbashスクリプトです。

このツールを使用すると、開発者向けのファイルの転送が簡単になり、EclipseとIntelliJに統合して開発をさらに効率化できます。

## 概要 {#overview}

ファイルシステム上の`jcr_root` FileVault構造内の特定のパスに対して、AEM Repo Toolはサブツリー全体に対して単一のフィルタを持つパッケージを作成し（FTP `put`と同様）サーバにプッシュし、サーバから取り込むか（ `status`と`diff`）の違いを比較します。`get`

このツールは、複数のフィルタパスまたはFileVaultの`filter.xml`をサポートしていません。

>[!CAUTION]
>
>AEM Repo ツールは、指定したファイル全体またはディレクトリを常に上書きすることに注意してください。

## ダウンロードとドキュメント  {#download-and-documentation}

[AEM Repo Toolは、GitHub上で、このリンク](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo)と共に、詳細なインストールおよび使用方法に関する説明と共に利用できます。

AEM Repo ツールのソースをダウンロードする場合は、GitHub プロジェクト（次のリンク）を参照してください。

GitHub のコード

このページのコードは GitHub にあります

* [GitHubでツールプロジェクトを開く](https://github.com/Adobe-Marketing-Cloud/tools)
* プロジェクトを [ZIP ファイル](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)としてダウンロードします
