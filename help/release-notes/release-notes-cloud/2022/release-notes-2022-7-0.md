---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.7.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.7.0 リリースのリリースノート。'
exl-id: b339ab48-e836-4589-a573-9c50917b9280
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 27%

---

# [!DNL Adobe Experience Manager] のas a Cloud Serviceに関する 202278.0 リリースノート {#release-notes}

以下の節では、[!DNL Experience Manager]as a Cloud Serviceの 2022.7.0 バージョンの機能リリースノートの概要を説明します。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2020 年、2021 年のバージョンなど）のリリースノートに移動できます。

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の最新リリース（2022.7.0）のリリース日は 2022年8月8日（PT）です。

次回のリリース（2022.8.0）は 2022 年 9 月 1 日（PT）に予定されています。

## リリースビデオ {#release-video}

2022.7.0 リリースで追加された機能の概要については、2022年7月リリースの概要ビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3454197/?quality=12&captions=jpn)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### の新機能[!DNL Sites] {#sites-features}

* [&#x200B; コンテンツフラグメントコンソール &#x200B;](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console) で [&#x200B; キーボードショートカット &#x200B;](/help/sites-cloud/administering/content-fragments/keyboard-shortcuts.md) がサポートされるようになりました。

* AEM as a Cloud Serviceの [web に最適化された画像配信 &#x200B;](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/web-optimized-image-delivery.html?lang=ja) を使用すると、WebP などの形式の配信によりページの速度を大幅に向上させることができます。 この新しいサービスでは、画像のサイズ変更や変換をより柔軟に行うこともできます。 [&#x200B; コア画像コンポーネント &#x200B;](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html?lang=ja) のすべてのバージョンでは、このサービスを使用し、画像コンポーネントのポリシーでオプションをクリックすることで、画像を WebP として配信できます。

* AEMのパーソナライゼーションアクティビティで、従来のオファーの代わりにエクスペリエンスフラグメントを使用できるようになりました。 この機能：
   * は、従来のライブラリオファーではなく、AEM コンテンツがエクスペリエンスフラグメントオファーを促進する移行パスを有効にして、今後の大規模なパーソナライゼーションに合わせて適切にスタイル設定されたコンテンツを提供します。
   * スタイル設定されていないコンテンツをコンテンツ作成者が誤ってサイトに提供するのを防ぐ。
   * 任意のコンポーネントのターゲティングモードを、編集可能なテンプレートを使用するエクスペリエンスフラグメント（JSON タイプとHTMLタイプの両方）に変換できる。

>[!NOTE]
>
>従来のオファーを既に使用している既存のパーソナライゼーションアクティビティは引き続き使用できますが、新しいパーソナライゼーションアクティビティはエクスペリエンスフラグメントとして作成する必要があります。これは今後のアプローチとして推奨されるからです。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] プレリリースチャネルで利用できる新機能 {#prerelease-features-assets}

Adobe Experience Manager Assetsを設定して [&#x200B; ユーザーがアップロードできるアセットのタイプを MIME タイプに基づいて制限 &#x200B;](/help/assets/configure-asset-upload-restrictions.md) できるようになりました。

![アセットアップロードの制限](/help/assets/assets/asset-upload-restrictions.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### の新機能[!DNL Forms] {#forms-features}

* **[手書き署名のキーボード入力のサポート](/help/forms/signing-forms-using-scribble.md)**：アダプティブFormsは、タッチデバイスでの使用が増えており、署名のサポートは一般的な要件の 1 つになっています。 タッチデバイスでのドキュメントへの署名は、フォームへの署名方法として受け入れられるようになりました。 アダプティブFormsでは、このようなユースケースに対して、手書き署名とAdobe Signをネイティブサポートしています。 これで、既にサポートされている他のオプションと共に、キーボードを使用してアダプティブフォームに手書き署名もできるようになりました。 また、アクセシビリティコンプライアンスの向上にも役立ちます。

![iphone での手書き署名のキーボード入力のサポート &#x200B;](/help/release-notes/assets/scribble-keyboard-mobile.png)

* **アダプティブFormsウィザードをローカル言語で使用**：選択した言語でウィザードを使用できます。 Adobe Experience Managerでサポートされているすべての言語をサポートするようになりました。

### [!DNL Forms] プレリリースチャネルで利用できる新機能 {#prerelease-features-forms}

<!-- 

* **[Launch Adaptive Form creation wizard from embed form component](/help/forms/using/embed-adaptive-form-aem-sites.md)**: You can now launch Adaptive Form creation wizard from embed form component. It helps improve content and forms authoring workflows for Sites and Forms practitioners trying to add enrollment experiences to a web page. 

![Keyboard input support for Scribble signatures on iphone](/help/release-notes/assets/froms-container.png) 

-->

* **[DDX の呼び出し – AEM ワークフローステップ](/help/forms/aem-forms-workflow-step-reference.md#invokeddx)**: Document Description XML （DDX）は宣言型マークアップ言語で、その要素はドキュメントの構築ブロックを表しています。 この構築ブロックには、PDF ドキュメント、XDP ドキュメントおよびその他の要素（コメント、しおり、スタイルを設定したテキストなど）が含まれます。DDX ドキュメントはドキュメントのテンプレートであり、結果のドキュメントに表示されるソースドキュメントの望ましい特性を記述します。 1 つの DDX を様々なソースドキュメントに使用できます。AEM ワークフローの呼び出しステップを使用して、ドキュメントの組み立てと分解、Acrobatと XFA Formsの作成と変更、[DDX リファレンス &#x200B;](https://helpx.adobe.com/content/dam/help/en/experience-manager/forms-cloud-service/ddxRef.pdf) ドキュメントに記載されているその他の操作など、様々な操作を実行できます。

* **[PDF/A に変換 – AEM ワークフローステップ](/help/forms/aem-forms-workflow-step-reference.md##convert-pdfa)**:PDF/A は、ドキュメントのコンテンツを長期保存するためのアーカイブ形式で、すべてのフォントが埋め込まれ、ファイルが圧縮されません。 AEM ワークフローの「PDF/A に変換」ステップを使用して、任意の形式のドキュメントまたはファイルをPDF/A 形式に変換できるようになりました。


## CIF アドオン {#cloud-services-cif}

### 新機能 {#what-is-new-cif}

* 製品カタログのエンリッチメントで AEM ページがサポートされるようになりました。 これにより、作成者はページと製品の関連付けを管理できます。

* CIF コアコンポーネントの様々な改善点

### バグ修正 {#bug-fixes-cif}

* クライアントサイドの価格取得にログイントークンを追加

* データレイヤーのページコンポーネントが正しくありません

## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### 新機能 {#what-is-new-foundation}

* [&#x200B; リポジトリブラウザー &#x200B;](/help/implementing/developing/tools/repository-browser.md) にパス入力フィールドが追加され、リポジトリ階層内の特定のフォルダーに直接ジャンプできるようになりました。
* Sling コンテンツ配布（SCD）で、コンテンツを公開せずに無効にするための明示的な「無効化」アクションがサポートされるようになりました。 詳しくは、[AEM as a Cloud Serviceでのキャッシュ &#x200B;](/help/implementing/dispatcher/caching.md#explicit-invalidation) ページを参照してください。
* mod_macro がAEM as a Cloud Serviceで使用できるようになりました。 サポートされている Apache モジュールのリストについては、[&#x200B; この表 &#x200B;](/help/implementing/dispatcher/disp-overview.md) を参照してください。

### AEM as a Cloud Service SDK Dispatcher ツールの機能強化 {#dispatcher-tools-enhancements}

* Apache を `docker_run_hot_reload.sh` スクリプトで起動すると、その後 Apache および Dispatcher 設定に対して行われた変更を自動的に読み込んで検証するので、開発者の速度が向上します。 Dispatcher ツールのフレキシブルモードでのみサポートされます。 また、自動再読み込みおよび検証について詳しくは、[Apache およびDispatcher設定のデバッグ &#x200B;](/help/implementing/dispatcher/validation-debug.md#automatic-reloading) も参照してください。
* ローカルの Apache および Dispatcher 設定では、クラウド環境の変更をより詳細に追跡するので、2 つの環境間の同等性が向上します。

### [!DNL Experience Manager] プレリリースチャネルで利用できる新機能 {#prerelease-features-foundation}

* AEM as a Cloud Service が統合シェルと統合され、ユーザーエクスペリエンスが向上し、他のすべての Experience Cloud アプリケーションと統合されました。詳しくは、統合シェルでの [AEM as a Cloud Service](/help/overview/aem-cloud-service-on-unified-shell.md) を参照してください。

## Adobe Learning Manager コネクタ {#learn-manage}

* 新しいAdobe Learning Managerには、Adobe Experience Manager Sites、Marketo EngageおよびAdobe Commerceへのコネクタが含まれています。 詳しくは、[Adobe Learning Manager ユーザーガイド &#x200B;](https://helpx.adobe.com/jp/learning-manager/user-guide.html) を参照してください。

## Cloud Manager {#cloud-manager}

Cloud Manager の月次リリースの完全なリストは、[こちら](/help/implementing/cloud-manager/release-notes/current.md)で確認できます。

## 移行ツール {#migration-tools}

移行ツールのリリースの完全なリストは、[こちら](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)で確認できます
