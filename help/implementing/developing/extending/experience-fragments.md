---
title: エクスペリエンスフラグメント 概要
description: Adobe Experience Manager as a Cloud Service のエクスペリエンスフラグメントの拡張
exl-id: bd4ea763-d17c-40a6-9a86-a24d7600229e
source-git-commit: 29d8d08899bb60b2bf3027ed32dbcdca3a73e671
workflow-type: tm+mt
source-wordcount: '1646'
ht-degree: 49%

---

# エクスペリエンスフラグメント{#experience-fragments}

## 基本知識 {#the-basics}

[エクスペリエンスフラグメント](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)は、ページ内で参照できるコンテンツおよびレイアウトを含む 1 つ以上のコンポーネントのグループです。

エクスペリエンスフラグメントマスター、バリアント、またはその両方で、次のものが使用されます。

* `sling:resourceType`：`/libs/cq/experience-fragments/components/xfpage`

なぜなら、 `/libs/cq/experience-fragments/components/xfpage/xfpage.html`を呼び出すと、次の場所に戻ります。

* `sling:resourceSuperType`：`wcm/foundation/components/page`

## プレーン HTML レンディション {#the-plain-html-rendition}

URL で `.plain.` セレクターを使用すると、プレーン HTML レンディションにアクセスできます。

このレンディションはブラウザーで使用できます。 ただし、その主な目的は、他のアプリケーション（サードパーティの Web アプリ、カスタムモバイル実装など）が URL のみを使用して、エクスペリエンスフラグメントのコンテンツに直接アクセスできるようにすることです。

プレーンHTMLレンディションは、次のパスにプロトコル、ホストおよびコンテキストパスを追加します。

* タイプが `src`、`href`、`action` のいずれか

* または、`-src` か `-href` で終わる

次に例を示します。

`.../brooklyn-coat/master.plain.html`

>[!NOTE]
>
>リンクは、常にパブリッシュインスタンスを参照します。これらはサードパーティによる使用を目的としているので、リンクは常にオーサーインスタンスからではなく、パブリッシュインスタンスから呼び出されます。
>
>詳しくは、 [URL の外部化](/help/implementing/developing/tools/externalizer.md).

![プレーン HTML レンディション](assets/xf-14.png)

プレーンレンディションセレクターでは、追加のスクリプトとは異なり、トランスフォーマーを使用します。The [Sling Rewriter](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) は変換サービスとして使用されます。 この変換サービスは、次の場所で設定します。

* `/libs/experience-fragments/config/rewriter/experiencefragments`

### HTML レンディション生成の設定 {#configuring-html-rendition-generation}

HTML レンディションは、Sling Rewriter パイプラインを使用して生成されます。パイプラインは、`/libs/experience-fragments/config/rewriter/experiencefragments` で定義されます。HTML 変換サービスでは、次のオプションをサポートしています。

* `allowedCssClasses`
   * 最終レンディションに残す CSS クラスに一致する正規表現。
   * このオプションは、お客様が特定の CSS クラスを取り除く場合に役立ちます
* `allowedTags`
   * 最終レンディションで許可されるHTMLタグのリスト。
   * デフォルトでは、次のタグが許可されています（設定は不要）：html、head、title、body、img、p、span、ul、li、a、b、i、em、strong、h1、h2、h3、h4、h5、h6、br、noscript、div、link、script

Adobeでは、オーバーレイを使用してリライターを設定することをお勧めします。 詳しくは、 [AEMでのオーバーレイas a Cloud Service](/help/implementing/developing/introduction/overlays.md).

## エクスペリエンスフラグメントのテンプレート {#templates-for-experience-fragments}

>[!CAUTION]
>
>エクスペリエンスフラグメントでサポートされているのは、編集可能なテンプレート&#x200B;***だけ***&#x200B;です。

<!-- >***Only*** [editable templates](/help/sites-developing/page-templates-editable.md) are supported for Experience Fragments.
-->

エクスペリエンスフラグメント用の新しいテンプレートを開発する際は、編集可能なテンプレートの標準的な手法に従うことができます。

<!-- When developing a new template for Experience Fragments you can follow the standard practices for an [editable template](/help/sites-developing/page-templates-editable.md).
-->

で検出されるエクスペリエンスフラグメントテンプレートを作成するには、以下を実行します。 **エクスペリエンスフラグメントを作成** ウィザードでは、次のいずれかのルールセットに従う必要があります。

1. 次の両方：

   1. テンプレート（初期ノード）のリソースタイプは、次のものから継承する必要があります。
      `cq/experience-fragments/components/xfpage`

   1. テンプレートの名前は次の文字列で始まる必要があります。
      `experience-fragments`
このパターンを使用すると、ユーザーは/content/experience-fragments 内にエクスペリエンスフラグメントを `cq:allowedTemplates` このフォルダーのプロパティには、名前がで始まるすべてのテンプレートが含まれます `experience-fragment`. ユーザーは、このプロパティを更新して、独自の命名方式やテンプレート場所を取り入れることができます。

1. [使用可能なテンプレート](/help/sites-cloud/authoring/fundamentals/experience-fragments.md#configure-allowed-templates-folder)はエクスペリエンスフラグメントコンソールで設定できます。

<!--
1. Add the template details manually in `cq:allowedTemplates` on the `/content/experience-fragment` node.
-->

<!-- >[!NOTE]
>
>[Allowed templates](/help/sites-authoring/experience-fragments.md#configuring-allowed-templates) can be configured in the Experience Fragments console.
-->

## エクスペリエンスフラグメントのコンポーネント {#components-for-experience-fragments}

エクスペリエンスフラグメントで使用するコンポーネントの開発は、標準的な方法に従って行います。

追加の設定は、コンポーネントがテンプレートで許可されるようにすることです。 この引き渡しは、コンテンツポリシーでおこないます。

<!--
[Developing components](/help/sites-developing/components.md) for use with/in Experience Fragments follow standard practices.

The only additional configuration is to ensure that the components are [allowed on the template, this is achieved with the Content Policy](/help/sites-developing/page-templates-editable.md#content-policies).
-->

## Experience Fragment Link Rewriter Provider - HTML {#the-experience-fragment-link-rewriter-provider-html}

AEMでは、エクスペリエンスフラグメントを作成できます。 エクスペリエンスフラグメントは、

* コンポーネントグループとレイアウトで構成されます。
* AEM ページとは独立して存在できます。

このようなグループの使用例の 1 つは、Adobe Targetなどのサードパーティのタッチポイントにコンテンツを埋め込む場合です。

### デフォルトのリンク書き換え {#default-link-rewriting}

<!--Using the [Export to Target](/help/sites-administering/experience-fragments-target.md) feature, you can:
-->

「Adobe Target に書き出し」機能を使用すると、次の操作が可能です。

* エクスペリエンスフラグメントを作成する
* エクスペリエンスフラグメントにコンポーネントを追加する
* エクスペリエンスフラグメントを HTML 形式または JSON 形式で Adobe Target オファーとして書き出す

この機能は、AEM のオーサーインスタンスで有効にすることができます。有効な Adobe Target 設定と、Link Externalizer の設定が必要です。

<!--
This feature can be [enabled on an author instance of AEM](/help/sites-administering/experience-fragments-target.md#Prerequisites). It requires a valid Adobe Target Configuration, and configurations for the Link Externalizer.
-->

Link Externalizer は、Target オファーのHTMLバージョンを作成する際に必要な正しい URL を決定するために使用されます。オファーはAdobe Targetに送信されます。 このプロセスは、Adobe Targetでは、TargetHTMLオファー内のすべてのリンクに公開でアクセスできる必要があるので必要です。 つまり、リンクが参照するすべてのリソースと、エクスペリエンスフラグメント自体を使用するには、それらを使用する前に公開する必要があります。

デフォルトでは、Target HTML オファーを作成すると、AEM のカスタム Sling セレクターにリクエストが送信されます。このセレクターの名前は `.nocloudconfigs.html` です。これはエクスペリエンスフラグメントのプレーン HTML レンダリングを作成しますが、その名前が示すとおり、クラウド設定を含んでいません（クラウド設定は余分な情報です）。

HTMLページを生成した後、Sling Rewriter パイプラインは出力に変更されます。

1. `html`、`head`、`body` の各要素が `div` 要素に置き換わります。The `meta`, `noscript`、および `title` 要素が削除されます（元の要素の子要素です）。 `head` 要素であり、 `div` 要素 ) を参照してください。

   このプロセスは、HTMLTarget オファーを Target アクティビティに確実に含めることができるようにするためにおこなわれます。

2. AEM では、HTML に存在するすべての内部リンクを変更して、公開されたリソースを指すようにします。

   変更するリンクを決定するために、AEM では HTML 要素の次の属性パターンに従います。

   1. `src` 属性
   2. `href` 属性
   3. `*-src` 属性 ( `data-src`、および `custom-src`)
   4. `*-href` 属性 ( `data-href`, `custom-href`、および `img-href`)

   >[!NOTE]
   >
   >HTML内の内部リンクは相対リンクですが、カスタムコンポーネントがHTML内で完全な URL を指定する場合があります。 デフォルトでは、AEM はこれらの完全な URL を無視し、変更しません。

   これらの属性のリンクは、AEM Link Externalizer を通じて実行されます `publishLink()` 公開済みのインスタンス上にあるかのように URL を再作成し、公開済みの状態にします。

そのまま使用できる標準実装を使用する場合、エクスペリエンスフラグメントから Target オファーを生成して Adobe Target に書き出すには、上記のプロセスで十分です。ただし、このプロセスでは考慮されない使用例もあります。 が考慮されないこれらのケースには、次のものが含まれます。

* Sling マッピングがパブリッシュインスタンスでのみ使用可能
* Dispatcher によるリダイレクト

このような使用例では、AEMに Link Rewriter Provider インターフェイスが用意されています。

### Link Rewriter Provider インターフェイス {#link-rewriter-provider-interface}

（[デフォルトのリンク書き換え](#default-link-rewriting)では対応していない）より複雑な場合のために、AEM では Link Rewriter Provider インターフェイスを提供しています。このインターフェイスは、 `ConsumerType` バンドルにサービスとして実装できるインターフェイス。 このインターフェイスは、エクスペリエンスフラグメントからレンダリングされる HTML オファーの内部リンクに対して AEM で実行される変更をバイパスします。このインターフェイスを使用すると、内部HTMLのリンクを書き換えるプロセスを、ビジネスニーズに合わせてカスタマイズできます。

このインターフェイスをサービスとして実装する使用例としては、例えば次のものがあります。

* Sling マッピングがパブリッシュインスタンスでは有効になっているが、オーサーインスタンスでは有効になっていない
* Dispatcher または類似のテクノロジーを使用して URL を内部的にリダイレクトする
* The `sling:alias mechanisms` リソース用に配置されている

>[!NOTE]
>
>このインターフェイスでは、生成された Target オファーからの内部 HTML リンクのみ処理します。

Link Rewriter Provider インターフェイス（`ExperienceFragmentLinkRewriterProvider`）は次のとおりです。

```java
public interface ExperienceFragmentLinkRewriterProvider {

    String rewriteLink(String link, String tag, String attribute);

    boolean shouldRewrite(ExperienceFragmentVariation experienceFragment);

    int getPriority();

}
```

### Link Rewriter Provider インターフェイスの使用方法 {#how-to-use-the-link-rewriter-provider-interface}

このインターフェイスを使用するには、まず、Link Rewriter Provider インターフェイスを実装する新しいサービスコンポーネントを含むバンドルを作成する必要があります。

このサービスは、様々なリンクにアクセスできるように、エクスペリエンスフラグメントの「Adobe Target に書き出し」機能の書き換えにプラグインするために使用されます。

例えば、`ComponentService` の場合は次のようになります。

```java
import com.adobe.cq.xf.ExperienceFragmentLinkRewriterProvider;
import com.adobe.cq.xf.ExperienceFragmentVariation;
import org.osgi.service.component.annotations.Service;
import org.osgi.service.component.annotations.Component;

@Component
@Service
public class GeneralLinkRewriter implements ExperienceFragmentLinkRewriterProvider {

    @Override
    public String rewriteLink(String link, String tag, String attribute) {
        return null;
    }

    @Override
    public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
        return false;
    }

    @Override
    public int getPriority() {
        return 0;
    }

}
```

このサービスが動作するには、サービス内に実装する必要がある次の 3 つのメソッドがあります。

* `[shouldRewrite](#shouldrewrite)`
* `[rewriteLink](#rewritelink)`

   * `rewriteLinkExample2`

* `[getPriority](#priorities-getpriority)`

#### shouldRewrite {#shouldrewrite}

エクスペリエンスフラグメントの特定のバリエーションに対して「Adobe Target に書き出し」機能が呼び出された場合に、リンクを書き換える必要があるかどうかをシステムに示します。 次のメソッドを実装できます。

`shouldRewrite(ExperienceFragmentVariation experienceFragment);`

例：

```java
@Override
public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
    return experienceFragment.getPath().equals("/content/experience-fragment/master");
}
```

このメソッドは、「Adobe Target に書き出し」システムによって書き換えられるエクスペリエンスフラグメントバリエーションをパラメーターとして受け取ります。

上記の例では、次の内容を書き換えます。

* `src` に指定されているリンク

* `href` 属性のみ

* 特定のエクスペリエンスフラグメントの場合：
  `/content/experience-fragment/master`

「Adobe Target に書き出し」システムに通す他のあらゆるエクスペリエンスフラグメントは無視され、本サービスに実装される変更の影響を受けません。

#### rewriteLink {#rewritelink}

書き換えプロセスの影響を受けるエクスペリエンスフラグメントバリエーションの場合は、次に、サービスにリンクの書き換えを処理させます。 内部HTMLでリンクが検出されるたびに、次のメソッドが呼び出されます。

`rewriteLink(String link, String tag, String attribute)`

このメソッドは入力として次のパラメーターを受け取ります。

* `link`
The `String` 処理中のリンクの表現。 この表現は通常、オーサーインスタンス上のリソースを指す相対 URL です。

* `tag`
処理中のHTML要素の名前。

* `attribute`：
正確な属性名です。

例えば、「Adobe Target に書き出し」システムがこの要素を処理している場合、 `CSSInclude` 形式：

```java
<link rel="stylesheet" href="/etc.clientlibs/foundation/clientlibs/main.css" type="text/css">
```

`rewriteLink()` メソッドの呼び出しは、次のパラメーターを使用して行います。

```java
rewriteLink(link="/etc.clientlibs/foundation/clientlibs/main.css", tag="link", attribute="href" )
```

サービスを作成する際、指定された入力に基づいて決定し、それに応じてリンクを書き換えます。

例えば、 `/etc.clientlibs` URL の一部を含め、適切な外部ドメインを追加します。 話を簡単にするには、に示すように、サービスのリソースリゾルバーにアクセスできると考えます。 `rewriteLinkExample2`:

>[!NOTE]
>
>サービスユーザーを通じてリソースリゾルバーを取得する方法について詳しくは、「AEM のサービスユーザー」を参照してください。

<!--
>For more information on how to get a resource resolver through a service user see [Service Users in AEM](/help/sites-administering/security-service-users.md).
-->

```java
private ResourceResolver resolver;

private Externalizer externalizer;

@Override
public String rewriteLink(String link, String tag, String attribute) {

    // get the externalizer service
    externalizer = resolver.adaptTo(Externalizer.class);
    if(externalizer == null) {
        // if there was an error, then we do not modify the link
        return null;
    }

    // remove leading /etc.clientlibs from resource link before externalizing
    link = link.replaceAll("/etc.clientlibs", "");

    // considering that we configured our publish domain, we directly apply the publishLink() method
    link = externalizer.publishLink(resolver, link);

    return link;
}
```

>[!NOTE]
>
>上記のメソッドが `null`「Adobe Target に書き出し」を選択した場合、そのリンクをそのままの状態で、リソースへの相対リンクとして残します。

#### 優先度 - getPriority {#priorities-getpriority}

様々な種類のエクスペリエンスフラグメントに対応するためや、すべてのエクスペリエンスフラグメントの外部化とマッピングを処理する汎用サービスを用意するために、いくつかのサービスが必要になることは珍しくありません。このような場合、使用するサービスに関するの競合が発生する可能性があるので、AEM では、様々なサービスの&#x200B;**優先度**&#x200B;を定義できるようになっています。優先度は、次のメソッドを使用して指定します。

* `getPriority()`

このメソッドを使用すると、複数のサービスを使用しても、同じエクスペリエンスフラグメントについては `shouldRewrite()` メソッドが true を返すようにすることができます。`getPriority()` メソッドから最高の優先度が返されるサービスが、対象となっているエクスペリエンスフラグメントバリエーションを処理するサービスになります。

例えば、エクスペリエンスフラグメントのすべてのバリエーションについて `shouldRewrite()` メソッドが `true` を返す場合にすべてのエクスペリエンスフラグメントの基本マッピングを処理する `GenericLinkRewriterProvider` を用意することができます。一部の特定のエクスペリエンスフラグメントについては、特別な処理が必要になる場合があります。その場合は、一部のエクスペリエンスフラグメントバリエーションについてのみ `shouldRewrite()` メソッドが true を返すような `SpecificLinkRewriterProvider` を用意することができます。それらのエクスペリエンスフラグメントバリエーションを処理するために `SpecificLinkRewriterProvider` が必ず選択されるようにするには、そのプロバイダーの `getPriority()` メソッドで返される優先度が `GenericLinkRewriterProvider.` の場合より高くなるようにする必要があります。
