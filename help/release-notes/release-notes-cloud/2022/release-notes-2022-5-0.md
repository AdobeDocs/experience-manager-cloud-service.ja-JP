---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2022.5.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2022.5.0 リリースのリリースノート。'
exl-id: 1b867582-e34c-435b-b8f8-fc71dddcaccb
source-git-commit: 7d09cafc4f8518fee185d3f9efc76c33ec20f9a3
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 75%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の 2022.5.0 リリースノート {#release-notes}

以下の節では、の 2022.5.0 バージョンの機能リリースノートの概要を説明します [!DNL Experience Manager] as a Cloud Service。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2020 年、2021 年のバージョンなど）のリリースノートに移動できます。

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の最新リリース（2022.5.0）のリリース日は 2022年6月9日です。
次回のリリース（2022.6.0）は 2022年6月30日に予定されています。

## リリースビデオ {#release-video}

2022.5.0 リリースで追加された機能の概要については、2022年5月リリースの概要ビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/343321/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] プレリリースチャネルで利用できる新機能 {#prerelease-features-sites}

* GraphQL の様々な機能
* コンテンツフラグメントのヘッドレス使用に最適化された[新しいコンソール](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### の新機能[!DNL Assets] {#assets-features}

* [Dynamic Media スマートイメージング](https://medium.com/adobetech/one-solution-fits-all-smart-imaging-with-aem-dynamic-media-be690b62df9f)が AVIF ファイル形式をサポートするようになりました。Google Core Web Vital（Largest Contentful Paint）をさらに改善し、AVIF は WebP よりも 20%余分なサイズ削減を実現します。合計すると、AVIF は JPEG に比べて最大 41%の平均サイズ削減を実現します（一部の画像では 76% にもなります）。

* [!UICONTROL Experience Manager Assets Brand Portal] では、12 時間ごとに自動ジョブを実行し、AEMに公開されているすべてのBrand Portalアセットを削除するようになりました。 その結果、投稿フォルダー内のアセットを手動で削除して、フォルダーサイズをしきい値の制限以下に保つ必要がなくなりました。 [Experience Manager Assets Brand Portal の新機能](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html?lang=ja)を参照してください。

### [!DNL Assets] プレリリースチャネルで利用できる新機能 {#prerelease-features-assets}

Experience Manager Assets は、Adobe Sensei AI 機能を使用して、[画像内のカラーを識別し、取り込み時に自動的にタグとして適用](/help/assets/color-tag-images.md)するようになりました。これらのタグを使用すると、画像の色の構成に基づいて、検索エクスペリエンスを強化できます。 画像にタグ付けされる色の数を 1 ～ 40 の範囲で設定し、後でそれらの色に基づいて画像を検索できるようにします。


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] プレリリースチャネルで利用できる新機能 {#prerelease-features-forms}

* **アダプティブフォームと Microsoft® Power Automate の統合**：送信時に Microsoft® Power Automate の Cloud Flow を実行するようにアダプティブフォームを設定できるようになりました。設定済みのアダプティブフォームは、キャプチャされたデータ、添付ファイルおよびレコードのドキュメントを Power Automate クラウドフローに送信して処理します。 Microsoft® Power Automate の機能を活用して、キャプチャされたデータを中心にビジネスロジックを構築し、顧客のワークフローを自動化しながら、カスタムのデータキャプチャエクスペリエンスを構築するのに役立ちます。

* **アダプティブフォームを作成するためのウィザード**：ビジネスユーザーにとって使いやすいウィザードを使用して、アダプティブFormsをすばやくオーサリングできます。 このウィザードではクイックタブナビゲーションを使用して、アダプティブフォームを作成するための事前設定済みのテンプレート、スタイル設定、フィールド、送信オプションを簡単に選択できます。

  ![アダプティブフォームの作成ウィザード](/help/release-notes/assets/wizard.png)

## CIF アドオン {#cloud-services-cif}

### 新機能 {#what-is-new-cif}

* 製品コックピットに素早くアクセス：サイトエディターでワンクリックで詳細な製品情報に簡単にアクセス

  ![ウィッシュリストを有効にする](/help/assets/CIF/enable-wishlist.png)

* 追加のマーケティングコマースコンポーネントのサポート：コンポーネントを、買い物かごへの追加と、リストへの追加のコールトゥアクションを表示するように設定できます。

  ![製品コックピットへのサイトエディターショートカット](/help/assets/CIF/sites-editor-shortcut-to-cockpit.png)


## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### 新機能 {#what-is-new-foundation}

* レプリケーションエージェント管理画面の「ツリーを追加」オプション **「分布」タブ**（以前は非推奨と発表）は、2022 年 6 月 20 日以降に削除されました。 代わりに、コンテンツのツリー階層を持つパッケージは、[公開を管理](/help/operations/replication.md#manage-publication)または[コンテンツツリーの公開ワークフロー](/help/operations/replication.md#publish-content-tree-workflow)を使用してレプリケートする必要があります。

* 10 MB を超えるコンテンツパッケージ（バイナリを含まないプロパティを持つノード）を配布するためのレプリケーションエージェント管理画面またはレプリケーション API の使用は、廃止され、2022 年 9 月 12 日以降に適用されます。 代わりに、[公開を管理](/help/operations/replication.md#manage-publication)または[コンテンツツリーの公開ワークフロー](/help/operations/replication.md#publish-content-tree-workflow)を使用して、これらの大規模なコンテンツパッケージをレプリケートする必要があります。 7月に、これらの大規模なコンテンツパッケージをレプリケートしようとすると、レプリケーションエージェント管理画面の&#x200B;**「配布」タブ**&#x200B;に警告メッセージが表示されます。また、レプリケーション API を使用してこれらの大規模なコンテンツパッケージをレプリケートしようとすると、AEM エラーログに警告メッセージが表示されます。9 月には、警告はエラーに置き換えられました。 プロセスを適宜調整します。

### [!DNL Experience Manager] プレリリースチャネルで利用できる新機能 {#prerelease-features-foundation}

* AEM as a Cloud Service が統合シェルと統合され、ユーザーエクスペリエンスが向上し、他のすべての Experience Cloud アプリケーションと統合されました。詳しくは、 [統合シェルでas a Cloud ServiceのAEMを使用](/help/overview/aem-cloud-service-on-unified-shell.md) を参照してください。

## [!DNL Experience Manager] as a [!DNL Cloud Service] 基盤セキュリティ {#foundation-security}

### TLS 1.0、1.1 の廃止

2022 年 6 月 30 日以降、Experience Manageras a Cloud Serviceは、より安全なネットワーク通信とユーザーシステムとのデータ交換を必要とします。 AEM は、TLS（トランスポートレイヤーセキュリティ）1.2 プロトコルのみを使用します。古い TLS バージョン 1.0 および 1.1 は非推奨（廃止予定）となりました。

古いバージョンの TLS 1.0 および 1.1 を引き続き使用する場合、Experience Manager as a Cloud Service のへのアクセス権が失われる可能性があります。

## Cloud Manager {#cloud-manager}

Cloud Manager の月次リリースの完全なリストは、[こちら](/help/implementing/cloud-manager/release-notes/current.md)で確認できます。

## 移行ツール {#migration-tools}

移行ツールのリリースの完全なリストは、[こちら](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)で確認できます
