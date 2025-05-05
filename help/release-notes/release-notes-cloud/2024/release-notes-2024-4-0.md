---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2024.4.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2024.4.0 リリースのリリースノート。'
exl-id: 153a3172-676f-4434-94d4-12fab8e17734
feature: Release Information
role: Admin
source-git-commit: 7069ee2453b0c589f92f9899db0b8307e4133756
workflow-type: tm+mt
source-wordcount: '2707'
ht-degree: 97%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の 2024.4.0 リリースノート {#release-notes}

以下の節では、[!DNL Experience Manager] as a Cloud Service の 2024.4.0 バージョンの機能リリースノートの概要について説明します。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2021年、2022年）のリリースノートに移動できます。
>
>[!DNL Experience Manager] as a Cloud Service の今後の機能のアクティベーションについての詳細は、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=ja)をご覧ください。

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の最新の機能リリース（2024.4.0）のリリース日は、2024年4月25日（PT）です。次回の機能リリース（2024.5.0）は 2024年5月30日（PT）に予定されています。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

## リリースビデオ {#release-video}

2024.4.0 リリースで追加された機能の概要については、2024年4月リリースの概要ビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3429111?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### 早期導入プログラム {#sites-early-adopter}

**バリエーションを生成**

AEM の新機能を通じて GenAI を活用し、[バリエーションを生成](/help/generative-ai/generate-variations.md)し、クラウドサービスでアクセスできるようになりました。バリエーションを生成は、生成 AI を使用してコンテンツの作成を生成し拡張するのに役立ちます。プログラムでの検討については、アドビのアカウントチームにお問い合わせください。

**コンテンツフラグメントコンソールでのアセットのブラウジング**

コンテンツ作成者は、コンテンツフラグメントコンソールを離れることなく、画像やその他のアセットを参照、表示およびアクションを実行できるようになりました。

![アセットブラウジング](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-browse.png)

この機能を試してフィードバックを共有いただける場合早期導入プログラムの詳細をご案内いたしますので、ご自身の正式なメール ID から aemcs-headless-adopter@adobe.com までご連絡ください。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### アセットビューの新機能 {#assets-view-new-features}


**コンテキスト検索**

また、[テキストプロンプトを定義して、リポジトリで使用可能なアセットを検索](/help/assets/search-assets-view.md#contextual-search)することもできるようになりました。Experience Manager Assets は、これらのテキストプロンプトを検索フィルターに自動変換し、検索結果を表示します。フィルターペインを使用して自動フィルターを表示および変更すると、検索結果をさらに絞り込むことができます。

![コンテキスト検索](/help/assets/assets/contextual-search-text-prompt1.png)

**ビデオのクイックアクションの高速化**

Experience Manager Assets には、[Adobe Express を活用した簡単で直感的なビデオ編集ツール](/help/assets/edit-videos-assets-view.md)が含まれており、コンテンツの再利用を増やし、コンテンツの速度を高速化します。編集オプションには、ビデオのトリミング、切り抜き、サイズ変更、MP4 から GIF ファイルへの変換などが含まれます。

![Adobe Express を使用したビデオの切り抜き](/help/assets/assets/adobe-express-crop-video.png)

**動的レンディション**

Experience Manager Assets で、[動的レンディション（スマート切り抜きを含む）の表示とダウンロード](/help/assets/renditions.md)が可能になりました。動的レンディションは、特定のニーズに合うようにリアルタイムで作成される、カスタマイズされた画像アセットバージョンです。例えば、デバイスの解像度に基づく画像のサイズ変更や、様々な縦横比に合わせた切り抜きなどです。これらのレンディションにより、組織は、様々なオーディエンスニーズに合わせて、パーソナライズされ最適化されたエクスペリエンスを提供できます。

![動的レンディション](/help/assets/assets/preset_smart_crop.png)

**アセットおよびフォルダーのインプレース名前変更**

Experience Manager Assets では、[シングルクリックでアセットまたはフォルダーの名前を変更できる機能](/help/assets/manage-organize-assets-view.md)を提供して、簡素化されたユーザーエクスペリエンスを提供するようになりました。

**複数のフォルダーへのメタデータフォームの割り当てまたは削除**

[複数のフォルダーにメタデータフォームを割り当てる、または削除](/help/assets/metadata-assets-view.md#assign-metadata-form-to-a-folder)できるようになりました。

### 管理ビューの新機能 {#admin-view-new-features}

**リンク共有設定**

[リンク共有の作成](/help/assets/share-assets.md)で新しい改善されたユーザーエクスペリエンスが実現し、さらにユーザーに対するこの機能のデフォルトの動作を管理者がカスタマイズできる、まったく新しい設定セットが追加されました。

![ リンク共有設定 ](/help/assets/assets/config-email-service.png)



## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### AEM Forms の新機能 {#forms-new-features}

* **コアコンポーネントベースのアダプティブフォーム向けビジュアルルールエディターの機能強化**：このリリースでは、コアコンポーネントベースのアダプティブフォームのビジュアルルールエディターが大幅にアップグレードされました。このリリースでは、コアコンポーネントベースのアダプティブフォームのビジュアルルールエディターが大幅にアップグレードされました。この更新では、より堅牢で効率的なフォームを作成できるように、カスタム関数とのインタラクションを効率化することに焦点を当ています。

  次の方法で、カスタム関数とのインタラクションを効率化できるようになりました。

   * [新しい注釈を活用すると、より明確な機能定義を行えます](/help/forms/create-and-use-custom-functions.md#supported-javascript-annotations-for-custom-function)。
   * [カスタム関数にキャッシュメカニズムを使用すると、フォームのパフォーマンスが向上します](/help/forms/create-and-use-custom-functions.md#caching-support-for-custom-function)。
   * [カスタム関数内のグローバルオブジェクトをシームレスに操作できます](/help/forms/create-and-use-custom-functions.md#field-and-global-scope-objects-in-custom-functions)。
   * [カスタム関数内でのオプションのパラメーターを定義して利用します](/help/forms/create-and-use-custom-functions.md#parameter)。

  このアップデートでは、ルールエディターの機能にも次の機能強化が追加されています。次の操作を実行できます。

   * 条件付き実行に強力な[「when-then-else」](/help/forms/rule-editor-core-components.md#when)ロジックを実装します。
   * let 関数や arrow 関数などの最新の JavaScript 機能を活用します（ES10 サポート）。
   * フィールドだけでなく、パネルやフォーム全体を検証またはリセットして、ユーザー操作のコントロールを拡大します。

  これらの機能強化により、ビジュアルルールエディター内でルールやカスタム関数を作成する際のエクスペリエンスが、より直感的かつ強力になります。

* **[アダプティブフォームの複数バージョンの作成](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md)**：既存フォームのバリエーションを簡単に管理できるようになりました。これにより、合理化された単一のワークフロー内で、バージョン管理をシンプルに、フォーム最適化の比較を容易に行えるようになります。

* **[アダプティブフォームの比較](/help/forms/compare-forms.md)**：2 つのフォームを簡単に比較して、その違いを特定できるようになりました。チームメンバーがリビジョンを比較し、変更を効率的に議論できるので、共同作業がスムーズになります。

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

* **[Reader Extension サービス](/help/forms/aem-forms-cloud-service-communications-introduction.md#reader-extension-service)**：AEM Forms Communication API では Reader Extension サービスを導入しました。通常の PDF にフォーム入力やコメントなどの機能を追加できるので、無料の Adobe Reader を使ってユーザーが PDF をインタラクティブに使用できるようになります。

* [右横書き言語のサポート](/help/forms/supporting-new-language-localization-core-components.md)：コアコンポーネントに基づいて作成されたアダプティブフォームを、アラビア語、ペルシア語、ウルドゥー語などの右横書き（RTL）言語で表示できるようになりました。RTL 言語は、世界中で 20 億人以上の人々が話しています。RTL 言語のフォームを使用すると、アダプティブフォームのリーチを拡大して、これらの多様なオーディエンスに対応し、RTL マーケットを選択できます。また、特定の地域では、現地の言語でフォームを提供することは法的義務として定められています。現地の言語に対応することで、より幅広いオーディエンスに扉を開くだけでなく、関連する法律や規制を確実に遵守できます。

* **[DocAssurance API（通信 API の一部）を使用したドキュメントの保護](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**：DocAssurance API を使用すると、ドキュメントに署名および暗号化して、機密情報を保護できます。暗号化により、ドキュメントのコンテンツは読み取り不可能な形式に変換され、許可されたユーザーのみがアクセスできるようになります。この強化された保護層は、貴重なデータを信頼できない環境にさらすことなく、安心感ももたらします。Signature API を使用すると、組織は配布および受信する Adobe PDF ドキュメントのセキュリティとプライバシーを保護できます。このサービスでは、デジタル署名と証明書を使用して、意図された受信者のみがドキュメントを変更できるようにします。

  公式メール ID から `aem-forms-ea@adobe.com` に送信して早期導入プログラムに参加し、機能へのアクセスをリクエストできます。

* **[Real Use Monitoring （RUM） Data Service を利用すると](/help/implementing/cloud-manager/content-requests.md#real-user-monitoring-for-aem-as-a-cloud-service)**&#x200B;AEM as a Cloud Serviceのクライアントサイド収集を有効にできます。
実際の使用のモニタリング（RUM）データサービスは、ユーザーインタラクションをより正確に反映し、web サイトのエンゲージメントの信頼性の高い測定を保証します。ページのパフォーマンスに関する高度なインサイトを取得する絶好の機会です。 これは、アドビが管理する CDN やアドビ以外が管理する CDN を使用するお客様にとって有益です。さらに、アドビ以外が管理する CDN を使用しているお客様は、自動トラフィックレポートを有効にできるようになり、アドビとトラフィックレポートを共有する必要がなくなります。

  この新機能をテストしてフィードバックを共有することに興味がある場合は、Adobe ID に関連付けられたメールアドレスから、RUM を有効にする各環境のドメイン名を添付して、`aemcs-rum-adopter@adobe.com` にメールを送信してください。Adobeの製品チームが、Real Use Monitoring （RUM）データサービスを有効にします。

## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### CDN 設定 {#cdn-config}

次の方法で、アドビの CDN でのトラフィックを設定します。

* [リクエスト変換](/help/implementing/dispatcher/cdn-configuring-traffic.md#request-transformations) - 受信リクエストが AEM にルーティングされる前に、パス、クエリパラメーターおよび HTTP ヘッダーなど、受信リクエストの側面を変更します。
* [応答変換](/help/implementing/dispatcher/cdn-configuring-traffic.md#response-transformations) - 送信応答がブラウザーに提供される前に、送信応答の HTTP ヘッダーを変更します。
* [接触チャネルセレクター](/help/implementing/dispatcher/cdn-configuring-traffic.md#response-transformations#origin-selectors) - CDN 経由でトラフィックを AEM 以外のサイトやアプリケーションにルーティングします。

これらのルールをソース管理（Git）で宣言すると、Cloud Manager 設定パイプラインを使用して CDN にデプロイできます。また、以下の早期導入に関する節のクライアントサイドのリダイレクト機能も参照してください。

### カスタム CDN エラーページ {#cdn-error-pages}

万が一、CDN が AEM 接触チャネルにトラフィックをルーティングできない場合は、カスタムエラーページを宣言して、汎用バージョンを置き換えることができます。ブランドのエラーページを提供する方法について詳しくは、[こちら](/help/implementing/dispatcher/cdn-error-pages.md)を参照してください。

### 早期導入プログラム {#foundation-early-adopter}

#### サーバーサイドのリダイレクト（早期導入プログラム） {#server-side-redirects-early-adopter}

ソース管理で 301/302 サーバーサイドのリダイレクトを設定し、CDN にデプロイします。 [詳細情報](/help/implementing/dispatcher/cdn-configuring-traffic.md#server-side-redirectors)を確認し、早期導入プログラムに参加するには、**<aemcs-cdn-config-adopter@adobe.com>** にメールを送信してください。

#### トラフィックフィルタールールアラート（早期導入プログラム） {#traffic-filter-rules-alerts-early-adopter}

最近リリースされた[トラフィックフィルタールール](/help/security/traffic-filter-rules-including-waf.md)には、オプションでライセンス可能な web アプリケーションファイアウォール（WAF）ルールが含まれており、許可または拒否するトラフィックを設定できます。

**<aemcs-cdn-config-adopter@adobe.com>** にメールを送信して早期導入プログラムに参加すると、トラフィックフィルタールールがトリガーされるたびにアラートを受け取ることができます。特定のトラフィック状況が発生するとアクションセンターのメール通知が送信されるので、適切な対策を講じることができます。

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

## [!DNL Experience Manager] ガイド {#guides}

### 事前設定された言語グループを使用してコンテンツを複数の言語に翻訳する機能

Experience Manager Guides では、言語グループを作成し、コンテンツを複数の言語へと容易に翻訳できるようになりました。この機能は、組織のニーズに応じて翻訳を整理および管理するのに役立ちます。

例えば、ヨーロッパの一部の国向けにコンテンツを翻訳する必要がある場合、英語（EN）、フランス語（FR）、ドイツ語（DE）、スペイン語（ES）、イタリア語（IT）などのヨーロッパ言語の言語グループを作成できます。

![翻訳パネル](/help/release-notes/assets/guides/translation-languages-2404.png)

*ドキュメントを翻訳する言語グループまたは言語を選択します。*

>[!NOTE]
>
>言語のターゲットフォルダーが見つからない場合や、ターゲット言語がソース言語と同じ場合は、グレー表示され、警告サインが表示されます。

管理者は、言語グループを作成し、複数のフォルダープロファイルに設定できます。作成者は、フォルダープロファイルで設定されている言語グループを表示できます。


全体として、言語グループを作成すると、翻訳プロジェクトの効率と生産性が向上し、最終的には複数の言語にわたるローカライゼーションプロセスが向上します。


[Web エディターからドキュメントを翻訳](https://experienceleague.adobe.com/ja/docs/experience-manager-guides/using/user-guide/author-content/create-preview-topics/author-content-aem-guides/work-with-web-editor/translate-documents-web-editor)する方法を参照してください

### リポジトリビューでファイルを検索およびフィルタリングするためのエクスペリエンスの刷新

ファイルのフィルタリング時のエクスペリエンスが向上しました。ファイルをフィルタリングする刷新された機能によりファイルを簡単に検索および移動する方法が改善されました。

![リポジトリビューでファイルを検索](/help/release-notes/assets/guides/repository-filter-search-2404.png)

*テキスト`general purpose.`* を含むファイルを検索します

関連ファイルへの迅速なアクセスや、より直感的なユーザーインターフェイスなどのメリットが得られ、検索エクスペリエンスがよりスムーズかつ効率的になります。

![迅速な検索フィルター](/help/release-notes/assets/guides/repository-filter-search-quick.png)

*クイックフィルターを使用して、DITA ファイルと非 DITA ファイルを検索します。*

**フィルター検索**&#x200B;機能について詳しくは、[左パネル](https://experienceleague.adobe.com/ja/docs/experience-manager-guides/using/user-guide/author-content/create-preview-topics/author-content-aem-guides/work-with-web-editor/web-editor-features#id2051EA0M0HS)の節を参照してください。

### データソースコネクタの機能強化

2024.4.0 リリースでは、データソースコネクタに対して次の機能強化を行いました。

#### Salsify、Akeneo、Microsoft Azure DevOps Boards（ADO）データソースに接続

また、既存の標準コネクタに加えて、Experience Manager Guides では、Salsify、Akeneo、Microsoft Azure DevOps Boards（ADO）データソース用のコネクタも提供します。管理者は、これらのコネクタをダウンロードしてインストールできます。次に、インストールしたコネクタを設定します。

#### サンプルクエリをコピー＆ペーストし、コンテンツスニペットまたはトピックを作成

サンプルデータクエリをジェネレーターにコピー＆ペーストするだけで、コンテンツスニペットまたはトピックを作成できます。この機能を使用すると、構文を覚えたり、クエリを手動で作成したりする必要がありません。クエリを手動で入力する代わりに、サンプルクエリをコピー＆ペーストし、編集し、使用して要件に応じたデータを取得できます。

![コンテンツスニペットを挿入ダイアログボックス](/help/release-notes/assets/guides/insert-content-snippet.png)

*サンプルクエリをコピーして編集し、コンテンツスニペットを作成します。*

#### ファイルコネクタを使用して JSON データファイルに接続


管理者は、JSON データファイルをデータソースとして使用するように JSON ファイルコネクタを設定できるようになりました。コネクタを使用して、コンピューターまたは Adobe Experience Manager Assets から JSON ファイルを読み込みます。次に、作成者は、ジェネレーターを使用してコンテンツスニペットまたはトピックを作成できます。

この機能は、JSON ファイルに保存されたデータを使用し、様々なスニペット間で再利用するのに役立ちます。また、JSON ファイルを更新するたびに、コンテンツも動的に更新されます。

#### コネクタの複数のリソース URL を設定してコンテンツスニペットまたはトピックを作成

管理者は、Generic REST Client、Salsify、Akeneo、Microsoft Azure DevOps Boards（ADO）などの一部のコネクタに対して複数のリソース URL を設定できます。
次に、作成者は、ジェネレーターを使用してデータソースに接続し、コンテンツスニペットまたはトピックを作成します。この機能は、URL ごとにデータソースを作成する必要がないので便利です。これは、単一のコンテンツスニペットまたはトピック内の特定のデータソースのリソースからデータを迅速に取得するのに役立ちます。データソースコネクタの詳細と、[ユーザーインターフェイスからデータソースコネクタを設定](https://experienceleague.adobe.com/ja/docs/experience-manager-guides/using/install-guide/cs-ig/web-editor-configs-cs/conf-data-source-connector-tools)する方法を参照してください。[データソースからデータを使用](https://experienceleague.adobe.com/ja/docs/experience-manager-guides/using/user-guide/author-content/create-preview-topics/author-content-aem-guides/work-with-web-editor/web-editor-content-snippet)する方法を参照してください。

新機能および機能強化について詳しくは、[Experience Manager Guides リリース情報 ](https://experienceleague.adobe.com/ja/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap) を参照してください。

## Cloud Manager {#cloud-manager}

Cloud Manager の月次リリースの完全なリストは、[こちら](/help/implementing/cloud-manager/release-notes/current.md)で確認できます。

## 移行ツール {#migration-tools}

移行ツールのリリースの完全なリストは、[こちら](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)で確認できます
