---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: b7e7bc7546b836667fff9db0ea5419e751f492cb
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 78%

---

# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 15977 {#release-15977}

2024年4月19日（PT）に公開された、メンテナンスリリース 15977 の継続的な改善点を以下にまとめます。以前のメンテナンスリリースは、リリース 15939 でした。

2024.4.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=ja)を参照してください。

### 機能強化 {#enhancements-15977}

* GRANITE-51335：AEM ヘルスチェックを最適化して、インスタンスの安定性を向上。

### 修正された問題 {#fixed-issues-15977}

* CQ-4357226：OAuth 資格情報の IMS 設定サポートにおける回帰を修正。
* GRANITE-51335：レート制限を 5.0.4 にアップグレードして、Felix ヘルスチェックの登録を修正

### 既知の問題 {#known-issues-15977}

* **（AEM Formsのみ）** AEM Cloud Foundation メンテナンスリリース 15977 をインストールした後、アダプティブフォームのフィールドが、フォームのオーサリング中および公開済みフォームで誤った順序でレンダリングされます。 AEM Formsを使用している場合、ご不便をおかけしないよう、今後のメンテナンスリリースで問題が解決されるまで、15977 リリースにはアップグレードしないことをお勧めします。


### 廃止された機能と API {#deprecated-15977}

* [Adobe Developer Console での JWT 資格情報の廃止](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md)

AEM as a Cloud Serviceで廃止または削除された機能については、[廃止または削除された機能と API](/help/release-notes/deprecated-removed-features.md) を参照してください。

### 組み込みテクノロジー {#embedded-tech-15977}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM OAK | 1.62.0 | [Oak API 1.62.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.62.0/index.html) |
| AEM SLING API | 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | 2.24.6 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
