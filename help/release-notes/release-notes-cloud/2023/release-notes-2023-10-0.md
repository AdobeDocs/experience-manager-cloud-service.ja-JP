---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.10.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.10.0 リリースのリリースノート。'
exl-id: 81a6cbd2-7101-429b-8572-2650c5bea963
source-git-commit: 559b4afa975dcd2204cd06c95f19ed38da00033e
workflow-type: tm+mt
source-wordcount: '918'
ht-degree: 98%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の 2023.10.0 リリースノート {#release-notes}

以下の節では、[!DNL Experience Manager] as a Cloud Service の 2023.10.0 バージョンの機能リリースノートの概要について説明します。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2021年、2022年）のリリースノートに移動できます。
>
>[!DNL Experience Manager] as a Cloud Service の今後の機能のアクティベーションについての詳細は、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=ja)をご覧ください。

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の最新の機能リリース（2023.10.0）のリリース日は、2023年10月26日（PT）です。次回の機能リリース（2023.11.0）は 2023年11月30日（PT）に予定されています。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

## リリースビデオ {#release-video}

2023.10.0 リリースで追加された機能の概要については、2023年10月リリースの概要ビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3425186/?quality=12)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 新機能 {#assets-features}

**Adobe Express用AEM Assets アドオン**:Experience Manager Assetsには、Adobe Express用のアドオンが用意されるようになりました。 アドオンを使用すると、Adobe Express ユーザーインターフェイス内から Experience Manager Assets に保存されているアセットに直接アクセスできます。AEM Assets で管理されているコンテンツを Express キャンバスに配置し、新しいコンテンツや編集したコンテンツを AEM Assets リポジトリに保存できます。アドオンには、次のような主なメリットがあります。

* AEM での新しいアセットの編集と保存による、コンテンツ再利用の増加

* 新しいアセットの作成や、既存のアセットの新しいバージョンの作成にかかる全体的な時間と労力の削減

  ![Assets アドオンのアセットを含める](/help/assets/assets/aem-assets-add-on-include-assets.png)

### アセットビューの新機能 {#assets-view-features}

* **OneDrive データソースのアセットの一括読み込み**：管理者は、[多数のアセットを OneDrive から AEM Assets に読み込める](/help/assets/bulk-import-assets-view.md#onedrive-developer-application)ようになりました。一括読み込みでサポートされるデータソースの更新リストには、Azure、AWS、Google Cloud、Dropbox、OneDrive が含まれます。

  ![フォルダーにメタデータフォームの割り当て](/help/assets/assets/bulk-import-source-details-onedrive.png)

* **ライブラリに対する組織間の権限付与のサポート**：Experience Manager Assets では、別の IMS 組織の Creative Cloud ライブラリへのアクセスを設定できるようになりました。これにより、Creative Cloud と Experience Manager の間の最新の製品間ワークフローに容易にアクセスできるようになり、クリエイティブの時間と労力を削減できます。

### [!DNL Experience Manager Assets] で利用できるプレリリース機能 {#prerelease-features-assets}

* **Dynamic Media**：[Dynamic Media のビデオに対するマルチサブタイトルとマルチオーディオトラックのサポート](/help/assets/dynamic-media/video.md#about-msma) - プライマリビデオに複数のサブタイトルと複数のオーディオトラックを簡単に追加できるようになりました。この機能により、グローバルなオーディエンスがビデオにアクセスできるようになります。1 つの公開済みプライマリビデオを複数の言語でグローバルオーディエンスに向けてカスタマイズし、様々な地理的地域のアクセシビリティガイドラインに従うことができます。また、作成者は、ユーザーインターフェイスの 1 つのタブからサブタイトルとオーディオトラックを管理することもできます。

  ![選択したビデオアセットのプロパティページの「サブタイトルとオーディオトラック」タブ。](/help/release-notes/assets/msma-aem-cs.png)*選択したビデオアセットのプロパティページの「サブタイトルとオーディオトラック」タブ。*

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### の新機能[!DNL Experience Manager Forms] {#forms-features}

* **[アダプティブフォームのカスタムプロパティ](/help/forms/template-editor-core-components.md#add-a-custom-group-name-in-the-policy-of-template-editor)**：カスタム属性（キーと値のペア）をフォームテンプレートまたはアダプティブフォームコンポーネントに関連付けることで、フォーム開発者がこれらのカスタム属性の値に基づいて適応する、動的なフォーム動作を提供できるようになります。例えば、開発者は、カスタム属性の値に基づいて、モバイル、デスクトップ、web プラットフォーム上にヘッドレスフォームコンポーネントの様々なレンディションを作成できるので、幅広いデバイスでのユーザーエクスペリエンスが大幅に向上します。

* **テーマとテンプレート**：経験豊富な専門家と新しいフォーム作成者の両方を支援するように、新しいテーマとテンプレートをカスタマイズし使用して、フォーム作成プロセスを開始します。アダプティブフォームコアコンポーネントを使用してシームレスに構築され、慎重に厳選されたテーマとテンプレートを使用すると、一般的な使用例に合わせてフォームの作成を迅速に開始できます。

  ![標準テンプレート](/help/forms/assets/form-templates-ootb.png)


### 早期導入プログラム {#forms-early-adopter}

* **[DocAssurance API（通信 API の一部）を使用したドキュメントの保護](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**：DocAssurance API を使用すると、ドキュメントに署名および暗号化して、機密情報を保護できます。暗号化により、ドキュメントのコンテンツは読み取り不可能な形式に変換され、許可されたユーザーのみがアクセスできるようになります。この強化された保護層は、貴重なデータを信頼できない環境にさらすことなく、安心感ももたらします。Signature API を使用すると、組織は配布および受信する Adobe PDF ドキュメントのセキュリティとプライバシーを保護できます。このサービスでは、デジタル署名と証明書を使用して、意図された受信者のみがドキュメントを変更できるようにします。

  公式メール ID から `aem-forms-ea@adobe.com` に送信して早期導入プログラムに参加し、機能へのアクセスをリクエストできます。

## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### WAF ルールを含むトラフィックフィルタールール {#traffic-filter-rules-waf}

URL、IP アドレス、ユーザーエージェントなどのプロパティによって web サイトのトラフィックに一致するルールを宣言することにより、[アドビが管理する CDN でトラフィックをフィルタリング](/help/security/traffic-filter-rules-including-waf.md)したり、DoS 攻撃から保護するためにカスタムのトラフィックレート制限を設定したりできます。また、お客様は、高度な web サイトの脅威に対する追加の保護のために、一連の高度な web アプリケーションファイアウォール（WAF）ルールのライセンスを取得することもできます。

トラフィックフィルタールールに慣れるには、[チュートリアルを試してみること](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/security/traffic-filter-and-waf-rules/overview.html?lang=ja)をお勧めします。新しい Cloud Manager 設定パイプラインの指定、設定ファイルでのルールの宣言、悪意のあるトラフィックの CDN ログの分析に関する手順について説明します。

トラフィックフィルタールールは、現在開発環境で使用でき、11月にステージング環境と実稼動環境へ段階的に展開されます。ステージ上および実稼動環境での事前アクセスを、**aemcs-waf-adopter@adobe.com** にメールでリクエストすることができます。

高度な WAF トラフィックフィルタールールでは、拡張セキュリティまたは WAF-DDoS 保護製品を通じて今年後半にライセンスを取得できるようになります。

## Cloud Manager {#cloud-manager}

Cloud Manager の月次リリースの完全なリストは、[こちら](/help/implementing/cloud-manager/release-notes/current.md)で確認できます。

## 移行ツール {#migration-tools}

移行ツールのリリースの完全なリストは、[こちら](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)で確認できます
