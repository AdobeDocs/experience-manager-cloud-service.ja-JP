---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 534fd193181fe22392fb598625d3a018a4a09e69
workflow-type: tm+mt
source-wordcount: '1628'
ht-degree: 24%

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

[!DNL Adobe Experience Manager]のリリース日(2021.8.0)は2021年8月26日です。
[!DNL Cloud Service]次のリリース(2021.9.0)は2021年9月30日です。

## リリースビデオ {#release-video}

追加された機能の概要については、 2021年8月リリースの概要](https://video.tv.adobe.com/v/336277)ビデオをご覧ください。[

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets]の新機能 {#assets-features}

* デジタルアセットをリンクとして共有する場合、ユーザーはURLをすぐにクリップボードにコピーできます。 この機能強化により、アセットをより迅速かつ便利に共有できます。 この機能により、アセットを迅速かつ便利に共有できます。

   ![アセットをリンクとして共有する場合の「 URLをコピー」オプション](/help/assets/assets/link-share-copy-URL-option.png)
   *図：アセットをリンクとして共有する場合、URLをコピーして別々に共有できるようになりました。*

* TXTファイルをアップロードすると、アセットマイクロサービスによって自動的にサムネールが生成されます。 PNGサムネールは、ユーザーがファイルを開かずに、コンテンツやファイルをある程度識別するのに役立つTXTファイルのレンディションです。 この機能は設定を必要とせず、デフォルトで機能します。

   ![TXTファイルのレンディションは、PNG形式でに自 [!DNL Assets] 動的に生成されます](/help/assets/assets/thumbnail-rendition-txt-file.png)
   *図：TXTファイルのレンディションは、開かずにファイルを識別できるように、自動的に生成されます。*

### [!DNL Assets]プレリリースチャネルの新機能 {#assets-prerelease-features}

* 列表示およびカード表示で、検索結果に表示されるアセットを並べ替えることができるようになりました。 並べ替えは、「名前」、「作成済み」、「変更済み」、「なし」のいずれかの列で行います。

   ![列表示とカード表示での [!DNL Assets] 検索結果の並べ替え](/help/assets/assets/sort-searched-assets.png)
   *図：列表示およびカード表示で [!DNL Assets] の検索結果の並べ替え*

### [!DNL Assets] で修正されたバグ {#assets-bugs-fixed}

* 寄稿者グループのメンバーが[!DNL Assets]コンソールに移動すると、コレクションを作成するための追加の`POST`要求が生成されます。 このリクエストは必須ではなく、権限の問題が原因で失敗し、多くのエラーがログに作成されます。 （CQ-4328856）
* ユーザーがアセットを表示し、左側のパネルのポップアップメニューから「[!UICONTROL タイムライン]」を選択すると、エラーが表示されます。 ログでは、不正なクエリが原因で多くの警告が記録されます。 （CQ-4328919）

## [!DNL Experience Manager Forms] として  [!DNL Cloud Service] {#forms}

### [!DNL Forms] の新機能 {#what-is-new-forms}

<!-- * Automated Forms Conversion service can [convert PDF Forms in Italian and Portuguese language](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model) to Adaptive Forms. -->

* Forms as aCloud ServiceのAEMアーキタイププロジェクトに、Microsoft DynamicsおよびSalesforce.comの[フォームデータモデルが含まれるようになりました。](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/setup-environment/setup-local-development-environment.html?#forms-cloud-service-local-development-environment)

* **Acroformベースのレコードのドキュメント**:AEM Forms as aCloud Serviceでは、 [Adobe Acrobat Form PDF(Acroform PDF)](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html?lang=ja) を、XFAベースのフォームテンプレート以外のレコードのドキュメントのテンプレートとして使用することができます。

* **Microsoft Azure データストアコネクタ**：[フォームデータモデルを Microsoft Azure Storage に接続](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html?lang=ja)できるようになりました。アダプティブフォームデータを取得して、Microsoft Azure ストレージに BLOB として保存することができます。

### [!DNL Forms] のベータ版機能 {#aug-what-is-new-forms-prerelease}

* **統合ストレージコネクタ：** 統合ストレージコネクタを使用して、顧客管理リポジトリ内の処理中のデータを外部化します。例えば、
   * Forms Portalの保存と再開機能を有効にし、アダプティブフォームのドラフトを顧客管理データリポジトリに保存します。
   * 顧客が管理するリポジトリに、機密性の高い個人データ(SPD)を含むプロセス内のAEM Workflowsデータ(AEM Workflow Variablesデータ)を格納します。

* **[!DNL AEM Forms as a Cloud Service - Communications]**：[通信 API](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/aem-forms-cloud-service-communications.html?lang=ja) では、XDP テンプレートと XML データを組み合わせて、様々な形式の印刷用ドキュメントを生成できます。このサービスを使用すると、ドキュメントを同期モードで生成できます。この API により、以下の機能を備えたアプリケーションを作成できます。
   * テンプレートファイルに XML データを入力することでドキュメントを生成する
   * 非インタラクティブ PDF 印刷ストリームを含む様々な形式の出力フォームを生成する
   * XFA フォーム PDF および Adobe Acrobat フォームから印刷用 PDF ファイルを生成する

ベータ版プログラムに新規登録するには、[!DNL formscsbeta@adobe.com] 宛てに電子メールを送信します。

### [!DNL Forms] プレリリースチャネルで利用できる新機能 {#prerelease-features-forms}

* **アダプティブフォームでのAdobe Signの役割の使用**:Adobe Sign for business and enterpriseサービスレベルでは、署名者だけでなく、契約の受信者の役割を拡張して、ワークフロー要件に合わせることができます。同意書の各受信者がアダプティブフォーム](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/use-adobe-sign/working-with-adobe-sign.html?#addsignerstoanadaptiveform)で自分の役割を設定できるようになりました。署名者はデフォルトの役割です。[

* **Analytics for Adaptive Forms**:Adobe Analyticsを介してエンドユーザーの行動をキャプチャおよび追跡し、アダプティブFormsでエンドユーザーのインサイトを収集できるようになりました。情報に基づくデータ決定をおこない、エンドユーザーエクスペリエンスを向上させるのに役立ちます。

* **AEM FormsをMicrosoft DynamicsおよびSalesforce.comに簡単に接続できます**。このサービスは、Microsoft DynamicsとSalesforce.com用の標準のデータソース設定とデータモデルを提供し、開発者がMicrosoft DynamicsとSalesforce.comをアダプティブフォームのデータソースとしてより迅速かつ簡単に設定できま [す](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-msdynamics-salesforce.html)。

## [!DNL Experience Manager Screens] として  [!DNL Cloud Service] {#screens}

### 新機能 {#what-is-new-screens}

* Cloud ServiceとしてのScreensで、基本的な再生監視がサポートされるようになりました。 プレーヤーでは、各pingで様々な再生指標がレポートされるようになります（デフォルトは30秒）。 指標に基づいて、様々なエッジケース（動きのないエクスペリエンス、空白画面、スケジュールの問題など）を検出できます。 この機能を使用すると、プレーヤーがコンテンツを適切に再生しているかどうかをチームがリモートで監視し、空白の画面やフィールド内のエクスペリエンスの破損に対する反応性を向上し、エンドユーザーに壊れたエクスペリエンスを表示するリスクを低減できます。
詳しくは、[基本的な再生監視](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/manage-player-registration/installing-screens-cloud-player.html?lang=en#playback-monitoring)を参照してください。

* でのビデオのサムネールのサポートが、Screens as aCloud Serviceとしてサポートされるようになりました。 コンテンツ作成者は、ビデオのサムネールを定義して、画像をプレースホルダーとして使用し、コンテンツの再生とターゲティングを適切にテストしながら、実際のビデオを適切なチームで確定できます。 ビデオの再生に失敗した場合にも、画像を使用できます。
詳しくは、[ビデオのサムネールのサポート](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/core-product-features/thumbnail-support-videos.html)を参照してください。

### バグ修正 {#bug-fixes-screens}

* 埋め込みページのコンテンツをプレーヤーに表示できなかったので、この問題は修正されました。

* ログインに成功した後、デフォルトのページ（チャネル）に移動すると、内部サーバーエラーページが表示されます。

* プレイリストを削除する際に、関連するタグエントリが削除されませんでした。


## CIFアドオン {#cloud-services-cif}

### 新機能 {#what-is-new-cif}

* 新しいカテゴリピッカーUIにより、ユーザーエクスペリエンスの向上、効率の向上、複雑な製品カタログのサポートの向上を実現

   ![新しいカテゴリピッカー](/help/assets/CIF/category-picker.png)

* CIFコアコンポーネントのサポートの向A11Y

## Cloud Manager  {#cloud-manager}

この節では、AEM as a Cloud Service 2021.9.0 および 2021.8.0 に含まれている Cloud Manager のリリースノートの概要を説明しています。

## リリース日 {#release-date-cm-sept}

AEM as aCloud Service2021.9.0のCloud Managerのリリース日は2021年9月09日です。
次回のリリースは2021年10月7日に予定されています。

### 新機能 {#what-is-new-cm-sept}

* Cloud Manager で使用される AEM プロジェクトアーキタイプのバージョンが 30 に更新されました。

* Cloud Managerランディングページのプログラムカードと関連するエクスペリエンスが更新されました。

* コード品質ステップログに、OakPalスキャンプロセスの詳細なログ情報が含まれるようになりました。

* アクティビティページのメニューオプションに、コードジェネレーターの実行完了時に&#x200B;**ログをダウンロード**&#x200B;するオプションが追加されました。 これを選択すると、ビルド手順のログがダウンロードされます。

* 「プログラム」カードを直接クリックして、 Cloud Managerの概要ページに移動するようになりました。


### バグ修正 {#bug-fixes-sept}

* 設定可能なIP許可リストの最大数に達したプログラムに新しいIP許可リストを追加しようとすると、よりわかりやすくなるメッセージが表示されるようになりました。

* リポジトリ画面でURLコピーメニューオプションを選択すると、間違ったURLがコピーされていました。

## リリース日 {#release-date-cm-aug}

AEM as aCloud Service2021.8.0のCloud Managerのリリース日は2021年8月12日です。

### 新機能 {#what-is-new-aug}

* Cloud Serviceのお客様は、Cloud Managerでサービスレベル契約(SLA)レポートを表示できるようになりました。 これは今後数ヶ月間徐々に利用可能になる予定です。
詳しくは、[SLAレポート](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sla-reporting.html)を参照してください。

* IndexTypeと`IndexDamAssetLucene`品質ルールの種類と重大度が変更されました。 現在は、これらは&#x200B;*サーバー性*&#x200B;のブロッカーのバグです。

* 非同期およびtikaの設定をカバーする新しいOakインデックス品質ルールが導入されました。

* プログラムごとの最大SSL証明書数を50に増やします。

* ユーザーが Cloud Manager UI を使用して複数のリポジトリを作成および管理できるセルフサービス機能。

* SonarQubeがGitの履歴データを不必要に読み取っていた問題を修正しました。 大規模なコードベースでは、これにより、ビルドパフォーマンスが不必要に低下することがありました。

* パイプラインごとに Maven 依存関係キャッシュを無効にする API が追加されました。

* Cloud Manager で使用される AEM プロジェクトアーキタイプのバージョンが 29 に更新されました。

### バグ修正 {#bug-fixes-aug}

* 最新のリリースが現在のリリースより前の場合は、更新可能ステータスは表示されるべきではありません。

* 名前が非常に長い新しい組織で、最初のオンボーディングが失敗していました。

* 何らかの理由でパイプラインが 2 回トリガーされた場合、「*パイプライン実行ステータスを更新できませんでした*」エラーで、いずれかの実行が失敗します。

## コンテンツ転送ツール {#content-transfer-tool}

### リリース日 {#release-date-ctt-latest}

コンテンツ転送ツールv1.5.6のリリース日は2021年8月11日です。

### バグ修正 {#bug-fixes-ctt}

* 場合によっては、一部のユーザーがターゲットインスタンスに移行されないことがありました。 この修正を受けるには、ターゲットAEM as aCloud Serviceインスタンス上のaem-ethos-tools 1.2.354以降のバージョンと共に、CTT v1.5.6が必要です。

* パブリッシュインスタンスへの取り込み中に、「**取り込みを停止**」ボタンが無効になっていた問題を修正しました。 パブリッシュの取り込み中にMongoの復元手順がないので、この操作は必要ありません。

* CTTは、抽出が正常に完了した後、`/tmp`ディレクトリをクリーンアップしませんでした。 これにより、ディスク容量の問題が発生することがありました。

## ベストプラクティスアナライザー {#best-practices-analyzer}

### リリース日 {#release-date-bpa-latest}

Best Practices Analyzer v2.1.18のリリース日は2021年9月2日です。

### 新機能 {#what-is-new}

* ノード数の合計を検出し、レポートする機能。

* ノードストアのタイプとサイズを検出し、レポートする機能。

### バグ修正 {#bug-fixes-bpa}

* BPAが、コマース統合フレームワークの存在を誤って検出しました。

