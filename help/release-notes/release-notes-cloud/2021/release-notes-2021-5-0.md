---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.5.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.5.0 リリースのリリースノート。'
source-git-commit: 6a81e04a7de657d222cdd965fb6e2d4351b4c338
workflow-type: tm+mt
source-wordcount: '1380'
ht-degree: 44%

---


# [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート  {#release-notes}

以下では、[!DNL Experience Manager] as a Cloud Service の現在（最新）のバージョンのリリースノート全般の概要を説明します。

>[!NOTE]
>ここから、以前のバージョン（例えば、2020 年、2021 年のバージョンなど）のリリースノートに移動できます。

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a Cloud Service 2021.5.0 のリリース日は 2021 年 5 月 27 日です。次のリリース(2021.6.0)は、2021年6月29日に予定されています。

## AEM as a Cloud Service の基盤 {#foundation}

### AEM as a Cloud Service基盤の新機能 {#what-is-new-foundation}

* [プレリリースチャネル](/help/release-notes/prerelease.md):本番運用開始前の1ヶ月間に予定されている機能のプレビュー

* [APIの廃止](/help/release-notes/deprecated-apis.md):AEM as a Experienceの最新の非推奨APIのリストをご利用いただけます。Cloud Service

* [AEM as aCloud ServiceSDK Build Analyzer Mavenプラグイン](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html):非推奨のJava APIチェックやその他の改善点を含む、Mavenプロジェクトを最新バージョンに更新します。

## [!DNL Adobe Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] の新機能  {#what-is-new-sites}

* 近日中に、新しい[プレビュー層](/help/sites-cloud/authoring/fundamentals/previewing-content.md)でコンテンツを検証して、パブリッシュ層と同じように最終的なエクスペリエンスのルックアンドフィールをシミュレートできます。 これは、AEM Sites Managed Publishionウィザードで有効になり、公開またはプレビューのどちらかの公開先を選択できるようになりました。 プレビュー時のエクスペリエンスは、専用のURLからアクセスできます。 プレビューでの検証後、通常どおりコンテンツをオーサーからパブリッシュに公開できます。 AEM as a Cloud Service環境でのPreview Serviceの有効化は、今後数週間で徐々に展開される予定です。

## [!DNL Adobe Experience Manager Assets] として  [!DNL Cloud Service] {#assets}

### [!DNL Assets] の新機能  {#what-is-new-assets}

* リンク共有機能を使用して、共有したアセットをダウンロードできます。 このダウンロードでは、非同期サービスを使用するようになり、非常に大きなダウンロードでも、高速で中断のないダウンロードを提供します。 詳しくは、「[アセットのダウンロード](/help/assets/download-assets-from-aem.md#link-share-download)」を参照してください。

   ![ダウンロードインボックス](/help/assets/assets/download-inbox.png)

### プレリリースチャネルで使用できる新機能 {#what-is-new-assets-prerelease}

* メタデータスキーマは、フォルダーのプロパティに直接適用できます。

   ![フォルダープロパティからのメタデータスキーマの追加](/help/assets/assets/metadata-schema-folder-properties.png)

* アセット一括取り込みツールを使用すると、一括取り込み中にメタデータを追加できます。

* ユーザーエクスペリエンスの機能強化では、フォルダー内に存在するアセットの数が表示されます。 1つのフォルダー内のアセットが1000個を超える場合、[!DNL Assets]には1000以上と表示されます。

   ![フォルダー内のアセット数がインターフェイスに表示されます](/help/assets/assets/browse-folder-number-of-assets.png)

### [!DNL Assets] で修正されたバグ  {#assets-bugs-fixed}

* 非常に大きなファイルをアップロードすると、[!DNL Experience Manager desktop app]がクラッシュします。 （CQ-4320942）
* フォルダー内で同じコレクションが選択されている場合と、検索結果から同じコレクションが選択されている場合で、ツールバーのオプションは異なります。 （CQ-4321406）

#### Dynamic Mediaの新機能 {#what-is-new-dm}

* スマートイメージングDPR(Device Pixel Ratio)とネットワーク帯域幅の最適化により、高解像度のディスプレイとネットワーク帯域幅の制約があるデバイスで、最高品質の画像を効率的に配信できます。 詳しくは、[スマートイメージングのFAQ](/help/assets/dynamic-media/imaging-faq.md)を参照してください。

   >[!NOTE]
   >
   >上記のスマートイメージング機能強化のリリースタイムラインは、次のとおりです。
   >
   >* 北米2021年5月24日、NA、
      >
      >
   * ヨーロッパ、中東、アフリカ2021年6月25日、
      >
      >
   * アジア太平洋2021年7月19日。


* Dynamic Media配信で、次世代画像形式AVIFのサポートが導入されました（fmt URL修飾子）。

   >[!NOTE]
   >
   >AVIFサポートのリリースタイムラインは次のとおりです。
   >
   >* 北米2021年5月10日、
      >
      >
   * ヨーロッパ、中東、アフリカ2021年5月24日、
      >
      >
   * アジア太平洋2021年6月24日。


## [!DNL Adobe Experience Manager Forms] として  [!DNL Cloud Service] {#forms}

### [!DNL Forms] の新機能  {#what-is-new-forms}

* **コンテキストヘルプ**:アダプティブフォームエディター、テンプレートエディター、テーマエディターのコンテキストヘルプを追加し、作成者がエディターの様々な機能をより深く理解できるようにしました。
* **プロパティブラウザーのエラーメッセージ**:アダプティブFormsのプロパティブラウザーで、各プロパティに関するエラーメッセージを追加しました。これらのメッセージは、フィールドの許可値を理解するのに役立ちます。

### [!DNL Forms]の今後のベータ版機能 {#what-is-new-forms-prerelease}

as a Cloud Serviceの出力：出力サービスを使用すると、XDPテンプレートとXMLデータを組み合わせて様々な形式の印刷ドキュメントを生成できます。 このサービスを使用すると、同期および非同期のバッチモードでドキュメントを生成できます。 出力サービスにより、以下のような機能を備えたアプリケーションを作成することができます。

* テンプレートファイルに XML データを格納することで、最終形式のドキュメントを生成する
* 非インタラクティブPDF印刷ストリームを含む様々な形式で出力フォームを生成します。
* XFA フォームの PDF ファイルから印刷用 PDF を生成する

ベータ版プログラムに新規登録する場合は、 formscsbeta@adobe.comまでお書きください。

### [!DNL Forms] で修正されたバグ  {#forms-bugs-fixed}

* AEM Forms Workflowsの「タスクの割り当て」手順で、アクションボタンのデフォルトのアイコンをCoralアイコンに置き換えると、ワークフローは動作を停止し、例外がログに記録されます。 デフォルトのアイコンが使用されている場合、ワークフローは期待どおりに実行されます。
* レイアウトレイヤーで、列数を変更し、編集レイヤーを開いて、パネル内の一部のコンポーネントをドラッグすると、青い四角いボックスがアダプティブフォームエディターのコンテンツ領域に表示され、エディターが応答しなくなります。
* アダプティブアセットまたは外部アセットのURLの提供に関連するルールエディターオプションのエラーメッセージが長すぎて、使いやすいものではありません。


## Cloud Manager {#cloud-manager}

この節では、AEM as a Cloud Service 2021.5.0 に含まれている Cloud Manager のリリースノートの概要を説明しています。

### リリース日 {#release-date-cm-may}

AEM as a Cloud Service 2021.5.0 Cloud Manager のリリース日は 2021 年 5 月 6 日です。次回のリリースは 2021 年 6 月 3 日に予定されています。

### 新機能 {#what-is-new-may}

* PackageOverlaps 品質ルールは、同じパッケージが複数回デプロイされたケース（同一のデプロイ済みパッケージセット内の複数の埋め込み場所にデプロイされたケース）を検出するようになりました。

* パブリック API のリポジトリーエンドポイントに Git の URL が含まれるようになりました。

* Cloud Manager ユーザーがダウンロードしたデプロイメントログは、失敗と成功シナリオに関する詳細が含まれるようになり、よりわかりやすくなりました。

* コードを Adobe Git にプッシュ中に発生していた断続的なエラーが解決されました。

* Commerce アドオンは、プログラムの編集ワークフロー中に、サンドボックスプログラムに適用できるようになりました。

* プログラムの編集エクスペリエンスが更新されました。

* 環境の詳細ページの「ドメイン名」テーブルには、ページネーション経由で最大 250 個のドメイン名が表示されます。

* プログラムの追加とプログラムの編集のワークフローの「ソリューション」タブには、プログラムで使用できるソリューションが 1 つだけでも、ソリューションが表示されます。

* ビルドでデプロイ済みコンテンツパッケージが生成されなかった場合のビルド手順ログのエラーメッセージが明確でありませんでした。

### バグ修正 {#bug-fixes-cm-may}

* 該当する設定がデプロイされていない場合でも、IP 許可リストの横に緑色の「アクティブ」ステータスが表示される場合がありました。

* パイプライン変数 API は、「削除済み」の変数を削除する代わりに、 **DELETED** ステータスを示すだけでした。

* 「コードの臭い」の品質問題の一部が、信頼性評価に誤って影響していました。

* ワイルドカードドメインはサポートされていないので、UI ではワイルドカードドメインを送信できません。

* UTC の午前 0 時から午前 1 時の間にパイプラインの実行が開始された場合、Cloud Manager で生成されるアーティファクトのバージョンが前日に作成されたバージョンよりも大きくなることが保証されていませんでした。

* サンドボックスプログラムのセットアップ中に、サンプルコードを含んだプロジェクトが正常に作成されると、「Git を管理」がヒーローカードからのリンクとして概要ページに表示されるようになります。

## コンテンツ転送ツール {#content-transfer-tool}

### リリース日 {#release-date-ctt-latest}

コンテンツ転送ツール v1.4.6 のリリース日は 2021 年 5 月 27 日です。

### 新機能 {#what-is-new-ctt-latest}

* ユーザーにJava実行可能ファイルに対する実行権限がない場合、新しいログ文がクイックスタートのエラーログに追加されました。

* 抽出を実行したCTT UIから移行セットを削除すると、その移行セットに関連付けられている`tmp`フォルダーが削除され、領域を節約できます。

### バグ修正 {#bug-fixes-ctt-latest}

* 移行セットを削除する際に、CTT UIに役に立たないエラーメッセージが表示される場合があります。 この問題が修正されました。

* ユーザーマッピングの実行中に、ユーザーがターゲットとホストで同じ電子メールアドレスを持っていても、ユーザー名が異なる場合、取り込み全体が失敗します。 この問題が修正されました。競合するシナリオでは、ユーザー/グループはスキップされ、競合としてログファイルに記録されます。

### リリース日 {#release-date-ctt}

コンテンツ転送ツール v1.4.0 のリリース日は 2021 年 5 月 11 日です。

### 新機能 {#what-is-new-ctt-may}

* このバージョンのコンテンツ転送ツールは、Cloud Service に移行するアセットのテキストレンディションを作成します。取得したアセットでフルテキスト検索をサポートするには、テキストレンディションが必要です。
* ユーザーが作成できるコンテンツ転送ツール移行セットの最大数が 4 から 10 に増えました。

### バグ修正 {#bug-fixes-ctt-may}

* コンテンツ転送ツール UI の自動更新機能に関する複数のバグを修正しました。
* コンテンツ転送ツールで `wipe=true` を指定すると、ターゲットのカウンターインデックスが正しくないという問題がありました。この問題が修正されました。

## Commerce アドオン {#cloud-services-commerce}

### 新機能 {#what-is-new-commerce}

* 製品コンソールのプロパティでの関連コンテンツのページネーションのサポート

### バグ修正 {#bug-fixes-commerce}

* 製品プロパティの「アセット」タブにアセットサムネールが表示されない

* 製品コンソールのプレビューデータをリセットするパンくずリスト
