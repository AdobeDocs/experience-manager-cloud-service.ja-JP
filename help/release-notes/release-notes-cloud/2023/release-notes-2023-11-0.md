---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.11.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.11.0 リリースのリリースノート。'
source-git-commit: c33874869bccae1e9837b30827a655e70636dd56
workflow-type: tm+mt
source-wordcount: '1286'
ht-degree: 15%

---


# [!DNL Adobe Experience Manager] as a Cloud Service の 2023.11.0 リリースノート {#release-notes}

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

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の最新の機能リリース（2023.11.0）のリリース日は 2023年11月30日です。次回の機能リリース（2023.12.0）は 2023年12月14日（PT）に予定されています。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

## リリースビデオ {#release-video}

2023.11.0リリースで追加された機能の概要については、 2023 年 11 月リリースの概要ビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3425864?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### アーリーアダプタープログラム {#sites-early-adopter}

**[コンテンツフラグメント内の文字列の検索と置換](/help/sites-cloud/administering/content-fragments/managing.md#find-and-replace-find-and-replace)**：コンテンツフラグメントコンソールを使用すると、複数のコンテンツフラグメントに表示される文字列を一度に置き換えて、コンテンツの速度を高めることができ、簡単で直感的な方法で置き換えることができます。

![検索と置換](/help/sites-cloud/administering/content-fragments/assets/cf-managing-find-replace.png)

この機能を試して、フィードバックを共有したい場合は、 電子メールの送信先 **aemcs-headless-adopter@adobe.com** アーリーアダプタープログラムの詳細については、公式電子メール ID を参照してください。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### アセット表示の新機能 {#assets-view-features}

* **AEM Assetsの埋め込みAdobe Expressエディター**:Express へのアクセス権を持つユーザーは、Adobe ExpressとAdobe Fireflyの画像編集および作成ツールをAEM Assets内で直接利用できるようになり、コンテンツの再利用を改善し、コンテンツ速度を向上させることができます。

  ![フォルダーにメタデータフォームを割り当て](/help/assets/assets/adobe-express-aem-assets.png)

<!--

* **Smart tags blocklist**: Experience Manager Assets now enables you to define a list of blocked tags. These tags are automatically removed from the auto-generated smart tags when you upload assets to the repository. This capability performs tags governance and saves a lot of time as you can add a tag to the block list and AEM Assets automatically excludes it from the list of tags for any of the assets that are added to the repository.

  ![storage usage insights](/help/assets/assets/block-tags.png)

-->


* **インサイトのストレージ使用状況レポート**：管理者は、インサイトの一部として使用できるストレージ使用量レポートを表示できるようになりました。

  ![ストレージ使用状況インサイト](/help/assets/assets/storage-usage-insights.png)

* **最初のホームページ設定を検索**:Experience Manager Assetsでは、組織に合わせてホームページのエクスペリエンスを設定できるようになりました。 ホームページで最初に検索を選択した場合は、組織の検索バーの配置、背景画像、ロゴを設定できます。

  ![最初の設定を検索](/help/assets/assets/search-first-configuration.png)

### 管理ビューのプレリリースの新機能 {#admin-view-features-prerelease}

**ビデオプレビュー**:AEM Assetsでは、処理プロファイルを設定する必要なく、デフォルトで、サポートされるすべてのビデオ形式のプレビューレンディションを生成するようになりました。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### の新機能 [!DNL Experience Manager Forms] {#forms-features}

* **[チェックボックスコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox.html)**：コアコンポーネントに基づくアダプティブFormsで、チェックボックスコンポーネントを含めることができるようになりました。 ユーザーは、特定のオプションの選択または選択解除を行い、バイナリ選択をおこなうことができます。 これは通常、小さなボックスとして表示され、クリックまたはタップすると、2 つの状態（チェック済みとオフ）を切り替えることができます。 このチェックボックスは、はい/いいえ、真/偽の選択肢を提示するために使用される一般的なフォーム要素です。

* **[利用条件コンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/terms-and-conditions.html)**：コアコンポーネントに基づくアダプティブFormsで、利用条件コンポーネントを含めることができるようになりました。 フォーム作成者は、フォーム内に特定のセクションを導入できます。このセクションには、サービス、製品、プラットフォームの使用に関連する利用条件、または法的契約が表示されます。 このコンポーネントは、フォームを送信することで、同意するルール、規制、義務をユーザーに通知するように設計されています。

  ![チェックボックス、利用条件、および「垂直」タブのコンポーネント](/help/forms/assets/forms-components.png)

* **[垂直タブコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs.html)**：コアコンポーネントに基づくアダプティブFormsで、フォームコンテンツをタブの縦並びのリストに整理でき、構造化されたナビゲーション可能なレイアウトが提供されるようになりました。 フォーム内で縦置きのタブを使用すると、ナビゲーションが簡単になり、フォームコンテンツの構成が改善され、特にフォームに複数のセクションや複雑な情報が含まれる場合に、ユーザーの操作性が向上します。



### の新機能 [!DNL Forms] プレリリース {#prerelease-features-forms}

* **[Microsoft® SharePointリストとのアダプティブFormsの接続](/help/forms/configure-submit-actions-core-components.md#submit-to-sharepoint)**:AEM Formsは、フォームデータを直接SharePointリストに送信するための OOTB 統合機能を提供し、SharePointのリスト機能を活用できます。 Microsoft SharePoint List をフォームデータモデルのデータソースとして設定し、 **フォームデータモデルを使用して送信** アダプティブフォームをSharePointリストに接続するための送信アクション。

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### アーリーアダプタープログラム {#forms-early-adopter}

* **アダプティブフォームをAdobe Workfront Fusion に送信するシナリオ**:Forms as a Cloud Serviceには、アダプティブフォームをAdobe Workfrontに簡単に接続するための既製のオプションが用意されています。 これにより、アダプティブフォームをAdobe Workfrontシナリオに送信するプロセスが簡単になり、アダプティブフォームの送信時にWorkfront Fusion シナリオをトリガーできます。

* **右から左への言語のサポート**：コアコンポーネントに基づいて構築されたアダプティブFormsは、アラビア語、ペルシャ語、ウルドゥー語などの右から左 (RTL) 言語で表示できるようになりました。 RTL 言語は世界で 20 億人以上の人々が話しています RTL 言語のフォームを使用すると、アダプティブフォームのリーチを拡大して、これらの多様なオーディエンスに対応し、RTL 市場をタップできます。 地域によっては、現地の言語でフォームを提供することが法的義務でもあります。 現地の言語に対応することで、より広いオーディエンスへの扉を開くだけでなく、関連する法令への準拠も確保できます。

  ![右から左への言語サポート](/help/forms/assets/right-to-left-language-support.png)

* **[DocAssurance API（通信 API の一部）を使用してドキュメントをProtect](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**:DocAssurance API を使用すると、ドキュメントに署名し、暗号化することで、機密情報を保護できます。 暗号化を通じて、ドキュメントのコンテンツは読み取り不可能な形式に変換され、許可されたユーザーのみがアクセス権を取得できるようになります。 この防護の強化された層は、不正な目から貴重なデータを守るだけでなく、心の安らぎも提供します。 Signature API を使用すると、組織は配布および受信する Adobe PDF ドキュメントのセキュリティとプライバシーを保護できます。このサービスでは、電子署名と証明書を使用して、意図された受信者のみがドキュメントを変更できるようにします。

  次に書き込むことができます： `aem-forms-early-adopter-program@adobe.com` アーリーアダプタープログラムに参加し、機能へのアクセスをリクエストするために、公式の電子メール id から。

## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### WAF トラフィックフィルタールールをライセンス可能に {#cdn-waf-license}

トラフィックフィルタールールは 10 月にリリースされ、 Sites およびFormsのお客様が既に利用できるルールを補うために、今年後半に Web Application Firewall (WAF) ルールの特殊なカテゴリが利用可能になることに注意する必要があります。 WAF-DDoS Protection 製品のライセンスを取得できるようになりました。

ライセンスを取得したら、これらの高度な WAF ルールを Cloud Manager 設定パイプラインを使用して CDN にデプロイし、Web 攻撃に対する保護をさらに強化できます。

お読みください [トラフィックフィルタールール](/help/security/traffic-filter-rules-including-waf.md)（WAF を含む） WAF-DoS 保護または拡張セキュリティのライセンスについては、AEMアカウントチームにお問い合わせください。

### CDN 設定アーリーアダプタープログラム {#cdn-config-early-adopter}

最近リリースされたに加えて [トラフィックフィルタールール（WAF を含む）](/help/security/traffic-filter-rules-including-waf.md)を使用すると、設定パイプラインを使用して他のタイプの CDN 設定を宣言してデプロイする機会があります。 以下を含め、お客様の使用例についてお知らせします。
* 301/302クライアントサイドのリダイレクト
* エッジでのリクエストの任意のオリジンへのプロキシ処理
* URL 変換
* 要求または応答ヘッダーの設定または変更
* CDN がAEMに到達できない場合のカスタムエラーページ
* ユーザー名/パスワードによる認証
* その他の役に立つ CDN 設定

電子メールの送信先 **aemcs-cdn-config-adopter@adobe.com** を公式の電子メール ID から取得し、フィードバックを入力します。

## Cloud Manager {#cloud-manager}

Cloud Manager の月次リリースの完全なリストは、[こちら](/help/implementing/cloud-manager/release-notes/current.md)で確認できます。

## 移行ツール {#migration-tools}

移行ツールのリリースの完全なリストは、[こちら](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)で確認できます

## 既知の問題 {#known-issues}

* コアコンポーネントに基づいたアダプティブFormsを送信できない。 この問題は、コアコンポーネントバージョン 2.0.38 ～ 2.0.60 を使用して構築されたアダプティブFormsで発生します。

  問題を解決する。 アダプティブフォームのコアコンポーネントバージョン 2.0.62 以降に移行できます。 お使いの環境用にアダプティブFormsコアコンポーネントのバージョンを設定するには、次の手順を実行します。 [core.forms.components.version、core.forms.components.af.version および core.wcm.components.version コンポーネントのバージョンを設定します。](/help/forms/enable-adaptive-forms-core-components.md#2-add-adaptive-forms-core-components-dependencies-to-your-git-repository) Formsas a Cloud ServiceリポジトリまたはAEMアーキタイプベースのプロジェクトとの依存関係 [Formsas a Cloud Service環境に変更をデプロイする](/help/forms/enable-adaptive-forms-core-components.md#build-and-deploy-updated-code-on-an-aem-forms-as-a-cloud-service-environment). アダプティブFormsコアコンポーネントの依存関係の最新バージョンは、次の場所にあります。 [アダプティブFormsコアコンポーネント Git リポジトリ](https://github.com/adobe/aem-core-forms-components#system-requirements).
