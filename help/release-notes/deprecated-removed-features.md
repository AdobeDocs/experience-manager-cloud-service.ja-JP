---
title: 廃止される機能および削除された機能
description: リリースノート（ [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の非推奨（廃止予定）の機能と削除された機能）。
exl-id: ef082184-4eb7-49c7-8887-03d925e3da6f
feature: Release Information
role: Admin
source-git-commit: 1ff3a9a0ff6b408794956323f12194f136d6b2ad
workflow-type: tm+mt
source-wordcount: '2800'
ht-degree: 90%

---

# 非推奨（廃止予定）および削除された機能と API {#deprecated-and-removed-features-apis}

>[!CONTEXTUALHELP]
>id="aem_cloud_deprecated_features"
>title="AEM as a Cloud Service の非推奨（廃止予定）の機能と削除された機能"
>abstract="AEM as a Cloud Service には、クラウドネイティブなデプロイメントモデルがあります。一部の機能や特徴は、クラウドネイティブでの同等機能に置き換えられました。ここでは、それらの機能を示します。"

アドビでは、製品の機能を絶えず評価して、常に後方互換性を慎重に考慮しながら、古い機能を作成し直したり、新たな機能に置き換えて、お客様にとっての全体的な価値を向上させます。また、[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] はクラウドネイティブなデプロイメントモデルを提供するので、一部の機能はクラウドネイティブな同等機能に置き換わりました。

近い将来行われる [!DNL Experience Manager] 機能の削除や置換を通知するため、次のルールが適用されます。

1. まず、非推奨（廃止予定）の発表が行われます。廃止される機能は引き続き使用できますが、それ以上改善されません。
1. 廃止予定と発表された機能は、早ければ後続のメジャーリリースで削除されます。削除の実際の目標日が通知されます。

このプロセスにより、機能が実際に削除されるまでに、非推奨（廃止予定）の機能の新しいバージョンまたは後継機能にお客様が実装を合わせるためのリリースサイクルが少なくとも 1 回あります。

## 非推奨（廃止予定）の機能 {#deprecated-features}

ここでは、[!DNL Experience Manager] as a [!DNL Cloud Service] で廃止予定の機能について説明します。通常、将来のリリースで削除が予定される機能はまず廃止対象として代替手段が提示されます。

現在のデプロイメントでその機能を利用しているかどうかを確認し、提示される代替手段を使用するために実装の変更を計画するようにお勧めします。

| 機能 | 非推奨（廃止予定）の機能 | 代替手段 |
| ------------ | ------------------ | ----------- |
| [!DNL Sites] | [JavaScript Use API](https://github.com/adobe/htl-spec/blob/master/SPECIFICATION.md#42-javascript-use-api) | [Java Use API](https://experienceleague.adobe.com/ja/docs/experience-manager-htl/content/java-use-api) |
| [!DNL Sites] | **ソーシャルメディアのステータス** のエクスペリエンスフラグメントのプロパティ。  | この機能は間もなく削除されます。 |
| [!DNL Sites] | テンプレートベースのシンプルなコンテンツフラグメント。 | 現在は[モデルベースの構造化コンテンツフラグメント](/help/assets/content-fragments/content-fragments-models.md)。 |
| [!DNL Assets] | 取り込んだ画像を処理する `DAM Asset Update` ワークフロー | 現在は、アセットの取り込みで[アセットマイクロサービス](/help/assets/asset-microservices-overview.md)が使用されています。 |
| [!DNL Assets] | [!DNL Experience Manager] へのアセットの直接アップロード。[非推奨（廃止予定）のアセットアップロード API](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api) を参照してください。 | [直接バイナリアップロード](/help/assets/add-assets.md)を使用。技術的な詳細については、[直接アップロード API](/help/assets/developer-reference-material-apis.md#upload-binary) を参照してください。 |
| [!DNL Assets] | [!DNL ImageMagick] などのコマンドラインツールの呼び出しを含め、`DAM Asset Update` ワークフローの[特定のワークフローステップ](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps)はサポートされていません。 | [アセットマイクロサービス](/help/assets/asset-microservices-overview.md)が多くのワークフローの代替機能となります。カスタム処理の場合は、[後処理ワークフロー](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)を使用します。 |
| [!DNL Assets] | ビデオの FFmpeg トランスコード。 | FFmpeg サムネールの生成には、[アセットマイクロサービス](/help/assets/asset-microservices-overview.md)を使用。FFmpeg トランスコードの場合は、[Dynamic Media](/help/assets/manage-video-assets.md) を使用。 |
| [!DNL Foundation] | レプリケーションエージェントの「配布」タブのツリーレプリケーション UI（2021 年 9 月 30 日以降に削除） | [ パブリケーションの管理 ](/help/operations/replication.md#manage-publication) または [ ツリーアクティベーションワークフローステップ ](/help/operations/replication.md#tree-activation) アプローチ。 |
| [!DNL Foundation] | レプリケーションエージェントの管理画面の「配布」タブも、レプリケーション API も、10 MB を超えるコンテンツパッケージのレプリケーションには使用できません。 | [ パブリケーションの管理 ](/help/operations/replication.md#manage-publication) または [ ツリーアクティベーションワークフローステップ ](/help/operations/replication.md#tree-activation) |
| [!DNL Foundation] | Adobe Developer Console プロジェクトから生成された資格情報を使用した統合では、サービスアカウント（JWT）資格情報のサポートが段階的に失われます。2024 年5月1日（PT）以降、Adobe Developer Console で新しいサービスアカウント（JWT）資格情報を作成できなくなります。ただし、既存のサービスアカウント（JWT）資格情報は、2025年1月1日（PT）までは設定済みの統合に引き続き使用できます。この時点で、既存のサービスアカウント（JWT）資格情報は機能しなくなり、お客様は OAuth サーバー間の資格情報に移行する必要があります。[詳細情報](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/security/jwt-credentials-deprecation-in-adobe-developer-console)。 | OAuth サーバー間の資格情報に[移行](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview)します。 |
| [!DNL Foundation] | Publish コンテンツツリーワークフローと、コンテンツ階層のレプリケーションに使用された、関連するPublish コンテンツツリーワークフローステップ。 | よりパフォーマンスの高い [ ツリーのアクティベーションワークフローステップ ](/help/operations/replication.md#tree-activation) を使用します。 |


## 削除された機能 {#removed-features}

ここでは、[!DNL Experience Manager] as a [!DNL Cloud Service] の導入で [!DNL Experience Manager] から削除された機能の一覧を示します。

| 領域 | 機能 | 代替手段 | 削除予定日 |
| ------------ | ------------------ | ----------- | ------------------- |
| ユーザーインターフェイス | クラシック UI が製品ユーザーインターフェイスから削除されました。いくつかのクラシック UI ダイアログは、リンクチェッカー、バージョンパージ、一部の Cloud Service 設定など、いくつかの機能で使用できます。今後の[製品アップデート](/help/release-notes/home.md)により、クラシック UI の利用範囲がさらに狭まる可能性があります。 | 標準 UI | 削除済み |
| [!DNL Dynamic Media] | [Dynamic Media Classic](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/scene7.html?lang=ja#integration) および [Dynamic Media Hybrid モード](https://experienceleague.adobe.com/docs/experience-manager-65/assets/dynamic/config-dynamic.html?lang=ja#dynamic)との従来の統合は、[!DNL Experience Manager] as a [!DNL Cloud Service] では使用できません。 | [!DNL Experience Manager] as a [!DNL Cloud Service] に用意されている [Dynamic Media](/help/assets/dynamic-media/dynamic-media.md) を使用します。 | 削除済み |
| [!DNL Sites] | Portal Director とポートレットコンポーネント | これらの機能は [!DNL Experience Manager] 6.4 で非推奨（廃止予定）となり、現在は [!DNL Experience Manager] から削除されています。 | 削除済み |
| [!DNL Sites] | デザインインポーター | 実行時に [!DNL Experience Manager] リポジトリーの不変セクションにアクセスできないので、この機能は削除されました。 | 削除済み |
| [!DNL Assets] | [!DNL Assets]Experience Cloud Assets コアサービスおよび Creative Cloud サービスとの の共有は使用できません。 | [!DNL Adobe Creative Cloud] との統合には、[Adobe Asset Link](https://helpx.adobe.com/jp/enterprise/using/adobe-asset-link.html) を使用します。 | 削除済み |
| [!DNL Foundation] | Apache Sling データソースのサポート（OSGi バンドル org.apache.sling.datasource） | 該当なし | 削除済み |
| [!DNL Foundation] | JST スクリプティングテンプレートのサポート（OSGi バンドル org.apache.sling.scripting.jst） | 該当なし | 削除済み |
| [!DNL Foundation] | Apache Felix Http Whiteboard のサポート | OSGi Http Whiteboard | 2022年3月 |
| [!DNL Foundation] | com.adobe.granite.oauth.server のサポート | Adobe IMS 統合 | 2023年3月 |
| [!DNL Foundation] | [サービスユーザー ID を取得](https://sling.apache.org/apidocs/sling12/org/apache/sling/serviceusermapping/ServiceUserMapper.html#getServiceUserID-org.osgi.framework.Bundle-java.lang.String-)するための org.apache.sling.serviceusermapping 機能のサポート | 該当なし | 2024年8月30日（PT） |


## AEM API {#aem-apis}

非推奨（廃止予定）の AEM API とそれらの削除予定日の一覧を以下に示します。お客様は、削除予定日までに、これらの API をコードから削除する必要があります。該当する API を削除日以降に使用すると、ローカル SDK／開発環境および Cloud Manager ビルドプロセスでエラーが発生します。

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
    <td>代わりに、Sling の Auth Core／Auth Core SPI インターフェイスを使用します。<a href="#org.apache.sling.commons.auth">以下の削除に関するメモを参照してください。</a></td>
    <td>2015</td>
    <td>2021/7/30</td>
  </tr>
  <tr>
    <td>org.apache.sling.runmode</td>
    <td></td>
    <td>2015</td>
    <td>2021/7/30</td>
  </tr>
  <tr>
    <td>com.day.cq.jcrclustersupport</td>
    <td>Sling の Discovery API を代わりに使用してください。</td>
    <td>2015</td>
    <td>削除済み</td>
  </tr>
  <tr>
    <td>org.apache.fop.apps</td>
    <td></td>
    <td>2021/3/1</td>
    <td>削除済み</td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.vault.util.xml.xerces.dom<br>org.apache.jackrabbit.vault.util.xml.xerces.util<br>org.apache.jackrabbit.vault.util.xml.xerces.xni<br>org.apache.jackrabbit.vault.util.xml.xerces.xni.parser</td>
    <td></td>
    <td>2021/3/5</td>
    <td>削除済み</td>
  </tr>
  <tr>
    <td>org.json</td>
    <td><a href="https://johnzon.apache.org/index.html">javax.json</a> の Apache Johnzon 実装の使用をお勧めします。 </td>
    <td>2021/4/30</td>
    <td>2021/12/31</td>
  </tr>
  <tr>
    <td>org.apache.felix.cm<br>org.apache.felix.cm.file</td>
    <td>AEM as a Cloud Service では、カスタム永続性マネージャーはサポートされていません。</td>
    <td>2021/4/30</td>
    <td>削除済み</td>
  </tr>
  <tr>
    <td>org.apache.commons.lang<br>org.apache.commons.lang.enums<br>org.apache.commons.lang.builder<br>org.apache.commons.lang.exception<br>org.apache.commons.lang.math<br>org.apache.commons.lang.mutable<br>org.apache.commons.lang.reflect<br>org.apache.commons.lang.text<br>org.apache.commons.lang.time</td>
    <td>Commons Lang 2 はメンテナンスモードになっています。Commons Lang 3 を代わりに使用してください。</td>
    <td>2021/4/30</td>
    <td>2021/12/31</td>
  </tr>
  <tr>
    <td>org.apache.commons.collections<br>org.apache.commons.collections.bag<br>org.apache.commons.collections.bidimap<br>org.apache.commons.collections.buffer<br>org.apache.commons.collections.collection<br>org.apache.commons.collections.comparators<br>org.apache.commons.collections.functors<br>org.apache.commons.collections.iterators<br>org.apache.commons.collections.keyvalue<br>org.apache.commons.collections.list<br>org.apache.commons.collections.map<br>org.apache.commons.collections.set</td>
    <td>Commons Collections 3 はメンテナンスモードになっています。Commons Collections 4 を代わりに使用してください。</td>
    <td>2021/4/30</td>
    <td>2021/12/31</td>
  </tr>
  <tr>
    <td>org.apache.felix.systemready</td>
    <td>Apache Felix HealthCheck API を代わりに使用することをお勧めします。</td>
    <td>2021/4/30</td>
    <td>削除済み</td>
  </tr>
  <tr>
    <td>org.apache.felix.webconsole<br>org.apache.felix.webconsole.bundleinfo<br>org.apache.felix.webconsole.i18n</td>
    <td>Felix web コンソールはクラウド環境ではサポートされていません。</td>
    <td>2021/4/30</td>
    <td>2021/7/30</td>
  </tr>
  <tr> <td>org.apache.felix.http.jetty<br>org.eclipse.jetty.client.jmx<br>org.eclipse.jetty.jmx<br>org.eclipse.jetty.server.handler.jmx<br>org.eclipse.jetty.server.nio<br>org.eclipse.jetty.server.jmx<br>org.eclipse.jetty.servlet.jmx<br>org.eclipse.jetty.util.preventers<br>org.eclipse.jetty.util.thread.strategy<br>org.eclipse.jetty.webapp<br>org.eclipse.jetty.websocket.api<br>org.eclipse.jetty.websocket.api.annotations<br>org.eclipse.jetty.websocket.api.extensions<br>org.eclipse.jetty.websocket.api.util<br>org.eclipse.jetty.websocket.client<br>org.eclipse.jetty.websocket.client.io<br>org.eclipse.jetty.websocket.client.masks<br>org.eclipse.jetty.websocket.common<br>org.eclipse.jetty.websocket.common.events<br>org.eclipse.jetty.websocket.common.events.annotated<br>org.eclipse.jetty.websocket.common.extensions<br>org.eclipse.jetty.websocket.common.extensions.compress<br>org.eclipse.jetty.websocket.common.extensions.fragment<br>org.eclipse.jetty.websocket.common.extensions.identity<br>org.eclipse.jetty.websocket.common.frames<br>org.eclipse.jetty.websocket.common.io<br>org.eclipse.jetty.websocket.common.io.http<br>org.eclipse.jetty.websocket.common.io.payload<br>org.eclipse.jetty.websocket.common.message<br>org.eclipse.jetty.websocket.common.scopes<br>org.eclipse.jetty.websocket.common.util<br>org.eclipse.jetty.websocket.server<br>org.eclipse.jetty.websocket.server.pathmap<br>org.eclipse.jetty.websocket.servlet<br>org.eclipse.jetty.xml</td>
    <td>Eclipse Jetty パッケージと Felix Http Jetty パッケージはサポートされなくなりました。<a href="#org.eclipse.jetty">以下の削除に関するメモを参照してください。</a></td>
    <td>2021/5/27</td>
    <td>2021/8/26</td>
  </tr>
  <tr> <td>org.eclipse.jetty.client<br>org.eclipse.jetty.client.api<br>org.eclipse.jetty.client.http<br>org.eclipse.jetty.client.util<br>org.eclipse.jetty.http<br>org.eclipse.jetty.http.pathmap<br>org.eclipse.jetty.io<br>org.eclipse.jetty.io.ssl<br>org.eclipse.jetty.security<br>org.eclipse.jetty.server<br>org.eclipse.jetty.server.handler<br>org.eclipse.jetty.server.handler.gzip<br>org.eclipse.jetty.server.session<br>org.eclipse.jetty.servlet<br>org.eclipse.jetty.servlet.listener<br>org.eclipse.jetty.util<br>org.eclipse.jetty.util.annotation<br>org.eclipse.jetty.util.component<br>org.eclipse.jetty.util.log<br>org.eclipse.jetty.util.resource<br>org.eclipse.jetty.util.security<br>org.eclipse.jetty.util.ssl<br>org.eclipse.jetty.util.statistic<br>org.eclipse.jetty.util.thread
</td>
    <td>Eclipse Jetty パッケージと Felix Http Jetty パッケージはサポートされなくなりました。</td>
    <td>2021/5/27</td>
    <td>2021/8/26</td>
  </tr>  
  <tr>     <td>com.mongodb<br>com.mongodb.annotations<br>com.mongodb.assertions<br>com.mongodb.async<br>com.mongodb.binding<br>com.mongodb.bulk<br>com.mongodb.client<br>com.mongodb.client.gridfs<br>com.mongodb.client.gridfs.codecs<br>com.mongodb.client.gridfs.model<br>com.mongodb.client.jndi<br>com.mongodb.client.model<br>com.mongodb.client.model.changestream<br>com.mongodb.client.model.geojson<br>com.mongodb.client.model.geojson.codecs<br>com.mongodb.client.result<br>com.mongodb.connection<br>com.mongodb.connection.netty<br>com.mongodb.diagnostics.logging<br>com.mongodb.event<br>com.mongodb.gridfs<br>com.mongodb.internal<br>com.mongodb.internal.async<br>com.mongodb.internal.authentication<br>com.mongodb.internal.connection<br>com.mongodb.internal.dns<br>com.mongodb.internal.event<br>com.mongodb.internal.management.jmx<br>com.mongodb.internal.session<br>com.mongodb.internal.thread<br>com.mongodb.internal.validator<br>com.mongodb.management<br>com.mongodb.operation<br>com.mongodb.selector<br>com.mongodb.session<br>com.mongodb.util</td>
    <td>この API の使用は、AEM as a Cloud Service ではサポートされていません。<a href="#com.mongodb">以下の削除に関するメモを参照してください。</a></td>
    <td>2021/5/27</td>
    <td>2021/7/30</td>
  </tr>
  <tr>
    <td>org.apache.felix.metatype<br>org.apache.felix.scr<br>org.apache.felix.scr.info<br>org.apache.felix.scr.component</td>
    <td>Apache Felix メタタイプと SCR API は非推奨（廃止予定）です。OSGi メタタイプおよび Declarative Service API を代わりに使用してください。</td>
    <td>2021/5/27</td>
    <td>削除済み</td>
  </tr>
  <tr>
    <td>org.slf4j.impl</td>
    <td>ログ実装クラスは、AEM as a Cloud Service と互換性がありません。</td>
    <td>2021/7/4</td>
    <td>削除済み</td>
  </tr>
  <tr>
    <td>org.apache.abdera<br>org.apache.abdera.model<br>org.apache.abdera.factory<br>org.apache.abdera.ext.media<br>org.apache.abdera.util<br>org.apache.abdera.i18n.iri<br>org.apache.abdera.writer<br>org.apache.abdera.i18n.rfc4646<br>org.apache.abdera.i18n.rfc4646.enums<br>org.apache.abdera.i18n.text<br>org.apache.abdera.filter<br>org.apache.abdera.xpath<br>org.apache.abdera.i18n.text.io<br>org.apache.abdera.i18n.text.data<br>org.apache.abdera.parser</td>
    <td>Apache Abdera が 2017年以降廃止されたプロジェクトなので、この API は廃止されました。<a href="#org.apache.abdera_or_org.apache.sling.atom.taglib">以下の削除に関するメモを参照してください。</a></td>
    <td>2021/7/29</td>
    <td>2021/9/29</td>
  </tr>
  <tr>
    <td>org.apache.abdera.ext.opensearch<br>org.apache.abdera.ext.opensearch.model<br>org.apache.abdera.ext.opensearch.server<br>org.apache.abdera.ext.opensearch.server.impl<br>org.apache.abdera.ext.opensearch.server.processors<br>org.apache.abdera.i18n.iri.data<br>org.apache.abdera.i18n.lang<br>org.apache.abdera.i18n.templates<br>org.apache.abdera.i18n.unicode.data<br>org.apache.abdera.parser.stax<br>org.apache.abdera.parser.stax.util<br>org.apache.abdera.protocol<br>org.apache.abdera.protocol.client<br>org.apache.abdera.protocol.client.cache<br>org.apache.abdera.protocol.client.util<br>org.apache.abdera.protocol.error<br>org.apache.abdera.protocol.server<br>org.apache.abdera.protocol.server.context<br>org.apache.abdera.protocol.server.filters<br>org.apache.abdera.protocol.server.impl<br>org.apache.abdera.protocol.server.multipart<br>org.apache.abdera.protocol.server.processors<br>org.apache.abdera.protocol.server.provider.basic<br>org.apache.abdera.protocol.server.provider.managed<br>org.apache.abdera.protocol.server.servlet<br>org.apache.abdera.protocol.util<br>org.apache.abdera.util.filter</td>
    <td>Apache Abdera が 2017年以降廃止されたプロジェクトなので、この API は廃止されました。</td>
    <td>2019/4/8</td>
    <td>2021/9/29</td>
  </tr>
  <tr>
    <td>org.apache.sling.startupfilter<br>com.adobe.granite.crypto.spi<br>com.adobe.granite.crpyto.spi.base<br>com.adobe.agl.impl.data.icudt40b<br>com.adobe.agl.impl.data.icudt40b.brkitr<br>com.adobe.agl.impl.data.icudt40b.coll<br>com.adobe.agl.impl.data.icudt40b.rbnf<br>com.<br>adobe.agl.impl.data.icudt40b.translit<br>com.adobe.internal.pdf.tika<br>com.adobe.internal.pdftoolkit.color<br>com.adobe.internal.pdftoolkit.core.encryption<br>com.adobe.internal.pdftoolkit.core.encryption.impl<br>com.adobe.internal.pdftoolkit.core.traverser<br>com.adobe.internal.pdftoolkit.graphicsDOM<br>com.adobe.internal.pdftoolkit.graphicsDOM.shading<br>com.adobe.internal.pdftoolkit.graphicsDOM.utils<br>com.adobe.internal.pdftoolkit.image<br>com.adobe.internal.pdftoolkit.pdf.content<br>com.adobe.internal.pdftoolkit.pdf.content.processor<br>com.adobe.internal.pdftoolkit.pdf.content.processor.base14fontwidths<br>com.adobe.internal.pdftoolkit.pdf.contentmodify<br>com.adobe.internal.pdftoolkit.pdf.contentmodify.impl<br>com.adobe.internal.pdftoolkit.pdf.digsig<br>com.adobe.internal.pdftoolkit.pdf.document<br>com.adobe.internal.pdftoolkit.pdf.document.listener<br>com.adobe.internal.pdftoolkit.pdf.document.permissionhandlers<br>com.adobe.internal.pdftoolkit.pdf.filters<br>com.adobe.internal.pdftoolkit.pdf.graphics<br>com.adobe.internal.pdftoolkit.pdf.graphics.colorspaces<br>com.adobe.internal.pdftoolkit.pdf.graphics.colorspaces.cmykresources<br>com.adobe.internal.pdftoolkit.pdf.graphics.font<br>com.adobe.internal.pdftoolkit.pdf.graphics.font.encodings<br>com.adobe.internal.pdftoolkit.pdf.graphics.font.impl<br>com.adobe.internal.pdftoolkit.pdf.graphics.impl<br>com.adobe.internal.pdftoolkit.pdf.graphics.optionalcontent<br>com.adobe.internal.pdftoolkit.pdf.graphics.patterns<br>com.adobe.internal.pdftoolkit.pdf.graphics.shading<br>com.adobe.internal.pdftoolkit.pdf.graphics.xobject<br>com.adobe.internal.pdftoolkit.pdf.impl<br>com.adobe.internal.pdftoolkit.pdf.inlineimage<br>com.adobe.internal.pdftoolkit.pdf.interactive<br>com.adobe.internal.pdftoolkit.pdf.interactive.action<br>com.adobe.internal.pdftoolkit.pdf.interactive.annotation<br>com.adobe.internal.pdftoolkit.pdf.interactive.forms<br>com.adobe.internal.pdftoolkit.pdf.interactive.forms.impl<br>com.adobe.internal.pdftoolkit.pdf.interactive.geospatial<br>com.adobe.internal.pdftoolkit.pdf.interactive.markedcontent<br>com.adobe.internal.pdftoolkit.pdf.interactive.navigation<br>com.adobe.internal.pdftoolkit.pdf.interactive.navigation.collection<br>com.adobe.internal.pdftoolkit.pdf.interactive.readerrequirements<br>com.adobe.internal.pdftoolkit.pdf.interactive.requirement<br>com.adobe.internal.pdftoolkit.pdf.interchange<br>com.adobe.internal.pdftoolkit.pdf.interchange.documentparts<br>com.adobe.internal.pdftoolkit.pdf.interchange.metadata<br>com.adobe.internal.pdftoolkit.pdf.interchange.prepress<br>com.adobe.internal.pdftoolkit.pdf.interchange.structure<br>com.adobe.internal.pdftoolkit.pdf.multimedia<br>com.adobe.internal.pdftoolkit.pdf.page<br>com.adobe.internal.pdftoolkit.pdf.rendering<br>com.adobe.internal.pdftoolkit.pdf.transparency<br>com.adobe.internal.pdftoolkit.pdf.utils<br>com.adobe.internal.pdftoolkit.services.Jpeg2000<br>com.adobe.internal.pdftoolkit.services.fontresources<br>com.adobe.internal.pdftoolkit.services.fontresources.subsetting<br>com.adobe.internal.pdftoolkit.services.interchange.structure<br>com.adobe.internal.pdftoolkit.services.optionalcontent<br>com.adobe.internal.pdftoolkit.services.optionalcontent.impl<br>com.adobe.internal.pdftoolkit.services.pdfParser<br>com.adobe.internal.pdftoolkit.services.permissions<br>com.adobe.internal.pdftoolkit.services.rasterizer<br>com.adobe.internal.pdftoolkit.services.readingorder<br>com.adobe.internal.pdftoolkit.services.security<br>com.adobe.internal.pdftoolkit.services.swf<br>com.adobe.internal.pdftoolkit.services.textextraction<br>com.adobe.internal.pdftoolkit.services.textextraction.impl<br>com.adobe.internal.pdftoolkit.services.xmp<br>com.adobe.internal.util.base64<br>com.adobe.internal.xmp.utils<br>com.day.crx.core.cluster<br>com.day.crx.packaging<br>com.day.crx.packaging.gfx<br>com.day.crx.query<br>com.day.crx.sling.server.jmx<br>com.day.durbo<br>com.day.durbo.io<br>com.day.imageio.plugins<br>org.apache.aries.jmx.codec<br>org.h2.mvstore<br>org.h2.mvstore.rtree<br>org.h2.mvstore.type<br>org.openxmlformats.schemas.drawingml.x2006.chart.impl<br>org.openxmlformats.schemas.drawingml.x2006.main.impl<br>org.openxmlformats.schemas.drawingml.x2006.picture.impl<br>org.openxmlformats.schemas.drawingml.x2006.spreadsheetDrawing.impl<br>org.openxmlformats.schemas.drawingml.x2006.wordprocessingDrawing.impl<br>org.openxmlformats.schemas.officeDocument.x2006.customProperties.impl<br>org.openxmlformats.schemas.officeDocument.x2006.docPropsVTypes.impl<br>org.openxmlformats.schemas.officeDocument.x2006.extendedProperties.impl<br>org.openxmlformats.schemas.officeDocument.x2006.relationships.impl<br>org.openxmlformats.schemas.presentationml.x2006.main.impl<br>org.openxmlformats.schemas.spreadsheetml.x2006.main.impl<br>org.openxmlformats.schemas.wordprocessingml.x2006.main.impl<br>org.openxmlformats.schemas.xpackage.x2006.contentTypes<br>org.openxmlformats.schemas.xpackage.x2006.contentTypes.impl<br>org.openxmlformats.schemas.xpackage.x2006.digitalSignature<br>org.openxmlformats.schemas.xpackage.x2006.digitalSignature.impl<br>org.openxmlformats.schemas.xpackage.x2006.metadata.coreProperties<br>org.openxmlformats.schemas.xpackage.x2006.metadata.coreProperties.impl<br>org.openxmlformats.schemas.xpackage.x2006.relationships<br>org.openxmlformats.schemas.xpackage.x2006.relationships.impl<br>com.adobe.internal.afml<br>com.adobe.internal.agm<br>com.adobe.internal.pdftoolkit.legacy.services.ap.es2<br>com.adobe.internal.pdftoolkit.legacy.services.ap.es3<br>com.adobe.internal.pdftoolkit.pdf.pieceinfo.compoundtype<br>com.adobe.internal.pdftoolkit.pdf.pieceinfo.editablepdf<br>com.adobe.internal.pdftoolkit.services.ap<br>com.adobe.internal.pdftoolkit.services.ap.annot<br>com.adobe.internal.pdftoolkit.services.ap.extension<br>com.adobe.internal.pdftoolkit.services.ap.impl<br>com.adobe.internal.pdftoolkit.services.ap.spi<br>com.adobe.internal.pdftoolkit.services.digsig<br>com.adobe.internal.pdftoolkit.services.digsig.cryptoprovider<br>com.adobe.internal.pdftoolkit.services.digsig.docmodanalysis<br>com.adobe.internal.pdftoolkit.services.digsig.spi<br>com.adobe.internal.pdftoolkit.services.fdf<br>com.adobe.internal.pdftoolkit.services.formflattener<br>com.adobe.internal.pdftoolkit.services.forms<br>com.adobe.internal.pdftoolkit.services.imageconversion<br>com.adobe.internal.pdftoolkit.services.javascript<br>com.adobe.internal.pdftoolkit.services.javascript.extension<br>com.adobe.internal.pdftoolkit.services.manipulations<br>com.adobe.internal.pdftoolkit.services.manipulations.impl<br>com.adobe.internal.pdftoolkit.services.optimizer<br>com.adobe.internal.pdftoolkit.services.pdfa<br>com.adobe.internal.pdftoolkit.services.pdfa.error<br>com.adobe.internal.pdftoolkit.services.pdfa2<br>com.adobe.internal.pdftoolkit.services.pdfa2.error<br>com.adobe.internal.pdftoolkit.services.pdfa2.error.codes<br>com.adobe.internal.pdftoolkit.services.pdfa3<br>com.adobe.internal.pdftoolkit.services.pdfport<br>com.adobe.internal.pdftoolkit.services.portfolio<br>com.adobe.internal.pdftoolkit.services.rcg<br>com.adobe.internal.pdftoolkit.services.rcg.impl<br>com.adobe.internal.pdftoolkit.services.redaction<br>com.adobe.internal.pdftoolkit.services.redaction.handler<br>com.adobe.internal.pdftoolkit.services.sanitization<br>com.adobe.internal.pdftoolkit.services.xbm<br>com.adobe.internal.pdftoolkit.services.xdp<br>com.adobe.internal.pdftoolkit.services.xfa<br>com.adobe.internal.pdftoolkit.services.xfa.form<br>com.adobe.internal.pdftoolkit.services.xfatext<br>com.adobe.internal.pdftoolkit.services.xfdf<br>com.adobe.internal.pdftoolkit.services.xobjhandler<br>com.adobe.internal.pdftoolkit.xml<br>com.adobe.octopus.extract<br>opennlp.tools.doccat<br>opennlp.tools.entitylinker<br>opennlp.tools.formats<br>opennlp.tools.formats.ad<br>opennlp.tools.formats.brat<br>opennlp.tools.formats.convert<br>opennlp.tools.formats.frenchtreebank<br>opennlp.tools.formats.muc<br>opennlp.tools.formats.ontonotes<br>opennlp.tools.lemmatizer<br>opennlp.tools.parser<br>opennlp.tools.parser.chunking<br>opennlp.tools.parser.lang.en<br>opennlp.tools.parser.lang.es<br>opennlp.tools.parser.treeinsert<br>opennlp.tools.sentdetect<br>opennlp.tools.sentdetect.lang<br>opennlp.tools.sentdetect.lang.th<br>opennlp.tools.stemmer<br>opennlp.tools.stemmer.snowball<br>opennlp.tools.tokenize.lang.en<br>org.apache.commons.imaging.color<br>org.apache.commons.imaging.common<br>org.apache.commons.imaging.common.itu_t4<br>org.apache.commons.imaging.common.mylzw<br>org.apache.commons.imaging.formats.bmp<br>org.apache.commons.imaging.formats.dcx<br>org.apache.commons.imaging.formats.gif<br>org.apache.commons.imaging.formats.icns<br>org.apache.commons.imaging.formats.ico<br>org.apache.commons.imaging.formats.jpeg<br>org.apache.commons.imaging.formats.jpeg.decoder<br>org.apache.commons.imaging.formats.jpeg.exif<br>org.apache.commons.imaging.formats.jpeg.iptc<br>org.apache.commons.imaging.formats.jpeg.segments<br>org.apache.commons.imaging.formats.jpeg.xmp<br>org.apache.commons.imaging.formats.pcx<br>org.apache.commons.imaging.formats.png<br>org.apache.commons.imaging.formats.png.chunks<br>org.apache.commons.imaging.formats.png.scanlinefilters<br>org.apache.commons.imaging.formats.png.transparencyfilters<br>org.apache.commons.imaging.formats.pnm<br>org.apache.commons.imaging.formats.psd<br>org.apache.commons.imaging.formats.psd.dataparsers<br>org.apache.commons.imaging.formats.psd.datareaders<br>org.apache.commons.imaging.formats.rgbe<br>org.apache.commons.imaging.formats.tiff<br>org.apache.commons.imaging.formats.tiff.constants<br>org.apache.commons.imaging.formats.tiff.datareaders<br>org.apache.commons.imaging.formats.tiff.fieldtypes<br>org.apache.commons.imaging.formats.tiff.photometricinterpreters<br>org.apache.commons.imaging.formats.tiff.taginfos<br>org.apache.commons.imaging.formats.tiff.write<br>org.apache.commons.imaging.formats.wbmp<br>org.apache.commons.imaging.formats.xbm<br>org.apache.commons.imaging.formats.xpm<br>org.apache.commons.imaging.icc<br>org.apache.commons.imaging.palette<br>org.apache.commons.imaging.util<br>com.adobe.dam.print.ids.utils<br>com.day.cq.dam.api.reporting<br>com.day.cq.dam.entitlement.api<br>com.day.cq.dam.handler.standard.epub<br>com.day.cq.dam.handler.standard.keynote<br>com.day.cq.dam.handler.standard.mp3<br>com.day.cq.dam.handler.standard.msoffice<br>com.day.cq.dam.handler.standard.msoffice.wmf<br>com.day.cq.dam.handler.standard.ooxml<br>com.day.cq.dam.handler.standard.pdf<br>com.day.cq.dam.handler.standard.pict<br>com.day.cq.dam.handler.standard.ps<br>com.day.cq.dam.handler.standard.psd<br>com.day.cq.dam.handler.standard.zip<br>com.day.cq.dam.word.extraction<br>com.day.cq.dam.word.process<br>com.adobe.xmp.worker.files<br>com.adobe.cq.address.api<br>com.adobe.cq.address.api.location<br>com.day.cq.mcm.emailprovider.impl.types<br>com.day.io<br>com.day.io.disk<br>com.day.io.file<br>org.apache.commons.exec.environment<br>org.apache.commons.exec.launcher<br>org.apache.commons.exec.util<br>com.google.zxing<br>com.google.zxing.common<br>com.google.zxing.common.reedsolomon<br>com.google.zxing.qrcode.decoder<br>com.google.zxing.qrcode.encoder<br>com.adobe.cq.dam.dm.internalapi.image_server<br>com.day.cq.dam.api.s7dam.jobs<br>com.day.cq.dam.api.s7dam.omnisearch<br>com.day.cq.dam.api.s7dam.scene7<br>com.day.cq.dam.scene7<br>com.day.cq.dam.scene7.api.net<br>com.day.cq.analytics.sitecatalyst.rsmerger<br>com.day.cq.searchpromote<br>com.day.cq.searchpromote.xml<br>com.day.cq.searchpromote.xml.form<br>com.day.cq.searchpromote.xml.result&gt;</td>
    <td>従来の AEM 6.x API。</td>
    <td>2019/4/8</td>
    <td>削除済み</td>
  </tr>
  <tr>
    <td>org.apache.sling.discovery.commons<br>org.apache.sling.discovery.commons.providers<br>org.apache.sling.discovery.commons.providers.base<br>org.apache.sling.discovery.commons.providers.spi<br>org.apache.sling.discovery.commons.providers.spi.base<br>org.apache.sling.discovery.commons.providers.util</td>
    <td>この API は Cloud Service ではサポートされていません。</td>
    <td>2021/9/30</td>
    <td>削除済み</td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.vault.util.xml<br>org.apache.jackrabbit.vault.util.xml.serialize</td>
    <td>Apache Xerces に関連する Util クラスは、後続のリリースで削除され、メジャーバージョンが変更されます。これらのユーティリティは Filevault の内部使用のためのものであるため、API はパブリック API サーフェスから非推奨になります。</td>
    <td>2021/9/1</td>
    <td>削除済み</td>
  <tr>
    <td>org.apache.sling.atom.taglib<br>org.apache.sling.atom.taglib.media</td>
    <td>従来の AEM 6.x API。<a href="#org.apache.abdera_or_org.apache.sling.atom.taglib">以下の削除に関するメモを参照してください。</a></td>
    <td>2019/4/8</td>
    <td>2021/9/29</td>
  </tr>
  <tr>
    <td>org.apache.felix.http.whiteboard</td>
    <td>Apache Felix Http ホワイトボードはサポートされなくなりました。コードを OSGi Http ホワイトボードに移行します。<a href="#org.apache.felix.http.whiteboard">以下の削除に関するメモを参照してください。</a></td>
    <td>2022/1/27</td>
    <td>2022/3/24</td>
  </tr>
  <tr>
    <td>org.apache.cocoon.xml.dom<br>org.apache.cocoon.xml.sax</td>
    <td>この API は非推奨（廃止予定）です。JDK が提供する XML API にコードを移行してください。</td>
    <td>2022/1/27</td>
    <td>2022/3/24</td>
  </tr>
  <tr>
    <td>ch.qos.logback.classic<br>ch.qos.logback.classic.boolex<br>ch.qos.logback.classic.db.names<br>ch.qos.logback.classic.db.script<br>ch.qos.logback.classic.encoder<br>ch.qos.logback.classic.filter<br>ch.qos.logback.classic.helpers<br>ch.qos.logback.classic.html<br>ch.qos.logback.classic.jmx<br>ch.qos.logback.classic.joran<br>ch.qos.logback.classic.joran.action<br>ch.qos.logback.classic.jul<br>ch.qos.logback.classic.layout<br>ch.qos.logback.classic.log4j<br>ch.qos.logback.classic.net<br>ch.qos.logback.classic.net.server<br>ch.qos.logback.classic.pattern<br>ch.qos.logback.classic.pattern.color<br>ch.qos.logback.classic.selector<br>ch.qos.logback.classic.selector.servlet<br>ch.qos.logback.classic.servlet<br>ch.qos.logback.classic.sift<br>ch.qos.logback.classic.spi<br>ch.qos.logback.classic.turbo<br>ch.qos.logback.classic.util<br>ch.qos.logback.core<br>ch.qos.logback.core.boolex<br>ch.qos.logback.core.encoder<br>ch.qos.logback.core.filter<br>ch.qos.logback.core.helpers<br>ch.qos.logback.core.hook<br>ch.qos.logback.core.html<br>ch.qos.logback.core.joran<br>ch.qos.logback.core.joran.action<br>ch.qos.logback.core.joran.conditional<br>ch.qos.logback.core.joran.event<br>ch.qos.logback.core.joran.event.stax<br>ch.qos.logback.core.joran.node<br>ch.qos.logback.core.joran.spi<br>ch.qos.logback.core.joran.util<br>ch.qos.logback.core.joran.util.beans<br>ch.qos.logback.core.layout<br>ch.qos.logback.core.net<br>ch.qos.logback.core.net.server<br>ch.qos.logback.core.net.ssl<br>ch.qos.logback.core.pattern<br>ch.qos.logback.core.pattern.color<br>ch.qos.logback.core.pattern.parser<br>ch.qos.logback.core.pattern.util<br>ch.qos.logback.core.property<br>ch.qos.logback.core.read<br>ch.qos.logback.core.recovery<br>ch.qos.logback.core.rolling<br>ch.qos.logback.core.rolling.helper<br>ch.qos.logback.core.sift<br>ch.qos.logback.core.spi<br>ch.qos.logback.core.status<br>ch.qos.logback.core.subst<br>ch.qos.logback.core.util</td>
    <td>この内部 logback API は、AEM as a Cloud Service ではサポートされていません。</td>
    <td>2022/1/27</td>
    <td>2022/3/24</td>
  </tr>
  <tr>
    <td>org.slf4j.spi</td>
    <td>この内部 log4j API は、AEM as a Cloud Service ではサポートされていません。</td>
    <td>2022/1/27</td>
    <td>2022/3/24</td>
  </tr>
  <tr>
    <td>org.apache.log4j<br>org.apache.log4j.helpers<br>org.apache.log4j.spi<br>org.apache.log4j.xml</td>
    <td>Apache Log4j 1 は 2015年に提供が終了し、サポートは終了しました。</td>
    <td>2022/1/27</td>
    <td>2022/3/24</td>
  </tr>
  <tr>
    <td>org.apache.sling.commons.log.logback<br>org.apache.sling.commons.log.logback.webconsole</td>
    <td>この内部 logback API は、AEM as a Cloud Service ではサポートされていません。</td>
    <td>2022/1/27</td>
    <td>削除済み</td>
  </tr>
  <tr>
    <td>com.github.jcotness.handlebars.js</td>
    <td>Handlebars のアップグレードは、セキュリティの脆弱性により、4.0.5 から 4.3.0 に必要です。 このパッケージは、アップグレードされたハンドルバーには存在しません。</td>
    <td>2022/5/5（PT）</td>
    <td>2022/8/5（PT）</td>
  </tr>
  <tr>
    <td>com.adobe.granite.resourceresolverhelper</td>
    <td>この API は、サポートされなくなりました。代わりに、org.apache.sling.api.resource.ResourceResolverFactory を使用します。</td>
    <td>2022/9/29</td>
    <td>2022/11/24</td>
  </tr>
  <tr>
    <td>com.day.cq.contentsync.handler.util</td>
    <td>この API は非推奨です。代わりに、Apache Sling のビルダーを使用します。</td>
    <td>2022/10/31</td>
    <td>2023/1/1</td>
  </tr>
  <tr><td>org.apache.sling.commons.json<br>org.apache.sling.commons.json.http<br>org.apache.sling.commons.json.io<br>org.apache.sling.commons.json.jcr<br>org.apache.sling.commons.json.sling<br>org.apache.sling.commons.json.util<br>org.apache.sling.commons.json.xml</td>
    <td>この API は AEM as a Cloud Service ではサポートされていません。</td>
    <td>2023/05/15</td>
    <td>2023/06/15</td>
  </tr><td>com.google.common.annotations<br>com.google.common.base<br>com.google.common.cache<br>com.google.common.collect<br>com.google.common.escape<br>com.google.common.eventbus<br>com.google.common.hash<br>com.google.common.html<br>com.google.common.io<br>com.google.common.math<br>com.google.common.net<br>com.google.common.primitives<br>com.google.common.reflect<br>com.google.common.util.concurrent<br>com.google.common.xml</td>
    <td>Google Guava コアライブラリは非推奨です。</td>
    <td>2023/05/15</td>
    <td>2023/06/15</td>
  </tr>
  <tr>
    <td>org.slf4j.event    </td>
    <td>この内部 slf4j API は、AEM as a Cloud Service ではサポートされていません。</td>
    <td>2022/4/11</td>
    <td>2024/08/30</td>
  </tr>
  <tr>
    <td>org.apache.sling.repoinit.jcr<br>org.apache.sling.repoinit.parser.operations</td>
    <td>この API の使用は、AEM as a Cloud Service ではサポートされていません。</td>
    <td>2024/05/17</td>
    <td>2024年6月30日（PT）</td>
  </tr>
  <tr>
    <td>com.day.cq.xss<br>com.day.cq.xss.taglib<br>com.day.cq.xss.impl</td>
    <td>代わりに、org.apache.sling.xss を使用します。</td>
    <td>2023年12月12日（PT）</td>
    <td>2024年6月30日（PT）</td>
  </tr>
  <tr>
    <td>com.adobe.granite.xss<br>com.adobe.granite.xss.impl</td>
    <td>代わりに、org.apache.sling.xss を使用します。</td>
    <td>2023年12月12日（PT）</td>
    <td>2024年6月30日（PT）</td>
  </tr>  
  <tr>
    <td>com.drew.*</td>
    <td>画像やビデオからのメタデータの抽出には、Cloud Service の Asset Compute、Apache POI または Apache Tika を使用する必要があります。</td>
    <td>2024年9月17日（PT）</td>
    <td>2024年12月17日（PT）</td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.oak.plugins.blob.*</td>
    <td></td>
    <td>2024年9月23日（PT）</td>
    <td>2024月12月23日（PT）</td>
  </tr>       
</tbody>
</table>
</details>

### `org.apache.sling.commons.auth*` の削除 {#org.apache.sling.commons.auth}

`org.apache.sling.commons.auth` や `org.apache.sling.commons.auth.spi` を使用している場合、コードをそれぞれ `org.apache.sling.auth` または。 `org.apache.sling.auth.spi` に移行することで使用を置き換えることができます。古いバージョンの [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/) を使用している場合は、最新バージョンに更新する必要があります。

アクションリスト：
* ACS AEM Commons を最新バージョンに更新
* `org.apache.sling.commons.auth` や `org.apache.sling.commons.auth.spi` から `org.apache.sling.auth` または `org.apache.sling.auth.spi` にそれぞれ移行します。

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

### `org.apache.abdera*` および `org.apache.sling.atom.taglib` の使用 {#org.apache.abdera_or_org.apache.sling.atom.taglib}

`org.apache.abdera` および `org.apache.sling.atom.taglib` のパッケージの使用を、同様の機能を備えたサードパーティライブラリまたは独自のコードに置き換えます。

アクションリスト：
* `org.apache.abdera` および `org.apache.sling.atom.taglib` のパッケージの使用を他のサードパーティライブラリ／独自のコードに置き換える。

### `org.apache.felix.http.whiteboard` の使用 {#org.apache.felix.http.whiteboard}

`org.apache.felix.http.whiteboard` の使用を [OSGi Http ホワイトボード](https://docs.osgi.org/specification/osgi.cmpn/7.0.0/service.http.whiteboard.html)に置き換えます。公式の OSGi API には同様の機能があり、ほとんどの場合、置き換えにはサービス登録プロパティの変更のみが必要です。

アクションリスト：
* `org.apache.felix.http.whiteboard` の使用を [OSGi Http ホワイトボード](https://docs.osgi.org/specification/osgi.cmpn/7.0.0/service.http.whiteboard.html)に置き換える

## OSGi 設定 {#osgi-configuration}

次の 2 つのリストは、AEM as a Cloud Service の OSGi 設定サーフェスを反映しており、顧客が設定できる内容を示しています。

1. 顧客コードで設定してはいけない OSGi 設定のリスト
1. プロパティを設定できるが、示されている検証ルールに従う必要がある OSGi 設定のリスト。これらのルールには、プロパティの宣言が必須かどうか、プロパティの型、場合によっては許容される値の範囲が許可されます。

OSGi 設定がリストに表示されない場合は、顧客コードで設定できます。

これらのルールは、Cloud Manager のビルドプロセス中に検証されます。今後、ルールが追加される可能性があり、その実施予定日が表に記載されています。顧客は、目標の実施日までにこれらのルールを遵守する必要があります。削除日の後にルールに従わないと、Cloud Manager のビルドプロセスでエラーが発生します。ローカル SDK の開発中に OSGI 設定エラーにフラグを付けるには、Maven プロジェクトに [AEM as a Maven SDK Build Analyzer Maven プラグイン](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=ja) を含める必要があります。

OSGI 設定に関する追加情報は、[この場所](/help/implementing/deploying/configuring-osgi.md)にあります。

+++変更できない OSGi 設定。
* **`org.apache.felix.webconsole.internal.servlet.OsgiManager`**（発表日：4/30/2021、施行日：7/31/2021）
* **`com.day.cq.auth.impl.cug.CugSupportImpl`**（発表日：4/30/2021、施行日：7/31/2021）
* **`com.day.cq.jcrclustersupport.ClusterStartLevelController`**（発表日：4/30/2021、施行日：7/31/2021）
* **`org.apache.felix.http (Factory)`**（発表日：4/30/2021、施行日：7/31/2021）
* **`org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`**（発表日：8/25/2021、施行日：11/26/2021）
+++

+++ビルド検証ルールの対象となる OSGi 設定。
* **`org.apache.felix.eventadmin.impl.EventAdmin`**（発表日：4/30/2021、施行日：7/31/2021）
* `org.apache.felix.eventadmin.ThreadPoolSize`
   * 型：integer
   * 要求範囲：2 ～ 100
* `org.apache.felix.eventadmin.AsyncToSyncThreadRatio`
   * 型：double
* `org.apache.felix.eventadmin.Timeout`
   * 型：integer
* `org.apache.felix.eventadmin.RequireTopic`
   * 型：boolean
* `org.apache.felix.eventadmin.IgnoreTimeout`
   * 必須
   * 型：文字列の配列
   * 要求範囲：少なくとも `org.apache.felix*`、`org.apache.sling*`、`come.day*`、`com.adobe*` をすべてを含める必要があります。
* `org.apache.felix.eventadmin.IgnoreTopic`
   * 型：文字列の配列
* **`org.apache.felix.http`**（発表日：4/30/2021、施行日：7/31/2021）
   * `org.apache.felix.http.timeout`
      * 型：integer
   * `org.apache.felix.http.session.timeout`
      * 型：integer
   * `org.apache.felix.http.jetty.threadpool.max`
      * 型：integer
   * `org.apache.felix.http.jetty.headerBufferSize`
      * 型：integer
   * `org.apache.felix.http.jetty.requestBufferSize`
      * 型：integer
   * `org.apache.felix.http.jetty.responseBufferSize`
      * 型：integer
   * `org.apache.felix.http.jetty.maxFormSize`
      * 型：integer
   * `org.apache.felix.https.jetty.session.cookie.httpOnly`
      * 型：boolean
   * `org.apache.felix.https.jetty.session.cookie.secure`
      * 型：boolean
   * `org.eclipse.jetty.servlet.SessionIdPathParameterName`
      * 型：string
   * `org.eclipse.jetty.servlet.CheckingRemoteSessionIdEncoding`
      * 型：boolean
   * `org.eclipse.jetty.servlet.SessionCookie`
      * 型：string
   * `org.eclipse.jetty.servlet.SessionDomain`
      * 型：string
   * `org.eclipse.jetty.servlet.SessionPath`
      * 型：string
   * `org.eclipse.jetty.servlet.MaxAge`
      * 型：integer
   * `org.eclipse.jetty.servlet.SessionScavengingInterval`
      * 型：integer
   * `org.apache.felix.jetty.gziphandler.enable`
      * 型：boolean
   * `org.apache.felix.jetty.gzip.minGzipSize`
      * 型：integer
   * `org.apache.felix.jetty.gzip.compressionLevel`
      * 型：integer
   * `org.apache.felix.jetty.gzip.inflateBufferSize`
      * 型：integer
   * `org.apache.felix.jetty.gzip.syncFlush`
      * 型：boolean
   * `org.apache.felix.jetty.gzip.excludedUserAgents`
      * 型：string
   * `org.apache.felix.jetty.gzip.includedMethods`
      * 型：文字列の配列
   * `org.apache.felix.jetty.gzip.excludedMethods`
      * 型：文字列の配列
   * `org.apache.felix.jetty.gzip.includedPaths`
      * 型：文字列の配列
   * `org.apache.felix.jetty.gzip.excludedPaths`
      * 型：文字列の配列
   * `org.apache.felix.jetty.gzip.includedMimeTypes`
      * 型：文字列の配列
   * `org.apache.felix.jetty.gzip.excludedMimeTypes`
      * 型：文字列の配列
   * `org.apache.felix.http.session.invalidate`
      * 型：boolean
   * `org.apache.felix.http.session.container.attribute`
      * 型：文字列の配列
   * `org.apache.felix.http.session.uniqueid`
      * 型：boolean
* **`org.apache.sling.scripting.cache`**（発表日：4/30/2021、施行日：7/31/2021）
   * `org.apache.sling.scripting.cache.size`
      * 型：integer
      * 要求範囲：>= 2048
   * `org.apache.sling.scripting.cache.additional_extensions`
      * 必須
      * 型：文字列の配列
      * 要求範囲：js を含める必要があります
* **`com.day.cq.mailer.DefaultMailService`**（発表日：4/30/2021、施行日：7/31/2021）
   * `smtp.host`
      * 型：string
   * `smtp.port`
      * 型：integer
      * 要求範囲：465、587、25 のいずれか
   * `smtp.user`
      * 型：string
   * `smtp.password`
      * 型：string
   * `from.address`
      * 型：string
   * `smtp.ssl`
      * 型：string
   * `smtp.starttls`
      * 型：boolean
   * `smtp.requiretls`
      * 型：boolean
   * `debug.email`
      * 型：boolean
   * `oauth.flow`
      * 型：boolean
* **`org.apache.sling.commons.log.LogManager.factory.config`**（発表日：21/11/16、施行日：21/2/16）
   * `org.apache.sling.commons.log.level`
      * タイプ：列挙
      * 必須範囲：情報、デバッグ、TRACE
   * `org.apache.sling.commons.log.names`
      * 型：string
   * `org.apache.sling.commons.log.file`
      * 型：string
   * `org.apache.sling.commons.log.additiv`
      * 型：boolean
+++

## Java ランタイムのバージョン 21 へのアップデート {#java-runtime-update-21}

AEM as a Cloud Service は Java 21 ランタイムに移行します。互換性を確保するには、次の調整を行うことが不可欠です。

### ランタイム要件

これらの調整は、Java 21 ランタイムとの互換性を確保するために必要です。 ライブラリは、古いバージョンの Java と互換性があるので、いつでも更新できます。

#### org.objectweb.asm の最小バージョン {#org.objectweb.asm}

新しい JVM ランタイムのサポートを確保するには、org.objectweb.asm の使用をバージョン 9.5 以降に更新します。

#### org.apache.groovy の最小バージョン {#org.apache.groovy}

新しい JVM ランタイムのサポートを確保するには、org.apache.groovy の使用をバージョン 4.0.22 以降に更新します。

このバンドルは、AEM Groovy コンソールなどのサードパーティの依存関係を追加することで間接的に含めることができます。

### ビルド時間の要件

これらの調整は、新しいバージョンの Java でプロジェクトを構築できるようにするために必要ですが、実行時の互換性には必要ありません。 Maven プラグインは、古いバージョンの Java と互換性があるので、いつでも更新できます。

#### bnd-maven-plugin の最小バージョン {#bnd-maven-plugin}

bnd-maven-plugin の使用方法をバージョン 6.4.0 に更新して、新しい JVM ランタイムがサポートされるようにします。 バージョン 7 以降は Java 11 以下と互換性がないので、現時点ではそのバージョンへのアップグレードは推奨されません。

#### aemanalyzer-maven-plugin の最小バージョン {#aemanalyser-maven-plugin}

aemanalyzer-maven-plugin の使用をバージョン 1.6.6 以降に更新して、新しい JVM ランタイムがサポートされるようにします。

#### Maven-bundle-plugin の最小バージョン  {#maven-bundle-plugin}

新しい JVM ランタイムがサポートされるように、maven-bundle-plugin の使用方法をバージョン 5.1.5 以降に更新します。

#### maven-scr-plugin の依存関係の更新  {#maven-scr-plugin}

`maven-scr-plugin` は Java 17 および 21 と直接互換性がありません。 ただし、以下のスニペットのように、プラグイン設定内で ASM 依存関係バージョンを更新することで、記述子ファイルを生成することは可能です。

```
[source,xml]
 <project>
   ...
   <build>
     ...
     <plugins>
       ...
       <plugin>
         <groupId>org.apache.felix</groupId>
         <artifactId>maven-scr-plugin</artifactId>
         <version>1.26.4</version>
         <executions>
           <execution>
             <id>generate-scr-scrdescriptor</id>
             <goals>
               <goal>scr</goal>
             </goals>
           </execution>
         </executions>
         <dependencies>
           <dependency>
             <groupId>org.ow2.asm</groupId>
             <artifactId>asm-analysis</artifactId>
             <version>9.7.1</version>
             <scope>compile</scope>
           </dependency>
         </dependencies>
       </plugin>
       ...
     </plugins>
     ...
   </build>
   ...
 </project>
```
