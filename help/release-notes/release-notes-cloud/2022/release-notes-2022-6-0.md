---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2022.6.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2022.6.0 リリースのリリースノート。'
source-git-commit: c2cd11b806f0cb961fc5ea0d8469f57b04e4aafa
workflow-type: tm+mt
source-wordcount: '641'
ht-degree: 22%

---


# [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート {#release-notes}

以下では、[!DNL Experience Manager] as a Cloud Service の現在（最新）のバージョンのリリースノート全般の概要を説明します。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2020 年、2021 年のバージョンなど）のリリースノートに移動できます。

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

のリリース日 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 現在のリリース (2022.6.0) は 2022 年 6 月 30 日です。

次回のリリース (2022.7.0) は、2022 年 8 月 8 日に予定されています。

## リリースビデオ {#release-video}

2022.6.0 リリースに追加された機能の概要については、 2022 年 6 月リリースの概要ビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/344308/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### の新機能[!DNL Sites] {#sites-features}

* 新しい [ユーザーインターフェイス](/help/sites-cloud/administering/content-fragments/content-fragments-console.md) は、コンテンツ管理者やコンテンツ作成者が効率的に管理（公開、非公開、コピー、移動などのアクションを実行）、検索/フィルタリング、ヘッドレスユースケース向けのコンテンツフラグメントの作成をおこなえるようになりました。

   ![コンテンツフラグメントコンソール](/help/release-notes/assets/cf-ui.png)

* 新しい [目次コンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/tableofcontents.html) は、コアコンポーネントだけでなく、すべてのコンポーネントで機能し、コンテンツページ上で ToCs が自動的にレンダリングされます。 また、Dispatcher はサーバー側でレンダリングされ、完全にキャッシュされるので、読み込みも効率的です。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### の新機能[!DNL Assets] {#assets-features}

Experience Manager AssetsはAdobe Sensei AI 機能を今まで使用 [画像内の色を区別し、取り込み時に自動的にタグとして適用する](/help/assets/color-tag-images.md). これらのタグは、画像の色合いに基づいて、より強化された検索エクスペリエンスを可能にします。 1 ～ 40 の範囲で、画像にタグ付けされるカラーの数を設定し、後でそれらのカラーに基づいて画像を検索できます。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### の新機能[!DNL Forms] {#forms-features}

* **[アダプティブFormsとMicrosoft® Power Automate の統合](/help/forms/forms-microsoft-power-automate-integration.md)**:送信時にMicrosoft® Power Automate Cloud Flow を実行するようにアダプティブフォームを設定できるようになりました。 設定済みのアダプティブフォームは、キャプチャされたデータ、添付ファイルおよびレコードのドキュメントを Power Automate Cloud Flow に送信して処理します。 Microsoft® Power Automate の機能を活用しながら、カスタムのデータキャプチャエクスペリエンスを構築し、取り込んだデータに関するビジネスロジックを構築し、顧客ワークフローを自動化できます。

* **アダプティブフォームを作成するためのウィザード**:ビジネスユーザーに適したウィザードを使用して、アダプティブFormsをすばやくオーサリングできます。 このウィザードでは、事前設定済みのテンプレート、スタイル設定、フィールド、送信オプションを簡単に選択して、アダプティブフォームを作成するためのクイックタブナビゲーションが提供されます。

   ![アダプティブフォームを作成するためのウィザード](/help/release-notes/assets/wizard.png)

## CIF アドオン {#cloud-services-cif}

### 新機能 {#what-is-new-cif}

* より良くシンプルな概要を示す新しい製品コックピットプロパティページ

![製品コクピットのプロパティの概要](/help/assets/CIF/product_cockpit_properties_overview.png)

* I/O Runtime 上のサードパーティコネクタの互換性と堅牢性の向上

* GQL クライアント設定の上書きのサポートを改善しました（例：カスタムキャッシュ動作の設定）

* 複数のコマースエンドポイントが標準でサポートされるようになり、Cloud Manager を介して設定できるようになりました。 詳細は、CIF ブログを参照してください [ここ](https://medium.com/adobetech/use-aem-as-a-cloud-service-with-multiple-adobe-commerce-systems-9295612a9554).


### バグ修正 {#bug-fixes-cif}

* 複数値の製品ピッカーフィールドに、2 番目と追加の製品が無効と表示される

* 製品ピッカーがコンポーネントの背後に隠れている場合があります

## 参照デモアドオン {#cloud-services-demos}

### 新機能 {#what-is-new-demos}

* 新しい WKND コンテンツ&amp;コマーステンプレート。WKND を拡張して、製品カタログ、買い物かご、チェックアウト、myAccount などの E2E ショッピングエクスペリエンスを実現します。 このテンプレートでは、CIF とその CIF コアコンポーネントを使用するので、CIF アドオンもインストールする必要があります。 詳細は、CIF ブログを参照してください [ここ](https://medium.com/adobetech/learn-how-to-create-a-shoppable-experience-with-the-new-wknd-reference-site-and-cif-b3b2c161f67e).

![WKND ショップ](/help/assets/CIF/wknd_shop.png)

![WKNDpdp](/help/assets/CIF/wknd_pdp.png)

## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### 新機能 {#what-is-new-foundation}

* (2022.5.0)5 月のリリースノートで述べたように、レプリケーションエージェント管理画面の「ツリーを追加」オプション **分布** 」タブが削除されました。 代わりに、コンテンツのツリー階層を持つパッケージは、 [公開を管理](/help/operations/replication.md#manage-publication) または [コンテンツツリーを公開](/help/operations/replication.md#manage-publication#publish-content-tree-workflow) ワークフロー。

## Cloud Manager {#cloud-manager}

Cloud Manager の月次リリースの完全なリストは、[こちら](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md)で確認できます。

## 移行ツール {#migration-tools}

移行ツールのリリースの完全なリストは、[こちら](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)で確認できます
