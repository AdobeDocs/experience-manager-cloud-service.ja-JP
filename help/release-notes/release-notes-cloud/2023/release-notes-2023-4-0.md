---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.4.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.4.0 リリースのリリースノート。'
exl-id: c34aedee-e45a-4e2a-ae7f-930bc0cc026f
feature: Release Information
role: Admin
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 100%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の 2023.4.0 リリースノート {#release-notes}

以下の節では、[!DNL Experience Manager] as a Cloud Service の 2023.4.0 バージョンの機能リリースノートの概要について説明します。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2021年、2022年）のリリースノートに移動できます。
>
>[!DNL Experience Manager] as a Cloud Service の今後の機能のアクティベーションについての詳細は、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=ja)をご覧ください。

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の最新の機能リリース（2023.4.0）のリリース日は 2023年6月7日です。次回の機能リリース（2023.6.0）は 2023年6月29日（PT）に予定されています。

## リリースビデオ {#release-video}

2023.4.0 リリースで追加された機能の概要については、2023年4月リリースの概要ビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3418681/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### の新機能[!DNL Experience Manager Sites] {#sites-features}

* AEM as a Cloud Service からコンテンツフラグメントを Adobe Target に JSON 形式で書き出し、Target で対応する JSON オファーを作成します。
* 複雑な GraphQL のクエリとフィルターを使用して大きなコンテンツセットを AEM から取得する際、GraphQL のページネーションと並べ替えのサポートに加え、内部キャッシュの強化によって、切り離されたクライアントアプリケーションのパフォーマンスの向上を支援するようになりました。

### [!DNL Experience Manager Sites] プレリリースの新機能 {#prerelease-sites}

* コンテンツフラグメントとその参照を、[コンテンツフラグメントコンソール](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html?lang=ja)を使用して [AEM プレビューサービス](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments.html?lang=ja#access-preview-service) に公開できるようになりました。これにより、ユーザーは実稼働環境に移行する前に、切り離されたプレビューアプリケーションで最終的なエクスペリエンスをプレビューできます。
* AEM GraphQL を使用したヘッドレスシナリオで、web 配信用に画像を動的に最適化できるようになりました。GraphQL クエリで[クエリ変数](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/images.html?lang=ja#query-variables)を定義できるようになり、切り離されたクライアントアプリケーションが、適切に最適化された画像を AEM からリクエストできるようになりました。
* [コンテンツフラグメントのバリエーション](https://experienceleague.adobe.com/docs/experience-manager-65/assets/content-fragments/content-fragments-variations.html?lang=ja)のタグを、AEM GraphQL コンテンツ配信 API を使用して JSON に出力できるようになりました。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### の新機能[!DNL Assets] {#assets-features}

* メタデータの自動抽出、サムネールおよびカスタムレンディションの生成を行う WebP 画像のサポートが追加されました。これらのファイルで、スマートタグ機能もサポートされるようになりました。Dynamic Media 機能は、WebP では入力形式としてサポートされていません。

* [検索エクスペリエンスの強化](/help/assets/search-assets.md#aftersearch) - 検索結果に表示されるアセットに対して、次の操作を素早く実行できるようになりました。

   * ワークフローの作成
   * バージョンを作成
   * アセットの関連付けまたは関連付けを解除

     これらの操作を実行する場合、アセットの場所に移動してアセットのプロパティを表示する必要はありません。

* カラー検索ファセットのユーザビリティの改善 - カラー値の入力フィールドが編集可能になり、カラーピッカーを終了した場合にのみ検索結果が更新されるようになりました。

* CMAF が有効な Dynamic Media ビデオ配信で、アダプティブストリーミングをサポートする新しいプロトコル（DASH - HTTP での動的アダプティブストリーミング）が開始しました。
   * アダプティブストリーミング（DASH／HLS）により、ユーザーがビデオを視聴する際の操作性が向上します
   * DASH はアダプティブビデオストリーミング用の国際標準プロトコルで、業界で広く採用されています
   * すべての地域で利用可能で、サポートチケットを通じて有効になります。

* Dynamic Media _スナップショット_ - テスト画像や Dynamic Media の URL を試して、様々な画像修飾子の出力を確認したり、ファイルサイズ（WebP および AVIF 配信による）、ネットワーク帯域幅、デバイスのピクセル比を最適化するスマートイメージングを評価します。詳しくは、[Dynamic Media スナップショット](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot.html?lang=ja)を参照してください。

### [!DNL Assets] プレリリースの機能 {#prerelease-feature-assets}

* Dynamic Media - 画像プロファイルのスマート切り抜き関連のフィールドの一部でユーザーインターフェイスが更新され、スマート切り抜きを定義するための最新のガイドラインが反映されました。詳しくは、[切り抜きオプション](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles.html?lang=ja#crop-options)を参照してください。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] で利用できる新機能 {#new-features-available-in-channel}

* **[Microsoft® SharePoint と Microsoft® OneDrive にアダプティブフォームを送信](/help/forms/configuring-submit-actions.md)**：ビジネスユーザーの俊敏性を向上させ、新しいフォームをすばやく起動し、送信されたデータを Microsoft® SharePoint サイトや OneDrive フォルダーなどの毎日使用するツールに保存します。

### [!DNL Forms] の機能プレリリース {#prerelease-features-forms}

* [AEM ページエディター内のアダプティブフォーム](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)：AEM ページエディターを使用して、複数のフォームをすばやく作成し、Sites ページに追加できるようになりました。この機能を使用すると、コンテンツ作成者は、動的な動作、検証、データ統合、レコードのドキュメントの生成、ビジネスプロセスの自動化など、アダプティブフォームコンポーネントの機能を利用して、Sites ページ内にシームレスなデータキャプチャエクスペリエンスを作成できます。以下の操作を実行できます。

   * フォームコンポーネントを AEM サイトエディターまたはエクスペリエンスフラグメントのアダプティブフォームコンテナコンポーネントにドラッグ＆ドロップして、アダプティブフォームを作成します。
   * AEM サイトエディター内でアダプティブフォームウィザードを使用すると、任意の Sites ページとは独立したフォームを作成して、自由に複数のページでそのフォームを再利用できます。
   * 複数のフォームを Sites ページに追加し、ユーザーエクスペリエンスを合理化し、柔軟性を高めます。

     >[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

* [Adobe Acrobat Sign Solutions for Government](/help/forms/adobe-sign-integration-adaptive-forms.md)：AEM Forms が、Adobe Acrobat Sign Solutions for Government と統合されました。この統合により、政府関連のアカウント（政府機関および機関）に対するアダプティブフォーム送信による電子サインに、高度なコンプライアンスとセキュリティを提供します。

  Adobe Acrobat Sign for Government との統合により、アドビのパートナーや政府のお客様はアダプティブフォームで、最もミッションクリティカルで機密性の高い業務の一部に電子サインを使用できるようになります。このセキュリティの強化により、すべての電子サインが FedRAMP Moderate コンプライアンスに完全に準拠し、アドビの政府機関のお客様に安心感を提供します。

* ルールエディターのカスタムエラーハンドラーによるエラー処理の強化：外部サービスから返されたエラーへの応答で（クライアントライブラリを使用して）カスタム関数を呼び出し、エンドユーザーに対してカスタマイズされた応答を提供できるようになりました。または、サービスから返されたエラーに対して特定のアクションを実行できます。例えば、特定のエラーコードに対してバックエンドでカスタムワークフローを呼び出したり、サービスが停止していることを顧客に通知したりできます。

  この機能は、OOTB エラーハンドラーとの下位互換性のある標準ベースのエラー応答を導入し、柔軟性と制御性を高め、全体的なエラー処理機能を改善するのに役立ちます。

### ヘッドレスアダプティブフォーム早期導入者プログラム {#forms-early-adopter}

ヘッドレスアダプティブフォームを使用すると、開発者は、従来のグラフィカルユーザーインターフェイスではなく、API を介してアクセスおよび操作できるインタラクティブなフォームを作成、公開、管理できます。ヘッドレスアダプティブフォームは以下の場合に役立ちます。

* 高品質のマルチチャネルフォームを好みのプログラミング言語で作成
* デスクトップおよびモバイルアプリ、web サイト、チャットアプリケーションにフォームをネイティブに統合
* フォームアプリケーションで独自の UI コンポーネントを再利用
* Adobe Experience Manager Forms の機能を活用

ご自身の公式メール ID から `aem-forms-headless@adobe.com` にメールを送信して、早期導入者プログラムにご参加ください。

## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### 新機能 {#what-is-new-foundation}

* 追加の公開地域：Sites のお客様は、プライマリ地域に加えて、最大 3 つの公開地域のライセンスを取得できます。トラフィックは追加の公開ファームにルーティングされるので、特定のリクエストの待ち時間が短縮され、地域単位の停止に対する回復力が向上します。ご自身のプログラム用の[追加の公開地域](/help/operations/additional-publish-regions.md)のライセンスについて詳しくは、アドビのアカウントマネージャーにお問い合わせください。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

## Cloud Manager {#cloud-manager}

Cloud Manager の月次リリースの完全なリストは、[こちら](/help/implementing/cloud-manager/release-notes/current.md)で確認できます。

## 移行ツール {#migration-tools}

移行ツールのリリースの完全なリストは、[こちら](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)で確認できます
