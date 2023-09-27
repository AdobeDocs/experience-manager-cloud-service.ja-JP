---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.7.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.7.0 リリースのリリースノート。'
exl-id: 848f6a29-2e0f-4976-8ed7-6b7f69408c1b
source-git-commit: f956b8379b5b93bc00e25f0eec641430c5565e34
workflow-type: tm+mt
source-wordcount: '1319'
ht-degree: 58%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート {#release-notes}

以下では、[!DNL Experience Manager] as a Cloud Service の現在（最新）のバージョンのリリースノート全般の概要を説明します。

>[!NOTE]
>
>ここから、以前のバージョンのリリースノート（2020 年と 2021 年のバージョンなど）に移動できます。

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a 
[!DNL Cloud Service]の現在リリース（2021.7.0）のリリース日は 2021 年 7 月 29 日です。次のリリース（2021.8.0）は 2021 年 8 月 26 日です。

## リリースビデオ {#release-video}

追加された機能の概要については、](https://video.tv.adobe.com/v/335580)2021 年 7 月リリースの概要ビデオ[をご覧ください。

## Experience Manager Foundation as a Cloud Service {#foundation}

### 新着情報 {#what-is-new-foundation}

* より柔軟な Dispatcher 設定：プロジェクトをより簡単に整理できます。 例えば、サイト構造を反映した複数の書き換えルールファイルを含めることができるようになりました。[詳細](/help/implementing/dispatcher/disp-overview.md#validation-debug) この柔軟なモードには、Dispatcher 設定を構築して活用する方法などがあります。
* レプリケーションエージェントの「配布」タブのツリーレプリケーション UI は、廃止済みと見なされ、2021 年 9 月 30 日以降に削除されました。 代替レプリケーション戦略について[ご確認](/help/operations/replication.md#tree-activation)ください。
* Sling 用 `org.apache.sling.datasource-1.0.4.jar` データソースサポート用バンドルは、機能が古く、顧客に使用されていないので、削除されました。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### の新機能[!DNL Assets] {#assets-features}

* コンテンツ自動化機能により、 [!DNL Experience Manager Assets] を使用します。 [!DNL Adobe Creative Cloud] 大規模なアセット作成を自動化する API。 同じアセットのバリエーションを作成するのに必要な時間と繰り返しを大幅に減らし、コンテンツベロシティを向上させます。この機能はプログラミングを必要とせず、DAM 内で動作します。[アセットの統合を使用して Creative Cloud のバリエーションを生成する](/help/assets/cc-api-integration.md)を参照してください。

* [!DNL Experience Manager Assets] には [!DNL Document Cloud] PDF ビューアが含まれており、PDF ドキュメントをネイティブにプレビューできます。この機能を使用すると、ファイルの処理や変換をおこなわずに、複数ページの PDF ファイルをプレビューできます。この機能により、[!DNL Experience Manager] 6.5 と同等の機能が使用できるようになりました。ビューアで使用できるコントロールには、ズーム、ページへ移動、ドッキング解除、全画面表示などがあります。また、プレビューしたり、ページやブックマークにジャンプしたりすることもできます。 ファイル自体に対するコメントがサポートされます。 PDFファイル内のコンテンツに対するコメントと注釈は、今後のリリースで提供される予定です。

  ![PDF ビューアを使用した [!DNL Experience Manager] での PDF ファイルのプレビュー](/help/assets/assets/preview-pdf-file-viewer.png)

* リンク共有のダウンロード機能では、非同期ダウンロードを使用してダウンロード速度を上げます。 詳しくは、 [リンク共有を使用して共有されたアセットをダウンロードする](/help/assets/download-assets-from-aem.md#link-share-download).

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

* これで、Automated forms conversionサービスを [PDF formsをフランス語、ドイツ語、スペイン語で変換する](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=ja#language-specific-meta-model) をアダプティブフォームに追加します。
* アダプティブフォームのコンポーネントに関連するエラーを表示するためのパネルをテンプレートエディターに別に追加しました。 これにより、すべてのアダプティブフォームのエラーが 1 か所に集約されるので、解決に要する時間を短縮できます。

### [!DNL Forms]プレリリースチャネルで利用できる新機能 {#beta-features-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**：[通信 API](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications.html) では、XDP テンプレートと XML データを組み合わせて、様々な形式の印刷用ドキュメントを生成できます。このサービスを使用すると、同期モードでドキュメントを生成できます。 API により、以下のような機能を備えたアプリケーションを作成することができます。
   * テンプレートファイルに XML データを格納することで、最終形式のドキュメントを生成します。
   * 非インタラクティブ PDF 印刷ストリームを含む様々な形式で出力フォームを生成します。
   * XFA フォーム PDF および Adobe Acrobat フォームから印刷用 PDF ファイルを生成します。

* **Variable Data Externalizer**：AEM ワークフロー変数のデータを、組織で管理される外部ストレージシステムに保存できます。

* **Acroform べースのレコードのドキュメント**：XFA ベースのフォームテンプレート以外にも、[Adobe Acrobat Form PDF（Acroform PDF）](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/generate-document-of-record-for-non-xfa-based-adaptive-forms.html?lang=ja) を、レコードドキュメントのテンプレートとして使用することもできます。

* **Microsoft® Azure データストアコネクタ**：次が可能です。 [フォームデータモデルをMicrosoft® Azure ストレージに接続する](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-azure-storage.html). これにより、アダプティブフォームのデータを取得し、BLOB としてMicrosoft® Azure Storage に保存することができます。

## CIF アドオン {#cloud-services-cif}

### 新機能 {#what-is-new-cif}

* CIF コアコンポーネント v2
   * PDP/PLP URL と SEO の構成の簡素化と改善
   * オーサリングモードでのステージングされた製品データの視覚的インジケーターにより、今後の変更の可視性が向上
   * コンテンツページとコマースページ用の新しいサイトマップコンポーネント

* 事前定義済みのレコメンデーションまたはオンザフライで作成されたレコメンデーションを使用した、AEM Storefront の Adobe Sensei](https://business.adobe.com/jp/products/magento/product-recommendations.html) による [Adobe Commerce Sensei 製品レコメンデーションのサポート

## [!DNL Experience Manager Screens] as a [!DNL Cloud Service] {#screens}

### バグ修正 {#bug-fixes-screens}

* コンテンツプロバイダーの設定は、作成または更新時に検証されるようになりました。

* すべての表示ビューにはフォルダ列があります。

* Screens コンテンツ構造を展開できます。

* `bulk-offline-update-service` 一部の環境のすべての権限が欠落していました。

* ヘルプリンクが更新され、新しい Screens クラウドドキュメントと一致するようになりました。

* プレイリストの割り当てを解除し、プレーヤーが割り当てられたプレイリストの削除を許可しなくなりました。

* 「すべて」のキャッシュがクリアされると、プレーヤーがアセットを再ダウンロードするようになりました。

* スケジュール設定を今すぐ繰り返す ( *終了時刻* が翌日に設定されます。

* `Back&Forward` が、Screens as a Cloud Service UI で機能するようになりました。

* 同じ名前で異なる名前空間を持つタグを以前に作成することはできませんでした。

## Experience Manager as a Cloud Service の XML ドキュメント {#xml-documentation}

### 新機能 {#what-is-new-xml-documentation}

Experience Manager as a Cloud Service の XML ドキュメントが一般利用可能になりました。これにより、as a Cloud ServiceのExperience Managerのお客様がXML Documentationアドオンを調達して、Experience Manager Sitesを含む複数のチャネルにわたって技術コンテンツを読み込み、作成、管理および配信できます。

## Cloud Manager {#cloud-manager}

この節では、AEM as a Cloud Service 2021.7.0 に含まれている Cloud Manager のリリースノートの概要を説明しています。

### リリース日 {#release-cm-july}

AEM as a Cloud Service 2021.7.0 の Cloud Manager のリリース日は 2021 年 7 月 15 日です。次回のリリースは 2021年8月12日（PT）に予定されています。

### 新機能 {#what-is-new-cm-july}

* お客様は、Cloud Manager のビルドプロセスに Azul 8 および 11 JDK を使用できるようになり、ツールチェーン互換の Maven プラグインにこれらの JDK の 1 つを使用するように選択できます。 *または* Maven プロセスの実行全体。

* 送信エグレス IP がビルドステップのログファイルに記録されます。

* 古いバージョンのAEMを実行するステージ環境と実稼動環境で、「 **更新可能**.

* サポートされる SSL 証明書の最大数が、プログラムあたり 20 に増えました。

* 設定できるドメインの最大数が、環境あたり 500 に増えました。

* The **Git を管理** ボタンのタイトルが次の値に変更されました： **Git 情報にアクセス** ダイアログボックスが視覚的に更新されました。

* Cloud Manager で使用される AEM プロジェクトアーキタイプのバージョンが 28 に更新されました。

### バグ修正 {#bug-fixes-cm-july}

* IP 環境を環境にバインドする際に、プレビューを使用できない許可リストに加える場合がありました。

* 存在しない実行の実行詳細ページに手動で移動しても、エラーが表示されず、読み込みが無限に繰り返される画面が表示されるだけでした。

* SSL 証明書の最大数に達した場合に表示されるエラーメッセージが役に立ちませんでした。

* 状況によっては、**概要**&#x200B;ページのパイプラインカードに表示されるリリースバージョンが矛盾していることがありました。

* プログラムの追加ウィザードで、作成後に名前を変更できないと誤って表示されていました。

### 既知の問題 {#known-issues-cm-july}

Azul JDK を使用するように切り替えるお客様は、Azul JDK でエラーなしにコンパイルされない既存のアプリケーションがあることを知っている必要があります。 Adobeでは、切り替える前にローカルでテストすることをお勧めします。

## Cloud Acceleration Manager {#cam}

### リリース日 {#release-date-july-cam}

Cloud Acceleration Manager のリリース日は 2021 年 7 月 15 日です。

### 新機能 {#what-is-new-cam}

Cloud Acceleration Manager は、Cloud Service の計画から運用開始まで、移行プロセス全体を通じて IT チームをガイドするために設計されたクラウドベースのアプリケーションです。Adobeが推奨するベストプラクティス、ヒント、ドキュメント、ツールを使用して、AEMへのCloud Serviceとしてのジャーニーのあらゆる段階で役立つように、チームを設定して移行を成功させます。 詳細は[こちら](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/getting-started-cam.html?lang=en)をご覧ください。

>[!NOTE]
>
> ご確認ください [Cloud Acceleration Manager のデモビデオ](https://video.tv.adobe.com/v/335547).
