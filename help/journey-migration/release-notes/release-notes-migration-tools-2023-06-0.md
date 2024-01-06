---
title: AEM as a Cloud Service リリース 2023.06.0 の移行ツールのリリースノート
description: AEM as a Cloud Service リリース 2023.06.0 の移行ツールのリリースノート
feature: Release Information
exl-id: 021b7472-d1e4-4ef6-a040-c612fed8d3c3
source-git-commit: a77e5dc4273736b969e9a4a62fcac75664495ee6
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 100%

---

# AEM as a Cloud Service リリース 2023.06.0 の移行ツールのリリースノート {#release-notes}

このページでは、AEM as a Cloud Service 2023.06.0 の移行ツールのリリースノートの概要を説明しています。

## コンテンツ転送ツール {#ctt-release}

### リリース日 {#release-date-ctt}

コンテンツ転送ツール v2.0.20 のリリース日は 2023年6月8日（PT）です。

### 新機能 {#what-is-new-ctt}

* 新しい移行ツール - コンテンツ変換サービス（CT）が、このリリースでコンテンツ転送ツール（CTT）と統合されました。コンテンツ変換サービスは、現在の AEM 実装（オンプレミスまたはManaged Services）から AEM as a Cloud Service にコンテンツを移行する前に[ベストプラクティスアナライザー（BPA）](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=ja)によって報告されたコンテンツ関連の問題を自動的に検出し、修正できます。
コンテンツ変換サービスのメリットは次のとおりです。
   * フェイルセーフ：問題を修正しようとリポジトリを変更するたびに、コンテンツ変換サービスによってパッケージが作成されます。必要に応じて、パッケージをインストールして前の状態に戻すことができます。
   * 使いやすさ：コンテンツ変換サービスは、コンテンツ転送ツールに統合され、直感的なシンプルなユーザーインターフェイスを備えています。
   * 時間を節約：1 つのパターンカテゴリに分類されるコンテンツの問題が多数ある場合は、コンテンツ変換サービスを使用すると、数回のクリックですべての問題を解決して、大幅な時間の節約と移行の複雑さの軽減を実現できます。
