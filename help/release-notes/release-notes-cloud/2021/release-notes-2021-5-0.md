---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.5.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.5.0 リリースのリリースノート。'
exl-id: 3f9d7339-7e37-4702-821e-f2b03cd7e224
feature: Release Information
role: Admin
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '1355'
ht-degree: 92%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート  {#release-notes}

以下では、[!DNL Experience Manager] as a Cloud Service の現在（最新）のバージョンのリリースノート全般の概要を説明します。

>[!NOTE]
>ここから、以前のバージョン（例えば、2020 年、2021 年のバージョンなど）のリリースノートに移動できます。

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a Cloud Service 2021.5.0 のリリース日は 2021 年 5 月 27 日です。次回のリリース（2021.6.0）は、2021 年 6 月 28 日に予定されています。

## AEM as a Cloud Service の基盤 {#foundation}

### AEM as a Cloud Service 基盤の新機能 {#what-is-new-foundation}

* [プレリリースチャネル](/help/release-notes/prerelease.md)：本番運用開始前の 1 か月間に予定されている機能のプレビュー

* [非推奨 API](/help/release-notes/deprecated-removed-features.md)：AEM as a Cloud Service の最新の非推奨 API リストが公開されています。

* [AEM as a Cloud Service SDK Build Analyzer Maven プラグイン](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=ja)：非推奨の Java API のチェックやその他の改善点を含む最新バージョンに、Maven プロジェクトを更新します。

## [!DNL Adobe Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] の新機能  {#what-is-new-sites}

* 近日中に、新しい[プレビュー層](/help/sites-cloud/authoring/sites-console/previewing-content.md)でコンテンツを検証し、最終的なエクスペリエンスのルックアンドフィールをパブリッシュ層と同じようにシミュレートできるようになります。これは、AEM Sites Managed Publishion ウィザードで、公開先を公開またはプレビューから選択できるようになったことによるものです。プレビュー時のエクスペリエンスには、専用の URL からアクセスできます。プレビューで検証した後は、通常どおり作成者がコンテンツを公開できます。AEM as a Cloud Service 環境でのプレビューサービスの有効化は、今後数週間で徐々に展開される予定です。

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] の新機能  {#what-is-new-assets}

* リンク共有機能を使用して、共有アセットをダウンロードできます。このダウンロードには、非同期サービスが採用されており、大容量のダウンロードであっても、高速で中断のないダウンロードが可能になっています。 詳しくは、「[アセットのダウンロード](/help/assets/download-assets-from-aem.md#link-share-download)」を参照してください。

  ![インボックスをダウンロード](/help/assets/assets/download-inbox.png)

### プレリリースチャネルで使用できる新機能 {#what-is-new-assets-prerelease}

* メタデータスキーマは、フォルダーのプロパティに直接適用できます。

  ![フォルダープロパティからメタデータスキーマを追加する](/help/assets/assets/metadata-schema-folder-properties.png)

* アセット一括取得ツールを使用すると、一括取得中にメタデータを追加できます。

* ユーザーエクスペリエンスが改善され、フォルダー内に存在するアセットの数が表示されます。1 つのフォルダー内のアセットが 1000 個を超える場合、[!DNL Assets] には「1000+」と表示されます。

  ![フォルダー内のアセット数がインターフェイスに表示されます](/help/assets/assets/browse-folder-number-of-assets.png)

### [!DNL Assets] で修正されたバグ  {#assets-bugs-fixed}

* 非常に大きなファイルをアップロードすると、[!DNL Experience Manager desktop app] がクラッシュします。（CQ-4320942）
* 同じコレクションがフォルダー内で選択されている場合と、検索結果から選択されている場合では、ツールバーのオプションは異なります。（CQ-4321406）

#### Dynamic Media の新機能 {#what-is-new-dm}

* スマートイメージング DPR（Device Pixel Ratio）とネットワーク帯域幅の最適化により、高解像度のディスプレイとネットワーク帯域幅の制約があるデバイスで、最高品質の画像を効率的に配信できます。詳しくは、[ スマートイメージングに関する FAQ](/help/assets/dynamic-media/imaging-faq.md) および [ 次世代の画像形式 WebP および AVIF による画像の最適化 ](https://medium.com/adobetech/image-optimisation-with-next-gen-image-formats-webp-and-avif-248c75afacc4) を参照してください。
* Dynamic Media 配信で、次世代画像形式 AVIF のサポートが導入されました（fmt URL 修飾子）。

## [!DNL Adobe Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] の新機能 {#what-is-new-forms}

* **コンテキストヘルプ**：アダプティブフォームエディター、テンプレートエディター、テーマエディターのコンテキストヘルプが追加され、作成者がエディターの様々な機能をより深く理解できるようになりました。
* **プロパティブラウザーのエラーメッセージ**：アダプティブフォームのプロパティブラウザーに、各プロパティに関するエラーメッセージを追加しました。これらのメッセージは、フィールドの許可値を理解するのに役立ちます。

### [!DNL Forms] の今後のベータ版機能 {#what-is-new-forms-prerelease}

Output as a Cloud service：出力サービスを使用すると、XDP テンプレートと XML データを組み合わせて、様々な形式の印刷用ドキュメントを生成できます。このサービスを使用すると、同期および非同期の一括モードでドキュメントを生成できます。出力サービスにより、以下のような機能を備えたアプリケーションを作成することができます。

* テンプレートファイルに XML データを格納することで、最終形式のドキュメントを生成する。
* 非インタラクティブ PDF 印刷ストリームを含む様々な形式で出力フォームを生成します。
* XFA フォームの PDF ファイルから印刷用 PDF を生成する。

ベータ版プログラムに新規登録するには、formscsbeta@adobe.com 宛てにメールを送信します。

### [!DNL Forms] で修正されたバグ  {#forms-bugs-fixed}

* AEM Forms ワークフローの「タスクの割り当て」手順で、アクションボタンのデフォルトのアイコンを Coral アイコンに置き換えると、ワークフローは動作を停止し、例外がログに記録されます。デフォルトのアイコンが使用されている場合、ワークフローは期待どおりに実行されます。
* レイアウトレイヤーで、列数を変更し、編集レイヤーを開いてパネル内の一部のコンポーネントをドラッグすると、青い四角いボックスがアダプティブフォームエディターのコンテンツ領域に表示され、エディターが応答しなくなります。
* アダプティブアセットまたは外部アセットの URL の提供に関連するルールエディターオプションのエラーメッセージが長すぎて、使いやすいものではありません。


## Cloud Manager {#cloud-manager}

この節では、AEM as a Cloud Service 2021.5.0 に含まれている Cloud Manager のリリースノートの概要を説明しています。

### リリース日 {#release-date-cm-may}

AEM as a Cloud Service 2021.5.0 Cloud Manager のリリース日は 2021 年 5 月 6 日です。次回のリリースは 2021 年 6 月 3 日に予定されています。

### 新機能 {#what-is-new-may}

* PackageOverlaps 品質ルールは、デプロイされたパッケージセットに同じパッケージが複数回（複数の埋め込み場所に）デプロイされた場合に検出するようになりました。

* パブリック API のリポジトリエンドポイントに Git の URL が含まれるようになりました。

* Cloud Manager ユーザーがダウンロードしたデプロイメントログは、よりインサイトに富み、失敗と成功シナリオに関する詳細が含まれています。

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

* ユーザーに Java 実行可能ファイルの実行権限がない場合、新しいログ文がクイックスタートのエラーログに追加されました。

* 抽出を実行した CTT ユーザーインターフェイスから移行セットを削除すると、その移行セットに関連付けられている `tmp` フォルダーが削除され、領域を節約できます。

### バグ修正 {#bug-fixes-ctt-latest}

* 移行セットを削除する際に、CTT UI に参考にならないエラーメッセージが表示されることがありました。この問題が修正されました。

* ユーザーマッピングの実行中に、ユーザーがターゲットとホストで同じメールアドレスを持っていても、ユーザー名が異なる場合、取り込み全体が失敗することがありました。この問題が修正されました。このような競合が発生した場合、そのユーザー／グループはスキップされ、ログファイルに競合として記録されます。

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

* パンくずリストが製品コンソールのプレビューデータをリセットする
