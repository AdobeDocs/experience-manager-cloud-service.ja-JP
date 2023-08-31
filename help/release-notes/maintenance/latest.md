---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: bb7d8145eb954557d185b58f884532f8f08c5a54
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 37%

---

# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 13239 {#release-13239}

2023 年 8 月 29 日に公開されたメンテナンスリリース13239の継続的な改善点を以下にまとめます。 このメンテナンスリリースは、リリース13206に代わるものです。

2023.9.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。 詳しくは、 [Experience Managerリリースロードマップ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=ja) を参照してください。

### 機能強化 {#enhancements-13239}

- GRANITE-46784:BearerAuthenticationHandler を無効にするオプションを追加します。
- GRANITE-36205：内部 oak リリースバージョンを最新に更新
- ASSETS-26713：新しい Experience UI ダッシュボードへのタッチ UI 外部リンク — unified-shell-integration および ui-touch-optimized アップグレード
- SKYOPS-63302: com.adobe.granite:com.adobe.granite.auth.saml を v1.0.54 にアップグレード
- GRANITE-46634: eventing client 1.4.0 へのアップグレード
- GRANITE-46788: Apache Commons IO 2.13.0、Commons Lang 3.13.0、Commons Code 1.16.0および Commons Compress へのライブラリの更新1.23.0
- GRANITE-46705: Apache Felix Http Jetty 4.1.14 への更新
- GRANITE-46631:Jackrabbit のバージョンを2.20.11に更新
- SKYOPS-61895: Jackrabbit Filevault 3.7.0 への更新

### 修正された問題 {#fixed-issues-13239}

- SKYOPS-63290：バケットの誤った展開を修正しました。
- SKYOPS-54607: Ratelimiter のサーバロード計算が失敗したリクエストに対して正しく行われない
- ASSETS-27648:ContentModelIT が他のバンドルから除外ファイルを読み取れません
- GRANITE-43744：認証要件とバニティパスの設定に誤りがある場合、Sling Authenticator が正しく機能しない
- GRANITE-46419:Auth0 Idp とのAEM統合の問題
- GRANITE-46292: AEM Cloud の更新後に Okta SAML 設定が機能しない
- GRANITE-47059: Granite Jetty SSL バンドルを削除

### 既知の問題 {#known-issues-13239}

なし。

### 組み込みテクノロジー {#embedded-tech-13239}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM OAK | 1.54-T20230817132355-3800a65 | [Oak API 1.54.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.54.0/index.html) |
| AEM SLING API | バージョン 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Version 1.4.20-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | バージョン 2.23.2 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
