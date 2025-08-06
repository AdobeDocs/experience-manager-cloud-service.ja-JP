---
title: 廃止される機能および削除された機能
description: リリースノート（ [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の非推奨（廃止予定）の機能と削除された機能）。
mini-toc-levels: 1
exl-id: ef082184-4eb7-49c7-8887-03d925e3da6f
feature: Release Information
role: Admin
source-git-commit: fbe20eb0e57be3a6d02d163d92b13be060ac8ba6
workflow-type: tm+mt
source-wordcount: '3193'
ht-degree: 100%

---

# 非推奨（廃止予定）および削除された機能と API {#deprecated-and-removed-features-apis}

>[!CONTEXTUALHELP]
>id="aem_cloud_deprecated_features"
>title="AEM as a Cloud Service の廃止された機能と削除された機能"
>abstract="AEM as a Cloud Service には、クラウドネイティブなデプロイメントモデルがあります。このタブには、クラウドネイティブな機能に置き換えられた機能がハイライト表示されます。"

アドビでは、AEM as a Cloud Service のパフォーマンス、セキュリティ、全体的な価値に関する進化する標準を満たすように、API や設定などの機能を定期的にレビューしています。これらの評価に基づいて、特定の機能が非推奨（廃止予定）としてマークされる場合があります。可能であれば、アドビが適切な代替手段を提供します。

廃止が発表されると、この機能は限られた期間のみ利用可能となり、お客様は指定された削除日までにすべての使用を削除する必要があります。アドビは、スムーズな移行をサポートするために、合理的な通知とガイダンスを提供します。

廃止期間中、アドビでは、メール通知、アクションセンターのアラートまたは Cloud Manager のリマインダーを通じて、機能の使用を停止するために必要なアクションをお客様に通知します。

>[!WARNING]
>
>場合によっては、新しい Cloud Manager ビルドをデプロイする前や AEM as a Cloud Service の最新バージョンにアップグレードする前に、機能の削除が必要になることがあります。

## 非推奨の機能 {#deprecated-features}

以下の表に示す機能は、非推奨として発表されていますが、まだ削除されていません。削除予定日までに機能の使用を中止する必要があります。そうしないと、パフォーマンス、可用性、セキュリティに関連する問題が発生する可能性があります。

| 機能 | 非推奨（廃止予定）の機能 | 代替手段 |
| ------------ | ------------------ | ----------- |
| Sites | [Assets HTTP API でのコンテンツフラグメントのサポート](/help/assets/content-fragments/assets-api-content-fragments.md) | [OpenAPI を使用したコンテンツフラグメント配信](/help/headless/aem-content-fragment-delivery-with-openapi.md)<br>と<br> [コンテンツフラグメントおよびコンテンツフラグメントモデルの管理 OpenAPI](/help/headless/content-fragment-openapis.md) |
| Sites | [PWA 機能](/help/sites-cloud/authoring/sites-console/enable-pwa.md) | なし |
| Sites | [SPA Editor](/help/implementing/developing/hybrid/introduction.md) | AEM でヘッドレスコンテンツの管理に推奨されるエディターは次のとおりです。<br>- ビジュアル編集用の[ユニバーサルエディター](/help/edge/wysiwyg-authoring/authoring.md)。<br>- フォームベース編集用の[コンテンツフラグメントエディター](/help/assets/content-fragments/content-fragments-managing.md)。 |
| [!DNL Sites] | [JavaScript Use API](https://github.com/adobe/htl-spec/blob/master/SPECIFICATION.md#42-javascript-use-api) | [Java Use API](https://experienceleague.adobe.com/ja/docs/experience-manager-htl/content/java-use-api) |
| [!DNL Sites] | **ソーシャルメディアのステータス** のエクスペリエンスフラグメントのプロパティ。 | この機能は間もなく削除される予定です。 |
| Sites | [Experience Cloud 設定自動化](/help/sites-cloud/integrating/adobe-analytics-exc-setup-automation.md) | なし |
| [!DNL Sites] | テンプレートベースのシンプルなコンテンツフラグメント。 | 現在は[モデルベースの構造化コンテンツフラグメント](/help/assets/content-fragments/content-fragments-models.md)。 |
| [!DNL Assets] | 取り込んだ画像を処理する `DAM Asset Update` ワークフロー | 現在は、アセットの取り込みで[アセットマイクロサービス](/help/assets/asset-microservices-overview.md)が使用されています。 |
| [!DNL Assets] | [!DNL Experience Manager] へのアセットの直接アップロード。 [非推奨（廃止予定）のアセットアップロード API](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api) を参照してください。 | [直接バイナリアップロード](/help/assets/add-assets.md)を使用。 技術的な詳細については、[直接アップロード API](/help/assets/developer-reference-material-apis.md#upload-binary) を参照してください。 |
| [!DNL Assets] | [!DNL ImageMagick] などのコマンドラインツールの呼び出しを含め、`DAM Asset Update` ワークフローの[特定のワークフローステップ](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps)はサポートされていません。 | [アセットマイクロサービス](/help/assets/asset-microservices-overview.md)が多くのワークフローの代替機能となります。 カスタム処理の場合は、[後処理ワークフロー](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)を使用します。 |
| [!DNL Assets] | ビデオの FFmpeg トランスコード。 | FFmpeg サムネールの生成には、[アセットマイクロサービス](/help/assets/asset-microservices-overview.md)を使用。 FFmpeg トランスコードの場合は、[Dynamic Media](/help/assets/manage-video-assets.md) を使用。 |
| [!DNL Foundation] | レプリケーションエージェントの「配布」タブのツリーレプリケーション UI（2021年9月30日（PT）以降に削除） | [パブリケーションの管理](/help/operations/replication.md#manage-publication)または[ツリーアクティベーションワークフローステップ](/help/operations/replication.md#tree-activation)のアプローチ。 |
| [!DNL Foundation] | レプリケーションエージェントの管理画面の「配布」タブとレプリケーション API では、10 MB を超えるコンテンツパッケージをレプリケートできません。 | [パブリケーションの管理](/help/operations/replication.md#manage-publication)または[ツリーアクティベーションワークフローステップ](/help/operations/replication.md#tree-activation) |
| [!DNL Foundation] | Adobe Developer Console プロジェクトから生成された資格情報を使用した統合では、サービスアカウント（JWT）資格情報のサポートが段階的に失われます。2024年5月1日（PT）以降、Adobe Developer Console で新しいサービスアカウント（JWT）資格情報を作成できなくなります。既存のサービスアカウント（JWT）資格情報は、2025年1月1日（PT）まで引き続き、設定済みの統合に使用できますが、それ以降は機能しなくなり、お客様は OAuth サーバー間の資格情報に移行する必要があります。[詳細情報](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/security/jwt-credentials-deprecation-in-adobe-developer-console)。 | OAuth サーバー間の資格情報に[移行](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration#migration-overview)します。 |
| [!DNL Foundation] | コンテンツツリーを公開ワークフローと、コンテンツの階層のレプリケーションに使用された関連するコンテンツツリーを公開ワークフローステップ。 | よりパフォーマンスの高い[ツリーアクティベーションワークフローステップ](/help/operations/replication.md#tree-activation)を使用します。 |
| [!DNL Foundation] | YUI を使用した JavaScript クライアントライブラリの圧縮／軽量化。アドビでは、YUI ライブラリを今後更新する予定はありません。 | アドビは、実装を Google Closure Compiler（GCC）に切り替えることをお勧めします。 |

## 削除された機能 {#removed-features}

この節では、削除された機能を一覧表示します。

| 領域 | 機能 | 代替手段 | 削除予定日 |
| ------------ | ------------------ | ----------- | ------------------- |
| ユーザーインターフェイス | クラシック UI が製品ユーザーインターフェイスから削除されました。 いくつかのクラシック UI ダイアログは、リンクチェッカー、バージョンパージ、一部の Cloud Service 設定など、いくつかの機能で使用できます。 今後の[製品アップデート](/help/release-notes/home.md)により、クラシック UI の利用範囲がさらに狭まる可能性があります。 | 標準 UI | 削除済み |
| [!DNL Dynamic Media] | [Dynamic Media Classic](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/sites/administering/integration/scene7#integration) および [Dynamic Media Hybrid モード](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/assets/dynamic/config-dynamic#dynamic)との従来の統合は、[!DNL Experience Manager] as a [!DNL Cloud Service] では使用できません。 | [!DNL Experience Manager] as a [!DNL Cloud Service] に用意されている [Dynamic Media](/help/assets/dynamic-media/dynamic-media.md) を使用します。 | 削除済み |
| [!DNL Sites] | Portal Director とポートレットコンポーネント | これらの機能は [!DNL Experience Manager] 6.4 で非推奨（廃止予定）となり、現在は [!DNL Experience Manager] から削除されています。 | 削除済み |
| [!DNL Sites] | デザインインポーター | 実行時に [!DNL Experience Manager] リポジトリーの不変セクションにアクセスできないので、この機能は削除されました。 | 削除済み |
| [!DNL Assets] | Assets コアサービスおよび Creative Cloud サービスとの [!DNL Assets] 共有は使用できません。 | [!DNL Adobe Creative Cloud] との統合には、[Adobe Asset Link](https://helpx.adobe.com/jp/enterprise/using/adobe-asset-link.html) を使用します。 | 削除済み |
| [!DNL Foundation] | Apache Sling データソースのサポート（OSGi バンドル org.apache.sling.datasource） | 該当なし | 削除済み |
| [!DNL Foundation] | JST スクリプティングテンプレートのサポート（OSGi バンドル org.apache.sling.scripting.jst） | 該当なし | 削除済み |
| [!DNL Foundation] | Apache Felix Http Whiteboard のサポート | OSGi Http Whiteboard | 2022年3月 |
| [!DNL Foundation] | com.adobe.granite.oauth.server のサポート | Adobe IMS 統合 | 2023年3月 |
| [!DNL Foundation] | [サービスユーザー ID を取得](https://sling.apache.org/apidocs/sling12/org/apache/sling/serviceusermapping/ServiceUserMapper.html#getServiceUserID-org.osgi.framework.Bundle-java.lang.String-)するための org.apache.sling.serviceusermapping 機能のサポート | 該当なし | 2024年8月30日（PT） |
| [!DNL Foundation] | Java 11 ランタイムは非推奨となり、アドビにより Java 21 ランタイムに置き換えられました。コードを Java 11 でビルドすることは引き続き可能です（Java 17 と 21 も選択肢） | Java 21 ランタイムが適用されます。互換性を確保するには、[ランタイム要件](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)の説明に従って、ライブラリバージョンをアップデートすることが重要です。 | 2025/5/29 |

## 非推奨（廃止予定）の API {#aem-apis}

以下の表の API（クリックして展開して確認）は、非推奨と発表されましたが、まだ削除されていません。削除予定日までにこれらの API の使用を中止する必要があります。そうしないと、パフォーマンス、可用性、セキュリティに関連する問題が発生する可能性があります。一部の API では、以下の API 削除ガイダンスの節が参照されています。

<details>
  <summary>展開して、非推奨（廃止予定）の API のリストを確認します。</summary>
<table style="table-layout:auto">
  <tr>
    <th>パッケージ／クラス</th>
    <th>コメント</th>
    <th>廃止日</th>
    <th>削除予定日</th>
  </tr>
<tbody>
  <tr>
    <td>org.apache.sling.commons.auth<br>org.apache.sling.commons.auth.spi</td>
    <td>代替として、Sling の Auth Core／Auth Core SPI インターフェイスを使用します。<a href="#org.apache.sling.commons.auth">以下の削除に関するメモを参照してください。</a></td>
    <td>2015</td>
    <td>2025/8/31</td>
  </tr>
  <tr>
<td>org.eclipse.jetty.client<br>org.eclipse.jetty.client.api<br>org.eclipse.jetty.client.http<br>org.eclipse.jetty.client.util<br>org.eclipse.jetty.http<br>org.eclipse.jetty.http.pathmap<br>org.eclipse.jetty.io<br>org.eclipse.jetty.io.ssl<br>org.eclipse.jetty.security<br>org.eclipse.jetty.server<br>org.eclipse.jetty.server.handler<br>org.eclipse.jetty.server.handler.gzip<br>org.eclipse.jetty.server.session<br>org.eclipse.jetty.servlet<br>org.eclipse.jetty.servlet.listener<br>org.eclipse.jetty.util<br>org.eclipse.jetty.util.annotation<br>org.eclipse.jetty.util.component<br>org.eclipse.jetty.util.log<br>org.eclipse.jetty.util.resource<br>org.eclipse.jetty.util.security<br>org.eclipse.jetty.util.ssl<br>org.eclipse.jetty.util.statistic<br>org.eclipse.jetty.util.thread</td>
    <td>Eclipse Jetty パッケージと Felix Http Jetty パッケージはサポートされなくなりました。 <a href="#org.eclipse.jetty">以下の削除に関するメモを参照してください。</a></td>
    <td>2021/5/27</td>
    <td>2025/8/31</td>
  </tr>
 <tr>     <td>com.mongodb<br>com.mongodb.annotations<br>com.mongodb.assertions<br>com.mongodb.async<br>com.mongodb.binding<br>com.mongodb.bulk<br>com.mongodb.client<br>com.mongodb.client.gridfs<br>com.mongodb.client.gridfs.codecs<br>com.mongodb.client.gridfs.model<br>com.mongodb.client.jndi<br>com.mongodb.client.model<br>com.mongodb.client.model.changestream<br>com.mongodb.client.model.geojson<br>com.mongodb.client.model.geojson.codecs<br>com.mongodb.client.result<br>com.mongodb.connection<br>com.mongodb.connection.netty<br>com.mongodb.diagnostics.logging<br>com.mongodb.event<br>com.mongodb.gridfs<br>com.mongodb.internal<br>com.mongodb.internal.async<br>com.mongodb.internal.authentication<br>com.mongodb.internal.connection<br>com.mongodb.internal.dns<br>com.mongodb.internal.event<br>com.mongodb.internal.management.jmx<br>com.mongodb.internal.session<br>com.mongodb.internal.thread<br>com.mongodb.internal.validator<br>com.mongodb.management<br>com.mongodb.operation<br>com.mongodb.selector<br>com.mongodb.session<br>com.mongodb.util</td>
    <td>この API の使用は、AEM as a Cloud Service ではサポートされていません。 <a href="#com.mongodb">以下の削除に関するメモを参照してください。</a></td>
    <td>2021/5/27</td>
    <td>2025/8/31</td>
  </tr>
   <tr>
    <td>org.apache.abdera<br>org.apache.abdera.model<br>org.apache.abdera.factory<br>org.apache.abdera.ext.media<br>org.apache.abdera.util<br>org.apache.abdera.i18n.iri<br>org.apache.abdera.writer<br>org.apache.abdera.i18n.rfc4646<br>org.apache.abdera.i18n.rfc4646.enums<br>org.apache.abdera.i18n.text<br>org.apache.abdera.filter<br>org.apache.abdera.xpath<br>org.apache.abdera.i18n.text.io<br>org.apache.abdera.i18n.text.data<br>org.apache.abdera.parser</td>
    <td>Apache Abdera が 2017年以降廃止されたプロジェクトなので、この API は廃止されました。 <a href="#org.apache.abdera_or_org.apache.sling.atom.taglib">以下の削除に関するメモを参照してください。</a></td>
    <td>2021/7/29</td>
    <td>2025/8/31</td>
  </tr>
  <tr>
    <td>org.apache.abdera.ext.opensearch<br>org.apache.abdera.ext.opensearch.model<br>org.apache.abdera.ext.opensearch.server<br>org.apache.abdera.ext.opensearch.server.impl<br>org.apache.abdera.ext.opensearch.server.processors<br>org.apache.abdera.i18n.iri.data<br>org.apache.abdera.i18n.lang<br>org.apache.abdera.i18n.templates<br>org.apache.abdera.i18n.unicode.data<br>org.apache.abdera.parser.stax<br>org.apache.abdera.parser.stax.util<br>org.apache.abdera.protocol<br>org.apache.abdera.protocol.client<br>org.apache.abdera.protocol.client.cache<br>org.apache.abdera.protocol.client.util<br>org.apache.abdera.protocol.error<br>org.apache.abdera.protocol.server<br>org.apache.abdera.protocol.server.context<br>org.apache.abdera.protocol.server.filters<br>org.apache.abdera.protocol.server.impl<br>org.apache.abdera.protocol.server.multipart<br>org.apache.abdera.protocol.server.processors<br>org.apache.abdera.protocol.server.provider.basic<br>org.apache.abdera.protocol.server.provider.managed<br>org.apache.abdera.protocol.server.servlet<br>org.apache.abdera.protocol.util<br>org.apache.abdera.util.filter</td>
    <td>Apache Abdera が 2017年以降廃止されたプロジェクトなので、この API は廃止されました。 <a href="#org.apache.abdera_or_org.apache.sling.atom.taglib">以下の削除に関するメモを参照してください。</a></td>
    <td>2019/4/8</td>
    <td>2025/8/31</td>
  </tr>
  <tr>
    <td>org.apache.felix.http.whiteboard</td>
    <td>Apache Felix Http ホワイトボードはサポートされなくなりました。 コードを OSGi Http ホワイトボードに移行します。 <a href="#org.apache.felix.http.whiteboard">以下の削除に関するメモを参照してください。</a></td>
    <td>2022年1月27日（PT）</td>
    <td>2025/8/31</td>
  </tr>
  <tr>
    <td>org.apache.cocoon.xml.dom<br>org.apache.cocoon.xml.sax</td>
    <td>この API は非推奨（廃止予定）です。JDK が提供する XML API にコードを移行してください。</td>
    <td>2022年1月27日（PT）</td>
    <td>2025/8/31</td>
  </tr>
  <tr>
    <td>ch.qos.logback.classic<br>ch.qos.logback.classic.boolex<br>ch.qos.logback.classic.db.names<br>ch.qos.logback.classic.db.script<br>ch.qos.logback.classic.encoder<br>ch.qos.logback.classic.filter<br>ch.qos.logback.classic.helpers<br>ch.qos.logback.classic.html<br>ch.qos.logback.classic.jmx<br>ch.qos.logback.classic.joran<br>ch.qos.logback.classic.joran.action<br>ch.qos.logback.classic.jul<br>ch.qos.logback.classic.layout<br>ch.qos.logback.classic.log4j<br>ch.qos.logback.classic.net<br>ch.qos.logback.classic.net.server<br>ch.qos.logback.classic.pattern<br>ch.qos.logback.classic.pattern.color<br>ch.qos.logback.classic.selector<br>ch.qos.logback.classic.selector.servlet<br>ch.qos.logback.classic.servlet<br>ch.qos.logback.classic.sift<br>ch.qos.logback.classic.spi<br>ch.qos.logback.classic.turbo<br>ch.qos.logback.classic.util<br>ch.qos.logback.core<br>ch.qos.logback.core.boolex<br>ch.qos.logback.core.encoder<br>ch.qos.logback.core.filter<br>ch.qos.logback.core.helpers<br>ch.qos.logback.core.hook<br>ch.qos.logback.core.html<br>ch.qos.logback.core.joran<br>ch.qos.logback.core.joran.action<br>ch.qos.logback.core.joran.conditional<br>ch.qos.logback.core.joran.event<br>ch.qos.logback.core.joran.event.stax<br>ch.qos.logback.core.joran.node<br>ch.qos.logback.core.joran.spi<br>ch.qos.logback.core.joran.util<br>ch.qos.logback.core.joran.util.beans<br>ch.qos.logback.core.layout<br>ch.qos.logback.core.net<br>ch.qos.logback.core.net.server<br>ch.qos.logback.core.net.ssl<br>ch.qos.logback.core.pattern<br>ch.qos.logback.core.pattern.color<br>ch.qos.logback.core.pattern.parser<br>ch.qos.logback.core.pattern.util<br>ch.qos.logback.core.property<br>ch.qos.logback.core.read<br>ch.qos.logback.core.recovery<br>ch.qos.logback.core.rolling<br>ch.qos.logback.core.rolling.helper<br>ch.qos.logback.core.sift<br>ch.qos.logback.core.spi<br>ch.qos.logback.core.status<br>ch.qos.logback.core.subst<br>ch.qos.logback.core.util</td>
    <td>AEM as a Cloud Service は、この内部ログバック API をサポートしていません。<a href="#ch.qos.logback">以下の削除に関するメモを参照してください。</a></td>
    <td>2022年1月27日（PT）</td>
    <td>2025/8/31</td>
  </tr>
  <tr>
    <td>org.slf4j.spi</td>
    <td>AEM as a Cloud Service は、この内部 log4j API をサポートしていません。<a href="#org.slf4j">以下の削除に関するメモを参照してください。</a></td>
    <td>2022年1月27日（PT）</td>
    <td>2025/8/31</td>
  </tr>
  <tr>
    <td>org.apache.log4j<br>org.apache.log4j.helpers<br>org.apache.log4j.spi<br>org.apache.log4j.xml</td>
    <td>Apache Log4j 1 は 2015年に提供が終了し、サポートは終了しました。<a href="#org.apache.log4j">以下の削除に関するメモを参照してください。</a></td>
    <td>2022年1月27日（PT）</td>
    <td>2025/8/31</td>
  </tr>
  <tr>  <td>com.google.common.annotations<br>com.google.common.base<br>com.google.common.cache<br>com.google.common.collect<br>com.google.common.escape<br>com.google.common.eventbus<br>com.google.common.hash<br>com.google.common.html<br>com.google.common.io<br>com.google.common.math<br>com.google.common.net<br>com.google.common.primitives<br>com.google.common.reflect<br>com.google.common.util.concurrent<br>com.google.common.xml</td>
    <td>Google Guava コアライブラリは Cloud Service で廃止されました。<a href="#com.google.common">以下の削除に関するメモを参照してください。</a></td>
    <td>2023/5/15</td>
    <td>2025/8/31</td>
  </tr>
  <tr>
    <td>org.slf4j.event</td>
    <td>AEM as a Cloud Service は、この内部 slf4j API をサポートしていません。<a href="#org.slf4j">以下の削除に関するメモを参照してください。</a></td>
    <td>2022/4/11</td>
    <td>2025/8/31</td>
  </tr> 
    <tr>
    <td>com.drew.*</td>
    <td>画像やビデオからのメタデータの抽出には、Cloud Service の Asset Compute、Apache POI または Apache Tika を使用する必要があります。</td>
    <td>2024年9月17日（PT）</td>
    <td>2025/8/31</td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.oak.plugins.blob.*</td>
    <td>この API は内部でのみ使用されます。</td>
    <td>2024/9/23</td>
    <td>2025/8/31</td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.oak.plugins.memory</td>
    <td>この API は内部でのみ使用されます。</td>
    <td>2024/9/23</td>
    <td>2025/8/31</td>
  </tr>
  <tr>
<td>org.apache.felix.webconsole<br>org.apache.felix.webconsole.bundleinfo<br>org.apache.felix.webconsole.i18n<br>org.apache.felix.webconsole.spi</td>
    <td>Felix web コンソールはクラウド環境ではサポートされていません。<a href="#org.apache.felix.webconsole">以下の削除に関するメモを参照してください。</a></td>
    <td>2021/4/30</td>
    <td>2025/8/31</td>
  </tr>
<td>org.bson<br/>org.bson.assertions<br/>org.bson.codecs<br/>org.bson.codecs.configuration<br/>org.bson.codecs.pojo<br/>org.bson.codecs.pojo.annotations<br/>org.bson.conversions<br/>org.bson.diagnostics<br/>org.bson.internal<br/>org.bson.io<br/>org.bson.json<br/>org.bson.types<br/>org.bson.util</td>
    <td>この API の使用は、AEM as a Cloud Service ではサポートされていません。</td>
    <td>2022/10/31</td>
    <td>2025/8/31</td>
  </tr>  
  <tr>
    <td>org.apache.sling.runmode</td>
    <td></td>
    <td>2015</td>
    <td>未定</td>
  </tr>
  <tr>
    <td>org.json</td>
    <td><a href="https://johnzon.apache.org/index.html">javax.json</a> の Apache Johnzon 実装の使用をお勧めします。 </td>
    <td>2021/4/30</td>
    <td>未定</td>
  </tr>
  <tr>
<td>org.apache.commons.lang<br>org.apache.commons.lang.enums<br>org.apache.commons.lang.builder<br>org.apache.commons.lang.exception<br>org.apache.commons.lang.math<br>org.apache.commons.lang.mutable<br>org.apache.commons.lang.reflect<br>org.apache.commons.lang.text<br>org.apache.commons.lang.time</td>
    <td>Commons Lang 2 はメンテナンスモードになっています。 Commons Lang 3 を代わりに使用してください。<a href="#apache.commons">以下の削除に関するメモを参照してください。</a></td>
    <td>2021/4/30</td>
    <td>未定</td>
  </tr>
  <tr>
    <td>org.apache.commons.collections<br>org.apache.commons.collections.bag<br>org.apache.commons.collections.bidimap<br>org.apache.commons.collections.buffer<br>org.apache.commons.collections.collection<br>org.apache.commons.collections.comparators<br>org.apache.commons.collections.functors<br>org.apache.commons.collections.iterators<br>org.apache.commons.collections.keyvalue<br>org.apache.commons.collections.list<br>org.apache.commons.collections.map<br>org.apache.commons.collections.set</td>
    <td>Commons Collections 3 はメンテナンスモードになっています。 Commons Collections 4 を代わりに使用してください。<a href="#apache.commons">以下の削除に関するメモを参照してください。</a></td>
    <td>2021/4/30</td>
    <td>未定</td>
  </tr>
  <tr>
    <td>com.day.cq.contentsync.handler.util</td>
    <td>この API は非推奨（廃止予定）です。代わりに、Apache Sling のビルダーを使用します。</td>
    <td>2022/10/31</td>
    <td>未定</td>
  </tr>
  <tr><td>org.apache.sling.commons.json<br>org.apache.sling.commons.json.http<br>org.apache.sling.commons.json.io<br>org.apache.sling.commons.json.jcr<br>org.apache.sling.commons.json.sling<br>org.apache.sling.commons.json.util<br>org.apache.sling.commons.json.xml</td>
    <td>AEM as a Cloud Service は、この API をサポートしていません。</td>
    <td>2023/5/15</td>
    <td>未定</td>
  </tr>
  <tr>
    <td>com.day.cq.xss<br>com.day.cq.xss.taglib<br>com.day.cq.xss.impl</td>
    <td>代わりに、org.apache.sling.xss を使用します。</td>
    <td>2023年12月12日（PT）</td>
    <td>未定</td>
  </tr>
  <tr>
    <td>com.adobe.granite.xss<br>com.adobe.granite.xss.impl</td>
    <td>代わりに、org.apache.sling.xss を使用します。</td>
    <td>2023年12月12日（PT）</td>
    <td>未定</td>
  </tr>
  </tbody>
</table>
</details>

## 削除された API {#removed-apis}

この節では、非推奨および削除された API を一覧表示します。一部の API では、以下の API 削除ガイダンスの節が参照されています。

<details>
  <summary>展開して、削除された API のリストを表示します。</summary>
<table style="table-layout:auto">
  <tr>
    <th>パッケージ／クラス</th>
    <th>コメント</th>
  </tr>
<tbody>
  <tr>
    <td>com.day.cq.jcrclustersupport</td>
    <td>Sling の Discovery API を代わりに使用してください。</td>
  </tr>
  <tr>
    <td>org.apache.fop.apps</td>
    <td></td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.vault.util.xml.xerces.dom<br>org.apache.jackrabbit.vault.util.xml.xerces.util<br>org.apache.jackrabbit.vault.util.xml.xerces.xni<br>org.apache.jackrabbit.vault.util.xml.xerces.xni.parser</td>
    <td></td>
  </tr>
  <tr>
    <td>org.apache.felix.cm<br>org.apache.felix.cm.file</td>
    <td>AEM as a Cloud Service では、カスタム永続性マネージャーはサポートされていません。</td>
  </tr>
  <tr>
    <td>org.apache.felix.systemready</td>
    <td>Apache Felix HealthCheck API を代わりに使用することをお勧めします。</td>
  </tr>
  <tr> <td>org.apache.felix.http.jetty<br>org.eclipse.jetty.client.jmx<br>org.eclipse.jetty.jmx<br>org.eclipse.jetty.server.handler.jmx<br>org.eclipse.jetty.server.nio<br>org.eclipse.jetty.server.jmx<br>org.eclipse.jetty.servlet.jmx<br>org.eclipse.jetty.util.preventers<br>org.eclipse.jetty.util.thread.strategy<br>org.eclipse.jetty.webapp<br>org.eclipse.jetty.websocket.api<br>org.eclipse.jetty.websocket.api.annotations<br>org.eclipse.jetty.websocket.api.extensions<br>org.eclipse.jetty.websocket.api.util<br>org.eclipse.jetty.websocket.client<br>org.eclipse.jetty.websocket.client.io<br>org.eclipse.jetty.websocket.client.masks<br>org.eclipse.jetty.websocket.common<br>org.eclipse.jetty.websocket.common.events<br>org.eclipse.jetty.websocket.common.events.annotated<br>org.eclipse.jetty.websocket.common.extensions<br>org.eclipse.jetty.websocket.common.extensions.compress<br>org.eclipse.jetty.websocket.common.extensions.fragment<br>org.eclipse.jetty.websocket.common.extensions.identity<br>org.eclipse.jetty.websocket.common.frames<br>org.eclipse.jetty.websocket.common.io<br>org.eclipse.jetty.websocket.common.io.http<br>org.eclipse.jetty.websocket.common.io.payload<br>org.eclipse.jetty.websocket.common.message<br>org.eclipse.jetty.websocket.common.scopes<br>org.eclipse.jetty.websocket.common.util<br>org.eclipse.jetty.websocket.server<br>org.eclipse.jetty.websocket.server.pathmap<br>org.eclipse.jetty.websocket.servlet<br>org.eclipse.jetty.xml</td>
    <td>Eclipse Jetty パッケージと Felix Http Jetty パッケージはサポートされなくなりました。</td>
  </tr>
  <tr>
    <td>org.apache.felix.metatype<br>org.apache.felix.scr<br>org.apache.felix.scr.info<br>org.apache.felix.scr.component</td>
    <td>Apache Felix メタタイプと SCR API は非推奨（廃止予定）です。  OSGi メタタイプおよび Declarative Service API を代わりに使用してください。</td>
  </tr>
  <tr>
    <td>org.slf4j.impl</td>
    <td>ログ実装クラスは、AEM as a Cloud Service と互換性がありません。</td>
  </tr>
  <tr>
    <td>org.apache.sling.startupfilter<br>com.adobe.granite.crypto.spi<br>com.adobe.granite.crpyto.spi.base<br>com.adobe.agl.impl.data.icudt40b<br>com.adobe.agl.impl.data.icudt40b.brkitr<br>com.adobe.agl.impl.data.icudt40b.coll<br>com.adobe.agl.impl.data.icudt40b.rbnf<br>com.<br>adobe.agl.impl.data.icudt40b.translit<br>com.adobe.internal.pdf.tika<br>com.adobe.internal.pdftoolkit.color<br>com.adobe.internal.pdftoolkit.core.encryption<br>com.adobe.internal.pdftoolkit.core.encryption.impl<br>com.adobe.internal.pdftoolkit.core.traverser<br>com.adobe.internal.pdftoolkit.graphicsDOM<br>com.adobe.internal.pdftoolkit.graphicsDOM.shading<br>com.adobe.internal.pdftoolkit.graphicsDOM.utils<br>com.adobe.internal.pdftoolkit.image<br>com.adobe.internal.pdftoolkit.pdf.content<br>com.adobe.internal.pdftoolkit.pdf.content.processor<br>com.adobe.internal.pdftoolkit.pdf.content.processor.base14fontwidths<br>com.adobe.internal.pdftoolkit.pdf.contentmodify<br>com.adobe.internal.pdftoolkit.pdf.contentmodify.impl<br>com.adobe.internal.pdftoolkit.pdf.digsig<br>com.adobe.internal.pdftoolkit.pdf.document<br>com.adobe.internal.pdftoolkit.pdf.document.listener<br>com.adobe.internal.pdftoolkit.pdf.document.permissionhandlers<br>com.adobe.internal.pdftoolkit.pdf.filters<br>com.adobe.internal.pdftoolkit.pdf.graphics<br>com.adobe.internal.pdftoolkit.pdf.graphics.colorspaces<br>com.adobe.internal.pdftoolkit.pdf.graphics.colorspaces.cmykresources<br>com.adobe.internal.pdftoolkit.pdf.graphics.font<br>com.adobe.internal.pdftoolkit.pdf.graphics.font.encodings<br>com.adobe.internal.pdftoolkit.pdf.graphics.font.impl<br>com.adobe.internal.pdftoolkit.pdf.graphics.impl<br>com.adobe.internal.pdftoolkit.pdf.graphics.optionalcontent<br>com.adobe.internal.pdftoolkit.pdf.graphics.patterns<br>com.adobe.internal.pdftoolkit.pdf.graphics.shading<br>com.adobe.internal.pdftoolkit.pdf.graphics.xobject<br>com.adobe.internal.pdftoolkit.pdf.impl<br>com.adobe.internal.pdftoolkit.pdf.inlineimage<br>com.adobe.internal.pdftoolkit.pdf.interactive<br>com.adobe.internal.pdftoolkit.pdf.interactive.action<br>com.adobe.internal.pdftoolkit.pdf.interactive.annotation<br>com.adobe.internal.pdftoolkit.pdf.interactive.forms<br>com.adobe.internal.pdftoolkit.pdf.interactive.forms.impl<br>com.adobe.internal.pdftoolkit.pdf.interactive.geospatial<br>com.adobe.internal.pdftoolkit.pdf.interactive.markedcontent<br>com.adobe.internal.pdftoolkit.pdf.interactive.navigation<br>com.adobe.internal.pdftoolkit.pdf.interactive.navigation.collection<br>com.adobe.internal.pdftoolkit.pdf.interactive.readerrequirements<br>com.adobe.internal.pdftoolkit.pdf.interactive.requirement<br>com.adobe.internal.pdftoolkit.pdf.interchange<br>com.adobe.internal.pdftoolkit.pdf.interchange.documentparts<br>com.adobe.internal.pdftoolkit.pdf.interchange.metadata<br>com.adobe.internal.pdftoolkit.pdf.interchange.prepress<br>com.adobe.internal.pdftoolkit.pdf.interchange.structure<br>com.adobe.internal.pdftoolkit.pdf.multimedia<br>com.adobe.internal.pdftoolkit.pdf.page<br>com.adobe.internal.pdftoolkit.pdf.rendering<br>com.adobe.internal.pdftoolkit.pdf.transparency<br>com.adobe.internal.pdftoolkit.pdf.utils<br>com.adobe.internal.pdftoolkit.services.Jpeg2000<br>com.adobe.internal.pdftoolkit.services.fontresources<br>com.adobe.internal.pdftoolkit.services.fontresources.subsetting<br>com.adobe.internal.pdftoolkit.services.interchange.structure<br>com.adobe.internal.pdftoolkit.services.optionalcontent<br>com.adobe.internal.pdftoolkit.services.optionalcontent.impl<br>com.adobe.internal.pdftoolkit.services.pdfParser<br>com.adobe.internal.pdftoolkit.services.permissions<br>com.adobe.internal.pdftoolkit.services.rasterizer<br>com.adobe.internal.pdftoolkit.services.readingorder<br>com.adobe.internal.pdftoolkit.services.security<br>com.adobe.internal.pdftoolkit.services.swf<br>com.adobe.internal.pdftoolkit.services.textextraction<br>com.adobe.internal.pdftoolkit.services.textextraction.impl<br>com.adobe.internal.pdftoolkit.services.xmp<br>com.adobe.internal.util.base64<br>com.adobe.internal.xmp.utils<br>com.day.crx.core.cluster<br>com.day.crx.packaging<br>com.day.crx.packaging.gfx<br>com.day.crx.query<br>com.day.crx.sling.server.jmx<br>com.day.durbo<br>com.day.durbo.io<br>com.day.imageio.plugins<br>org.apache.aries.jmx.codec<br>org.h2.mvstore<br>org.h2.mvstore.rtree<br>org.h2.mvstore.type<br>org.openxmlformats.schemas.drawingml.x2006.chart.impl<br>org.openxmlformats.schemas.drawingml.x2006.main.impl<br>org.openxmlformats.schemas.drawingml.x2006.picture.impl<br>org.openxmlformats.schemas.drawingml.x2006.spreadsheetDrawing.impl<br>org.openxmlformats.schemas.drawingml.x2006.wordprocessingDrawing.impl<br>org.openxmlformats.schemas.officeDocument.x2006.customProperties.impl<br>org.openxmlformats.schemas.officeDocument.x2006.docPropsVTypes.impl<br>org.openxmlformats.schemas.officeDocument.x2006.extendedProperties.impl<br>org.openxmlformats.schemas.officeDocument.x2006.relationships.impl<br>org.openxmlformats.schemas.presentationml.x2006.main.impl<br>org.openxmlformats.schemas.spreadsheetml.x2006.main.impl<br>org.openxmlformats.schemas.wordprocessingml.x2006.main.impl<br>org.openxmlformats.schemas.xpackage.x2006.contentTypes<br>org.openxmlformats.schemas.xpackage.x2006.contentTypes.impl<br>org.openxmlformats.schemas.xpackage.x2006.digitalSignature<br>org.openxmlformats.schemas.xpackage.x2006.digitalSignature.impl<br>org.openxmlformats.schemas.xpackage.x2006.metadata.coreProperties<br>org.openxmlformats.schemas.xpackage.x2006.metadata.coreProperties.impl<br>org.openxmlformats.schemas.xpackage.x2006.relationships<br>org.openxmlformats.schemas.xpackage.x2006.relationships.impl<br>com.adobe.internal.afml<br>com.adobe.internal.agm<br>com.adobe.internal.pdftoolkit.legacy.services.ap.es2<br>com.adobe.internal.pdftoolkit.legacy.services.ap.es3<br>com.adobe.internal.pdftoolkit.pdf.pieceinfo.compoundtype<br>com.adobe.internal.pdftoolkit.pdf.pieceinfo.editablepdf<br>com.adobe.internal.pdftoolkit.services.ap<br>com.adobe.internal.pdftoolkit.services.ap.annot<br>com.adobe.internal.pdftoolkit.services.ap.extension<br>com.adobe.internal.pdftoolkit.services.ap.impl<br>com.adobe.internal.pdftoolkit.services.ap.spi<br>com.adobe.internal.pdftoolkit.services.digsig<br>com.adobe.internal.pdftoolkit.services.digsig.cryptoprovider<br>com.adobe.internal.pdftoolkit.services.digsig.docmodanalysis<br>com.adobe.internal.pdftoolkit.services.digsig.spi<br>com.adobe.internal.pdftoolkit.services.fdf<br>com.adobe.internal.pdftoolkit.services.formflattener<br>com.adobe.internal.pdftoolkit.services.forms<br>com.adobe.internal.pdftoolkit.services.imageconversion<br>com.adobe.internal.pdftoolkit.services.javascript<br>com.adobe.internal.pdftoolkit.services.javascript.extension<br>com.adobe.internal.pdftoolkit.services.manipulations<br>com.adobe.internal.pdftoolkit.services.manipulations.impl<br>com.adobe.internal.pdftoolkit.services.optimizer<br>com.adobe.internal.pdftoolkit.services.pdfa<br>com.adobe.internal.pdftoolkit.services.pdfa.error<br>com.adobe.internal.pdftoolkit.services.pdfa2<br>com.adobe.internal.pdftoolkit.services.pdfa2.error<br>com.adobe.internal.pdftoolkit.services.pdfa2.error.codes<br>com.adobe.internal.pdftoolkit.services.pdfa3<br>com.adobe.internal.pdftoolkit.services.pdfport<br>com.adobe.internal.pdftoolkit.services.portfolio<br>com.adobe.internal.pdftoolkit.services.rcg<br>com.adobe.internal.pdftoolkit.services.rcg.impl<br>com.adobe.internal.pdftoolkit.services.redaction<br>com.adobe.internal.pdftoolkit.services.redaction.handler<br>com.adobe.internal.pdftoolkit.services.sanitization<br>com.adobe.internal.pdftoolkit.services.xbm<br>com.adobe.internal.pdftoolkit.services.xdp<br>com.adobe.internal.pdftoolkit.services.xfa<br>com.adobe.internal.pdftoolkit.services.xfa.form<br>com.adobe.internal.pdftoolkit.services.xfatext<br>com.adobe.internal.pdftoolkit.services.xfdf<br>com.adobe.internal.pdftoolkit.services.xobjhandler<br>com.adobe.internal.pdftoolkit.xml<br>com.adobe.octopus.extract<br>opennlp.tools.doccat<br>opennlp.tools.entitylinker<br>opennlp.tools.formats<br>opennlp.tools.formats.ad<br>opennlp.tools.formats.brat<br>opennlp.tools.formats.convert<br>opennlp.tools.formats.frenchtreebank<br>opennlp.tools.formats.muc<br>opennlp.tools.formats.ontonotes<br>opennlp.tools.lemmatizer<br>opennlp.tools.parser<br>opennlp.tools.parser.chunking<br>opennlp.tools.parser.lang.en<br>opennlp.tools.parser.lang.es<br>opennlp.tools.parser.treeinsert<br>opennlp.tools.sentdetect<br>opennlp.tools.sentdetect.lang<br>opennlp.tools.sentdetect.lang.th<br>opennlp.tools.stemmer<br>opennlp.tools.stemmer.snowball<br>opennlp.tools.tokenize.lang.en<br>org.apache.commons.imaging.color<br>org.apache.commons.imaging.common<br>org.apache.commons.imaging.common.itu_t4<br>org.apache.commons.imaging.common.mylzw<br>org.apache.commons.imaging.formats.bmp<br>org.apache.commons.imaging.formats.dcx<br>org.apache.commons.imaging.formats.gif<br>org.apache.commons.imaging.formats.icns<br>org.apache.commons.imaging.formats.ico<br>org.apache.commons.imaging.formats.jpeg<br>org.apache.commons.imaging.formats.jpeg.decoder<br>org.apache.commons.imaging.formats.jpeg.exif<br>org.apache.commons.imaging.formats.jpeg.iptc<br>org.apache.commons.imaging.formats.jpeg.segments<br>org.apache.commons.imaging.formats.jpeg.xmp<br>org.apache.commons.imaging.formats.pcx<br>org.apache.commons.imaging.formats.png<br>org.apache.commons.imaging.formats.png.chunks<br>org.apache.commons.imaging.formats.png.scanlinefilters<br>org.apache.commons.imaging.formats.png.transparencyfilters<br>org.apache.commons.imaging.formats.pnm<br>org.apache.commons.imaging.formats.psd<br>org.apache.commons.imaging.formats.psd.dataparsers<br>org.apache.commons.imaging.formats.psd.datareaders<br>org.apache.commons.imaging.formats.rgbe<br>org.apache.commons.imaging.formats.tiff<br>org.apache.commons.imaging.formats.tiff.constants<br>org.apache.commons.imaging.formats.tiff.datareaders<br>org.apache.commons.imaging.formats.tiff.fieldtypes<br>org.apache.commons.imaging.formats.tiff.photometricinterpreters<br>org.apache.commons.imaging.formats.tiff.taginfos<br>org.apache.commons.imaging.formats.tiff.write<br>org.apache.commons.imaging.formats.wbmp<br>org.apache.commons.imaging.formats.xbm<br>org.apache.commons.imaging.formats.xpm<br>org.apache.commons.imaging.icc<br>org.apache.commons.imaging.palette<br>org.apache.commons.imaging.util<br>com.adobe.dam.print.ids.utils<br>com.day.cq.dam.api.reporting<br>com.day.cq.dam.entitlement.api<br>com.day.cq.dam.handler.standard.epub<br>com.day.cq.dam.handler.standard.keynote<br>com.day.cq.dam.handler.standard.mp3<br>com.day.cq.dam.handler.standard.msoffice<br>com.day.cq.dam.handler.standard.msoffice.wmf<br>com.day.cq.dam.handler.standard.ooxml<br>com.day.cq.dam.handler.standard.pdf<br>com.day.cq.dam.handler.standard.pict<br>com.day.cq.dam.handler.standard.ps<br>com.day.cq.dam.handler.standard.psd<br>com.day.cq.dam.handler.standard.zip<br>com.day.cq.dam.word.extraction<br>com.day.cq.dam.word.process<br>com.adobe.xmp.worker.files<br>com.adobe.cq.address.api<br>com.adobe.cq.address.api.location<br>com.day.cq.mcm.emailprovider.impl.types<br>com.day.io<br>com.day.io.disk<br>com.day.io.file<br>org.apache.commons.exec.environment<br>org.apache.commons.exec.launcher<br>org.apache.commons.exec.util<br>com.google.zxing<br>com.google.zxing.common<br>com.google.zxing.common.reedsolomon<br>com.google.zxing.qrcode.decoder<br>com.google.zxing.qrcode.encoder<br>com.adobe.cq.dam.dm.internalapi.image_server<br>com.day.cq.dam.api.s7dam.jobs<br>com.day.cq.dam.api.s7dam.omnisearch<br>com.day.cq.dam.api.s7dam.scene7<br>com.day.cq.dam.scene7<br>com.day.cq.dam.scene7.api.net<br>com.day.cq.analytics.sitecatalyst.rsmerger<br>com.day.cq.searchpromote<br>com.day.cq.searchpromote.xml<br>com.day.cq.searchpromote.xml.form<br>com.day.cq.searchpromote.xml.result&gt;</td>
    <td>従来の AEM 6.x API。</td>
  </tr>
  <tr>
    <td>org.apache.sling.discovery.commons<br>org.apache.sling.discovery.commons.providers<br>org.apache.sling.discovery.commons.providers.base<br>org.apache.sling.discovery.commons.providers.spi<br>org.apache.sling.discovery.commons.providers.spi.base<br>org.apache.sling.discovery.commons.providers.util</td>
    <td>この API は Cloud Service ではサポートされていません。</td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.vault.util.xml<br>org.apache.jackrabbit.vault.util.xml.serialize</td>
    <td>Apache Xerces に関連する Util クラスは、後続のリリースで削除され、メジャーバージョンが変更されます。 これらの Util は File vault での内部使用を目的としているので、API はパブリック API サーフェスから非推奨（廃止予定）になります。</td>
  </tr>
  <tr>
    <td>org.apache.sling.atom.taglib<br>org.apache.sling.atom.taglib.media</td>
    <td>従来の AEM 6.x API。 <a href="#org.apache.abdera_or_org.apache.sling.atom.taglib">以下の削除に関するメモを参照してください。</a></td>
  </tr>
  <tr>
    <td>org.apache.sling.commons.log.logback<br>org.apache.sling.commons.log.logback.webconsole</td>
    <td>AEM as a Cloud Service は、この内部ログバック API をサポートしていません。</td>
  </tr>
  <tr>
    <td>com.github.jknack.handlebars.js</td>
    <td>セキュリティの脆弱性により、Handlebars を 4.0.5 から 4.3.0 にアップグレードする必要があります。このパッケージは、アップグレードされたハンドルバーには存在しません。</td>
  </tr>
  <tr>
    <td>com.adobe.granite.resourceresolverhelper</td>
    <td>この API は、サポートされなくなりました。 代わりに、org.apache.sling.api.resource.ResourceResolverFactory を使用します。</td>
  </tr>
  <tr>
    <td>org.apache.sling.repoinit.jcr<br>org.apache.sling.repoinit.parser.operations</td>
    <td>この API の使用は、AEM as a Cloud Service ではサポートされていません。</td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.oak.cache</td>
    <td>この API は内部でのみ使用されます。</td>
  </tr>
</tbody>
</table>
</details>

## API 削除ガイダンス {#api-removal-guidance}

この節では、上記の表に示した様々な API の API 削除ガイダンスを反映しています。

### `org.apache.sling.commons.auth*` の削除 {#org.apache.sling.commons.auth}

`org.apache.sling.commons.auth`、`org.apache.sling.commons.auth.spi`、またはその両方を使用している場合、コードをそれぞれ `org.apache.sling.auth` または `org.apache.sling.auth.spi` に移行することで使用を置き換えることができます。古いバージョンの [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/) を使用している場合は、最新バージョンに更新する必要があります。

アクションリスト：

* ACS AEM Commons を最新バージョン（6.11.0 以降）にアップデート
* `org.apache.sling.commons.auth` や `org.apache.sling.commons.auth.spi` から `org.apache.sling.auth` または `org.apache.sling.auth.spi` にそれぞれ移行します。

### `org.apache.felix.webconsole*` の削除 {#org.apache.felix.webconsole}

`org.apache.felix.webconsole*` のパッケージを使用する場合は、このコードをプロジェクトから削除します。Cloud Service から web コンソールにアクセスできません。

アクションリスト：

* `org.apache.felix.webconsole*` のパッケージを使用したコードの削除

### `org.eclipse.jetty*` の削除 {#org.eclipse.jetty}

`org.eclipse.jetty` パッケージまたはそのサブパッケージのいずれかを使用する場合は、同様の機能を備えた他のサードパーティライブラリに移行することをお勧めします。移行が不可能な場合は、以下のリストから必要なバンドルをプロジェクトに追加します。

アクションリスト：

* `org.eclipse.jetty` パッケージの使用を他のサードパーティライブラリ／独自のコードに置き換える
* 次のリストから必要なバンドルを選択し、プロジェクトに追加
   * `org.eclipse.jetty:jetty-client:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-http:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-io:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-security:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-servlet:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-server:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-util:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-util-ajax:9.4.54.v20240208`

### `com.mongodb` の削除 {#com.mongodb}

Mongo client API をプロジェクトに追加します。

アクションリスト：

* このバンドルをプロジェクトに追加
   * `org.mongodb:mongo-java-driver:3.12.7`

要件に応じて、別のバージョンを選択することもできます。

### `com.google.common*` の削除 {#com.google.common}

Google Guava コアライブラリの使用を中止するか、プロジェクトに適切なバージョンを含めます。多くの場合、このライブラリの使用方法は、JDK のコレクションクラスまたは Apache Commons Collections4 に置き換えることができます。置き換えるバージョンが見つからない場合は、プロジェクトに最新バージョンの Google Guave コアライブラリを含めます。古いバージョンの [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/) を使用している場合は、最新バージョンに更新する必要があります。

アクションリスト：

* ACS AEM Commons を最新バージョン（6.11.0 以降）にアップデート
* Google Guava コアライブラリの使用を JDK コレクションまたは Apache Commons Collections4 に置き換える
* それでも必要な場合は、このバンドルをプロジェクトに追加します（バージョンを利用可能な最新のものに置き換えてください）。
   * `com.google.guava:guava:33.4.8-jre`

### `Apache Commons Lang 2 and Apache Commons Collections 3` の削除 {#apache.commons}

メンテナンスされていない Apache Commons ライブラリの使用を削除し、サポートバージョンの使用に置き換えます。ほとんどの場合、これはパッケージの読み込みを調整するだけで済みますが、クラスやメソッドの名前が変更される場合もあります。古いバージョンの [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/) を使用している場合は、最新バージョンに更新する必要があります。

アクションリスト：

* ACS AEM Commons を最新バージョン（6.11.0 以降）にアップデート
* `org.apache.commons.lang*` の読み込みの `org.apache.commons.lang3` への置き換え
* `org.apache.commons.collections*` の読み込みの `org.apache.commons.collecitons4` への置き換え

### `org.apache.abdera*` および `org.apache.sling.atom.taglib` の使用 {#org.apache.abdera_or_org.apache.sling.atom.taglib}

`org.apache.abdera` および `org.apache.sling.atom.taglib` のパッケージの使用を、同様の機能を備えたサードパーティライブラリまたは独自のコードに置き換えます。

アクションリスト：

* `org.apache.abdera` および `org.apache.sling.atom.taglib` のパッケージの使用を他のサードパーティライブラリ／独自のコードに置き換える

### `org.apache.felix.http.whiteboard` の使用 {#org.apache.felix.http.whiteboard}

`org.apache.felix.http.whiteboard` の使用を [OSGi Http ホワイトボード](https://docs.osgi.org/specification/osgi.cmpn/7.0.0/service.http.whiteboard.html)に置き換えます。 公式の OSGi API には同様の機能があり、ほとんどの場合、置き換えにはサービス登録プロパティの変更のみが必要です。

アクションリスト：

* `org.apache.felix.http.whiteboard` の使用を [OSGi Http ホワイトボード](https://docs.osgi.org/specification/osgi.cmpn/7.0.0/service.http.whiteboard.html)に置き換える

### `ch.qos.logback*` の使用 {#ch.qos.logback}

Cloud Service ではログバックはサポートされていないため、その使用をすべて削除してください。古いバージョンの [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/) を使用している場合は、最新バージョンに更新する必要があります。

アクションリスト：

* ACS AEM Commons を最新バージョン（6.11.0 以降）にアップデート
* `ch.qos.logback` のパッケージを使用したコードの削除

### `org.slf4j.event and org.slf4j.spi` の使用 {#org.slf4j}

`org.slf4j.event` または `org.slf4j.spi` を使用している場合は、その使用をすべて削除してください。古いバージョンの [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/) を使用している場合は、最新バージョンに更新する必要があります。

アクションリスト：

* ACS AEM Commons を最新バージョン（6.11.0 以降）にアップデート
* `org.slf4j.event` と `org.slf4j.spi` を使用してコードを削除します

### `org.apache.log4j` の使用 {#org.apache.log4j}

`org.apache.log4j` を使用している場合は、SLF4J（`org.slf4j`）または Log4J 2.x（`org.apache.logging.log4j`）に切り替えます。

アクションリスト：

* `org.apache.log4j` の使用を `org.slf4j`（推奨）または `org.apache.logging.log4j` の使用に置き換えます

## OSGi 設定 {#osgi-configuration}

以下の節は、AEM as a Cloud Service の OSGi 設定サーフェスを反映しており、顧客が設定できる内容を示しています。

1. 顧客コードでは、リストされた OSGi 設定を行わないでください。
1. プロパティを設定できるが、示されている検証ルールに従う必要がある OSGi 設定のリスト。 これらのルールには、プロパティの宣言が必須かどうか、プロパティの型、場合によっては許容される値の範囲が許可されます。

顧客コードでは、リストされていない任意の OSGi 設定を行うことができます。

これらのルールは、Cloud Manager のビルドプロセス中に検証されます。 今後、ルールが追加される可能性があり、その実施予定日が表に記載されています。 顧客は、目標の実施日までにこれらのルールを遵守する必要があります。 削除日以降にルールを遵守しないと、Cloud Manager ビルドプロセスでエラーが発生します。ローカル SDK の開発中に OSGI 設定エラーにフラグを付けるには、Maven プロジェクトに [AEM as a Maven SDK Build Analyzer Maven プラグイン](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin) を含める必要があります。

OSGI 設定に関する追加情報は、[この場所](/help/implementing/deploying/configuring-osgi.md)にあります。

### 非推奨の OSGi プロパティ（間もなく変更不可） {#deprecated-unmodifiable-osgi-properties}

次の OSGi コンポーネント PID のプロパティは非推奨となっており、施行日までに使用を停止する必要があります。

| **OSGI コンポーネント ID** | **変更不能プロパティ** | **非推奨（廃止予定）** | **適用** |
|---|---|---|---|
| **`org.apache.sling.commons.log.LogManager`** | すべて | 2025/4/24 | 2025/08/31 (設定は 6 月には無視されます) |
| **`org.apache.sling.commons.log.LogManager.factory.config`** | org.apache.sling.commons.log.file, org.apache.sling.commons.log.pattern | 2025/4/24 | 2025/08/31 (設定は 6 月には無視されます) |
| **`org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`** | すべて | 2024 | 2025/08/31 |
| **`com.adobe.granite.toggle.impl.dev.DynamicToggleProviderImpl`** | すべて | 2025/06/03 | 2025/08/31 |
| **`org.apache.http.proxyconfigurator`** | すべて | 2025/06/03 | 2025/08/31 |

### 変更不能な OSGi 設定 {#unmodifiable-osgi-properties}

次の OSGi コンポーネント PID のプロパティは変更できないので、設定しないでください。

| **OSGI コンポーネント ID** | **変更不能プロパティ** |
|---|---|
| **`com.day.cq.auth.impl.cug.CugSupportImpl`** |
| **`com.day.cq.jcrclustersupport.ClusterStartLevelController`** | すべて |
| **`com.adobe.granite.toggle.impl.ToggleRouterImpl`** | すべて |
| **`org.apache.sling.engine.impl.log.RequestLoggerFilter`** | すべて |
| **`org.apache.sling.feature.apiregions.impl`** | すべて |
| **`org.apache.sling.jcr.resource.internal.helper.jcr.BinaryDownloadUriProvider`** | すべて |
| **`com.adobe.cq.unifiedshell.impl.discovery.DiscoveryServlet`** | すべて |
| **`com.adobe.cq.unifiedshell.impl.ui.FrameErrorHandler`** | すべて |
| **`com.adobe.cq.unifiedshell.impl.config.UnifiedShellConfService`** | すべて |
| **`com.adobe.cq.unifiedshell.impl.config.RepositoryIdentifier`** | すべて |
| **`org.apache.sling.feature.apiregions.factory`** | すべて |
| **`com.adobe.granite.toggle.monitor.systemproperty`** | すべて |


### 将来的に適用される OSGi プロパティの制限 {#future-restrictions-osgi-properties}

今後、アドビは次の OSGi プロパティ制限を適用します。上記の PID の場合、リストに表示されているプロパティのみを設定できます。

| OSGi コンポーネントの PID |   | 必須 | タイプ | 制限 (該当する場合) |
|---|---|---|---|---|
| `com.day.cq.mailer.DefaultMailService` | `smtp.host` |   | 文字列 |   |
|   | `smtp.port` | はい | 整数 | 「465」、「587」または「25」のいずれか |
|   | `smtp.user` |   | 文字列 |   |
|   | `smtp.password` |   | 文字列 |   |
|   | `from.address` |   | 文字列 |   |
|   | `smtp.ssl` |   | 文字列 |   |
|   | `smtp.starttls` |   | ブーリアン |   |
|   | `smtp.requiretls` |   | ブーリアン |   |
|   | `debug.email` |   | ブーリアン |   |
|   | `oauth.flow` |   | ブーリアン |   |
| `org.apache.sling.commons.log.LogManager.factory.config` | `org.apache.sling.commons.log.level` | はい | 文字列 | 「情報」、「デバッグ」、「TRACE」のいずれか |
|   | `org.apache.sling.commons.log.names` |   | 文字列の配列 |   |
|   | `org.apache.sling.commons.log.additiv` |   | ブーリアン |   |
| `com.day.cq.commons.impl.ExternalizerImpl` | `externalizer.domains` | 不要 | 文字列[] |   |
|   | `externalizer.encodedpath` | 不要 | ブーリアン |   |
|   | `externalizer.host` | 不要 | 文字列 |   |
|   | `externalizer.contextpath` | 不要 | 文字列 |   |

### OSGi プロパティの制限 {#restrictions-osgi-properties}

これらの OSGi プロパティの値は、以下に説明するルールによって制限されています。

| OSGi コンポーネントの PID |   | 必須 | タイプ | 制限 (該当する場合) |
|---|---|---|---|---|
| `org.apache.felix.eventadmin.impl.EventAdmin` | `org.apache.felix.eventadmin.ThreadPoolSize` | はい | 整数 | 2-100 |
|   | `org.apache.felix.eventadmin.AsyncToSyncThreadRatio` |   | 倍精度浮動小数点 | -- |
|   | `org.apache.felix.eventadmin.AsyncToSyncThreadRatio` |   | 整数 | -- |
|   | `org.apache.felix.eventadmin.RequireTopic` |   | ブーリアン | -- |
|   | `org.apache.felix.eventadmin.IgnoreTimeout` | はい | 文字列の配列 | 少なくとも `org.apache.felix*`、`org.apache.sling*`、`come.day*`、`com.adobe*` をすべてを含める必要があります。 |
|   | `org.apache.felix.eventadmin.IgnoreTopic` |   | 文字列の配列 | -- |
| `org.apache.felix.http` | `org.apache.felix.http.timeout` |   | 整数 |   |
|   | `org.apache.felix.http.session.timeout` |   | 整数 |   |
|   | `org.apache.felix.http.jetty.threadpool.max` |   | 整数 |   |
|   | `org.apache.felix.http.jetty.headerBufferSize` |   | 整数 |   |
|   | `org.apache.felix.http.jetty.requestBufferSize` |   | 整数 |   |
|   | `org.apache.felix.http.jetty.responseBufferSize` |   | 整数 |   |
|   | `org.apache.felix.http.jetty.maxFormSize` |   | 整数 |   |
|   | `org.apache.felix.https.jetty.session.cookie.httpOnly` |   | ブーリアン |   |
|   | `org.apache.felix.https.jetty.session.cookie.secure` |   | ブーリアン |   |
|   | `org.eclipse.jetty.servlet.SessionIdPathParameterName` |   | 文字列 |   |
|   | `org.eclipse.jetty.servlet.CheckingRemoteSessionIdEncoding` |   | ブーリアン |   |
|   | `org.eclipse.jetty.servlet.SessionCookie` |   | 文字列 |   |
|   | `org.eclipse.jetty.servlet.SessionDomain` |   | 文字列 |   |
|   | `org.eclipse.jetty.servlet.SessionPath` |   | 文字列 |   |
|   | `org.eclipse.jetty.servlet.MaxAge` |   | 整数 |   |
|   | `org.eclipse.jetty.servlet.SessionScavengingInterval` |   | 整数 |   |
|   | `org.apache.felix.jetty.gziphandler.enable` |   | ブーリアン |   |
|   | `org.apache.felix.jetty.gzip.minGzipSize` |   | 整数 |   |
|   | `org.apache.felix.jetty.gzip.compressionLevel` |   | 整数 |   |
|   | `org.apache.felix.jetty.gzip.inflateBufferSize` |   | 整数 |   |
|   | `org.apache.felix.jetty.gzip.syncFlush` |   | ブーリアン |   |
|   | `org.apache.felix.jetty.gzip.excludedUserAgents` |   | 文字列 |   |
|   | `org.apache.felix.jetty.gzip.includedMethods` |   | 文字列の配列 |   |
|   | `org.apache.felix.jetty.gzip.excludedMethods` |   | 文字列の配列 |   |
|   | `org.apache.felix.jetty.gzip.includedPaths` |   | 文字列の配列 |   |
|   | `org.apache.felix.jetty.gzip.excludedPaths` |   | 文字列の配列 |   |
|   | `org.apache.felix.jetty.gzip.includedMimeTypes` |   | 文字列の配列 |   |
|   | `org.apache.felix.http.session.invalidate` |   | ブーリアン |   |
|   | `org.apache.felix.http.session.container.attribute` |   | 文字列の配列 |   |
|   | `org.apache.felix.http.session.uniqueid` |   | ブーリアン |   |
| `org.apache.sling.scripting.cache` | `org.apache.sling.scripting.cache.size` | はい | 整数 | >= 2048 |
|   | `org.apache.sling.scripting.cache.additional_extensions` | はい | 文字列の配列 | 「js」を含める必要があります |
| `org.apache.sling.engine.impl.log.RequestLogger` | `request.log.output` | 不要 | 文字列 |   |
|   | `request.log.outputtype` | 不要 | 文字列 |   |
|   | `request.log.entry.format` | 不要 | 文字列 |   |
|   | `request.log.exit.format` | 不要 | 文字列 |   |
|   | `request.log.enabled` | 不要 | 文字列 |   |
|   | `access.log.output` | 不要 | 文字列 |   |
|   | `access.log.outputtype` | 不要 | 文字列 |   |
|   | `access.log.enabled` | 不要 | 文字列 |   |
| `org.apache.sling.servlets.resolver.SlingServletResolver` | `servletresolver.servletRoot` | 不要 | 文字列 |   |
|   | `servletresolver.cacheSize` | 不要 | 整数 |   |
|   | `servletresolver.paths` | 不要 | 文字列[] |   |
|   | `servletresolver.defaultExtensions` | 不要 | 文字列 |   |
|   | `servletresolver.mountProviders` | 不要 | ブーリアン |   |
|   | `servletresolver.scriptUser` | 不要 | 文字列 | 廃止されています。使用しないでください。 |

## Java ランタイムのバージョン 21 へのアップデート {#java-runtime-update-21}

Adobe Experience Manager as a Cloud Service は、Java 21 ランタイムに移行されました。互換性を確保するには、[ランタイム要件](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)の説明に従って、ライブラリバージョンをアップデートすることが不可欠です。

