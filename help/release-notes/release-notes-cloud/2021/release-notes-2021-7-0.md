---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.7.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.7.0 リリースのリリースノート。'
exl-id: 848f6a29-2e0f-4976-8ed7-6b7f69408c1b
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1292'
ht-degree: 69%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート {#release-notes}

以下では、[!DNL Experience Manager] as a Cloud Service の現在（最新）のバージョンのリリースノート全般の概要を説明します。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2020 年と 2021 年のバージョン）のリリースノートに移動できます。

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a 
[!DNL Cloud Service]の現在リリース（2021.7.0）のリリース日は 2021 年 7 月 29 日です。次のリリース（2021.8.0）は 2021 年 8 月 26 日です。

## リリースビデオ {#release-video}

追加された機能の概要については、[&#128279;](https://video.tv.adobe.com/v/335580)2021 年 7 月リリースの概要ビデオをご覧ください。

## Experience Manager Foundation as a Cloud Service {#foundation}

### 新機能 {#what-is-new-foundation}

* より柔軟なDispatcher設定：プロジェクトをより簡単に整理できます。 例えば、サイト構造を反映した複数の書き換えルールファイルを含めることができるようになりました。Dispatcher設定を活用できるよう [&#128279;](/help/implementing/dispatcher/disp-overview.md#validation-debug) 設定する方法など、この柔軟なモードについて  ご確認ください。
* レプリケーションエージェントの「配布」タブにあるツリーレプリケーション UI は、非推奨（廃止予定）と見なされ、2021 年 9 月 30 日（PT）以降に削除されました。 代替レプリケーション戦略について[ご確認](/help/operations/replication.md#tree-activation)ください。
* Sling 用 `org.apache.sling.datasource-1.0.4.jar` データソースサポート用バンドルは、機能が古く、顧客に使用されていないので、削除されました。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### の新機能[!DNL Assets] {#assets-features}

* コンテンツ自動化機能を使用 [!DNL Experience Manager Assets] ると、[!DNL Adobe Creative Cloud] API を使用して、アセットの大規模な生成を自動化できます。 同じアセットのバリエーションを作成するのに必要な時間と繰り返しを大幅に減らし、コンテンツベロシティを向上させます。この機能はプログラミングを必要とせず、DAM 内で動作します。[アセットの統合を使用して Creative Cloud のバリエーションを生成する](/help/assets/cc-api-integration.md)を参照してください。

* [!DNL Experience Manager Assets] には [!DNL Document Cloud] PDF ビューアが含まれており、PDF ドキュメントをネイティブにプレビューできます。この機能を使用すると、ファイルの処理や変換をおこなわずに、複数ページの PDF ファイルをプレビューできます。この機能により、[!DNL Experience Manager] 6.5 と同等の機能が使用できるようになりました。ビューアで使用できるコントロールには、ズーム、ページへ移動、ドッキング解除、全画面表示などがあります。また、プレビューして、ページやブックマークにジャンプすることもできます。 ファイル自体へのコメントはサポートされています。 PDFファイル内のコンテンツに対するコメントと注釈は、今後のリリースで追加される予定です。

  ![PDF ビューアを使用した [!DNL Experience Manager] での PDF ファイルのプレビュー](/help/assets/assets/preview-pdf-file-viewer.png)

* リンク共有のダウンロード機能は、非同期ダウンロードを使用してダウンロード速度を上げます。 詳しくは、[ リンク共有を使用して共有されたアセットのダウンロード ](/help/assets/download-assets-from-aem.md#link-share-download) を参照してください。

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

* デジタルアセットをリンクとして共有する場合、ユーザーは URL をクリップボードにコピーできます。 この機能強化により、アセットをより迅速かつ便利に共有できます。

### [!DNL Assets] で修正されたバグ  {#assets-bugs-fixed}

API `com.day.cq.dam.api.collection.SmartCollection` は、[!DNL Experience Manager] as a [!DNL Cloud Service] では使用できません。（CQ-4326322）

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] の新機能 {#what-is-new-forms}

* automated forms conversionサービスを使用して [ フランス語、ドイツ語、スペイン語のPDF formsをアダプティブフォームに変換 ](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=ja#language-specific-meta-model) できるようになりました。
* テンプレートエディターに、アダプティブフォームのコンポーネントに関連するエラーを表示するためのパネルを別途追加しました。 これにより、すべてのアダプティブフォームのエラーが 1 か所に集約されるので、解決に要する時間を短縮できます。

### [!DNL Forms]プレリリースチャネルで利用できる新機能 {#beta-features-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**：[通信 API](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications.html) では、XDP テンプレートと XML データを組み合わせて、様々な形式の印刷用ドキュメントを生成できます。このサービスを使用すると、同期モードでドキュメントを生成できます。API により、以下のような機能を備えたアプリケーションを作成することができます。
   * テンプレートファイルに XML データを格納することで、最終形式のドキュメントを生成します。
   * 非インタラクティブ PDF 印刷ストリームを含む様々な形式で出力フォームを生成します。
   * XFA フォーム PDF および Adobe Acrobat フォームから印刷用 PDF ファイルを生成します。

* **Variable Data Externalizer**：AEM ワークフロー変数のデータを、組織で管理される外部ストレージシステムに保存できます。

* **Acroform べースのレコードのドキュメント**：XFA ベースのフォームテンプレート以外にも、[Adobe Acrobat Form PDF（Acroform PDF）](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/generate-document-of-record-for-non-xfa-based-adaptive-forms.html?lang=ja) を、レコードドキュメントのテンプレートとして使用することもできます。

* **Microsoft® Azure データストアコネクタ**: [ フォームデータモデルをMicrosoft® Azure ストレージに接続 ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-azure-storage.html) できるようになりました。 アダプティブフォームデータを取得して、BLOB としてMicrosoft® Azure ストレージに保存できます。

## CIF アドオン {#cloud-services-cif}

### 新機能 {#what-is-new-cif}

* CIF コアコンポーネント v2
   * PDP/PLP URL と SEO の構成の簡素化と改善
   * オーサリングモードでのステージングされた製品データの視覚的インジケーターにより、今後の変更の可視性が向上
   * コンテンツページとコマースページ用の新しいサイトマップコンポーネント

* 事前定義済みのレコメンデーションまたはオンザフライで作成されたレコメンデーションを使用した、AEM Storefront の Adobe Sensei[&#128279;](https://business.adobe.com/jp/products/magento/product-recommendations.html) による Adobe Commerce Sensei 製品レコメンデーションのサポート

## [!DNL Experience Manager Screens] as a [!DNL Cloud Service] {#screens}

### バグ修正 {#bug-fixes-screens}

* コンテンツプロバイダーの設定は、作成または更新時に検証されるようになりました。

* すべての表示ビューにはフォルダー列があります。

* Screens コンテンツ構造を展開できます。

* `bulk-offline-update-service` 一部の環境のすべての権限が欠落していました。

* ヘルプリンクが更新され、新しい Screens クラウドドキュメントと一致するようになりました。

* プレイリストの割り当てを解除し、プレーヤーを割り当てたプレイリストの削除を許可しない機能が追加されました。

* 「すべて」のキャッシュがクリアされると、プレーヤーがAssetsを再ダウンロードするようになりました。

* *終了時間* が次の日に設定されている場合、繰り返しスケジュールが機能するようになりました。

* `Back&Forward` が、Screens as a Cloud Service UI で機能するようになりました。

* 以前は、名前が同じで異なる名前空間を持つタグを作成することができませんでした。

## Experience Manager as a Cloud Service の XML ドキュメント {#xml-documentation}

### 新機能 {#what-is-new-xml-documentation}

Experience Manager as a Cloud Service の XML ドキュメントが一般利用可能になりました。Experience Managerのas a Cloud Serviceがあるお客様は、XML Documentation アドオンを入手して、Experience Manager Sitesを含む複数のチャネルで技術コンテンツをインポート、作成、管理、配信できます。

## Cloud Manager {#cloud-manager}

この節では、AEM as a Cloud Service 2021.7.0 に含まれている Cloud Manager のリリースノートの概要を説明しています。

### リリース日 {#release-cm-july}

AEM as a Cloud Service 2021.7.0 の Cloud Manager のリリース日は 2021 年 7 月 15 日です。次回のリリースは 2021年8月12日（PT）に予定されています。

### 新機能 {#what-is-new-cm-july}

* お客様は、Cloud Manager のビルドプロセスに Azul 8 および 11 JDK を使用できるようになりました。ツールチェーン対応の Maven プラグイン&#x200B;*または* Maven プロセスの実行全体に対して、これらの JDK のいずれかを使用するように選択できます。

* 送信エグレス IP がビルドステップログファイルに記録されるようになりました。

* 古いバージョンのAEMを実行しているステージ環境と実稼動環境で、**利用可能な更新** のステータスがレポートされるようになりました。

* サポートされる SSL 証明書の最大数が、プログラムあたり 20 に増えました。

* 設定できるドメインの最大数が、環境あたり 500 に増えました。

* 「**Git を管理**」ボタンのタイトルが「**Git 情報にアクセス**」に変更され、ダイアログが視覚的に更新されました。

* Cloud Manager で使用される AEM プロジェクトアーキタイプのバージョンが 28 に更新されました。

### バグ修正 {#bug-fixes-cm-july}

* IP 許可リストを環境にバインドする際に、「プレビュー」オプションが使用できないことがありました。

* 存在しない実行の実行詳細ページに手動で移動しても、エラーが表示されず、読み込みが無限に繰り返される画面が表示されるだけでした。

* SSL 証明書の最大数に達した場合に表示されるエラーメッセージが参考になりませんでした。

* 状況によっては、**概要**&#x200B;ページのパイプラインカードに表示されるリリースバージョンが矛盾していることがありました。

* プログラムの追加ウィザードで、作成後に名前を変更できないと誤って表示されていました。

### 既知の問題 {#known-issues-cm-july}

Azul JDK の使用に切り替えるお客様は、すべての既存アプリケーションが Azul JDK でエラーなしにコンパイルされるとは限らないことを知っておく必要があります。Adobeでは、切り替える前にローカルでテストすることをお勧めします。

## Cloud Acceleration Manager {#cam}

### リリース日 {#release-date-july-cam}

Cloud Acceleration Manager のリリース日は 2021 年 7 月 15 日です。

### 新機能 {#what-is-new-cam}

Cloud Acceleration Manager は、Cloud Service の計画から運用開始まで、移行プロセス全体を通じて IT チームをガイドするために設計されたクラウドベースのアプリケーションです。Cloud ServiceとしてのAEMへの移行プロセスの各段階で役立つ、Adobeが推奨するベストプラクティス、ヒント、ドキュメント、ツールを使用して、移行を成功させるためのチームを設定します。 詳細は[こちら](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/getting-started-cam.html?lang=ja)をご覧ください。

>[!NOTE]
>
> この [Cloud Acceleration Manager デモビデオ ](https://video.tv.adobe.com/v/335547) をご覧ください。
