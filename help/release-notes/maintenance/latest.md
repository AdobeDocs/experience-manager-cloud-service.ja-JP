---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: a3c414f9b5e575856a942e02661e8c70a7083495
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 89%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 19149 {#19149}

2025年1月21日（PT）に公開された、メンテナンスリリース 19149 の継続的な改善点を以下にまとめます。 前回のメンテナンスリリースは、リリース 18751 でした。

2025.1.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。 詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-19149}

* ASSETS-45286：ダウンロードアーカイブ非同期ジョブの詳細な進行状況を表示。
* ASSETS-46296：アセットセレクターでの Dynamic Media テンプレートのサポート。
* ASSETS-44796：DAM 非同期アセットジョブに対して Assets イベントを実行。

### 修正された問題 {#fixed-issues-19149}

* GRANITE-55074：エラー応答に CORS 応答ヘッダーが設定されていることを確認。
* ASSETS-43755：一括アセット関連のスケーラビリティの改善。
* ASSETS-45399：アセットのライブコピーを作成した後、Assets コンソールにリダイレクトされる。
* ASSETS-45462：カスタムフォルダーのサムネールに関するブラウザーのキャッシュの問題。
* ASSETS-46398：DM テンプレートのダウンロードおよび再処理アクションが非表示になる。
* ASSETS-44484：接続されたアセット設定の再保存に関する問題。
* ASSETS-44122：非同期コピーアセットジョブで、現在のフォルダーにコピーする際に、宛先フォルダーの名前が変更されない。
* ASSETS-44463：メタデータの書き出しが成功しても「CSV をダウンロード」ボタンが表示されない。
* ASSETS-45134：宛先タイトル付きの移動ジョブで、すべてのフォルダータイトルが上書きされる。
* ASSETS-45137：アセットビューを通じた一括アップロードで競合が発生する。
* ASSETS-45758：アセットの関連付けで関係を追加した後、ビジー／読み込みアニメーションが無限に続く。
* ASSETS-44148：AEM の NODE_MOVED イベントにより、ログに偽の NPE が発生する場合がある。
* ASSETS-28607：カスタムビデオサムネールを設定する際に JS エラーが発生する。
* GRANITE-55781：Adobe Developer Console と AEM 間のグループ同期を改善。 詳しくは、[ユーザーグループと製品プロファイルの同期の変更](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/security/changes-in-user-group-and-product-profile-synchronization)を参照してください。
* GRANITE-55754：SDK 起動スクリプトが Java 21 をサポートしていることを確認。
* GRANITE-54248：大きなアセットフォルダー内のすべての項目をスクロールできない。
* SCRNS-4597：検索結果リスト表示の改善。


### 既知の問題 {#known-issues-19149}

なし。

### 廃止された機能と API {#deprecated-19149}

AEM as a Cloud Service で廃止および削除された機能と API について詳しくは、[廃止および削除された機能と API](/help/release-notes/deprecated-removed-features.md) ドキュメントを参照してください。

#### ユーザーグループと製品プロファイルの同期の変更

権限管理に Adobe Admin Console を使用する際、次のグループは AEM に同期されなくなるので、使用しないでください。
* _GROUP_NAME_SUFFIX で終わる AEM グループ。
* 他の環境、プログラム、製品からの製品プロファイル。

詳しくは、[ユーザーグループと製品プロファイルの同期の変更](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/security/changes-in-user-group-and-product-profile-synchronization)を参照してください。

#### SPA Editor の廃止 {#deprecate-spa-editor}

[SPA エディター ](/help/implementing/developing/hybrid/introduction.md) は、リリース 2025.1.0 以降の新しいプロジェクトでは廃止されました。SPA エディターは、既存のプロジェクトでは引き続きサポートされますが、新しいプロジェクトには使用しないでください。

AEMでヘッドレスコンテンツを管理するために推奨されるエディターは次のとおりです。

* ビジュアル編集用の [ ユニバーサルエディター ](/help/edge/wysiwyg-authoring/authoring.md)。
* フォームベースの編集用の [ コンテンツフラグメントエディター ](/help/assets/content-fragments/content-fragments-managing.md)。

### セキュリティ修正 {#security-19149}

AEM as a Cloud Service では、プラットフォームのセキュリティとパフォーマンスの最適化に取り組んでいます。 このメンテナンスリリースでは、特定された 4 つの脆弱性に対処し、堅牢なシステム保護に対する取り組みを強化しています。

### 組み込みテクノロジー {#embedded-tech-19149}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.72.0 | [Oak API 1.72.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.72.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | 2.27.0 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
