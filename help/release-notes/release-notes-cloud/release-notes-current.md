---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service の最新のリリースノート。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 75816f35a8bca8356e17b13341c2ddbd850f8eff
workflow-type: tm+mt
source-wordcount: '2077'
ht-degree: 95%

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

**AI 生成のメタデータ**

AEM Assets では [AI を使用して、タイトル、説明、キーワードなどのメタデータが自動生成されるようになりました ](/help/assets/metadata-assets-view.md#ai-smart-tags)。これらの AI で生成されたフィールドは、メタデータの精度を高め、アセットの検索、分類および推奨を容易にします。このアプローチでは、手動でのタグ付けが不要なために効率が向上するだけでなく、大量のデジタルコンテンツ間の一貫性とスケーラビリティも確保できます。

![AI 生成のメタデータ](/help/assets/assets/enhanced-smart-tags.png)

**Figma との統合**

AEM Assets は Figma とネイティブに統合されているので、AEM Assets に保存されているアセットに Figma ユーザーインターフェイスから直接アクセスできます。AEM Assetsで管理されているコンテンツを Figma キャンバスに配置してから、新しいコンテンツや編集したコンテンツをAEM Assets リポジトリに保存することができます。 Figma コミュニティページで利用可能なAEM Assets コネクタにアクセスするには、[ ここ ](https://www.figma.com/community/plugin/1512561378275712210/adobe-experience-manager-aem-assets-connector) をクリックします。

>[!VIDEO](https://video.tv.adobe.com/v/3463828)


### コンテンツハブの新機能 {#new-features-content-hub}

**属性ベースのアクセス制御の概要（ABAC）**

[コンテンツハブで、アセットへのアクセスについてルールベースの制限を適用できるようになりました](/help/assets/attribute-based-access-control.md)。アセット権限を使用すると、ガバナンスが確保され、ユーザーは関連するアセットにのみアクセスできるようになります。

アセット制限ルールはメタデータに基づいており、ルールで定義された条件がアセットメタデータに一致する場合、アセットはユーザーグループに表示されます。

属性ベースのアクセス制御の主なメリットには、次のようなものがあります。

* 権限に対するフォルダー構造への依存が排除される

* 管理者がアセットをアップロードし、遡及的に権限構造を決定できる

* 重複の数を減らす – アセットの整合性を向上させます。同じアセットが異なるグループと共有される場合は、フォルダーベースの権限で重複が必要になります。

**UI ブランディング**

コンテンツハブでは、管理者がプライマリカラーとセカンダリカラーに加え、バナー画像、バナータイトル、本文などの[ブランド固有の要素を使用してユーザーインターフェイスをカスタマイズ](/help/assets/configure-content-hub-ui-options.md##configure-branding-content-hub)できます。これらの機能強化により、ブランドの一貫性の確保、ユーザーのオンボーディングの簡素化、信頼の構築が可能になります。

![UI ブランディング](/help/assets/assets/content-hub-ui-branding.png)

**公開リンクの共有**

コンテンツハブでは、外部のユーザーがアプリケーションにアクセスすることなくアセットのメタデータを表示したり、アセットをダウンロードしたりできるように[共有可能なリンクを生成](/help/assets/share-assets-content-hub.md##share-assets)できるようになりました。

![UI ブランディング](/help/assets/assets/public-and-private-link.png)

**コレクションに関するガバナンス**

コンテンツハブでは、[作成中のコレクションへのアクセスを制御し、許可されたユーザーのみがグループ化されたアセットを表示または管理できるようになりました](/help/assets/collections-content-hub.md##create-collections)。これにより、セキュリティの強化、共同作業の向上、アセットの組織的な管理、ガバナンスの効率化が実現します。

>[!VIDEO](https://video.tv.adobe.com/v/3463336)

>[!NOTE]
>
>コレクションに関するガバナンスは提供が限定される機能です。サポートチケットを作成して、有効にすることができます。

**複数のアセットを ZIP としてダウンロードする**

また、Content Hubではファイル管理を簡単にする個別のファイルとしてではなく、[選択したアセットとそのレンディションを ZIP ファイルでダウンロード](/help/assets/download-assets-content-hub.md#download-asset-renditions) できるようになりました。

**コンテンツハブにおける Dynamic Media のレンディション**

すべての [Dynamic Media プリセットレンディションおよびダウンロード用のスマート切り抜きには、コンテンツハブのユーザーインターフェイス内から直接アクセスできます](/help/assets/download-assets-content-hub.md#download-asset-renditions)。

![Dynamic Media レンディション](/help/assets/assets/dm-renditions-content-hub.png)

### Dynamic Media の新機能 {#new-features-dynamic-media}

**AJO B2C と Dynamic Media のネイティブ統合&#x200B;**

[Experience Manager (AEM) Dynamic Media とJourney Optimizer (AJO) B2C のネイティブ統合](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/content-management/combine/aem-dynamic)により、マーケターは AEM Dynamic Media アセット (レンディションおよび DM テンプレート) を AJO コンテンツに簡単に埋め込んで、チャネル間でのリアルタイムの更新と高度にパーソナライズされたエクスペリエンスを提供できます。

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

Adobe は、パフォーマンス、セキュリティ、価値に関する標準を満たすように、機能、ライブラリ、API および設定を定期的に見直しています。機能がこれらの標準を満たさなくなった場合は廃止とマークされ、指定した削除日までに使用が停止されます。この日付までに、新しいビルドを進めたりデプロイしたりする前に、お客様にメール通知を届けたり、Cloud Managerで実行する必要があるアクションをお知らせしたりします。必要な対策を講じないと、AEM の新しいバージョンにアップグレードできなくなる可能性があり、セキュリティ、パフォーマンス、信頼性、可用性に関する影響が潜在します。

詳しくは、[廃止に関する記事](/help/release-notes/deprecated-removed-features.md)を参照してください。

#### 削除日近くの廃止予定の Java API と OSGi の設定 {#deprecated-near-removals}

以下のリストを展開して、使用できなくなった廃止予定の API と OSGi 設定を確認します。 削除のタイムラインなどの詳細については、廃止に関するの記事を参照してください。

<details>
  <summary>展開して廃止について確認</summary>

Java API
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

* `org.apache.sling.commons.log.LogManager` (すべてのプロパティ)
* `org.apache.sling.commons.log.LogManager.factory.config` (`org.apache.sling.commons.log.file`、`org.apache.sling.commons.log.pattern`)

</details>

### Java 11 ランタイムのデプロイメント {#java11-runtime-deprecation}

**Java 11 ランタイム** は廃止となり、大半の環境はよりパフォーマンスの高い **Java 21 ランタイム**&#x200B;にアップグレードされています。

サポートされていない依存関係が原因で環境をアップグレードできなかった場合 ([Java 21 ランタイム要件](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)を参照) は、次の具体的な手順を記載したメールが Adobeから届いているはずです。**2025 年 8 月 28 日**&#x200B;までに必要な更新がすべて完了していることを確認してください。これにより、中断することなく環境をアップグレードできます。

注：ランタイムバージョンは、コードのビルドバージョンとは別のものです。Java 21 を使用してビルドすることをお勧めしますが、Java 11 ビルドは引き続きサポートされています。Java 11 ビルドの廃止に関する通知は、今後共有される予定です。

### AEM Java ログ設定ポリシーの適用 {#logconfig-policy}

4 月のリリースノートに記載されているように、AEMの Java ログは、すべてのお客様の環境で信頼性の高い監視を確実に行うために、標準に従う必要があります。ログ形式、出力ファイル、デフォルトログレベルの変更といったカスタムログ設定は、サポートされなくなりました。ログはデフォルトファイルにダイレクトされ続け、AEM 製品コードのデフォルトログレベルは保持される必要があります。 詳しくは、[ログに関する記事](/help/implementing/developing/introduction/logging.md#configuration-loggers)を参照してください。

**8 月下旬**&#x200B;から、サポートされていないカスタムログの上書きは無視されるようになります。Adobe の分析によると、ほとんどのお客様は影響を受けることはありません。現在の設定が影響を受ける可能性があるお客様には直接連絡します。

カスタムログ動作に依存するダウンストリームプロセスを確認し、更新してください。例：

* ログ転送システムでカスタムログ形式が想定されている場合は、取り込みルールを調整する必要がある可能性があります。
* 以前にログレベルを変更してログの冗長性を削減したことがある場合は、デフォルトレベルに戻すとログのボリュームが増える可能性があることに注意してください。

### 古いバージョンと監査ログのデフォルトのパージ {#mt-defaults}

現在、コンテンツバージョンと監査ログは、関連付けられた *パージメンテナンスタスク* をデフォルトで無効にしているので、明示的に設定されない限り、データは削除されません。

ただし、リポジトリのパフォーマンスを最適化するために、**2025 年 6 月下旬**&#x200B;から次のガイドラインに従って、デフォルトでパージが有効になります。

#### コンテンツのバージョン {#mt-content}

* **新しい環境** (今後の日付より後に作成) (後で通知)
   * **30 日**&#x200B;より古いバージョンは定期的に削除されます。
   * 作成日に関係なく、最新のバージョンと現在のバージョンと共に過去 30 日間の最新の 5 つのバージョンが保持されます。

* **既存の環境** （この日付より前に作成）:
   * **7 年**&#x200B;より古いバージョンは定期的に削除されます。
   * 過去 7 年間のすべてのバージョンが保持されます。
   * このデフォルトの高いしきい値によって、最近のデータが意図せずに削除されるのを防ぎます。ただし、リポジトリのパフォーマンスを最適化するには、小さい値を設定することをお勧めします。

* 設定パイプラインを使用してデプロイされた YAML 設定を通じて、これらのデフォルトを変更できます。

#### 監査ログ {#mt-auditlogs}

* **新しい環境** （今後作成され、個別に通知されます）：
   * **7 日**&#x200B;より古いレプリケーション、DAM、ページ監査のログは、定期的に削除されます。

   * デフォルトでは、すべてのイベントがログに記録されます。

* **既存の環境** (この予定日より前に作成)：
   * **7 年**&#x200B;より古いレプリケーション、DAM、ページ監査のログは、定期的に削除されます。
   * デフォルトでは、すべてのイベントがログに記録されます。
   * このデフォルトの高いしきい値によって、最近のデータが意図せずに削除されるのを防ぎます。ただし、リポジトリのパフォーマンスを最適化するには、小さい値を設定することをお勧めします。

* 設定パイプラインを使用してデプロイされた YAML 設定を通じて、これらのデフォルトを変更できます。

詳しくは、[メンテナンスタスクに関する記事](/help/operations/maintenance.md#defaults)を参照してください。

### Edge コンピューティング (Alpha プログラム) {#edge-computing}

Edge コンピューティングを使用すると、CDN レイヤーで JavaScript を実行し、データ処理をエンドユーザーに近づけることができます。これにより待ち時間が短縮され、エッジでレスポンシブな動的エクスペリエンスが実現します。

一般的なユースケースを次に示します。

* コンテンツへのアクセスを許可する前に、ID プロバイダーを使用してユーザーを認証する
* 位置情報、デバイスタイプまたはユーザー属性に基づくコンテンツのパーソナライズ
* CDN と接触チャネルの間のミドルウェアとして機能させる
* サードパーティの API からの応答をブラウザーに配信する前に再フォーマットする（および複数の API 応答を集計する）
* 様々なバックエンドからステッチされたコンテンツを使用して、サーバーレンダリングされたHTMLをエッジで作成および提供する

AEM パブリッシュ配信またはライブ実稼動サイトのEdge Delivery Services プロジェクトで利用できる機会の数は限られています。参加に関心がある場合や、詳細を確認したい場合は、ユースケースの簡単な説明を添えて [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)までメールでご連絡ください。

### Edge Delivery Servicesの CDN 設定 (Beta プログラム) {#cdn-eds-beta}

Adobe が管理する CDN では、[設定パイプラインの記事](/help/operations/config-pipeline.md#configurations)で説明されているように、柔軟な設定オプションが提供されます。

Beta 版では、CDN 接触チャネルセレクター、応答、リクエスト変換などの機能に対して設定パイプラインをデプロイします。ユースケースの詳細については、 [aemcs-cdn-config-adopter@adobe.com](mailto:aemcs-cdn-config-adopter@adobe.com) にお問い合わせください。

### その他の宛先への AEM ログ転送 (Beta プログラム) {#log-forwarding-beta}

ログは Cloud Manager からダウンロードできますが、多くの組織では、これらのログを優先されるログの宛先にストリーミングすると役立ちます。AEM では、Azure Blob Storage、Datadog、HTTPS、Elasticsearch (および OpenSearch)、Splunk への AEM および CDN ログ転送をサポートしています。この機能は、セルフサービス方式で設定し、設定パイプラインを使用してデプロイします。

Beta では、Amazon S3、Sumo Logic および独自のNew Relic アカウント (Adobeが提供するアカウントではありません) に AEM ログを転送できます。 AEM ログ (Apache／Dispatcher など) はサポートされていますが、CDN ログはサポートされていません。アクセスについて詳しくは、[aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) までメールで送信してください。

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
