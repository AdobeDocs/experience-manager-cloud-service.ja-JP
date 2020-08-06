---
title: Cloud Serviceの2020.7.0リリース [!DNL Adobe Experience Manager] のリリースノート。
description: '[!DNLAdobe Experience Manager] 2020.7.0のCloud Serviceリリースノートとして。'
translation-type: tm+mt
source-git-commit: a2b7ca2ab6ab3c95b07de49a43c8b119a792a7ac
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 37%

---


# Release Notes for [!DNL Adobe Experience Manager] as a Cloud Service 2020.7.0 {#release-notes}

Experience Manager as a Cloud Service 2020.7.0 の一般的なリリースノートの概要を次に説明します。

## リリース日 {#release-date}

The release date for [!DNL Experience Manager] as a Cloud Service 2020.7.0 is July 30, 2020.

## Cloud ServiceとしてのAdobe Experience Manager Sites {#cloud-services-sites}

### 新機能 {#what-is-new-sites}

[!DNL Experience Manager] を、およびのCloud Serviceコネクタ [!DNL Adobe Target] に対して次のよう [!DNL Adobe Analytics] に拡張しました。

* 新しいユーザーインターフェイスの実装は、クラシックUIに基づく実装に代わるものです。

* ユーザーインターフェイスダイアログの簡素化。変数マッピングおよび他の設定用のフレームワークの作成はに残り [!DNL Adobe Launch]ます。 「 [Adobe Analyticsの統合](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/sites/integrations/integrating-adobe-analytics.html) 」および「Adobe Targetの [統合」を参照してください](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/sites/integrations/integrating-adobe-target.html)。

* 設定は、Experience Managerリポジトリではなく、に保存され `/conf` るよう `/etc/cloudsettings` になりました。

## Adobe Experience Manager Assets as a Cloud Service {#assets}

### 新機能 {#what-is-new-assets}

* [!DNL Asset Compute Service] は、アセットを処理するための拡張性と拡張性に優れたサービスです。 管理者は、を使用して作成したカスタムExperience Managerを呼び出すようにアプリケーションを設定でき [!DNL Asset Compute Service]ます。 開発者はこのサービスを使用して、複雑な使用例に対応した特殊なカスタムアプリケーションを作成できます。 このWebサービスでは、様々なファイルタイプのサムネールを生成したり、Adobeファイル形式から高品質な画像レンダリングを生成したり、ビデオのエンコード（将来）、メタデータの抽出、インデックス作成の前駆としてのフルテキストの抽出を行ったりできます。 詳しくは、アセットマイクロサービスと処理プロファイルの [使用を参照してください](/help/assets/asset-microservices-configure-and-use.md)。

* Cloud Service [!DNL Dynamic Media] としてのの初期設定 [!DNL Experience Manager] が改善され、より堅牢になりました。 これで、管理者にプロセスの進行状況を提供できます。

* にアセットを公開する方法 [!DNL Dynamic Media] は、アセットマイクロサービスを使用するアセット処理パイプライン全体の不可欠な要素とし、バッチ公開バックエンドを改善することで、簡単になり、より堅牢になります。

* Cloud Serviceの展開と互換性のないワークフローステップは、 [!UICONTROL ワークフローモデル] エディターで警告のマークが付けられるようになりました。 また、Cloud Service環境上で既存のワークフローを実行する場合、互換性のないワークフロー手順はスキップされます。

* Cloud Managerの環境に関連付けられたGitプロジェクトにデプロイされ `/conf/global` たユーザーが作成したワークフローモデルは、に自動的にデプロイされ、Experience Managerで使用で `/var` きます。 顧客が変更した、下位の製品ワークフローモデル `/libs` は、に自動的にはデプロイされません `/var`。

## コアコンポーネント {#core-components}

### 新機能 {#what-is-new-core-components}

Release 2.11.0 of the [AEM Core Components](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/introduction.html) is now available as part of AEM Sites including:

* 新しい [PDF Viewerコンポーネントの紹介](https://aemcomponents.dev/content/core-components-examples/library/page-authoring/pdf-viewer.html)。

* コアコンポーネントのAccelerated Mobile Pages(AMP)サポートが利用できるようになりました。 Googleのモバイル検索結果からサイトに入るときにページトランジションを瞬時に入れるので、より迅速な顧客体験を作成でき、ユーザーエンゲージメントとSEOが向上します。
詳しくは、コアコンポーネントの [AMPサポートを参照してください](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/amp.html) 。

* Adobeクライアントデータレイヤーのバージョン1.0.2との互換性 [](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/data-layer/overview.html)。

* バグの修正とコードの質の改善。

## Cloud Manager {#cloud-manager}

### リリース日 {#release-date-cm}

[!UICONTROL Cloud Manager] バージョン 2020.7.0 のリリース日は 2020 年 7 月 09 日です。

### 新機能 {#what-is-new-cloud-manager}

* 環境ページのデザインが変更されました。

* 環境が休止状態になると、Cloud Manager に個別のステータスが表示されるようになりました。

* 環境ごとの環境変数の数が 200 に増えました。

* Cloud Manager のパイプラインで、カスタマーセットの変数とシークレットがサポートされるようになりました。


   詳細は、「 [パイプライン変数](/help/onboarding/getting-access-to-aem-in-cloud/creating-aem-application-project.md#pipeline-variables)」を参照してください。

### バグ修正 {#bug-fixes-cm}

* 環境が完全に作成される前に、Cloud Manager から開発者コンソールへのリンクが正しくアクティブになっていませんでした。

* Cloud Manager から開発者コンソールへの直接リンクが、サンドボックスプログラムの環境を非休止／休止にするオプションを表示していませんでした。

* 非実稼動パイプライン編集ページの「**キャンセル**」および「**保存**」のオプションが常に表示されていませんでした。

* コード品質プロセスで特定のエラーが発生すると、ログファイルが正しく生成されない場合があります。

* 新しいプログラムを作成する際に、推奨名が既存のプログラム名と重複する場合がありました。

* 一部の大規模なパイプラインステップログは、ユーザーインターフェイスから一貫性のある方法でダウンロードできませんでした。

* 環境名の検証が、1 つずれていました。

* 何も存在しない場合、環境ページにパブリッシュセグメントと Dispatcher セグメントが表示されることがありました。

### 既知の問題 {#known-issues}

* コードカバレッジの計算方法の変更により、Jacoco プラグインの&#x200B;*最小*&#x200B;バージョンは 0.7.5.201505241946（2015 年 5 月リリース）になりました。古いバージョンを明示的に参照するお客様は、コード品質プロセスでエラーメッセージを受け取ります。

## Adobe Experience Manager as a Cloud Service Foundation {#cloud-foundation}

### 新機能 {#what-is-new-foundations}

* [ログはSplunkアカウントに転送でき](/help/implementing/developing/introduction/logging.md#splunk-logs)、組織はSplunkへの投資を活用できます。

* [静的な専用出力IPアドレスは](/help/implementing/developing/introduction/development-guidelines.md#dedicated-egress-ip-address) 、Javaコードでプログラムされたアウトバウンドトラフィックに割り当てることができます。これは、一部の統合で役立つ場合があります。

* AEM AnalyticsクラウドサービスUIをクラシックUIから新しいAEM UIに移行しました。 また、AEMリポジトリ内のAnalyticsクラウドサービスの場所を、他のAEMクラウドサービスと連携す `/etc` るために、 `/conf`に移動しました。

* AEMターゲットクラウドサービスUIをクラシックUIから新しいAEM UIに移動。 また、AEMリポジトリ内のターゲットクラウドサービスの場所を、他のAEMクラウドサービスと連携さ `/etc` せるために、 `/conf`に移動しました。

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### 新機能 {#what-is-new-commerce}

AEMコマースがCloud Serviceで利用できるようになりました。

詳しくは、 [「AEM Commerceを使い始める前にCloud Service](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/commerce/getting-started.html) 」を参照してください。

## Cloud Readiness Analyzer {#cloud-readiness-analyzer}

Cloud Readiness Analyzer リリース v1.0.2 の新機能と更新点については、このセクションを参照してください。

### バグ修正 {#cra-bug-fixes}

* 以前のバージョンの CRA を Adobe Experience Manager（AEM）6.1 で実行できませんでした。管理者グループのユーザーに対する明示的なサポートが追加されました。

   詳しくは、[AEM 6.1 への CRA のインストール](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/moving/cloud-migration/cloud-readiness-analyzer/using-cloud-readiness-analyzer.html#installing-on-aem61)を参照してください。

* 概要レポートに表示される有効期限のタイムスタンプが正しくありませんでした。

* CRA は重複するカスタムコンポーネントを検出していました。

* AEM 6.1 では、完全な検査を完了する前に、コンテンツ検査が終了していました。例外処理が追加されたので、スキップして、検査が完了するまで続行できるようになりました。
