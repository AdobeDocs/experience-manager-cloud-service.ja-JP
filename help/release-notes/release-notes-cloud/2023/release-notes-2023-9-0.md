---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.9.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.9.0 リリースのリリースノート。'
exl-id: d747f58b-8d6c-418d-9d2b-ec3ae4b6dc03
source-git-commit: 6bb7b2d056d501d83cf227adb239f7f40f87d0ce
workflow-type: tm+mt
source-wordcount: '1442'
ht-degree: 32%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート {#release-notes}

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

のリリース日 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 現在の機能リリース (2023.9.0) は 2023 年 9 月 28 日です。 次回の機能リリース (2023.10.0) は、2023 年 10 月 26 日に予定されています。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

## リリースビデオ {#release-video}

2023.9.0 リリースに追加された機能の概要については、 2023 年 9 月リリースの概要ビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3424826/?quality=12)

## AEMEdge Delivery Services {#edge-delivery}

エッジ配信は、コンテンツの影響を最大限に高め、顧客とのインタラクションの時点でのビジネス成果を測定できるようにする、合成可能な一連の新しいサービスです。

記事のEdge Delivery Servicesの詳細 [ここ](/help/edge/overview.md).

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### アセットビューの新機能 {#assets-view-features}

**フォルダーへのメタデータフォームの割り当て**

これで、デプロイメント内の特定のフォルダーにメタデータフォームを割り当てることができるようになりました。 フォルダー内のすべてのアセット（サブフォルダー内のアセットを含む）には、割り当てられたメタデータフォームで定義されたプロパティが表示されます。

![フォルダーにメタデータフォームを割り当て](/help/release-notes/assets/assign-to-folder.png)

### 管理ビューの新機能 {#admin-view-features}

* **AEM Assetsas a Cloud ServiceとドキュメントベースのオーサリングをEdge Delivery Servicesに統合**: AEM Assetsをドキュメントベースのオーサリングと統合して、Edge Delivery Servicesが Web サイト作成者が [Microsoft Word またはGoogleドキュメントでドキュメントを作成する際に、AEM Assetsリポジトリで使用できる画像を使用します。](/help/edge/using.md#integrate-assets-edge).

* **ZIP アーカイブの抽出**:Experience Managerで管理される ZIP アーカイブおよび [ファイルを直接Experience Managerに抽出](/help/assets/manage-digital-assets.md#extract-zip-archives) ダウンロードせずに

  ![グループ用の項目のピン留め](/help/release-notes/assets/extract-archive.png)

### で使用可能なリリース前機能 [!DNL Experience Manager Assets] {#prerelease-features-assets}

* **Dynamic Media**: [Dynamic Mediaでのビデオのマルチサブタイトルおよびマルチオーディオトラックのサポート](/help/assets/dynamic-media/video.md#about-msma) — プライマリビデオに複数のサブタイトルや複数のオーディオトラックを簡単に追加できるようになりました。 この機能により、グローバルなオーディエンスがビデオにアクセスできるようになります。1 つの公開済みプライマリビデオを複数の言語でグローバルオーディエンスに向けてカスタマイズし、様々な地理的地域のアクセシビリティガイドラインに従うことができます。また、作成者は、ユーザーインターフェイスの 1 つのタブからサブタイトルとオーディオトラックを管理することもできます。

  ![選択したビデオアセットのプロパティページの「サブタイトルとオーディオトラック」タブ。](/help/release-notes/assets/msma-aem-cs.png)*選択したビデオアセットのプロパティページの「サブタイトルとオーディオトラック」タブ。*

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### の新機能[!DNL Experience Manager Forms] {#forms-features}

* [**Google reCAPTCHA エンタープライズサポート**](/help/forms/captcha-adaptive-forms-core-components.md)：アダプティブフォームでGoogle reCAPTCHA Enterprise を使用して、不正なアクティビティやスパムに対する保護を強化し、より安全なユーザーエクスペリエンスを提供します。 高度なリスク分析とシームレスな統合により、本物のユーザーは、ボットを効果的にブロックしながらフォームを簡単に送信できます。

* [**Forms向けのExperience Cloud設定自動化機能を備えたAdobe Analytics**](/help/forms/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation.md)：いくつかのボタンをフリップして、Experience Cloud設定の自動化でAdobe Analyticsを有効にできるようになりました。 これにより、AEM Formsas a Cloud ServiceをExperience PlatformタグとAdobe Analyticsに接続して、発行されたフォームのパフォーマンス指標を取得し、追跡できます。

  >[!VIDEO](https://video.tv.adobe.com/v/3424577/enable-adobe-analytics/?quality=12&learn=on)

* [**Adobe AnalyticsアダプティブFormsのレポートテンプレート**](/help/forms/view-understand-aem-forms-analytics-reports.md):Forms as a Cloud ServiceがAdobe Analyticsレポート OOTB を提供するようになりました。 これにより、フォームのパフォーマンスを簡単に理解できます。フォームレベルの指標を使用すると、レンディション、訪問者、送信、平均記入時間など、複数の主要業績評価指標（KPI）に対するフォームのパフォーマンスに関するインサイトを得ることができます。ユーザーの行動やフィードバックを追跡することで、フォームの混乱の原因となっている領域を特定し、フォームのデザインと機能に関するガイドを改善できます。

  ![アダプティブフォームのユーザーエンゲージメントの Adobe Analytics レポート](/help/forms/assets/forms-analytics-report.png)

* **[コアコンポーネントに基づくアダプティブFormsのフォームフラグメント](/help/forms/adaptive-form-fragments-core-components.md)**：フォームフラグメントを使用してフォーム構築のエクスペリエンスを向上させるため、複製を避け、デジタルインベントリを最適化し、コラボレーションを強化します。 これらの再利用可能なコンポーネントは複数のフォームにシームレスに統合され、一貫性のあるプロフェッショナルな外観のフォームの作成を合理化します。 フォームフラグメントは、「一度変更してすべてに反映」機能を通じて、再利用性、標準化、ブランドの一貫性を確保します。 1 か所でおこなわれた更新が、これらのフラグメントを利用するすべてのフォームに自動的に反映されるので、メンテナンス性と効率性が向上します。

* **[Adobe Sign Workflow ステップの強化](/help/forms/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step)**: Adobe Sign Workflow ステップが拡張され、以下が含まれるようになりました。
   * **Adobe Signの政府機関 ID ベースの認証**:Adobe Acrobat Signの政府 ID ベースの認証では、政府発行の ID（運転免許証、国民 ID、パスポート）を使用してユーザーが ID を認証できるようにすることで、さらに検証レイヤーを提供しています。 この機能強化により、信頼できる ID ドキュメントを使用することで、署名プロセスの信頼性がさらに高まり、高度なセキュリティ、コンプライアンスおよびユーザー検証を必要とするシナリオに最適になります。

   * **Adobe Signドキュメントの監査証跡**：監査記録機能を使用すると、Adobe Signドキュメントのライフサイクルに関する詳細なインサイトを得ることができます。 監査証跡を使用すると、ドキュメントに関連するすべてのアクションとインタラクションの包括的な記録を保持できるようになります。これには、ドキュメントを表示、編集、署名したユーザーなどの詳細と、各イベントのタイムスタンプが含まれます。この機能強化は、コンプライアンスの保持、紛争の解決、デジタル契約の整合性を確保する上で重要です。

   * **署名者以外の契約受信者の新しい役割**:Adobe Acrobat Signには、署名者だけでなく、契約受信者の役割を拡張して、ワークフロー要件をより適切に満たすことができます。 有効にすると、契約の各受信者の役割を個別に設定でき、署名者がデフォルトになります。

* **通信 API でのページ数のサポート**：これで、通信 API を使用してドキュメントを取得すると共に、ドキュメント内に含まれるページ数に関する貴重な情報を受け取ることができます。

* **[ルールエディターでのカスタムエラーハンドラーによるエラー処理](/help/forms/add-custom-error-handler-adaptive-forms-core-components.md)**：外部サービスから返されたエラーに応じてカスタム関数を呼び出し、エンドユーザーに対してカスタマイズされた応答を提供できるようになりました。 例えば、特定のエラーコードに対してバックエンドでカスタムワークフローを呼び出したり、サービスが停止していることを顧客に通知したりできます。

* **[64 ビット版のAEM Forms Designer](/help/forms/installing-configuring-designer.md)**: 64 ビット版のAEM Forms Designer では、パフォーマンス、拡張性、メモリ管理の機能が強化され、フォーム作成エクスペリエンスが強化されます。 64 ビットアーキテクチャを使用すると、より大規模で複雑なプロジェクトに簡単に取り組むことができ、シームレスな設計ワークフローと最適化された効率を確保できます。 フォームデザインの機能を向上させ、この最先端リリースでAEM Forms Designer の将来を受け入れます。

### アーリーアダプタープログラム {#forms-early-adopter}

* **[DocAssurance API（通信 API の一部）を使用してドキュメントをProtect](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**:DocAssurance API を使用すると、ドキュメントに署名し、暗号化することで、機密情報を保護できます。 暗号化を通じて、ドキュメントのコンテンツは読み取り不可能な形式に変換され、許可されたユーザーのみがアクセス権を取得できるようになります。 この防護の強化された層は、不正な目から貴重なデータを守るだけでなく、心の安らぎも提供します。 署名 API を使用すると、組織が配信および受信するAdobe PDFドキュメントのセキュリティとプライバシーを保護できます。 このサービスでは、デジタル署名と証明書を使用して、意図された受信者のみがドキュメントを変更できるようにします。

  次に書き込むことができます： `aem-forms-early-adopter-program@adobe.com` アーリーアダプタープログラムに参加し、機能へのアクセスをリクエストするために、公式の電子メール id から。

* **[ヘッドレスアダプティブForms](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=jp)**：ヘッドレスアダプティブFormsを使用すると、開発者は、従来のグラフィカルユーザーインターフェイスを使用するのではなく、API を使用してアクセスし、操作できるインタラクティブフォームを作成、公開、管理できます。 ヘッドレスアダプティブフォームは以下の場合に役立ちます。

   * 高品質のマルチチャネルフォームを好みのプログラミング言語で作成
   * デスクトップおよびモバイルアプリ、web サイト、チャットアプリケーションにフォームをネイティブに統合
   * フォームアプリケーションで独自の UI コンポーネントを再利用
   * Adobe Experience Manager Forms の機能を活用

  ご自身の公式メール ID から `aem-forms-headless@adobe.com` にメールを送信して、早期導入者プログラムにご参加ください。

## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### キャンペーン関連の URL パラメーターに対する新しい CDN キャッシュ動作 {#cache-url-params}

新しい環境の場合、CDN は、マーケティングキャンペーンのパフォーマンスとキャッシュヒット率を高めるために、デフォルトでマーケティング関連のクエリパラメーターを削除します。 既存の環境は影響を受けません。 [詳細情報。](/help/implementing/dispatcher/caching.md#marketing-parameters)

### トラフィックフィルタルール（WAF ルールを含む）アーリーアダプタプログラム {#waf-early-adopter}

CDN でのトラフィックのフィルタリング基準：

* ヘッダーとプロパティのリクエスト（IP アドレスなど）
* 悪意のあるトラフィックに関連付けられていると知られているトラフィックパターン

この機能を試して、フィードバックを共有したい場合は、 電子メールの送信先 **aemcs-waf-adopter@adobe.com** アーリーアダプタープログラムの詳細については、公式電子メール ID を参照してください。 スペースは制限されています。

この機能の詳細については、この記事を参照してください。 [ここ](/help/security/traffic-filter-rules-including-waf.md).

## Cloud Manager {#cloud-manager}

Cloud Manager の月次リリースの完全なリストは、[こちら](/help/implementing/cloud-manager/release-notes/current.md)で確認できます。

## 移行ツール {#migration-tools}

移行ツールのリリースの完全なリストは、[こちら](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)で確認できます
