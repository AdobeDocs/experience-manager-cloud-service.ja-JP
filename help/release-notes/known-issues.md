---
title: 既知の問題
description: クラウドサービスとしてのAdobe Experience Managerの既知の問題に関するリリースノート
translation-type: tm+mt
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1

---


# 既知の問題 {#known-issues}

この記事では、クラウドサービスとしてのAdobe Experience Managerの既知の問題を示します。 リストが改訂され、Experience Managerの継続的なリリースごとに更新されます。

[既知の問題の詳細については](https://helpx.adobe.com/support/experience-manager.html) 、サポートにお問い合わせください。

<!-- 
## Platform {#platform}

## Sites {#sites}
-->

## アセット {#assets}

<!-- Jira label: assets-cloud-known-issues -->

既知の問題は次のとおりです。

* **Metadata Schema**:アセットレーティングウィジェットは、JSPコンパイルエラーの原因となる場合があります。 回避策として、アセットの評価コンポーネントをメタデータスキーマから削除します。 <!-- CQ-4282865 -->

アセット機能には、次のような制限があります。

* AEM Assetsをクラウドサービスとして使用すると、AEM 6.5サイトをAMSにデプロイする場合に、接続されたアセット機能が機能します。

### 今後のアセット機能 {#upcoming-assets-capabilities}

Adobe Experience Manager Assetsの機能のうち、基盤機能に依存するもののいくつかは、クラウドサービスのデプロイメントアーキテクチャとしてExperience Managerではまだ利用できないもので、後で有効にする予定です。

* Brand portalへの公開は、現時点では有効になっていません。 アセット配布の使用例に対し [ては、Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) （アセット共有コモンズ）の実装を拡張およびデプロイできます。
* Adobe I/OのAIサービスを利用する強化されたスマートタグ機能は、現時点では使用できません。
* Commerce Integration Framework APIへの依存が原因で、この段階で機能が有効になっていません。
   * フォトシュートワークフローモデル
   * アセットプロパティユーザーインターフェイスの「製品情報」タブに値が入力されない。
* InDesign serverの統合に依存しているため、この段階で機能が有効になりません。
   * アセットテンプレートとアセットカタログを参照してください。
   * InDesignファイルの複数ページのプレビュー。

>[!MORELIKETHIS]
>
>* [AEMの主な変更点](aem-cloud-changes.md)
>* [廃止および削除された機能](deprecated-removed-features.md)
>* [リリースノート](home.md)

