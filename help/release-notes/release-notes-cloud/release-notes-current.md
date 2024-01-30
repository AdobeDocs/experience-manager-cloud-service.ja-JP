---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: 77d38f03f18eb6b0fdc2f2eec5b2dc4b608b8057
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 46%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート  {#release-notes}

以下のセクションでは、[!DNL Experience Manager] as a Cloud Service の現在（最新）のバージョンの機能リリースノートの概要について説明します。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2021年、2022年）のリリースノートに移動できます。
>
>[!DNL Experience Manager] as a Cloud Service の今後の機能のアクティベーションについての詳細は、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=ja)をご覧ください。

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の最新の機能リリース（2024.1.0）のリリース日は、2024年1月25日（PT）です。次回の機能リリース（2024.2.0）は 2024年2月29日（PT）に予定されています。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

## リリースビデオ {#release-video}

2024.1.0 リリースで追加された機能の概要については、2024年1月 のリリースに関する概要ビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3427041?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### AEM SitesでのExtension Manager {#sites-extension-manager}

**新しい [AEM SitesでのExtension Manager](https://developer.adobe.com/uix/docs/extension-manager/)** UI 拡張機能を設定してAEM設定をパーソナライズする。

![AEM SitesでのExtension Manager](/help/assets/sites/extension-manager/homepage.png)

AEM SitesのExtension Managerを使用すると、開発者や実務担当者は、デベロッパーがアクセス、管理およびカスタマイズできます [UI 拡張機能](https://developer.adobe.com/uix/docs/) で作成済み [AdobeApp Builder](https://developer.adobe.com/app-builder/) AEM Sitesの機能を強化する。
Extension Managerを使用すると、次のことができます。

* インスタンス単位で拡張機能を有効または無効にする。
* 拡張パラメーターを設定する。
* 拡張機能をプレビューし、共有可能なプレビューリンクを生成する。
* インタラクティブデモを介して UI の拡張機能を確認する
* ファーストパーティの拡張機能を使用して、Adobeの実験機能にアクセスします。

アドビでは、UI 拡張機能に関するフィードバックと新しい使用例を積極的に求めています。 連携を希望される場合は、次の宛先にメールを送信してください： `uix@adobe.com`.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 管理ビューのプレリリース機能 {#admin-view-prerelease}

**サポートされるすべてのビデオタイプのレンディションをプレビュー**

Experience Manager Assetsでは、処理プロファイルの設定が不要で、サポートされるすべてのビデオタイプのプレビューレンディションがデフォルトで生成されるようになりました

### Assets ビュー {#assets-view-features}

**スマートタグのブロックリスト**

Assets Essentials では、ブロックリストを定義できるようになりました。このリストは、リポジトリにアップロードする際に、アセットにスマートタグとして追加する必要がない単語で構成されます。この機能は、ブランドのコンプライアンスを保持し、スマートタグのモデレートにかかる作業を軽減するのに役立ちます。

![スマートタグのブロックリストに加える](/help/assets/assets/block-tags.png)


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### アーリーアダプタープログラム {#forms-early-adopter}

* **[アダプティブフォームをAdobe Workfront Fusion に送信するシナリオ](/help/forms/submit-adaptive-form-to-workfront-fusion.md)**:Forms as a Cloud Serviceには、アダプティブフォームをAdobe Workfrontに簡単に接続するための既製のオプションが用意されています。 これにより、アダプティブフォームをAdobe Workfrontシナリオに送信するプロセスが簡単になり、アダプティブフォームの送信時にWorkfront Fusion シナリオをトリガーできます。

* **[右から左への言語のサポート](/help/forms/supporting-new-language-localization-core-components.md)**：コアコンポーネントに基づいて構築されたアダプティブFormsは、アラビア語、ペルシャ語、ウルドゥー語などの右から左 (RTL) 言語で表示できるようになりました。 RTL 言語は世界で 20 億人以上の人々が話しています RTL 言語のフォームを使用すると、アダプティブフォームのリーチを拡大して、これらの多様なオーディエンスに対応し、RTL 市場へと選択することができます。 地域によっては、現地の言語でフォームを提供することが法的義務でもあります。 現地の言語に対応することで、より広いオーディエンスへの扉を開くだけでなく、関連する法令への準拠も確保できます。

  ![右から左への言語サポート](/help/forms/assets/right-to-left-language-support.png)

* **[DocAssurance API（通信 API の一部）を使用したドキュメントの保護](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**：DocAssurance API を使用すると、ドキュメントに署名および暗号化して、機密情報を保護できます。暗号化により、ドキュメントのコンテンツは読み取り不可能な形式に変換され、許可されたユーザーのみがアクセスできるようになります。この強化された保護層は、貴重なデータを信頼できない環境にさらすことなく、安心感ももたらします。Signature API を使用すると、組織は配布および受信する Adobe PDF ドキュメントのセキュリティとプライバシーを保護できます。このサービスでは、デジタル署名と証明書を使用して、意図された受信者のみがドキュメントを変更できるようにします。

  公式メール ID から `aem-forms-early-adopter-program@adobe.com` に送信して早期導入プログラムに参加し、機能へのアクセスをリクエストできます。

## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### Dynatrace のサポート {#dynatrace}

Dynater のお客様は、AEMの使用状況を監視できます。 [読み方](/help/implementing/cloud-manager/dynatrace.md) をクリックして、アプリケーションのパフォーマンス監視用に Dynaterace 環境との接続をリクエストします。 すべてのお客様が利用できるNew Relic APM は、Dynatrace が有効になっている場合、データの収集を停止します。

### サイトテーマとサイトテンプレートを使用したフロントエンドコードの RDE サポート：アーリーアダプタープログラム {#rde-frontend-early-adopter}

[急速な開発環境 (RDE)](/help/implementing/developing/introduction/rapid-development-environments.md) 次の基づくフロントエンドコードをサポートするようになりました。 [サイトテーマ](/help/sites-cloud/administering/site-creation/site-themes.md) および [サイトテンプレート](/help/sites-cloud/administering/site-creation/site-templates.md)早期採用者向け。 RDE を使用すると、これは、 [フロントエンドパイプライン](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md). 次の場所に連絡してください： **aemcs-rde-support@adobe.com** 試してみて、フィードバックを提供してください。

## Cloud Manager {#cloud-manager}

Cloud Manager の月次リリースの完全なリストは、[こちら](/help/implementing/cloud-manager/release-notes/current.md)で確認できます。

## 移行ツール {#migration-tools}

移行ツールのリリースの完全なリストは、[こちら](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)で確認できます
