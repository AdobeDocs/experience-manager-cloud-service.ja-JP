---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: f447303d3618eb2e9ea38873c88ed04280670218
workflow-type: tm+mt
source-wordcount: '1685'
ht-degree: 15%

---


# [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート {#release-notes}

以下では、[!DNL Experience Manager] as a Cloud Service の現在（最新）のバージョンのリリースノート全般の概要を説明します。

>[!NOTE]
>ここから、以前のバージョンのリリースノートに移動できます。例えば、2020、2021などの場合、

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager]のCloud Service2021.5.0のリリース日は2021年5月27日です。
次のリリース(2021.6.0)は、2021年6月25日に予定されています。

## ビデオをリリース{#release-video}

追加された機能の概要については、 2021年5月リリースの概要](https://video.tv.adobe.com/v/333602)ビデオをご覧ください。[

## AEM as a Cloud Service の基盤 {#foundation}

### AEM as a Cloud Service基盤の新機能{#what-is-new-foundation}

* [プレリリースチャネル](/help/release-notes/prerelease.md):本番運用開始前の1ヶ月間に予定されている機能のプレビュー

* [APIの廃止](/help/release-notes/deprecated-apis.md):AEM as a Experienceの最新の非推奨APIのリストをご利用いただけます。Cloud Service

* [AEM as aCloud ServiceSDK Build Analyzer Mavenプラグイン](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html):非推奨のJava APIチェックやその他の改善点を含む、Mavenプロジェクトを最新バージョンに更新します。

## [!DNL Adobe Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] の新機能 {#what-is-new-sites}

* 近日中に、新しい[プレビュー層](/help/sites-cloud/authoring/fundamentals/previewing-content.md)でコンテンツを検証して、パブリッシュ層と同じように最終的なエクスペリエンスのルックアンドフィールをシミュレートできます。 これは、AEM Sites Managed Publishionウィザードで有効になり、公開またはプレビューのどちらかの公開先を選択できるようになりました。 プレビュー時のエクスペリエンスは、専用のURLからアクセスできます。 プレビューでの検証後、通常どおりコンテンツをオーサーからパブリッシュに公開できます。 AEM as a Cloud Service環境でのPreview Serviceの有効化は、今後数週間で徐々に展開される予定です。

## [!DNL Adobe Experience Manager Assets] として  [!DNL Cloud Service] {#assets}

### プレリリースチャネルで使用できる新機能{#what-is-new-assets-prerelease}

* メタデータスキーマは、フォルダーのプロパティに直接適用できます。

   ![フォルダープロパティからのメタデータスキーマの追加](/help/assets/assets/metadata-schema-folder-properties.png)

* アセット一括取り込みツールを使用すると、一括取り込み中にメタデータを追加できます。

* ユーザーエクスペリエンスの機能強化では、フォルダー内に存在するアセットの数が表示されます。 1つのフォルダー内のアセットが1000個を超える場合、[!DNL Assets]には1000以上と表示されます。

   ![フォルダー内のアセット数がインターフェイスに表示されます](/help/assets/assets/browse-folder-number-of-assets.png)

### [!DNL Assets] で修正されたバグ {#assets-bugs-fixed}

* 非常に大きなファイルをアップロードすると、[!DNL Experience Manager desktop app]がクラッシュします。 （CQ-4320942）
* フォルダー内で同じコレクションが選択されている場合と、検索結果から同じコレクションが選択されている場合で、ツールバーのオプションは異なります。 （CQ-4321406）

#### [!DNL Dynamic Media] の新機能 {#what-is-new-dm}

* スマートイメージングデバイスのピクセル比(DPR)とネットワーク帯域幅の最適化により、高解像度のディスプレイとネットワーク帯域幅の制約があるデバイスで、最高品質の画像を効率的に配信できます。 [スマートイメージングのFAQ](/help/assets/dynamic-media/imaging-faq.md)を参照してください。

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


* [!DNL Dynamic Media]配信での次世代画像形式AVIFのサポートが導入されました（fmt URL修飾子）。

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

### [!DNL Forms] の新機能 {#what-is-new-forms}

* **コンテキストヘルプ**:アダプティブフォームエディター、テンプレートエディター、テーマエディターのコンテキストヘルプを追加し、作成者がエディターの様々な機能をより深く理解できるようにしました。
* **プロパティブラウザーのエラーメッセージ**:アダプティブFormsのプロパティブラウザーで、各プロパティに関するエラーメッセージを追加しました。これらのメッセージは、フィールドの許可値を理解するのに役立ちます。

### [!DNL Forms] {#what-is-new-forms-prerelease}の今後のベータ版機能

as a Cloud Serviceの出力：出力サービスを使用すると、XDPテンプレートとXMLデータを組み合わせて様々な形式の印刷ドキュメントを生成できます。 このサービスを使用すると、同期および非同期のバッチモードでドキュメントを生成できます。 出力サービスにより、以下のような機能を備えたアプリケーションを作成することができます。

* テンプレートファイルに XML データを格納することで、最終形式のドキュメントを生成する
* 非インタラクティブPDF印刷ストリームを含む様々な形式で出力フォームを生成します。
* XFA フォームの PDF ファイルから印刷用 PDF を生成する

ベータ版プログラムに新規登録する場合は、 formscsbeta@adobe.comまでお書きください。

### [!DNL Forms] で修正されたバグ {#forms-bugs-fixed}

* AEM Forms Workflowsの「タスクの割り当て」手順で、アクションボタンのデフォルトのアイコンをCoralアイコンに置き換えると、ワークフローは動作を停止し、例外がログに記録されます。 デフォルトのアイコンが使用されている場合、ワークフローは期待どおりに実行されます。
* レイアウトレイヤーで、列数を変更し、編集レイヤーを開いて、パネル内の一部のコンポーネントをドラッグすると、青い四角いボックスがアダプティブフォームエディターのコンテンツ領域に表示され、エディターが応答しなくなります。
* アダプティブアセットまたは外部アセットのURLの提供に関連するルールエディターオプションのエラーメッセージが長すぎて、使いやすいものではありません。

## Cloud Manager {#cloud-manager}

この節では、AEM as aCloud Service2021.6.0および2021.5.0のCloud Managerのリリースノートの概要を説明します。

## リリース日 {#release-date-june-cm}

AEM as aCloud Service2021.6.0のCloud Managerのリリース日は2021年6月10日です。
次回のリリースは2021年7月16日に予定されています。

### 新機能 {#what-is-new-junecm}

* プレビューサービスは、すべてのプログラムに周期的にデプロイされます。 お客様は、プログラムがプレビューサービスに対して有効になると、製品内で通知を受けます。 詳しくは、[Preview Serviceへのアクセス](/help/implementing/cloud-manager/manage-environments.md#access-preview-service)を参照してください。

* ビルド手順中にダウンロードされたMavenの依存関係は、パイプライン実行の間でキャッシュされるようになりました。 この機能は、今後数週間のお客様に対して有効になる予定です。

* プログラムの名前は、プログラムを編集ダイアログで編集できるようになりました。

* プロジェクトの作成時と、Gitワークフローを管理するデフォルトのプッシュコマンドで使用されるデフォルトのブランチ名が`main`に変更されました。

* UIでのプログラムの編集エクスペリエンスが更新されました。

* 品質ルール`ImmutableMutableMixCheck`が更新され、`/oak:index`ノードが不変として分類されるようになりました。

* 品質ルール`CQBP-84`と`CQBP-84--dependencies`は、1つのルールに統合されました。 この統合の一環として、依存関係のスキャンにより、AEM Runtimeにデプロイされるサードパーティの依存関係の問題をより正確に特定できます。

* 混乱を避けるために、環境の詳細ページのパブリッシュAEMとパブリッシュDispatcherのセグメント行が統合されました。

   ![](/help/onboarding/release-notes-cloud-manager/assets/aem-dispatcher.png)

* `damAssetLucene`インデックスの構造を検証するための新しいコード品質ルールが追加されました。 詳しくは、[カスタムDAM Asset Lucene Oakインデックス](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-damAssetLucene-sanity-check)を参照してください。

* 環境の詳細ページに、公開サービスとプレビューサービスの複数のドメイン名が表示されるようになりました（該当する場合）。 詳しくは、[環境の詳細](/help/implementing/cloud-manager/manage-environments.md#viewing-environment)を参照してください。

### バグ修正 {#bug-fixes-junecm}

* ルート要素名の後に改行を含むJCRノード定義が正しく解析されなかった問題を修正しました。

* リストリポジトリAPIは、削除されたリポジトリをフィルタリングしません。

* スケジュール手順に無効な値が指定された場合、誤ったエラーメッセージが表示されていました。

* 場合によっては、IP許可リストがデプロイされていない場合でも、その設定の横に緑色の&#x200B;*アクティブ*&#x200B;ステータスが表示されることがあります。

* 一部のプログラム編集シーケンスでは、実稼動パイプラインを作成または編集できなくなる可能性があります。

* 一部のプログラム編集シーケンスでは、**概要**&#x200B;ページに、プログラム設定を再実行する際に誤解を招くようなメッセージが表示される場合があります。


### リリース日 {#release-date-cm-may}

AEM as aCloud Service2021.5.0のCloud Managerのリリース日は2021年5月6日です。

### 新機能 {#what-is-new-may}

* PackageOverlaps 品質ルールは、デプロイされたパッケージセットに同じパッケージが複数回（複数の埋め込み場所に）デプロイされた場合に検出するようになりました。

* Public API のリポジトリーエンドポイントに、Git URL が含まれるようになりました。

* Cloud Managerユーザーがダウンロードしたデプロイメントログは、より洞察に富み、失敗と成功シナリオに関する詳細が含まれるようになります。

* コードをAdobeGitにプッシュ中に発生した断続的なエラーが解決されました。

* Commerceアドオンは、プログラムの編集ワークフロー中にサンドボックスプログラムに適用できるようになりました。

* プログラムの編集エクスペリエンスが新しくなりました。

* 環境の詳細ページの「ドメイン名」テーブルには、ページネーション経由で最大250個のドメイン名が表示されます。

* プログラムの追加とプログラムの編集のワークフローの「ソリューション」タブには、プログラムで使用できるソリューションが1つだけでも、ソリューションが表示されます。

* ビルドでデプロイ済みコンテンツパッケージが生成されなかった場合のビルド手順ログのエラーメッセージが不明でした。

### バグ修正 {#bug-fixes-cm-may}

* 場合によっては、その設定がデプロイされていない場合でも、IP許可リストの横に緑色の「アクティブ」ステータスが表示されることがあります。

* パイプライン変数APIは、「削除済み」の変数を削除する代わりに、ステータス&#x200B;**DELETED**&#x200B;のみをマークします。

* コードの臭いのタイプの品質問題が、誤って信頼性の評価に影響していました。

* ワイルドカードドメインはサポートされていないので、UIではユーザーがワイルドカードドメインを送信できません。

* パイプラインの実行が午前 0 時から午前 1 時（UTC）の間に開始された場合、Cloud Manager で生成されるアーティファクトのバージョンが、前日に作成されたバージョンより大きいことが保証されませんでした。

* サンドボックスプログラムの設定中に、サンプルコードを含むプロジェクトが正常に作成されると、「 Gitを管理」が概要ページのヒーローカードからのリンクとして表示されます。

## コンテンツ転送ツール {#content-transfer-tool}

### リリース日 {#release-date-ctt-latest}

コンテンツ転送ツールv1.4.6のリリース日は2021年5月28日です。

### 新機能 {#what-is-new-ctt-latest}

* ユーザーにJava実行可能ファイルに対する実行権限がない場合、新しいログ文がクイックスタートのエラーログに追加されました。

* 抽出を実行したCTT UIから移行セットを削除すると、その移行セットに関連付けられている`tmp`フォルダーが削除され、領域を節約できます。

### バグ修正 {#bug-fixes-ctt-latest}

* 移行セットを削除する際に、CTT UIに役に立たないエラーメッセージが表示される場合があります。 この問題が修正されました。

* ユーザーマッピングの実行中に、ユーザーがターゲットとホストで同じ電子メールアドレスを持っていても、ユーザー名が異なる場合、取り込み全体が失敗します。 この問題が修正されました。競合するシナリオでは、ユーザー/グループはスキップされ、競合としてログファイルに記録されます。

### リリース日 {#release-date-ctt-may}

コンテンツ転送ツールv1.4.0のリリース日は2021年5月11日です。

### 新機能 {#what-is-new-ctt-may}

* このバージョンのコンテンツ転送ツールでは、Cloud Serviceに移行されるアセットのテキストレンディションを作成します。 取り込んだアセットでフルテキスト検索をサポートするには、テキストレンディションが必要です。
* ユーザーが作成できるコンテンツ転送ツール移行セットの最大数が4から10に増えました。

### バグ修正 {#bug-fixes-ctt-may}

* コンテンツ転送ツールUIの自動更新機能に関する複数のバグ修正がおこなわれました。
* `wipe=true`を含むコンテンツ転送ツールがターゲットのカウンターインデックスに正しくなかった問題を修正しました。 この問題が修正されました。

## Commerce アドオン {#cloud-services-commerce}

### 新機能 {#what-is-new-commerce}

* 製品コンソールのプロパティでの関連コンテンツのページネーションのサポート

### バグ修正 {#bug-fixes-commerce}

* 製品プロパティの「アセット」タブにアセットサムネールが表示されない

* 製品コンソールのプレビューデータをリセットするパンくずリスト
