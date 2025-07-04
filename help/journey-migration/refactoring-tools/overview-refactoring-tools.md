---
title: リファクタリングツールの概要
description: AEM リファクタリングツールの基本を学ぶ
exl-id: b8137e01-87e8-4298-b0cc-b376330cb730
source-git-commit: 879f4f3476ee369554188d6e3b7973d32454ed4b
workflow-type: ht
source-wordcount: '338'
ht-degree: 100%

---

<!-- Alexandru: temporarily commeting this out, since it breaks validation

>[!CONTEXTUALHELP]
>id="aemcloud_rs_overview"
>title="Overview"
>abstract="Refactoring Tools is a solution developed by Adobe to help refactor existing AEM projects for compatibility with AEM as a Cloud Service. The tools are executed via Cloud Acceleration Manager (CAM) and automate key modernization tasks."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=ja" text="Guidelines and Best Practices"

-->

# リファクタリングツールの概要 {#refactoring-tools-overview}

**リファクタリングツール**&#x200B;は、**AEM as a Cloud Service（AEMaaCS）**&#x200B;と互換性を持たせるために、既存の AEM プロジェクトを更新するプロセスを合理化します。これらのツールは、一般的なリファクタリングおよび最新化タスクを自動化し、**Cloud Acceleration Manager（CAM）**&#x200B;と統合して、シームレスなエクスペリエンスを実現します。

以前は CLI ユーティリティとしてのみ利用可能だったリファクタリングツールは、自動化された検査、設定の生成、ジョブの実行などの機能を備えた統合インターフェイスを提供するようになり、手動によるオーバーヘッドを削減し、可視性を向上させます。

## 検査ワークフロー {#inspection-workflow}

**検査ワークフロー**&#x200B;を使用すると、リファクタリングツールを実行するための準備プロセスを簡単に行うことができます。

### 主な機能：

* **自動トリガー** - プロジェクトをアップロードすると、検査が自動的に開始されます。
* **設定の生成** - このツールは、アップロードされたソースコードを検査し、必要な設定を生成します。
* **ペイロード送信** – これらの設定は、選択したツールに直接渡されて実行されます。

## 利用可能なリファクタリングツール

### Repository Modernizer {#repo-modernizer}

**Repository Modernizer** は、AEM プロジェクトのリポジトリレイアウトとコンテンツを再構築して、AEMaaCS の標準とベストプラクティスに準拠させます。従来のリポジトリ最新化ツールを、強化された自動化と精度で置き換えます。

### コード変換サービス {#code-transformer}

**コード変換**&#x200B;は、インテリジェントパターン認識と AI 駆動の分析を使用して、AEMaaCS と互換性のないコードセグメントを検出および更新します。このツールにより、移行作業が簡素化され、手動によるコード変更が減ります。

## リファクタリングのワークフローフェーズ {#phases-in-refactoring-tools}

リファクタリングツールは、構造化された 2 段階のプロセスに従います。

### フェーズ 1：ソースコードのアップロード

* CAM インターフェイスを使用して、ソースコード（ZIP 形式）をアップロードします。
* アップロードが完了すると、**検査ワークフロー**&#x200B;が自動的にトリガーされ、プロジェクトの分析とツールの実行準備が行われます。

>[!NOTE]
>検査プロセス中は、別のプロジェクトをアップロードすることはできません。

### フェーズ 2：リファクタリングジョブのトリガー

検査が正常に完了したら、1 つ以上のリファクタリングツールを実行できます。

* **Repository Modernizer の実行** - リポジトリの最新化を実行します。
* **コード変換の実行** – 検査出力に基づいてコード変換を実行します。
* **すべてのツールを同時に実行** – 使用可能なすべてのツールを 1 回の操作で実行します。

>[!NOTE]
>リファクタリングジョブは、ソースコードが正常にアップロードおよび検査された後にのみ開始できます。

>[!NOTE]
>ユーザーは複数のリファクタリングジョブを並行してトリガーできますが、各ジョブは個別に実行されます。
