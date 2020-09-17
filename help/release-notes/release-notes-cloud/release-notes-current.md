---
title: Cloud Serviceの2020.9.0リリース [!DNL Adobe Experience Manager] のリリースノート。
description: '[!DNLAdobe Experience Manager] 2020.9.0のCloud Serviceリリースノートとして。'
translation-type: tm+mt
source-git-commit: 529a538948f537fde8b2c50fb1f3acc942a7cb64
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 19%

---


# Release Notes for [!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0 {#release-notes}

Experience Manager as a Cloud Service 2020.9.0 の一般的なリリースノートの概要を次に説明します。

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### What is new in [!DNL Sites] {#what-is-new-sites}

* シングルページアプリケーション(SPA)エディターのJavaScript SDK [がオープンソースになりました。](/help/implementing/developing/spa/reference-materials.md)

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### 新機能 {#what-is-new-commerce}

* CIFコアコンポーネントv1.3.0をリリースしました。詳しくは、「 [CIFコアコンポーネント](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.3.0) 」を参照してください。

* 商品やカテゴリテンプレート用の商品/カテゴリに関するプレビュー機能が利用できるようになりました。 これにより、AEMのビジネスユーザーやマーケターは、商品やカテゴリのテンプレートに実際のデータを表示できます。

* 製品およびカテゴリに追加されたプロパティページ。これにより、ビジネスユーザーは、製品のSKU/カテゴリIDに関連付けられた表示の詳細を確認できます。

* 製品コンソールに追加され、製品/カテゴリを名前または価格属性で並べ替えられるようになりました。

* 製品コンソールに追加された製品検索機能。

### バグ修正 {#bug-fixes-commerce}

* Commerce Cloud構成は継承を尊重しませんでした。 この問題は、設定に値が継承されるように修正されました。

## Cloud Manager {#cloud-manager}

### リリース日 {#release-date-cm}

[!UICONTROL Cloud Manager] バージョン 2020.9.0 のリリース日は 2020 年 9 月 03 日です。

### 新機能 {#what-is-new-cloud-manager}

* 「コンテンツ監査」は、「エクスペリエンス監査」という名称に変更されました。
* ビルドプロセスは、3つの Maven コマンドに分けられています。
* Gitリポジトリを複製できない場合は、最大3回再試行されます。

### バグ修正 {#bug-fixes-cm}

* 「コンテンツ監査」タブで、パブリッシュドメインではなく作成者ドメインを使用してベースURLが正しく表示されませんでした。

## Cloud Readiness Analyzer {#cloud-readiness-analyzer}

Cloud Readiness Analyzer リリース v1.1.0 の新機能と更新点については、このセクションを参照してください。

### 新機能 {#what-is-new-cra}

* Cloud Readiness Analyzer(CRA)には、開始状態コンソールがあり、ユーザーがクリックしてCRAを実行するための明示的な「レポートの生成」ボタンを表示します。

* CRA UIの実行中は進行状況が表示されます。 分析中の項目と実行中に見つかった結果が表示されます。

* CRAレポートには、検索のタイプと重要度レベル別に整理された表形式で、結果の概要と数が表示されます。 その検索結果の数をクリックすると、自動的にレポート内のその検索結果の場所にスクロールします。

### バグ修正 {#cra-bug-fixes}

* 場合によっては、更新を強制した後にCRAレポートが更新されないことがありました。 このバージョンは修正されました。

