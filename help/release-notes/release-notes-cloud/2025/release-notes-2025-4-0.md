---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2025.4.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2025.4.0 リリースのリリースノート。'
feature: Release Information
role: Admin
exl-id: 48e09824-5c67-49d8-8896-358d679649fc
source-git-commit: c8391e09b7e2888423187f48360423c52b18fe0a
workflow-type: tm+mt
source-wordcount: '1828'
ht-degree: 91%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の 2025.4.0 リリースノート {#release-notes}

以下の節では、[!DNL Experience Manager] as a Cloud Service の 2025.4.0 バージョンの機能リリースノートの概要について説明します。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2023年、2024年）のリリースノートに移動できます。
>
>[!DNL Experience Manager] as a Cloud Service の今後の機能のアクティベーションについての詳細は、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)をご覧ください。

>[!NOTE]
>
>Experience Cloud リリースノートの更新に関するメール通知を毎月受信するには、[アドビ製品アップデートの優先通知](https://www.adobe.com/subscription/priority-product-update.html)を購読してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の最新の機能リリース（2025.4.0）のリリース日は、2025年4月24日（PT）です。次回の機能リリース（2025.5.0）は 2025年6月5日（PT）に予定されています。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

## リリースビデオ {#release-video}

2025.4.0 リリースで追加された機能の概要については、2025年4月リリースの概要ビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3464003?quality=12&captions=jpn)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Experience Manager Sites の新機能 {#enhancements-sites}

**新しいコンテンツフラグメントモデル管理 UI**

AEM コンテンツフラグメントを操作する際の新しいクライアントサイドユーザーインターフェイスのリストがさらに完成し、コンテンツフラグメントモデル用の新しい管理 UI が使用できるようになりました。新しい UI には、フィルターを使用してモデルを検索でき、モデルタグと、存在するコンテンツフラグメントを特定のモデルに基づいて表示する、クリーンでモダンなリスト表示が用意されています。ドキュメントについて詳しくは、[こちら](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md)を参照してください。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Dynamic Media（Scene7） {#dynamic-media-scene7}

**Dynamic Media （Scene7）はセキュリティの強化環境ではサポートされない**

AEM as a Cloud Service 上の Dynamic Media （Scene7）は HIPAA に対応していないので、セキュリティの強化が有効になっている AEM 環境では使用できません。

2025年4月の AEM as a Cloud Service リリース以降、技術的な制限により、セキュリティの強化環境では Dynamic Media（Scene7）を設定できなくなります。その結果、これらの環境では、**ツール**／**Cloud Services** の **Dynamic Media 設定**&#x200B;カードが表示されなくなります。

さらに、AEM 6.5 を使用しているお客様は、Dynamic Media（Scene7）スタックが HIPAA に対応していないことに注意する必要があります。

### Dynamic Media Classic {#dynamic-media-classic}

**レポート**

Dynamic Media Classic レポートダッシュボードの「帯域幅」タブは、2025年4月以降サポートされなくなりました。

[帯域幅とストレージ、レポートのタイプ](https://experienceleague.adobe.com/ja/docs/dynamic-media-classic/using/setup/administration-setup#types-of-reports)を参照してください。

## アセットビューの新機能 {#new-features-assets-view}

**アセットの関連付け**

アセットビューでは、簡素化されたアセットの詳細パネルでアセットの関係付けの表示と編集がサポートされるようになりました。ソースや派生などの関係をコンテンツに簡単に追加できるので、ユーザーは関連するヒーローコンテンツをより効果的に見つけることができます。

![アセットの関連付けの例](/help/assets/assets/asset-relations-example.png)

**アセットのバージョンを比較**

アセットビューを使用して、アセットの任意のバージョンをすばやく選択し、最新バージョンと比較できるようになりました。

![アセットのバージョンを比較](/help/assets/assets/version-compare2.png)


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### プレリリース機能

* [ アダプティブFormsおよびフォームフラグメント用のユニバーサルエディター ](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)：ユニバーサルエディターでは、アダプティブFormsと再利用可能なフォームフラグメントの両方の作成がサポートされるようになりました。 作成者は、フォームの作成、送信アクションの設定、reCAPTCHA 検証の追加を、すべてシンプルなWYSIWYG オーサリング環境で視覚的に行えます。 この機能により、フォームの作成を促進し、一貫性を高め、スパムや自動不正使用に対する保護を向上させることができます。

* [SharePoint ドキュメントライブラリ - 添付ファイルを元のファイル名で保存](/help/forms/connect-forms-to-sharepoint-document-library.md#connect-an-adaptive-form-to-microsoft-sharepoint-document-library)：フォームの添付ファイルを SharePoint ドキュメントライブラリに保存する際に、元のファイル名を使用して保存するオプションが追加されました。この機能強化により、アップロードしたファイルの識別と管理が簡素化されます。

* **ルールエディター**：
   * [「When」句のクリックイベントを含むバイナリ条件](/help/forms/rule-editor-core-components-events-operators.md#available-operator-types-and-events-in-rule-editor)：ルールエディターでは、ボタンクリックイベント（_Is Clicked_）を「When」句内の他の条件と組み合わせることができるようになりました。これにより、ユーザーの操作やその他の要因に基づいて、ルールの実行をより正確に制御できます。メモ：複数の条件を使用する場合、クリックイベントを最初の条件としてリストする必要があります。
   * [フィールドとパネルの検証条件](/help/forms/rule-editor-core-components-usecases.md)：ルールエディターに _IsValid_ 条件と _IsNotValid_ 条件が含まれるようになりました。これらを使用すると、特定のフィールドまたはパネル全体（水平タブ、垂直タブ、アコーディオン、ウィザードなどのレイアウトを含む）の検証ステータスを確認できるので、検証結果に基づいてフォームのナビゲーションとユーザーエクスペリエンスが向上します。
* [SharePoint リストの範囲管理の改善](/help/forms/connect-forms-to-sharepoint-list.md)：SharePoint サイトでは、/sites や /teams などのすべての管理パスをサポートするようになりました。この機能強化により、様々な SharePoint サイト構造をまたいで幅広い統合が可能になり、組織のコンテンツに接続する際の柔軟性が向上します。
* [SharePoint リストへのレコードのドキュメントの保存のサポート](/help/forms/generate-document-of-record-core-components.md#bind-adaptive-form-components-with-template-fields)：SharePoint リストベースのフォームデータモデル（FDM）を使用して作成したフォームでは、レコードのドキュメントのバインド参照フィールドプロパティを設定して、レコードのドキュメント（DoR）を SharePoint リストに保存できるようになりました。この機能強化により、サポートされているフォームデータとドキュメントの SharePoint ストレージとのシームレスな統合が可能になります。
* [ アダプティブフォームフラグメントの自動マッピングのサポート ](/help/forms/adaptive-form-fragments-core-components.md#auto-mapping-support-for-fragments-in-an-adaptive-form)：アダプティブFormsでは、スキーマオブジェクトが定義済みのフラグメント構造に一致する場合の、マッチングフラグメントの自動挿入をサポートするようになりました。これにより、フォームの作成が合理化され、再利用が促進されます。

### AEM Forms の早期アクセス機能 {#forms-new-early-access-features}

AEM Forms 早期アクセスプログラムでは、最先端のイノベーションに排他的にアクセスし、その開発に貢献できるユニークな機会を提供します。

このリリースノートでは、現在のリリースで提供されるイノベーションのリストを示します。 早期アクセスプログラムで利用可能なイノベーションの完全なリストについては、[AEM Forms 早期アクセスプログラムのドキュメント](/help/forms/early-access-ea-features.md)を参照してください。

#### Adobe Experience Platform（AEP）と Forms の統合

* [AEM FormsとAdobe Experience Platformの統合 ](/help/forms/aem-forms-aep-connector.md):AEM Forms to Adobe Experience Platform Connector を使用すると、Adaptive FormsとAdobe Experience Platformをシームレスに統合できます。 この機能を使用すると、フォームデータを XDM スキーマにマッピングし、リアルタイムでAEPに直接送信できます。 Adobe Experience Cloud ソリューション全体で、パーソナライゼーションおよびアクティベーションのユースケースのためのデータキャプチャを効率化します。

## CIF アドオン {#cloud-services-cif}

### 機能強化 {#enhancements-cif}

* CIF 製品参照データタイプに製品バリアント選択の追加
* **試行用**:[JSON+LD をCIF コアコンポーネントの PDP に使用 ](/help/commerce-cloud/customizing/json-ld.md)
* **試行的**: [CIFでキャッシュをクリアする機能 ](/help/commerce-cloud/configuring/clear-cache.md)

### バグ修正 {#bug-fixes-cif}

* 製品フィールドでの検索の問題を修正
* 製品 URL 形式が #variant_sku に対して期待どおりに機能しない
* 製品リストコンポーネントに 20 個を超える SKU を追加できない

## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### OpenAPI ベースの API {#open-apis}

開発者は、AEM as Cloud Service の機能を、自分たちのアプリケーションやツールに深く統合できます。新しい AEM as a Cloud Service API は、OpenAPI 仕様に従い、一貫性の確保、明確な文書化、使いやすさを目標とします。認証を必要とするエンドポイントの資格情報は、Adobe Developer Console プロジェクトを作成することによって生成され、OAuth サーバー間、web アプリ、単一ページアプリ（SPA）をサポートします。

[詳しく](/help/implementing/developing/open-api-based-apis.md)は、OpenAPI ベースの API の[完全なリストを参照](https://developer.adobe.com/experience-cloud/experience-manager-apis/#openapi-based-apis)し、設定と使用方法を説明した[エンドツーエンドチュートリアル](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/aem-apis/openapis/invoke-api-using-oauth-s2s)を試してください。

後で使用するために認証済み API を設定する方法について詳しくは、次のビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3457510?quality=12&learn=on)

### CDN 設定関連の機能強化 {#cdn-enhancements}

アドビが管理する CDN では、[設定パイプラインの記事](/help/operations/config-pipeline.md#configurations)で説明されているように、柔軟な設定オプションが提供されます。最新の機能のいくつかを以下に示します。

#### CDN ログに追加のプロパティを含める {#props-in-cdnlogs}

デバッグやデータ分析などのシナリオに役立ち、[リクエストと応答の変換](/help/implementing/dispatcher/cdn-configuring-traffic.md#request-transformations)で `logProperty` アクションを設定して、デフォルトのプロパティ以外の詳細情報を CDN ログに含めることができます。

#### 一致条件としての地域、大陸、組織のプロパティ {#matching-conditions}

CDN ルールは、トラフィックのブロックやリダイレクトなどのユースケースに対して、地域、大陸、組織に基づいて照合できるようになりました。`clientRegion` と `clientContinent` は、既にサポートされている `clientCountry` を拡張して地域に基づいて照合し、`clientAsName` と `clientAsNumber` は自律システムと照合して大規模な ISP、会社、クラウドプロバイダーを識別します。詳しくは、これらの[新しく公開したリクエストプロパティ](/help/security/traffic-filter-rules-including-waf.md#condition-structure)を参照してください。

#### cookie の値を設定 {#cookie-attributes}

cookie の属性は、[応答変換](/help/implementing/dispatcher/cdn-configuring-traffic.md#response-transformations)で設定できます。

### Java 21 サポート {#java21}

1月リリース以降、Java 21 および Java 17 を使用してコードをビルドできます。パターンマッチング、sealed クラス、様々なパフォーマンスの向上などの新しい機能にアクセスできます。Maven プロジェクトとライブラリのバージョンのアップデートを含む設定手順について詳しくは、[ビルド環境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support)の記事を参照してください。

Java 17 または 21 ビルドが検出されると、より高パフォーマンスの Java 21 **ランタイム**&#x200B;が自動的にデプロイされます。ただし、アドビでは、Java 11 でビルドされた環境については、[aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com) にメールを送信して Java 21 ランタイムをオプトインすることをお勧めします。[Java 21 ランタイム要件](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)について説明します。

>[!IMPORTANT]
>
> Java 21 **ランタイム**&#x200B;は、2月に開発／RDE 環境にデプロイされました。**4月28日（PT）と29日（PT）**&#x200B;にステージ／実稼動環境に適用する予定です。Java 21（または Java 17）を使用した&#x200B;**コードのビルド**&#x200B;は、Java 21 ランタイムとは独立しています。Java 21（または Java 17）でコードをビルドする手順を明示的に実行する必要があります。

### AEM のログ設定ポリシーの適用 {#logconfig-policy}

顧客環境を効果的に監視するには、AEM Java ログで一貫性のある形式を維持し、カスタム設定で上書きされないようにする必要があります。ログ出力は、デフォルトのファイルに出力されたままにする必要があります。AEM 製品コードの場合、デフォルトのログレベルを保持する必要があります。ただし、顧客開発コードの場合、ログレベルを調整できます。

そのため、次の OSGi プロパティを変更しないでください。
* **Apache Sling ログ設定**（PID：`org.apache.sling.commons.log.LogManager`）- *すべてのプロパティ*
* **Apache Sling Logging Logger Configuration**（ファクトリー PID：`org.apache.sling.commons.log.LogManager.factory.config`）：
   * `org.apache.sling.commons.log.file`
   * `org.apache.sling.commons.log.pattern`

5月中旬に、AEM ではこれらのプロパティに対するカスタム変更がすべて無視されるポリシーが適用されます。ダウンストリームプロセスを確認し、それに応じて調整してください。例えば、ログ転送機能を使用する場合：
* ログ宛先でカスタム（デフォルト以外）ログ形式が必要な場合は、取り込みルールを更新する必要があります。
* ログレベルの変更によってログの冗長性が低下する場合は、デフォルトのログレベルではログのボリュームが大幅に増加することがあります。

### その他の宛先へのAEM ログ転送 - ベータ版プログラム {#log-forwarding-earlyadopter}

現在のベータ版では、AEM ログを New Relic（HTTPS を使用）、Amazon S3、Sumo Logic に転送できます。AEM ログ（Apache／Dispatcher を含む）はサポートされていますが、CDN ログはサポートされていません。アクセスについて詳しくは、[aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) までメールで送信してください。

ログは Cloud Manager からダウンロードできますが、多くの組織では、これらのログを優先されるログの宛先にストリームすると役立ちます。AEM では既に、Azure Blob Storage、Datadog、HTTPS、Elasticsearch（および OpenSearch）、Splunk への AEM および CDN ログ転送（GA）をサポートしています。この機能は、セルフサービス方式で設定し、設定パイプラインを使用してデプロイします。

詳しくは、[ログ転送ドキュメント](/help/implementing/developing/introduction/log-forwarding.md)を参照してください。

### Edge コンピューティング - フィードバックのリクエスト {#edge-computing-feedback}

Edge コンピューティングには、データ処理がブラウザーに近づくので、待ち時間が短縮されるなどのメリットがあります。 このテクノロジーが AEM の配信を公開および Edge Delivery Services プロジェクトに役立つかどうかについて、ぜひお聞かせください。さらに、製品ロードマップへのインプットとして、お客様が何を想定されるかをお教えください。

いくつかの考えられるユースケース：

* コンテンツへのアクセスをゲートする IdP を使用した認証
* 位置情報、デバイスタイプ、ユーザー属性などに基づく動的コンテンツのレンダリングによるパーソナライゼーション。
* 高度な画像操作
* CDN とオリジンの間のミドルウェア
* ブラウザーとサードパーティ API の間のレイヤー（API 応答の再フォーマット用など）
* クライアントブラウザーでレンダリングしやすくする、複数のオリジンからのデータの集計

ご質問やご意見がある場合は、[aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) までメールで送信してください。

## [!DNL Experience Manager] ガイド {#guides}

Adobe Experience Manager Guides の最新リリースの新機能と強化機能の完全なリストについては、[こちら](https://experienceleague.adobe.com/ja/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)を参照してください。

## Cloud Manager {#cloud-manager}

Cloud Manager の月次リリースの完全なリストは、[こちら](/help/implementing/cloud-manager/release-notes/current.md)で確認できます。

## 移行ツール {#migration-tools}

移行ツールのリリースの完全なリストは、[こちら](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)で確認できます

## ユニバーサルエディター {#universal-editor}

ユニバーサルエディターのリリースの完全なリストは、[こちら](/help/release-notes/universal-editor/current.md)で確認できます。

## バリエーションの生成 {#generate-variations}

バリエーションの生成のリリースの完全なリストは、[こちら](/help/generative-ai/release-notes-generate-variations.md)で確認できます。

## Experience Cloud のリリースノート {#experience-cloud}

他の Experience Cloud アプリケーションのリリースについて詳しくは、[こちら](https://experienceleague.adobe.com/ja/docs/release-notes/experience-cloud/current)を参照してください。
