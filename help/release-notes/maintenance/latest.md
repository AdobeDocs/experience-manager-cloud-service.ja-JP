---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: c8a798e1f1b7234f91682b6e5ef7072e024df022
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 36%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 18751 {#18751}

2024年12月11日（PT）に公開された、メンテナンスリリース 18751 の継続的な改善点を以下にまとめます。前回のメンテナンスリリースは、リリース 18598 でした。

2025.1.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-18751}

* SKYOPS-88509:AEM SDK の Java 21 サポート。

### 修正された問題 {#fixed-issues-18751}

* ASSETS-42802:MFE の「戻る」ボタンが常に機能するとは限らず、追加のダイアログが表示されます。
* ASSETS-44148:AEMの修正された NODE_MOVED イベントが NPE を引き起こす可能性があります。
* ASSETS-44418：修正スカイラインで正しい環境が設定されない。
* ASSETS-44821：アップロードイベント用にフォーム URL でエンコードされたデータを含める更新イベントフィルターを修正しました。
* CNTBF-298:UUID の競合により、フィックス・コンテンツのコピーが失敗する。
* CNTBF-331: [content-copy-bundle] リリース 2.0.14。
* FORMS-16572:Java 21 SDK ビルドのワークフローテストエラーを削除。
* GRANITE-36205:QS の内部 Oak リリースの自動アップデート。
* GRANITE-53704：リポジトリサービスの Sling 検出を再評価します。
* GRANITE-54300：Oak を最新のパブリックリリース（1.70.0）にアップデート。
* GRANITE-54416：FileVault をバージョン 3.8.2 に更新します。
* GRANITE-54462:「systemready」の hc.tags を使用するように SubscriberAgents を設定する。
* GRANITE-54542: commons-io の依存関係を 2.17.0 に更新します。
* GRANITE-54658:QS の fullGC に、delayFactor および batch-size OSGi 設定を追加。
* GRANITE-54696:Jackrabbit API の読み込み範囲を拡大しました。
* GRANITE-54803:imsauth がアクティブな場合は、AEMで ClusterAtExchange を無効にします。
* GRANITE-55095：Oak を最新のパブリックリリース（1.72.0）にアップデート。
* GUIDES-20006：完了とマークされたドキュメントの状態が新しいバージョンを保存する前にドラフトに戻るので、完了の状態がどのドキュメントバージョンにも保持されません。
* GUIDES-21840：ネイティブPDF出力で、チャプタータイトルが目次から欠落し、誤った階層が発生します。
* GUIDES-19558：ベースラインに多数のトピックまたはマップがある場合、1 分後にクラウド設定のタイムアウトでベースラインを編集して保存します。
* GUIDES-19733: ベースラインを使用したマップの変換が遅くなり、最終的に関連するすべてのトピックとマップファイルのリストの読み込みに失敗します。
* SITES-26798：自動昇格のローンチで、昇格ステータス（昇格日）が更新されない。
* SITES-27137:MSM コアから Sling Commons の指標の依存関係を削除します。
* SKYOPS-75446：固定AEMは、コンテンツが欠落している 404 ページまたはページを返す場合があります。
* SKYOPS-76366:AEM リリース 15977 以降、Jetty スレッドプール指標がありません。
* SKYOPS-82371: java.io.IOException: classFile.delete （）が失敗しました。
* SKYOPS-83369：変換ジョブの実行でバンドルが生成されない場合、AEM デプロイメントの開始に失敗する。
* SKYOPS-83910:SKYOPS-82371 で見つかった同時実行の問題を修正しました。
* SKYOPS-84821:Sling メインサーブレットの sling.includes.checkcontenttype 設定を true に設定する。
* SKYOPS-85798：固定変換ジョブにより、空のインデックス定義が生成されます。
* SKYOPS-86251: AEM Analyzer core 1.5.6 にアップグレードし、変換ジョブで product-package-import analyzer を有効にします。
* SKYOPS-86710:Java 21 sdk ビルドの縮小テストエラーを削除します。
* SKYOPS-86745:Sling ResourceResolver 1.12.2 を更新しました。
* SKYOPS-89616:Adobe Developer Consoleでテクニカルアカウントを作成できなかった問題を修正しました。
* SKYOPS-89691:ASM 警告に使用される不正なアーティファクト ID を修正しました。
* SKYOPS-89699:Groovy コンソールの「orbinson」フレーバーに埋め込まれている、古い Groovy バージョンに関する警告が欠落しています。
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
