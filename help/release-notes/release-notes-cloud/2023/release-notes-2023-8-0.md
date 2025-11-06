---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.8.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.8.0 リリースのリリースノート。'
exl-id: a0ffa6cf-64ae-468c-93f4-ac6805ef907e
feature: Release Information
role: Admin
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1691'
ht-degree: 100%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の 2023.8.0 リリースノート {#release-notes}

以下の節では、[!DNL Experience Manager] as a Cloud Service の 2023.8.0 バージョンの機能リリースノートの概要について説明します。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の最新の機能リリース（2023.8.0）の公開日は 2023年8月31日（PT）です。次回の機能リリース（2023.9.0）は、2023年9月28日（PT）に予定されています。

## リリースビデオ {#release-video}

2023.8.0 リリースで追加された機能の概要については、2023年8月リリースの概要ビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3423535/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### の新機能[!DNL Experience Manager Sites] {#sites-features}

* [コンテンツフラグメントコンソール](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html?lang=ja)では、タグを表示し、メタデータとしてコンテンツフラグメントに適用されたタグで検索できるようになりました。そのために Assets UI に切り替える必要がなくなり、コンテキストの切り替えも減って効率性が向上しています。

  ![コンテンツフラグメントコンソールでのタグ付け](/help/assets/content-fragments-console-tags.png)
* AEM as a Cloud Service で新しいコンテンツフラグメントエディターを使用できるようになりました。これにより、コンテンツ作成者のオーサリングタスクが合理化され、コンテンツの編集中に異なるアプリを切り替える必要が減り、生産性が向上します。
  ![新しいコンテンツフラグメントエディター](/help/release-notes/assets/newCFEditor.png)

新しいコンテンツフラグメントエディターには、元のエディターにはない次の利点があります。

* 自動保存によりオーサリングの効率が向上し、誤って編集内容が失われるのが防止されます。
* 深く構造化されたフラグメント内ですばやく移動できるように、構造ツリーを使用したコンテンツフラグメントとその参照の階層表示。
  ![コンテンツフラグメントエディターの構造ツリー](/help/release-notes/assets/newCFEditor_StructureTree.png)

* 最初にアセット DAM にアップロードする必要のない、コンテンツ参照としてのアセットのインラインアップロード
* コンテンツフラグメントによって提供されるレンダリングエクスペリエンスのアドホックプレビューを使用して、作成者がフロントエンドアプリでのコンテンツのルックアンドフィールを視覚化するのに役立てます
* エディターでコンテンツフラグメントのワンクリック公開および非公開
* コンテンツフラグメント編集時の言語コピーの表示と言語コピーへの移動
  ![コンテンツフラグメントエディターの言語コピー](/help/release-notes/assets/newCFEditor_LanguageCopies.PNG)

* コンテンツフラグメントのタイムラインを追跡するのに役立つバージョンの表示

  ![コンテンツフラグメントエディターのバージョン](/help/release-notes/assets/newCFEditor_Versionhistory.PNG)

* 作成者が自分の編集の影響を理解しやすくするための親参照の表示

  ![コンテンツフラグメントエディターの親参照](/help/release-notes/assets/newCFEditor_Parentreferences.PNG)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### アセットビューの新機能 {#assets-view-features}

<!--

**Assign metadata form to a folder**

You can now assign metadata form to a specific folder within your Assets Essentials deployment. All assets in the folder, including assets in the sub-folders, then display properties defined in the assigned metadata form.

![assign metadata form to a folder](/help/release-notes/assets/assign-to-folder.png)

-->

* **データソースからのアセットの一括読み込み**：管理者は、データソースから AEM Assets に[多数のアセットを読み込む機能](/help/assets/bulk-import-assets-view.md)を使用できます。管理者は、個々のアセットやフォルダーを AEM Assets にアップロードする必要がなくなりました。一括読み込みでサポートされるデータソースには、Azure、AWS、Google Cloud、Dropbox が含まれます。

  ![データソースからのアセットの一括読み込み](/help/release-notes/assets/bulk-import.png)

* **Adobe Express を活用した画像編集ツール**：AEM Assets 内で直接使用できる、簡単で直感的な [Adobe Express を活用した画像編集ツール](/help/assets/edit-images-assets-view.md)により、コンテンツの再利用性を高め、コンテンツの処理速度を向上させます。

  ![Adobe Express を使用した画像の編集](/help/release-notes/assets/edit-adobe-express.png)

* **マイワークスペースのクイックアクセス用に項目をピン留めする際の柔軟性**：自分用、組織全体用またはグループのリスト用の項目を選択してピン留めし、選択に基づいて[マイワークスペースのクイックアクセスセクション](/help/assets/my-workspace-assets-view.md)に項目が表示されるようにする機能です。

  ![グループ用の項目をピン留め](/help/release-notes/assets/pin-items-for-groups.png)

### 管理ビューの新機能 {#admin-view-features}

**検索の機能強化**

* 管理者が、検索の実行時に表示される[アセットのバッチサイズを設定](/help/assets/search-assets.md#configure-asset-batch-size)できるようになりました。アセット検索結果をさらに下にスクロールして結果を読み込むと、設定したバッチサイズの倍数でアセット検索結果が表示されます。200、500、1,000 個のアセットの使用可能なバッチサイズから選択できます。バッチサイズを小さく設定すると、検索応答時間が短縮されます。

  ![アセットのバッチサイズ設定](/help/release-notes/assets/assets-batch-size-configuration.png)

* Experience Manager Assets に、`damAssetLucene` インデックスの新しいバージョン 9 が含まれるようになりました。`damAssetLucene-9` が Oak クエリファセットのカウントの動作を変更し、基になる検索インデックスによって返される[ファセット数のアクセス制御を評価しなくなるため](/help/assets/search-assets.md)、検索応答時間が短縮されます。

### [!DNL Experience Manager Assets] で利用できるプレリリース機能 {#prerelease-features-assets}

* **Dynamic Media**：[Dynamic Media のビデオに対するマルチキャプションとマルチオーディオトラックのサポート](/help/assets/dynamic-media/video.md#about-msma) - プライマリビデオに複数のキャプションと複数のオーディオトラックを簡単に追加できるようになりました。この機能により、グローバルなオーディエンスがビデオにアクセスできるようになります。1 つの公開済みプライマリビデオを複数の言語でグローバルオーディエンスに向けてカスタマイズし、様々な地理的地域のアクセシビリティガイドラインに従うことができます。また、作成者は、ユーザーインターフェイスの 1 つのタブからキャプションとオーディオトラックを管理することもできます。

  ![選択したビデオアセットのプロパティページの「キャプションとオーディオトラック」タブ。](/help/release-notes/assets/msma-aem-cs.png)*選択したビデオアセットのプロパティページの「キャプションとオーディオトラック」タブ。*

* **アセット**：Experience Manager で管理されている ZIP アーカイブを選択し、ファイルをダウンロードせずに [Experience Manager に直接ファイルを抽出](/help/assets/manage-digital-assets.md#extract-zip-archives)する機能。

  ![グループ用の項目をピン留め](/help/release-notes/assets/extract-archive.png)


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] で利用できる新機能 {#new-features-available-in-forms-channel}

* [**Google reCAPTCHA Enterprise のサポート**](/help/forms/captcha-adaptive-forms.md)：アダプティブフォームで Google reCAPTCHA Enterprise を使用して、不正なアクティビティやスパムに対する保護を強化し、より安全なユーザーエクスペリエンスを提供します。高度なリスク分析とシームレスな統合により、ユーザーはボットを効果的にブロックしながらフォームを簡単に送信できます。


### [!DNL Forms] で利用できるプレリリース機能 {#pre-release-features-available-in-forms-channel}

* **Forms 向けの Experience Cloud 設定自動化機能を備えた Adobe Analytics**：いくつかのボタンをフリップして、Experience Cloud 設定の自動化で Adobe Analytics を有効にできるようになりました。これにより、AEM Forms as a Cloud Service を Experience Platform タグと Adobe Analytics に接続して、公開したフォームのパフォーマンス指標を取得し、追跡できます。

* **アダプティブフォームの Adobe Analytics レポートテンプレート**：Forms as a Cloud Service が Adobe Analytics レポート OOTB を提供するようになりました。これにより、フォームのパフォーマンスを簡単に理解できます。フォームレベルの指標を使用すると、レンディション、訪問者、送信、平均記入時間など、複数の主要業績評価指標（KPI）に対するフォームのパフォーマンスに関するインサイトを得ることができます。ユーザーの行動とフィードバックを追跡して、フォームのわかりにくい箇所を特定し、フォームのデザインと機能の改善についてガイドします。

  ![アダプティブフォームのユーザーエンゲージメントの Adobe Analytics レポート](/help/forms/assets/forms-analytics-report.png)

* **[コアコンポーネントに基づくアダプティブフォームのフォームフラグメント](/help/forms/adaptive-form-fragments-core-components.md)**：重複を避け、デジタルインベントリを最適化し、共同作業を強化することで、フォームフラグメントを使用してフォーム構築のエクスペリエンスを向上させます。これらの再利用可能なコンポーネントは複数のフォームにシームレスに統合され、一貫性のあるプロフェッショナルな外観のフォームの作成を効率化します。フォームフラグメントは、「一度変更すればすべてに反映」機能を通じて、再利用性、標準化、ブランドの一貫性を確保します。1 か所で行われた更新が、これらのフラグメントを利用するすべてのフォームに自動反映されるので、メンテナンス性と効率性が向上します。

* **[Adobe Sign ワークフローステップの機能強化](/help/forms/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step)**：Adobe Sign ワークフローステップが強化機能され、次が含まれるようになりました。
   * **Adobe Sign の行政 ID に基づいた認証**：Adobe Acrobat Sign の行政 ID に基づいた認証は、ユーザーが行政発行の ID（運転免許証、国民 ID、パスポート）を使用して身元を認証できるようにすることで、追加の検証レイヤーを提供します。この機能強化により、信頼できる ID ドキュメントを使用することで、署名プロセスの信頼性がさらに高まり、高度なセキュリティ、コンプライアンスおよびユーザー検証を必要とするシナリオに最適になります。

   * **Adobe Sign ドキュメントの監査記録**：監査記録機能を使用すると、Adobe Sign ドキュメントのライフサイクルに関する詳細なインサイトが得られます。監査記録を使用すると、ドキュメントに関連するすべてのアクションとインタラクションの包括的な記録を保持できるようになります。これには、ドキュメントを表示、編集、署名したユーザーなどの詳細と、各イベントのタイムスタンプが含まれます。この機能強化は、コンプライアンスの保持、紛争の解決、デジタル契約の整合性を確保する上で重要です。

   * **契約受信者の役割を署名者以外にも拡張**：Adobe Acrobat Sign には、契約受信者の役割を署名者以外にも拡張して、ワークフロー要件にさらに適合するオプションがあります。有効にすると、契約の各受信者の役割を個別に設定でき、署名者がデフォルトになります。

* **[ドキュメント保証 API（通信 API の一部）を使用したドキュメントの保護](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**：ドキュメント保証 API を使用すると、ドキュメントに署名し、暗号化することで、機密情報を保護できます。暗号化を通じて、ドキュメントのコンテンツは読み取り不可能な形式に変換され、許可されたユーザーのみがアクセス権を取得できるようになります。この強化された保護層は、貴重なデータを信頼できない環境にさらすことなく、安心感ももたらします。Signature API を使用すると、組織は配布および受信する Adobe PDF ドキュメントのセキュリティとプライバシーを保護できます。このサービスでは、デジタル署名と証明書を使用して、意図された受信者のみがドキュメントを変更できるようにします。

* **通信 API でのページ数のサポート**：通信 API を使用してドキュメントを取得すると共に、ドキュメント内に含まれるページ数に関する貴重な情報を受け取ることができます。

* **[ルールエディターでのカスタムエラーハンドラーによるエラー処理](/help/forms/add-custom-error-handler-adaptive-forms-core-components.md)**：外部サービスから返されたエラーに応じて、カスタム関数を呼び出し、エンドユーザーに対してカスタマイズされた応答を提供できるようになりました。例えば、特定のエラーコードに対してバックエンドでカスタムワークフローを呼び出したり、サービスが停止していることを顧客に通知したりできます。


### ヘッドレスアダプティブフォーム早期導入者プログラム {#forms-early-adopter}

[ヘッドレスアダプティブフォーム](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=ja)を使用すると、開発者は、従来のグラフィカルユーザーインターフェイスではなく、API を介してアクセスおよび操作できるインタラクティブなフォームを作成、公開、管理できます。ヘッドレスアダプティブフォームは以下の場合に役立ちます。

* 高品質のマルチチャネルフォームを好みのプログラミング言語で作成
* デスクトップおよびモバイルアプリ、web サイト、チャットアプリケーションにフォームをネイティブに統合
* フォームアプリケーションで独自の UI コンポーネントを再利用
* Adobe Experience Manager Forms の機能を活用

ご自身の公式メール ID から `aem-forms-headless@adobe.com` にメールを送信して、早期導入者プログラムにご参加ください。


## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### CDN ログ {#cdn-logs}

Cloud Manager から CDN ログをダウンロードします。これは、キャッシュヒット率の最適化や、コンテンツ配信フローの可視性の向上に役立ちます。[CDN ログの形式について説明します](/help/implementing/developing/introduction/logging.md#cdn-log)。この機能は、9 月上旬に段階的にロールアウトされる予定です。

### CDN および WAF ルールの早期導入プログラム {#waf-early-adopter}

CDN でのトラフィックのフィルタリング基準：

* リクエストのヘッダーとプロパティ（IP アドレスなど）
* 悪意のあるトラフィックと関連付けられていることがわかっているトラフィックパターン

この機能を試してフィードバックを共有いただける場合早期導入プログラムについて詳しくは、ご自身の公式メール ID から **aemcs-waf-adopter@adobe.com** にメールを送信してください。参加者の数は制限されています。

この機能について詳しくは、[こちら](/help/security/traffic-filter-rules-including-waf.md)の記事を参照してください。


## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

## Cloud Manager {#cloud-manager}

Cloud Manager の月次リリースの完全なリストは、[こちら](/help/implementing/cloud-manager/release-notes/current.md)で確認できます。

## 移行ツール {#migration-tools}

移行ツールのリリースの完全なリストは、[こちら](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)で確認できます
