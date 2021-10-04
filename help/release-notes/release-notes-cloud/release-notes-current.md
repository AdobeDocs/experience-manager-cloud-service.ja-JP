---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 49e88e18e17a2675151a11339a01b3ea7b71d555
workflow-type: tm+mt
source-wordcount: '1628'
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

## リリースビデオ {#release-video}

追加された機能の概要については、[2021 年 8 月リリースの概要 ](https://video.tv.adobe.com/v/336277) ビデオをご覧ください。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] の新機能 {#assets-features}

* デジタルアセットをリンクとして共有する場合、ユーザーは URL をすぐにクリップボードにコピーできます。 この機能強化により、アセットをより迅速かつ便利に共有できます。 この機能により、アセットの共有を迅速かつ便利におこなえます。

   ![アセットをリンクとして共有する場合の「 URL をコピー」オプション](/help/assets/assets/link-share-copy-URL-option.png)
   *図：アセットをリンクとして共有する場合、URL をコピーして別々に共有できるようになりました。*

* TXT ファイルをアップロードすると、アセットマイクロサービスによって自動的にサムネールが生成されます。 PNG サムネールは TXT ファイルのレンディションで、ユーザーがファイルを開かずに、コンテンツやファイルをある程度識別するのに役立ちます。 この機能は設定を必要とせず、デフォルトで機能します。

   ![TXT ファイルのレンディションは、PNG 形式でに [!DNL Assets] 自動的に生成されます](/help/assets/assets/thumbnail-rendition-txt-file.png)
   *図：TXT ファイルのレンディションが自動的に生成され、ファイルを開かずに識別できます。*

### [!DNL Assets] プレリリースチャネルの新機能 {#assets-prerelease-features}

* 列表示およびカード表示で、検索結果に表示されたアセットを並べ替えることができるようになりました。 並べ替えは、「名前」、「作成済み」、「変更済み」、「なし」の各列で行います。

   ![列表示およびカード表示での [!DNL Assets] 検索結果の並べ替え](/help/assets/assets/sort-searched-assets.png)
   *図：列表示およびカード表示で [!DNL Assets] 検索結果を並べ替えます。*

### [!DNL Assets] で修正されたバグ {#assets-bugs-fixed}

* コントリビューターグループのメンバーが [!DNL Assets] コンソールに移動すると、コレクションを作成するための追加の `POST` 要求が生成されます。 このリクエストは必須ではなく、権限の問題が原因で失敗し、多くのエラーがログに作成されます。 （CQ-4328856）
* ユーザーがアセットを表示し、左側のパネルのポップアップメニューから「[!UICONTROL  タイムライン ]」を選択すると、エラーが表示されます。 ログでは、クエリが正しくないため、多くの警告が記録されます。 （CQ-4328919）

## [!DNL Experience Manager Forms] as a  [!DNL Cloud Service] {#forms}

### [!DNL Forms] の新機能 {#what-is-new-forms}

<!-- * Automated Forms Conversion service can [convert PDF Forms in Italian and Portuguese language](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model) to Adaptive Forms. -->

* Forms as aCloud ServiceのAEMアーキタイププロジェクトに、Microsoft Dynamics および Salesforce.com の [ フォームデータモデルが含まれるようになりました。](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/setup-environment/setup-local-development-environment.html?#forms-cloud-service-local-development-environment)

* **AcroForm ベースのレコードのドキュメント**：AEM Forms as a Cloud Service では、XFA ベースのフォームテンプレート以外に、[Adobe Acrobat フォーム PDF（AcroForm PDF）](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html?lang=ja)をレコードのドキュメントのテンプレートとして使用できます。

* **Microsoft Azure データストアコネクタ**：[フォームデータモデルを Microsoft Azure Storage に接続](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html?lang=ja)できるようになりました。アダプティブフォームデータを取得して、Microsoft Azure ストレージに BLOB として保存することができます。

### [!DNL Forms] のベータ版機能 {#aug-what-is-new-forms-prerelease}

* **統合ストレージコネクタ：**&#x200B;統合ストレージコネクタを使用すると、顧客側で管理されるリポジトリー内の処理中のデータを外部化することができます。例えば、次のことができます。
   * Forms ポータルの保存および再開機能を有効にし、顧客側で管理されるデータリポジトリーにアダプティブフォームのドラフトを格納する
   * 個人の機密情報（SPD）を含んだ処理中の AEM ワークフローデータ（AEM ワークフロー変数データ）を、顧客側で管理されるリポジトリーに格納する

* **[!DNL AEM Forms as a Cloud Service - Communications]**：[通信 API](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/aem-forms-cloud-service-communications.html?lang=ja) では、XDP テンプレートと XML データを組み合わせて、様々な形式の印刷用ドキュメントを生成できます。このサービスを使用すると、ドキュメントを同期モードで生成できます。この API により、以下の機能を備えたアプリケーションを作成できます。
   * テンプレートファイルに XML データを入力することでドキュメントを生成する
   * 非インタラクティブ PDF 印刷ストリームを含む様々な形式の出力フォームを生成する
   * XFA フォーム PDF および Adobe Acrobat フォームから印刷用 PDF ファイルを生成する

ベータ版プログラムに新規登録するには、[!DNL formscsbeta@adobe.com] 宛てに電子メールを送信します。

### [!DNL Forms] プレリリースチャネルで利用できる新機能 {#prerelease-features-forms}

* **アダプティブフォームでの Adobe Sign の役割の使用**：ビジネスおよびエンタープライズサービスレベルの Adobe Sign では、ワークフロー要件に適切に合致するように、契約書受信者の役割を署名者以外にも拡大できます。[契約書の受信者ごとに、アダプティブフォームでの自分の役割を設定できる](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/use-adobe-sign/working-with-adobe-sign.html?#addsignerstoanadaptiveform)ようになりました。デフォルトの役割は署名者です。

* **アダプティブフォーム用の Analytics**：アダプティブフォーム用の Adobe Analytics でエンドユーザーの行動を捉えて追跡し、エンドユーザーのインサイトを収集できるようになりました。十分な情報に基づいて決定をおこない、エンドユーザーエクスペリエンスを向上させることができます。

* **AEM Formsを Microsoft Dynamics および Salesforce.com に簡単に接続**:このサービスは、Microsoft Dynamics と Salesforce.com 用の標準のデータソース設定とデータモデルを提供し、開発者が Microsoft Dynamics と Salesforce.com をアダプティブフォームのデータソースとしてより迅速かつ簡単に設定できま [す](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-msdynamics-salesforce.html)。

## [!DNL Experience Manager Screens] as a  [!DNL Cloud Service] {#screens}

### 新機能 {#what-is-new-screens}

* Cloud Serviceとしての Screens で、基本的な再生監視がサポートされるようになりました。 現在は、各 ping で様々な再生指標が報告されます（デフォルトは 30 秒）。 指標に基づいて、様々なエッジケース（動きのないエクスペリエンス、空白の画面、スケジュールの問題など）を検出する機能を提供します。 この機能を使用すると、プレーヤーがコンテンツを適切に再生しているかどうかをチームがリモートで監視し、空白の画面やフィールド内の壊れたエクスペリエンスに対する反応を改善して、エンドユーザーに壊れたエクスペリエンスを表示するリスクを低減できます。
詳しくは、[ 基本的な再生監視 ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/manage-player-registration/installing-screens-cloud-player.html?lang=en#playback-monitoring) を参照してください。

* でのビデオのサムネールのサポートが、Screens でCloud Serviceとしてサポートされるようになりました。 コンテンツ作成者は、ビデオのサムネールを定義して、画像をプレースホルダーとして使用し、コンテンツの再生とターゲティングを適切にテストしながら、実際のビデオを適切なチームが完了させることができます。 また、ビデオの再生に失敗した場合にも、画像を使用できます。
詳しくは、[ ビデオのサムネールのサポート ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/core-product-features/thumbnail-support-videos.html) を参照してください。

### バグ修正 {#bug-fixes-screens}

* 埋め込みページのコンテンツをプレーヤーに表示できず、この問題が修正されました。

* ログインに成功した後、デフォルトのページ（チャネル）に移動すると、内部サーバーエラーページが表示されます。

* プレイリストを削除する際に、関連するタグエントリが削除されませんでした。


## CIF アドオン {#cloud-services-cif}

### 新機能 {#what-is-new-cif}

* 新しいカテゴリピッカー UI により、ユーザーエクスペリエンスの向上、効率の向上、複雑な製品カタログのサポートの向上を実現

   ![新しいカテゴリピッカー](/help/assets/CIF/category-picker.png)

* CIF コアコンポーネントのサポートの向A11Y

## Cloud Manager  {#cloud-manager}

この節では、AEM as a Cloud Service 2021.9.0 および 2021.8.0 に含まれている Cloud Manager のリリースノートの概要を説明しています。

## リリース日 {#release-date-cm-sept}

AEM as aCloud Service2021.9.0 の Cloud Manager のリリース日は 2021 年 9 月 09 日です。
次回のリリースは 2021 年 10 月 7 日（PT）に予定されています。

### 新機能 {#what-is-new-cm-sept}

* Cloud Manager で使用される AEM プロジェクトアーキタイプのバージョンが 30 に更新されました。

* Cloud Manager ランディングページのプログラムカードと関連するエクスペリエンスが新しくなりました。

* コード品質ステップログに、OakPal スキャンプロセスの詳細なログ情報が含まれるようになりました。

* アクティビティページのメニューオプションに、完了したコードジェネレーターの実行に対して **ログをダウンロード** するオプションが追加されました。 これを選択すると、ビルド手順のログがダウンロードされます。

* 「プログラム」カードを直接クリックすると、Cloud Manager の概要ページに移動するようになりました。


### バグ修正 {#bug-fixes-sept}

* 設定可能な IP許可リストの最大数に達したプログラムに新しい IP許可リストを追加しようとすると、わかりやすいメッセージが表示されるようになりました。

* リポジトリ画面で　URL　コピーメニューオプションを選択すると、間違った　URL　がコピーされていました。

## リリース日 {#release-date-cm-aug}

AEM as aCloud Service2021.8.0 の Cloud Manager のリリース日は 2021 年 8 月 12 日です。

### 新機能 {#what-is-new-aug}

* Cloud Serviceのお客様は、Cloud Manager でサービス契約 (SLA) レポートを表示できるようになりました。 これは今後数ヶ月間徐々に利用可能になる予定です。
詳しくは、[SLA レポート ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sla-reporting.html) を参照してください。

* IndexType と `IndexDamAssetLucene` 品質ルールの種類と重大度が変更されました。 現在は両方ともブロッカー *serverity* のバグです。

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

コンテンツ転送ツール v1.5.6 のリリース日は 2021 年 8 月 11 日です。

### バグ修正 {#bug-fixes-ctt}

* 場合によっては、一部のユーザーがターゲットインスタンスに移行されないことがあります。 この修正を受けるには、ターゲットAEM上の aem-ethos-tools 1.2.354 以降のバージョンと共に、Cloud Serviceインスタンスとして CTT v1.5.6 が必要です。

* パブリッシュインスタンスへの取り込み中に、「**取り込みを停止**」ボタンが無効になっていた問題を修正しました。 公開の取り込み中に Mongo の復元手順がないので、この操作は不要です。

* CTT は、抽出が正常に完了した後に `/tmp` ディレクトリをクリーンアップしませんでした。 これにより、ディスク容量の問題が発生する場合がありました。

## ベストプラクティスアナライザー {#best-practices-analyzer}

### リリース日 {#release-date-bpa-latest}

Best Practices Analyzer v2.1.18 のリリース日は 2021 年 9 月 2 日です。

### 新機能 {#what-is-new}

* ノード数の合計を検出し、レポートする機能。

* ノードストアのタイプとサイズを検出し、レポートする機能。

### バグ修正 {#bug-fixes-bpa}

* BPA が誤ってコマース統合フレームワークの存在を検出しました。

