---
title: 翻訳するコンテンツの特定
description: 翻訳ルールが翻訳を必要とするコンテンツを識別する方法を学びます。
translation-type: tm+mt
source-git-commit: 4fc4dbe2386d571fa39fd6d10e432bb2fc060da1
workflow-type: tm+mt
source-wordcount: '1126'
ht-degree: 47%

---


# 翻訳するコンテンツの特定 {#identifying-content-to-translate}

翻訳プロジェクトに追加する、または翻訳プロジェクトから除外するページ、コンポーネントおよびアセットの翻訳対象コンテンツは翻訳ルールによって特定されます。ページまたはアセットを翻訳する場合は、AEM がそのコンテンツを抽出して、翻訳サービスに送信できるようにします。

ページとアセットは、JCR リポジトリ内のノードとして表されます。抽出されるコンテンツはノードの 1 つ以上のプロパティ値です。翻訳ルールは、抽出するコンテンツを含むプロパティを識別します。

翻訳ルールは XML 形式で表現され、次の場所に格納されています。

* `/libs/settings/translation/rules/translation_rules.xml`
* `/apps/settings/translation/rules/translation_rules.xml`
* `/conf/global/settings/translation/rules/translation_rules.xml`

このファイルはすべての翻訳プロジェクトに適用されます。

ルールには以下の情報が含まれます。

* ルールを適用するノードのパス
   * この規則は、ノードの子孫にも適用されます。
* 変換するコンテンツを含むノードプロパティの名前
   * このプロパティは、特定のリソースタイプまたはすべてのリソースタイプに固有のものです。

例えば、作成者がページ上のすべてのテキストコンポーネントに追加するコンテンツを翻訳するルールを作成できます。 このルールでは、`/content`ノードと`core/wcm/components/text/v2/text`コンポーネントの`text`プロパティを識別できます。

翻訳ルールの設定用に追加された[コンソール](#translation-rules-ui)があります。UI での定義の内容がファイルに自動的に入力されます。

AEMのコンテンツ翻訳機能の概要については、[多言語サイト用のコンテンツの翻訳](overview.md)を参照してください。

>[!NOTE]
>
>AEM は、ページ上の参照コンテンツの翻訳に関して、リソースタイプと参照属性の 1 対 1 マッピングをサポートしています。

## ページ、コンポーネントおよびアセット用のルールの構文 {#rule-syntax-for-pages-components-and-assets}

ルールとは、1 個以上の `node` 子要素と 0 個以上の `property` 子要素を含む `node` 要素です。

```xml
<node path="content path">
          <property name="property name" [translate="false"]/>
          <node resourceType="component path" >
               <property name="property name" [translate="false"]/>
          </node>
</node>
```

これらの`node`要素はそれぞれ次の特性を持ちます。

* `path` 属性には、ルールが適用されるブランチのルートノードのパスが格納されます。
* `property` 子要素は、すべてのリソースタイプについて、翻訳するノードプロパティを特定します。
   * `name` 属性には、プロパティ名が格納されます。
   * プロパティが変換されない場合、オプションの`translate`属性は`false`です。 デフォルト値は `true` です。この属性は、以前のルールを上書きする場合に役立ちます。
* `node` 子要素は、特定のリソースタイプについて、翻訳するノードプロパティを特定します。
   * `resourceType` 属性には、リソースタイプを実装するコンポーネントに解決されるパスが格納されます。
   * `property` 子要素は、翻訳するノードプロパティを特定します。このノードは、ノードルールの `property` 子要素と同じ方法で使用します。

次のルールの例では、`/content`ノードの下のすべてのページについて、すべての`text`プロパティの内容が変換されます。 このルールは、テキストコンポーネントなど、`text`プロパティにコンテンツを格納するコンポーネントに対して有効です。

```xml
<node path="/content">
          <property name="text"/>
</node>
```

次の例は、すべての`text`プロパティの内容を変換し、また、イメージコンポーネントの他のプロパティも変換します。 その他のコンポーネントに同じ名前のプロパティが含まれている場合、それらのプロパティにはルールが適用されません。

```xml
<node path="/content">
      <property name="text"/>
      <node resourceType="core/wcm/components/image/v2/image">
         <property name="image/alt"/>
         <property name="image/jcr:description"/>
         <property name="image/jcr:title"/>
      </node>
</node>
```

## ページからアセットを抽出するルールの構文   {#rule-syntax-for-extracting-assets-from-pages}

次に示すルールの構文を使用して、コンポーネントに埋め込むアセットまたはコンポーネントから参照するアセットを追加します。

```xml
<assetNode resourceType="path to component" assetReferenceAttribute="property that stores asset"/>
```

各 `assetNode` 要素には以下の特徴があります。

* コンポーネントに解決されるパスと等しい1つの`resourceType`属性
* 1つの`assetReferenceAttribute`属性。アセットバイナリ（埋め込みアセットの場合）を格納するプロパティの名前と等しいか、または参照されているアセットのパスです

次の例では、画像コンポーネントから画像を抽出します。

```xml
<assetNode resourceType="core/wcm/components/image/v2/image" assetReferenceAttribute="fileReference"/>
```

## ルールの上書き {#overriding-rules}

`translation_rules.xml`ファイルは、`nodelist`要素といくつかの子`node`要素で構成されます。 AEMは、ノードリストを上から下に読み取ります。 複数のルールが同じノードにターゲットする場合は、ファイル内で下位のルールが使用されます。 例えば、次のルールでは、`text`プロパティのすべてのコンテンツが変換されます。ただし、ページの`/content/mysite/en`分岐は例外です。

```xml
<nodelist>
     <node path="/content”>
           <property name="text" />
     </node>
     <node path=“/content/mysite/en”>
          <property name=“text” translate=“false" />
     </node>
<nodelist>
```

## プロパティのフィルタリング {#filtering-properties}

`filter`   要素を使用して、特定のプロパティを持つノードをフィルタリングできます。

例えば、次のルールを使用すると、プロパティ `text` が `draft` に設定されている場合を除き、`true` プロパティのすべてのコンテンツが翻訳されます。

```xml
<nodelist>
    <node path="/content”>
     <filter>
   <node containsProperty="draft" propertyValue="true" />
     </filter>
        <property name="text" />
    </node>
<nodelist>
```

## 翻訳ルール UI {#translation-rules-ui}

コンソールを使用して翻訳ルールを設定することもできます。

コンソールにアクセスするには：

1. **ツール**／**一般**&#x200B;に移動します。

1. 「**翻訳設定**」を選択します。

変換ルールUIでは、次の操作を実行できます。

1. **追加コンテキスト**。パスを追加できます。

   ![追加翻訳文脈](../assets/add-translation-context.png)

1. パスブラウザーを使用して必要なコンテキストを選択し、「**確認**」ボタンをタップまたはクリックして保存します。

   ![コンテキストを選択](../assets/select-context.png)

1. 次に、コンテキストを選択し、「**編集**」をクリックします。 これにより、翻訳ルールエディターが開きます。

   ![翻訳ルールエディター](../assets/translation-rules-editor.png)

UIを使用して変更できる属性は4つあります。

* `isDeep`
* `inherit`
* `translate`
* `updateDestinationLanguage`

### isDeep {#isdeep}

**`isDeep`**  はノードフィルターに適用され、デフォルトではtrueです。ノード（またはその上位ノード）に、フィルターで指定されたプロパティ値を持つそのプロパティが含まれているかどうかをチェックします。false の場合は、現在のノードのみでチェックします。

例えば、親ノードがプロパティ`draftOnly`をtrueに設定してドラフトコンテンツにフラグを付けている場合でも、子ノードが翻訳ジョブに追加されます。 ここで、`isDeep` が機能し、親ノードの `draftOnly` プロパティが true であるかどうかをチェックして、それらの子ノードを除外します。

エディターの「**フィルター**」タブで、「**深い**」をオンまたはオフにできます。

![フィルタールール](../assets/translation-rules-editor-filters.png)

UIで&#x200B;**Is Deep**&#x200B;がオフになっている場合に表示されるXMLの例を次に示します。

```xml
 <filter>
    <node containsProperty="draftOnly" isDeep="false" propertyValue="true"/>
</filter>
```

### inherit {#inherit}

**`inherit`** はプロパティに適用できます。デフォルトでは、すべてのプロパティが継承されますが、一部のプロパティを子ノードに継承させない場合は、このプロパティをfalseに設定して、特定のノードにのみ適用することができます。

UI では、「**プロパティ**」タブで「**継承**」をチェックまたはチェック解除できます。

### translate {#translate}

**`translate`** は、プロパティを変換するかどうかを指定する目的でのみ使用します。

UIの「**プロパティ**」タブで、「**翻訳**」のチェック/チェックを外します。

### updateDestinationLanguage {#updatedestinationlanguage}

**`updateDestinationLanguage`** は、テキスト以外の言語コードを持つプロパティ(例： `jcr:language`)に使用します。ユーザーはテキストを翻訳していませんが、ソースから宛先への言語ロケールを設定します。そのようなプロパティは、翻訳用に送信されません。

UIで、「**プロパティ**」タブの「**翻訳**」をオンまたはオフにして、この値を変更できます。ただし、言語コードを値として持つ特定のプロパティに対しては、この値を変更できます。

`updateDestinationLanguage` と `translate` の違いを明確にするために、ルールが 2 つのみのコンテキストの単純な例を次に示します。

![updateDestinationLanguageの例](../assets/translation-rules-updatedestinationlanguage.png)

xml での結果は、次のようになります。

```xml
<property inherit="true" name="text" translate="true" updateDestinationLanguage="false"/>
<property inherit="true" name="jcr:language" translate="false" updateDestinationLanguage="true"/>
```

## ルールファイルの手動編集  {#editing-the-rules-file-manually}

AEMと共にインストールされる`translation_rules.xml`ファイルには、デフォルトの変換ルールのセットが含まれています。 このファイルを編集して、翻訳プロジェクトの要件を満たすことができます。 例えば、カスタムコンポーネントのコンテンツが翻訳されるようにルールを追加できます。

`translation_rules.xml`ファイルを編集する場合は、バックアップコピーをコンテンツパッケージに保存します。 特定のAEMパッケージを再インストールすると、現在の`translation_rules.xml`ファイルを元のファイルに置き換えることができます。 この状況でルールを復元するには、バックアップコピーを含むパッケージをインストールします。

>[!NOTE]
>
>コンテンツパッケージを作成した後は、ファイルを編集するたびにパッケージを再ビルドしてください。

## 翻訳ルールファイルのサンプル  {#example-translation-rules-file}

```xml
<?xml version="1.0" encoding="UTF-8"?><nodelist>
  <node path="/content">
    <property name="addLabel"/>
    <property name="allowedResponses"/>
    <property name="alt"/>
    <property name="attachFileLabel"/>
    <property name="benefits"/>
    <property name="buttonLabel"/>
    <property name="chartAlt"/>
    <property name="confirmationMessageToggle"/>
    <property name="confirmationMessageUntoggle"/>
    <property name="constraintMessage"/>
    <property name="contentLabel"/>
    <property name="denyText"/>
    <property name="detailDescription"/>
    <property name="emptyText"/>
    <property name="helpMessage"/>
    <property name="image/alt"/>
    <property name="image/jcr:description"/>
    <property name="image/jcr:title"/>
    <property name="jcr:description"/>
    <property name="jcr:title"/>
    <property name="heading"/>
    <property name="label"/>
    <property name="main"/>
    <property name="listLabel"/>
    <property name="moreText"/>
    <property name="pageTitle"/>
    <property name="placeholder"/>
    <property name="requiredMessage"/>
    <property name="resetTitle"/>
    <property name="subjectLabel"/>
    <property name="subtitle"/>
    <property name="tableData"/>
    <property name="text"/>
    <property name="title"/>
    <property name="navTitle"/>
    <property name="titleDivContent"/>
    <property name="toggleLabel"/>
    <property name="transitionLabel"/>
    <property name="untoggleLabel"/>
    <property name="name"/>
    <property name="occupations"/>
    <property name="greetingLabel"/>
    <property name="signInLabel"/>
    <property name="signOutLabel"/>
    <property name="pretitle"/>
    <property name="cq:panelTitle"/>
    <property name="actionText"/>
    <property name="cq:language" updateDestinationLanguage="true"/>
    <node pathContains="/cq:annotations">
      <property name="text" translate="false"/>
    </node>
    <node path="/content/wknd"/>
  </node>
  <node path="/content/forms">
    <property name="text" translate="false"/>
  </node>
  <node path="/content/dam">
    <property name="dc:description"/>
    <property name="dc:rights"/>
    <property name="dc:subject"/>
    <property name="dc:title"/>
    <property name="defaultContent"/>
    <property name="jcr:description"/>
    <property name="jcr:title"/>
    <property name="pdf:Title"/>
    <property name="xmpRights:UsageTerms"/>
    <property name="main"/>
    <property name="adventureActivity"/>
    <property name="adventureDescription"/>
    <property name="adventureDifficulty"/>
    <property name="adventureGearList"/>
    <property name="adventureGroupSize"/>
    <property name="adventureItinerary"/>
    <property name="adventurePrice"/>
    <property name="adventureTitle"/>
    <property name="adventureTripLength"/>
    <property name="adventureType"/>
    <node pathContains="/jcr:content/metadata/predictedTags">
      <property name="name"/>
    </node>
  </node>
  <assetNode assetReferenceAttribute="fragmentPath" resourceType="cq/experience-fragments/editor/components/experiencefragment"/>
  <assetNode assetReferenceAttribute="fragmentVariationPath" resourceType="core/wcm/components/experiencefragment/v1/experiencefragment"/>
  <assetNode assetReferenceAttribute="fileReference" resourceType="dam/cfm/components/contentfragment"/>
  <assetNode resourceType="docs/components/download"/>
  <assetNode resourceType="docs/components/image"/>
  <assetNode assetReferenceAttribute="fileReference" resourceType="foundation/components/image"/>
  <assetNode assetReferenceAttribute="asset" resourceType="foundation/components/video"/>
  <assetNode assetReferenceAttribute="fileReference" resourceType="foundation/components/download"/>
  <assetNode assetReferenceAttribute="fileReference" resourceType="core/wcm/components/download/v1/download"/>
  <assetNode assetReferenceAttribute="fileReference" resourceType="wcm/foundation/components/image"/>
  <assetNode assetReferenceAttribute="fragmentPath" resourceType="core/wcm/components/contentfragment/v1/contentfragment"/>
  <assetNode assetReferenceAttribute="fileReference" resourceType="core/wcm/components/image/v2/image"/>
</nodelist>
```
