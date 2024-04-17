---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 36fefbf74a288d60a9529f0c7273dd6b0557177b
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 39%

---

# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 15939 {#release-15939}

2024年4月17日（PT）に公開された、メンテナンスリリース 15939 の継続的な改善点を以下にまとめます。以前のメンテナンスリリースは、リリース 15860 でした。

2024.4.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=ja)を参照してください。

### 機能強化 {#enhancements-15939}

* GRANITE-39892：キューサイズ制限および公開準備完了のために、配布を更新します。
* GRANITE-48777:QS を com.adobe.granite.security.user-0.4.84 に更新します。
* GRANITE-49421：セグメントサービスプリンシパルのプロパティを追加しました。
* GRANITE-49855：新しい commons.json の使用時にクイックスタートビルドに失敗する機能モデルアナライザーを作成する。
* GRANITE-47995:cq:isDelivered の書き込みを切り替えることができます。
* GRANITE-36205：内部の Oak リリースのバージョンを最新のバージョンに更新します。
* GRANITE-50156 ユニバーサルエディターの AEMCS アフィニティを IMS ユーザー ID にバインドします。
* GRANITE-50556:Crosswalk バンドルを v0.1.18 にアップグレードします。
* GRANITE-50728:FileVault を 3.7.3-T20240308111857-81fa88f1 に更新します。
* GRANITE-50957:QS を com.adobe.granite.repository に 1.8.114 に更新します。
* GRANITE-50158:YAML ローダーでの OAuth サーバー間資格情報フローのサポートを追加。
* GRANITE-51327:Oak を最新の公開リリース（1.62.0）に更新します。
* SKYOPS-68091 Java 11 ランタイム イメージをバージョン 3.0.0 に更新します。
* SKYOPS-70421: org.apache.sling.servlet-helpers バンドルをアップグレードします
* SKYOPS-73483: AEMでのトークンのログを許可します。

### 修正された問題 {#fixed-issues-15939}

* GRANITE-46901：メッセージングクライアントに指標を追加する。
* GRANITE-48793:QS を com.adobe.granite.crx-explorer-1.1.28 に更新します。
* GRANITE-48937：オムニサーチがaem/start.html ページで機能しない。
* GRANITE-49638:RUM トランスファーファクトリの間違ったコンテンツタイプ設定を修正します。
* GRANITE-50141:IMSProviderImpl がログをスパム化している。
* SITES-20949:Youtube に referrerpolicy=&quot;strict-origin-when-cross-origin&quot;が追加された後、ComponentsIT.testEmbed が失敗する。
* SITES-21233：コアコンポーネントの更新 – 15860 へのアップグレード後にアコーディオンを修正。
* SKYOPS-74819:Apache Commons の重複したキーに対する後方互換性が損なわれました。
* SKYOPS-67087：特定のケースで Clientlib の集計が機能しない。
* CQ-4355415:6.5 SP18 でAEM通知のリンクが機能しない。

### 既知の問題 {#known-issues-15939}

なし。

### 廃止された機能と API {#deprecated-15939}

* [Adobe Developer Console での JWT 資格情報の廃止](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md)

AEM as a Cloud Serviceで廃止または削除された機能については、[廃止または削除された機能と API](/help/release-notes/deprecated-removed-features.md) を参照してください。

### 組み込みテクノロジー {#embedded-tech-15939}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM OAK | 1.62.0 | [Oak API 1.62.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.62.0/index.html) |
| AEM SLING API | 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | 2.24.6 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
