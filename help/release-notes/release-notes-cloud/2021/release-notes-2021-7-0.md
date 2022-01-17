---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.7.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.7.0 リリースのリリースノート。'
exl-id: 848f6a29-2e0f-4976-8ed7-6b7f69408c1b
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: ht
source-wordcount: '1315'
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

[!DNL Adobe Experience Manager] as a 
[!DNL Cloud Service]の現在リリース（2021.7.0）のリリース日は 2021 年 7 月 29 日です。次のリリース（2021.8.0）は 2021 年 8 月 26 日です。

## リリースビデオ {#release-video}

追加された機能の概要については、](https://video.tv.adobe.com/v/335580)2021 年 7 月リリースの概要ビデオ[をご覧ください。

## Experience Manager Foundation as a Cloud Service {#foundation}

### 新機能 {#what-is-new-foundation}

* より柔軟な Dispatcher 設定：プロジェクトをより簡単に整理できます。例えば、サイト構造を反映した複数の書き換えルールファイルを含めることができるようになりました。このモードを活用するために Dispatcher 設定を構築する方法など、この柔軟なモードについて[ご確認](/help/implementing/dispatcher/disp-overview.md#validation-debug)ください。
* レプリケーションエージェントの「配布」タブにあるツリーレプリケーション UI は、非推奨と見なされ、9 月 30 日以降に削除される予定です。代替レプリケーション戦略について[ご確認](/help/operations/replication.md#tree-activation)ください。
* Sling 用 `org.apache.sling.datasource-1.0.4.jar` データソースサポート用バンドルは、機能が古く、顧客に使用されていないので、削除されました。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### の新機能[!DNL Assets] {#assets-features}

* コンテンツ自動処理機能を使用すると、 [!DNL Experience Manager Assets] で [!DNL Adobe Creative Cloud] API を活用して、アセットの大規模な生成を自動化できます。同じアセットのバリエーションを作成するのに必要な時間と繰り返しを大幅に減らし、コンテンツベロシティを向上させます。この機能はプログラミングを必要とせず、DAM 内で動作します。[アセットの統合を使用して Creative Cloud のバリエーションを生成する](/help/assets/cc-api-integration.md)を参照してください。

* [!DNL Experience Manager Assets] には [!DNL Document Cloud] PDF ビューアが含まれており、PDF ドキュメントをネイティブにプレビューできます。この機能を使用すると、ファイルの処理や変換をおこなわずに、複数ページの PDF ファイルをプレビューできます。この機能により、[!DNL Experience Manager] 6.5 と同等の機能が使用できるようになりました。ビューアで使用できるコントロールには、ズーム、ページへ移動、ドッキング解除、全画面表示などがあります。また、ページをプレビューしたり、ブックマークにジャンプしたりすることもできます。ファイル自体へのコメントはサポート済で、PDF ファイル内のコンテンツに対するコメントと注釈が今後のリリースで追加される予定です。

   ![PDF ビューアを使用した [!DNL Experience Manager] での PDF ファイルのプレビュー](/help/assets/assets/preview-pdf-file-viewer.png)

* リンク共有ダウンロード機能では、非同期ダウンロードを使用してダウンロード速度を向上させています。[リンク共有を使用して共有アセットをダウンロードする](/help/assets/download-assets-from-aem.md#link-share-download)を参照してください。

   ![ダウンロードインボックス](/help/assets/assets/download-inbox.png)

* ビュー設定が強化され、デフォルトのビューとデフォルトの並べ替えパラメーターを選択できるようになりました。

   ![[!UICONTROL 表示設定]](/help/assets/assets/view-settings-for-defaults.png)でデフォルト表示を設定する

* プロパティの述語に基づいて、フォルダーを検索およびフィルタリングできます。

   ![検索用述語を使用して検索フォルダーをフィルタリングする](/help/assets/assets/search-folders-via-predicates.png)

### [!DNL Assets]プレリリースチャネルで利用できる新機能 {#assets-prerelease-features}

<!-- TBD: Not sure about GA of these enh. Shall check with the team.

* A user experience enhancements displays the number of assets present in a folder. For more than 1000 assets in a folder, [!DNL Assets] displays 1000+.

  ![Number of assets in a folder are displayed on the interface](/help/assets/assets/browse-folder-number-of-assets.png)

* You can directly apply a metadata schemas to a folder in its [!UICONTROL Properties].

  ![Add metadata schema from folder properties](/help/assets/assets/metadata-schema-folder-properties.png)
-->

* デジタルアセットをリンクとして共有する場合に URL をクリップボードにコピーできます。この機能強化により、アセットをより迅速かつ便利に共有できます。

### [!DNL Assets] で修正されたバグ  {#assets-bugs-fixed}

API `com.day.cq.dam.api.collection.SmartCollection` は、[!DNL Experience Manager] as a [!DNL Cloud Service] では使用できません。（CQ-4326322）

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] の新機能  {#what-is-new-forms}

* 自動フォーム変換サービスを使用して、[フランス語、ドイツ語、スペイン語の PDF フォームをアダプティブフォームに変換](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=ja#language-specific-meta-model)できるようになりました。
* テンプレートエディターに、アダプティブフォームのコンポーネントに関連するエラーを表示するためのパネルを別途追加しました。これにより、すべてのアダプティブフォームのエラーが 1 か所に集約されるので、解決に要する時間を短縮できます。

### [!DNL Forms]プレリリースチャネルで利用できる新機能 {#beta-features-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**：[通信 API](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/aem-forms-cloud-service-communications.html?lang=ja) では、XDP テンプレートと XML データを組み合わせて、様々な形式の印刷用ドキュメントを生成できます。このサービスを使用すると、同期モードでドキュメントを生成できます。API により、以下のような機能を備えたアプリケーションを作成することができます。
   * テンプレートファイルに XML データを格納することで、最終形式のドキュメントを生成します。
   * 非インタラクティブ PDF 印刷ストリームを含む様々な形式で出力フォームを生成します。
   * XFA フォーム PDF および Adobe Acrobat フォームから印刷用 PDF ファイルを生成します。

* **Variable Data Externalizer**：AEM ワークフロー変数のデータを、組織で管理される外部ストレージシステムに保存できます。

* **Acroform べースのレコードのドキュメント**：XFA ベースのフォームテンプレート以外にも、[Adobe Acrobat Form PDF（Acroform PDF）](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html?lang=ja) を、レコードドキュメントのテンプレートとして使用することもできます。

* **Microsoft Azure データストアコネクタ**：[フォームデータモデルを Microsoft Azure Storage に接続できるようになりました](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html?lang=ja)。アダプティブフォームデータを取得し、BLOB として Microsoft Azure Storage に保存することができます。

## CIF アドオン {#cloud-services-cif}

### 新機能 {#what-is-new-cif}

* CIF コアコンポーネント v2
   * PDP/PLP URL と SEO の構成の簡素化と改善
   * オーサリングモードでのステージングされた製品データの視覚的インジケーターにより、今後の変更の可視性が向上
   * コンテンツページとコマースページ用の新しいサイトマップコンポーネント

* 事前定義済みのレコメンデーションまたはオンザフライで作成されたレコメンデーションを使用した、AEM Storefront の Adobe Sensei](https://business.adobe.com/jp/products/magento/product-recommendations.html) による [Adobe Commerce Sensei 製品レコメンデーションのサポート

## [!DNL Experience Manager Screens] as a [!DNL Cloud Service] {#screens}

### バグ修正 {#bug-fixes-screens}

* コンテンツプロバイダーの設定は、作成またはアップデートの際に検証されるようになりました。

* すべての表示にはフォルダー列があります。

* Screens コンテンツ構造を展開できます。

* `bulk-offline-update-service` 一部の環境のすべての権限が欠落していました。

* ヘルプリンクが更新され、新しい Screens クラウドドキュメントと一致するようになりました。

* プレイリストの割り当てを解除し、プレーヤーを割り当てたプレイリストの削除を許可しない機能が追加されました。

* 「すべて」のキャッシュがクリアされた場合、プレーヤーがアセットを再ダウンロードするようになりました。

* *終了時間*&#x200B;が次の日に設定されている場合、繰り返しスケジュールが機能するようになりました。

* `Back&Forward` が、Screens as a Cloud Service UI で機能するようになりました。

* 以前は、名前が同じで異なる名前空間を持つタグを作成することができませんでした。

## Experience Manager as a Cloud Service の XML ドキュメント {#xml-documentation}

### 新機能 {#what-is-new-xml-documentation}

Experience Manager as a Cloud Service の XML ドキュメントが一般利用可能になりました。Experience Manager as a Cloud Service の顧客は、XML ドキュメントのアドオンを入手し、Experience Manager サイトを含む複数のチャネルで技術コンテンツをインポート、作成、管理、配信できます。

## Cloud Manager {#cloud-manager}

この節では、AEM as a Cloud Service 2021.7.0 に含まれている Cloud Manager のリリースノートの概要を説明しています。

### リリース日 {#release-cm-july}

AEM as a Cloud Service 2021.7.0 の Cloud Manager のリリース日は 2021 年 7 月 15 日です。次回のリリースは 2021年8月12日（PT）に予定されています。

### 新機能 {#what-is-new-cm-july}

* お客様は、Cloud Manager のビルドプロセスに Azul 8 および 11 JDK を使用できるようになりました。ツールチェーン対応の Maven プラグイン&#x200B;*または* Maven プロセスの実行全体に対して、これらの JDK のいずれかを使用するように選択できます。

* 送信エグレス IP がビルドステップログファイルに記録されるようになりました。

* 古いバージョンの AEM を実行しているステージ環境と実稼動環境で、**アップデートが使用可能**&#x200B;のステータスがレポートされるようになりました。

* サポートされる SSL 証明書の最大数が、プログラムあたり 20 に増えました。

* 設定できるドメインの最大数が、環境あたり 500 に増えました。

* 「**Git を管理**」ボタンのタイトルが「**Git 情報にアクセス**」に変更され、ダイアログが視覚的に更新されました。

* Cloud Manager で使用される AEM プロジェクトアーキタイプのバージョンが 28 に更新されました。

### バグ修正 {#bug-fixes-cm-july}

* 許可リストを IP 環境をバインドする際に、「プレビュー」オプションが使用できないことがありました。

* 存在しない実行の実行詳細ページに手動で移動しても、エラーが表示されず、読み込みが無限に繰り返される画面が表示されるだけでした。

* SSL 証明書の最大数に達した場合に表示されるエラーメッセージが参考になりませんでした。

* 状況によっては、**概要**&#x200B;ページのパイプラインカードに表示されるリリースバージョンが矛盾していることがありました。

* プログラムの追加ウィザードで、作成後に名前を変更できないと誤って表示されていました。

### 既知の問題 {#known-issues-cm-july}

Azul JDK の使用に切り替えるお客様は、すべての既存アプリケーションが Azul JDK でエラーなしにコンパイルされるとは限らないことに注意してください。切り替える前に、ローカルでテストすることを強くお勧めします。

## Cloud Acceleration Manager {#cam}

### リリース日 {#release-date-july-cam}

Cloud Acceleration Manager のリリース日は 2021 年 7 月 15 日です。

### 新機能 {#what-is-new-cam}

Cloud Acceleration Manager は、Cloud Service の計画から運用開始まで、移行プロセス全体を通じて IT チームをガイドするために設計されたクラウドベースのアプリケーションです。AEM as Cloud Service への移行の各段階で、アドビが推奨するベストプラクティス、ヒント、ドキュメント、ツールを使用して、チームを成功に導きます。詳細は[こちら](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/getting-started-cam.html?lang=ja)をご覧ください。

>[!NOTE]
>
> この [Cloud Acceleration Manager のデモビデオ](https://video.tv.adobe.com/v/335547)を確認してください。
