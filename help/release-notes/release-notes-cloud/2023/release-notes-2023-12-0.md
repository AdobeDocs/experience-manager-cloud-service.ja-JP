---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.12.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.12.0 リリースのリリースノート。'
exl-id: b36add58-a2ba-4299-94be-e0026e9c553c
feature: Release Information
role: Admin
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 72%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の 2023.12.0 リリースノート {#release-notes}

以下の節では、[!DNL Experience Manager] as a Cloud Service の 2023.12.0 バージョンの機能リリースノートの概要について説明します。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2021年、2022年）のリリースノートに移動できます。
>
>[!DNL Experience Manager] as a Cloud Service の今後の機能のアクティベーションについての詳細は、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=ja)をご覧ください。

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の最新の機能リリース（2023.12.0）の公開日は 2023年12月14日（PT）です。次回の機能リリース（2024.1.0）は 2023年1月25日（PT）に予定されています。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

<!-- 

## Release Video {#release-video}

Have a look at the December 2023 Release Overview video for a summary of the features added in the 2023.12.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3425864?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### 早期導入プログラム {#sites-early-adopter}

**運用上のテレメトリサービス [ を利用して、AEM as a Cloud Serviceのクライアントサイド収集を有効にすることもできます](/help/implementing/cloud-manager/content-requests.md#real-user-monitoring-for-aem-as-a-cloud-service)**。

運用上のテレメトリデータサービスは、ユーザーのインタラクションをより正確に反映し、web サイトエンゲージメントの信頼性の高い測定を保証します。 ページのパフォーマンスに関する高度なインサイトを取得する絶好の機会です。 これは、アドビが管理する CDN やアドビ以外が管理する CDN を使用するお客様にとって有益です。さらに、アドビ以外が管理する CDN を使用しているお客様は、自動トラフィックレポートを有効にできるようになり、アドビとトラフィックレポートを共有する必要がなくなります。

この新機能のテストやフィードバックの送信に関心がある場合は、Adobe IDに関連付けられたメールアドレスから、実稼動、ステージ、開発環境のドメイン名と共に `aemcs-rum-adopter@adobe.com` にメールを送信してください。 Adobeの製品チームが、運用上のテレメトリデータサービスを有効にします。


## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Assets ビューの新機能 {#assets-view-features}

**Adobe Firefly を使用した生成 AI 画像の作成**

Adobe Firefly のテキストから画像生成機能を統合して、検索クエリに基づいて新しい画像を作成します（Adobe Firefly ライセンスが必要です）。

![Assets Firefly の統合](/help/assets/assets/assets-firefly-integration.png)

**類似検索画像**

画像を選択し、Experience Manager Assets リポジトリで類似の画像を表示することで、コンテンツを簡単に検索できるようになりました。

<!--

* **Smart tags blocklist**: Experience Manager Assets now enables you to define a list of blocked tags. These tags are automatically removed from the auto-generated smart tags when you upload assets to the repository. This capability performs tags governance and saves a lot of time as you can add a tag to the block list and AEM Assets automatically excludes it from the list of tags for any of the assets that are added to the repository.

  ![storage usage insights](/help/assets/assets/block-tags.png)


**Video Preview**: AEM Assets now generates preview renditions of all supported video formats by default, without the need to configure a processing profile.

-->

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Experience Manager Forms] の新機能 {#forms-features}

* **[アダプティブFormsとMicrosoftの接続® SharePoint リスト](/help/forms/configure-submit-actions-core-components.md#submit-to-sharepoint)**:AEM Formsでは、SharePointのリスト機能を使用できるフォームデータをSharePoint リストに直接送信する OOTB 統合が提供されます。 Microsoft SharePoint リストをフォームデータモデルのデータソースとして設定し、**フォームデータモデルを使用して送信** 送信アクションを使用して、アダプティブフォームをSharePoint リストに接続できます。

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### 早期導入プログラム {#forms-early-adopter}

* **[Adobe Workfront Fusion シナリオへのアダプティブフォームの送信](/help/forms/submit-adaptive-form-to-workfront-fusion.md)**：Forms as a Cloud Service には、アダプティブフォームを Adobe Workfront に簡単に接続するための標準オプションが用意されています。これにより、Adobe Workfront シナリオにアダプティブフォームを送信するプロセスが簡単になり、アダプティブフォームの送信時に Workfront Fusion シナリオをトリガーできます。

* **[右横書き言語のサポート](/help/forms/supporting-new-language-localization-core-components.md)**：コアコンポーネントに基づいて作成されたアダプティブフォームを、アラビア語、ペルシア語、ウルドゥー語などの右横書き（RTL）言語で表示できるようになりました。RTL 言語は、世界中で 20 億人以上の人々が話しています。RTL 言語のフォームを使用すると、アダプティブフォームのリーチを拡大して、これらの多様なオーディエンスに対応し、RTL マーケットを選択できます。また、特定の地域では、現地の言語でフォームを提供することは法的義務として定められています。現地の言語に対応することで、より幅広いオーディエンスに扉を開くだけでなく、関連する法律や規制を確実に遵守できます。

  ![右横書き言語のサポート](/help/forms/assets/right-to-left-language-support.png)

* **[DocAssurance API（通信 API の一部）を使用したドキュメントの保護](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**：DocAssurance API を使用すると、ドキュメントに署名および暗号化して、機密情報を保護できます。暗号化により、ドキュメントのコンテンツは読み取り不可能な形式に変換され、許可されたユーザーのみがアクセスできるようになります。この強化された保護層は、貴重なデータを信頼できない環境にさらすことなく、安心感ももたらします。Signature API を使用すると、組織は配布および受信する Adobe PDF ドキュメントのセキュリティとプライバシーを保護できます。このサービスでは、デジタル署名と証明書を使用して、意図された受信者のみがドキュメントを変更できるようにします。

  公式メール ID から `aem-forms-ea@adobe.com` に送信して早期導入プログラムに参加し、機能へのアクセスをリクエストできます。

## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### ドメインマッピング早期導入プログラム {#cdn-config-early-adopter}

オプションでライセンス利用可能な Web Application Firewall （WAF）ルールを含む、最近リリースされた [ トラフィックフィルタールール ](/help/security/traffic-filter-rules-including-waf.md) に加えて、設定パイプラインを使用して、他のタイプの CDN 設定を宣言およびデプロイすることもできます。 次のようなユースケースについてお聞かせください。

* 301/302 クライアントサイドのリダイレクト
* 任意の接触チャネルに対するエッジでのリクエストのプロキシ処理
* URL 変換
* リクエストヘッダーまたは応答ヘッダーの設定または変更
* CDN が AEM に到達できない場合のカスタムエラーページ
* ユーザー名/パスワードによる認証
* その他の便利な CDN 設定

公式メール ID からフィードバックを記載したメールを **0}aemcs-cdn-config-adopter@adobe.com} に送信します。**

## Cloud Manager {#cloud-manager}

Cloud Manager の月次リリースの完全なリストは、[こちら](/help/implementing/cloud-manager/release-notes/current.md)で確認できます。

## 移行ツール {#migration-tools}

移行ツールのリリースの完全なリストは、[こちら](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)で確認できます
