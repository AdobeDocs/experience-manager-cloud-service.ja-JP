---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.11.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.11.0 リリースのリリースノート。'
exl-id: 19cff082-80aa-445c-9462-5e319b7fe0e9
feature: Release Information
role: Admin
source-git-commit: 0845447c1c4f47b77debd179f24eac95a0d2c2db
workflow-type: tm+mt
source-wordcount: '1282'
ht-degree: 57%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の 2023.11.0 リリースノート {#release-notes}

以下の節では、[!DNL Experience Manager] as a Cloud Service の 2023.11.0 バージョンの機能リリースノートの概要について説明します。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2021年、2022年）のリリースノートに移動できます。
>
>[!DNL Experience Manager] as a Cloud Service の今後の機能のアクティベーションについての詳細は、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=ja)をご覧ください。

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の最新の機能リリース（2023.11.0）のリリース日は、2023年11月30日（PT）です。 次回の機能リリース（2023.12.0）は 2023年12月14日（PT）に予定されています。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

## リリースビデオ {#release-video}

2023.11.0 リリースで追加された機能の概要については、2023年11月リリースの概要ビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3425864?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### 早期導入プログラム {#sites-early-adopter}

**[コンテンツフラグメント内の文字列の検索と置換](/help/sites-cloud/administering/content-fragments/managing.md#find-and-replace-find-and-replace)**：コンテンツフラグメントコンソールを使用すると、複数のコンテンツフラグメントに一度に表示される文字列を置換して、コンテンツベロシティを向上させるための簡単で直感的な方法がユーザーに提供されます。

![検索と置換](/help/sites-cloud/administering/content-fragments/assets/cf-managing-find-replace.png)

この機能を試してフィードバックを共有いただける場合公式メール ID から **aemcs-headless-adopter@adobe.com** にメールを送信して、早期導入プログラムの詳細を確認してください。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Assets ビューの新機能 {#assets-view-features}

* **AEM Assetsの組み込みAdobe Express エディター**:Express にアクセスできるユーザーは、Adobe ExpressおよびAdobe Fireflyの画像編集および作成ツールを統合して、AEM Assets内で直接使用できるようになりました。これにより、コンテンツの再利用が促進され、コンテンツベロシティが向上します。

  ![フォルダーにメタデータフォームの割り当て](/help/assets/assets/adobe-express-aem-assets.png)

<!--

* **Smart tags blocklist**: Experience Manager Assets now enables you to define a list of blocked tags. These tags are automatically removed from the auto-generated smart tags when you upload assets to the repository. This capability performs tags governance and saves a lot of time as you can add a tag to the block list and AEM Assets automatically excludes it from the list of tags for any of the assets that are added to the repository.

  ![storage usage insights](/help/assets/assets/block-tags.png)

-->


* **インサイトのストレージ使用状況レポート**：管理者は、インサイトの一部として使用できるストレージ使用状況レポートを表示できるようになりました。

  ![ストレージ使用状況インサイト](/help/assets/assets/storage-usage-insights.png)

* **最初のホームページ設定を検索**:Experience Manager Assetsで、組織のホームページエクスペリエンスを設定できるようになりました。 ホームページとして検索ファーストを選択した場合は、組織の検索バーの位置、背景画像、ロゴを設定できます。

  ![検索ファーストの設定](/help/assets/assets/search-first-configuration.png)

### 管理者向けプレリリースの新機能 {#admin-view-features-prerelease}

**ビデオプレビュー**:AEM Assetsは、処理プロファイルを設定する必要なく、サポートされるすべてのビデオ形式のプレビューレンディションをデフォルトで生成するようになりました。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Experience Manager Forms] の新機能 {#forms-features}

* **[チェックボックスコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox.html?lang=ja)**：コアコンポーネントに基づくアダプティブフォームにチェックボックスコンポーネントを含めることができるようになりました。これにより、ユーザーは特定のオプションを選択または選択解除する二者択一の選択を行うことができます。通常、小さなボックスとして表示され、クリックまたはタップすると、オンとオフの 2 つの状態を切り替えることができます。チェックボックスは、はい／いいえ、または真／偽の選択肢を提示するために使用される一般的なフォーム要素です。

* **[利用条件コンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/terms-and-conditions.html?lang=ja)**：コアコンポーネントに基づくアダプティブフォームに利用条件コンポーネントを含めることができるようになりました。これにより、フォーム作成者は、サービス、製品、プラットフォームの使用に関連する利用条件または法的合意をユーザーに提示するフォーム内に特定のセクションを導入できます。このコンポーネントは、フォームを送信することで同意するルール、規制、義務についてユーザーに通知するように設計されています。

  ![&#x200B; チェックボックス、利用条件、垂直タブコンポーネント &#x200B;](/help/forms/assets/forms-components.png)

* **[垂直タブコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs.html?lang=ja)**：コアコンポーネントに基づくアダプティブフォームでは、フォームのコンテンツをタブの垂直リストに整理し、構造化されたナビゲートしやすいレイアウトを提供できるようになりました。フォームで垂直タブを使用すると、特にフォームに複数のセクションや複雑な情報が含まれている場合、ナビゲーションが簡素化され、フォームコンテンツの整理が改善され、全体的なユーザーエクスペリエンスが向上します。



### [!DNL Forms] プレリリースの新機能 {#prerelease-features-forms}

* **[アダプティブFormsとMicrosoftの接続® SharePoint リスト](/help/forms/configure-submit-actions-core-components.md#submit-to-sharepoint)**:AEM Formsは、SharePointのリスト機能を活用できるように、フォームデータをSharePoint リストに直接送信する OOTB 統合を提供します。 Microsoft SharePoint リストをフォームデータモデルのデータソースとして設定し、**フォームデータモデルを使用して送信** 送信アクションを使用して、アダプティブフォームをSharePoint リストに接続できます。

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### 早期導入プログラム {#forms-early-adopter}

* **Adobe Workfront Fusion シナリオへのアダプティブフォームの送信**：Forms as a Cloud Service には、アダプティブフォームを Adobe Workfront に簡単に接続するための標準オプションが用意されています。これにより、Adobe Workfront シナリオにアダプティブフォームを送信するプロセスが簡単になり、アダプティブフォームの送信時に Workfront Fusion シナリオをトリガーできます。

* **右横書き言語のサポート**：コアコンポーネントに基づいて作成されたアダプティブフォームを、アラビア語、ペルシア語、ウルドゥー語などの右横書き（RTL）言語で表示できるようになりました。RTL 言語は、世界中で 20 億人以上の人々が話しています。RTL 言語でフォームを使用すると、アダプティブフォームの範囲を拡張してこれらの多様なオーディエンスに対応し、RTL 市場を活用することができます。 また、特定の地域では、現地の言語でフォームを提供することは法的義務として定められています。現地の言語に対応することで、より幅広いオーディエンスに扉を開くだけでなく、関連する法律や規制を確実に遵守できます。

  ![右横書き言語のサポート](/help/forms/assets/right-to-left-language-support.png)

* **[DocAssurance API（通信 API の一部）を使用したドキュメントの保護](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**：DocAssurance API を使用すると、ドキュメントに署名および暗号化して、機密情報を保護できます。暗号化により、ドキュメントのコンテンツは読み取り不可能な形式に変換され、許可されたユーザーのみがアクセスできるようになります。この強化された保護層は、貴重なデータを信頼できない環境にさらすことなく、安心感ももたらします。Signature API を使用すると、組織は配布および受信する Adobe PDF ドキュメントのセキュリティとプライバシーを保護できます。このサービスでは、デジタル署名と証明書を使用して、意図された受信者のみがドキュメントを変更できるようにします。

  公式メール ID から `aem-forms-ea@adobe.com` に送信して早期導入プログラムに参加し、機能へのアクセスをリクエストできます。

## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### WAF トラフィックフィルタールールのライセンスを取得できるようになりました {#cdn-waf-license}

トラフィックフィルタールールは 10 月にリリースされ、Sites とFormsのお客様が既に利用できるルールを補完するために、今年後半に web アプリケーションファイアウォール（WAF）の特別なカテゴリのルールが利用可能になる予定であることが記載されました。 更新として、WAF-DDoS Protection 製品のライセンスを取得できるようになりました。

ライセンスが取得されると、これらの高度なWAF ルールをCloud Manager設定パイプラインを使用して CDN にデプロイし、web 攻撃に対する保護をさらに強化できます。

WAFなど、[&#x200B; トラフィックフィルタールール &#x200B;](/help/security/traffic-filter-rules-including-waf.md) を参照してください。 WAF-DDoS Protection または Enhanced Security のライセンスについては、AEM アカウントチームにお問い合わせください。

### ドメインマッピング早期導入プログラム {#cdn-config-early-adopter}

最近リリースされた [&#x200B; トラフィックフィルタールール（WAFを含む） &#x200B;](/help/security/traffic-filter-rules-including-waf.md) に加えて、設定パイプラインを使用して、他の種類の CDN 設定を宣言およびデプロイすることもできます。 次のようなユースケースについてお聞かせください。
* 301/302 クライアントサイドのリダイレクト
* 任意の接触チャネルに対するエッジでのリクエストのプロキシ処理
* URL 変換
* リクエストヘッダーまたは応答ヘッダーの設定または変更
* CDN が AEM に到達できない場合のカスタムエラーページ
* ユーザー名/パスワードによる認証
* その他の便利な CDN 設定

公式メール ID からフィードバックを記載したメールを **0&rbrace;aemcs-cdn-config-adopter@adobe.com&rbrace; に送信します。**

## Cloud Manager {#cloud-manager}

Cloud Manager の月次リリースの完全なリストは、[こちら](/help/implementing/cloud-manager/release-notes/current.md)で確認できます。

## 移行ツール {#migration-tools}

移行ツールのリリースの完全なリストは、[こちら](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)で確認できます

## 既知の問題 {#known-issues}

* コアコンポーネントに基づくアダプティブ Formsを送信できない。 この問題は、コアコンポーネントバージョン 2.0.38～2.0.60 を使用して作成されたアダプティブFormsで発生します。

  問題を解決する方法は次のとおりです。 アダプティブフォームのコアコンポーネントバージョン 2.0.62 以降に移行できます。 お使いの環境でアダプティブ Forms コアコンポーネントのバージョンを設定するには、Forms as a Cloud Service リポジトリまたはAEM アーキタイプベースのプロジェクトで `core.forms.components.version`、`core.forms.components.af.version`、`core.wcm.components.version component`dependencies のバージョンを設定して、Forms as a Cloud Service環境に変更内容をデプロイします。 アダプティブForms コアコンポーネントの依存関係の最新バージョンは、[&#x200B; アダプティブForms コアコンポーネント Git リポジトリ &#x200B;](https://github.com/adobe/aem-core-forms-components#system-requirements) で確認できます。
