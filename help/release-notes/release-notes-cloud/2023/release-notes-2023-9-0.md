---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.9.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.9.0 リリースのリリースノート。'
exl-id: d747f58b-8d6c-418d-9d2b-ec3ae4b6dc03
feature: Release Information
role: Admin
source-git-commit: bb149cd43158bfd1ceb43b04cc536c8c8291f968
workflow-type: tm+mt
source-wordcount: '1440'
ht-degree: 84%

---


# [!DNL Adobe Experience Manager] as a Cloud Service の 2023.9.0 リリースノート {#release-notes}

以下の節では、[!DNL Experience Manager] as a Cloud Service の 2023.9.0 バージョンの機能リリースノートの概要について説明します。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2021年、2022年）のリリースノートに移動できます。
>
>[!DNL Experience Manager] as a Cloud Service の今後の機能のアクティベーションについての詳細は、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=ja)をご覧ください。

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の最新の機能リリース（2023.9.0）の公開日は 2023年9月28日（PT）です。次回の機能リリース（2023.10.0）は、2023年10月26日（PT）に予定されています。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

## リリースビデオ {#release-video}

2023.9.0 リリースで追加された機能の概要については、2023年9月リリースの概要ビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3424826/?quality=12)

## AEMEdge Delivery Services {#edge-delivery}

Edge Deliveryは、コンテンツの影響を最大化し、お客様とのやり取りの時点で測定可能なビジネス成果を促進することに重点を置いた、構成可能な新しいサービスセットです。

Edge Delivery Servicesについて詳しくは、記事 [&#x200B; こちら &#x200B;](/help/edge/overview.md) を参照してください。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### アセットビューの新機能 {#assets-view-features}

**フォルダーにメタデータフォームの割り当て**

デプロイメント内の特定のフォルダーにメタデータフォームを割り当てることができるようになりました。 サブフォルダー内のアセットを含むフォルダー内のすべてのアセットには、割り当てられたメタデータフォームで定義されたプロパティが表示されます。

![フォルダーにメタデータフォームの割り当て](/help/release-notes/assets/assign-to-folder.png)

### 管理ビューの新機能 {#admin-view-features}

* **AEM Assets as a Cloud ServiceとEdge Delivery Servicesのドキュメントベースのオーサリングの統合**: AEM AssetsとEdge Delivery Servicesのドキュメントベースのオーサリングを統合して、web サイト作成者が [AEM Assets リポジトリで利用可能な画像を使用しながら、Microsoft Word またはGoogle Docsでドキュメントをオーサリング &#x200B;](/help/edge/overview.md) できるようにします。

* **ZIP アーカイブを抽出**:Experience Managerで管理される ZIP アーカイブを選択し、ダウンロードせずに [&#x200B; ファイルをExperience Managerに直接抽出 &#x200B;](/help/assets/manage-digital-assets.md#extract-zip-archives) する機能。

  ![グループ用の項目をピン留め](/help/release-notes/assets/extract-archive.png)

### [!DNL Experience Manager Assets] で利用できるプレリリース機能 {#prerelease-features-assets}

* **Dynamic Media**：[Dynamic Media のビデオに対するマルチキャプションとマルチオーディオトラックのサポート](/help/assets/dynamic-media/video.md#about-msma) - プライマリビデオに複数のキャプションと複数のオーディオトラックを簡単に追加できるようになりました。この機能により、グローバルなオーディエンスがビデオにアクセスできるようになります。1 つの公開済みプライマリビデオを複数の言語でグローバルオーディエンスに向けてカスタマイズし、様々な地理的地域のアクセシビリティガイドラインに従うことができます。また、作成者は、ユーザーインターフェイスの 1 つのタブからキャプションとオーディオトラックを管理することもできます。

  ![選択したビデオアセットのプロパティページの「キャプションとオーディオトラック」タブ。](/help/release-notes/assets/msma-aem-cs.png)*選択したビデオアセットのプロパティページの「キャプションとオーディオトラック」タブ。*

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### の新機能[!DNL Experience Manager Forms] {#forms-features}

* [**Google reCAPTCHA Enterprise のサポート**](/help/forms/captcha-adaptive-forms-core-components.md)：アダプティブフォームで Google reCAPTCHA Enterprise を使用して、不正なアクティビティやスパムに対する保護を強化し、より安全なユーザーエクスペリエンスを提供します。高度なリスク分析とシームレスな統合により、ユーザーはボットを効果的にブロックしながらフォームを簡単に送信できます。

* [**Forms 向けの Experience Cloud 設定自動化機能を備えた Adobe Analytics**](/help/forms/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation.md)：いくつかのボタンをフリップして、Experience Cloud 設定の自動化で Adobe Analytics を有効にできるようになりました。これにより、AEM Forms as a Cloud Service を Experience Platform タグと Adobe Analytics に接続して、公開したフォームのパフォーマンス指標を取得し、追跡できます。

  >[!VIDEO](https://video.tv.adobe.com/v/3424577/enable-adobe-analytics/?quality=12&learn=on)

* [**アダプティブフォームの Adobe Analytics レポートテンプレート**](/help/forms/view-understand-aem-forms-analytics-reports.md)：Forms as a Cloud Service が Adobe Analytics レポート OOTB を提供するようになりました。これにより、フォームのパフォーマンスを簡単に理解できます。フォームレベルの指標を使用すると、レンディション、訪問者、送信、平均記入時間など、複数の主要業績評価指標（KPI）に対するフォームのパフォーマンスに関するインサイトを得ることができます。ユーザーの行動とフィードバックを追跡して、フォームのわかりにくい箇所を特定し、フォームのデザインと機能の改善についてガイドします。

  ![アダプティブフォームのユーザーエンゲージメントの Adobe Analytics レポート](/help/forms/assets/forms-analytics-report.png)

* **[コアコンポーネントに基づくアダプティブフォームのフォームフラグメント](/help/forms/adaptive-form-fragments-core-components.md)**：重複を避け、デジタルインベントリを最適化し、共同作業を強化することで、フォームフラグメントを使用してフォーム構築のエクスペリエンスを向上させます。これらの再利用可能なコンポーネントは複数のフォームにシームレスに統合され、一貫性のあるプロフェッショナルな外観のフォームの作成を効率化します。フォームフラグメントは、「一度変更すればすべてに反映」機能を通じて、再利用性、標準化、ブランドの一貫性を確保します。1 か所で行われた更新が、これらのフラグメントを利用するすべてのフォームに自動反映されるので、メンテナンス性と効率性が向上します。

* **[Adobe Sign ワークフローステップの機能強化](/help/forms/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step)**：Adobe Sign ワークフローステップが強化機能され、次が含まれるようになりました。
   * **Adobe Sign の行政 ID に基づいた認証**：Adobe Acrobat Sign の行政 ID に基づいた認証は、ユーザーが行政発行の ID（運転免許証、国民 ID、パスポート）を使用して身元を認証できるようにすることで、追加の検証レイヤーを提供します。この機能強化により、信頼できる ID ドキュメントを使用することで、署名プロセスの信頼性がさらに高まり、高度なセキュリティ、コンプライアンスおよびユーザー検証を必要とするシナリオに最適になります。

   * **Adobe Sign ドキュメントの監査記録**：監査記録機能を使用すると、Adobe Sign ドキュメントのライフサイクルに関する詳細なインサイトが得られます。監査記録を使用すると、ドキュメントに関連するすべてのアクションとインタラクションの包括的な記録を保持できるようになります。これには、ドキュメントを表示、編集、署名したユーザーなどの詳細と、各イベントのタイムスタンプが含まれます。この機能強化は、コンプライアンスの保持、紛争の解決、デジタル契約の整合性を確保する上で重要です。

   * **契約受信者の役割を署名者以外にも拡張**：Adobe Acrobat Sign には、契約受信者の役割を署名者以外にも拡張して、ワークフロー要件にさらに適合するオプションがあります。有効にすると、契約の各受信者の役割を個別に設定でき、署名者がデフォルトになります。

* **通信 API でのページ数のサポート**：通信 API を使用してドキュメントを取得すると共に、ドキュメント内に含まれるページ数に関する貴重な情報を受け取ることができます。

* **[ルールエディターでのカスタムエラーハンドラーによるエラー処理](/help/forms/add-custom-error-handler-adaptive-forms-core-components.md)**：外部サービスから返されたエラーに応じて、カスタム関数を呼び出し、エンドユーザーに対してカスタマイズされた応答を提供できるようになりました。例えば、特定のエラーコードに対してバックエンドでカスタムワークフローを呼び出したり、サービスが停止していることを顧客に通知したりできます。

* **[64 ビット版のAEM Forms Designer](/help/forms/installing-configuring-designer.md)**: 64 ビット版のAEM Forms Designerでは、パフォーマンス、スケーラビリティ、メモリ管理が向上し、フォーム作成エクスペリエンスが強化されます。 64 ビットアーキテクチャを使用すると、さらに大規模で複雑なプロジェクトに簡単に取り組むことができ、シームレスな設計ワークフローと最適化された効率が保証されます。この最先端のリリースでフォームデザイン機能を強化し、AEM Forms Designer の未来を体現します。

### 早期導入プログラム {#forms-early-adopter}

* **[DocAssurance API（通信 API の一部）を使用したドキュメントの保護](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**：DocAssurance API を使用すると、ドキュメントに署名および暗号化して、機密情報を保護できます。暗号化により、ドキュメントのコンテンツは読み取り不可能な形式に変換され、許可されたユーザーのみがアクセスできるようになります。この強化された保護層は、貴重なデータを信頼できない環境にさらすことなく、安心感ももたらします。Signature API を使用すると、組織は配布および受信する Adobe PDF ドキュメントのセキュリティとプライバシーを保護できます。このサービスでは、デジタル署名と証明書を使用して、意図された受信者のみがドキュメントを変更できるようにします。

  公式メール ID から `aem-forms-ea@adobe.com` に送信して早期導入プログラムに参加し、機能へのアクセスをリクエストできます。

* **[ヘッドレスアダプティブForms](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=ja)**：ヘッドレスアダプティブFormsを使用すると、デベロッパーは、従来のグラフィカルユーザーインターフェイスではなく、API を介してアクセスおよび操作できるインタラクティブフォームを作成、公開、管理できます。 ヘッドレスアダプティブフォームは以下の場合に役立ちます。

   * 高品質のマルチチャネルフォームを好みのプログラミング言語で作成
   * デスクトップおよびモバイルアプリ、web サイト、チャットアプリケーションにフォームをネイティブに統合
   * フォームアプリケーションで独自の UI コンポーネントを再利用
   * Adobe Experience Manager Forms の機能を活用

  ご自身の公式メール ID から `aem-forms-headless@adobe.com` にメールを送信して、早期導入者プログラムにご参加ください。

## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### キャンペーン関連の URL パラメーターの新しい CDN キャッシュ動作 {#cache-url-params}

新規環境の場合、CDN は、マーケティングキャンペーンのパフォーマンスとキャッシュヒット率を高めるために、マーケティング関連のクエリパラメーターをデフォルトで削除します。 既存の環境は影響を受けません。 [詳細情報](/help/implementing/dispatcher/caching.md#marketing-parameters)。

### トラフィックフィルタールール（WAF ルールを含む）早期導入プログラム {#waf-early-adopter}

CDN でのトラフィックのフィルタリング基準：

* リクエストのヘッダーとプロパティ（IP アドレスなど）
* 悪意のあるトラフィックと関連付けられていることがわかっているトラフィックパターン

この機能を試してフィードバックを共有いただける場合早期導入プログラムについて詳しくは、ご自身の公式メール ID から **aemcs-waf-adopter@adobe.com** にメールを送信してください。参加者の数は制限されています。

この機能について詳しくは、[こちら](/help/security/traffic-filter-rules-including-waf.md)の記事を参照してください。

## Cloud Manager {#cloud-manager}

Cloud Manager の月次リリースの完全なリストは、[こちら](/help/implementing/cloud-manager/release-notes/current.md)で確認できます。

## 移行ツール {#migration-tools}

移行ツールのリリースの完全なリストは、[こちら](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)で確認できます
