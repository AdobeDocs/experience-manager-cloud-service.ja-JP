---
title: エクスペリエンスフラグメント
description: Adobe Experience Managerをクラウドサービスエクスペリエンスフラグメントとして拡張します。
translation-type: tm+mt
source-git-commit: 625e56efdab2f41026988fb90b72c31ff876db57

---


# エクスペリエンスフラグメント{#experience-fragments}

## 基本知識 {#the-basics}

[エクスペリエンスフラグメント](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)は、ページ内で参照できるコンテンツおよびレイアウトを含む 1 つ以上のコンポーネントのグループです。

エクスペリエンスフラグメントマスターまたはバリアントでは、次を使用します。

* `sling:resourceType` : `/libs/cq/experience-fragments/components/xfpage`

何も変わらな `/libs/cq/experience-fragments/components/xfpage/xfpage.html` いので、

* `sling:resourceSuperType` : `wcm/foundation/components/page`

## プレーン HTML レンディション {#the-plain-html-rendition}

Using the `.plain.` selector in the URL, you can access the plain HTML rendition.

これはブラウザーから利用できますが、主な目的は、他のアプリケーション（例えば、サードパーティ Web アプリ、カスタムモバイル実装など）が、URL のみを使用して、エクスペリエンスフラグメントのコンテンツに直接アクセスできるようにすることです。

プレーン HTML レンディションは、次のようなパスにプロトコル、ホストおよびコンテキストパスを追加します。

* のタイプ： `src`、 `href`または `action`

* or end with: `-src`, or `-href`

次に例を示します。

`.../brooklyn-coat/master.plain.html`

>[!NOTE]
>
>リンクは、常に、パブリッシュインスタンスを参照します。リンクは、サードパーティによって使用されることを意図しているので、オーサーインスタンスではなく、常にパブリッシュインスタンスから呼び出されます。

![プレーンHTMLレンディション](assets/xf-14.png)

プレーンレンディションセレクターは、追加のスクリプトとは異なり、トランスフォームを使用します。変 [圧器としてSling Rewriter](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) を使用。 これは、

* `/libs/experience-fragments/config/rewriter/experiencefragments`

## ソーシャルバリエーション {#social-variations}

ソーシャルバリアントは、ソーシャルメディア（テキストおよび画像）に投稿できます。 AEMでは、これらのソーシャルバリアントにコンポーネントを含めることができます。例えば、テキストコンポーネント、画像コンポーネントなどです。

ソーシャル投稿の画像とテキストは、任意の画像リソースタイプまたはテキストリソースタイプから、（構築ブロックまたはレイアウトコンテナの）任意の深さのレベルで取得できます。

また、ソーシャルバリエーションを使用すると、（投稿環境で）ソーシャルアクションを行う際に、構築ブロックを考慮することもできます。

ソーシャルメディアネットワークに正しいテキストと画像を投稿するには、独自のカスタマイズコンポーネントを開発する場合、一部の規則を考慮する必要があります。

この場合、次のプロパティを使用する必要があります。

* 画像の抽出

   * `fileReference`
   * `fileName`

* テキストの抽出

   * `text`

この規則を使用しないコンポーネントは考慮されません。

## エクスペリエンスフラグメントのテンプレート {#templates-for-experience-fragments}

>[!CAUTION]
>
>***編集可能なテンプレート*** のみが、エクスペリエンスフラグメントでサポートされています。

<!-- >***Only*** [editable templates](/help/sites-developing/page-templates-editable.md) are supported for Experience Fragments.
-->

エクスペリエンスフラグメント用の新しいテンプレートを開発する場合は、編集可能なテンプレートの標準的な手法に従うことができます。

<!-- When developing a new template for Experience Fragments you can follow follow the standard practices for an [editable template](/help/sites-developing/page-templates-editable.md).
-->

エクスペリエンスフラグメントを作成ウィザードで検出されたエクスペリエンスフラグメ **ントテンプレートを作成するには** 、次のいずれかのルールセットに従う必要があります。

1. 両方:

   1. テンプレート（初期ノード）のリソースタイプは、次のものから継承する必要があります。
      `cq/experience-fragments/components/xfpage`

   1. また、テンプレートの名前は次の文字で始まる必要があります。
      `experience-fragments`
これにより、ユーザーは/content/experience-fragmentsにエクスペリエンスフラグメントを作成できます。このフォルダーのプロパティには、で始まる名前を持つすべてのテ `cq:allowedTemplates` ンプレートが含まれていま `experience-fragment`す。 お客様は、このプロパティを更新して、独自の命名スキームやテンプレートの場所を含めることができます。

1. [使用可能なテンプレートは](/help/sites-cloud/authoring/fundamentals/experience-fragments.md#configure-allowed-templates-folder) 、エクスペリエンスフラグメントコンソールで設定できます。

<!--
1. Add the template details manually in `cq:allowedTemplates` on the `/content/experience-fragment` node.
-->

<!-- >[!NOTE]
>
>[Allowed templates](/help/sites-authoring/experience-fragments.md#configuring-allowed-templates) can be configured in the Experience Fragments console.
-->

## エクスペリエンスフラグメントのコンポーネント {#components-for-experience-fragments}

エクスペリエンスフラグメントと共に使用するコンポーネントの開発は、標準的な方法に従って行います。

追加の設定は、コンポーネントがテンプレートで許可されるようにすることだけです。これは、コンテンツポリシーを使用して行います。

<!--
[Developing components](/help/sites-developing/components.md) for use with/in Experience Fragments follow standard practices.

The only additional configuration is to ensure that the components are [allowed on the template, this is achieved with the Content Policy](/help/sites-developing/page-templates-editable.md#content-policies).
-->

## The Experience Fragment Link Rewriter Provider - HTML {#the-experience-fragment-link-rewriter-provider-html}

AEMでは、エクスペリエンスフラグメントを作成できます。 エクスペリエンスフラグメントは、

* は、コンポーネントのグループとレイアウトで構成され、
* はAEMページとは独立して存在できます。

このようなグループの使用例の1つは、Adobe targetなどのサードパーティのタッチポイントにコンテンツを埋め込む場合です。

### デフォルトのリンク書き換え {#default-link-rewriting}

<!--Using the [Export to Target](/help/sites-administering/experience-fragments-target.md) feature, you can:
-->

ターゲットにエクスポート機能を使用すると、次のことができます。

* エクスペリエンスフラグメントの作成、
* コンポーネントを追加します。
* その後、HTML形式またはJSON形式でAdobe targetオファーとして書き出します。

この機能は、AEMの作成者インスタンスで有効にできます。 有効なAdobe target設定およびLink Externalizerの設定が必要です。

<!--
This feature can be [enabled on an author instance of AEM](/help/sites-administering/experience-fragments-target.md#Prerequisites). It requires a valid Adobe Target Configuration, and configurations for the Link Externalizer.
-->

Link Externalizerは、TargetオファーのHTMLバージョンを作成する際に必要な正しいURLを判断するために使用され、その後Adobe targetに送信されます。 これは、Adobe targetでTarget HTMLオファー内のすべてのリンクが一般にアクセスできる必要があるので、つまり、リンクが参照するリソースとエクスペリエンスフラグメント自体は、使用する前に発行する必要があります。

デフォルトでは、Target HTMLオファーを作成すると、AEMのカスタムSlingセレクターにリクエストが送信されます。 このセレクターは呼び出されま `.nocloudconfigs.html`す。 その名前が示すように、エクスペリエンスフラグメントのプレーンHTMLレンダリングを作成しますが、クラウド設定は含まれません（過剰な情報となります）。

HTMLページを生成した後、Slingリライタパイプラインは出力を変更します。

1. 、お `html`よびの `head`要素は `body` 要素に置き換えら `div` れます。 要素、 `meta`および `noscript` 要素 `title` は削除されます(元の要素の子要素であり、 `head` 要素に置き換えられる場合は考慮され `div` ません)。

   これは、HTMLターゲットオファーをTargetアクティビティに確実に含めるために行います。

2. AEMは、HTMLに存在するすべての内部リンクを変更し、公開されたリソースを指すようにします。

   変更するリンクを決定する際、AEMはHTML要素の属性に対して次のパターンに従います。

   1. `src` 属性
   2. `href` 属性
   3. `*-src` 属性（data-src、custom-srcなど）
   4. `*-href` 属性(例 `data-href`え `custom-href`ば、 `img-href`など)
   >[!NOTE]
   >
   >ほとんどの場合、HTML内の内部リンクは相対リンクですが、カスタムコンポーネントがHTML内で完全なURLを提供する場合があります。 デフォルトでは、AEMはこれらの完全に公開されたURLを無視し、変更は行われません。

   これらの属性のリンクは、AEM Link Externalizerを使用して実行され、URLを公開済みのインスタンス上にあるかのように再作成します。そのため、公開済みのURLも作成できます。 `publishLink()`

そのまま使用できる実装を使用する場合、上記のプロセスでは、エクスペリエンスフラグメントからTargetオファーを生成し、Adobe targetに書き出すのに十分です。 ただし、このプロセスでは考慮されない使用例がいくつかあります。以下が含まれます。

* Slingマッピングは、発行インスタンスでのみ使用可能
* ディスパッチャーリダイレクト

これらの使用例では、AEMがリンクリライタプロバイダーインターフェイスを提供します。

### リンクリライタプロバイダーインターフェイス {#link-rewriter-provider-interface}

より複雑な場合（デフォルトでは対象外）には、AEM [では](#default-link-rewriting)「リンクリライタープロバイダー」インターフェイスを提供しています。 これは、サービスと `ConsumerType` してバンドルに実装できるインターフェイスです。 エクスペリエンスフラグメントからレンダリングされると、HTMLオファーの内部リンクに対してAEMが実行する変更をバイパスします。 このインターフェイスを使用すると、社内のHTMLリンクを書き換えてビジネスニーズに合わせるプロセスをカスタマイズできます。

このインターフェイスをサービスとして実装する場合の使用例を次に示します。

* 発行インスタンスでSling Mappingsが有効になっているが、作成者インスタンスでは有効になっていない
* 内部的なURLのリダイレクトには、ディスパッチャーまたは同様のテクノロジーが使用されます
* 資源が `sling:alias mechanisms` ある

>[!NOTE]
>
>このインターフェイスは、生成されたTargetオファーからの内部HTMLリンクのみを処理します。

リンクリライタプロバイダのインターフェ `ExperienceFragmentLinkRewriterProvider`イス()は次のとおりです。

```java
public interface ExperienceFragmentLinkRewriterProvider {

    String rewriteLink(String link, String tag, String attribute);

    boolean shouldRewrite(ExperienceFragmentVariation experienceFragment);

    int getPriority();

}
```

### リンクリライタプロバイダーインターフェイスの使用方法 {#how-to-use-the-link-rewriter-provider-interface}

このインターフェイスを使用するには、まず、リンクリライタプロバイダーインターフェイスを実装する新しいサービスコンポーネントを含むバンドルを作成する必要があります。

このサービスは、様々なリンクにアクセスするために、エクスペリエンスフラグメントをターゲットにエクスポート書き換えにプラグインするために使用されます。

For example, `ComponentService`:

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

サービスが機能するには、サービス内に実装する必要がある3つのメソッドが用意されています。

* ` [shouldRewrite](#shouldrewrite)`
* ` [rewriteLink](#rewritelink)`

   * `rewriteLinkExample2`

* ` [getPriority](#priorities-getpriority)`

#### shouldRewrite {#shouldrewrite}

特定のエクスペリエンスフラグメントのバリエーションでTargetへの書き出しの呼び出しが行われた場合、システムにリンクを書き換える必要があるかどうかを指定する必要があります。 これを行うには、次のメソッドを実装します。

`shouldRewrite(ExperienceFragmentVariation experienceFragment);`

次に例を示します。

```java
@Override
public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
    return experienceFragment.getPath().equals("/content/experience-fragment/master");
}
```

このメソッドは、パラメーターとして、Export to targetシステムが現在書き換え中のエクスペリエンスフラグメントのバリエーションを受け取ります。

上の例では、次の内容を書き直します。

* 存在するリンク `src`

* `href` 属性のみ

* 特定のエクスペリエンスフラグメントの場合：
   `/content/experience-fragment/master`

Export to targetシステムを通過するその他のエクスペリエンスフラグメントは無視され、本サービスに実装された変更の影響を受けません。

#### rewriteLink {#rewritelink}

書き換えプロセスの影響を受けるエクスペリエンスフラグメントのバリエーションの場合は、次に、サービスでリンクの書き換えを処理するように進みます。 内部HTMLでリンクが検出されるたびに、次のメソッドが呼び出されます。

`rewriteLink(String link, String tag, String attribute)`

入力として、メソッドは次のパラメーターを受け取ります。

* `link`
現在 `String` 処理中のリンクの表現です。 これは通常、作成者インスタンス上のリソースを指す相対URLです。

* `tag`
現在処理中のHTML要素の名前。

* `attribute`
正確な属性名。

例えば、Targetへのエクスポートシステムが現在この要素を処理している場合、次のように定義で `CSSInclude` きます。

```java
<link rel="stylesheet" href="/etc.clientlibs/foundation/clientlibs/main.css" type="text/css">
```

メソッドの呼び出しは、 `rewriteLink()` 次のパラメーターを使用して行います。

```java
rewriteLink(link="/etc.clientlibs/foundation/clientlibs/main.css", tag="link", attribute="href" )
```

サービスを作成する場合は、指定した入力に基づいて決定を行い、それに従ってリンクを書き直すことができます。

この例では、URLの一部を削除し、適切な外 `/etc.clientlibs` 部ドメインを追加することを希望しています。 これを簡単にするために、お客様のサービス用のリソースリゾルバーへのアクセス権があると考えます。次に例を示しま `rewriteLinkExample2`す。

>[!NOTE]
>
>サービスユーザーを介してリソースリゾルバーを取得する方法について詳しくは、「AEMのサービスユーザー」を参照してください。

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
>上記のメソッドが返され `null`た場合、Export to targetシステムは、リンクをそのままの状態（リソースへの相対リンク）にします。

#### 優先度 — getPriority {#priorities-getpriority}

様々な種類のエクスペリエンスフラグメントに対応するため、またはすべてのエクスペリエンスフラグメントの外部化とマッピングを処理する汎用サービスを用意するために、いくつかのサービスが必要になることは珍しくありません。 このような場合、使用するサービスに関する競合が発生する可能性があるので、AEMは異なるサービスに対して **Priority** （優先度）を定義できます。 優先度は、次の方法を使用して指定します。

* `getPriority()`

このメソッドを使用すると、同じエクスペリエンスフラグメントに対して `shouldRewrite()` trueを返す複数のサービスを使用できます。 メソッドから最も高い数を返すサービスは、エクスペリエ `getPriority()`ンスフラグメントのバリエーションを処理するサービスです。

例えば、すべてのエクスペリエンスフラグメントの基本マッピ `GenericLinkRewriterProvider` ングを処理し、そのメソッドがすべてのエクスペリエンスフラグメントのバリエーションに `shouldRewrite()` 戻る `true` ときの基本マッピングを使用できます。 特定のエクスペリエンスフラグメントの中には、特別な処理が必要な場合があります。この場合は、一部のエクスペリエンスフラグメントのバリエーションに対してのみメソッドがtrueを返 `SpecificLinkRewriterProvider``shouldRewrite()` す対象のを指定できます。 がこれらのエクスペリエン `SpecificLinkRewriterProvider` スフラグメントのバリエーションを処理するように選択されていることを確認するには、メソッドに `getPriority()``GenericLinkRewriterProvider.`