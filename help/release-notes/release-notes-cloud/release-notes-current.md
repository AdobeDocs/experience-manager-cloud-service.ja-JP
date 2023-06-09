---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: 3209b3098544275bd31ee19842bef0eb2e7a29d8
workflow-type: tm+mt
source-wordcount: '1049'
ht-degree: 39%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート  {#release-notes}

以下のセクションでは、[!DNL Experience Manager] as a Cloud Service の現在（最新）のバージョンの機能リリースノートの概要について説明します。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2021年、2022年のバージョンなど）のリリースノートに移動できます。
>
>[!DNL Experience Manager] as a Cloud Service の今後の機能のアクティベーションについての詳細は、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=ja)をご覧ください。

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

のリリース日 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 現在の機能リリース (2023.4.0) は 2023 年 6 月 8 日です。 次回の機能リリース (2023.6.0) は、2023 年 6 月 30 日に予定されています。

## リリースビデオ {#release-video}

2023.4.0 リリースに追加された機能の概要については、 2023 年 4 月リリースの概要ビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3418681/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### の新機能[!DNL Experience Manager Sites] {#sites-features}

* AEM as a Cloud Service からコンテンツフラグメントを JSON オファーとして Adobe Target に書き出します。
* 複雑な GraphQL のクエリとフィルターを使用して大きなコンテンツセットを AEM から取得する際、GraphQL のページネーションと並べ替えのサポートに加え、内部キャッシュの強化によって、切り離されたクライアントアプリケーションのパフォーマンスの向上を支援するようになりました。

### の新機能 [!DNL Experience Manager Sites] 予約 {#prerelease-sites}

* コンテンツフラグメントとその参照を [AEM Preview Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments.html?lang=en#access-preview-service) の使用 [コンテンツフラグメントコンソール](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html?lang=en)を使用すると、ユーザーは、運用を開始する前に、切り離されたプレビューアプリケーションで最終的なエクスペリエンスをプレビューできます。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### の新機能[!DNL Assets] {#assets-features}

* メタデータの自動抽出、サムネールおよびカスタムレンディションの生成を行う WebP 画像のサポートが追加されました。これらのファイルでスマートタグ機能もサポートされるようになりました。 Dynamic Media機能は、WebP で入力形式としてサポートされていません。

* [検索エクスペリエンスの強化](/help/assets/search-assets.md#aftersearch)  — 検索結果に表示されるアセットに対して、次の操作をすばやく実行できるようになりました。

   * ワークフローの作成
   * 新しいバージョンを作成
   * アセットの関連付けまたは関連付け解除

     これらの操作を実行する場合、アセットの場所に移動してアセットのプロパティを表示する必要はありません。

* カラー検索ファセットのユーザビリティの改善 — カラー値の入力フィールドが編集可能になり、カラーピッカーを終了した場合にのみ検索結果が更新されるようになりました。

* Dynamic Media ビデオ配信でアダプティブストリーミング用に開始された新しいプロトコル（DASH - Dynamic Adaptive Streaming over HTTP）のサポート（CMAF を有効にした場合）:
   * アダプティブストリーミング（DASH／HLS）により、エンドユーザーがビデオを視聴する際の操作性が向上します
   * DASH はアダプティブビデオストリーミング用の国際標準プロトコルで、業界で広く採用されています
   * すべての地域で利用可能で、サポートチケットを介して有効にできます。

* Dynamic Media _スナップショット_  — テスト画像やDynamic Media URL を試して、様々な画像修飾子の出力を確認し、スマートイメージングを最適化してファイルサイズ（WebP および AVIF 配信を使用）、ネットワーク帯域幅、デバイスピクセル比を確認します。 詳しくは、 [Dynamic Media Snapshot](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot.html).

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] で利用できる新機能 {#new-features-available-in-channel}

* **[Microsoft SharePoint と Microsoft OneDrive にアダプティブフォームを送信](/help/forms/configuring-submit-actions.md)**：ビジネスユーザーの俊敏性を向上させ、新しいフォームを素早く起動し、送信されたデータを Microsoft SharePoint サイトや OneDrive フォルダーなどの毎日使用するツールに保存します。

### [!DNL Forms] の機能プレリリース {#prerelease-features-forms}

* [AEM Page Editor 内のアダプティブForms](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md):AEMページエディターを使用して、複数のフォームをすばやく作成し、サイトページに追加できるようになりました。 この機能を使用すると、コンテンツ作成者は、動的な動作、検証、データ統合、レコードのドキュメントの生成、ビジネスプロセスの自動化など、アダプティブフォームコンポーネントの機能を利用して、Sites ページ内にシームレスなデータ取得エクスペリエンスを作成できます。 以下の操作を実行できます。

   * フォームコンポーネントをAEM SitesエディターまたはエクスペリエンスフラグメントのアダプティブFormsコンテナコンポーネントにドラッグ&amp;ドロップして、アダプティブフォームを作成します。
   * AEM Sitesエディター内でアダプティブFormsウィザードを使用すると、任意のサイトページとは独立したフォームを作成でき、複数のページで自由にそのようなフォームを再利用できます。
   * 複数のフォームを Sites ページに追加し、ユーザーエクスペリエンスを合理化し、より柔軟に提供します。

     >[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

* [Adobe Acrobat Signの統合とコンプライアンスの強化](/help/forms/adobe-sign-integration-adaptive-forms.md):AEM Formsは、Adobe Acrobat Sign for Government と統合され、e-Signatures の高度なレベルのコンプライアンスとセキュリティを、政府関連のアカウント（政府機関や機関）に対するアダプティブフォーム送信と共に提供するようになりました。

  Adobe Acrobat Sign for Government との統合により、パートナーや政府のお客様は、最もミッションクリティカルで機密性の高い業務の一部に対して、Adaptive Formsで電子署名を使用できます。 このセキュリティの追加層により、すべての電子署名が FedRAMP Moderate コンプライアンスに完全に準拠し、政府のお客様に安心を提供します。

* ルールエディターのカスタムエラーハンドラーによるエラー処理の強化：外部サービスから返されたエラーに応じて（クライアントライブラリを使用して）カスタム関数を呼び出し、エンドユーザーに合わせて応答を提供したり、サービスから返されたエラーに対して特定のアクションを実行したりできるようになりました。 例えば、特定のエラーコードに対してバックエンドでカスタムワークフローを呼び出したり、サービスが停止していることを顧客に通知したりできます。

  これにより、OOTB エラーハンドラとの下位互換性を持つ標準ベースのエラー応答を導入し、柔軟性と制御性を高め、全体的なエラー処理機能を改善できます。

### ヘッドレスアダプティブフォーム早期導入者プログラム {#forms-early-adopter}

ヘッドレスアダプティブフォームを使用すると、開発者は、従来のグラフィカルユーザーインターフェイスではなく、API を介してアクセスおよび操作できるインタラクティブなフォームを作成、公開、管理できます。ヘッドレスアダプティブフォームは以下の場合に役立ちます。

* 高品質のマルチチャネルフォームを好みのプログラミング言語で作成
* デスクトップおよびモバイルアプリ、web サイト、チャットアプリケーションにフォームをネイティブに統合
* フォームアプリケーションで独自の UI コンポーネントを再利用
* Adobe Experience Manager Forms の機能を活用

メールを `aem-forms-headless@adobe.com` アーリーアダプタープログラムに参加するための公式電子メール ID から

## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### 新機能 {#what-is-new-foundation}

* その他の公開地域：Sites のお客様は、主要地域に加えて、最大 3 つのパブリッシュ地域のライセンスを取得できます。 トラフィックは追加の公開ファームにルーティングされ、特定のリクエストの遅延が短縮され、地域の停止に対する耐障害性が向上します。 ライセンスについて詳しくは、Adobeのアカウントマネージャーにお問い合わせください [その他の公開地域](/help/operations/additional-publish-regions.md) プログラムの

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

## Cloud Manager {#cloud-manager}

Cloud Manager の月次リリースの完全なリストは、 [こちら](/help/implementing/cloud-manager/release-notes/current.md)で確認できます。

## 移行ツール {#migration-tools}

移行ツールのリリースの完全なリストは、[こちら](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)で確認できます
