---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: f3d3bc92eb47bf5008167f660f26dfede2700540
workflow-type: tm+mt
source-wordcount: '2285'
ht-degree: 34%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート  {#release-notes}

以下のセクションでは、[!DNL Experience Manager] as a Cloud Service の現在（最新）のバージョンの機能リリースノートの概要について説明します。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2021年、2022年）のリリースノートに移動できます。
>
>[!DNL Experience Manager] as a Cloud Service の今後の機能のアクティベーションについての詳細は、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)をご覧ください。

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates)を参照してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の最新の機能リリース（2024.3.0）のリリース日は、2024年4月11日（PT）です。次回の機能リリース（2024.4.0）は 2024年4月25日（PT）に予定されています。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

## リリースビデオ {#release-video}

2024.3.0 リリースで追加された機能の概要については、2024 年 3 月リリースの概要ビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3428342?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### の新機能[!DNL Experience Manager Sites] {#sites-features}

**Edge Delivery Services向けのAEM オーサリング**

AEM SitesをEdge Delivery Servicesのコンテンツソースとして使用できるようになりました。 作成者は、コンテキスト内 wysiwyg オーサリングを備えた新しいユニバーサルエディターを使用して、AEMで web サイトを管理します。 これにより、企業はEdge Delivery Servicesを使用して高速でパフォーマンスの高い web ページを構築できるだけでなく、コンテンツ管理にAEMの強力な機能を活用できます。

![AEM オーサリング](/help/edge/assets/universal_editor_edge_delivery_services.png)

詳しくは、 [詳細を見る](/help/edge/overview.md) およびウォッチ [AEM Gems - AEM オーサリングとEdge Delivery Servicesの概要](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/aem-gems-getting-started-with-aem-authoring-and-edge-delivery/m-p/652694#M43905)

**ヘッドレス実装用のユニバーサルエディター**

また、ユニバーサルエディターを使用すると、分離された web アプリケーションで、従来のサイト専用のそれと同じ直感的なコンテキスト内 WYSIWYG オーサリングを利用できます。 コンテンツ作成者は、ページ内のコンポーネントと同じ容易さで、コンテンツフラグメントを使用してレイアウトを視覚的に作成できるようになりました。

ユニバーサルエディターの最大の特徴は、様々な web アーキテクチャへの適応性、サーバーサイドとクライアントサイドの両方のレンダリングへの対応、フレームワークに依存しない、AEM ホスティングの必要性の排除です。 既存の web アプリケーションとコンテンツ編集用のユニバーサルエディターの統合は簡単です。主に、開発者がマークアップに特定のデータ属性を組み込む必要があります。

これにより、ユニバーサルエディターは、コンテンツ構造や基盤となるテクノロジースタックに関係なく、一貫した編集エクスペリエンスを保証します。 詳しくは、 [ユニバーサルエディターの概要](/help/implementing/universal-editor/introduction.md).

**コンテンツフラグメントおよびモデルのコンテンツ管理 OpenAPI**

開発者は、コンテンツフラグメントおよびコンテンツフラグメントモデルをプログラムで操作し、コンテンツ管理の OpenAPI を使用して CruD 操作を実行できるようになりました。 詳しくは、を参照してください [API ドキュメント](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)

**エクスペリエンスフラグメントのマルチサイト管理のサポート**

マルチサイト管理のサポートがエクスペリエンスフラグメントを保存するフォルダー構造に対して拡張され、ユーザーがエクスペリエンスフラグメントを使用して完全なコンテンツ構造をロールアウトできるようになりました。

**コンテンツフラグメントのバージョンの比較**

新しいコンテンツフラグメントエディターでは、コンテンツ作成者がコンテンツフラグメントの現在のバージョンと以前のバージョンの違いを比較および表示できるようになりました。

### 早期導入プログラム {#sites-early-adopter}

**バリエーションを生成**

AEMの新機能による GenAI の活用 [バリエーションを生成](/help/generative-ai/generate-variations.md)、Cloud Serviceからアクセスできるようになりました。 バリエーションを生成は、生成 AI を使用してコンテンツの作成を生成および拡張するのに役立ちます。 プログラムでの検討については、Adobeアカウントチームにお問い合わせください。

**コンテンツフラグメントコンソールでのアセットの参照**

コンテンツ作成者は、コンテンツフラグメントコンソールを離れることなく、画像およびその他のアセットを参照、表示およびアクションを実行できるようになりました。

![アセットの参照](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-browse.png)

この機能を試してフィードバックを共有いただける場合公式メール ID からaemcs-headless-adopter@adobe.comにメールを送信して、早期導入プログラムの詳細を確認します。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 管理ビューの新機能 {#admin-view}

**Adobe Expressとのネイティブ統合**

AEM Assetsは、Adobe Expressとネイティブに統合されており、AEM Assetsに保存されているアセットにAdobe Expressユーザーインターフェイス内から直接アクセスできます。 AEM Assetsで管理されているコンテンツを Express キャンバスに配置してから、新しいコンテンツや編集したコンテンツをAEM Assets リポジトリに保存することができます。

![Assets アドオンのアセットを含める](/help/assets/assets/adobe-express-native-integration.png)

**サポートされるすべてのビデオタイプのレンディションのプレビュー**

Experience Manager Assetsは、処理プロファイルの設定を必要とせずに、サポートされるすべてのビデオタイプのプレビューレンディションをデフォルトで生成するようになりました。

### アセットビューの新機能 {#assets-view}

**コレクションの権限の管理**

Assets Essentialsを使用すると、管理者は、リポジトリで使用可能な非公開コレクションのアクセスレベルを管理できます。 管理者は、ユーザーグループを作成し、それらのグループに権限を割り当てて、アクセスレベルを管理できます。ユーザーグループに権限管理の権限をデリゲートすることもできます。


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### AEM Formsの新機能 {#forms-new-features}

* **[Adobe Experience Manager FormsEdge Delivery Services](/help/edge/docs/forms/overview.md)**:AEM Forms Edge Delivery Servicesは、作成者が新しいフォームを迅速に更新、公開、ローンチできる、迅速な開発環境を可能にする構成可能なサービスセットです。 これらのサービスは、エンゲージメントとコンバージョンを促進する、優れた効果の高いフォームエクスペリエンスを提供します。これらのフォームエクスペリエンスは、簡単に作成および開発できます。

  ![EDS Formsの機能](/help/edge/assets/eds-forms-features.png)

これらのサービスにより、次のことが可能になります。

* 同じフォームサイト上で複数のコンテンツソースを操作し、好みのオーサリングツール（Microsoft Excel、Google Sheets、アダプティブFormsエディターなど）を使用する。
* Real User Monitoring （RUM）を通じて、フォームのパフォーマンスを迅速かつ継続的に読み込み、レンダリングするデジタル登録エクスペリエンスを提供します。
* プレーンなHTML、最新の CSS、vanilla JavaScript を使用して、特別なエクスペリエンスを作成し、特定のフレームワークの急な学習曲線を避けます。


### AEM Formsのプレリリースの新機能 {#forms-pre-release}

* **コアコンポーネントベースのアダプティブFormsの強化されたビジュアルルールエディター**：このリリースでは、コアコンポーネントに基づくアダプティブフォームのビジュアルルールエディターが大幅にアップグレードされました。 このリリースでは、コアコンポーネントをベースとするアダプティブフォームのビジュアルルールエディターが大幅にアップグレードされました。 この更新では、カスタム関数とのインタラクションを効率化し、より堅牢で効率的なフォームを作成できるようにすることに重点を置いています。

  次の方法で、カスタム関数のインタラクションを効率化できるようになりました。

   * [新しい注釈を活用して、より明確な機能定義を提供](/help/forms/create-and-use-custom-functions.md#supported-javascript-annotations-for-custom-function).
   * [カスタム関数のキャッシュメカニズムの使用によるフォームのパフォーマンスの向上](/help/forms/create-and-use-custom-functions.md#caching-support-for-custom-function).
   * [カスタム関数内のグローバルオブジェクトのシームレスな操作](/help/forms/create-and-use-custom-functions.md#field-and-global-scope-objects-in-custom-functions).
   * [カスタム関数内でのオプション・パラメータの定義と使用](/help/forms/create-and-use-custom-functions.md#parameter).

  この更新により、ルールエディター機能が次のように強化されました。 以下の操作を実行できます。

   * 強力な機能の実装 [「when-then-else」](/help/forms/rule-editor-core-components.md#when) 条件実行のロジック。
   * let 関数や arrow 関数などの最新の JavaScript 機能を活用します（ES10 のサポート）。
   * フィールドだけでなく、パネルやフォーム全体を検証またはリセットすることで、ユーザーの操作に対するコントロールを拡張できます。

  これらの機能強化により、ビジュアルルールエディター内でルールやカスタム関数を直感的かつ強力に作成できるようになりました。

* **[アダプティブフォームの複数バージョンの作成](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md)**：既存のフォームのバリエーションを簡単に管理できるようになりました。 これにより、バージョン管理が簡素化され、フォームの最適化の比較が、合理化された単一のワークフロー内で容易になります。

* **[アダプティブフォームの比較](/help/forms/compare-forms.md)**:2 つのフォームを簡単に比較して、2 つのフォームの違いを特定できるようになりました。 チームメンバーがリビジョンを比較し、変更を効率的に議論できるので、共同作業がスムーズになります。

* **手書き署名コンポーネントのアクセシビリティの強化**：この更新により、手書き署名コンポーネントのアクセシビリティが大幅に向上しました。

  **キーボードナビゲーションの改善：**
   * Tab キーを押すと、署名ダイアログボックス内のすべてのインタラクティブ要素間を移動できます。
   * ブラシまたはキーボードで署名して Enter キーを押すと、ダイアログが閉じます。
   * 署名して「OK」をクリックした後も、署名コントロールにフォーカスが移動したままになります。

  **署名のクリア機能：**

   * Tab キーを使用すると、署名を消去するための明確なクロスアイコンにアクセスできます。
   * 「署名確認をクリア」ダイアログには、タブナビゲーションからもアクセスできます。

  **ラベルとコントロールの機能強化：**
   * キーボード署名ボタンのラベルが、「aria-label」を使用して機能（「aria-label=&#39;キーボードを使用して署名」など）をアナウンスする方が明確になりました。
   * コントラストが向上し、手書き署名内のすべてのコントロールを簡単に区別できるようになりました。
   * OK/チェックマークボタンが、非アクティブの場合に視覚的に示されるようになりました。

  **スクリーンReaderのシグネチャーフィードバック：**
   * 署名を入力すると、スクリーンリーダーのユーザーは、署名の作成に使用されるテキストを聞くことができます。

このアップデートにより、手書き署名コンポーネントのナビゲーション、明確さ、フィードバックが改善され、障害のあるユーザーのエクスペリエンスがより包括的になります。

### 早期導入プログラム {#forms-early-adopter}

* **[アダプティブフォームをAdobe Workfront Fusion シナリオに送信する](/help/forms/submit-adaptive-form-to-workfront-fusion.md)**:Forms as a Cloud Serviceは、アダプティブフォームをAdobe Workfrontと簡単に接続するための標準のオプションを提供します。 これにより、Adobe Workfront シナリオにアダプティブフォームを送信するプロセスが簡単になり、アダプティブフォームの送信時に Workfront Fusion シナリオをトリガーできます。

  <br/> ![Adobe Workfront](/help/forms/assets/adobe-workfront.png) <br/> Adobe Workfront Fusion コネクタを使用すると、アダプティブフォームの送信時に自動的にトリガーされるワークフローを設計できます。例えば、送信されたデータを確認するタスクを特定の個人に割り当てるワークフローが開始され、アダプティブフォームから取り込まれた情報に基づいて、申し込みの承認または拒否ができるようになるシナリオを想定します。この合理化された統合により、効率が向上し、ワークフロープロセスに新しいレベルの自動化が実現します。|

* **[Reader拡張サービス](/help/forms/aem-forms-cloud-service-communications-introduction.md#reader-extension-service)**:AEM Forms Communication API は、通常のユーザーにフォーム入力やコメントなどの機能を追加できるReader拡張サービスを導入しました。これにより、無料のAdobe Readerを使用してPDFにとってインタラクティブなコミュニケーションを実現できます。

* [右横書き言語のサポート](/help/forms/supporting-new-language-localization-core-components.md)：コアコンポーネントに基づいて作成されたアダプティブフォームを、アラビア語、ペルシア語、ウルドゥー語などの右横書き（RTL）言語で表示できるようになりました。RTL 言語は、世界中で 20 億人以上の人々が話しています。RTL 言語のフォームを使用すると、アダプティブフォームのリーチを拡大して、これらの多様なオーディエンスに対応し、RTL マーケットを選択できます。また、特定の地域では、現地の言語でフォームを提供することは法的義務として定められています。現地の言語に対応することで、より幅広いオーディエンスに扉を開くだけでなく、関連する法律や規制を確実に遵守できます。

* **[DocAssurance API（通信 API の一部）を使用したドキュメントの保護](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**：DocAssurance API を使用すると、ドキュメントに署名および暗号化して、機密情報を保護できます。暗号化により、ドキュメントのコンテンツは読み取り不可能な形式に変換され、許可されたユーザーのみがアクセスできるようになります。この強化された保護層は、貴重なデータを信頼できない環境にさらすことなく、安心感ももたらします。Signature API を使用すると、組織は配布および受信する Adobe PDF ドキュメントのセキュリティとプライバシーを保護できます。このサービスでは、デジタル署名と証明書を使用して、意図された受信者のみがドキュメントを変更できるようにします。

  公式メール ID から `aem-forms-ea@adobe.com` に送信して早期導入プログラムに参加し、機能へのアクセスをリクエストできます。

* **[リアルユーザーモニタリング（RUM）データサービスを活用](/help/implementing/cloud-manager/content-requests.md#real-user-monitoring-for-aem-as-a-cloud-service)**して、AEM as a Cloud Service のクライアントサイドのコレクションを有効にすることができます。
実ユーザーモニタリング（RUM）データサービスは、ユーザーインタラクションをより正確に反映し、web サイトのエンゲージメントの信頼性の高い測定を保証します。 ページのパフォーマンスに関する高度なインサイトを取得する絶好の機会です。 これは、アドビが管理する CDN やアドビ以外が管理する CDN を使用するお客様にとって有益です。さらに、アドビ以外が管理する CDN を使用しているお客様は、自動トラフィックレポートを有効にできるようになり、アドビとトラフィックレポートを共有する必要がなくなります。

  この新機能をテストしてフィードバックを共有することに興味がある場合は、Adobe ID に関連付けられたメールアドレスから、RUM を有効にする各環境のドメイン名を添付して、`aemcs-rum-adopter@adobe.com` にメールを送信してください。その後、アドビの製品チームが、リアルユーザーモニタリング（RUM）データサービスを有効にします。

## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### 早期導入プログラム {#foundation-early-adopter}

#### トラフィックフィルタールールアラート（早期導入プログラム） {#traffic-filter-rules-alerts-early-adopter}

最近リリースされたもの [トラフィックフィルタールール](/help/security/traffic-filter-rules-including-waf.md)には、オプションでライセンス可能な web アプリケーションファイアウォール（WAF）ルールが含まれており、許可または拒否するトラフィックを設定できます。

メールを送信できるようになりました **<aemcs-cdn-config-adopter@adobe.com>** トラフィックフィルタールールがトリガーされるたびにアラートを受け取れるように、早期導入プログラムに参加します。 特定のトラフィック状況が発生した場合にアクションセンターのメール通知が送信されるので、適切な対策を講じることができます。

#### CDN 設定（早期導入プログラム） {#cdn-config-early-adopter}

最近リリースされたに加えて [トラフィックフィルタールール](/help/security/traffic-filter-rules-including-waf.md)（オプションでライセンス可能な Web アプリケーションファイアウォール（WAF）ルールが含まれる）場合は、設定パイプラインを使用して、他のタイプの CDN 設定を宣言およびデプロイできます。 [詳細情報](/help/implementing/dispatcher/cdn-configuring-traffic.md) 電子メールで早期導入プログラムに参加 **<aemcs-cdn-config-adopter@adobe.com>** アクセス権を取得するには：

* 301/302 クライアントサイドのリダイレクト
* エッジにあるリクエストを任意のオリジンにプロキシ化（AEM以外のアプリケーションなど）
* URL 変換
* リクエストヘッダーまたは応答ヘッダーの設定または変更
* CDN が AEM に到達できない場合のカスタムエラーページ

#### 書き換えマップの Apache/Dispatcher ランタイム取り込み（早期導入プログラム） {#apache-rewritemaps-early-adopter}

AEM 6.5 と同様に、Apache/Dispatcher は、web 階層パイプラインの実行を必要とせずに、パブリッシュリポジトリー内の特定の場所に配置された書き換えマップを取り込んで読み込みます。 これにより、ビジネスユーザーが UI を使用してリダイレクトを宣言する機会が生まれます（ACS Commons リダイレクトマップマネージャーで提供されるなど）。 にご連絡ください。 **<aemcs-cdn-config-adopter@adobe.com>** を参照してください。

#### 動的コンテンツを読み込むためのエッジサイドインクルード（ESI）（早期導入プログラム） {#esi-early-adopter}

Adobeが管理する CDN で、エッジレベルの動的 web コンテンツアセンブリ用のマークアップ言語であるエッジサイドインクルード（ESI）がサポートされるようになりました。 ESI スニペットを含めることで、より高い TTL で CDN のHTMLページ全体をキャッシュしながら、より高いケイデンスの更新（低い TTL）を必要とする小さなセクションをオリジンから頻繁に取得できます。 にご連絡ください。 **<aemcs-cdn-config-adopter@adobe.com>** を参照してください。

#### サイトテーマとサイトテンプレートを使用したフロントエンドコードの RDE サポート（早期導入プログラム） {#rde-frontend-early-adopter}

[迅速な開発環境（RDE）](/help/implementing/developing/introduction/rapid-development-environments.md)は、早期導入者向けに、[サイトテーマ](/help/sites-cloud/administering/site-creation/site-themes.md)と[サイトテンプレート](/help/sites-cloud/administering/site-creation/site-templates.md)に基づいたフロントエンドコードをサポートするようになりました。RDE では、[フロントエンドパイプライン](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md)ではなくコマンドラインディレクティブを使用して行われます。にご連絡ください。 **<aemcs-rde-support@adobe.com>** 試してみて、フィードバックを提供する。

#### RDE のロギングの強化（早期導入プログラム） {#rde-logging-early-adopter}

でコードをデバッグする場合 [迅速な開発環境（RDE）](/help/implementing/developing/introduction/rapid-development-environments.md)のバージョン管理で OSGi プロパティを変更することなく、コマンドラインを使用して、開発者がより効率的にログを設定し、ストリーミングできるようになりました。 次のような機能があります。

* パッケージまたはクラスレベルごとのログレベルの宣言
* ログ出力形式のカスタマイズ
* 複数のログを並行してストリーミング

にご連絡ください。 **<aemcs-rde-support@adobe.com>** 試してみて、フィードバックを提供する。

## Cloud Manager {#cloud-manager}

Cloud Manager の月次リリースの完全なリストは、[こちら](/help/implementing/cloud-manager/release-notes/current.md)で確認できます。

## 移行ツール {#migration-tools}

移行ツールのリリースの完全なリストは、[こちら](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)で確認できます

