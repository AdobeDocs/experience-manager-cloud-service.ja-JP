---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: 325769d4a3b93502b0c6857e20911b05df34a24a
workflow-type: tm+mt
source-wordcount: '1861'
ht-degree: 13%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート  {#release-notes}

以下のセクションでは、[!DNL Experience Manager] as a Cloud Service の現在（最新）のバージョンの機能リリースノートの概要について説明します。

>[!NOTE]
>
>ここから、2021 年や 2022 年など、以前のバージョンのリリースノートに移動できます。
>
>[!DNL Experience Manager] as a Cloud Service の今後の機能のアクティベーションについての詳細は、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=ja)をご覧ください。

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

のリリース日 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 現在の機能リリース (2023.8.0) は 2023 年 8 月 31 日です。 次の機能リリース (2023.9.0) は、2023 年 9 月 28 日に予定されています。

## リリースビデオ {#release-video}

2023.8.0 リリースに追加された機能の概要については、 2023 年 8 月リリースの概要ビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3423535/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### の新機能[!DNL Experience Manager Sites] {#sites-features}

* The [コンテンツフラグメントコンソール](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html?lang=en) では、タグを表示し、メタデータとしてコンテンツフラグメントに適用されたタグで検索できるようになりました。 この機能で Assets UI に切り替える必要がなくなり、コンテキストの切り替えが減り、効率が向上します。

  ![コンテンツフラグメントコンソールでのタグ付け](/help/assets/content-fragments-console-tags.png)
* AEM as a Cloud Serviceで新しいコンテンツフラグメントエディターを使用できるようになりました。 これにより、コンテンツ作成者は、オーサリングタスクを合理化し、コンテンツの編集中に異なるアプリを切り替える必要性を減らし、生産性を高めることができます。
  ![新しいコンテンツフラグメントエディター](/help/release-notes/assets/newCFEditor.png)

新しいコンテンツフラグメントエディターには、元のエディターでは使用できない次の利点があります。
* 自動保存によりオーサリングの効率が向上し、誤って編集内容が失われるのを防ぎます。
* 深く構造化されたフラグメント内ですばやく移動できるように、構造ツリーを使用したコンテンツフラグメントとその参照の階層表示。
  ![コンテンツフラグメントエディターの構造ツリー](/help/release-notes/assets/newCFEditor_StructureTree.png)

* 最初に Asset DAM にアップロードする必要なく、コンテンツ参照としてアセットをインラインでアップロードできる
* コンテンツフラグメントによって提供されるレンダリングされたエクスペリエンスのアドホックプレビューを使用して、フロントエンドアプリでのコンテンツのルックアンドフィールを視覚化できます
* エディターでコンテンツフラグメントの公開と非公開を 1 回クリックします。
* コンテンツフラグメントの編集中に言語コピーを表示し、そこに移動する
  ![コンテンツフラグメントエディターの言語コピー](/help/release-notes/assets/newCFEditor_LanguageCopies.PNG)

* コンテンツフラグメントのタイムラインを追跡するのに役立つバージョンを表示する

  ![コンテンツフラグメントエディターのバージョン](/help/release-notes/assets/newCFEditor_Versionhistory.PNG)

* 親参照を表示して、作成者が編集の影響を理解できるようにします

  ![コンテンツフラグメントエディターの親参照](/help/release-notes/assets/newCFEditor_Parentreferences.PNG)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Assets ビューの新機能 {#assets-view-features}

<!--

**Assign metadata form to a folder**

You can now assign metadata form to a specific folder within your Assets Essentials deployment. All assets in the folder, including assets in the sub-folders, then display properties defined in the assigned metadata form.

![assign metadata form to a folder](/help/release-notes/assets/assign-to-folder.png)

-->

* **データソースからのアセットの一括読み込み**：管理者は、 [多数のアセットを読み込む機能](/help/assets/bulk-import-assets-view.md) データソースからAEM Assetsへ。 管理者は、個々のアセットやフォルダーをAEM Assetsにアップロードする必要はありません。 一括インポートでサポートされるデータソースには、Azure、AWS、Google Cloud、Dropboxが含まれます。

  ![データソースからのアセットの一括読み込み](/help/release-notes/assets/bulk-import.png)

* **画像編集ツール (Adobe Express機能 )**：簡単で直感的 [画像編集ツール (Adobe Express機能を利用 )](/help/assets/edit-images-assets-view.md) は、AEM Assets内で直接使用して、コンテンツの再利用を促進し、コンテンツの速度を向上できます。

  ![画像編集とAdobe Express](/help/release-notes/assets/edit-adobe-express.png)

* **My Workspace クイックアクセス用に項目をピン留めする際の柔軟性**：組織全体またはグループのリストの項目を選択してピン留めし、それらを [My Workspace のクイックアクセスセクション](/help/assets/my-workspace-assets-view.md) 選択内容に基づいて選択します。

  ![グループの項目をピン留めする](/help/release-notes/assets/pin-items-for-groups.png)

### 管理ビューの新機能 {#admin-view-features}

**検索の機能強化**

* 管理者が [アセットのバッチサイズの設定](/help/assets/search-assets.md#configure-asset-batch-size) 検索を実行すると表示される アセット検索結果をさらに下にスクロールして結果を読み込むと、設定したバッチサイズの数倍の値でアセット検索結果が表示されます。 200、500、1,000 個のアセットの使用可能なバッチサイズから選択できます。 バッチサイズを小さく設定すると、検索応答時間が短縮されます。

  ![Assets のバッチサイズ設定](/help/release-notes/assets/assets-batch-size-configuration.png)

* Experience Manager Assetsに、の新しいバージョン 9 が含まれるようになりました。 `damAssetLucene` インデックス。 `damAssetLucene-9` Oak クエリファセットの動作を次の値にカウントするように変更しました。 [ファセット数のアクセス制御を評価しなくなりました。](/help/assets/search-assets.md) 基になる検索インデックスによって返されるので、検索応答時間が短くなります。

### で使用可能なリリース前機能 [!DNL Experience Manager Assets] {#prerelease-features-assets}

* **Dynamic Media**: [Dynamic Mediaでのビデオのマルチサブタイトルおよびマルチオーディオトラックのサポート](/help/assets/dynamic-media/video.md#about-msma) — プライマリビデオに複数のサブタイトルや複数のオーディオトラックを簡単に追加できるようになりました。 この機能を使用すると、ビデオにアクセスできるのは、全世界のオーディエンス全体です。 複数の言語でグローバルオーディエンスに対して 1 つの公開済みプライマリビデオをカスタマイズし、様々な地域のアクセシビリティガイドラインに従うことができます。 作成者は、ユーザーインターフェイスの 1 つのタブからサブタイトルやオーディオトラックを管理することもできます。

  ![選択したビデオアセットのプロパティページの「サブタイトルとオーディオトラック」タブ。](/help/release-notes/assets/msma-aem-cs.png)*選択したビデオアセットのプロパティページの「サブタイトルとオーディオトラック」タブ。*

* **Assets**:Experience Managerで管理される ZIP アーカイブおよび [ファイルを直接Experience Managerに抽出](/help/assets/manage-digital-assets.md#extract-zip-archives) ダウンロードせずに

  ![グループの項目をピン留めする](/help/release-notes/assets/extract-archive.png)


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### で使用可能なリリース前機能 [!DNL Forms] {#pre-release-features-available-in-forms-channel}

* [**Google reCAPTCHA エンタープライズサポート**](/help/forms/captcha-adaptive-forms-core-components.md)：アダプティブフォームでGoogle reCAPTCHA Enterprise を使用して、不正なアクティビティやスパムに対する保護を強化し、より安全なユーザーエクスペリエンスを提供します。 高度なリスク分析とシームレスな統合により、本物のユーザーは、ボットを効果的にブロックしながらフォームを簡単に送信できます。

* **Forms向けのExperience Cloud設定自動化機能を備えたAdobe Analytics**：いくつかのボタンをフリップして、Experience Cloud設定の自動化でAdobe Analyticsを有効にできるようになりました。 これにより、AEM Formsas a Cloud ServiceをExperience PlatformタグとAdobe Analyticsに接続して、発行されたフォームのパフォーマンス指標を取得し、追跡できます。

* **Adobe AnalyticsアダプティブFormsのレポートテンプレート**:Forms as a Cloud ServiceがAdobe Analyticsレポート OOTB を提供するようになりました。 これにより、フォームのパフォーマンスを簡単に理解できます。フォームレベルの指標を使用すると、レンディション、訪問者、送信、平均記入時間など、複数の主要業績評価指標（KPI）に対するフォームのパフォーマンスに関するインサイトを得ることができます。ユーザーの行動やフィードバックを追跡することで、フォームの混乱の原因となっている領域を特定し、フォームのデザインと機能に関するガイドを改善できます。

  ![アダプティブフォームのユーザーエンゲージメントの Adobe Analytics レポート](/help/forms/assets/forms-analytics-report.png)

* **[コアコンポーネントに基づくアダプティブFormsのフォームフラグメント](/help/forms/adaptive-form-fragments-core-components.md)**：フォームフラグメントを使用してフォーム構築のエクスペリエンスを向上させるため、複製を避け、デジタルインベントリを最適化し、コラボレーションを強化します。 これらの再利用可能なコンポーネントは複数のフォームにシームレスに統合され、一貫性のあるプロフェッショナルな外観のフォームの作成を合理化します。 フォームフラグメントは、「一度変更してすべてに反映」機能を通じて、再利用性、標準化、ブランドの一貫性を確保します。 1 か所でおこなわれた更新が、これらのフラグメントを利用するすべてのフォームに自動的に反映されるので、メンテナンス性と効率性が向上します。

* **[Adobe Sign Workflow ステップの強化](/help/forms/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step)**: Adobe Sign Workflow ステップが拡張され、以下が含まれるようになりました。
   * **Adobe Signの政府機関 ID ベースの認証**:Adobe Acrobat Signの政府 ID ベースの認証では、政府発行の ID（運転免許証、国民 ID、パスポート）を使用してユーザーが ID を認証できるようにすることで、さらに検証レイヤーを提供しています。 この機能強化は、信頼できる識別ドキュメントを活用することで、署名プロセスにさらに信頼性を高め、セキュリティ、コンプライアンス、およびユーザーの検証を強化する必要があるシナリオに最適です。

   * **Adobe Signドキュメントの監査証跡**：監査記録機能を使用すると、Adobe Signドキュメントのライフサイクルに関する詳細なインサイトを得ることができます。 監査証跡を使用すると、ドキュメントに関連するすべてのアクションとインタラクションの包括的な記録を維持できるようになりました。 これには、ドキュメントの閲覧者、編集者、署名者、および各イベントのタイムスタンプなどの詳細が含まれます。 この強化は、コンプライアンスの維持、紛争の解決、およびデジタル契約の整合性の確保に不可欠です。

   * **署名者以外の契約受信者の新しい役割**:Adobe Acrobat Signには、署名者だけでなく、契約受信者の役割を拡張して、ワークフロー要件をより適切に満たすことができます。 有効にすると、契約の各受信者の役割は個別に設定でき、署名者がデフォルトとなります。

* **[Document Assurance API（通信 API の一部）を使用してドキュメントをProtect](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**:Document Assurance API を使用すると、ドキュメントに署名し、暗号化することで、機密情報を保護できます。 暗号化を通じて、ドキュメントのコンテンツは読み取り不可能な形式に変換され、許可されたユーザーのみがアクセス権を取得できるようになります。 この防護の強化された層は、不正な目から貴重なデータを守るだけでなく、心の安らぎも提供します。 署名 API を使用すると、組織が配信および受信するAdobe PDFドキュメントのセキュリティとプライバシーを保護できます。 このサービスでは、デジタル署名と証明書を使用して、意図された受信者のみがドキュメントを変更できるようにします。

* **通信 API でのページ数のサポート**：これで、通信 API を使用してドキュメントを取得すると共に、ドキュメント内に含まれるページ数に関する貴重な情報を受け取ることができます。

* **[ルールエディターでのカスタムエラーハンドラーによるエラー処理](/help/forms/add-custom-error-handler-adaptive-forms-core-components.md)**：外部サービスから返されたエラーに応じてカスタム関数を呼び出し、エンドユーザーに対してカスタマイズされた応答を提供できるようになりました。 例えば、特定のエラーコードに対してバックエンドでカスタムワークフローを呼び出したり、サービスが停止していることを顧客に通知したりできます。


### アーリーアダプタープログラム {#forms-early-adopter}

* **[DocAssurance API（通信 API の一部）を使用してドキュメントをProtect](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**:DocAssurance API を使用すると、ドキュメントに署名し、暗号化することで、機密情報を保護できます。 暗号化を通じて、ドキュメントのコンテンツは読み取り不可能な形式に変換され、許可されたユーザーのみがアクセス権を取得できるようになります。 この防護の強化された層は、不正な目から貴重なデータを守るだけでなく、心の安らぎも提供します。 署名 API を使用すると、組織が配信および受信するAdobe PDFドキュメントのセキュリティとプライバシーを保護できます。 このサービスでは、デジタル署名と証明書を使用して、意図された受信者のみがドキュメントを変更できるようにします。

Adobeサポートに接続して、DocAssurance API 用のアーリーアダプタープログラムに参加できます。

**ヘッドレスアダプティブForms**：使用 [ヘッドレスアダプティブForms](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=jp) 開発者が、従来のグラフィカルユーザーインターフェイスを使用するのではなく、API を使用してアクセスし、操作できるインタラクティブフォームを作成、公開、管理できるようにする。 ヘッドレスアダプティブフォームは以下の場合に役立ちます。

* 高品質のマルチチャネルフォームを好みのプログラミング言語で作成
* デスクトップおよびモバイルアプリ、web サイト、チャットアプリケーションにフォームをネイティブに統合
* フォームアプリケーションで独自の UI コンポーネントを再利用
* Adobe Experience Manager Formsの力を使う

電子メールを `aem-forms-headless@adobe.com` アーリーアダプタープログラムに参加するための公式電子メール ID から


## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### CDN ログ {#cdn-logs}

Cloud Manager から CDN ログをダウンロードします。これは、キャッシュヒット率の最適化や、コンテンツ配信フローの可視性の向上に役立ちます。 [詳細](/help/implementing/developing/introduction/logging.md#cdn-log) CDN ログの形式を設定します。 この機能は、9 月上旬に段階的に提供される予定です。

### CDN および WAF ルールのアーリーアダプタープログラム {#waf-early-adopter}

CDN でのトラフィックのフィルタリング基準：
* リクエストヘッダーとプロパティ（IP アドレスなど）
* 悪意のあるトラフィックに関連付けられていると知られているトラフィックパターン

この機能を試して、フィードバックを共有したい場合は、 電子メールの送信先 **aemcs-waf-adopter@adobe.com** アーリーアダプタープログラムの詳細については、公式電子メール ID を参照してください。 スペースは制限されています。

この機能の詳細については、この記事を参照してください。 [ここ](/help/security/cdn-and-waf-rules.md).


## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

## Cloud Manager {#cloud-manager}

Cloud Manager の月次リリースの完全なリストは、[こちら](/help/implementing/cloud-manager/release-notes/current.md)で確認できます。

## 移行ツール {#migration-tools}

移行ツールのリリースの完全なリストは、[こちら](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)で確認できます
