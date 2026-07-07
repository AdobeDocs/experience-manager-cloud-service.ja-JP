---
title: OpenAPI機能を備えたDynamic Mediaを使用してバニティ URLを作成する
description: Dynamic Media OpenAPI機能を使用して、長いアセット配信URLを、ブランド化された短いバニティ URLに変換します。 バニティ URLは、複雑な配信URLの短く、クリーンで、覚えやすく、読みやすいバージョンです。 バニティ URLには、ブランド名、商品名、関連キーワードを含めることができるため、ブランドの可視性とユーザーエンゲージメントを向上させることができます
role: Admin
feature: Asset Management, Publishing, Collaboration, Asset Processing
badgeSaas: label="AEM Assets" type="Positive" tooltip="AEM Assetsに適用）。"
exl-id: 596136e9-7c2a-43a1-8091-2d8b6226b695
source-git-commit: bcdfc9bb418ab405faa82c55820a6ec6062c2b17
workflow-type: tm+mt
source-wordcount: '1510'
ht-degree: 5%

---

# バニティ URLを使用{#vanity-urls}

[!DNL Dynamic Media with OpenAPI capabilities]を使用して、長いアセット配信URLを、ブランド化された短いバニティ URLに変換します。 標準的なアセット配信URLには、配信URLを複雑にし、覚えにくく、共有しにくくするシステム生成のアセット UUIDが含まれています。 これらのアセットのUUIDをバニティ URLを生成するためにシンプルな識別子（バニティ ID）に置き換えます。 バニティ URLは、複雑な配信URLの短く、クリーンで読みやすいバージョンです。

違いを理解するには、次のURL形式を参照してください。

* [標準配信URL](#standard-urls)
* [バニティ URL](#vanity-url)

標準的な配信URLでは`aaid`に続いてUUIDが使用され、バニティ URLでは`avid`に続いてカスタム識別子（バニティ識別子）が使用されます。

短くてシンプルなバニティ IDを使用して、バニティ URLを短く、クリーンで、読みやすく、覚えやすく、共有します。 ブランドの可視性とユーザーエンゲージメントを向上させるために、ブランド名、商品名、関連性の高いキーワードをバニティ IDとして使用します。

ユーザーがバニティ URLをクリックすると、[!DNL Dynamic Media with OpenAPI]は取り込み時に元のアセットの場所に自動的にマッピングされ、配信時に適切に解決され、ユーザーにアセットがサーバーされます。

[ バニティ URLの作成](#create-vanity-urls)について説明します。

## 標準配信URL{#standard-urls}

標準の[!DNL Dynamic Media with OpenAPI] アセット配信URLには、システムで生成された一意の識別子が含まれており、次の形式に従っています。

***形式：*** `https://delivery-<tenant>.adobeaemcloud.com/adobe/assets/urn:aaid:aem:<asset-uuid>/as/<seoname>.<format>`

標準の配信URLには、`urn:`の後の`aaid` （*実際のアセット識別子*）と`urn:aaid:aem:`から`/as/<seoname>.<format>`の間のUUIDが含まれています。

***例：*** `https://delivery-p30902-e145436.adobeaemcloud.com/adobe/assets/urn:aaid:aem:43341ab1-4086-44d2-b7ce-ee546c35613b/as/check.jpeg`

上記の例では、`43341ab1-4086-44d2-b7ce-ee546c35613b`はUUIDです。

## バニティ URL{#vanity-url}

バニティ URLには、アセット UUIDの代わりにバニティ IDが含まれ、次の形式に従います。

***形式：*** `https://delivery-<tenant>.adobeaemcloud.com/adobe/assets/urn:avid:aem:<vanity-id>/as/<seoname>.<format>`

バニティ URLには、`urn:`の後の`avid` （*実際のバニティ ID*）と`urn:avid:aem:`から`/<seoname>.<format>`の間のバニティ IDが含まれています。

***例：*** `https://delivery-p30902-e145436.adobeaemcloud.com/adobe/assets/urn:avid:aem:VanityCheck/as/check.jpeg`

上記の例では、`VanityCheck`はUUIDを置き換えたバニティ IDです。

## 主な機能とメリット{#capabilities-and-benefits-of-vanity-urls}

有意義なバニティ IDを使用して、標準的なアセット配信URLをカスタマイズすることで、いくつかの利点と測定可能な影響がもたらされます。 バニティ URLの主な機能と利点には、次のようなものがあります。

### 主な機能{#key-capabilities}

* **URL カスタマイズ：**&#x200B;配信URLの長い識別子（アセット UUID）を、ブランドに沿った短い代替案に置き換えて、よりクリーンな配信URLを生成します。
* **リアルタイムのリダイレクト：** バニティ URLは、ワークフローを中断することなく、実行時に元のアセット UUIDにリダイレクトされます。 ユーザーはアドレスバーにクリーンなURLを表示し、システムは技術的なルーティングを処理します。
* **簡単なリンク管理：** アセット配信のパフォーマンスに影響を与えることなく、バニティ URLをいつでもカスタマイズできます。

### 主な特長{#key-benefits}

* **ユーザーエクスペリエンスの向上：** クリーンで短いバニティ URLは、読みやすく、ユーザーフレンドリーで、覚えやすく、共有しやすいものです。

* **ユーザーのエンゲージメントを向上：** ブランド URLは、ユーザーの信頼と信用を構築します。 オーディエンスがブランド付きのプロフェッショナルなリンクをクリックする可能性が高く、その結果、クリック率が高まります。

* **SEO最適化：**&#x200B;関連キーワードを含むURLは、検索エンジンのランキングと見つけやすさを向上させます。

* **拡張ブランドの可視性:** ブランド固有のURLは、電子メール、ソーシャルメディア、広告キャンペーンなど、あらゆるマーケティングチャネルをまたいでブランドプレゼンスを強化します。また、あらゆるコミュニケーションでブランド URLを一貫性のある方法で使用することで、ブランドアイデンティティと認知度を強化できます。

* **キャンペーンのトラッキングと分析：**&#x200B;様々なキャンペーンやチャネルに対して一意のバニティ URLを使用して、トラフィックソースとコンバージョンのパフォーマンスに関する詳細なインサイトを得ることができます。

## 前提条件{#prerequisites-for-creating-vanity-id}

バニティ URLを作成するには、[公開配信のアセットを既に承認していることを確認してください](/help/assets/manage-organize-assets-view.md#manage-asset-status)。

## バニティ URLの作成{#create-vanity-urls}

バニティ URLを作成するには、次の手順を実行します。

1. [アセットメタデータの設定](#set-up-asset-metadata)
1. [Cloud manager環境変数の作成とマッピング](#map-cloud-manager-environment-variable)
1. [配信にバニティ URLを必要とするアセットの承認](/help/assets/manage-organize-assets-view.md#manage-asset-status)
1. [バニティ URLの生成](#generate-vanity-urls)

### アセットメタデータの設定{#set-up-asset-metadata}

アセットのメタデータフォームにバニティ IDを設定するには、次の手順を実行します。

1. アセットを保持するフォルダーの詳細ページに移動して、[!DNL Dynamic Media with OpenAPI]配信を行います。
1. [次のいずれかの操作を行って、そのメタデータフォーム ](/help/assets/metadata-assets-view.md#edit-metadata-forms)を編集します。

   * 新しいメタデータフィールドを追加し、必須のバニティ IDをそのフィールドの値として指定します。
   * 既存のメタデータプロパティの値を必要なバニティ IDに置き換えて、既存のフィールドを更新します。 バニティ IDを作成するための[ ベストプラクティス ](#best-practices)について説明します。

   ![ バニティ ID](/help/assets/assets/vanity-id-metadata.png)

   詳しくは[メタデータスキーマ](/help/assets/metadata-schemas.md)を参照してください。

   >[!NOTE]
   >
   > * 各アセットに一意のバニティ IDを使用します。 同じメタデータフォームを共有するアセットが、バニティ URLを介したOpenAPI配信を備えたDM用の一意のバニティ IDを持っていることを常に確認します。 2つのアセットが同じバニティ IDを共有する場合、OpenAPIを使用したDMは、そのIDを最近受信したアセットを配信し、そのIDの以前の使用権限を別のアセットに上書きします。
   >
   > * 1つのアセットに複数のバニティ IDを含めることができます。 [Adobe サポート ](https://helpx.adobe.com/jp/contact.html)に連絡し、必要なバニティ IDの生成をリクエストします。

アセットメタデータフォームでバニティ IDを設定した後、[このメタデータフィールドをシステムの配信メカニズム ](#map-cloud-manager-environment-variable)にマッピングします。

### Cloud manager環境変数の作成とマッピング{#map-cloud-manager-environment-variable}

次の手順を実行して環境変数を作成し、バニティ IDを保持するメタデータフィールドにマッピングします。

1. [Cloud Manager環境](/help/implementing/cloud-manager/environment-variables.md)の設定ページに移動し、次の操作を行います。
   1. `ASSET_DELIVERY_VANITY_ID`変数を追加します。 これは重要なポイントです。
   1. 値フィールドを使用して、バニティ IDを保持するアセットメタデータプロパティにマッピングします。 マッピングは`dc:<your-metadata-property>`形式に従います。ここで、メタデータマッピングの接頭辞（dcなど）は、アセットメタデータ設定プロパティによって異なります。      ![ASSET_DELIVERY_VANITY_ID変数](/help/assets/assets/environment-config.png)
1. 変更を保存して、環境でポッドを再起動します。

### 配信のためのアセットの承認{#approve-assets-for-delivery}

Cloud Manager環境の`ASSET_DELIVERY_VANITY_ID`変数を、バニティ IDを保持するアセットメタデータプロパティにマッピングした後、[配信にバニティ URLを必要とするアセットを承認](/help/assets/manage-organize-assets-view.md#manage-asset-status)します。

### バニティ URLの生成{#generate-vanity-urls}

標準的な配信URLで次の置き換えを行い、バニティ URLに変換します。

* **UUID**&#x200B;を&#x200B;**バニティ ID**&#x200B;に置き換えます。
* `aaid`を`avid`に置き換えます。

上記の[URLの標準からバニティ URL](#standard-urls)への変換を参照してください。アセットのOpenAPI配信URL](/help/assets/approve-assets.md#copy-delivery-url-for-approved-assets)を使用してDynamic Mediaを[ コピーする方法について説明します。

ユーザーがバニティ URLをクリックすると、[!DNL Dynamic Media with OpenAPI]は取り込み時にバニティ IDを元のアセット UUIDに自動的にマッピングし、配信時に適切に解決して、アセットをユーザーに遅延なく提供します。 アセット配信のパフォーマンスに影響を与えることなく、バニティ URLをリアルタイムでカスタマイズできます。

[ バニティ URLでAEM Cloud Serviceの高度なカスタマイズ機能を使用して、その影響を強化します](#scale-using-vanity-url)。

## バニティ URLを使用して拡大・縮小{#scale-using-vanity-url}

AEM as a Cloud Serviceを使用すると、web アドレス内で[DNS名とCDN名](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/introduction)をカスタマイズできます。 これらのAEMCS機能をバニティ URLと組み合わせて使用すると、クリーンで記述的で、ブランド化され、直感的で、前述の[のメリット ](#key-benefits)を提供する一意のweb アドレスに変換できます。

次のバニティ URLとカスタマイズ可能なコンポーネントを参照してください。

**バニティ URL形式：**

`https://delivery-<tenant>.adobeaemcloud.com/adobe/assets/urn:avid:aem:<vanity-id>/as/<seoname>.<format>`

<table style="border-collapse:collapse; table-layout:auto; width:auto;">
<tr valign="top">
<td style="padding:0 4px; white-space:nowrap; text-align:center;">
<div style="text-align:left;"><code>https://delivery&#8209;&lt;tenant&gt;.adobeaemcloud.com</code></div>
<div style="text-align:center;">↓</div>
<div style="text-align:center;"><a href="#customize-dns">このDNSをカスタマイズ </a></div>
</td>
<td style="padding:0 6px; white-space:nowrap; text-align:center;">／</td>
<td style="padding:0 4px; white-space:nowrap; text-align:center;">
<div style="text-align:left;"><code>adobe/assets/urn:avid:aem:</code></div>
<div style="text-align:center;">↓</div>
<div style="text-align:center;"><a href="#rewrite-cdn-rules">書き換えルールを使用してURLをカスタマイズ </a></div>
</td>
<td style="padding:0 4px; white-space:nowrap; text-align:center;">
<div style="text-align:left;"><code>&lt;vanity-id&gt;</code></div>
<div style="text-align:center;">↓</div>
<div style="text-align:center;"><a href="#create-vanity-urls"> バニティ IDを作成</a></div>
</td>
<td style="padding:0 4px; white-space:nowrap; text-align:left; width:1%;">
<code>/as/&lt;seoname&gt;.&lt;format&gt;</code>
</td>
</tr>
</table>

カスタマイズされたDNS名とCDN名を持つ&#x200B;**バニティ URL形式：**

`https://<custom-dns>` `/` `dam/assets/` `<vanity-id>` `/as/<seoname>.<format>`

**カスタマイズ可能なURL コンポーネント**

* ***[DNS名（ホスト名）:](#customize-DNS)*** `https://delivery-<tenant>.adobeaemcloud.com`は、アセットをホストするサーバードメインです。 [ ホスト名を変更するには、DNSをカスタマイズしてください](#customize-DNS)。
* ***[CDN書き換えルール：](#rewrite-cdn-rules)*** `adobe/assets/urn:avid:aem:`は、アセットの種類と配信方法を識別するパス構造です。 [CDN ルール ](#rewrite-cdn-rules)を書き換えて、ドメイン パスを変更します。

### DNSのカスタマイズ{#customize-dns}

[Adobe サポート ](https://helpx.adobe.com/jp/contact.html)にリクエストを送信して、配信層に必要なカスタム DNSを生成します。 カスタム DNS名を作成するには、次の[ ベストプラクティス ](#best-practices)に従ってください。

### CDN ルールの書き換え{#rewrite-cdn-rules}

配信のCDN ルールを書き換えるには、次の手順を実行します。

1. AEM リポジトリに移動して、YAML設定ファイルを作成します。
2. 「[setup](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-error-pages#setup)」セクションの手順を実行してCDN ルールを設定し、Cloud Manager設定パイプラインを介して設定をデプロイします。ドメインパスを作成するには、次の[ ベストプラクティス ](#best-practices)に従ってください。   [CDN ルールの書き換えについて詳しく見る](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-configuring-traffic#request-transformations)。

バニティ URLに拡張子を付けたファイル名を追加する書き換えルールの例を次に示します。 特定の要件に従ってこれらの書き換えルールをカスタマイズします。 [詳しくは、Adobe サポート ](https://helpx.adobe.com/jp/contact.html)にお問い合わせください：

```- name: cdn-rewrite-rule
  when:
    allOf:
      - reqProperty: tier
        equals: delivery
```

#### SVG、GIF、PDFの場合 {#svg-gif-pdf}

```
    type: transform
      reqProperty: path
      op: replace
      match: ^/dam/assets/([^/]+\.(?:svg|gif|pdf|docx|xlsx))(\?.*)?$
      replacement: /adobe/assets/urn:avid:aem:\1/original/as/\1\2
```

#### ビデオの場合{#video}

MP4、MOV、AVI、MKVなどのビデオの場合

```
type: transform
      reqProperty: path
      op: replace
      match: ^/dam/assets/([^/]+\.(?:mp4|mov|avi|mkv))(\?.*)?$
      replacement: /adobe/assets/urn:avid:aem:\1/play\2
```

#### 画像用{#image}

SVGを除くすべての画像タイプ。

```
type: transform
      reqProperty: path
      op: replace
      match: ^/dam/assets/([^/]+\.[^/]+)(\?.*)?$
      replacement: /adobe/assets/urn:avid:aem:\1/as/\1\2
```

## クリーンなバニティ URLを作成するためのベストプラクティスに従ってください{#best-practices}

[ バニティ ID](#create-vanity-urls)、[ カスタム DNS](#customize-dns)、[CDN名](#rewrite-cdn-rules)を作成するには、次のベストプラクティスに従ってください。

1. スペース、スラッシュ、ハイフンなどのバニティ IDでは、特殊文字を使用しないでください。 システムは、定義済みのマッピングを使用して、バニティ IDの特殊文字を置き換えます。
1. [ バニティ ID](#create-vanity-urls)、[ カスタム DNS](#customize-dns)、[CDN名](#rewrite-cdn-rules)でブランド名、製品名、関連キーワードを使用して、ブランドの可視性とユーザーのエンゲージメントを向上させます。
1. 意味を表す短い単語や文字列を使いましょう。
1. クリック数を増やすためにユーザーを招待するテキストを使用します。


**関連情報**

* [アセットを翻訳](/help/assets/translate-assets.md)
* [Assets HTTP API](/help/assets/mac-api-assets.md)
* [AEM Assets as a Cloud Service でサポートされているファイル形式](/help/assets/file-format-support.md)
* [アセットを検索](/help/assets/search-assets.md)
* [接続されたアセット](/help/assets/use-assets-across-connected-assets-instances.md)
* [アセットレポート](/help/assets/asset-reports.md)
* [メタデータスキーマ](/help/assets/metadata-schemas.md)
* [アセットをダウンロード](/help/assets/download-assets-from-aem.md)
* [メタデータを管理](/help/assets/manage-metadata.md)
* [Dynamic Media テンプレートの管理](/help/assets/dynamic-media/manage-dynamic-media-templates.md)
* [レポートの管理](/help/assets/manage-reports-assets-view.md)
* [検索ファセット](/help/assets/search-facets.md)
* [コレクションを管理](/help/assets/manage-collections.md)
* [メタデータの一括読み込み](/help/assets/metadata-import-export.md)
* [AEM および Dynamic Media へのアセットの公開](/help/assets/publish-assets-to-aem-and-dm.md)

