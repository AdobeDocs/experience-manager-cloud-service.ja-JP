---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.8.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.8.0 リリースのリリースノート。'
exl-id: 8b041934-1c4a-4670-9b03-d38f683b99e5
source-git-commit: 6bb7b2d056d501d83cf227adb239f7f40f87d0ce
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 57%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート {#release-notes}

以下では、[!DNL Experience Manager] as a Cloud Service の現在（最新）のバージョンのリリースノート全般の概要を説明します。

>[!NOTE]
>
>ここから、以前のバージョンのリリースノートに移動できます。 例えば、2020 および 2021 の場合は、

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の現在のリリース（2021.8.0）のリリース日は 2021年8月26日（PT）です。
次回のリリース（2021.9.0）は 2021年10月6日（PT）です。

## リリースビデオ {#release-video}

追加された機能の概要については、[&#128279;](https://video.tv.adobe.com/v/336277)2021年8月リリースの概要ビデオをご覧ください。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### の新機能[!DNL Assets] {#assets-features}

* デジタルアセットをリンクとして共有する場合、ユーザーは URL をすぐにクリップボードにコピーできます。 この機能強化により、アセットをより迅速かつ便利に共有できます。この機能により、迅速で便利なアセット共有が可能になります。

  ![アセットをリンクとして共有する場合の「URL をコピー」オプション](/help/assets/assets/link-share-copy-URL-option.png)
  *図：アセットをリンクとして共有する場合、URL をコピーして別々に共有できるようになりました。*

* TXT ファイルをアップロードすると、アセットマイクロサービスによって自動的にサムネールが生成されます。 PNG サムネールは、ユーザーがファイルを開かずに、コンテンツやファイルをある程度識別するのに役立つ TXT ファイルのレンディションです。 この機能は設定が不要で、デフォルトで動作します。

  ![TXT ファイルのレンディションが [!DNL Assets] により PNG 形式で自動的に生成される](/help/assets/assets/thumbnail-rendition-txt-file.png)
  *図：TXT ファイルのレンディションが自動的に生成されるので、ファイルを開かずにある程度識別できるようになります。*

### [!DNL Assets] プレリリースチャネルの新機能 {#assets-prerelease-features}

* 検索結果に表示されるアセットを、ユーザーが列表示およびカード表示で並べ替えることができるようになりました。並べ替えは、「名前」、「作成日」、「変更日」、「なし」の各列に対して機能します。

  ![[!DNL Assets] での検索結果の並べ替え（列表示とカード表示）](/help/assets/assets/sort-searched-assets.png)
  *図：[!DNL Assets] での検索結果の並べ替え（列表示とカード表示）*

### [!DNL Assets] で修正されたバグ  {#assets-bugs-fixed}

* 寄稿者グループのメンバーが [!DNL Assets] コンソール、追加 `POST` リクエストが生成され、コレクションが作成されます。 このリクエストは必須ではありません。権限の問題が原因で失敗し、多くのエラーがログに記録されます。 （CQ-4328856）
* ユーザーがアセットを表示し、 [!UICONTROL タイムライン] 左パネルのポップアップメニューから、エラーが表示されます。 ログには、無効なクエリが原因で多数の警告が記録されます。（CQ-4328919）

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] の新機能 {#what-is-new-forms}

* 自動フォーム変換サービスで、[イタリア語とポルトガル語の PDF フォームをアダプティブフォームに変換](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=ja#language-specific-meta-model)できます。

* **AcroForm ベースのレコードのドキュメント**：AEM Forms as a Cloud Service では、XFA ベースのフォームテンプレート以外に、[Adobe Acrobat フォーム PDF（AcroForm PDF）](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/generate-document-of-record-for-non-xfa-based-adaptive-forms.html?lang=ja)をレコードのドキュメントのテンプレートとして使用できます。

* **Microsoft® Azure データストアコネクタ**：次が可能です。 [フォームデータモデルをMicrosoft® Azure ストレージに接続する](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-azure-storage.html). これにより、アダプティブフォームのデータを取得し、BLOB としてMicrosoft® Azure Storage に保存することができます。

### [!DNL Forms] プレリリースチャネルで利用できる新機能 {#prerelease-features-forms}

* **アダプティブフォームでのAdobe Signの役割の使用** - Adobe Sign for business and enterprise service levels では、契約受信者の役割を、署名者だけでなく拡張して、ワークフロー要件に合わせることができます。 これで、契約の各受信者がアダプティブフォームでの役割を設定できるようになり、署名者がデフォルトの役割になります。

* **Analytics for Adaptive Forms** - Adobe Analyticsを介してエンドユーザーの行動をキャプチャおよび追跡し、アダプティブFormsでエンドユーザーのインサイトを収集できるようになりました。 データに基づく情報に基づく意思決定をおこない、エンドユーザーエクスペリエンスを向上させるのに役立ちます。

* **AEM FormsをMicrosoft® Dynamics およびSalesforce.comと簡単に接続**  — このサービスは、Microsoft® Dynamics およびSalesforce.com用の標準のデータソース設定およびデータモデルを提供します。 これにより、開発者は、Microsoft® Dynamics とSalesforce.comをアダプティブフォームのデータソースとしてより迅速かつ簡単に設定できます。

## CIF アドオン {#cloud-services-cif}

### 新機能 {#what-is-new-cif}

* ユーザーエクスペリエンスの向上、効率の向上、複雑な製品カタログのサポートの向上を実現する新しいカテゴリピッカー UI

  ![新しいカテゴリピッカー](/help/assets/CIF/category-picker.png)

* A11Y での CIF コアコンポーネントのサポートが向上しました。

## Cloud Manager {#cloud-manager}

この節では、AEM as a Cloud Service 2021.8.0 および 2021.7.0 に含まれている Cloud Manager のリリースノートの概要を説明しています。

## リリース日 {#release-date-cm-aug}

AEM as a Cloud Service 2021.8.0 の Cloud Manager のリリース日は 2021年8月12日（PT）です。
次回のリリースは 2021年9月9日（PT）に予定されています。

### 新機能 {#what-is-new-aug}

* Cloud Service ユーザーは、Cloud Manager でサービスレベル契約（SLA）レポートを表示できるようになりました。これは今後数か月で段階的に利用可能になる予定です。
詳しくは、[SLA レポート](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/sla-reporting.html?lang=ja)を参照してください。

* IndexType および `IndexDamAssetLucene` 品質ルールのタイプと重大度が変更されました。これらは現在、両方ともブロッカーのバグです *重大度*.

* 新しい Oak インデックス品質ルールが導入されて、非同期設定と Tika 設定に対応するようになりました。

* プログラムごとの SSL 証明書の最大数が 50 に増えました。

* ユーザーが Cloud Manager UI を使用して複数のリポジトリを作成および管理できるセルフサービス機能。

* SonarQube が Git 履歴データを不必要に読み取っていました。大規模なコードベースでは、これにより、ビルドパフォーマンスが不必要に低下することがありました。

* パイプラインごとに Maven 依存関係キャッシュを無効にする API が追加されました。

* Cloud Manager で使用される AEM プロジェクトアーキタイプのバージョンが 29 に更新されました。

### バグ修正 {#bug-fixes-aug}

* 最新リリースが現在のリリースよりも小さい場合は、「更新可能」ステータスが表示されません。

* 名前が長い新しい組織では、初回のオンボーディングが失敗していました。

* 何らかの理由でパイプラインが 2 回トリガーされた場合、実行の 1 つが *`cannot update pipeline execution status`* エラー。

## コンテンツ転送ツール {#content-transfer-tool}

### リリース日 {#release-date-ctt-latest}

コンテンツ転送ツール v1.5.6 のリリース日は 2021年8月11日（PT）です。

### バグ修正 {#bug-fixes-ctt}

* 一部のユーザーがターゲットインスタンスに移行されない場合がありました。 この修正を得るには、ターゲットAEMas a Cloud Serviceインスタンス上の aem-ethos-tools 1.2.354 以降のバージョンと共に、CTT v1.5.6 が必要です。

* パブリッシュインスタンスへの取り込み時に、「**取り込みを停止**」ボタンが無効になっていました。パブリッシュへの取り込み時には Mongo の復元ステップがないので、これは必要ありません。

* 抽出に成功したあと、CTT が `/tmp` ディレクトリをクリーンアップしていませんでした。これが原因で、ディスク容量の問題が発生することがありました。
