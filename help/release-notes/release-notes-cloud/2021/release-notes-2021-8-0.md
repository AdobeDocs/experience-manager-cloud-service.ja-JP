---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.8.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.8.0 リリースのリリースノート。'
source-git-commit: d37193833d784f3f470780b8f28e53b473fd4e10
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 39%

---


# [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート  {#release-notes}

以下では、[!DNL Experience Manager] as a Cloud Service の現在（最新）のバージョンのリリースノート全般の概要を説明します。

>[!NOTE]
>
>ここから、以前のバージョンのリリースノートに移動できます。例えば、2020、2021 の場合は、

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] のリリース日 (2021.8.0) は 2021 年 8 月 26 日です。
[!DNL Cloud Service]次のリリース (2021.9.0) は 2021 年 10 月 7 日です。

## Release Video {#release-video}

追加された機能の概要については、[2021 年 8 月リリースの概要 ](https://video.tv.adobe.com/v/336277) ビデオをご覧ください。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] の新機能 {#assets-features}

* デジタルアセットをリンクとして共有する場合、ユーザーは URL をすぐにクリップボードにコピーできます。 The enhancement lets you share assets in a faster and more convenient way. This functionality allows for faster and convenient asset sharing.

   ![アセットをリンクとして共有する場合の「 URL をコピー」オプション](/help/assets/assets/link-share-copy-URL-option.png)
   *図：アセットをリンクとして共有する場合、URL をコピーして別々に共有できるようになりました。*

* TXT ファイルをアップロードすると、アセットマイクロサービスによってサムネールが自動的に生成されます。 PNG サムネールは TXT ファイルのレンディションで、ユーザーがファイルを開かずに、コンテンツやファイルをある程度識別するのに役立ちます。 この機能は設定を必要とせず、デフォルトで機能します。

   ![TXT ファイルのレンディションは、PNG 形式でに [!DNL Assets] 自動的に生成されます](/help/assets/assets/thumbnail-rendition-txt-file.png)
   *図：TXT ファイルのレンディションが自動的に生成され、ファイルを開かずに識別できます。*

### [!DNL Assets] プレリリースチャネルの新機能 {#assets-prerelease-features}

* 列表示およびカード表示で、検索結果に表示されたアセットを並べ替えることができるようになりました。 並べ替えは、「名前」、「作成済み」、「変更済み」、「なし」の各列で行います。

   ![列表示およびカード表示での [!DNL Assets] 検索結果の並べ替え](/help/assets/assets/sort-searched-assets.png)
   *図：列表示およびカード表示で [!DNL Assets] 検索結果を並べ替えます。*

### [!DNL Assets] で修正されたバグ {#assets-bugs-fixed}

* コントリビューターグループのメンバーが [!DNL Assets] コンソールに移動すると、コレクションを作成するための追加の `POST` 要求が生成されます。 このリクエストは必須ではなく、権限の問題が原因で失敗し、多くのエラーがログに作成されます。 （CQ-4328856）
* ユーザーがアセットを表示し、左側のパネルのポップアップメニューから「[!UICONTROL  タイムライン ]」を選択すると、エラーが表示されます。 In the logs, many warnings are logged due to a bad query. （CQ-4328919）

## [!DNL Experience Manager Forms] as a  [!DNL Cloud Service] {#forms}

### [!DNL Forms] の新機能 {#what-is-new-forms}

* automated forms conversionサービスは、イタリア語とポルトガル語のPDF forms](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=ja#language-specific-meta-model) をアダプティブFormsに変換できます。[

* **AcroForm ベースのレコードのドキュメント**：AEM Forms as a Cloud Service では、XFA ベースのフォームテンプレート以外に、[Adobe Acrobat フォーム PDF（AcroForm PDF）](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html?lang=ja)をレコードのドキュメントのテンプレートとして使用できます。

* **Microsoft Azure データストアコネクタ**：[フォームデータモデルを Microsoft Azure Storage に接続](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html?lang=ja)できるようになりました。アダプティブフォームデータを取得して、Microsoft Azure ストレージに BLOB として保存することができます。

### [!DNL Forms] プレリリースチャネルで利用できる新機能 {#prerelease-features-forms}

* **アダプティブフォームでの Adobe Sign の役割の使用**：ビジネスおよびエンタープライズサービスレベルの Adobe Sign では、ワークフロー要件に適切に合致するように、契約書受信者の役割を署名者以外にも拡大できます。契約書の受信者ごとに、アダプティブフォームでの自分の役割を設定できるようになりました。デフォルトの役割は署名者です。

* **アダプティブフォーム用の Analytics**：アダプティブフォーム用の Adobe Analytics でエンドユーザーの行動を捉えて追跡し、エンドユーザーのインサイトを収集できるようになりました。十分な情報に基づいて決定をおこない、エンドユーザーエクスペリエンスを向上させることができます。

* **AEM FormsをMicrosoft Dynamics および Salesforce.com に簡単に接続**:このサービスは、すぐに使用できるデータソース設定と、Microsoft Dynamics および Salesforce.com 用のデータモデルを提供し、開発者がMicrosoft Dynamics および Salesforce.com をアダプティブフォームのデータソースとしてより迅速かつ簡単に設定できます。

## CIF アドオン {#cloud-services-cif}

### 新機能 {#what-is-new-cif}

* 新しいカテゴリピッカー UI により、ユーザーエクスペリエンスの向上、効率の向上、複雑な製品カタログのサポートの向上を実現

   ![新しいカテゴリピッカー](/help/assets/CIF/category-picker.png)

* CIF コアコンポーネントのサポートの向A11Y

## Cloud Manager  {#cloud-manager}

この節では、AEM as a Cloud Service 2021.8.0 および 2021.7.0 に含まれている Cloud Manager のリリースノートの概要を説明しています。

## リリース日 {#release-date-cm-aug}

AEM as a Cloud Service 2021.8.0 の Cloud Manager のリリース日は 2021 年 8 月 12 日です。
次回のリリースは2021年9月9日（PT）に予定されています。

### 新機能 {#what-is-new-aug}

* Cloud Serviceのお客様は、Cloud Manager でサービス契約 (SLA) レポートを表示できるようになりました。 This will be made available progressively over the next few months.
詳しくは、[SLA レポート ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sla-reporting.html) を参照してください。

* The type and severity of the IndexType and `IndexDamAssetLucene` quality rules has been changed. 現在は両方ともブロッカー *serverity* のバグです。

* 非同期および tika の設定に対応する新しい Oak インデックス品質ルールが導入されました。

* プログラムごとの最大 SSL 証明書数を 50 に増やします。

* ユーザーが Cloud Manager UI を使用して複数のリポジトリを作成および管理できるセルフサービス機能。

* SonarQube が Git の履歴データを不必要に読み取っていた問題を修正しました。 大規模なコードベースでは、これにより、ビルドパフォーマンスが不必要に低下することがありました。

* パイプラインごとに Maven 依存関係キャッシュを無効にする API が追加されました。

* Cloud Manager で使用される AEM プロジェクトアーキタイプのバージョンが 29 に更新されました。

### バグ修正 {#bug-fixes-aug}

* 最新のリリースが現在のリリースより前の場合は、更新可能ステータスは表示されるべきではありません。

* 名前が非常に長い新規組織で、初期のオンボーディングが失敗していました。

* 何らかの理由でパイプラインが 2 回トリガーされた場合、「*パイプライン実行ステータスを更新できませんでした*」エラーで、いずれかの実行が失敗します。

## コンテンツ転送ツール {#content-transfer-tool}

### リリース日 {#release-date-ctt-latest}

The Release Date for Content Transfer Tool v1.5.6 is August 11, 2021.

### バグ修正 {#bug-fixes-ctt}

* 場合によっては、一部のユーザーがターゲットインスタンスに移行されないことがあります。 この修正を受けるには、ターゲットAEMas a Cloud Serviceインスタンス上の aem-ethos-tools 1.2.354 以降のバージョンと共に、CTT v1.5.6 が必要です。

* パブリッシュインスタンスへの取り込み中に、「**取り込みを停止**」ボタンが無効になっていた問題を修正しました。 公開の取り込み中に Mongo の復元手順がないので、この操作は不要です。

* CTT は、抽出が正常に完了した後に `/tmp` ディレクトリをクリーンアップしませんでした。 これにより、ディスク容量の問題が発生する場合がありました。
