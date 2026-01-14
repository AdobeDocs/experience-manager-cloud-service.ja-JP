---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.6.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.6.0 リリースのリリースノート。'
exl-id: cf2133dc-56cd-4a07-ab11-72e16f015ff5
feature: Release Information
role: Admin
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 77%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の 2022.6.0 リリースノート {#release-notes}

以下の節では、as a Cloud Serviceの 2022.6.0 バージョンの機能リリースノートの概要 [!DNL Experience Manager] 説明します。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2020 年、2021 年のバージョンなど）のリリースノートに移動できます。

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の最新リリース（2022.6.0）のリリース日は 2022年6月30日（PT）です。

次回のリリース（2022.7.0）は 2022年8月8日（PT）に予定されています。

## リリースビデオ {#release-video}

2022.6.0 リリースで追加された機能の概要については、2022年6月リリースの概要ビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/344308/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### の新機能[!DNL Sites] {#sites-features}

* コンテンツ管理者やコンテンツ作成者が、ヘッドレスのユースケースでのコンテンツフラグメントの管理（公開、非公開、コピー、移動など）、検索/フィルタリング、作成を効率的に行うための新しい [ ユーザーインターフェイス ](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console) を使用できるようになりました。

  ![コンテンツフラグメントコンソール](/help/release-notes/assets/cf-ui.png)

* 新しい[目次コンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/tableofcontents.html?lang=ja)は、コアコンポーネントだけでなく、すべてのコンポーネントで機能し、コンテンツページの目次を自動的にレンダリングします。 また、Dispatcher はサーバー側でレンダリングされ、完全にキャッシュされるので、読み込みも効率的です。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### の新機能[!DNL Assets] {#assets-features}

Experience Manager AssetsはAdobe AI 機能を使用し、[ 画像内のカラーを区別して、取り込み時に自動的にタグとして適用する ](/help/assets/color-tag-images.md) ようになりました。 これらのタグを使用すると、画像の色の構成に基づいて、検索エクスペリエンスを強化できます。 画像にタグ付けされるカラーの数を 1 ～ 40 の範囲で設定し、後でそれらのカラーに基づいて画像を検索できます。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### の新機能[!DNL Forms] {#forms-features}

* **[アダプティブフォームと Microsoft® Power Automate の統合](/help/forms/forms-microsoft-power-automate-integration.md)**：送信時に Microsoft® Power Automate クラウドフローを実行するようにアダプティブフォームを設定できるようになりました。 設定済みのアダプティブフォームは、キャプチャされたデータ、添付ファイルおよびレコードのドキュメントを Power Automate クラウドフローに送信して処理します。 Microsoft® Power Automate の機能を活用して、キャプチャされたデータを中心にビジネスロジックを構築し、顧客のワークフローを自動化しながら、カスタムのデータキャプチャエクスペリエンスを構築するのに役立ちます。

* **アダプティブフォームの作成ウィザード**：ビジネスユーザー向けの使いやすいウィザードで、アダプティブフォームをすばやく作成できます。このウィザードではクイックタブナビゲーションを使用して、アダプティブフォームを作成するための事前設定済みのテンプレート、スタイル設定、フィールド、送信オプションを簡単に選択できます。

  ![アダプティブフォームの作成ウィザード](/help/release-notes/assets/wizard.png)

## CIF アドオン {#cloud-services-cif}

### 新機能 {#what-is-new-cif}

* よりわかりやすいシンプルな概要を示す新しい製品コックピットのプロパティページ

![製品コックピットのプロパティの概要](/help/assets/CIF/product_cockpit_properties_overview.png)

* I/O Runtime 上のサードパーティのコネクタの互換性と堅牢性の向上

* GQL クライアント設定の上書きのサポートを改善しました（例：カスタムキャッシュ動作の設定）

* 複数のコマースエンドポイントが標準でサポートされるようになり、Cloud Manager を介して設定できるようになりました。 詳細については、[こちら](https://medium.com/adobetech/use-aem-as-a-cloud-service-with-multiple-adobe-commerce-systems-9295612a9554)の CIF ブログを参照してください。


### バグ修正 {#bug-fixes-cif}

* 複数値の製品ピッカーフィールドに、2 番目の製品と追加の製品が無効と表示されます

* 製品ピッカーがコンポーネントの背後に隠れている場合があります

## 参照デモのアドオン {#cloud-services-demos}

### 新機能 {#what-is-new-demos}

* 新しい WKND コンテンツとコマーステンプレート。WKND を拡張して、製品カタログ、買い物かご、チェックアウト、myAccount などの E2E ショッピングエクスペリエンスを実現します。 このテンプレートでは、CIF とその CIF コアコンポーネントを使用するので、CIF アドオンもインストールする必要があります。 詳細については、[こちら](https://medium.com/adobetech/learn-how-to-create-a-shoppable-experience-with-the-new-wknd-reference-site-and-cif-b3b2c161f67e)の CIF ブログを参照してください。

![WKND ショップ](/help/assets/CIF/wknd_shop.png)

![WKND pdp](/help/assets/CIF/wknd_pdp.png)

## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### 新機能 {#what-is-new-foundation}

* 5 月（2022.5.0）のリリースノートに記載されているように、レプリケーションエージェント管理画面の「**配布**」タブにある「ツリーを追加」オプションが削除されました。 代わりに、コンテンツのツリー階層を持つパッケージは、[公開を管理](/help/operations/replication.md#manage-publication)または[コンテンツツリーを公開](/help/operations/replication.md#manage-publication#publish-content-tree-workflow)ワークフローを使用して複製する必要があります。

## Cloud Manager {#cloud-manager}

Cloud Manager の月次リリースの完全なリストは、[こちら](/help/implementing/cloud-manager/release-notes/current.md)で確認できます。

## 移行ツール {#migration-tools}

移行ツールのリリースの完全なリストは、[こちら](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)で確認できます
