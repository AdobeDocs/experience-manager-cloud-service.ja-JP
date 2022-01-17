---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.8.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.8.0 リリースのリリースノート。'
source-git-commit: d37193833d784f3f470780b8f28e53b473fd4e10
workflow-type: ht
source-wordcount: '1032'
ht-degree: 100%

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

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の現在のリリース（2021.8.0）のリリース日は 2021年8月26日（PT）です。
次回のリリース（2021.9.0）は 2021年10月6日（PT）です。

## リリースビデオ {#release-video}

追加された機能の概要については、](https://video.tv.adobe.com/v/336277)2021年8月リリースの概要ビデオ[をご覧ください。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### の新機能[!DNL Assets] {#assets-features}

* デジタルアセットをリンクとして共有する場合、ユーザーは URL をクリップボードにすぐにコピーできます。この機能強化により、アセットをより迅速かつ便利に共有できます。この機能により、迅速で便利なアセット共有が可能になります。

   ![アセットをリンクとして共有する場合の「URL をコピー」オプション](/help/assets/assets/link-share-copy-URL-option.png)
   *図：アセットをリンクとして共有する場合、URL をコピーして別々に共有できるようになりました。*

* TXT ファイルをアップロードすると、アセットマイクロサービスによって自動的にサムネールが生成されます。PNG サムネールは TXT ファイルのレンディションで、ユーザーがファイルを開かずにコンテンツやファイルをある程度識別できるようにするものです。この機能は設定が不要で、デフォルトで動作します。

   ![TXT ファイルのレンディションが [!DNL Assets] により PNG 形式で自動的に生成される](/help/assets/assets/thumbnail-rendition-txt-file.png)
   *図：TXT ファイルのレンディションが自動的に生成されるので、ファイルを開かずにある程度識別できるようになります。*

### [!DNL Assets] プレリリースチャネルの新機能 {#assets-prerelease-features}

* 検索結果に表示されるアセットを、ユーザーが列表示およびカード表示で並べ替えることができるようになりました。並べ替えは、「名前」、「作成日」、「変更日」、「なし」の各列に対して機能します。

   ![[!DNL Assets] での検索結果の並べ替え（列表示とカード表示）](/help/assets/assets/sort-searched-assets.png)
   *図：[!DNL Assets] での検索結果の並べ替え（列表示とカード表示）*

### [!DNL Assets] で修正されたバグ  {#assets-bugs-fixed}

* 投稿者グループのメンバーが [!DNL Assets] コンソールに移動すると、追加の `POST` リクエストが生成されて、コレクションを作成しようとします。このリクエストは必須ではなく、権限の問題が原因で失敗して、ログに多数のエラーが記録されます。（CQ-4328856）
* ユーザーがアセットを表示し、左パネルのポップアップメニューから「[!UICONTROL タイムライン]」を選択すると、エラーが表示されます。ログには、無効なクエリが原因で多数の警告が記録されます。（CQ-4328919）

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] の新機能  {#what-is-new-forms}

* 自動フォーム変換サービスで、[イタリア語とポルトガル語の PDF フォームをアダプティブフォームに変換](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=ja#language-specific-meta-model)できます。

* **AcroForm ベースのレコードのドキュメント**：AEM Forms as a Cloud Service では、XFA ベースのフォームテンプレート以外に、[Adobe Acrobat フォーム PDF（AcroForm PDF）](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html?lang=ja)をレコードのドキュメントのテンプレートとして使用できます。

* **Microsoft Azure データストアコネクタ**：[フォームデータモデルを Microsoft Azure Storage に接続できるようになりました](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html?lang=ja)。アダプティブフォームデータを取得し、BLOB として Microsoft Azure Storage に保存することができます。

### [!DNL Forms] プレリリースチャネルで利用できる新機能 {#prerelease-features-forms}

* **アダプティブフォームでの Adobe Sign の役割の使用**：ビジネスおよびエンタープライズサービスレベルの Adobe Sign では、ワークフロー要件に適切に合致するように、契約書受信者の役割を署名者以外にも拡大できます。契約書の受信者ごとに、アダプティブフォームでの自分の役割を設定できるようになりました。デフォルトの役割は署名者です。

* **アダプティブフォーム用の Analytics**：アダプティブフォーム用の Adobe Analytics でエンドユーザーの行動を捉えて追跡し、エンドユーザーのインサイトを収集できるようになりました。十分な情報に基づいて決定を行い、エンドユーザーのエクスペリエンスを向上させることができます。

* **AEM Forms と Microsoft Dynamics および Salesforce.com との簡単な接続**：Microsoft Dynamics と Salesforce.com のデータソース設定およびデータモデルが標準で提供されるので、開発者が Microsoft Dynamics と Salesforce.com をアダプティブフォームのデータソースとしてより迅速かつ簡単に設定できるようになりました。

## CIF アドオン {#cloud-services-cif}

### 新機能 {#what-is-new-cif}

* 新しいカテゴリピッカー UI により、ユーザーエクスペリエンス、効率および複雑な製品カタログのサポートが向上しました。

   ![新しいカテゴリピッカー](/help/assets/CIF/category-picker.png)

* A11Y での CIF コアコンポーネントのサポートが向上しました。

## Cloud Manager {#cloud-manager}

この節では、AEM as a Cloud Service 2021.8.0 および 2021.7.0 に含まれている Cloud Manager のリリースノートの概要を説明しています。

## リリース日 {#release-date-cm-aug}

AEM as a Cloud Service 2021.8.0 の Cloud Manager のリリース日は 2021年8月12日（PT）です。
次回のリリースは 2021年9月9日（PT）に予定されています。

### 新機能 {#what-is-new-aug}

* Cloud Service ユーザーは、Cloud Manager でサービスレベル契約（SLA）レポートを表示できるようになりました。これは、今後数か月で段階的に利用可能になる予定です。
詳しくは、[SLA レポート](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sla-reporting.html?lang=ja)を参照してください。

* IndexType および `IndexDamAssetLucene` 品質ルールのタイプと重大度が変更されました。これらはどちらも、*重大度*&#x200B;が「ブロッカー」のバグになりました。

* 新しい Oak インデックス品質ルールが導入されて、非同期設定と Tika 設定に対応するようになりました。

* プログラムごとの SSL 証明書の最大数が 50 に増えました。

* セルフサービス機能により、ユーザーが Cloud Manager UI を使用して複数のリポジトリーを作成および管理できるようになりました。

* SonarQube が Git 履歴データを不必要に読み取っていました。大規模なコードベースでは、これにより、ビルドパフォーマンスが不必要に低下することがありました。

* パイプラインごとに Maven 依存関係キャッシュを無効にする API が追加されました。

* Cloud Manager で使用される AEM プロジェクトアーキタイプのバージョンが 29 に更新されました。

### バグ修正 {#bug-fixes-aug}

* 最新のリリースが現在のリリースより前の場合は、更新可能ステータスは表示されるべきではありません。

* 名前が非常に長い新規組織で、初回のオンボーディングが失敗していました。

* 何らかの理由でパイプラインが 2 回トリガーされた場合、「*パイプライン実行ステータスを更新できませんでした*」エラーで、いずれかの実行が失敗します。

## コンテンツ転送ツール {#content-transfer-tool}

### リリース日 {#release-date-ctt-latest}

コンテンツ転送ツール v1.5.6 のリリース日は 2021年8月11日（PT）です。

### バグ修正 {#bug-fixes-ctt}

* 一部のユーザーがターゲットインスタンスに移行されない場合がありました。この修正を適用するには、ターゲット AEM as a Cloud Service インスタンスに CTT v1.5.6 と aem-ethos-tools 1.2.354 以降のバージョンが必要です。

* パブリッシュインスタンスへの取り込み時に、「**取り込みを停止**」ボタンが無効になっていました。パブリッシュへの取り込み時には Mongo の復元ステップがないので、これは必要ありません。

* 抽出に成功したあと、CTT が `/tmp` ディレクトリをクリーンアップしていませんでした。これが原因で、ディスク容量の問題が発生することがありました。
