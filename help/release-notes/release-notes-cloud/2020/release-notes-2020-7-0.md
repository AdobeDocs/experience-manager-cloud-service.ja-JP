---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2020.7.0 リリースのリリースノート。'
description: '[!DNL Adobe Experience Manager] as a Cloud Service 2020.7.0 のリリースノート.'
exl-id: 75d354a3-6987-4de0-aec8-24043461c516
feature: Release Information
role: Admin
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 93%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2020.7.0 のリリースノート  {#release-notes}

Experience Manager as a Cloud Service 2020.7.0 の一般的なリリースノートの概要を次に説明します。

## リリース日 {#release-date}

[!DNL Experience Manager] as a Cloud Service 2020.7.0 のリリース日は 2020年7月30日です。

## Adobe Experience Manager Sites as a Cloud Service {#cloud-services-sites}

### 新機能 {#what-is-new-sites}

[!DNL Adobe Target] および [!DNL Adobe Analytics] 用の [!DNL Experience Manager] as a Cloud Service コネクタは以下のように強化されています。

* 新しいユーザーインターフェイスの実装は、クラシック UI に基づく実装に代わるものです。

* ユーザーインターフェイスダイアログの簡素化。変数マッピングおよび他の設定用のフレームワークの作成は [!DNL Adobe Launch] に残ります。[Adobe Analytics の統合](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/integrations/integrating-adobe-analytics.html?lang=ja)および [Adobe Target の統合](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/integrations/integrating-adobe-target.html?lang=ja)を参照してください。

* 設定は、Experience Manager リポジトリの `/etc/cloudsettings` ではなく、`/conf` に保存されるようになりました。

## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

### [!DNL Assets] の新機能 {#what-is-new-assets}

* [!DNL Asset Compute Service] は、アセットを処理するための拡張性に優れたサービスです。管理者は、[!DNL Asset Compute Service] を使用して作成したカスタムアプリケーションを呼び出すように [!DNL Experience Manager] を設定できます。デベロッパーはこのサービスを使用して、複雑な使用例に対応する特殊なカスタムアプリケーションを作成できます。この web サービスでは、様々なファイルタイプのサムネールを生成したり、アドビファイル形式から高品質な画像レンダリングを生成したり、ビデオのエンコード（将来）、メタデータの抽出、インデックス作成の前段階としてのフルテキストの抽出を行ったり、利用可能なすべての [!DNL AI] サービスでアセットを実行できます。詳しくは、[アセットマイクロサービスと処理プロファイルの使用](/help/assets/asset-microservices-configure-and-use.md)を参照してください。

* [!DNL Experience Manager] as a Cloud Service の [!DNL Dynamic Media] の初期設定が改善され、より堅牢になりました。管理者にプロセスの進行状況が提供されます。

* [!DNL Dynamic Media] へのアセットの発行は、アセットマイクロサービスを使用するアセット処理パイプライン全体で不可欠な要素とし、バッチ発行バックエンドを改善することで、簡単になり、より堅牢になっています。

* [!UICONTROL ワークフローモデル]エディターで、Cloud Service の展開と互換性のないワークフローステップに警告のマークがつくようになりました。また、Cloud Service環境で既存のワークフローを実行する場合、互換性のないワークフローステップはスキップされます。

* [!DNL Cloud Manager] の環境に関連付けられた Git プロジェクトの `/conf/global` にデプロイされた、顧客が作成したワークフローモデルは、`/var` に自動的にデプロイされ、[!DNL Experience Manager] で使用できます。顧客が変更した、`/libs` にある製品ワークフローモデルは、自動的には `/var` にデプロイされません。

### バグ修正 {#assets-bugs-fixed}

* コレクションに含まれるアセットに対して、アセットの移動ウィザードが期待どおりに読み込まれません。（CQ-4296756）
* `dam:size` 値および `dam:sha1` 値は、XMP の書き戻しから除外されます。（CQ-4237355）
* アセットを一括して非公開にすると、要求 URI が長すぎることを示すエラーが [!DNL Brand Portal] によって生成されます。（CQ-4299474）

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### 新機能 {#what-is-new-commerce}

AEM Commerce が Cloud Service で利用できるようになりました。

詳しくは [AEM Commerce as a Cloud Serviceの概要 ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/commerce/getting-started.html?lang=ja) を参照してください。

## コアコンポーネント {#core-components}

### 新機能 {#what-is-new-core-components}

[コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja)のリリース 2.11.0 は、AEM Sites の一部として使用できるようになり、以下を含みます。

* 新しい [PDF ビューアコンポーネント](https://www.aemcomponents.dev/content/core-components-examples/library/core-content/pdf-viewer.html)の導入。

* コアコンポーネントの Accelerated Mobile Pages（AMP）
サポートが利用できるようになりました。Google のモバイル検索結果からサイトに入るときにページトランジションを瞬時に入れるので、より迅速な顧客体験を作成でき、ユーザーエンゲージメントと SEO が向上します。
詳しくは、[ コアコンポーネントの AMP サポート ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/amp.html?lang=ja) を参照してください。

* [アドビクライアントデータレイヤー](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html?lang=ja)のバージョン 1.0.2 との互換性。

* バグの修正とコードの質の改善。

## Cloud Manager {#cloud-manager}

### リリース日 {#release-date-cm}

[!UICONTROL Cloud Manager] バージョン 2020.7.0 のリリース日は 2020年7月9日（PT）です。

### 新機能 {#what-is-new-cloud-manager}

* 環境ページのデザインが変更されました。

* 環境が休止状態になると、Cloud Manager に個別のステータスが表示されるようになりました。

* 環境ごとの環境変数の数が 200 に増えました。

* Cloud Manager のパイプラインで、顧客が設定した変数とシークレットがサポートされるようになりました。

  詳しくは、パイプライン変数を参照してください。

* 認証にバインドされたプライベート Maven リポジトリがサポートされるようになりました。

* Cloud Manager ビルドコンテナで、Java 8 と Java 11 の両方がサポートされるようになりました。詳しくは、Java 11 サポートの使用を参照してください。

### バグの修正 {#bug-fixes-cm}

* 環境が完全に作成される前に、Cloud Manager から開発者コンソールへのリンクが正しくアクティブになっていませんでした。

* Cloud Manager から開発者コンソールへの直接リンクが、サンドボックスプログラムの環境を非休止／休止にするオプションを表示していませんでした。

* 非実稼動パイプライン編集ページの「**キャンセル**」および「**保存**」のオプションが常に表示されていませんでした。

* コード品質プロセスで特定のエラーが発生すると、ログファイルが正しく生成されない場合があります。

* プログラムを作成する際に、推奨名が既存のプログラム名と重複する場合がありました。

* 一部の大規模なパイプラインステップログは、ユーザーインターフェイスから一貫性のある方法でダウンロードできませんでした。

* 環境名の検証が、1 つずれていました。

* 何も存在しない場合、環境ページにパブリッシュセグメントと Dispatcher セグメントが表示されることがありました。

### 既知の問題 {#known-issues}

* コードカバレッジの計算方法が変更されたことで、Jacoco プラグインの&#x200B;*最小*&#x200B;バージョンが 0.7.5.201505241946（2015 年 5 月リリース）になりました。古いバージョンを明示的に参照している場合は、コード品質プロセスでエラーメッセージが表示されます。

## Adobe Experience Manager as a Cloud Service の基盤 {#cloud-foundation}

### 新機能 {#what-is-new-foundations}

* [ ログは Splunk アカウントに転送できます ](/help/implementing/developing/introduction/logging.md#splunk-logs) これにより、組織は Splunk への投資を使用できます。

* [静的な専用 egress IP アドレス](/help/implementing/developing/introduction/development-guidelines.md#dedicated-egress-ip-address)は、Java コードでプログラムされたアウトバウンドトラフィックに割り当てることができます。これは、一部の統合で役立つ場合があります。

* AEM Analytics Cloud Service UI をクラシック UI から新しい AEM UI に移行しました。また、AEM リポジトリ内の Analytics クラウドサービスの場所を、他の AEM クラウドサービスと連携するために、`/etc` から `/conf` に移動しました。

* AEM Target Cloud Service UI をクラシック UI から新しい AEM UI に移行しました。また、AEM リポジトリ内の Target Cloud Service の場所を、他の AEM クラウドサービスと連携させるために、`/etc` から `/conf` に移動しました。

## Cloud Readiness Analyzer {#cloud-readiness-analyzer}

Cloud Readiness Analyzer リリース v1.0.2 の新機能と更新点については、このセクションを参照してください。

### バグの修正 {#cra-bug-fixes}

* 以前のバージョンの CRA を Adobe Experience Manager（AEM）6.1 で実行できませんでした。管理者グループのユーザーに対する明示的なサポートが追加されました。

  詳しくは、[AEM 6.1 への CRA のインストール ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/cloud-readiness-analyzer/using-cloud-readiness-analyzer.html?lang=ja#installing-on-aem61) を参照してください。

* 概要レポートに表示される有効期限のタイムスタンプが正しくありませんでした。

* CRA は重複するカスタムコンポーネントを検出していました。

* AEM 6.1 では、完全な検査を完了する前に、コンテンツ検査が終了していました。例外処理が追加されたので、スキップして、検査が完了するまで続行できるようになりました。
