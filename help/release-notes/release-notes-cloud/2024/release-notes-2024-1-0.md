---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2024.1.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2024.1.0 リリースのリリースノート。'
exl-id: 9f5d97c6-6536-4593-acbf-cbe8bf9b5eeb
feature: Release Information
role: Admin
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 89%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の 2024.1.0 リリースノート {#release-notes}

以下の節では、[!DNL Experience Manager] as a Cloud Service の 2024.1.0 バージョンの機能リリースノートの概要について説明します。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2021年、2022年）のリリースノートに移動できます。
>
>[!DNL Experience Manager] as a Cloud Service の今後の機能のアクティベーションについての詳細は、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=ja)をご覧ください。

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の最新の機能リリース（2024.1.0）のリリース日は、2024年1月25日（PT）です。次回の機能リリース（2024.3.0）は 2024年4月11日（PT）に予定されています。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

## リリースビデオ {#release-video}

2024.1.0 リリースで追加された機能の概要については、2024年1月のリリースに関する概要ビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3427041?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### AEM Sites での Extension Manager {#sites-extension-manager}

**新しい [AEM Sites での Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/)** を探索して、UI 拡張機能を設定して AEM 設定をパーソナライズします。

![AEM Sites での Extension Manager](/help/assets/sites/extension-manager/homepage.png)

AEM Sites での Extension Manager を使用すると、開発者や実務担当者は、AEM Sites の機能を強化するために [Adobe App Builder](https://developer.adobe.com/app-builder/) で作成された [UI 拡張機能](https://developer.adobe.com/uix/docs/)にアクセスしたり、このような拡張機能を管理およびカスタマイズしたりできます。
Extension Manager で以下を実行できます。

* インスタンス単位で拡張機能を有効または無効にする
* 拡張パラメーターの設定
* 拡張機能のプレビューと、共有可能なプレビューリンクの生成
* インタラクティブデモを介した UI 拡張機能の確認
* ファーストパーティの拡張機能を使用した、アドビの実験機能へのアクセス

アドビでは、UI 拡張機能に関するフィードバックと新しいユースケースを積極的に求めています。連絡を希望される場合は、`uix@adobe.com` にメールを送信してください。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 管理ビューのプレリリース機能 {#admin-view-prerelease}

**サポートされるすべてのビデオタイプのレンディションのプレビュー**

Experience Manager Assets では、処理プロファイル設定を行わなくても、サポートされるすべてのビデオタイプのプレビューレンディションをデフォルトで生成するようになりました。

### アセットビュー {#assets-view-features}

**スマートタグのブロックリスト**

Assets Essentials では、ブロックリストを定義できるようになりました。このリストは、リポジトリにアップロードする際に、アセットにスマートタグとして追加する必要がない単語で構成されます。この機能は、ブランドのコンプライアンスを保持し、スマートタグのモデレートにかかる作業を軽減するのに役立ちます。

![スマートタグのブロックリスト](/help/assets/assets/block-tags.png)


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### 早期導入プログラム {#forms-early-adopter}

* **[Adobe Workfront Fusion シナリオへのアダプティブフォームの送信](/help/forms/submit-adaptive-form-to-workfront-fusion.md)**：Forms as a Cloud Service には、アダプティブフォームを Adobe Workfront に簡単に接続するための標準オプションが用意されています。これにより、Adobe Workfront シナリオにアダプティブフォームを送信するプロセスが簡単になり、アダプティブフォームの送信時に Workfront Fusion シナリオをトリガーできます。

* **[右横書き言語のサポート](/help/forms/supporting-new-language-localization-core-components.md)**：コアコンポーネントに基づいて作成されたアダプティブフォームを、アラビア語、ペルシア語、ウルドゥー語などの右横書き（RTL）言語で表示できるようになりました。RTL 言語は、世界中で 20 億人以上の人々が話しています。RTL 言語のフォームを使用すると、アダプティブフォームのリーチを拡大して、これらの多様なオーディエンスに対応し、RTL マーケットを選択できます。また、特定の地域では、現地の言語でフォームを提供することは法的義務として定められています。現地の言語に対応することで、より幅広いオーディエンスに扉を開くだけでなく、関連する法律や規制を確実に遵守できます。

  ![右横書き言語のサポート](/help/forms/assets/right-to-left-language-support.png)

* **[DocAssurance API（通信 API の一部）を使用したドキュメントの保護](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**：DocAssurance API を使用すると、ドキュメントに署名および暗号化して、機密情報を保護できます。暗号化により、ドキュメントのコンテンツは読み取り不可能な形式に変換され、許可されたユーザーのみがアクセスできるようになります。この強化された保護層は、貴重なデータを信頼できない環境にさらすことなく、安心感ももたらします。Signature API を使用すると、組織は配布および受信する Adobe PDF ドキュメントのセキュリティとプライバシーを保護できます。このサービスでは、デジタル署名と証明書を使用して、意図された受信者のみがドキュメントを変更できるようにします。

  公式メール ID から `aem-forms-early-adopter-program@adobe.com` に送信して早期導入プログラムに参加し、機能へのアクセスをリクエストできます。

* **[運用上のテレメトリサービスを利用](/help/implementing/cloud-manager/content-requests.md#real-user-monitoring-for-aem-as-a-cloud-service)** して、AEM as a Cloud Serviceのクライアントサイド収集を有効にできます。
運用上のテレメトリサービスは、ユーザーのインタラクションをより正確に反映し、web サイトのエンゲージメントの信頼性の高い測定値を保証します。 ページのパフォーマンスに関する高度なインサイトを取得する絶好の機会です。 これは、アドビが管理する CDN やアドビ以外が管理する CDN を使用するお客様にとって有益です。さらに、アドビ以外が管理する CDN を使用しているお客様は、自動トラフィックレポートを有効にできるようになり、アドビとトラフィックレポートを共有する必要がなくなります。

  この新機能のテストやフィードバックの提供に関心がある場合は、Adobe IDに関連付けられたメールアドレスから、運用上のテレメトリを有効にする各環境のドメイン名と共に、`aemcs-rum-adopter@adobe.com` にメールを送信してください。 Adobeの製品チームが、運用上のテレメトリサービスを有効にします。

## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### Dynatrace のサポート {#dynatrace}

Dynatrace のお客様は、AEM の使用状況を監視できます。アプリケーションのパフォーマンスをモニタリングするために Dynatrace 環境との接続をリクエストする方法については、[こちら](/help/implementing/cloud-manager/dynatrace.md)を参照してください。Dynatrace が有効になっている場合、すべてのお客様が利用できる New Relic APM は、データの収集を停止します。

### サイトテーマとサイトテンプレートを使用したフロントエンドコードの RDE サポート：早期導入プログラム {#rde-frontend-early-adopter}

[高速開発環境（RDE）](/help/implementing/developing/introduction/rapid-development-environments.md)は、早期導入者向けに、[サイトテーマ](/help/sites-cloud/administering/site-creation/site-themes.md)と[サイトテンプレート](/help/sites-cloud/administering/site-creation/site-templates.md)に基づいたフロントエンドコードをサポートするようになりました。RDE では、[フロントエンドパイプライン](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md)ではなくコマンドラインディレクティブを使用して行われます。試してフィードバックを提供するには、**aemcs-rde-support@adobe.com** までご連絡ください。

### ドメインマッピング早期導入プログラム {#cdn-config-early-adopter}

オプションでライセンス可能な web アプリケーションファイアウォール（WAF）ルールを含む、最近リリースされた[トラフィックフィルタールール](/help/security/traffic-filter-rules-including-waf.md)に加えて、設定パイプラインを使用して[他のタイプの CDN 設定](/help/implementing/dispatcher/cdn-configuring-traffic.md)を宣言およびデプロイする機会があります。早期導入プログラムに参加するには、**`aemcs-cdn-config-adopter@adobe.com`** に電子メールを送信して、次へのアクセス権を取得します。

* 301/302 クライアントサイドのリダイレクト
* 任意の接触チャネルに対するエッジでのリクエストのプロキシ処理
* URL 変換
* リクエストヘッダーまたは応答ヘッダーの設定または変更
* CDN が AEM に到達できない場合のカスタムエラーページ

## Cloud Manager {#cloud-manager}

Cloud Manager の月次リリースの完全なリストは、[こちら](/help/implementing/cloud-manager/release-notes/current.md)で確認できます。

## 移行ツール {#migration-tools}

移行ツールのリリースの完全なリストは、[こちら](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)で確認できます
