---
title: OpenAPI 機能を備えた Dynamic Media を使用したバニティー URL の作成
description: Dynamic Media OpenAPI 機能を使用して、長いアセット配信 URL を短いブランドのバニティー URL に変換します。 バニティー URL は、複雑な配信 URL の短く、クリーンで、覚えやすく、読みやすいバージョンです。 バニティ URL には、ブランド名、製品名および関連キーワードを含めて、ブランドの可視性とユーザーエンゲージメントを高めることができます
role: Admin
feature: Asset Management, Publishing, Collaboration, Asset Processing
source-git-commit: 73574b3358451dfe135b91011abb5cad372a783e
workflow-type: tm+mt
source-wordcount: '1377'
ht-degree: 0%

---


# バニティ URL を使用しますか？{#vanity-urls}

[!DNL Dynamic Media OpenAPI capabilities] を使用すると、長いアセット配信 URL を短いブランドのバニティ URL に変換できます。 標準のアセット配信 URL には、システム生成のアセット UUID が含まれています。このアセット UUID が配信 URL を複雑にし、覚えておいたり共有したりするのが困難になります。 これらのアセット UUID を単純な識別子（バニティ ID）に置き換えて、バニティ URL を生成します。 バニティ URL は、複雑な配信 URL の短く、クリーンで読みやすいバージョンです。

その違いを理解するには、次の URL 形式を参照してください。
* [標準配信 URL](#standard-urls)
* [バニティ URL](#vanity-url)

標準の配信 URL では、`aaid` の後に UUID を使用し、バニティ URL では、`avid` の後にカスタム識別子（バニティ識別子）を使用します。

短くシンプルなバニティ識別子を使用して、配信 URL を短く、クリーンで、読みやすく、覚えやすく、共有します。 ブランド名、製品名および関連するキーワードをバニティ ID として使用して、ブランドの可視性とユーザーエンゲージメントを高めます。

ユーザーがバニティー URL をクリックすると、[!DNL Dynamic Media with OpenAPI] は取り込み時に元のアセットの場所に自動的にマッピングし、配信時に適切に解決して、アセットをユーザーにサーバーします。

[ バニティ URL の作成 ](#create-vanity-urls) の詳細情報

## 標準配信 URL{#standard-urls}

標準の [!DNL Dynamic Media with OpenAPI] アセット配信 URL は、一意のシステム生成識別子を含み、次の形式に従います。

***形式：*** `https://delivery-<tenant>.adobeaemcloud.com/adobe/assets/urn:aaid:aem:<asset-uuid>/as/<seoname>.<format>`

標準配信 URL には、`aaid` の後の *（* 実際のアセット識別子 `urn:`）と、`urn:aaid:aem:` から `/as/<seoname>.<format>` の間の UUID が含まれます。

***例：*** `https://delivery-p30902-e145436.adobeaemcloud.com/adobe/assets/urn:aaid:aem:43341ab1-4086-44d2-b7ce-ee546c35613b/as/check.jpeg`

上記の例では、`43341ab1-4086-44d2-b7ce-ee546c35613b` は UUID です。

## バニティ URL{#vanity-url}

バニティ URL は、アセット UUID の代わりにバニティ識別子を含み、次の形式に従います。

***形式：*** `https://delivery-<tenant>.adobeaemcloud.com/adobe/assets/urn:avid:aem:<vanity-id>/<seoname>.<format>`

バニティ URL には、`avid` の後の *（* 実際のバニティ識別子 `urn:`）と、`urn:avid:aem:` から `/<seoname>.<format>` の間のバニティ ID が含まれます。

***例：*** `https://delivery-p30902-e145436.adobeaemcloud.com/adobe/assets/urn:avid:aem:VanityCheck/as/check.jpeg`

上記の例では、`VanityCheck` は UUID を置き換えたバニティ ID です。

## 主な機能とメリットを確認{#capabilities-and-benefits-of-vanity-urls}

意味のあるバニティ ID を使用して標準のアセット配信 URL をカスタマイズすると、いくつかの利点と測定可能な影響があります。 バニティ URL の主な機能と利点には、次のようなものがあります。

### 主な機能{#key-capabilities}

* **URL のカスタマイズ：** 配信 URL の長い識別子（アセット UUID）を、ブランドに合わせた短い代替値に置き換えて、よりクリーンな配信 URL を生成します。
* **リアルタイムリダイレクト：** バニティ URL は、ワークフローを中断することなく、実行時に元のアセット UUID にリダイレクトされます。 システムが技術的なルーティングを処理している間、ユーザーにはアドレスバーにクリーンな URL が表示される。
* **簡単なリンク管理：** アセット配信のパフォーマンスに影響を与えることなく、バニティ URL をいつでもカスタマイズできます。

### 主なメリット{#key-benefits}

* **ユーザーエクスペリエンスを向上：** クリーンで短いバニティ URL は、読みやすく、使いやすく、覚えやすく、共有しやすいです。

* **ユーザーエンゲージメントを向上：** ブランド URL はユーザーの信頼性と信頼を構築します。 ユーザーがクリックする可能性が高く、専門的なブランドリンクをクリックする可能性が高くなり、クリックスルー率が高くなります。

* **SEO の最適化：関連するキーワードを含む** URL は、検索エンジンのランキングと検出性を向上させます。

* **ブランドの可視性の向上：** ブランド固有の URL により、メール、ソーシャルメディア、広告キャンペーンを含むすべてのマーケティングチャネルでブランドのプレゼンスが強化されます。
また、すべての通信でブランド URL を一貫して使用すると、ブランドのアイデンティティと認識が強化されます。

* **キャンペーントラッキングと分析：** 様々なキャンペーンやチャネルに固有のバニティ URL を使用して、トラフィックソースとコンバージョンパフォーマンスに関する詳細なインサイトを得ます。

## 前提条件{#prerequisites-for-creating-vanity-id}

バニティー URL を作成するには、アセットが既に [ 公開配信用に承認 ](/help/assets/manage-organize-assets-view.md#manage-asset-status) されていることを確認します。

## バニティー URL の作成{#create-vanity-urls}

バニティ URL を作成するには、次の手順を実行します。
1. [アセットメタデータの設定](#set-up-asset-metadata)
1. [Cloud Manager 環境変数の作成とマッピング](#map-cloud-manager-environment-variable)
1. [配信にバニティ URL を必要とするアセットを承認](/help/assets/manage-organize-assets-view.md#manage-asset-status)
1. [バニティ URL を生成](#generate-vanity-urls)

### アセットメタデータの設定{#set-up-asset-metadata}

次の手順を実行して、アセットのメタデータフォームにバニティ ID を設定します。
1. 配信用のアセットを保持しているフォルダーの詳細ページ [!DNL Dynamic Media with OpenAPI] 移動します。
1. 次のいずれかの操作を行って [ そのメタデータフォームを編集します ](/help/assets/metadata-assets-view.md#edit-metadata-forms)。
   * 新しいメタデータフィールドを追加し、必要なバニティ ID をそのフィールドの値として指定します。
   * 既存のメタデータプロパティの値を必要なバニティ ID に置き換えて、既存のフィールドを更新します。 バニティ ID を作成するための [ ベストプラクティス ](#best-practices) について説明します。
     ![ バニティ ID](/help/assets/assets/vanity-id-metadata.png)
詳しくは、[ メタデータスキーマ ](/help/assets/metadata-schemas.md) を参照してください。

     >[!NOTE]
     >
     > * 各アセットに一意のバニティ ID を使用します。 同じメタデータフォームを共有するアセットに、バニティ URL を介して OpenAPI 配信される DM 用の一意のバニティ ID があることを必ず確認してください。 2 つのアセットが同じバニティ ID を共有する場合、OpenAPI を使用する DM は、最新にその ID を受信したアセットを配信し、ID の以前の使用権限を別のアセットに上書きします。
     >
     > * 1 つのアセットに複数のバニティ ID を含めることができます。 [Adobe サポートに連絡 ](https://helpx.adobe.com/jp/contact.html) し、必要なバニティ ID を生成するようリクエストを送信します。

アセットメタデータフォームでバニティ ID を設定したら、[ このメタデータフィールドをシステムの配信メカニズムにマッピング ](#map-cloud-manager-environment-variable) します。

### Cloud Manager 環境変数の作成とマッピング{#map-cloud-manager-environment-variable}

次の手順を実行して環境変数を作成し、バニティ ID を保持するメタデータフィールドにマッピングします。

1. [Cloud Manager環境の設定ページに移動して ](/help/implementing/cloud-manager/environment-variables.md) 次の手順を実行します。
   1. 変数 `ASSET_DELIVERY_VANITY_ID` 追加します。 これが鍵です。
   1. 値フィールドを使用して、バニティ ID を保持するメタデータプロパティにマッピングします。 マッピングは `dc:<your-metadata-property>` 形式に従います。ここで、メタデータマッピングプレフィックス（dc：など）は、メタデータ設定プロパティによって異なります。
      ![ASSET_DELIVERY_VANITY_ID 変数 ](/help/assets/assets/environment-config.png)
1. 変更を保存し、環境内のポッドを再起動します。

### 配信するアセットの承認{#approve-assets-for-delivery}

Cloud Manager環境の `ASSET_DELIVERY_VANITY_ID` 変数を、バニティ ID を保持するアセットメタデータプロパティにマッピングしたら、[ 配信にバニティ URL を必要とするアセットを承認 ](/help/assets/manage-organize-assets-view.md#manage-asset-status) します。

### バニティ URL を生成{#generate-vanity-urls}

標準の配信 URL をバニティー URL に変換するには、次のように置き換えます。

* **UUID** を **バニティ ID** に置き換えます。
* `aaid` を `avid` に置き換えます。

上記の [ 標準からバニティ URL への URL 変換 ](#standard-urls) を参照してください。
アセットの [Dynamic Media を OpenAPI 配信 URL と共にコピーする ](/help/assets/approve-assets.md#copy-delivery-url-for-approved-assets) 方法を説明します。

ユーザーがバニティ URL をクリックすると、[!DNL Dynamic Media with OpenAPI] は取り込み時にバニティ ID を元のアセット UUID に自動的にマッピングし、配信時に適切に解決して、遅滞なくアセットをユーザーに提供します。 アセット配信のパフォーマンスに影響を与えることなく、リアルタイムでバニティ URL をカスタマイズできます。

[AEM Cloud Service の高度なカスタマイズ機能を使用して、バニティ URL の影響を強化します。](#scale-using-vanity-url)

## バニティ URL を使用した拡大・縮小{#scale-using-vanity-url}

AEM as a Cloud Serviceを使用すると、web アドレス内で [DNS 名と CDN 名をカスタマイズ ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/introduction) できます。 これらの AEMCS 機能をバニティ URL と共に使用して、明確で説明的、ブランド化された、直感的で [ 前述のメリット ](#key-benefits) な独自の web アドレスに変換します。

次のバニティー URL と、カスタマイズ可能なコンポーネントを参照してください。

**バニティー URL 形式：**

`https://delivery-<tenant>.adobeaemcloud.com/adobe/assets/urn:avid:aem:<vanity-id>/<seoname>.<format>`

<table style="border-collapse:collapse; table-layout:auto; width:auto;">
<tr valign="top">
<td style="padding:0 4px; white-space:nowrap; text-align:center;">
<div style="text-align:left;"><code>https://delivery&#8209;&lt;tenant&gt;.adobeaemcloud.com</code></div>
<div style="text-align:center;">↓</div>
<div style="text-align:center;"><a href="#customize-dns"> この DNS をカスタマイズする </a></div>
</td>
<td style="padding:0 6px; white-space:nowrap; text-align:center;">／</td>
<td style="padding:0 4px; white-space:nowrap; text-align:center;">
<div style="text-align:left;"><code>adobe/assets/urn:avid:aem:</code></div>
<div style="text-align:center;">↓</div>
<div style="text-align:center;"><a href="#rewrite-cdn-rules"> 書き換えルールで URL をカスタマイズ </a></div>
</td>
<td style="padding:0 4px; white-space:nowrap; text-align:center;">
<div style="text-align:left;"><code>&lt;vanity-id&gt;</code></div>
<div style="text-align:center;">↓</div>
<div style="text-align:center;"><a href="#create-vanity-urls"> バニティ ID の作成 </a></div>
</td>
<td style="padding:0 4px; white-space:nowrap; text-align:left; width:1%;">
<code>/&lt;seoname&gt;.&lt;format&gt;</code>
</td>
</tr>
</table>

**カスタマイズされた DNS 名と CDN 名を使用したバニティー URL 形式：**

`https://<custom-dns>` `/` `dam/assets/` `<vanity-id>` `/<seoname>.<format>`

**カスタマイズ可能な URL コンポーネント**

* ***[DNS 名（hostname）:](#customize-DNS)*** `https://delivery-<tenant>.adobeaemcloud.com` は、アセットをホストするサーバードメインです。 [ ホスト名を変更するための DNS のカスタマイズ ](#customize-DNS)。
* ***[CDN 書き換えルール：](#rewrite-cdn-rules)*** `adobe/assets/urn:avid:aem:` は、アセットタイプと配信方法を識別するパス構造です。 [CDN ルールの書き換え ](#rewrite-cdn-rules) を行い、ドメインパスを変更します。

### DNS のカスタマイズ{#customize-dns}

[Adobe サポートへのリクエストを発行 ](https://helpx.adobe.com/jp/contact.html) して、配信層に必要なカスタム DNS を生成します。 カスタム DNS 名を作成するには、次の [ ベストプラクティス ](#best-practices) に従います。

### CDN ルールの書き換え{#rewrite-cdn-rules}

配信用の CDN ルールを書き換えるには、次の手順を実行します。

1. AEM リポジトリに移動して、YAML 設定ファイルを作成します。
2. [ 設定 ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-error-pages#setup) セクションの手順を実行して、CDN ルールを設定し、Cloud Manager設定パイプラインを通じて設定をデプロイします。
ドメインパスを作成するには、次の [ ベストプラクティス ](#best-practices) に従います。
   [CDN 書き換えルールの詳細情報 ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-configuring-traffic#request-transformations)。

バニティ URL に拡張子の付いたファイル名を追加する書き換えルールの例を次に示します。 特定の要件に従って、これらの書き換えルールをカスタマイズします。 [Adobe サポートにお問い合わせください ](https://helpx.adobe.com/jp/contact.html)。サポートが必要な場合：

```- name: cdn-rewrite-rule
  when:
    allOf:
      - reqProperty: tier
        equals: delivery
```

#### SVG、GIFおよびPDFの場合 {#svg-gif-pdf}

```
    type: transform
      reqProperty: path
      op: replace
      match: ^/dam/assets/([^/]+\.(?:svg|gif|pdf|docx|xlsx))(\?.*)?$
      replacement: /adobe/assets/urn:avid:aem:\1/original/as/\1\2
```

#### ビデオ用{#video}

MP4、MOV、AVI、MKV などのビデオの場合

```
type: transform
      reqProperty: path
      op: replace
      match: ^/dam/assets/([^/]+\.(?:mp4|mov|avi|mkv))(\?.*)?$
      replacement: /adobe/assets/urn:avid:aem:\1/play\2
```

#### 画像用{#image}

SVGを除くすべての画像タイプの場合。

```
type: transform
      reqProperty: path
      op: replace
      match: ^/dam/assets/([^/]+\.[^/]+)(\?.*)?$
      replacement: /adobe/assets/urn:avid:aem:\1/as/\1\2
```

## クリーンなバニティ URL を作成するためのベストプラクティスに従う{#best-practices}

バニティ ID、カスタム DNS およびドメイン名を作成する際は、次のベストプラクティスに従います。

1. バニティ ID には、スペース、スラッシュ、ハイフンなどの特殊文字を使用しないでください。 バニティ ID の特殊文字が、事前に定義されたマッピングを使用して置き換えられます。
1. ブランド名、製品名、関連キーワードをバニティ ID、カスタム DNS およびドメイン名で使用して、ブランドの可視性とユーザーエンゲージメントを高めます。
1. 意味を伝える短い説明的な単語または文字列を使用します。
1. クリックごとにユーザーを招待するテキストを使用します。
