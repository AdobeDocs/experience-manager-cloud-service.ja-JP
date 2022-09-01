---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2022.7.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2022.7.0 リリースのリリースノート。'
source-git-commit: b1c4706d2d148c136eed66b0bff6f792a89e9d8c
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 19%

---


# [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート {#release-notes}

以下では、[!DNL Experience Manager] as a Cloud Service の現在（最新）のバージョンのリリースノート全般の概要を説明します。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2020 年、2021 年のバージョンなど）のリリースノートに移動できます。

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の現在のリリース（2022.7.0）のリリース日は 2022年8月8日（PT）です。


次回のリリース (2022.8.0) は、2022 年 9 月 1 日 (PT) に予定されています。

## リリースビデオ {#release-video}

2022.7.0 リリースに追加された機能の概要については、 2022 年 7 月リリースの概要ビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/345409/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### の新機能[!DNL Sites] {#sites-features}

* この [コンテンツフラグメントコンソール](/help/sites-cloud/administering/content-fragments/content-fragments-console.md) がサポートされるようになりました [キーボードショートカット](/help/sites-cloud/administering/content-fragments/content-fragments-console-keyboard-shortcuts.md).

* AEM as aCloud Service [web に最適化された画像配信](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/web-optimized-image-delivery.html) を使用すると、WebP などの形式を配信することで、ページの速度を大幅に向上できます。 この新しいサービスでは、より柔軟に画像のサイズを変更したり、変換したりすることもできます。 のすべてのバージョン [コア画像コンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html?lang=ja) を使用すると、このサービスを利用し、画像コンポーネントのポリシーのオプションをクリックして、画像を WebP として配信できます。

* AEMのパーソナライゼーションアクティビティは、従来のオファーの代わりにエクスペリエンスフラグメントを利用できるようになりました。 この機能：
   * 従来のライブラリオファーではなく、AEMコンテンツでエクスペリエンスフラグメントオファーを促進する移行パスを有効にして、大規模なパーソナライゼーションに合わせて適切にスタイル設定されたコンテンツを提供します。
   * は、コンテンツ作成者が誤ってサイトでスタイル設定されていないコンテンツを提供するのを防ぎます。
   * を使用すると、任意のコンポーネントのターゲットモードを、編集可能なテンプレートを使用するエクスペリエンスフラグメント (JSON とHTMLタイプの両方 ) に変換できます。

>[!NOTE]
>
>既にレガシーオファーを使用している既存のパーソナライゼーションアクティビティでも引き続き使用できますが、今後推奨されるアプローチなので、新しいパーソナライゼーションアクティビティをエクスペリエンスフラグメントとして作成する必要があります。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] プレリリースチャネルで利用できる新機能 {#prerelease-features-assets}

Adobe Experience Manager Assets を [MIME タイプに基づいてユーザーがアップロードできるアセットのタイプを制限します](/help/assets/configure-asset-upload-restrictions.md).

![アセットのアップロード制限](/help/assets/assets/asset-upload-restrictions.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### の新機能[!DNL Forms] {#forms-features}

* **[手書き署名のキーボード入力のサポート](/help/forms/signing-forms-using-scribble.md)**:アダプティブFormsは、タッチデバイスでの使用が増えています。一般的な要件の 1 つは、署名をサポートすることです。 タッチデバイスでのドキュメントの署名は、フォームの署名方法として受け入れられるようになりました。 アダプティブFormsでは、このような使用例に対して、Scribble Signatures およびAdobe Signをネイティブでサポートしています。 これで、既にサポートされている他のオプションと共に、キーボードを使用してアダプティブフォーム内の手書き署名を行うこともできます。 また、アクセシビリティのコンプライアンスの向上にも役立ちます。

![iPhone での手書き署名のキーボード入力のサポート](/help/release-notes/assets/scribble-keyboard-mobile.png)

* **ローカル言語でのアダプティブFormsウィザードの使用**:ウィザードは、選択した言語で使用できます。 Adobe Experience Managerでサポートされているすべての言語をサポートするようになりました。

### [!DNL Forms] プレリリースチャネルで利用できる新機能 {#prerelease-features-forms}

<!-- 

* **[Launch Adaptive Form creation wizard from embed form component](/help/forms/using/embed-adaptive-form-aem-sites.md)**: You can now launch Adaptive Form creation wizard from embed form component. It helps improve content and forms authoring workflows for Sites and Forms practitioners trying to add enrollment experiences to a web page. 

![Keyboard input support for Scribble signatures on iphone](/help/release-notes/assets/froms-container.png) 

-->

* **[Invoke DDX - An AEM Workflow step](/help/forms/aem-forms-workflow-step-reference.md#invokeddx)**:Document Description XML (DDX) は、宣言的なマークアップ言語です。この言語の要素は、ドキュメントの構築ブロックを表します。 これらの構築ブロックには、PDFおよび XDP ドキュメントと、コメント、しおり、スタイル設定されたテキストなどのその他の要素が含まれます。 DDX ドキュメントはドキュメントのテンプレートで、結果のドキュメントに表示するソースドキュメントの必要な特性を記述します。 1 つの DDX を様々なソースドキュメントと共に使用できます。 AEMワークフローを起動ステップを使用して、ドキュメントの分解、Acrobatと XFA Formsの作成と変更、および [DDX リファレンス](https://helpx.adobe.com/content/dam/help/en/experience-manager/forms-cloud-service/ddxRef.pdf) ドキュメント。

* **[PDF/A に変換 — AEMワークフローステップ](/help/forms/aem-forms-workflow-step-reference.md##convert-pdfa)**:PDF/A は、ドキュメントのコンテンツを長期保存するためのアーカイブ形式で、すべてのフォントが埋め込まれ、ファイルが非圧縮になります。 これで、PDF/A に変換ステップを使用して、任意の形式のドキュメントまたはファイルをPDF/A 形式に変換できます。


## CIF アドオン {#cloud-services-cif}

### 新機能 {#what-is-new-cif}

* 製品カタログのエンリッチメントでAEMページがサポートされるようになりました。 これにより、作成者はページと製品の関連付けを管理できます。

* CIF コアコンポーネントの様々な改善点

### バグ修正 {#bug-fixes-cif}

* クライアント側の価格取得にログイントークンを追加

* データレイヤーのページコンポーネントが正しくありません

## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### 新機能 {#what-is-new-foundation}

* この [リポジトリブラウザ](/help/implementing/developing/tools/repository-browser.md) にパス入力フィールドが追加され、リポジトリ階層内の特定のフォルダーに直接ジャンプできるようになりました。
* Sling コンテンツ配布 (SCD) で、コンテンツが公開されずにコンテンツを無効にするための明示的な「無効化」アクションがサポートされるようになりました。 詳しくは、 [AEMでのキャッシュのas a Cloud Service](/help/implementing/dispatcher/caching.md#explicit-invalidation) ページを参照してください。
* mod_macro がAEM as a Cloud Serviceで使用できるようになりました。 参照： [このテーブル](/help/implementing/dispatcher/disp-overview.md) を参照してください。

### AEMas a Cloud ServiceSDK Dispatcher ツールの機能強化 {#dispatcher-tools-enhancements}

* Apache は `docker_run_hot_reload.sh` スクリプトを自動的に読み込み、その後の apache および dispatcher 設定の変更を検証するので、開発者の速度が向上します。 Dispatcher ツールの柔軟なモードでのみサポートされます。 また、 [Apache および Dispatcher 設定のデバッグ](/help/implementing/dispatcher/validation-debug.md#automatic-reloading) を参照してください。
* ローカルの Apache/Dispatcher 設定では、クラウド環境の変更をより詳細に追跡し、2 つの環境間のパリティを増やします。

### [!DNL Experience Manager] プレリリースチャネルで利用できる新機能 {#prerelease-features-foundation}

* AEM as a Cloud Serviceが統合シェルと統合され、ユーザーエクスペリエンスが向上し、他のすべてのExperience Cloudアプリケーションと統合されました。 参照： [統合シェルでas a Cloud ServiceのAEMを使用](/help/overview/aem-cloud-service-on-unified-shell.md) を参照してください。

## Adobeラーニングマネージャーコネクタ {#learn-manage}

* 新しいAdobeラーニングマネージャーには、Adobe Experience Manager Sites、Marketo Engage、Adobe Commerceへのコネクタが含まれます。 詳しくは、以下を参照してください。 [Adobeラーニングマネージャーユーザーガイド](https://helpx.adobe.com/learning-manager/user-guide.html).

## Cloud Manager {#cloud-manager}

Cloud Manager の月次リリースの完全なリストは、[こちら](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md)で確認できます。

## 移行ツール {#migration-tools}

移行ツールのリリースの完全なリストは、[こちら](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)で確認できます
