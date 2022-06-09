---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: a2cdc7c4e9d3dfd52ca76afcf951fa67b279918a
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 22%

---


# [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート  {#release-notes}

以下では、[!DNL Experience Manager] as a Cloud Service の現在（最新）のバージョンのリリースノート全般の概要を説明します。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2020 年、2021 年のバージョンなど）のリリースノートに移動できます。

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

のリリース日 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 現在のリリース (2022.5.0) は 2022 年 6 月 9 日です。
次回のリリース (2022.6.0) は、2022 年 6 月 30 日に予定されています。

## リリースビデオ {#release-video}

2022.5.0 リリースに追加された機能の概要については、 2022 年 5 月リリースの概要ビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/343321/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] プレリリースチャネルで利用できる新機能 {#prerelease-features-sites}

* 様々な GraphQL 機能
* コンテンツフラグメントのヘッドレス使用に最適化された新しいコンソール

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### の新機能[!DNL Assets] {#assets-features}

* [Dynamic Media Smart Imaging](https://medium.com/adobetech/one-solution-fits-all-smart-imaging-with-aem-dynamic-media-be690b62df9f) は AVIF ファイル形式をサポートし、Google Core Web Vital(Largest Contentful Paint) をさらに改善しました。AVIF は WebP に比べて 20%の追加サイズ削減を提供します。 AVIF は、JPEGに比べて最大 41%の平均サイズ削減を実現しています（一部の画像では 76%まで）。

* [!UICONTROL Experience Manager Assets Brand Portal] では、12 時間ごとに自動ジョブを実行し、AEMに公開されているすべてのBrand Portalアセットを削除するようになりました。 その結果、投稿フォルダー内のアセットを手動で削除して、フォルダーサイズをしきい値の制限以下に保つ必要がなくなりました。 [Experience Manager Assets Brand Portal の新機能](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html?lang=ja)を参照してください。

### [!DNL Assets] プレリリースチャネルで利用できる新機能 {#prerelease-features-assets}

Experience Manager AssetsはAdobe Sensei AI 機能を今まで使用 [画像内の色を区別し、取り込み時に自動的にタグとして適用する](../../assets/color-tag-images.md). これらのタグは、画像の色合いに基づいて、より強化された検索エクスペリエンスを可能にします。 1 ～ 40 の範囲で、画像にタグ付けされるカラーの数を設定し、後でそれらのカラーに基づいて画像を検索できます。


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] プレリリースチャネルで利用できる新機能 {#prerelease-features-forms}

* **アダプティブFormsとMicrosoft® Power Automate の統合**:送信時にMicrosoft® Power Automate Cloud Flow を実行するようにアダプティブフォームを設定できるようになりました。 設定済みのアダプティブフォームは、キャプチャされたデータ、添付ファイルおよびレコードのドキュメントを Power Automate Cloud Flow に送信して処理します。 Microsoft® Power Automate の機能を活用しながら、カスタムのデータキャプチャエクスペリエンスを構築し、取り込んだデータに関するビジネスロジックを構築し、顧客ワークフローを自動化できます。

* **アダプティブフォームを作成するためのウィザード**:ビジネスユーザーに適したウィザードを使用して、アダプティブFormsをすばやくオーサリングできます。 このウィザードでは、事前設定済みのテンプレート、スタイル設定、フィールド、送信オプションを簡単に選択して、アダプティブフォームを作成するためのクイックタブナビゲーションが提供されます。

   ![アダプティブフォームを作成するためのウィザード](/help/release-notes/assets/wizard.png)

## CIF アドオン {#cloud-services-cif}

### 新機能 {#what-is-new-cif}

* より良くシンプルな概要を示す新しい製品コックピットプロパティページ

![製品コクピットのプロパティの概要](/help/assets/CIF/product_cockpit_properties_overview.png)

* I/O Runtime 上のサードパーティコネクタの互換性と堅牢性の向上

* GQL クライアント設定の上書きのサポートを改善しました（例：カスタムキャッシュ動作の設定）

### バグ修正 {#bug-fixes-cif}

* 複数値の製品ピッカーフィールドに、2 番目と追加の製品が無効と表示される

* 製品ピッカーがコンポーネントの背後に隠れている場合があります

## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### 新機能 {#what-is-new-foundation}

* レプリケーションエージェント管理画面の「ツリーを追加」オプション **「分布」タブ**&#x200B;は、以前に非推奨と発表されていましたが、2022 年 6 月 20 日以降に削除されます。 代わりに、コンテンツのツリー階層を持つパッケージは、 [公開を管理](/help/operations/replication.md#manage-publication) または [コンテンツツリーの公開ワークフロー](/help/operations/replication.md#publish-content-tree-workflow).

* 10 MB（バイナリを含まないプロパティを持つノード）を超えるコンテンツパッケージを配布するためのレプリケーションエージェント管理画面またはレプリケーション API の使用は非推奨となり、2022 年 9 月 12 日以降に適用されます。 代わりに、 [公開を管理](/help/operations/replication.md#manage-publication) または [コンテンツツリーの公開ワークフロー](/help/operations/replication.md#publish-content-tree-workflow) これらの大規模なコンテンツパッケージのレプリケートに使用する必要があります。 7 月に、レプリケーションエージェントの管理画面の **「分布」タブ** レプリケーション API を使用してこれらの大きなコンテンツパッケージをレプリケートする場合は常に、これらの大きなコンテンツパッケージとAEMエラーログにもレプリケートします。 9 月には、警告はエラーに置き換えられます。 プロセスを適宜調整してください。

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation セキュリティ {#foundation-security}

### TLS 1.0、1.1 の廃止

2022 年 6 月 30 日以降、Experience Manageras a Cloud Serviceは、より安全なネットワーク通信とユーザーシステムとのデータ交換を必要とします。 AEMは、TLS(Transport Layer Security)1.2 プロトコルのみを使用します。 古いバージョンの TLS 1.0 および 1.1 は非推奨となります。

古いバージョンの TLS を 1.0、1.1 として引き続き使用する場合、as a Cloud ServiceのExperience Managerへのアクセス権が失われる可能性があります。

## Cloud Manager {#cloud-manager}

Cloud Manager の毎月のリリースの完全なリストを確認できます [ここ](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md).

## 移行ツール {#migration-tools}

移行ツールのリリースの完全なリストはこちらで確認できます [ここ](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
