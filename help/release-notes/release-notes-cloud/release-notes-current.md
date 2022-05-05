---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 7ee2e43ab8a5726b2ecf7f157f67b5f3cc73fcff
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 26%

---


# [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート  {#release-notes}

以下では、[!DNL Experience Manager] as a Cloud Service の現在（最新）のバージョンのリリースノート全般の概要を説明します。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2020 年、2021 年のバージョンなど）のリリースノートに移動できます。

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

のリリース日 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 現在のリリース (2022.4.0) は 2022 年 5 月 6 日です。
次回のリリース (2022.5.0) は、2022 年 5 月 26 日に予定されています。

## リリースビデオ {#release-video}

以下をご覧ください： [2022 年 4 月リリースの概要](https://video.tv.adobe.com/v/342612?quality=12) 2022.4.0 リリースで追加された機能の概要を示すビデオです。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### の新機能[!DNL Sites] {#sites-features}

* コンテンツモデルのデータタイプを [翻訳可能な](/help/assets/content-fragments/content-fragments-models.md#properties) コンテンツモデルエディターでの単純なチェックボックスの使用 さらに、AEMの翻訳ルールと設定は自動的に更新されます。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### の新機能[!DNL Assets] {#assets-features}

* 次の操作を実行できます。 [タグを並べ替え](/help/assets/organize-assets.md#use-tags-to-organize-assets) タグ名、作成日または変更日に基づいて昇順または降順でタグピッカーウィンドウを表示します。


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] の新機能 {#what-is-new-forms}

* **通信 — Formsas a Cloud ServiceSDK でのドキュメント操作 API のサポート**: [ドキュメント操作 API](/help/forms/aem-forms-cloud-service-communications.md) ヘルプ：PDFドキュメントの組み合わせ、並べ替え、検証に役立ちます。 AEM Formsas a Cloud ServiceSDK を利用して、ローカル開発環境で通信 — ドキュメント生成 API を使用できるようになりました。

* **レコードのドキュメントの生成にカスタム XCI を使用**:次の操作を実行できます。 [カスタム XCI ファイルを使用してレコードのドキュメントの様々なプロパティを設定する](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#use-a-custom-xci-file). カスタムの変更でマスター XCI を上書きします。 レコードのドキュメントの生成をより詳細に制御し、パーソナライゼーションやカスタマイズの機会を増やします。

* **アダプティブフォーム内で非表示の CAPTCHA を使用する**:以下を使用して、 [CAPTCHA チャレンジを示す目に見えない CAPTCHA は、疑わしいアクティビティの場合にのみ CAPTCHA チャレンジを表示します](/help/forms/captcha-adaptive-forms.md). 疑わしいアクティビティが見つからない場合は、CAPTCHA チャレンジは表示されません。 これにより、チェックボックス要件を持たずに人間がフォームを完成させたかどうかを評価し、カスタマイズ作業を軽減し、エンドユーザーエクスペリエンスを向上させることができます。

* **フォームデータモデル設定**:次の操作を実行できます。 [複数の環境でフォームデータモデルの設定を再利用する](/help/forms/create-form-data-models.md#runmode-specific-context-aware-config)を使用すると、データ統合をシンプル化し、IT コストを削減できます。

## CIF アドオン {#cloud-services-cif}

### 新機能 {#what-is-new-cif}

* 製品コックピットにすばやくアクセス：サイトエディターでワンクリックで詳細な製品情報に簡単にアクセス

   ![ウィッシュリストを有効にする](/help/assets/CIF/enable-wishlist.png)

* 追加のマーケティングコマースコンポーネントのサポート：コンポーネントは、買い物かごへの追加と、リストへの追加のコールトゥアクションを表示するように設定できます。

   ![製品コックピットへのサイトエディターショートカット](/help/assets/CIF/sites-editor-shortcut-to-cockpit.png)

## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### SDK ビルドアナライザー {#sdk-build-analyzers}

AEM as a Cloud Service の SDK ビルドアナライザー Maven プラグインでは、依存関係の欠落など、Maven プロジェクトの問題を検出します。これを使用すると、ローカル開発中に、Cloud Manager でクラウド環境にデプロイする前に開発者が問題を見つけることができます。

新しいアナライザが最近追加されました。

* `content-packages-validation`  — デプロイメント中にインストールされるパッケージの適切な形式のコンテンツ構文および構造を検証します。

アナライザーの最新バージョンで Maven プロジェクトを更新するか、アナライザーを含めることを強くお勧めします（まだおこなっていない場合）。 詳しくは、[こちらのドキュメント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=ja)を参照してください。

## Cloud Manager {#cloud-manager}

Cloud Manager の毎月のリリースの完全なリストを確認できます [ここ](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md).

## ベストプラクティスアナライザー {#bpa-release}

### リリース日 {#release-date-bpa}

ベストプラクティスアナライザー v2.1.28 のリリース日は 2022 年 4 月 22 日です。

### 新機能 {#what-is-new-bpa}

* サポートされていない Asset Manager API の使用状況を検出し、レポートする機能。 AEM as a Cloud Serviceではサポートされなくなった API は 4 つあります。 お客様は、これらの API を使用しなくなり、新しいアセットアップロード方法を使用する必要があります。

* コンテンツフラグメントテンプレートの使用を検出する機能。 AEM as a Cloud Serviceでの新しいコンテンツフラグメントの作成で、コンテンツフラグメントテンプレートがサポートされなくなりました。 コンテンツフラグメントテンプレートを置き換えるには、コンテンツフラグメントモデルを作成する必要があります。

* リポジトリ内のアセットの metadate ノードの下に 100 を超える子孫を持つアセットを検出できます。 このようなアセットで構成されるフォルダーを読み込む際に、パフォーマンスを向上させるために必要でないメタデータノードを削除することをお勧めします。

* 使用されるデータストアのタイプを検出し、レポートする機能。

* AEM Form Portal のパターンが更新されました。

### バグの修正 {#bug-fixes-bpa}

* BPA は、お客様のコンポーネントに対してのみレポートするのではなく、コアコンポーネントの結果をレポートしていました。 この問題が修正されました。
