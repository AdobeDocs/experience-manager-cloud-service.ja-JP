---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2024.3.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2024.3.0 リリースのリリースノート。'
exl-id: b3816929-2c0a-4d6a-b583-c928d2182ecd
feature: Release Information
role: Admin
source-git-commit: 7f63f66cb1753fc32996e4672214eccc33ca8d92
workflow-type: tm+mt
source-wordcount: '2293'
ht-degree: 95%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の 2024.3.0 リリースノート {#release-notes}

以下の節では、[!DNL Experience Manager] as a Cloud Service の 2024.3.0 バージョンの機能リリースノートの概要について説明します。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2021年、2022年）のリリースノートに移動できます。
>
>[!DNL Experience Manager] as a Cloud Service の今後の機能のアクティベーションについての詳細は、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=ja)をご覧ください。

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の最新の機能リリース（2024.3.0）のリリース日は、2024年4月11日（PT）です。次回の機能リリース（2024.4.0）は 2024年4月25日（PT）に予定されています。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

## リリースビデオ {#release-video}

2024.3.0 リリースで追加された機能の概要については、2024年3月のリリースに関する概要ビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3428342?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### の新機能[!DNL Experience Manager Sites] {#sites-features}

**Edge Delivery Services 用の AEM オーサリング**

AEM Sites を Edge Delivery Services のコンテンツソースとして使用できるようになりました。作成者は、コンテキスト依存 wysiwyg オーサリングを備えた新しいユニバーサルエディターを使用して、AEM で web サイトを管理します。これにより、企業は Edge Delivery Services を使用して高速でパフォーマンスの高い web ページを構築できるだけでなく、コンテンツ管理に AEM の強力な機能を活用できます。

![AEM オーサリング](/help/edge/assets/universal_editor_edge_delivery_services.png)

詳しくは、[ドキュメント](/help/edge/overview.md)および [AEM Gems - AEM オーサリングと Edge Delivery Services の概要](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/aem-gems-getting-started-with-aem-authoring-and-edge-delivery/m-p/652694?profile.language=ja#M43905)を参照してください。

**ヘッドレス実装用のユニバーサルエディター**

また、ユニバーサルエディターを使用すると、分離された web アプリケーションでも、従来の Sites 専用のそれと同じ直感的なコンテキスト依存の WYSIWYG オーサリングを利用できます。コンテンツ作成者は、コンテンツフラグメントを使用して、ページ内のコンポーネントと同じ容易さで、レイアウトを視覚的に作成できるようになりました。

ユニバーサルエディターの最大の特徴は、様々な web アーキテクチャへの適応性、サーバーサイドとクライアントサイドの両方のレンダリングへの対応、フレームワークに依存しない、AEM ホスティングの必要性を排除していることです。既存の web アプリケーションとコンテンツ編集用のユニバーサルエディターの統合は簡単です。主に、開発者が特定のデータ属性をマークアップに組み込む必要があります。

これにより、ユニバーサルエディターは、コンテンツ構造や基盤となるテクノロジースタックに関係なく、一貫した編集エクスペリエンスを提供します。詳しくは、[ユニバーサルエディターの概要](/help/implementing/universal-editor/introduction.md)を参照してください。

**コンテンツフラグメントとモデルのコンテンツ管理 OpenAPI**

開発者は、コンテンツフラグメントとコンテンツフラグメントモデルをプログラムで操作し、コンテンツ管理 OpenAPI を使用して、CruD 操作を実行できるようになりました。詳しくは、[API のドキュメント](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)を参照してください

**エクスペリエンスフラグメントのマルチサイト管理のサポート**

マルチサイト管理のサポートがエクスペリエンスフラグメントを保存するフォルダー構造に対して拡張されたので、ユーザーがエクスペリエンスフラグメントを含む完全なコンテンツ構造をロールアウトできるようになりました。

**コンテンツフラグメントのバージョンの比較**

新しいコンテンツフラグメントエディターでは、コンテンツ作成者は、コンテンツフラグメントの現在のバージョンと以前のバージョンの違いを比較して表示できるようになりました。

### 早期導入プログラム {#sites-early-adopter}

**バリエーションを生成**

AEM の新機能を通じて GenAI を活用し、[バリエーションを生成](/help/generative-ai/generate-variations.md)し、クラウドサービスでアクセスできるようになりました。バリエーションを生成は、生成 AI を使用してコンテンツの作成を生成し拡張するのに役立ちます。プログラムでの検討については、アドビのアカウントチームにお問い合わせください。

**コンテンツフラグメントコンソールでのアセットのブラウジング**

コンテンツ作成者は、コンテンツフラグメントコンソールを離れることなく、画像やその他のアセットを参照、表示およびアクションを実行できるようになりました。

![アセットブラウジング](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-browse.png)

この機能を試してフィードバックを共有いただける場合早期導入プログラムの詳細をご案内いたしますので、ご自身の正式なメール ID から aemcs-headless-adopter@adobe.com までご連絡ください。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 管理ビューの新機能 {#admin-view}

**Adobe Express とのネイティブ統合**

AEM Assets は Adobe Express とネイティブに統合されているので、Adobe Express ユーザーインターフェイス内から AEM Assets に保存されているアセットに直接アクセスできます。AEM Assets で管理されているコンテンツを Express キャンバスに配置し、新しいコンテンツや編集したコンテンツを AEM Assets リポジトリに保存できます。

![Assets アドオンのアセットを含める](/help/assets/assets/adobe-express-native-integration.png)

**サポートされるすべてのビデオタイプのレンディションのプレビュー**

Experience Manager Assets では、処理プロファイル設定を行わなくても、サポートされるすべてのビデオタイプのプレビューレンディションをデフォルトで生成するようになりました。

### アセットビューの新機能 {#assets-view}

**コレクションの権限の管理**

Assets Essentials では、管理者は、リポジトリで使用可能なプライベートコレクションのアクセスレベルを管理できます。管理者は、ユーザーグループを作成し、それらのグループに権限を割り当てて、アクセスレベルを管理できます。また、ユーザーグループに権限管理の権限をデリゲートすることもできます。


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### AEM Forms の新機能 {#forms-new-features}

* **[Adobe Experience Manager Forms Edge Delivery Services](/help/edge/docs/forms/overview.md)**: Edge Delivery Services for AEM Forms is a composable set of services that enables a rapid development environment where authors can update, publish, and launch new forms rapidly. これらのサービスは、エンゲージメントとコンバージョンを促進する、優れた効果の高いフォームエクスペリエンスを提供します。これらのフォームエクスペリエンスは、簡単に作成および開発できます。

  ![EDS Forms の機能](/help/edge/assets/eds-forms-features.png)

これらのサービスにより、次のことが可能になります。

* 同じフォームサイト上で複数のコンテンツソースを操作し、Microsoft Excel、Google Sheets、アダプティブフォームエディターなどの推奨オーサリングツールを使用します。
* Deliver Digital Enrollment experiences that load and render quickly and continuously monitor your forms performance through real use monitoring (RUM).
* プレーン HTML、最新の CSS、Vanilla JavaScript を使用して優れたエクスペリエンスを作成し、特定のフレームワークの急な学習曲線を回避します。


### AEM Forms のプレリリースでの新機能 {#forms-pre-release}

* **コアコンポーネントベースのアダプティブフォーム向けビジュアルルールエディターの機能強化**：このリリースでは、コアコンポーネントベースのアダプティブフォームのビジュアルルールエディターが大幅にアップグレードされました。このリリースでは、コアコンポーネントベースのアダプティブフォームのビジュアルルールエディターが大幅にアップグレードされました。この更新では、より堅牢で効率的なフォームを作成できるように、カスタム関数とのインタラクションを効率化することに焦点を当ています。

  次の方法で、カスタム関数とのインタラクションを効率化できるようになりました。

   * 新しい注釈を活用すると、より明確な機能定義を行えます。
   * カスタム関数にキャッシュメカニズムを使用すると、フォームのパフォーマンスが向上します。
   * カスタム関数内のグローバルオブジェクトをシームレスに操作できます。
   * カスタム関数内でのオプションのパラメーターを定義して利用します。

  このアップデートでは、ルールエディターの機能にも次の機能強化が追加されています。次の操作を実行できます。

   * 条件付き実行に強力な「when-then-else」ロジックを実装します。
   * let 関数や arrow 関数などの最新の JavaScript 機能を活用します（ES10 サポート）。
   * フィールドだけでなく、パネルやフォーム全体を検証またはリセットして、ユーザー操作のコントロールを拡大します。

  これらの機能強化により、ビジュアルルールエディター内でルールやカスタム関数を作成する際のエクスペリエンスが、より直感的かつ強力になります。

* **アダプティブフォームの複数バージョンの作成**：既存フォームのバリエーションを簡単に管理できるようになりました。これにより、合理化された単一のワークフロー内で、バージョン管理をシンプルに、フォーム最適化の比較を容易に行えるようになります。

* **アダプティブフォームの比較**：2 つのフォームを簡単に比較して、その違いを特定できるようになりました。チームメンバーがリビジョンを比較し、変更を効率的に議論できるので、共同作業がスムーズになります。

* **手書き署名コンポーネントのアクセシビリティの強化**：このアップデートにより、手書き署名コンポーネントのアクセシビリティが大幅に向上しました。

  **キーボードナビゲーションの向上：**
   * Tab キーを押すと、署名ダイアログボックス内のすべてのインタラクティブ要素間を移動できます。
   * ブラシまたはキーボードで署名して Enter キーを押すと、ダイアログが閉じます。
   * 署名して「OK」をクリックした後も、フォーカスは署名コントロールに残ります。

  **署名のクリア機能：**

   * Tab キーを使用すると、署名を消去するための消去クロスアイコンにアクセスできます。
   * 「署名のクリアを確認」ダイアログには、タブナビゲーションからもアクセスできます。

  **ラベルとコントロールの機能強化：**
   * キーボード署名ボタンのラベルがよりわかりやすくなり、「aria-label」を使用して機能を通知します（「aria-label=キーボードを使用して署名」など）。
   * コントラストが向上し、手書き署名内のすべてのコントロールを簡単に区別できるようになりました。
   * OK／チェックマークボタンが、非アクティブの場合でも視覚的に示されるようになりました。

  **スクリーンリーダーの署名フィードバック：**
   * 署名を入力すると、スクリーンリーダーのユーザーは、署名の作成に使用されるテキストを聞くことができます。

このアップデートにより、手書き署名コンポーネントのナビゲーション、明確さ、フィードバックを向上し、障がいのあるユーザーにとってより包括的なエクスペリエンスになります。

### 早期導入プログラム {#forms-early-adopter}

* **[Adobe Workfront Fusion シナリオへのアダプティブフォームの送信](/help/forms/submit-adaptive-form-to-workfront-fusion.md)**：Forms as a Cloud Service には、アダプティブフォームを Adobe Workfront に簡単に接続するための標準オプションが用意されています。これにより、Adobe Workfront シナリオにアダプティブフォームを送信するプロセスが簡単になり、アダプティブフォームの送信時に Workfront Fusion シナリオをトリガーできます。

  <br/> ![Adobe Workfront](/help/forms/assets/adobe-workfront.png) <br/> Adobe Workfront Fusion コネクタを使用すると、アダプティブフォームの送信時に自動的にトリガーされるワークフローを設計できます。例えば、送信されたデータを確認するタスクを特定の個人に割り当てるワークフローが開始され、アダプティブフォームから取り込まれた情報に基づいて、申し込みの承認または拒否ができるようになるシナリオを想定します。この合理化された統合によって効率が上がり、ワークフロープロセスの自動化が新たな段階に引き上げられます。

* **Reader Extension サービス**：AEM Forms Communication API では Reader Extension サービスを導入しました。通常の PDF にフォーム入力やコメントなどの機能を追加できるので、無料の Adobe Reader を使ってユーザーが PDF をインタラクティブに使用できるようになります。

* [右横書き言語のサポート](/help/forms/supporting-new-language-localization-core-components.md)：コアコンポーネントに基づいて作成されたアダプティブフォームを、アラビア語、ペルシア語、ウルドゥー語などの右横書き（RTL）言語で表示できるようになりました。RTL 言語は、世界中で 20 億人以上の人々が話しています。RTL 言語のフォームを使用すると、アダプティブフォームのリーチを拡大して、これらの多様なオーディエンスに対応し、RTL マーケットを選択できます。また、特定の地域では、現地の言語でフォームを提供することは法的義務として定められています。現地の言語に対応することで、より幅広いオーディエンスに扉を開くだけでなく、関連する法律や規制を確実に遵守できます。

* **[DocAssurance API（通信 API の一部）を使用したドキュメントの保護](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**：DocAssurance API を使用すると、ドキュメントに署名および暗号化して、機密情報を保護できます。暗号化により、ドキュメントのコンテンツは読み取り不可能な形式に変換され、許可されたユーザーのみがアクセスできるようになります。この強化された保護層は、貴重なデータを信頼できない環境にさらすことなく、安心感ももたらします。Signature API を使用すると、組織は配布および受信する Adobe PDF ドキュメントのセキュリティとプライバシーを保護できます。このサービスでは、デジタル署名と証明書を使用して、意図された受信者のみがドキュメントを変更できるようにします。

  公式メール ID から `aem-forms-ea@adobe.com` に送信して早期導入プログラムに参加し、機能へのアクセスをリクエストできます。

* **[You can leverage the Real Use Monitoring (RUM) Data Service](/help/implementing/cloud-manager/content-requests.md#real-user-monitoring-for-aem-as-a-cloud-service)** to enable client-side collection for AEM as a Cloud Service.
実際の使用のモニタリング（RUM）データサービスは、ユーザーインタラクションをより正確に反映し、web サイトのエンゲージメントの信頼性の高い測定を保証します。ページのパフォーマンスに関する高度なインサイトを取得する絶好の機会です。 これは、アドビが管理する CDN やアドビ以外が管理する CDN を使用するお客様にとって有益です。さらに、アドビ以外が管理する CDN を使用しているお客様は、自動トラフィックレポートを有効にできるようになり、アドビとトラフィックレポートを共有する必要がなくなります。

  この新機能をテストしてフィードバックを共有することに興味がある場合は、Adobe ID に関連付けられたメールアドレスから、RUM を有効にする各環境のドメイン名を添付して、`aemcs-rum-adopter@adobe.com` にメールを送信してください。Adobe&#39;s product team will then enable the Real Use Monitoring (RUM) Data Service for you.

## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### 早期導入プログラム {#foundation-early-adopter}

#### トラフィックフィルタールールアラート（早期導入プログラム） {#traffic-filter-rules-alerts-early-adopter}

最近リリースされた[トラフィックフィルタールール](/help/security/traffic-filter-rules-including-waf.md)には、オプションでライセンス可能な web アプリケーションファイアウォール（WAF）ルールが含まれており、許可または拒否するトラフィックを設定できます。

**<aemcs-cdn-config-adopter@adobe.com>** にメールを送信して早期導入プログラムに参加すると、トラフィックフィルタールールがトリガーされるたびにアラートを受け取ることができます。特定のトラフィック状況が発生するとアクションセンターのメール通知が送信されるので、適切な対策を講じることができます。

#### CDN 設定（早期導入プログラム） {#cdn-config-early-adopter}

オプションでライセンス可能な web アプリケーションファイアウォール（WAF）ルールを含む、最近リリースされた[トラフィックフィルタールール](/help/security/traffic-filter-rules-including-waf.md)の他に、設定パイプラインを使用して、他のタイプの CDN 設定を宣言およびデプロイすることもできます。[詳細情報](/help/implementing/dispatcher/cdn-configuring-traffic.md)を確認し、**<aemcs-cdn-config-adopter@adobe.com>** にメールを送信して早期導入プログラムに参加し、次の情報にアクセスしてください。

* 301/302 server-side redirects
* 任意の接触チャネルに対するエッジでのリクエストのプロキシ処理（AEM 以外のアプリケーションなど）
* URL 変換
* リクエストヘッダーまたは応答ヘッダーの設定または変更
* CDN が AEM に到達できない場合のカスタムエラーページ

#### Apache／Dispatcher ランタイムによる書き換えマップの取り込み（早期導入プログラム） {#apache-rewritemaps-early-adopter}

AEM 6.5 と同様に、Apache／Dispatcher は、web 階層パイプラインの実行を必要とせずに、公開リポジトリ内の特定の場所に配置された書き換えマップを取り込んで読み込みます。これにより、ビジネスユーザーが、ACS Commons リダイレクトマップマネージャーが提供するような UI を使用して、リダイレクトを宣言する機会が広がります。詳しくは **<aemcs-cdn-config-adopter@adobe.com>** までご連絡ください。

#### 動的コンテンツを読み込むためのエッジサイドインクルード（ESI）（早期導入プログラム） {#esi-early-adopter}

アドビが管理する CDN で、エッジレベルの動的 web コンテンツアセンブリ用のマークアップ言語であるエッジサイドインクルード（ESI）がサポートされるようになりました。ESI スニペットを含めることで、より大きい TTL で HTML ページ全体を CDN にキャッシュしながら、より頻繁なアップデート（小さい TTL）を必要とする小さなセクションを、接触チャネルから頻繁に取得できます。詳しくは **<aemcs-cdn-config-adopter@adobe.com>** までご連絡ください。

#### サイトテーマとサイトテンプレートを使用したフロントエンドコードの RDE サポート（早期導入プログラム） {#rde-frontend-early-adopter}

[迅速な開発環境（RDE）](/help/implementing/developing/introduction/rapid-development-environments.md)は、早期導入者向けに、[サイトテーマ](/help/sites-cloud/administering/site-creation/site-themes.md)と[サイトテンプレート](/help/sites-cloud/administering/site-creation/site-templates.md)に基づいたフロントエンドコードをサポートするようになりました。RDE では、[フロントエンドパイプライン](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md)ではなくコマンドラインディレクティブを使用して行われます。試用してフィードバックを提供するには、**<aemcs-rde-support@adobe.com>** までご連絡ください。

#### RDE ロギングの強化（早期導入プログラム） {#rde-logging-early-adopter}

[迅速な開発環境（RDE）](/help/implementing/developing/introduction/rapid-development-environments.md)でコードをデバッグする際、バージョン管理で OSGI プロパティを変更することなく、コマンドラインを使用して、開発者がより効率的にログを設定し、ストリーミングできるようになりました。次のような機能があります。

* パッケージまたはクラスレベルごとのログレベルの宣言
* ログ出力形式のカスタマイズ
* 複数のログを並行してストリーミング

試してフィードバックを提供するには、**<aemcs-rde-support@adobe.com>** までご連絡ください。

## Cloud Manager {#cloud-manager}

Cloud Manager の月次リリースの完全なリストは、[こちら](/help/implementing/cloud-manager/release-notes/current.md)で確認できます。

## 移行ツール {#migration-tools}

移行ツールのリリースの完全なリストは、[こちら](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)で確認できます
