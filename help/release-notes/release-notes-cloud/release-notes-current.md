---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service の最新のリリースノート。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 628d254ee130d436f0ac1728ab464d24db583b81
workflow-type: tm+mt
source-wordcount: '2074'
ht-degree: 31%

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


[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の最新の機能リリース（2025.5.0）のリリース日は 2025年6月5日です。次回の機能リリース（2025.6.0）は 2025年6月26日（PT）に予定されています。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

<!-- 

## Release Video {#release-video}

Have a look at the February 2025 Release Overview video for a summary of the features added in the 2025.2.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**AI が生成したメタデータ**

AEM Assetsでは [AI を使用して、タイトル、説明、キーワードなどのメタデータを自動生成するようになりました ](/help/assets/metadata-assets-view.md#ai-smart-tags)。 これらの AI で生成されたフィールドは、メタデータの精度を高め、アセットの検索、分類および推奨を容易にします。 このアプローチは、手動でのタグ付けを排除することで効率を向上させるだけでなく、大量のデジタルコンテンツ間の一貫性と拡張性も確保します。

![AI で生成されたメタデータ ](/help/assets/assets/enhanced-smart-tags.png)

**Figma との統合**

AEM Assetsは Figma とネイティブに統合されているので、デザイナーは Figma ユーザーインターフェイス内からAEM Assetsに保存されているアセットに直接アクセスできます。 AEM Assetsで管理されているコンテンツを Figma キャンバスに配置してから、新しいコンテンツや編集したコンテンツをAEM Assets リポジトリに保存することができます。 Figma コミュニティページで利用可能なAEM Assets コネクタにアクセスするには、[ ここ ](https://www.figma.com/community/plugin/1512561378275712210/adobe-experience-manager-aem-assets-connector) をクリックします。

>[!VIDEO](https://video.tv.adobe.com/v/3463828)


### Content Hubの新機能 {#new-features-content-hub}

**属性ベースのアクセス制御（ABAC）**

[Content Hubで、アセット ](/help/assets/attribute-based-access-control.md) にアクセスする際に、ルールベースの制限を適用できるようになりました。 アセット権限を使用すると、ガバナンスが確保され、ユーザーは関連するアセットにのみアクセスできるようになります。

アセット制限ルールはメタデータに基づいており、ルールで定義された条件がアセットメタデータに一致する場合、アセットはユーザーグループに表示されます。

属性ベースのアクセス制御の主なメリットには、次のようなものがあります。

* 権限のフォルダー構造への依存を排除

* 管理者がアセットをアップロードし、遡及的に権限構造を決定できるようになります。

* 重複の数を減らす – アセットの整合性を向上させます。 同じアセットが異なるグループと共有される場合は、フォルダーベースの権限で重複が必要です。

**UI ブランディング**

Content Hubでは、プライマリ色とセカンダリ色に加え、バナー画像、バナータイトル、本文テキストなど [&#128279;](/help/assets/configure-content-hub-ui-options.md##configure-branding-content-hub) ブランド固有の要素を使用してユーザーインターフェイスをカスタマイズ  できます。 これらの機能強化により、ブランドの一貫性の確保、ユーザーのオンボーディングの簡素化、信頼の構築が可能になります。

![UI ブランディング ](/help/assets/assets/content-hub-ui-branding.png)

**公開リンクの共有**

Content Hubでは、アプリケーションにアクセスすることなく [ アセットのメタデータを表示したり、アセットをダウンロードしたりできるように ](/help/assets/share-assets-content-hub.md##share-assets) 共有可能なリンクを生成」できるようになりました。

![UI ブランディング ](/help/assets/assets/public-and-private-link.png)

**回収ガバナンス**

Content Hubでは、[ 作成時のコレクションへのアクセスを制御し、許可されたユーザーのみがグループ化されたアセットを表示または管理できるようにする ](/help/assets/collections-content-hub.md##create-collections) ことができるようになりました。 これにより、セキュリティの向上、共同作業の向上、組織的なアセット管理、ガバナンスの効率化が実現します。

>[!VIDEO](https://video.tv.adobe.com/v/3463336)

>[!NOTE]
>
>コレクションガバナンスは限定提供の機能です。 有効にするには、サポートチケットを作成します。

**複数のアセットを ZIP としてダウンロードする**

また、Content Hubでは、ファイル管理を簡単にする個別のファイルとして使用するのではなく [&#128279;](/help/assets/download-assets-content-hub.md#download-asset-renditions) 選択したアセットとそのレンディションを ZIP ファイルでダウンロード  できるようになりました。

**Content Hubの Dynamic Media レンディション**

すべての [Dynamic Media プリセットレンディションおよびダウンロード用のスマート切り抜き ](/help/assets/download-assets-content-hub.md#download-asset-renditions) には、Content Hub ユーザーインターフェイス内から直接アクセスします。

&#x200B;![Dynamic Media レンディション ](/help/assets/assets/dm-renditions-content-hub.png)

### Dynamic Media の新機能 {#new-features-dynamic-media}

**AJO B2C と Dynamic Media のネイティブ統合&#x200B;**

[Experience Manager（AEM） Dynamic Media とJourney Optimizer（AJO） B2C](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/content-management/combine/aem-dynamic) のネイティブ統合により、マーケターはAEM Dynamic Media アセット（レンディションおよび DM テンプレート）をAJO コンテンツに簡単に埋め込み、チャネル間でリアルタイムに更新され、高度にパーソナライズされたエクスペリエンスを提供できます。

>[!VIDEO](https://video.tv.adobe.com/v/3457695/?learn=on&enablevpops=&autoplay=true)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### プレリリース機能

* [ユニバーサルエディター - フォームフラグメント](/help/edge/docs/forms/universal-editor/creating-form-fragments.md)：ユニバーサルエディターでは、アダプティブフォームのフォームフラグメントを作成して再利用できるようになりました。これらのフラグメントは、一度作成したら複数のフォームに適用できる、再利用可能なフォームセクション（連絡先の詳細、同意フィールドなど）です。この機能により、フォームの作成が効率化され、一貫性が確保され、オーサリングの効率が向上します。

* [SharePoint ドキュメントライブラリ - 添付ファイルを元のファイル名で保存](/help/forms/connect-forms-to-sharepoint-document-library.md#connect-an-adaptive-form-to-microsoft-sharepoint-document-library)：フォームの添付ファイルを SharePoint ドキュメントライブラリに保存する際に、元のファイル名を使用して保存するオプションが追加されました。この機能強化により、アップロードしたファイルの識別と管理が簡素化されます。

* **ルールエディター**：
   * [「When」句のクリックイベントを含むバイナリ条件](/help/forms/rule-editor-core-components-events-operators.md#available-operator-types-and-events-in-rule-editor)：ルールエディターでは、ボタンクリックイベント（_Is Clicked_）を「When」句内の他の条件と組み合わせることができるようになりました。これにより、ユーザーの操作やその他の要因に基づいて、ルールの実行をより正確に制御できます。メモ：複数の条件を使用する場合、クリックイベントを最初の条件としてリストする必要があります。
   * [フィールドとパネルの検証条件](/help/forms/rule-editor-core-components-usecases.md)：ルールエディターに _IsValid_ 条件と _IsNotValid_ 条件が含まれるようになりました。これらを使用すると、特定のフィールドまたはパネル全体（水平タブ、垂直タブ、アコーディオン、ウィザードなどのレイアウトを含む）の検証ステータスを確認できるので、検証結果に基づいてフォームのナビゲーションとユーザーエクスペリエンスが向上します。
* [SharePoint リストの範囲管理の改善](/help/forms/connect-forms-to-sharepoint-list.md)：SharePoint サイトでは、/sites や /teams などのすべての管理パスをサポートするようになりました。この機能強化により、様々な SharePoint サイト構造をまたいで幅広い統合が可能になり、組織のコンテンツに接続する際の柔軟性が向上します。
* [SharePoint リストへのレコードのドキュメントの保存のサポート](/help/forms/generate-document-of-record-core-components.md#bind-adaptive-form-components-with-template-fields)：SharePoint リストベースのフォームデータモデル（FDM）を使用して作成したフォームでは、レコードのドキュメントのバインド参照フィールドプロパティを設定して、レコードのドキュメント（DoR）を SharePoint リストに保存できるようになりました。この機能強化により、サポートされているフォームデータとドキュメントの SharePoint ストレージとのシームレスな統合が可能になります。

### AEM Forms の早期アクセス機能 {#forms-new-early-access-features}

AEM Forms 早期アクセスプログラムでは、最先端のイノベーションに排他的にアクセスし、その開発に貢献できるユニークな機会を提供します。

このリリースノートでは、現在のリリースで提供されるイノベーションのリストを示します。 早期アクセスプログラムで利用可能なイノベーションの完全なリストについては、[AEM Forms 早期アクセスプログラムのドキュメント](/help/forms/early-access-ea-features.md)を参照してください。

#### Adobe Experience Platform（AEP）と Forms の統合

Forms と AEP 間の統合機能が、早期導入者向けに提供されるようになりました。

## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### 更新された非推奨プロセス {#updated-deprecation-process}

Adobeは、パフォーマンス、セキュリティ、価値に関する標準を満たすように、機能、ライブラリ、API および設定を定期的にレビューします。 機能がこれらの標準を満たさなくなった場合、機能は廃止とマークされ、指定した削除日までに使用を停止する必要があります。 この日付までに、Adobeは、新しいビルドを進めたりデプロイしたりする前に、Cloud Managerで実行する必要があるメール通知やアクションをお客様に通知します。 必要な対策を講じないと、AEMの新しいバージョンにアップグレードできなくなる可能性があり、セキュリティ、パフォーマンス、信頼性、可用性に関する潜在的な影響を引き起こす可能性があります。

詳しくは、[ 非推奨の記事 ](/help/release-notes/deprecated-removed-features.md) を参照してください。

#### 廃止予定の Java API と削除日近くの OSGi 設定 {#deprecated-near-removals}

以下のリストを展開して、使用する必要がなくなった非推奨（廃止予定）の API と OSGi 設定を確認します。 削除のタイムラインなど、詳細については、非推奨（廃止予定）の記事を参照してください。

<details>
  <summary>展開して非推奨（廃止予定）を確認</summary>

Java API:
* `org.apache.sling.commons.auth`
* `org.apache.felix.webconsole`
* `org.eclipse.jetty`
* `com.mongodb`
* `org.apache.abdera`
* `org.apache.felix.http.whiteboard`
* `org.apache.cocoon.xml`
* `ch.qos.logback`
* `org.slf4j.spi`
* `org.slf4j.event`
* `org.apache.log4j`
* `com.google.common`
* `com.drew`
* `org.bson`
* `org.apache.jackrabbit.oak.plugins.blob`
* `org.apache.jackrabbit.oak.plugins.memory`

OSGi プロパティ：

* `org.apache.sling.commons.log.LogManager` （すべてのプロパティ）
* `org.apache.sling.commons.log.LogManager.factory.config` （`org.apache.sling.commons.log.file`, `org.apache.sling.commons.log.pattern`）

</details>

### Java 11 Runtime の廃止 {#java11-runtime-deprecation}

**Java 11 ランタイム** は非推奨（廃止予定）になり、ほとんどの環境は既に、よりパフォーマンスの高い **Java 21 ランタイム** にアップグレードされています。

サポートされていない依存関係が原因で、環境をアップグレードできなかった場合（[Java 21 ランタイム要件 ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements) を参照）、次の具体的な手順を記載したメールがAdobeから届いています。 **2025 年 8 月 28 日（PT）** までに必要な更新がすべて完了していることを確認してください。これにより、中断することなく環境をアップグレードできます。

メモ：ランタイムバージョンは、コードのビルドバージョンとは別のものです。 Java 21 を使用してビルドすることをお勧めしますが、現時点では、Java 11 ビルドは引き続きサポートされます。 Java 11 ビルドの廃止に関する通知は、今後共有される予定です。

### AEM Java ログ設定ポリシーの適用 {#logconfig-policy}

4 月のリリースノートに記載されているように、AEMの Java ログは、すべてのお客様の環境で信頼性の高い監視を確実に行うために、標準形式に従う必要があります。 ログ形式、出力ファイル、デフォルトログレベルの変更などのカスタムログ設定は、サポートされなくなりました。 ログはデフォルトファイルにダイレクトされ続け、AEM製品コードのデフォルトログレベルは保持される必要があります。 詳しくは、[ ログに関する記事 ](/help/implementing/developing/introduction/logging.md#configuration-loggers) を参照してください。

**8 月下旬** 以降、サポートされていないカスタムログの上書きは無視されます。 アドビの分析によると、ほとんどのお客様は影響を受けず、Adobeは、現在の設定が影響を受ける可能性があるお客様に直接連絡します。

カスタムログ動作に依存するダウンストリームプロセスを確認し、更新してください。 例：

* ログ転送システムでカスタムログ形式が想定されている場合は、取り込みルールを調整する必要がある可能性があります。
* 以前にログレベルを変更してログの冗長性を減らしたことがある場合は、デフォルトレベルに戻すとログのボリュームが増える可能性があることに注意してください。

### 古いバージョンと監査ログのデフォルトのパージ {#mt-defaults}

現在、コンテンツバージョンおよび監査ログは、関連する *パージメンテナンスタスク* がデフォルトで無効になっているので、それぞれの OSGi プロパティで明示的に設定されない限り、データは削除されません。

ただし、リポジトリのパフォーマンスを最適化するために、**2025 年 6 月下旬** 以降、次のガイドラインに従って、デフォルトでパージが有効になります。

#### コンテンツのバージョン {#mt-content}

* **新しい環境** （今後の日付以降に作成（後で通知します）
   * **30 日** より古いバージョンは定期的に削除されます。
   * 過去 30 日間の最新の 5 つのバージョンが、年齢に関係なく、最新のバージョンと現在のバージョンと共に保持されます。

* **既存の環境** （この予定日の前に作成）:
   * **7 年** より古いバージョンは定期的に削除されます。
   * 過去 7 年間のすべてのバージョンが保持されます。
   * このデフォルトのしきい値の高さは、最近のデータが意図せずに削除されるのを防ぎます。 ただし、リポジトリのパフォーマンスを最適化するには、小さい値を設定することをお勧めします。

* これらのデフォルトは、OSGi 設定の上書きで変更できます。

#### 監査ログ {#mt-auditlogs}

* **新しい環境** （今後作成され、個別にお知らせします）:
   * **7 日** より古いレプリケーション、DAM およびページ監査ログは、定期的に削除されます。
   * デフォルトでは、すべてのイベントがログに記録されます。

* **既存の環境** （この予定日の前に作成）:
   * **7 年以上前のレプリケーション、DAM、ページ監査ログは** 定期的に削除されます。
   * デフォルトでは、すべてのイベントがログに記録されます。
   * このデフォルトのしきい値の高さは、最近のデータが意図せずに削除されるのを防ぎます。 ただし、リポジトリのパフォーマンスを最適化するには、小さい値を設定することをお勧めします。

* これらのデフォルトは、OSGi 設定の上書きで変更できます。

詳しくは、[ メンテナンスタスクの記事 ](/help/operations/maintenance.md#defaults) を参照してください。

### Edge Computing （Alpha プログラム） {#edge-computing}

Edge コンピューティングを使用すると、CDN レイヤーでJavaScriptを実行し、データ処理をエンドユーザーに近づけることができます。 これにより、待ち時間が短縮され、エッジでのレスポンシブな動的エクスペリエンスが可能になります。

一般的なユースケースを次に示します。

* コンテンツへのアクセスを許可する前に、ID プロバイダーを使用してユーザーを認証する
* 位置情報、デバイスタイプまたはユーザー属性に基づくコンテンツのパーソナライズ
* CDN とオリジンの間のミドルウェアとして機能させる
* ブラウザーに配信する前に、サードパーティの API からの応答を再フォーマットする（および複数の API 応答を集計する）
* 様々なバックエンドからステッチされたコンテンツを使用して、サーバーレンダリングされたHTMLをエッジで作成および提供する

AEM パブリッシュ配信またはライブ実稼動サイトのEdge Delivery Services プロジェクトで利用できる機会の数は限られています。 参加に関心がある場合や、詳細を確認したい場合は、ユースケースの簡単な説明を添えて [&#128279;](mailto:aemcs-edgecompute-feedback@adobe.com)0&rbrace;aemcs-edgecompute-feedback@adobe.com&rbrace; までメールでお問い合わせください。

### Edge Delivery Servicesの CDN 設定（Beta プログラム） {#cdn-eds-beta}

Adobeが管理する CDN は、[ 設定パイプラインの記事 ](/help/operations/config-pipeline.md#configurations) で説明されているように、柔軟な設定オプションを提供します。

ベータ版では、CDN オリジンセレクター、応答、リクエスト変換などの機能の設定パイプラインをデプロイします。 ユースケースの詳細については、[aemcs-cdn-config-adopter@adobe.com](mailto:aemcs-cdn-config-adopter@adobe.com) にお問い合わせください。

### その他の宛先へのAEM ログ転送（Beta プログラム） {#log-forwarding-beta}

ログは Cloud Manager からダウンロードできますが、多くの組織では、これらのログを優先されるログの宛先にストリームすると役立ちます。AEMは、既に Azure Blob Storage、Datadog、HTTPS、Elasticsearch（および OpenSearch）、Splunk へのAEMおよび CDN ログ転送をサポートしています。 この機能は、セルフサービス方式で設定し、設定パイプラインを使用してデプロイします。

ベータ版では、AEM ログをAmazon S3、Sumo Logic および独自のNew Relic アカウント（Adobeが提供するアカウントではありません）に転送できます。 なお、これらのログ先ではAEM ログ（Apache/Dispatcherを含む）がサポートされていますが、CDN ログはサポートされていません。 アクセスについて詳しくは、[aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) までメールで送信してください。

詳しくは、[ログ転送ドキュメント](/help/implementing/developing/introduction/log-forwarding.md)を参照してください。

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
