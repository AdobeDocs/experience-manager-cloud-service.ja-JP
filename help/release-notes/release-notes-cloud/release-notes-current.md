---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: a5121436b2e48302fcf14478764aede1495e089c
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 24%

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

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の最新の機能リリース（2023.12.0）のリリース日は 2023年12月14日です。次回の機能リリース（2024.1.0）は 2023年1月25日（PT）に予定されています。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

<!-- 

## Release Video {#release-video}

Have a look at the December 2023 Release Overview video for a summary of the features added in the 2023.12.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3425864?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### アーリーアダプタープログラム {#sites-early-adopter}

**次の条件を満たす場合に、 [Real User Monitoring(RUM) データ・サービス](/help/implementing/cloud-manager/content-requests.md#real-user-monitoring-for-aem-as-a-cloud-service)** AEMas a Cloud Serviceのクライアント側のコレクションを有効にする

Real User Monitoring(RUM) データサービスは、ユーザーの操作をより正確に反映し、Web サイトのエンゲージメントを確実に測定できます。 これは、ページのパフォーマンスに関する高度なインサイトを得る絶好の機会です。 これは、Adobe管理 CDN またはAdobe管理以外の CDN のどちらを使用する場合にも便利です。 さらに、Adobeが管理していない CDN を使用するお客様の場合、自動トラフィックレポートをAdobeに対して有効にできるので、との間でトラフィックレポートを共有する必要がなくなりました。

この新機能のテストとフィードバックの共有に関心がある場合は、に電子メールを送信してください。 `aemcs-rum-adopter@adobe.com`Adobe IDに関連付けられた電子メールアドレスから、実稼動、ステージ、開発環境のドメイン名と共に入力します。 Adobeの製品チームが Real User Monitoring(RUM) データサービスを有効にします。


<!--

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### New Features in Admin View {#admin-view-features}



* **Smart tags blocklist**: Experience Manager Assets now enables you to define a list of blocked tags. These tags are automatically removed from the auto-generated smart tags when you upload assets to the repository. This capability performs tags governance and saves a lot of time as you can add a tag to the block list and AEM Assets automatically excludes it from the list of tags for any of the assets that are added to the repository.

  ![storage usage insights](/help/assets/assets/block-tags.png)


**Video Preview**: AEM Assets now generates preview renditions of all supported video formats by default, without the need to configure a processing profile.

-->

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### の新機能 [!DNL Experience Manager Forms] {#forms-features}

* **[Microsoft® SharePointリストとのアダプティブFormsの接続](/help/forms/configure-submit-actions-core-components.md#submit-to-sharepoint)**:AEM Formsは、フォームデータを直接SharePointリストに送信するための OOTB 統合機能を備えており、SharePointのリスト機能を使用できます。 Microsoft SharePoint List をフォームデータモデルのデータソースとして設定し、 **フォームデータモデルを使用して送信** アダプティブフォームをSharePointリストに接続するための送信アクション。

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### アーリーアダプタープログラム {#forms-early-adopter}

* **[アダプティブフォームをAdobe Workfront Fusion に送信するシナリオ](/help/forms/submit-adaptive-form-to-workfront-fusion.md)**:Forms as a Cloud Serviceには、アダプティブフォームをAdobe Workfrontに簡単に接続するための既製のオプションが用意されています。 これにより、アダプティブフォームをAdobe Workfrontシナリオに送信するプロセスが簡単になり、アダプティブフォームの送信時にWorkfront Fusion シナリオをトリガーできます。

* **[右から左への言語のサポート](/help/forms/supporting-new-language-localization-core-components.md)**：コアコンポーネントに基づいて構築されたアダプティブFormsは、アラビア語、ペルシャ語、ウルドゥー語などの右から左 (RTL) 言語で表示できるようになりました。 RTL 言語は世界で 20 億人以上の人々が話しています RTL 言語のフォームを使用すると、アダプティブフォームのリーチを拡大して、これらの多様なオーディエンスに対応し、RTL 市場へと選択することができます。 地域によっては、現地の言語でフォームを提供することが法的義務でもあります。 現地の言語に対応することで、より広いオーディエンスへの扉を開くだけでなく、関連する法令への準拠も確保できます。

  ![右から左への言語サポート](/help/forms/assets/right-to-left-language-support.png)

* **[DocAssurance API（通信 API の一部）を使用してドキュメントをProtect](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**:DocAssurance API を使用すると、ドキュメントに署名し、暗号化することで、機密情報を保護できます。 暗号化を通じて、ドキュメントのコンテンツは読み取り不可能な形式に変換され、許可されたユーザーのみがアクセス権を取得できるようになります。 この防護の強化された層は、不正な目から貴重なデータを守るだけでなく、心の安らぎも提供します。 Signature API を使用すると、組織は配布および受信する Adobe PDF ドキュメントのセキュリティとプライバシーを保護できます。このサービスでは、電子署名と証明書を使用して、意図された受信者のみがドキュメントを変更できるようにします。

  次に書き込むことができます： `aem-forms-early-adopter-program@adobe.com` アーリーアダプタープログラムに参加し、機能へのアクセスをリクエストするために、公式の電子メール id から。

## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### CDN 設定アーリーアダプタープログラム {#cdn-config-early-adopter}

最近リリースされたに加えて [トラフィックフィルタールール](/help/security/traffic-filter-rules-including-waf.md)( オプションでライセンス可能な Web アプリケーションファイアウォール (WAF) ルールを含む )、設定パイプラインを使用して他のタイプの CDN 設定を宣言し、デプロイする機会があります。 以下を含め、お客様の使用例についてお知らせします。
* 301/302クライアントサイドのリダイレクト
* エッジでのリクエストの任意のオリジンへのプロキシ処理
* URL 変換
* 要求または応答ヘッダーの設定または変更
* CDN がAEMに到達できない場合のカスタムエラーページ
* ユーザー名/パスワードによる認証
* その他の役に立つ CDN 設定

電子メールの送信先 **aemcs-cdn-config-adopter@adobe.com** を公式の電子メール ID から取得し、フィードバックを入力します。

## Cloud Manager {#cloud-manager}

Cloud Manager の月次リリースの完全なリストは、[こちら](/help/implementing/cloud-manager/release-notes/current.md)で確認できます。

## 移行ツール {#migration-tools}

移行ツールのリリースの完全なリストは、[こちら](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)で確認できます
