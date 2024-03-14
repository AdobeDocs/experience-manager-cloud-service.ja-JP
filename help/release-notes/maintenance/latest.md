---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: d16d908d39df3c7d72dc48ac877c1543d2442416
workflow-type: tm+mt
source-wordcount: '1240'
ht-degree: 11%

---

# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 15262 {#release-15262}

2024年3月6日に公開された、メンテナンスリリース 15262 の継続的な改善点を以下にまとめます。以前のメンテナンスリリースは、リリース 14697 でした。

2024.3.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=ja)を参照してください。

### 機能強化 {#enhancements-15262}

* ASSETS-30632：リスト表示にBrand Portal公開ステータス列を別に追加しました。
* ASSETS-30934：のサポートが追加されました。 `Iptc4xmpCore:AltTextAccessibility` および `Iptc4xmpCore:ExtDescrAccessibility` プロパティをアセットメタデータエディターに追加します。
* ASSETS-31297:Dynamic Media からコピーされたアセットが削除されないよう、チェックが改善されました。
* ASSETS-33246：リリースインデックス定義 `damAssetLucene-10`.
* ASSETS-33590：処理プロファイルでのビデオの Web レンディションのサポートが追加されました。
* GRANITE-36205:oak のバージョンを 1.60-T20240131102219-0cde853 に更新します。
* SITES-19326: Assets UI のリンクを更新して、新しい CF エディターで CF を開きます。
* GUIDES-12945: AI を利用したスマートサーチクエリで、コンテンツのオーサリング中にコンテンツ参照を追加
* GUIDES-12706: Web エディターの改良されたバージョン履歴機能
* GUIDES-14948：翻訳パネルでのユーザーエクスペリエンスの向上
* GUIDES-8782：要素を挿入ダイアログボックスの検索ロジックが改善されました。
* GUIDES-14681：動的ベースラインを使用した複数の出力プリセットの公開機能
* AEMガイドの機能強化の完全なリストについては、次を参照してください。 [AEMガイドの新機能](https://experienceleague.adobe.com/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2402-release/whats-new-2024-2-0.html?lang=en#release-info)

### 修正された問題 {#fixed-issues-15262}

* ASSETS-15977：非推奨（廃止予定）の v1 検索イベントとパイプラインプロデューサーを削除します。
* ASSETS-18088：バティックライブラリの依存関係を 1.17 にアップグレードします。
* ASSETS-21965：メタデータの書き戻しワークフローは、アセットメタデータの変更時にのみ起動する必要があります。
* ASSETS-26368：ジョブ設定が存在しない場合、スケジュールされた一括読み込みジョブは削除されません。
* ASSETS-26549:「jcr:lastModifiedBy」:「workflow-process-service」を含むアセット/ノードは、リスト表示で「外部ユーザー」として表示されます。
* ASSETS-26842:「Firefly」テキストを更新して、処理プロファイルの「App Builder」を読み上げました。
* ASSETS-28708：一部の IMS トークンリクエストの応答が非常に遅くなっています。
* ASSETS-28767：フォルダーに大きいが含まれている場合、アセットの公開状態が一貫しない。 公開されたアセットの数。
* ASSETS-29011：読み取り専用ユーザーにはスマート切り抜きが表示されます。
* ASSETS-29348: AssetMoveEventHandler はメモリを消費しすぎる可能性があります。
* ASSETS-29738:WOFF ファイルの NullPointerException で、アセットのアップロード制限が失敗する。
* ASSETS-30068: Asset Essentials の一括読み込みで、「ジョブは完了しましたが、エラーが発生しました」のステータス COMPLETED_WITH_ERROR が含まれます。
* ASSETS-30261：アセットイベントのパイプラインに送信された imsUserId が正しくありません。
* ASSETS-30538：ページファイルの移動後に「ページを表示」オプションが表示されないPDF。
* ASSETS-30626：空の assetId を持つアセットに関して報告された配信リクエストの作成に失敗しました。
* ASSETS-30756：フォルダー名が「html」で終わると、アセットの移動ウィザードアクションが失敗します。
* ASSETS-30810：従来の youtube 設定をレンダリングする前に、タグの不要部分を削除します。
* ASSETS-31015：ファイル名拡張子が.msg のアセットをアップロードできません。
* ASSETS-31038：通知サービスで受信したタスクイベントは処理されていません。
* ASSETS-31097：トラバーサルクエリの警告を避けるために、WCM コンテンツの非同期コピーを無効にします。
* ASSETS-31256:「jcr:lastModifiedBy」:「workflow-process-service」を含むアセット/ノードは、リスト表示で「外部ユーザー」として表示されます。
* ASSETS-31260：ドロップダウン JSON に大きなリストがある場合、アセットメタデータフォームドロップダウンフィールドが正しく機能しません。
* ASSETS-31280：コレクションに追加する際に、統合された構造でアセットをダウンロードする。
* ASSETS-31301: `dynamicmedia_sly.js` は、Use API で正しくインスタンス化できません。
* ASSETS-31330:ko_KR：字幕およびオーディオトラック内の非ローカライズの文字列。
* ASSETS-31405：大きなInDesignレイアウトでは、InDesignサーバーの処理が失敗する。
* ASSETS-31570：統合シェル — アセットの詳細「保存して閉じる」、「キャンセル」ボタンを複数回押して機能させる必要があります。
* ASSETS-31673：大きなアセットファイルの一括読み込みに失敗しましたDropbox。
* ASSETS-32108:AEM Assetsが表示設定でユーザー定義のカードサイズを保存しない。
* ASSETS-32230:com.adobe.aem.repoapi バンドルの最小ランタイムバージョンをアップグレードします。
* ASSETS-32544：メタデータの書き出しジョブが断続的に失敗する。
* ASSETS-32679：アセット (PDF) プレビューでのキャッシュの問題。
* ASSETS-32754：以前にログインしていないユーザーにタスクを割り当てることはできません。
* ASSETS-32755: com/adobe/cq/dam/assetmove ジョブトピックを、順序付きキューを使用するように設定します。
* ASSETS-32899：コレクション内の検索が非常に遅い。
* ASSETS-33098:AEM Assets検索ファセット「タグの述語」が期待どおりに動作しない。
* ASSETS-33454：レビュータスクアクティビティとコメントがタイムラインに表示されない。
* ASSETS-34088:PDFのプレビューがAEM Assetsで動作しない。
* ASSETS-34155:Dynamic Media - AEMビューア/2024.1.0 を更新しました。
* ASSETS-34684：コンテンツツリーで複数値の dc:title を処理します。
* ASSETS-34789：ファイル名の競合チェックでの正規化の問題を修正しました。
* DXML-13276: AEM Guides - GraniteContent のインデックスを統合し、ライブラリから削除します。
* GRANITE-47995:「cq:isDelivered」プロパティとの競合が原因で削除操作が失敗する場合があります。
* GRANITE-48079:OAuth オンライントークン検証のPOSTリクエストを有効にします。
* GRANITE-48143: org.apache.sling.resource を 1.4.4 にアップグレードします。
* GRANITE-49031: Jackson 2.16.1にアップデート。
* SCRNS-3961: Screens - Sequence channel：フェードトランジションで使用される Jquery アニメーションは黒い画面になります。
* SITES-15868：フラグメントを一覧表示する際のパフォーマンスを向上させます。
* SITES-16079: `/fragments/{id}/references` 重複の返却を開始しました。
* SITES-16118：フラグメントにパッチが適用され、モデルにフラグメントフィールドがない場合、例外が発生します。
* SITES-16121：モデル日付フィールドの取得で例外がスローされる。
* SITES-16207:POST/adobe/sites/cf/models 操作は、2 つの異なる OK ステータスコードを返します。
* SITES-17361: Jsup を sites-headless バンドルに再埋め込みします。
* SITES-17768：コンテンツフラグメントで参照されているアセットのDynamic Media URL を出力するGraphQL。
* SKYOPS-66622: buildTransform が有効なパイプラインの実行後にオーサーデプロイメントがループするとクラッシュする問題を修正しました。
* SKYOPS-69977：アダプティブ画像サーブレットが最新の更新後に画像を読み込まない。
* GUIDES-15045：エディターでのスペルチェックで、候補を選択できません。
* GUIDES-14968：グローバルナビゲーションボタンが機能せず、ダッシュボードの読み込みに失敗する。
* GUIDES-14943：ネイティブPDFの公開で、条件プリセット内のカスタム属性がネイティブPDFの公開で機能しない。
* GUIDES-15085：ネイティブPDFの公開で、2023 年 12 月のAdobe Experience Managerガイドのリリースで主要な参照が解決されません。
* GUIDES-13486: **ベースラインフィルター** ファイルが Web エディタでファイル名で動作しない。
* 修正された問題の完全なリストについては、 AEMガイドを参照してください。 [AEMガイドの修正された問題](https://experienceleague.adobe.com/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2402-release/fixed-issues-2024-2-0.html?lang=en#release-info)

### 既知の問題 {#known-issues-15262}

* ASSETS-35923: `UnsupportedClassVersionError` CM パイプラインビルドのステップ（アップグレード後） `aem-sdk-api` バージョン： `2024.2.15262.20240224T002940Z-231200`. **CM Java バージョンを 11 に設定するには、顧客のアクションが必要です**&#x200B;を参照してください。 [ビルド環境/ Maven JDK バージョンの設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/create-application-project/build-environment-details.html?lang=en#alternate-maven-jdk-version)
* ASSETS-35860: AEM Assets列表示のタイムゾーン変換が正しくありません。
* SCRNS-4171: Windows Screens にアップグレードしてチャネルを公開すると、Windows Screens が空白になり、機能しなくな15262る。
* GRANITE-50774: GraniteContent は、初期時にプロパティ値の決定論的順序を使用する必要があります。

### 変更通知 {#change-notice-15262}

**必要なアクション**

#### CM Java バージョンを 11 に設定 {#set-java-version-11}

新しいバージョンの aem-sdk-api には、Java 11 ターゲットでコンパイルされたクラスが含まれていますが、Cloud Manager ビルド環境のデフォルト JDK バージョン 1.8 とは互換性がありません。この更新では、Maven が JDK 11 を使用して実行されている必要があります。

お客様は、 `.cloudmanager/java-version` ファイルを git リポジトリのルートに、次の内容で保存します。 `11`. [ビルド環境/ Maven JDK バージョンの設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/create-application-project/build-environment-details.html?lang=en#alternate-maven-jdk-version)

#### aem-cloud-testing-clients を 1.2.1 に更新しました。 {#update-aem-cloud-testing-clients}

今後の変更にはライブラリが必要になります [aem-cloud-testing-clients](https://github.com/adobe/aem-testing-clients) カスタム機能テストで使用され、少なくともバージョンに更新されます **1.2.1**

依存関係を `it.tests/pom.xml` が更新されました。

```xml
<dependency>
   <groupId>com.adobe.cq</groupId>
   <artifactId>aem-cloud-testing-clients</artifactId>
   <version>1.2.1</version>
</dependency>
```

この変更は 2024 年 4 月 7 日以降に必要になります。

依存関係ライブラリの更新に失敗すると、「カスタム機能テスト」手順でパイプラインにエラーが発生します。

### 組み込みテクノロジー {#embedded-tech-15262}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM OAK | 1.60-T20240131102219-0cde853 | [Oak API 1.60.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.60.0/index.html) |
| AEM SLING API | バージョン 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Version 1.4.20-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | バージョン 2.23.4 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
