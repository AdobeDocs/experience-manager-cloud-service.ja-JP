---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 14dc3b308a839040fdf2efe42d2fa4ce35253df0
workflow-type: tm+mt
source-wordcount: '1309'
ht-degree: 10%

---


# [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート  {#release-notes}

以下では、[!DNL Experience Manager] as a Cloud Service の現在（最新）のバージョンのリリースノート全般の概要を説明します。

>[!NOTE]
>
>ここから、以前のバージョンのリリースノートに移動できます。例えば、2020、2021などの場合、

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager]のリリース日(2021.7.0)は2021年7月29日です。
[!DNL Cloud Service]次のリリース(2021.8.0)は2021年8月27日です。

## リリースビデオ {#release-video}

追加された機能の概要については、 2021年7月リリースの概要](https://video.tv.adobe.com/v/335580)ビデオをご覧ください。[

## [!DNL Experience Manager] 基盤とし [!DNL Cloud Service] て {#foundation}

### 新機能 {#what-is-new-foundation}

* より柔軟なDispatcher設定：プロジェクトは、より簡単に整理できます。 例えば、サイト構造を反映した複数の書き換えルールファイルを含めることができるようになりました。 [この柔](/help/implementing/dispatcher/disp-overview.md#validation-debug) 軟なモードについて説明します。このモードを活用するためにDispatcher設定を構築する方法などがあります。
* レプリケーションエージェントの「配布」タブにあるツリーレプリケーションUIは、非推奨と見なされ、9月30日以降に削除される予定です。 [代替レプリ](/help/operations/replication.md#tree-activation) ケーション戦略について説明します。
* Slingデータソースのサポート用のバンドル`org.apache.sling.datasource-1.0.4.jar`は、古い機能を持ち、お客様が使用していないので、削除されました。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets]の新機能 {#assets-features}

* コンテンツ自動化機能を使用すると、 [!DNL Experience Manager Assets]は[!DNL Adobe Creative Cloud] APIを活用して、アセットの大規模な生産を自動化できます。 同じアセットのバリエーションを作成するのに必要な時間と繰り返しを大幅に減らし、コンテンツの速度を向上させます。 この機能にはプログラミングは必要なく、DAM内から機能します。 [アセットの統合](/help/assets/cc-api-integration.md)を使用したCreative Cloudのバリエーションの生成を参照してください。

* [!DNL Experience Manager Assets] PDFビューアを [!DNL Document Cloud] 含めて、PDFドキュメントをネイティブにプレビューできます。この機能を使用すると、ファイルの処理や変換を行わずに、複数ページのPDFファイルをプレビューできます。 この機能により、[!DNL Experience Manager] 6.5と同等の機能が向上しました。ビューアで使用できるコントロールには、ズーム、ページへ移動、ドッキング解除の各コントロール、フルスクリーン表示などがあります。 また、ページやしおりをプレビューしたり、しおりにジャンプしたりすることもできます。 ファイル自体に対するコメントがサポートされ、PDFファイル内のコンテンツに対するコメントと注釈が今後のリリースで追加される予定です。

   ![PDFビューアを使用したPDFフ [!DNL Experience Manager] ァイルのプレビュー](/help/assets/assets/preview-pdf-file-viewer.png)

* Linkshareのダウンロード機能は、非同期ダウンロードを使用してダウンロード速度を向上させます。 [リンク共有](/help/assets/download-assets-from-aem.md#link-share-download)を使用して共有されたアセットのダウンロードを参照してください。

   ![ダウンロードインボックス](/help/assets/assets/download-inbox.png)

* ビュー設定が強化され、ユーザーがデフォルトのビューとデフォルトの並べ替えパラメーターを選択できるようになりました。

   ![表示設定でのデフォル [!UICONTROL ト表示の設定]](/help/assets/assets/view-settings-for-defaults.png)

* プロパティの述語に基づいて、フォルダーを検索およびフィルタリングできます。

   ![検索用述語を使用した検索フォルダーのフィルタリング](/help/assets/assets/search-folders-via-predicates.png)

### [!DNL Assets]プレリリースチャネルで利用できる新機能 {#assets-prerelease-features}

<!-- TBD: Not sure about GA of these enh. Shall check with the team.

* A user experience enhancements displays the number of assets present in a folder. For more than 1000 assets in a folder, [!DNL Assets] displays 1000+.

  ![Number of assets in a folder are displayed on the interface](/help/assets/assets/browse-folder-number-of-assets.png)

* You can directly apply a metadata schemas to a folder in its [!UICONTROL Properties].

  ![Add metadata schema from folder properties](/help/assets/assets/metadata-schema-folder-properties.png)
-->

* デジタルアセットをリンクとして共有する場合、ユーザーはURLをクリップボードにコピーできます。 この機能強化により、アセットをより迅速かつ便利に共有できます。

### [!DNL Assets] で修正されたバグ  {#assets-bugs-fixed}

API `com.day.cq.dam.api.collection.SmartCollection`は、[!DNL Cloud Service]として[!DNL Experience Manager]では使用できません。 （CQ-4326322）

## [!DNL Experience Manager Forms] として  [!DNL Cloud Service] {#forms}

### [!DNL Forms] の新機能  {#what-is-new-forms}

* automated forms conversionサービスを使用して、フランス語、ドイツ語、スペイン語のPDF forms](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model)をアダプティブフォームに変換できるようになりました。[
* アダプティブフォームのコンポーネントに関連するエラーを表示するためのパネルをテンプレートエディターに別に追加しました。 これにより、すべてのアダプティブフォームのエラーを1か所に統合し、解決に要する時間を短縮できます。

### [!DNL Forms]プレリリースチャネルで利用できる新機能 {#beta-features-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [通信APIシェル](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/aem-forms-cloud-service-communications.html) プでは、XDPテンプレートとXMLデータを組み合わせて、様々な形式の印刷ドキュメントを生成できます。このサービスを使用すると、同期モードでドキュメントを生成できます。 APIを使用すると、次の操作を可能にするアプリケーションを作成できます。
   * テンプレートファイルにXMLデータを入力してドキュメントを生成します。
   * 非インタラクティブPDF印刷ストリームを含む様々な形式で出力フォームを生成します。
   * XFAフォームPDFおよびAdobe Acrobatフォームから印刷用PDFファイルを生成します。

* **Variable Data Externalizer**：AEM ワークフロー変数のデータを、組織で管理される外部ストレージシステムに保存できます。

* **Acroformベースのレコードのドキュメント**:また、 [Adobe Acrobat Form PDF(Acroform PDF)](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html) を、XFAベースのフォームテンプレート以外のレコードのドキュメントのテンプレートとして使用することもできます。

* **Microsoft Azureデータストアコネクタ**:これで、フォームデ [ータモデルをMicrosoft Azure Storageに接続できます](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html)。アダプティブフォームデータを取得し、BLOBとしてMicrosoft Azure Storageに保存することができます。

## CIFアドオン {#cloud-services-cif}

### 新機能 {#what-is-new-cif}

* CIFコアコンポーネントv2
   * PDP/PLP URLとSEOの構成の簡素化と改善
   * オーサリングモードでのステージングされた製品データの視覚的インジケーターにより、今後の変更の可視性が向上
   * コンテンツページとコマースページ用の新しいサイトマップコンポーネント

* 事前定義済みのレコメンデーションまたはオンザフライで作成されたレコメンデーションを使用した、AEM StorefrontのAdobe Sensei](https://business.adobe.com/products/magento/product-recommendations.html)による[AdobeコマースSensei製品レコメンデーションのサポート

## [!DNL Experience Manager Screens] として  [!DNL Cloud Service] {#screens}

### バグ修正 {#bug-fixes-screens}

* コンテンツプロバイダーの設定は、作成または更新時に検証されるようになりました。

* すべての表示にはフォルダ列があります。

* Screensコンテンツ構造を展開できます。

* `bulk-offline-update-service` 一部の環境のすべての権限が欠落していました。

* ヘルプリンクが更新され、新しいScreensクラウドドキュメントと一致するようになりました。

* プレイリストの割り当てを解除し、プレイヤーを割り当てたプレイリストの削除を許可しないようになりました。

* 「すべて」のキャッシュがクリアされた場合、プレーヤーがアセットを再ダウンロードするようになりました。

* 次の日に&#x200B;*End Time*&#x200B;が設定されている場合、繰り返しスケジュールが機能するようになりました。

* `Back&Forward` は、ScreensでCloud ServiceUIとして機能します。

* 同じ名前で異なる名前空間を持つタグを以前に作成することはできませんでした。

## Cloud ServiceとしてのExperience Managerに関するXMLドキュメント {#xml-documentation}

### 新機能 {#what-is-new-xml-documentation}

Cloud ServiceとしてのExperience ManagerのXMLドキュメントは、一般に利用できます。 Experience Managerのお客様は、Cloud ServiceとしてXMLドキュメントのアドオンを入手し、Experience Managerサイトを含む複数のチャネルにわたって技術コンテンツをインポート、作成、管理、配信できます。

## Cloud Manager {#cloud-manager}

この節では、AEM as a Cloud Service 2021.7.0 に含まれている Cloud Manager のリリースノートの概要を説明しています。

### リリース日 {#release-cm-july}

AEM as aCloud Service2021.7.0のCloud Managerのリリース日は2021年7月15日です。
次回のリリースは2021年8月13日に予定されています。

### 新機能 {#what-is-new-cm-july}

* お客様は、Cloud ManagerのビルドプロセスにAzul 8および11 JDKを使用できるようになり、ツールチェーン互換のMavenプラグインに対してこれらのJDKの1つを使用するか、Mavenプロセスの実行全体を&#x200B;*または*&#x200B;使用するかを選択できます。

* 送信エグレスIPがビルドステップログファイルに記録されます。

* 古いバージョンのAEMを実行しているステージ環境と実稼動環境で、ステータスが&#x200B;**Update Available**&#x200B;とレポートされるようになりました。

* サポートされるSSL証明書の最大数が、プログラムあたり20に増えました。

* 設定できるドメインの最大数は、環境ごとに500に増えました。

* **「Gitを管理」**&#x200B;ボタンのタイトルが&#x200B;**「Git情報にアクセス」**&#x200B;に変更され、ダイアログが視覚的に更新されました。

* Cloud Managerで使用されるAEMプロジェクトアーキタイプのバージョンがバージョン28に更新されました。

### バグ修正 {#bug-fixes-cm-july}

* IP環境をバインドする際に、「プレビュー」オプションが使用できない許可リストが発生することがありました。

* 存在しない実行の実行の詳細ページに手動で移動しても、エラーが表示されず、無限の読み込み画面のみが表示されていた問題を修正しました。

* SSL証明書の最大数に達した場合に表示されるエラーメッセージは役に立ちませんでした。

* 状況によっては、**概要**&#x200B;ページのパイプラインカードに表示されるリリースバージョンに矛盾が生じる場合があります。

* プログラムの追加ウィザードで、作成後に名前を変更できないと誤って表示されていた問題を修正しました。

### 既知の問題 {#known-issues-cm-july}

Azul JDKを使用するように切り替えるお客様は、Azul JDKでエラーなしにコンパイルされるとは限らないことに注意する必要があります。 切り替える前に、ローカルでテストすることを強くお勧めします。

## Cloud Acceleration Manager {#cam}

### リリース日 {#release-date-july-cam}

Cloud Acceleration Managerのリリース日は2021年7月15日です。

### 新機能 {#what-is-new-cam}

Cloud Acceleration Managerは、Cloud Serviceの計画から運用開始まで、移行プロセス全体を通じてITチームを導くように設計されたクラウドベースのアプリケーションです。 Adobeが推奨するベストプラクティス、ヒント、ドキュメント、ツールを使用して、AEMへのCloud Serviceとしてのジャーニーの各段階で役立つように、チームを設定し、移行を成功に導きます。 詳細[こちら](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/getting-started-cam.html?lang=en)。

>[!NOTE]
>
> この[Cloud Acceleration Managerのデモビデオ](https://video.tv.adobe.com/v/335547)を確認してください。
