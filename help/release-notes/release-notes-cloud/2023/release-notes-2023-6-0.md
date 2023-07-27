---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.6.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.6.0 リリースのリリースノート。'
source-git-commit: 2d10d03e478bff5a162c620c41ceac38a6d7911a
workflow-type: tm+mt
source-wordcount: '1409'
ht-degree: 16%

---


# [!DNL Adobe Experience Manager] as a Cloud Service の 2023.6.0 リリースノート {#release-notes}

以下の節では、[!DNL Experience Manager] as a Cloud Service の 2023.6.0 バージョンの機能リリースノートの概要について説明します。

>[!NOTE]
>
>ここから、2021 年や 2022 年など、以前のバージョンのリリースノートに移動できます。
>
>[!DNL Experience Manager] as a Cloud Service の今後の機能のアクティベーションについての詳細は、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=ja)をご覧ください。

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

のリリース日 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 現在の機能リリース (2023.6.0) は 2023 年 6 月 30 日です。 次の機能リリース (2023.7.0) は、2023 年 7 月 27 日に予定されています。

## リリースビデオ {#release-video}

2023.6.0 リリースで追加された機能の概要については、2023年6月リリースの概要ビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3420971/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### の新機能[!DNL Experience Manager Sites] {#sites-features}

* コンテンツフラグメントとその参照を [AEM Preview Service](/help/implementing/cloud-manager/manage-environments.md#access-preview-service) の使用 [コンテンツフラグメントコンソール](/help/sites-cloud/administering/content-fragments/content-fragments-console.md)を使用すると、ユーザーは、運用を開始する前に、切り離されたプレビューアプリケーションで最終的なエクスペリエンスをプレビューできます。

![コンテンツフラグメントコンソールでプレビュー](/help/assets/content-fragments-console-preview.png)

* AEM GraphQLを使用したヘッドレスシナリオで、Web 配信用に画像を動的に最適化できるようになりました。 [クエリ変数](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/images.html?lang=en#query-variables) は、GraphQLクエリで定義でき、クライアントアプリケーションがAEMから適切に最適化された画像をリクエストする際に、それに応じて切り離すことができます。
* タグの適用先 [コンテンツフラグメントのバリエーション](https://experienceleague.adobe.com/docs/experience-manager-65/assets/content-fragments/content-fragments-variations.html?lang=en) AEM GraphQLコンテンツ配信 API を使用して JSON に出力できるようになりました。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### の新機能[!DNL Assets] {#assets-features}

**新しいアセットビューの可用性**

The [新しいアセットビュー](/help/assets/assets-view-introduction.md) は、Experience Manager Assetsで使用できるようになりました。 Assets ビューにはシンプルなユーザーインターフェイスが用意されており、デジタルアセットの管理、検出、配布が容易になります。 このエクスペリエンスの対象は、クリエイティブ、読み取り専用のアセット消費者、より軽量な DAM ユーザーです。

![タグ管理](/help/assets/assets/my-workspace.png)

**検索エクスペリエンスの強化**

Experience Manager Assetsを使用すると、検索結果のユーザーインターフェイスからさらに多くの作業をおこなうことができます。次の操作が可能になりました。

* [現在のリポジトリの場所内で検索を実行します](/help/assets/search-assets.md) デフォルトでは、リポジトリ全体でキーワードを検索する代わりに使用されます。

* [フォルダーの場所に移動します。](/help/assets/search-assets.md#aftersearch) 検索結果に表示されるアセットの場合。

**3D アセットのサムネールプレビュー**

[!DNL Experience Manager Assets] が生成されました [一般的な 3D ファイル形式のサムネールプレビュー](/help/assets/file-format-support.md) gLB、USDz、FBX、3DS、OBJ、SBSAR を含みます。 これらのファイルがアップロードされると、デフォルトでサムネールが自動的に生成されます。

**リンク共有設定**

の新しい改善されたユーザーエクスペリエンス [リンク共有を作成しています](/help/assets/share-assets.md) 管理者がユーザーに対するこの機能のデフォルトの動作をカスタマイズできる、まったく新しい設定セットが追加されました。

![タグ管理](/help/assets/assets/config-email-service.png)

**Dynamic Media：イメージプロファイルのスマート切り抜き関連のフィールドが更新されました**

イメージプロファイル内の一部のスマート切り抜き関連フィールドのユーザーインターフェイスが更新され、スマート切り抜きを定義する際の現在のガイドラインが反映されるようになりました。 詳しくは、 [切り抜きオプション](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles.html?lang=en#crop-options).

### Assets ビューの新機能 {#assets-view-features}

**アセットの階層タグ付けにより、検索操作を高速化**

時間の経過と共に、語彙が制御されるフラットなリストは管理できなくなります。 アセットビューがサポートされるようになりました。 [階層構造のタグ付け構造](/help/assets/tagging-management-assets-view.md)：関連するメタデータの適用、アセットの分類、検索のサポート、タグの再利用、検出性の向上などを容易におこなえます。

![タグ管理](/help/assets/assets/tags-hierarchy.png)

**ファイル、フォルダー、コレクションをピン留めして、すばやくアクセスできるようにする**

次の操作を実行できます。 [ファイル、フォルダー、コレクションをピン留めしてアクセスを高速化](/help/assets/my-workspace-assets-view.md) 後で必要になった場合に、これらの項目に追加します。 固定された項目は、 **クイックアクセス** を参照してください。 リポジトリ内の保存先に移動する代わりに、My Workspace を使用してアクセスできます。

![ワークスペースのタスク](/help/assets/assets/quick-access.png)

**ごみ箱フォルダー内のアセットのフィルタリング**

Assets ビューで次の操作が可能になりました。 [ごみ箱フォルダー内の使用可能なアセットのフィルタリング](/help/assets/navigate-assets-view.md). ごみ箱フォルダー内の適切なアセットを検索するために、標準フィルターまたはカスタムフィルターを適用して、アセットを復元または完全に削除できます。

**3D アセットのサムネールプレビュー**

Assets ビューで、gLB、USDz、FBX、3DS、OBJ、SBSAR など、一般的な 3D ファイル形式のサムネールプレビューが生成されるようになりました。 これらのファイルが Assets ビューにアップロードされると、デフォルトでは、システムによってサムネールが自動的に生成されます。

![ワークスペースのタスク](/help/assets/assets/3d-preview.png)

**上位の検索済みキーワードを表示**

アセットビューがサポートされるようになりました。 [デプロイメント内で検索された上位の用語の表示](/help/assets/my-workspace-assets-view.md) の使用 **インサイト** を参照してください。 詳細なインサイトに移動して、過去 30 日間または 12 ヶ月間の上位の検索結果を表示することもできます。

![ワークスペースのタスク](/help/assets/assets/insights-top-searches.png)

**メタデータフォームの強化**

Assets ビューで次の操作が可能になりました。 [複数値テキストおよびドロップダウンリストプロパティコンポーネントを追加する](/help/assets/metadata-assets-view.md#property-components) をメタデータフォームに追加します。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] で利用できる新機能 {#new-features-available-in-channel}

* [AEM Page Editor 内のアダプティブForms](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md): AEMページエディターを使用して、複数のフォームをすばやく作成し、サイトのページに追加できるようになりました。 この機能を使用すると、コンテンツ作成者は、動的な動作、検証、データ統合、レコードのドキュメントの生成、ビジネスプロセスの自動化など、アダプティブフォームコンポーネントの機能を利用して、Sites ページ内にシームレスなデータ取得エクスペリエンスを作成できます。 以下の操作を実行できます。

   * フォームコンポーネントをAEM SitesエディターまたはエクスペリエンスフラグメントのアダプティブFormsコンテナコンポーネントにドラッグ&amp;ドロップして、アダプティブフォームを作成します。
   * AEM Sitesエディター内でアダプティブFormsウィザードを使用すると、任意の Sites ページとは独立したフォームを作成して、自由に複数のページでそのようなフォームを再利用できます。
   * 複数のフォームを Sites ページに追加し、ユーザーエクスペリエンスを合理化し、より柔軟に提供します。

     >[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

* [Adobe Acrobat Sign Solutions for Government](/help/forms/adobe-sign-integration-adaptive-forms.md):AEM Formsは、Adobe Acrobat Sign Solutionsと統合され、政府機関向けになりました。 この統合により、政府関連のアカウント（政府機関および機関）に対するアダプティブフォーム送信により、e-Signatures の高度なコンプライアンスとセキュリティを提供します。

  Adobe Acrobat Sign Solutions for Government との統合により、Adobeのパートナーや政府のお客様は、Adaptive Formsで最もミッションクリティカルで機密性の高い業務の一部に電子署名を使用できます。 このセキュリティの強化により、すべての電子署名が FedRAMP Moderate コンプライアンスに完全に準拠し、Adobeの政府のお客様に安心して対応できるようになります。

* [ルールエディターでのカスタムエラーハンドラーによるエラー処理の強化](/help/forms/add-custom-error-handler-adaptive-forms.md)：外部サービスから返されたエラーに応じて（クライアントライブラリを使用して）カスタム関数を呼び出し、エンドユーザーに対してカスタマイズされた応答を提供できるようになりました。 または、サービスから返されたエラーに対して特定のアクションを実行できます。 例えば、特定のエラーコードに対してバックエンドでカスタムワークフローを呼び出したり、サービスが停止していることを顧客に通知したりできます。

  この機能は、OOTB エラーハンドラとの下位互換性のある標準ベースのエラー応答を導入し、柔軟性と制御性を高め、全体的なエラー処理機能を改善するのに役立ちます。

* [フォームデータモデルの強化された認証方法](/help/forms/configure-data-sources.md)：互換性のあるデータソースとAEM Formsを接続するためのクライアント資格情報ベースの認証が導入され、セキュリティが強化されました。 この機能強化により、データの保護を強化し、偽装やユーザーログインを必要としなくなりました。

* [繰り返し可能なセクションを持つアダプティブForms](/help/forms/create-forms-repeatable-sections.md): [アコーディオン](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html), [ウィザード](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html), [パネル](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel-container.html)、および [水平タブ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html) コアコンポーネントベースのアダプティブフォームのコンポーネントを使用して、繰り返し可能なセクションを作成します。

  >[!VIDEO](https://video.tv.adobe.com/v/3421052/adaptive-forms-repeatable-sections-repeat-sections/?quality=12&learn=on)

  これらの繰り返し可能なセクションでは、フィールド数を固定せずに、エントリ数を無制限に指定できます。 これは、必要なデータインスタンスが事前に不明な場合に役立ちます。 Formsのユーザーは、セクションを簡単に追加または削除できるので、フォームを様々なデータ入力シナリオに対応でき、同じデータに関する複数のオカレンスを簡単に収集できます。

* **[Microsoft® SharePointとMicrosoft® OneDrive にアダプティブFormsを送信する](/help/forms/configuring-submit-actions.md)**：ビジネスユーザーの俊敏性が向上し、Microsoft® SharePointサイトや OneDrive フォルダーなどの毎日のツールで、新しいフォームをすばやく起動して送信済みデータを保存できるようになります。

### ヘッドレスアダプティブフォーム早期導入者プログラム {#forms-early-adopter}

用途 [ヘッドレスアダプティブForms](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=jp) 開発者が、従来のグラフィカルユーザーインターフェイスを使用するのではなく、API を使用してアクセスし、操作できるインタラクティブフォームを作成、公開、管理できるようにする。 ヘッドレスアダプティブフォームは以下の場合に役立ちます。

* 高品質のマルチチャネルフォームを好みのプログラミング言語で作成
* デスクトップおよびモバイルアプリ、web サイト、チャットアプリケーションにフォームをネイティブに統合
* フォームアプリケーションで独自の UI コンポーネントを再利用
* Adobe Experience Manager Formsの力を使う

電子メールを `aem-forms-headless@adobe.com` アーリーアダプタープログラムに参加するための公式電子メール ID から

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

## Cloud Manager {#cloud-manager}

Cloud Manager の月次リリースの完全なリストは、[こちら](/help/implementing/cloud-manager/release-notes/current.md)で確認できます。

## 移行ツール {#migration-tools}

移行ツールのリリースの完全なリストは、[こちら](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)で確認できます
