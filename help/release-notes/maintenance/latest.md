---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: aa9629c3e48ca0bf4654351462a94777af9ed651
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 22%

---

# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 14029 {#release-14029}

2023 年 10 月 25 日に公開されたメンテナンスリリース14029の継続的な改善点を以下にまとめます。 このメンテナンスリリースは、以前のメンテナンスリリース 13804 からのアップデートです。

2023.11.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=ja)を参照してください。

### 機能強化 {#enhancements-14029}

* ASSETS-28551:My Link Shares UI のスケーラビリティが向上
* ASSETS-28566: dam:metadataForm Lucene インデックスの追加
* ASSETS-29281:RAPI を更新して v2 ダウンロードイベントを送信する

### 修正された問題 {#fixed-issues-14029}

* ASSETS-25199：画像コアコンポーネントに正しいスマート切り抜きが表示されない
* ASSETS-26142：検出リクエストが失敗したか中断された場合、unified-shell.js customEnvLabel は設定または再試行されません。
* ASSETS-26416：検索フォームで「1 日前」と常に定義される相対日付の述語。
* ASSETS-27321：チームメンバーシップの変更時にグループキャッシュをクリアします
* ASSETS-27591：古い org.json への依存関係を修正しました。
* ASSETS-28439：グローバルブロックリストが設定されていなブロックリストに加えるい場合、スマートタグは NPE をします
* ASSETS-28612:「repository-api」の BlockedTagResolver 修正
* ASSETS-28634: Asset Stock のオムニサーチフィールドにAdobeデータが自動的に追加されない
* ASSETS-28727：処理プロファイル設定リストに、指定したカスタムの高さと幅の値が表示されません。
* ASSETS-29056：トランスコーディングレンディションAEM標準処理プロファイルを追加します。
* ASSETS-29105: RDE 機能モデルの SecurityProviderRegistration requiredServicePids に制限プロバイダーがありません
* ASSETS-29106：統合シェルが有効なAEMで、Adobe在庫の表示でエラーがスローされる
* ASSETS-29115：制限プロバイダーパスの設定プロパティを削除します
* ASSETS-29208：サービス CompleteUploadAssetServlet が登録される前に作成者ポッドに送信された要求によって発生する、アセットのアップロード時のエラー
* ASSETS-29297：チェックアウト済みフィルターオプションを使用して検索を保存を作成する際の問題
* ASSETS-29363：メタデータプロファイルが IPTC にデフォルト値を適用しない
* ASSETS-29404：リンク共有レポートがクエリ制限を超えました
* ASSETS-29431：古い機能フラグを削除します。
* ASSETS-29443: Granite シェルヘッダーモードが「選択」に変更されても、統合シェルヒーローが表示されたままになり、クリック可能になります。
* ASSETS-29476: scene7DAMService.getS7FileReference(asset) Api 呼び出しで期待された値が返されない。
* ASSETS-29515:「jcr:lastModifiedBy」を含むアセット/ノード：「workflow-process-service」がリスト表示で「外部ユーザー」として表示される
* ASSETS-29579：管理者以外のユーザーが画像セットを作成できない
* ASSETS-29631：安全な配信/検索に dam:roles を使用
* ASSETS-29689:dc:roles （および新しいプロパティ dam:roles）をAEM側からフィルタリングする必要があります。
* ASSETS-29738: NullPointerException が発生してアセットのアップロード制限が失敗する
* ASSETS-29779: BLOB ストレージにないので、小さいアセットを Webp に処理できません
* ASSETS-29892：アセット数が多いフォルダーで、メタデータの書き出しが失敗する
* ASSETS-29996:PROD インスタンス上でのみアセットを断続的にアップロードする際の修飾子としての「外部ユーザー」
* ASSETS-30167: adobe_dam:restrictions のHTMLが、アセットをアップロードした後に壊れる
* ASSETS-30276：リンク UI を共有：アセットの詳細から共有できません
* ASSETS-30434：アセット処理が完了したイベントがパイプラインに送信されませんでした
* ASSETS-30519:REDMetricsServletFilter に RAPI を追加
* CQ-4354413: QueryBuilder：角括弧で囲まれたクエリが誤って xpath に変換される
* CQ-4354834：インボックスタスクにコメントを追加できません
* CQ-4354836：プロジェクトコンソールからワークフローを開始またはタスクを作成できません
* CQ-4354867: ToggleCondition 参照は、InstanceActionServlet 内の存在しないフィールドを参照します。
* CQ-4354895: AEM Translation Kit: 10 月 12 日
* GRANITE-45560：エンベロープのイベンティングでの共通スキーマ表現
* GRANITE-47267: Apache Felix Http Jetty 4.2.18 への更新
* GRANITE-47599：アップグレード後13323コンテンツの読み込みが失敗する (JCRVLT-721)
* GRANITE-47873: Apache Felix Webconsole 4.9.6 への更新

### 既知の問題 {#known-issues-14029}

* CQ-4354836：プロジェクトコンソールからワークフローを開始またはタスクを作成できません。
* CQ-4354834 ：ユーザーがインボックスタスクにコメントを追加できません。

### 組み込みテクノロジー {#embedded-tech-14029}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM OAK | 1.56-T20230927085643-189caed | [Oak API 1.56.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.56.0/index.html) |
| AEM SLING API | バージョン 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Version 1.4.20-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | バージョン 2.23.4 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
