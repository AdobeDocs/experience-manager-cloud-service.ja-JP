---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 60952db4172b882b71a0b230fc8f4c27154e9cc0
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 72%

---

# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 15977 {#release-15977}

2024年4月19日（PT）に公開された、メンテナンスリリース 15977 の継続的な改善点を以下にまとめます。以前のメンテナンスリリースは、リリース 15939 でした。

2024.4.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-15977}

* GRANITE-51335：AEM ヘルスチェックを最適化して、インスタンスの安定性を向上。

### 修正された問題 {#fixed-issues-15977}

* CQ-4357226：OAuth 資格情報の IMS 設定サポートにおける回帰を修正。
* GRANITE-51335：レート制限を 5.0.4 にアップグレードして、Felix ヘルスチェックの登録を修正

### 既知の問題 {#known-issues-15977}

* **（AEM Formsのみ）** AEM Cloud Foundation メンテナンスリリース 15977 をインストールした後、アダプティブフォームのフィールドが、フォームのオーサリング中および公開済みフォームで誤った順序でレンダリングされます。 AEM FormsAdobeを使用する場合は、今後のメンテナンスリリースで問題が解決されるまで、15977 リリースにアップグレードしないことをお勧めします。 これにより、不便を避けることができます。

### 廃止された機能と API {#deprecated-15977}

* [Adobe Developer Console での JWT 資格情報の廃止](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md)

* 2024年5月1日（PT）を以て、Adobe Dynamic Media は以下のサポートを終了します。

   * SSL（Secure Socket Layer）2.0
   * SSL 3.0
   * TLS（Transport Layer Security）1.0 および 1.1
   * TLS 1.2 での以下の脆弱な暗号：
      * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384`
      * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA`
      * `TLS_RSA_WITH_AES_256_GCM_SHA384`
      * `TLS_RSA_WITH_AES_256_CBC_SHA256`
      * `TLS_RSA_WITH_AES_256_CBC_SHA`
      * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256`
      * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA`
      * `TLS_RSA_WITH_AES_128_GCM_SHA256`
      * `TLS_RSA_WITH_AES_128_CBC_SHA256`
      * `TLS_RSA_WITH_AES_128_CBC_SHA`
      * `TLS_RSA_WITH_CAMELLIA_256_CBC_SHA`
      * `TLS_RSA_WITH_CAMELLIA_128_CBC_SHA`
      * `TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA`
      * `TLS_RSA_WITH_SDES_EDE_CBC_SHA`


AEMのas a Cloud Service機能で非推奨（廃止予定）または削除された機能については、以下を参照してください。 [非推奨（廃止予定）の機能および削除された API](/help/release-notes/deprecated-removed-features.md).

### 組み込みテクノロジー {#embedded-tech-15977}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.62.0 | [Oak API 1.62.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.62.0/index.html) |
| AEM SLING API | 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | 2.24.6 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
