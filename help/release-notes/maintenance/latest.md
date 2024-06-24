---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: fd687498a8c72bf5d47b7b97aadf22d7d1e8dd2b
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 30%

---

# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 16799 {#release-16799}

2024年6月18日（PT）に公開された、メンテナンスリリース 16799 の継続的な改善点を以下にまとめます。以前のメンテナンスリリースは、リリース 16544 でした。

2024.6.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-16799}

* ASSETS-31977：アセットの移動、コピー、削除の操作が強化されました。
* ASSETS-33618:Dynamic Mediaにおけるビデオの自動トランスクリプションと翻訳機能。
* ASSETS-35185:ContentHub および DM の承認アクションを実行して、プロパティを damAssetLucene プロパティに追加。
* ASSETS-35533:DRM プロパティと CAI プロパティを damAssetLucene インデックスに追加します。
* ASSETS-37280：ソースサブタイトル（vtt）がまだ処理中の場合の翻訳の順次ジョブ処理。
* ASSETS-37559：アセット削除イベントを改善しました。
* ASSETS-37723：アセットの公開イベントを実装する。
* ASSETS-37724：アセットの非公開イベントを実装する。
* ASSETS-38614：共有リンク UI の機能強化。
* ASSETS-39601：アセットライブコピー名に検証用の正規表現を自動的に適用します。
* ASSETS-39454：クイックスタートのビューア 2024.5.0 へのアップグレード。
* CNTBF-184：下のサポートパス `/conf` コンテンツのバックフローで。

### 修正された問題 {#fixed-issues-16799}

* ASSETS-37335：フィルターの検索パネルを編集すると、すべてのボックスのチェックが外される。
* ASSETS-38069：タイムラインフィルターを選択した際のAEM DAM PDFのプレビューの問題。
* ASSETS-38215：エンタープライズサブスクリプションのAEMas a Cloud Serviceで、Adobe Stock ライセンスボタンがグレー表示される。
* ASSETS-38578:Assets リンク共有レポートのハイパーリンクが正しくありません。
* ASSETS-38678：コレクションの詳細で、設定が壊れて表示される。
* ASSETS-39071：元のレンディションの mimetype が null の場合、web 最適化配信で例外がスローされる可能性がある。
* ASSETS-39316：名前での並べ替えがコレクションで機能しない。
* ASSETS-39377：リモート API からバックプレッシャを受け取ると、OneDrive からの一括読み込みが失敗する場合があります。
* ASSETS-39428：著作権管理 UI でのレンダリングの問題。
* CQ-4357150:cq-content-sync バンドルの Guava。
* GRANITE-52573：二重スラッシュを含むリクエスト `//` が拒否され、ステータスコード 400 が表示されます。
* SCRNS-4194:Google Guava API への依存を解消。
* SCRNS-4360：チャネルのコンテンツプロバイダーで、管理者以外のユーザーに対して「公開を管理」および「クイック公開」ボタンが表示されない。
* SCRNS-4323: screens.html からのローンチの表示/非表示。

### 既知の問題 {#known-issues-16799}

>[!NOTE]
> AEM エンジニアリングにより、16461 以降の現在のAEM リリースに影響するローンチ機能のリグレッションが特定されました。 このリグレッションのため、ディープページが含まれていない新しいローンチ（新しいリリースが適用された後に作成）は、設定が見つからないため、適切に昇格されません。
> 環境が影響を受ける場合は、不足している設定を識別および更新するシェルスクリプトをカスタマーサポートを通じて利用できます（内部参照 SITES-22457）。
> すべての適切な設定で新しいローンチが確実に作成されるように、より長期の修正が可能になります。 それまでは、内部パッチリリースもオンデマンドで利用できます。

#### Forms

1. ユーザーがAEM Forms SDK のバージョンよりも大きいバージョンをダウンロードする場合 `AEM Forms add-on v2024.05.04.00-240400`を指定すると、バッチファイルで Docker サービスを開始できなくなります。 この問題を解決するには：
   1. をダウンロード [フォルダー](/help/forms/assets/sdk_hotfix.zip).
   1. ダウンロードしたフォルダーからコンテンツを抽出し、 `sdk.sh` および `sdk.bat` ファイル。
   1. 既存のを `sdk.sh` および `sdk.bat` 新しいファイルを含むAEM Forms SDK 内のファイル。

### 変更通知 {#change-notice-16799}

* このリリースには、次の新しい製品インデックスバージョンが含まれています。
   * **damAssetLucene-11**
   * **fragments-11**

  以前のインデックスバージョンのカスタムバージョンは、新しい製品インデックスバージョンと自動的に結合されます。 統合後のバージョンに対して、さらにカスタムのアップデートを適用してください。

* 2024年9月以降、AEM as a Cloud Service では、Sling Model Exporter フレームワークを介したリソースリゾルバーのシリアル化が無効になります。詳しくは、[ドキュメント](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md)を参照してください。

### 非推奨（廃止予定）機能と API {#deprecated-16799}

AEM as a Cloud Service で非推奨（廃止予定）または削除された機能については、[非推奨（廃止予定）および削除された機能と API](/help/release-notes/deprecated-removed-features.md)を参照してください。

### 組み込みテクノロジー {#embedded-tech-16799}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.64.0 | [Oak API 1.64.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.64.0/index.html) |
| AEM SLING API | 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.22-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | 2.25.4 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
