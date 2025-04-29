---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service の最新のリリースノート。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 05c34d45e27a8ef22c1ebca72d362529669339fa
workflow-type: tm+mt
source-wordcount: '1713'
ht-degree: 43%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート {#release-notes}

以下のセクションでは、[!DNL Experience Manager] as a Cloud Service の現在（最新）のバージョンの機能リリースノートの概要について説明します。

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

<!-- 

## Release Video {#release-video}

Have a look at the February 2025 Release Overview video for a summary of the features added in the 2025.2.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Experience Manager Sitesの新機能 {#enhancements-sites}

**新しいコンテンツフラグメントモデル管理 UI**

さらに、新しいクライアントサイドユーザーインターフェイスのリストを確認AEM コンテンツフラグメントを使用する場合、コンテンツフラグメントモデル用に新しい管理 UI が使用できるようになりました。 新しい UI は、フィルターを使用してモデルを検索でき、モデルタグと、特定のモデルに基づいて存在するコンテンツフラグメントを表示する、クリーンで最新のリスト表示を提供します。 ドキュメントは [ こちら ](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md) で参照できます。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Dynamic Media （Scene7） {#dynamic-media-scene7}

**Dynamic Media （Scene7）はセキュリティの強化環境ではサポートされていません**

AEM as a Cloud Service上の Dynamic Media （Scene7）は HIPAA に対応しておらず、セキュリティの強化が有効になっているAEM環境では使用できません。

2025 年 4 月のAEM as a Cloud Service リリース以降、セキュリティが強化された環境では、技術的な制限により、Dynamic Media （Scene7）を設定できなくなります。 その結果、これらの環境では **ツール**/**クラウドサービス** の下の **Dynamic Media 設定** カードが表示されなくなります。

さらに、AEM 6.5 を使用しているお客様は、Dynamic Media （Scene7）スタックが HIPAA に対応していないことに注意してください。

### Dynamic Media Classic {#dynamic-media-classic}

**レポート**

Dynamic Media Classic レポートダッシュボードの「帯域幅」タブは、2025年4月以降サポートされなくなりました。

[帯域幅とストレージ、レポートのタイプ](https://experienceleague.adobe.com/ja/docs/dynamic-media-classic/using/setup/administration-setup#types-of-reports)を参照してください。


## Assets ビューの新機能 {#new-features-assets-view}

**アセットの関連付け**

アセットビューでは、簡素化されたアセットの詳細パネルでアセットの関係付けの表示と編集がサポートされるようになりました。Sourceや派生などの関係をコンテンツに簡単に追加して、関連するヒーローコンテンツをより効果的に見つけられるようにします。

![Assets関係の例 ](/help/assets/assets/asset-relations-example.png)

**アセットのバージョンの比較**

Assets ビューを使用して、アセットの任意のバージョンと最新のバージョンをすばやく選択および比較できるようになりました。

![アセットのバージョンを比較](/help/assets/assets/version-compare2.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### プレリリース機能

* [ ユニバーサルエディター – フォームフラグメント ](/help/edge/docs/forms/universal-editor/creating-form-fragments.md)：ユニバーサルエディターで、アダプティブForms用のフォームフラグメントを作成して再利用できるようになりました。 これらのフラグメントは、一度作成して、複数のフォームに適用できる再利用可能なフォームセクション（連絡先の詳細、同意フィールドなど）です。 この機能により、フォームの作成が合理化され、一貫性が確保され、オーサリングの効率が向上します。

* [SharePoint ドキュメントライブラリ – 添付ファイルを元のファイル名で保存 ](/help/forms/connect-forms-to-sharepoint-document-library.md#connect-an-adaptive-form-to-microsoft-sharepoint-document-library): SharePoint ドキュメントライブラリに添付ファイルを保存する際に、元のファイル名を使用してフォームの添付ファイルを保存するオプションが追加されました。 この機能強化により、アップロードされたファイルの識別と管理が簡素化されます。

* **ルールエディター**:
   * [ 「When」句内のクリックイベントを含むバイナリ条件 ](/help/forms/rule-editor-core-components-events-operators.md#available-operator-types-and-events-in-rule-editor)：ルールエディターでは、ボタンクリックイベント（_クリックされた_）と「When」句内の他の条件を組み合わせることができるようになりました。 これにより、ユーザーの操作などに基づいて、ルールの実行をより正確に制御できます。 メモ：複数の条件を使用する場合、クリックイベントを最初の条件にする必要があります。
   * [ フィールドおよびパネルの検証条件 ](/help/forms/rule-editor-core-components-usecases.md)：ルールエディターに _IsValid_ 条件と _IsNotValid_ 条件が含まれるようになりました。 これらを使用すると、特定のフィールドまたはパネル全体（水平タブ、垂直タブ、アコーディオン、ウィザードなどのレイアウトを含む）の検証ステータスを確認でき、検証結果に基づいてフォームのナビゲーションとユーザーエクスペリエンスを向上させることができます。
* **SharePoint リストの範囲管理の向上**:SharePoint サイトでは、/sites や/teams などのすべての管理パスをサポートするようになりました。 この機能強化により、様々なSharePoint サイト構造にわたる統合が可能になり、組織のコンテンツへの柔軟な接続が可能になります。
* **SharePoint リストへのレコードのドキュメントの保存のサポート**:SharePoint リストベースのフォームデータモデル（FDM）を使用して作成されたFormsでは、レコードのドキュメントバインド参照フィールドプロパティを設定することにより、レコードのドキュメント（DoR）をSharePoint リストに保存できるようになりました。 この機能強化により、サポートされているフォームデータとドキュメントをSharePoint ストレージとシームレスに統合できます。

### AEM Formsの早期アクセス機能 {#forms-new-early-access-features}

AEM Forms 早期アクセスプログラムでは、最先端のイノベーションに排他的にアクセスし、その開発に貢献できるユニークな機会を提供します。

このリリースノートでは、現在のリリースで提供されるイノベーションのリストを示します。 早期アクセスプログラムで利用可能なイノベーションの完全なリストについては、[AEM Forms 早期アクセスプログラムのドキュメント](/help/forms/early-access-ea-features.md)を参照してください。

#### Adobe Experience Platform（AEP）とFormsの統合

FormsとAEPの統合機能が、早期導入ユーザー向けに提供されるようになりました。

## CIF アドオン {#cloud-services-cif}

### 機能強化 {#enhancements-cif}

* CIF製品リファレンスデータタイプの製品バリアントセレクションを追加
* [ 試行用 ]:PDP のCIF コアコンポーネントにおける JSON+LD
* [ 試行的 ]:CIFでキャッシュをクリアする機能

### バグ修正 {#bug-fixes-cif}

* 製品フィールドの検索問題を修正しました
* 製品の URL 形式が#variant_sku で期待どおりに動作しない
* 製品リストコンポーネントに 20 個を超える SKU を追加できない

## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### OpenAPI ベースの API {#open-apis}

開発者は、AEM as Cloud Service の機能を独自のアプリケーションやツールに深く統合できます。 新しい AEM as a Cloud Service API は、OpenAPI 仕様に従い、一貫性の確保、明確な文書化、使いやすさを目標とします。認証が必要なエンドポイントの資格情報は、Adobe Developer Console プロジェクトを作成することで生成され、OAuth サーバー間、web アプリ、シングルページアプリ（SPA）をサポートします。

OpenAPI ベースの API の [ 完全なリストを参照 ](https://developer.adobe.com/experience-cloud/experience-manager-apis/#openapi-based-apis)、[ 詳細情報 ](/help/implementing/developing/open-api-based-apis.md) および設定と使用方法を説明した [ エンドツーエンドのチュートリアル ](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/aem-apis/openapis/invoke-api-using-oauth-s2s) を試してください。

認証済み API を後で使用できるように設定する方法については、このビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3457510?quality=12&learn=on)

### CDN 設定関連の機能強化 {#cdn-enhancements}

Adobeが管理する CDN は、[ 設定パイプラインの記事 ](/help/operations/config-pipeline.md#configurations) で説明されているように、柔軟な設定オプションを提供します。 最近の機能を次に示します。

#### CDN ログに追加のプロパティを含める {#props-in-cdnlogs}

デバッグやデータ分析などのシナリオで役立つ場合、[ リクエストと応答の変換 ](/help/implementing/dispatcher/cdn-configuring-traffic.md#request-transformations) で `logProperty` アクションを設定することで、デフォルトのプロパティ以外の詳細を CDN ログに含めることができます。

#### 一致条件としての地域、大陸、および組織プロパティ {#matching-conditions}

CDN ルールが、地域、大陸、組織に基づいて、トラフィックのブロックやリダイレクトなどのユースケースで一致するようになりました。 `clientRegion` と `clientContinent` は、既にサポートされている `clientCountry` を地域に基づいて照合するように強化し、`clientAsName` と `clientAsNumber` は Autonomous Systems と照合して、大規模な ISP、企業、クラウドプロバイダーを特定します。 これらの [ 新しく公開されたリクエストプロパティ ](/help/security/traffic-filter-rules-including-waf.md#condition-structure) について説明します。

#### Cookie の値を設定 {#cookie-attributes}

cookie の属性は [ 応答の変換 ](/help/implementing/dispatcher/cdn-configuring-traffic.md#response-transformations) で設定できます。

### Java 21 サポート {#java21}

1月リリース以降、Java 21 および Java 17 を使用してコードをビルドできます。パターンマッチング、sealed クラス、様々なパフォーマンスの向上などの新しい機能にアクセスできます。Maven プロジェクトとライブラリのバージョンのアップデートを含む設定手順について詳しくは、[ビルド環境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support)の記事を参照してください。

Java 17 または 21 ビルドが検出されると、より高パフォーマンスの Java 21 **ランタイム**&#x200B;が自動的にデプロイされます。ただし、アドビでは、Java 11 でビルドされた環境については、[aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com) にメールを送信して Java 21 ランタイムをオプトインすることをお勧めします。[Java 21 ランタイム要件](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)について説明します。

>[!IMPORTANT]
>
> Java 21 **ランタイム**&#x200B;は、2月に開発／RDE 環境にデプロイされました。**4月28日（PT）と29日（PT）**&#x200B;にステージ／実稼動環境に適用する予定です。Java 21（または Java 17）を使用した&#x200B;**コードのビルド**&#x200B;は、Java 21 ランタイムとは独立しています。Java 21（または Java 17）でコードをビルドする手順を明示的に実行する必要があります。

### AEMのログ設定ポリシーの適用 {#logconfig-policy}

お客様の環境を効果的に監視するには、AEM Java ログが一貫した形式を維持する必要があり、カスタム設定で上書きしてはなりません。 ログ出力は、デフォルトのファイルにダイレクトされたままにする必要があります。 AEMの商品コードの場合、デフォルトのログレベルを保持する必要があります。 ただし、顧客開発コードのログレベルを調整することは可能です。

このためには、次の OSGi プロパティは変更しないでください。
* **Apache Sling ログ設定** （PID:`org.apache.sling.commons.log.LogManager`） — *すべてのプロパティ*
* **Apache Sling Logging Logger Configuration** （ファクトリ PID:`org.apache.sling.commons.log.LogManager.factory.config`）:
   * `org.apache.sling.commons.log.file`
   * `org.apache.sling.commons.log.pattern`

5 月中旬、AEMは、これらのプロパティへのカスタム変更が無視されるポリシーを適用します。 ダウンストリームプロセスを確認し、それに応じて調整してください。 例えば、ログ転送機能を使用する場合は、次のようになります。
* ログ宛先でカスタム（デフォルト以外）のログ形式を使用したい場合は、取り込みルールを更新する必要がある可能性があります。
* ログレベルを変更するとログの冗長性が低下する場合は、デフォルトのログレベルを使用すると、ログのボリュームが大幅に増加する可能性があります。

### その他の宛先へのAEM ログ転送 – Beta プログラム {#log-forwarding-earlyadopter}

現在のベータ版では、AEM ログを New Relic（HTTPS を使用）、Amazon S3、Sumo Logic に転送できます。AEM ログ（Apache／Dispatcher を含む）はサポートされていますが、CDN ログはサポートされていません。アクセスについて詳しくは、[aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) までメールで送信してください。

ログは Cloud Manager からダウンロードできますが、多くの組織では、これらのログを優先されるログの宛先にストリームすると役立ちます。AEM では既に、Azure Blob Storage、Datadog、HTTPS、Elasticsearch（および OpenSearch）、Splunk への AEM および CDN ログ転送（GA）をサポートしています。この機能は、セルフサービス方式で設定し、設定パイプラインを使用してデプロイします。

詳しくは、[ログ転送ドキュメント](/help/implementing/developing/introduction/log-forwarding.md)を参照してください。

### Edge コンピューティング - フィードバックのリクエスト {#edge-computing-feedback}

Edge コンピューティングには、データ処理がブラウザーに近づくので、待ち時間が短縮されるなどのメリットがあります。 このテクノロジーが AEM の配信を公開および Edge Delivery Services プロジェクトに役立つかどうかについて、ぜひお聞かせください。さらに、製品ロードマップへのインプットとして、お客様が何を想定されるかをお教えください。

いくつかの考えられるユースケース：

* コンテンツへのアクセスをゲートする IdP を使用した認証
* 位置情報、デバイスタイプ、ユーザー属性などに基づいて動的コンテンツをレンダリングすることによるPersonalization
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
