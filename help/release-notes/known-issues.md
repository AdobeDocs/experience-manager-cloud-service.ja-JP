---
title: 既知の問題
description: リリースノート（Adobe Experience Manager as a Cloud Service の既知の問題）
translation-type: ht
source-git-commit: 165dc4af656ce1bc431d2f921775ebda4cf4de9f
workflow-type: ht
source-wordcount: '186'
ht-degree: 100%

---


# 既知の問題 {#known-issues}

ここでは、Adobe Experience Manager as a Cloud Service ソリューションの既知の問題について説明します。Adobe Experience Manager のリリースのたびに、このリストは改訂され更新されます。

既知の問題について詳しくは、[サポートまでお問い合わせ](https://helpx.adobe.com/jp/support/experience-manager.html)ください。

<!-- 
## Platform {#platform}

## Sites {#sites}
-->

## Assets {#assets}

<!-- Jira label: assets-cloud-known-issues -->

既知の問題の一部は次のとおりです。

* **メタデータスキーマ**：アセット評価ウィジェットが JSP コンパイルエラーを引き起こしていました。メタデータスキーマから削除されました。 <!-- CQ-4282865, CQ-4284633 -->

### 今後予定されている Assets の機能 {#upcoming-assets-capabilities}

Adobe Experience Manager Assets の機能のうち、基盤機能をベースにしているものは、Adobe Experience Manager as a Cloud Service のデプロイメントアーキテクチャではまだ利用できず、今後有効になる予定です。

* コマース統合フレームワーク API との依存関係により、現段階で有効になっていない機能は次のとおりです。
   * 写真撮影ワークフローモデル
   * アセットのプロパティユーザーインターフェイスの「製品情報」タブに値が入力されません。
* InDesign Server との依存関係により、現段階で有効になっていない機能は次のとおりです。
   * アセットテンプレートとアセットカタログ
   * Adobe InDesign ファイルの複数ページにわたるプレビュー

>[!MORELIKETHIS]
>
>* [Adobe Experience Manager（AEM）as a Cloud Service の主な変更点](aem-cloud-changes.md)
>* [廃止される機能および削除された機能](deprecated-removed-features.md)
>* [リリースノート](home.md)

