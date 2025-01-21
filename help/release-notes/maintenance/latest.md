---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: a091dd6b1b69d77f9eeb50065e8946af0133f4f9
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 42%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 19149 {#19149}

2025年1月21日（PT）に公開された、メンテナンスリリース 19149 の継続的な改善点を以下にまとめます。前回のメンテナンスリリースは、リリース 18751 でした。

2025.1.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-19149}

* ASSETS-45286：ダウンロードアーカイブ非同期ジョブの詳細な進行状況を表示します。
* ASSETS-46296：アセットセレクターでのDynamic Media テンプレートのサポート。
* ASSETS-44796:DAM 非同期アセットジョブに対してAssets イベントを実行します。

### 修正された問題 {#fixed-issues-19149}

* GRANITE-55074：エラー応答に CORS 応答ヘッダーが設定されていることを確認します。
* ASSETS-43755：アセットの一括関連付けの拡張性が向上しました。
* ASSETS-45399：アセットのライブコピーを作成した後、Assets コンソールにリダイレクトされる。
* ASSETS-45462：カスタムフォルダーサムネールでブラウザーキャッシュに問題が発生する。
* ASSETS-46398:DM テンプレートのダウンロードおよび再処理アクションを非表示にする。
* ASSETS-44484:Connected Assets設定を再保存する際の問題。
* ASSETS-44122：非同期コピーアセットジョブで、現在のフォルダーにコピーする際に、コピー先フォルダーの名前が変更されない。
* ASSETS-44463：メタデータの書き出しが成功しても「CSV をダウンロード」ボタンが表示されない。
* ASSETS-45134：宛先のタイトルを含むジョブの移動は、すべてのフォルダータイトルを上書きします。
* ASSETS-45137:Assets ビューを通じたバルクアップロードと競合します。
* ASSETS-45758:Asset Relations は、リレーションを追加した後、無限のビジー/読み込みアニメーションを取得します。
* ASSETS-44148:AEMの NODE_MOVED イベントが、ログに誤った NPE を引き起こす可能性があります。
* ASSETS-28607：カスタムビデオサムネールを設定する際に JS エラーが発生する。
* GRANITE-55781:Adobe Developer ConsoleとAEMの間のグループ同期を改善します。 詳しくは、[ ユーザーグループと製品プロファイルの同期の変更 ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/changes-in-user-group-and-product-profile-synchronization) を参照してください。
* GRANITE-55754:SDK スタートアップスクリプトで Java 21 がサポートされていることを確認します。
* GRANITE-54248：大きなアセットフォルダー内のすべての項目をスクロールできない。
* SCRNS-4597：検索結果リスト ビューの改善。


### 既知の問題 {#known-issues-19149}

なし。

### 非推奨（廃止予定）機能と API {#deprecated-19149}

Adobe Admin Consoleを使用して権限を管理する場合、次のグループはAEMに同期されないので、使用しないでください。
* _GROUP_NAME_SUFFIX で終わるAEM グループ。
* 他の環境、プログラム、製品からの製品プロファイル。

詳しくは、[ ユーザーグループと製品プロファイルの同期の変更 ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/changes-in-user-group-and-product-profile-synchronization) を参照してください。


AEM as a Cloud Service で廃止および削除された機能と API について詳しくは、[廃止および削除された機能と API](/help/release-notes/deprecated-removed-features.md) ドキュメントを参照してください。

### セキュリティ修正 {#security-19149}

AEM as a Cloud Service では、プラットフォームのセキュリティとパフォーマンスの最適化に取り組んでいます。このメンテナンスリリースでは、特定された 4 つの脆弱性に対処し、堅牢なシステム保護に対する取り組みを強化しています。

### 組み込みテクノロジー {#embedded-tech-19149}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.72.0 | [Oak API 1.72.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.72.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | 2.27.0 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
