---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: f4b2ea5dac880738e6412541f06b85a6a83ccf40
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 79%

---

# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 16799 {#release-16799}

2024年6月18日（PT）に公開された、メンテナンスリリース 16799 の継続的な改善点を以下にまとめます。以前のメンテナンスリリースは、リリース 16544 でした。

2024.6.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-16799}

* ASSETS-31977：アセットの移動、コピー、削除の操作を強化。
* ASSETS-33618：Dynamic Media におけるビデオの自動トランスクリプションと翻訳機能。
* ASSETS-35185：ContentHub および DM の承認アクションを実行して、プロパティを damAssetLucene プロパティに追加。
* ASSETS-35533：DRM プロパティと CAI プロパティを damAssetLucene インデックスに追加。
* ASSETS-37280：ソースサブタイトル（vtt）がまだ処理中の場合の翻訳の順次ジョブ処理。
* ASSETS-37559：アセット削除イベントの改善。
* ASSETS-37723：アセット公開イベントの実装。
* ASSETS-37724：アセット非公開イベントの実装。
* ASSETS-38614：共有リンク UI の機能強化。
* ASSETS-39601：アセットライブコピー名に検証用の正規表現を自動的に適用。
* ASSETS-39454：クイックスタートのビューア 2024.5.0 へのアップグレード。
* CNTBF-184：コンテンツバックフローの `/conf` の下のパスをサポート。

### 修正された問題 {#fixed-issues-16799}

* ASSETS-37335：フィルターの検索パネルを編集すると、すべてのボックスのチェックが外される。
* ASSETS-38069：タイムラインフィルターを選択した際の AEM DAM PDF プレビューの問題。
* ASSETS-38215：エンタープライズサブスクリプションの AEM as a Cloud Service で、Adobe Stock ライセンスボタンがグレー表示される。
* ASSETS-38578：アセットリンク共有レポートのハイパーリンクが正しくない。
* ASSETS-38678：コレクションの詳細で、設定が壊れて表示される。
* ASSETS-39071：元のレンディションの mimetype が null の場合、web 最適化配信で例外がスローされることがある。
* ASSETS-39316：コレクションで名前での並べ替えが機能しない。
* ASSETS-39377：リモート API からバックプレッシャを受け取ると、OneDrive からの一括読み込みが失敗することがある。
* ASSETS-39428：著作権管理 UI でのレンダリングの問題。
* CQ-4357150：cq-content-sync バンドルの Guava。
* GRANITE-52573：二重スラッシュ `//` を含むリクエストはステータスコード 400 で拒否される。
* SCRNS-4194：Google Guava API への依存関係の削除。
* SCRNS-4360：チャネルのコンテンツプロバイダーで、管理者以外のユーザーに対して「公開を管理」および「クイック公開」ボタンが表示されない。
* SCRNS-4323：screens.html からのローンチの表示／非表示。
* FORMS-14844:reCAPTCHA の検証に失敗しても、アダプティブFormsでフォーム送信が可能になります。
* FORMS-14984：送信されたデータに「submitMetaData」がない場合、CAPTCHA を使用したFormsが検証をスキップする。
* FORMS-14477：日付選択の検証で、ルールエディターの「次の後」および「次の前」オプションが正しく機能しません。
* FORMS-14019：ルールエディターの「サービスの呼び出し」機能がユニバーサルエディターで機能しない。
* FORMS-14336：フォームフィールドが選択されていない場合、エディターはフォーム要素全体にフォーカスを置いて開く必要があります。
* FORMS-15061：ルールエディターで「サービスを呼び出し」オプションを使用すると、ローダーの円が無期限に保持される。

### 既知の問題 {#known-issues-16799}

>[!NOTE]
> AEM エンジニアリングにより、16461 以降の現在の AEM リリースに影響するローンチ機能のリグレッションが特定されました。このリグレッションのため、ディープページが含まれていない新しいローンチ（新しいリリースが適用された後に作成）は、設定が見つからないため、適切に昇格されません。
> お使いの環境が影響を受ける場合は、不足している設定を特定して更新するシェルスクリプトをカスタマーサポートを通じて利用できます（内部参照 SITES-22457）。
> すべての適切な設定で新しいローンチが確実に作成されるように、より長期の修正を利用できるようになります。それまでは、内部パッチリリースもオンデマンドで利用できます。

#### Forms

* AEM SDK をインストールして以下を追加する場合： `AEM Forms add-on v2024.05.04.00-240400`の場合、Docker サービスは開始できません。 Docker サービスは、ローカル開発環境でレコードのドキュメントを生成するために必要です。 問題を修正するには：
   1. をダウンロード [ホットフィックス](/help/forms/assets/sdk_hotfix.zip). ホットフィックスをダウンロードすると、 `.zip` フォルダーがダウンロードされます。
   1. ダウンロードしたホットフィックスをフォルダーに抽出します。
   1. 古いバージョンを交換 `sdk.sh` および `sdk.bat` 手順 2 で抽出したフォルダー内に、新しいファイルがあるファイル。

### 変更通知 {#change-notice-16799}

* このリリースには、次の新しい製品インデックスバージョンが含まれています。
   * **damAssetLucene-11**
   * **fragments-11**

  以前のインデックスバージョンのカスタムバージョンは、新しい製品インデックスバージョンと自動的に結合されます。結合バージョンに対して、さらにカスタムアップデートを適用してください。

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
