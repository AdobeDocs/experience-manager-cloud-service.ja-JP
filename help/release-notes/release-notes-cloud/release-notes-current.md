---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: f1af229fa0fb75a6181eae545ac7e51b31f212f7
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 27%

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

のリリース日 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 現在の機能リリース (2023.10.0) は 2023 年 10 月 26 日です。 次回の機能リリース (2023.11.0) は、2023 年 11 月 30 日に予定されています。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

## リリースビデオ {#release-video}

2023.10.0 リリースで追加された機能の概要については、2023年10月リリースの概要ビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3425186/?quality=12)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 新機能 {#assets-features}

**Adobe Express用AEM Assetsアドオン**:Experience Manager Assetsは、 [Adobe Express用アドオン](/help/assets/addon-adobe-express.md). アドオンを使用すると、Experience Manager Assetsのユーザーインターフェイス内から直接に保存されているAdobe Expressにアクセスできます。 AEM Assetsで管理するコンテンツを Express キャンバスに配置し、新しいコンテンツや編集したコンテンツをAEM Assetsリポジトリに保存できます。 このアドオンには、次の主なメリットがあります。

* AEMでの新しいアセットの編集と保存によるコンテンツの再利用の向上

* 新しいアセットを作成したり、既存のアセットの新しいバージョンを作成したりする際の全体的な時間と労力を削減

  ![Assets アドオンのアセットを含める](/help/assets/assets/aem-assets-add-on-include-assets.png)

### アセットビューの新機能 {#assets-view-features}

* **OneDrive データソースからのアセットの一括読み込み**：管理者は、次の操作を実行できるようになりました。 [多数のアセットを OneDrive からAEM Assetsに読み込む](/help/assets/bulk-import-assets-view.md#onedrive-developer-application). 一括インポートでサポートされるデータソースの更新リストには、Azure、AWS、Google Cloud、Dropbox、OneDrive が含まれます。

  ![フォルダーにメタデータフォームを割り当て](/help/assets/assets/bulk-import-source-details-onedrive.png)

* **組織間のライブラリの権限付与のサポート**:Experience Manager Assetsで、別の IMS 組織のCreative Cloudライブラリへのアクセスを設定できるようになりました。 これにより、Creative CloudとExperience Managerの間の最新のクロス製品ワークフローに容易にアクセスでき、クリエイティブの時間と労力を削減できます。

### で使用可能なリリース前機能 [!DNL Experience Manager Assets] {#prerelease-features-assets}

* **Dynamic Media**: [Dynamic Mediaでのビデオのマルチサブタイトルおよびマルチオーディオトラックのサポート](/help/assets/dynamic-media/video.md#about-msma) — プライマリビデオに複数のサブタイトルや複数のオーディオトラックを簡単に追加できるようになりました。 この機能により、グローバルなオーディエンスがビデオにアクセスできるようになります。1 つの公開済みプライマリビデオを複数の言語でグローバルオーディエンスに向けてカスタマイズし、様々な地理的地域のアクセシビリティガイドラインに従うことができます。また、作成者は、ユーザーインターフェイスの 1 つのタブからサブタイトルとオーディオトラックを管理することもできます。

  ![選択したビデオアセットのプロパティページの「サブタイトルとオーディオトラック」タブ。](/help/release-notes/assets/msma-aem-cs.png)*選択したビデオアセットのプロパティページの「サブタイトルとオーディオトラック」タブ。*

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### の新機能[!DNL Experience Manager Forms] {#forms-features}

* **[アダプティブFormsのカスタムプロパティ](/help/forms/template-editor-core-components.md#add-a-custom-group-name-in-the-policy-of-template-editor)**：カスタム属性（キーと値のペア）をフォームテンプレートまたはアダプティブフォームコンポーネントに関連付けることで、フォーム開発者は、これらのカスタム属性の値に基づいて適応する動的なフォーム動作を配信できます。 例えば、開発者は、カスタム属性の値に基づいて、モバイル、デスクトップ、Web プラットフォーム上にヘッドレスFormsコンポーネントの様々なレンディションを作成でき、様々なデバイスでのユーザーエクスペリエンスを大幅に強化できます。

* **テーマとテンプレート**：経験豊富な専門家と新しいフォーム作成者の両方に力を貸すようにカスタマイズされた新しいテーマとテンプレートを使用して、フォーム作成プロセスを開始します。 アダプティブFormsのコアコンポーネントを使用してシームレスに構築され、細心の注意を払って厳選されたテーマとテンプレートを使用すれば、一般的な使用例に合わせてすばやくフォームの作成を開始できます。

  ![標準テンプレート](/help/forms/assets/form-templates-ootb.png)


### アーリーアダプタープログラム {#forms-early-adopter}

* **[DocAssurance API（通信 API の一部）を使用してドキュメントをProtect](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**:DocAssurance API を使用すると、ドキュメントに署名し、暗号化することで、機密情報を保護できます。 暗号化を通じて、ドキュメントのコンテンツは読み取り不可能な形式に変換され、許可されたユーザーのみがアクセス権を取得できるようになります。 この防護の強化された層は、不正な目から貴重なデータを守るだけでなく、心の安らぎも提供します。 署名 API を使用すると、組織が配信および受信するAdobe PDFドキュメントのセキュリティとプライバシーを保護できます。 このサービスでは、デジタル署名と証明書を使用して、意図された受信者のみがドキュメントを変更できるようにします。

  次に書き込むことができます： `aem-forms-early-adopter-program@adobe.com` アーリーアダプタープログラムに参加し、機能へのアクセスをリクエストするために、公式の電子メール id から。

## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### WAF を含むトラフィックフィルタールール {#traffic-filter-rules-waf}

[Adobe管理 CDN でのトラフィックのフィルタリング](/help/security/traffic-filter-rules-including-waf.md) url、IP アドレス、ユーザーエージェントなどのプロパティで web サイトトラフィックに一致するルールを宣言するか、DoS 攻撃を防ぐためにカスタムトラフィックレート制限を設定します。 また、高度な Web サイトの脅威に対する保護を強化するための、一連の高度な Web Application Firewall(WAF;Advanced Web Application Firewall) ルールのライセンスを取得することもできます。

トラフィックフィルタールールについて、 [チュートリアルを試す](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/security/traffic-filter-and-waf-rules/overview.html)! 新しい Cloud Manager 設定パイプラインの設定、設定ファイルでのルールの宣言、悪意のあるトラフィックの CDN ログの分析に関する手順を説明します。

トラフィックフィルタールールは、11 月にステージング環境と実稼動環境への段階的なロールアウトを含む、開発環境で使用できるようになりました。 ステージ上および実稼動環境での事前アクセスを電子メールで要求することができます **aemcs-waf-adopter@adobe.com**.

高度な WAF トラフィックフィルタールールは、今年後半に、拡張セキュリティまたは WAF-DoS 保護サービスを通じてライセンスを受けることができます。

## Cloud Manager {#cloud-manager}

Cloud Manager の月次リリースの完全なリストは、[こちら](/help/implementing/cloud-manager/release-notes/current.md)で確認できます。

## 移行ツール {#migration-tools}

移行ツールのリリースの完全なリストは、[こちら](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)で確認できます
