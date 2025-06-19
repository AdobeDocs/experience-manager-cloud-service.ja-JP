---
title: リファクタリングツールの概要
description: AEM リファクタリングツールの基本を学ぶ
exl-id: b8137e01-87e8-4298-b0cc-b376330cb730
source-git-commit: 879f4f3476ee369554188d6e3b7973d32454ed4b
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 1%

---

<!-- Alexandru: temporarily commeting this out, since it breaks validation

>[!CONTEXTUALHELP]
>id="aemcloud_rs_overview"
>title="Overview"
>abstract="Refactoring Tools is a solution developed by Adobe to help refactor existing AEM projects for compatibility with AEM as a Cloud Service. The tools are executed via Cloud Acceleration Manager (CAM) and automate key modernization tasks."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=ja" text="Guidelines and Best Practices"

-->

# リファクタリングツールの概要 {#refactoring-tools-overview}

**リファクタリングツール** は、**AEM as a Cloud Service（AEMaaCS）** と互換性を持たせるために、既存のAEM プロジェクトを更新するプロセスを合理化します。 これらのツールは、一般的なリファクタリングおよび最新化タスクを自動化し、**Cloud Acceleration Manager（CAM）** と統合して、シームレスなエクスペリエンスを実現します。

以前は CLI ユーティリティとしてのみ利用可能だったリファクタリングツールは、自動化された検査、設定の生成、ジョブの実行などの機能を備えた統合インターフェイスを提供するようになり、手動のオーバーヘッドを削減し、可視性を向上させます。

## 検査ワークフロー {#inspection-workflow}

**検査ワークフロー** を使用すると、リファクタリングツールを実行するための準備プロセスを簡単に行うことができます。

### 主な機能：

* **自動トリガー** - プロジェクトをアップロードすると、インスペクションが自動的に開始されます。
* **設定の生成** - ツールは、アップロードされたソースコードを検査し、必要な設定を生成します。
* **ペイロード送信** – これらの設定は、選択したツールに直接渡されて実行されます。

## 使用可能なリファクタリングツール

### リポジトリモダナイザー {#repo-modernizer}

**Repository Modernizer** は、AEM プロジェクトのリポジトリレイアウトとコンテンツを再構築して、AEMaaCS の標準とベストプラクティスに合わせます。 従来のリポジトリ最新化ツールに代わり、自動化と精度が向上しています。

### コード変換サービス {#code-transformer}

**コードトランスフォーマー** は、インテリジェントパターン認識と AI 駆動の分析を使用して、AEMaaCS と互換性のないコードセグメントを検出および更新します。 このツールにより、移行作業が簡素化され、手動でのコード変更が減ります。

## リファクタリングのワークフローフェーズ {#phases-in-refactoring-tools}

リファクタリングツールは、構造化された 2 段階のプロセスに従います。

### フェーズ 1:Source コードのアップロード

* CAM インターフェイスを使用して、ソースコード（ZIP 形式）をアップロードします。
* アップロードが完了すると、**検査ワークフロー** が自動的にトリガーされ、プロジェクトの分析とツールの実行準備が行われます。

>[!NOTE]
>検査プロセス中は、別のプロジェクトのアップロードは許可されません。

### フェーズ 2：リファクタリングジョブのトリガー

検査が正常に完了したら、1 つ以上のリファクタリングツールを実行できます。

* **Run Repository Modernizer** - リポジトリの最新化を実行します。
* **コード変換を実行** – 検査出力に基づいてコード変換を実行します。
* **すべてのツールを同時に実行** – 使用可能なすべてのツールを 1 回の操作で実行します。

>[!NOTE]
>リファクタリングジョブは、ソースコードが正常にアップロードおよび検査された後にのみ開始できます。

>[!NOTE]
>ユーザーは複数のリファクタリングジョブを並行してトリガーできますが、各ジョブは個別に実行されます。
