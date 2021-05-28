---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: dc66eca7b789cf3be1aeae3d63935362ab6f918a
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 14%

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


## Cloud Manager {#cloud-manager}

この節では、AEM as a Cloud Service 2021.5.0 に含まれている Cloud Manager のリリースノートの概要を説明しています。

### リリース日 {#release-date-cm-may}

AEM as aCloud Service2021.5.0のCloud Managerのリリース日は2021年5月6日です。
次回のリリースは2021年6月11日に予定されています。

### 新機能 {#what-is-new-may}

* PackageOverlaps品質ルールで、同じパッケージが複数回（同じデプロイ済みパッケージセット内の複数の埋め込み場所など）デプロイされた場合を検出するようになりました。

* パブリックAPIのリポジトリエンドポイントにGitのURLが含まれるようになりました。

* Cloud Managerユーザーがダウンロードしたデプロイメントログは、より洞察に富み、失敗と成功シナリオに関する詳細が含まれるようになります。

* コードをAdobeGitにプッシュ中に発生した断続的なエラーが解決されました。

* Commerceアドオンは、プログラムの編集ワークフロー中にサンドボックスプログラムに適用できるようになりました。

* プログラムの編集エクスペリエンスが更新されました。

* 環境の詳細ページの「ドメイン名」テーブルには、ページネーション経由で最大250個のドメイン名が表示されます。

* プログラムの追加とプログラムの編集のワークフローの「ソリューション」タブには、プログラムで使用できるソリューションが1つだけでも、ソリューションが表示されます。

* ビルドでデプロイ済みコンテンツパッケージが生成されなかった場合のビルド手順ログのエラーメッセージが不明でした。

### バグ修正 {#bug-fixes-cm-may}

* 場合によっては、その設定がデプロイされていない場合でも、IP許可リストの横に緑色の「アクティブ」ステータスが表示されることがあります。

* パイプライン変数APIは、「削除済み」の変数を削除する代わりに、ステータス&#x200B;**DELETED**&#x200B;のみをマークします。

* コードスメルタイプの品質の問題の一部が、信頼性評価に誤って影響していました。

* ワイルドカードドメインはサポートされていないので、UIではユーザーがワイルドカードドメインを送信できません。

* UTCの午前0時から午前1時の間にパイプラインの実行が開始された場合、Cloud Managerで生成されるアーティファクトのバージョンが前日に作成されたバージョンより大きくなることは保証されていませんでした。

* サンドボックスプログラムの設定中に、サンプルコードを含むプロジェクトが正常に作成されると、「 Gitを管理」が概要ページのヒーローカードからのリンクとして表示されます。

## コンテンツ転送ツール {#content-transfer-tool}

### リリース日 {#release-date-ctt}

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
