---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: c8a798e1f1b7234f91682b6e5ef7072e024df022
workflow-type: ht
source-wordcount: '693'
ht-degree: 100%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 18751 {#18751}

2024年12月11日（PT）に公開された、メンテナンスリリース 18751 の継続的な改善点を以下にまとめます。前回のメンテナンスリリースは、リリース 18598 でした。

2025.1.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-18751}

* SKYOPS-88509：AEM SDK の Java 21 サポート。

### 修正された問題 {#fixed-issues-18751}

* ASSETS-42802：MFE の「戻る」ボタンが機能しないことがあり、追加のダイアログが表示されます。
* ASSETS-44148：AEM の NODE_MOVED イベントが NPE を引き起こす場合がある問題を修正しました。
* ASSETS-44418：スカイラインで正しい環境が設定されていない問題を修正しました。
* ASSETS-44821：アップロードイベント用にフォーム URL でエンコードされたデータを含める、更新イベントフィルターを修正しました。
* CNTBF-298：UUID の競合によりコンテンツのコピーが失敗する問題を修正しました。
* CNTBF-331：[content-copy-bundle] リリース 2.0.14。
* FORMS-16572：Java 21 SDK ビルドのワークフローテストの失敗を削除。
* GRANITE-36205：QS での内部 Oak リリースの自動アップデート。
* GRANITE-53704：リポジトリサービスの Sling 検出を再評価。
* GRANITE-54300：Oak を最新のパブリックリリース（1.70.0）にアップデート。
* GRANITE-54416：FileVault をバージョン 3.8.2 にアップデート。
* GRANITE-54462：「systemready」の hc.tags を使用するように SubscriberAgents を設定。
* GRANITE-54542：commons-io 依存関係を 2.17.0 にアップデート。
* GRANITE-54658：QS の fullGC に delayFactor と batch-size OSGi 設定を追加。
* GRANITE-54696：Jackrabbit API の読み込み範囲を拡大。
* GRANITE-54803：imsauth がアクティブな場合は、AEM で ClusterAtExchange を無効にします。
* GRANITE-55095：Oak を最新のパブリックリリース（1.72.0）にアップデート。
* GUIDES-20006：完了としてマークされたドキュメントの状態は、新しいバージョンを保存する前にドラフトに戻り、どのドキュメントバージョンでも完了状態が保持されなくなります。
* GUIDES-21840：ネイティブ PDF 出力では、目次から章のタイトルが欠落しており、間違った階層になります。
* GUIDES-19558：ベースラインに多数のトピックまたはマップがある場合、クラウド設定でベースラインを編集して保存すると、1 分後にタイムアウトになります。
* GUIDES-19733：ベースラインを使用したマップの変換が遅くなり、最終的には関連するすべてのトピックとマップファイルのリストを読み込むことができなくなります。
* SITES-26798：自動昇格のローンチでは、昇格ステータス（昇格日）が更新されません。
* SITES-27137：MSM コアから Sling Commons Metrics の依存関係を削除。
* SKYOPS-75446：AEM が 404 を返す場合や、コンテンツが欠落しているページを返す場合がある問題を修正しました。
* SKYOPS-76366：AEM リリース 15977 以降、Jetty Threadpool Metrics がありません。
* SKYOPS-82371： java.io.IOException: classFile.delete() が失敗しました。
* SKYOPS-83369：変換ジョブの実行でバンドルが生成されない場合、AEM デプロイメントは起動に失敗します。
* SKYOPS-83910：SKYOPS-82371 で見つかった同時実行の問題を修正しました。
* SKYOPS-84821：Sling メインサーブレットの sling.includes.checkcontenttype 設定を true に設定します。
* SKYOPS-85798：変換ジョブで空のインデックス定義が生成される問題を修正しました。
* SKYOPS-86251：AEM アナライザーコア 1.5.6 にアップグレードし、変換ジョブで product-package-import アナライザーを有効にします。
* SKYOPS-86710：Java 21 SDK ビルドの縮小テストの失敗を削除します。
* SKYOPS-86745：Sling ResourceResolver 1.12.2 にアップデート。
* SKYOPS-89616：Adobe Developer Console でテクニカルアカウントを作成できなかった問題を修正しました。
* SKYOPS-89691：ASM 警告に使用される不正なアーティファクト ID を修正しました。
* SKYOPS-89699：Groovy コンソールの「orbinson」フレーバーに埋め込まれている、古い Groovy バージョンに関する警告が欠落しています。
* SKYOPS-88664：ダウンロードされたマップファイルの行が 1024 の制限を超えている場合に、ログに記録して保護します。
* SKYOPS-89734：リリース Dispatcher イメージ 2.0.235。

Experience Manager Guides の新機能や機能強化および修正された問題について詳しくは、[Experience Manager Guides リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)を参照してください。

### 既知の問題 {#known-issues-18751}

なし。

### 廃止された機能と API {#deprecated-18751}

AEM as a Cloud Service で廃止および削除された機能と API について詳しくは、[廃止および削除された機能と API](/help/release-notes/deprecated-removed-features.md) ドキュメントを参照してください。

### セキュリティ修正 {#security-18751}

AEM as a Cloud Service では、プラットフォームのセキュリティとパフォーマンスの最適化に取り組んでいます。このメンテナンスリリースでは、特定された 3 つの脆弱性に対処し、堅牢なシステム保護に対する取り組みを強化しています。

### 組み込みテクノロジー {#embedded-tech-18751}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.72.0 | [Oak API 1.72.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.72.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | 2.27.0 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
