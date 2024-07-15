---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.6.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.6.0 リリースのリリースノート。'
exl-id: 29cf9548-e413-4e4f-b233-d6bb04918b22
feature: Release Information
role: Admin
source-git-commit: f28f212574dda0ece2cedb56a714d381e5bd7d3c
workflow-type: tm+mt
source-wordcount: '1322'
ht-degree: 100%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の 2023.6.0 リリースノート {#release-notes}

以下の節では、[!DNL Experience Manager] as a Cloud Service の 2023.6.0 バージョンの機能リリースノートの概要について説明します。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2021年、2022年）のリリースノートに移動できます。
>
>[!DNL Experience Manager] as a Cloud Service の今後の機能のアクティベーションについての詳細は、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=ja)をご覧ください。

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の最新の機能リリース（2023.6.0）のリリース日は 2023年6月29日（PT）です。次回の機能リリース（2023.7.0）は 2023年7月27日（PT）に予定されています。

## リリースビデオ {#release-video}

2023.6.0 リリースで追加された機能の概要については、2023年6月リリースの概要ビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3420971/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### の新機能[!DNL Experience Manager Sites] {#sites-features}

* コンテンツフラグメントとその参照を、[コンテンツフラグメントコンソール](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console)を使用して [AEM プレビューサービス](/help/implementing/cloud-manager/manage-environments.md#access-preview-service) にパブリッシュできるようになりました。これにより、ユーザーは実稼動環境に移行する前に、切り離されたプレビューアプリケーションで最終的なエクスペリエンスをプレビューできます。

![コンテンツフラグメントコンソールでのプレビュー](/help/assets/content-fragments-console-preview.png)

* AEM GraphQL を使用したヘッドレスシナリオで、web 配信用に画像を動的に最適化できるようになりました。GraphQL クエリで[クエリ変数](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/images.html?lang=ja#query-variables)を定義できるようになり、切り離されたクライアントアプリケーションが、適切に最適化された画像を AEM からリクエストできるようになりました。
* [コンテンツフラグメントのバリエーション](https://experienceleague.adobe.com/docs/experience-manager-65/assets/content-fragments/content-fragments-variations.html?lang=ja)のタグを、AEM GraphQL コンテンツ配信 API を使用して JSON に出力できるようになりました。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### の新機能[!DNL Assets] {#assets-features}

**新しいアセットビューの可用性**

[新しいアセットビュー](/help/assets/assets-view-introduction.md)を Experience Manager Assets で使用できるようになりました。アセットビューにはシンプルなユーザーインターフェイスが用意されており、デジタルアセットの管理、検出、配布が容易になります。このエクスペリエンスの対象は、クリエイティブ、読み取り専用アセットの消費者、より軽量な DAM ユーザーです。

![タグ付けの管理](/help/assets/assets/my-workspace.png)

**検索エクスペリエンスの強化**

Experience Manager Assets では、検索結果のユーザーインターフェイスからさらに多くの作業を行えるようになり、次の操作が可能になりました。

* デフォルトで、リポジトリ全体でキーワードを検索するのではなく、[現在のリポジトリの場所内で検索を実行できます](/help/assets/search-assets.md)。

* 検索結果に表示されるアセットの、[フォルダーの場所へと移動できます](/help/assets/search-assets.md#aftersearch)。

**3D アセットのサムネールプレビュー**

[!DNL Experience Manager Assets] では、gLB、USDz、FBX、3DS、OBJ、SBSAR など、[一般的な 3D ファイル形式のサムネールプレビュー](/help/assets/file-format-support.md)を生成するようになりました。これらのファイルをアップロードすると、デフォルトでサムネールが自動的に生成されます。

**Dynamic Media：イメージプロファイルのスマート切り抜き関連のフィールドを更新**

イメージプロファイルのスマート切り抜き関連のフィールドの一部でユーザーインターフェイスが更新され、スマート切り抜きを定義するための最新のガイドラインが反映されました。詳しくは、[切り抜きオプション](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles.html?lang=ja#crop-options)を参照してください。

### アセットビューの新機能 {#assets-view-features}

**アセットの階層タグ付けにより、検索エクスペリエンスを高速化**

統制語彙のフラットなリストは、時間の経過と共に管理できなくなります。アセットビューでは、[階層的なタグ付け構造](/help/assets/tagging-management-assets-view.md)をサポートするようになりました。これにより、関連するメタデータの適用、アセットの分類、検索のサポート、タグの再利用、検出性の向上などを簡単に行えます。

![タグ付けの管理](/help/assets/assets/tags-hierarchy.png)

**ファイル、フォルダー、コレクションをピン留めして、すばやくアクセスできるようにする**

ファイル、フォルダー、コレクションを[ピン留めして、後で必要になった際に、すばやくアクセス](/help/assets/my-workspace-assets-view.md)できるようになりました。ピン留めした項目は、マイワークスペースの「**クイックアクセス**」セクションに表示されます。リポジトリ内の保存場所に移動する代わりに、マイワークスペースを使用してこれらにアクセスできます。

![ワークスペースのタスク](/help/assets/assets/quick-access.png)

**ごみ箱フォルダー内のアセットのフィルタリング**

アセットビューでは、[ごみ箱フォルダー内の使用可能なアセットをフィルタリングできるようになりました](/help/assets/navigate-assets-view.md)。ごみ箱フォルダー内の適切なアセットを検索するために、標準フィルターまたはカスタムフィルターを適用して、アセットを復元するか完全に削除することができます。

**3D アセットのサムネールプレビュー**

アセットビューでは、gLB、USDz、FBX、3DS、OBJ、SBSAR など、一般的な 3D ファイル形式のサムネールプレビューを生成するようになりました。これらのファイルをアセットビューにアップロードすると、デフォルトでは、システムによってサムネールが自動的に生成されます。

![ワークスペースのタスク](/help/assets/assets/3d-preview.png)

**上位の検索した用語の表示**

アセットビューでは、マイワークスペースの「**インサイト**」セクションを使用して、[アセットビューデプロイメント内で上位に検索した用語の表示](/help/assets/my-workspace-assets-view.md)がサポートされるようになりました。また、詳細なインサイトに移動して、過去 30 日間または 12 か月間で上位の検索結果を表示することもできます。

![ワークスペースのタスク](/help/assets/assets/insights-top-searches.png)

**メタデータフォームの機能強化**

アセットビューでは、[複数値テキストおよびドロップダウンリストのプロパティコンポーネントをメタデータフォームに追加](/help/assets/metadata-assets-view.md#property-components)できるようになりました。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] で利用できる新機能 {#new-features-available-in-channel}

* [AEM ページエディター内のアダプティブフォーム](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)：AEM ページエディターを使用して、複数のフォームを素早く作成し、Sites ページに追加できるようになりました。この機能を使用すると、コンテンツ作成者は、動的な動作、検証、データ統合、レコードのドキュメントの生成、ビジネスプロセスの自動化など、アダプティブフォームコンポーネントの機能を利用して、Sites ページ内にシームレスなデータキャプチャエクスペリエンスを作成できます。以下の操作を実行できます。

   * フォームコンポーネントを AEM サイトエディターまたはエクスペリエンスフラグメントのアダプティブフォームコンテナコンポーネントにドラッグ＆ドロップして、アダプティブフォームを作成します。
   * AEM サイトエディター内でアダプティブフォームウィザードを使用すると、任意の Sites ページとは独立したフォームを作成して、自由に複数のページでそのフォームを再利用できます。
   * 複数のフォームを Sites ページに追加し、ユーザーエクスペリエンスを合理化し、柔軟性を高めます。

     >[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

* [Adobe Acrobat Sign Solutions for Government](/help/forms/adobe-sign-integration-adaptive-forms.md)：AEM Forms が、Adobe Acrobat Sign Solutions for Government と統合されました。この統合により、政府関連のアカウント（政府機関および機関）に対するアダプティブフォーム送信による電子サインに、高度なコンプライアンスとセキュリティを提供します。

  Adobe Acrobat Sign Solutions for Government との統合により、アドビのパートナーや政府のお客様は、アダプティブフォームで最もミッションクリティカルで機密性の高い業務の一部に電子サインを使用できるようになります。このセキュリティの強化により、すべての電子サインが FedRAMP Moderate コンプライアンスに完全に準拠し、アドビの政府機関のお客様に安心感を提供します。

* [ルールエディターでのカスタムエラーハンドラーによるエラー処理の強化](/help/forms/add-custom-error-handler-adaptive-forms.md)：外部サービスから返されたエラーに応じて（クライアントライブラリを使用して）カスタム関数を呼び出し、エンドユーザーに対してカスタマイズされた応答を提供できるようになりました。または、サービスから返されたエラーに対して特定のアクションを実行できます。例えば、特定のエラーコードに対してバックエンドでカスタムワークフローを呼び出したり、サービスが停止していることを顧客に通知したりできます。

  この機能は、OOTB エラーハンドラーとの下位互換性のある標準ベースのエラー応答を導入し、柔軟性と制御性を高め、全体的なエラー処理機能を改善するのに役立ちます。

* [フォームデータモデルの強化された認証方法](/help/forms/configure-data-sources.md)：互換性のあるデータソースと AEM Forms に接続するためのクライアント資格情報ベースの認証が導入され、セキュリティが強化されました。この機能強化により、データの保護を強化し、偽装やユーザーログインを必要としなくなりました。

* [繰り返し可能なセクションを持つアダプティブフォーム](/help/forms/create-forms-repeatable-sections.md)：コアコンポーネントベースのアダプティブフォームで[アコーディオン](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html?lang=ja)、[ウィザード](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html?lang=ja)、[パネル](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel)、および[水平タブ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html?lang=ja)コンポーネントを作成し、繰り返し可能なセクションを作成できるようになりました。

  >[!VIDEO](https://video.tv.adobe.com/v/3421052/adaptive-forms-repeatable-sections-repeat-sections/?quality=12&learn=on)

  これらの繰り返し可能なセクションでは、フィールド数を固定せずに、エントリ数を無制限に指定できます。これは、必要なデータインスタンスがあらかじめ不明な場合に役立ちます。フォームのユーザーは、セクションを簡単に追加または削除できるので、フォームを様々なデータ入力シナリオに対応でき、同じデータに関する複数の発生を簡単に収集できます。

* **[Microsoft® SharePoint と Microsoft® OneDrive にアダプティブフォームを送信](/help/forms/configuring-submit-actions.md)**：ビジネスユーザーの俊敏性を向上させ、新しいフォームを素早く起動し、送信されたデータを Microsoft® SharePoint サイトや OneDrive フォルダーなどの毎日使用するツールに保存します。

### ヘッドレスアダプティブフォーム早期導入者プログラム {#forms-early-adopter}

[ヘッドレスアダプティブフォーム](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=jp)を使用すると、開発者は、従来のグラフィカルユーザーインターフェイスではなく、API を介してアクセスおよび操作できるインタラクティブなフォームを作成、公開、管理できます。ヘッドレスアダプティブフォームは以下の場合に役立ちます。

* 高品質のマルチチャネルフォームを好みのプログラミング言語で作成
* デスクトップおよびモバイルアプリ、web サイト、チャットアプリケーションにフォームをネイティブに統合
* フォームアプリケーションで独自の UI コンポーネントを再利用
* Adobe Experience Manager Forms の機能を活用

ご自身の公式メール ID から `aem-forms-headless@adobe.com` にメールを送信して、早期導入者プログラムにご参加ください。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

## Cloud Manager {#cloud-manager}

Cloud Manager の月次リリースの完全なリストは、[こちら](/help/implementing/cloud-manager/release-notes/current.md)で確認できます。

## 移行ツール {#migration-tools}

移行ツールのリリースの完全なリストは、[こちら](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)で確認できます
