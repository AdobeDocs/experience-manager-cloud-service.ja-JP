---
title: Adobe Experience Manager Assetsの検索オプションと機能の拡張
description: アセットの検索機能を拡張します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# アセット検索の拡張 {#extend-assets-search}

Adobe Experience Manager(AEM)Assets検索機能を拡張できます。 AEM Assets はデフォルトで、文字列によってアセットを検索します。

検索は QueryBuilder インターフェイスを介して実行されるので、複数の述語を使用することで検索をカスタマイズできます。You can overlay the default set of predicates in the following directory: `/apps/dam/content/search/searchpanel/facets`.

AEM Assetsの管理パネルにタブを追加することもできます。

## オーバーレイ {#overlay}

To overlay the preconfigured predicates, copy the `facets` node from `/libs/dam/content/search/searchpanel` to `/apps/dam/content/search/searchpanel/` or specify another `facetURL` property in the searchpanel configuration (the default is to `/libs/dam/content/search/searchpanel/facets.overlay.infinity.json`).

>[!NOTE]
>
>By default, the directory structure under `/apps` does not exist and needs to be created. Ensure that the node types match those under `/libs`.

### タブの追加 {#add-tabs}

追加の検索タブを追加するには、AEM Assets管理者で設定します。 追加のタブは以下の手順で作成します。

1. Create the folder structure `/apps/wcm/core/content/damadmin/tabs,`if it does not already exist, and copy the `tabs` node from `/libs/wcm/core/content/damadmin` and paste it.
1. 必要に応じて、2 つ目のタブを作成して設定します。

   >[!NOTE]
   >
   >When you create a second `siteadminsearchpanel`, be sure to set an `id` property in order to prevent form conflicts.

### カスタム述語の作成 {#create-custom-predicates}

AEM Assetsには、アセット共有ページのカスタマイズに使用できる事前定義済み述語のセットが付属しています。
<!-- In addition to using pre-existing predicates, AEM developers can also create their own predicates using the [Query Builder API](/help/sites-developing/querybuilder-api.md). -->

カスタムの述語を作成するには、[ウィジェットフレームワーク](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html)に関する基本的な知識が必要です。

ベストプラクティスとしては、既存の述語をコピー後に変更することです。サンプルの述語は、**/libs/cq/search/components/predicates** にあります。

#### 例：シンプルなプロパティ述語の作成 {#example-build-a-simple-property-predicate}

プロパティ述語の作成手順

1. プロジェクトディレクトリにコンポーネントフォルダーを作成します（**/apps/geometrixx/components/titlepredicate** など）。
1. 次の **content.xml** を追加します。

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Title Predicate"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Search"/>
   ```

1. ページの URL の末尾に `titlepredicate.jsp`.

   ```xml
   <%--
   
     Sample title predicate component
   
   --%><%@ page import="java.util.Calendar" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       // A unique id is necessary in case this predicate is inserted multiple times on the same page
       String elemId = "cq-predicate-" +  Long.toString(Calendar.getInstance().getTimeInMillis());
   
   %><div class="predicatebox">
   
       <div class="title">Title</div>
   
       <%-- The wrapper for the form elements. All items will be append to this wrapper. --%>
       <div id="<%= elemId %>" class="content"></div>
   
   </div><script type="text/javascript">
   
       CQ.Ext.onLoad(function() {
   
           var predicateName = "property";
           var propertyName = "jcr:content/metadata/dc:title";
           var elemId = "<%= elemId %>";
   
           // Get the page wide available QueryBuilder.
           var qb = CQ.search.Util.getQueryBuilder();
   
           // createId adds a counter to the predicate name - useful in case this predicate
           // is inserted multiple times on the same page.
           var id = qb.createId(predicateName);
   
           // Hidden field that defines the property to search for; in our case this
           // is the "dc:title" metadata. The name "property" (or "1_property", "2_property" etc.)
           // indicates the server to use the property predicate
           // (com.day.cq.search.eval.JcrPropertyPredicateEvaluator).
           qb.addField({
               "xtype": "hidden",
               "renderTo": elemId,
               "name": id,
               "value": propertyName
           });
   
           // The visible text field. The name has to be like the one of the hidden field above
           // plus the ".value" suffix.
           qb.addField({
               "xtype": "textfield",
               "renderTo": elemId,
               "name": id + ".value"
           });
   
           // Depending on the predicate additional parameters allow to configure the
           // predicate. Here we add an operation parameter to create a "like" query.
           // Again note the name set to the id and a suffix.
           qb.addField({
               "xtype": "hidden",
               "renderTo": elemId,
               "name": id + ".operation",
               "value": "like"
           });
       });
   </script>
   ```

1. コンポーネントを使用できるようにするには、それを編集可能にする必要があります。コンポーネントを編集可能にするには、CRXDE で、**cq:EditConfig** プライマリ型の **cq:editConfig** ノードを追加します。段落を削除できるように、**DELETE** という 1 つの値を持つ複数値プロパティ **cq:actions** を追加します。
1. ブラウザーを開き、サンプルページ（**press.html** など）でデザインモードに切り替えて、述語段落システムの新しいコンポーネント（「**左揃え**」など）を有効にします。

1. **編集**&#x200B;モードで、新しいコンポーネントがサイドキック（**検索**&#x200B;グループ）で使用できるようになります。「**Predicates**」列にコンポーネントを挿入し、「**Diamond**」などの検索語句を入力して、虫眼鏡アイコンをクリックして検索を開始します。

   >[!NOTE]
   >
   >検索時は、大文字と小文字の違いを含めて、語句を正確に入力してください。

#### 例：シンプルなグループ述語の作成 {#example-build-a-simple-group-predicate}

グループ述語の作成手順

1. プロジェクトディレクトリにコンポーネントフォルダーを作成します（**/apps/geometrixx/components/picspredicate** など）。
1. 次の **content.xml** を追加します。

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Image Formats"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Search"/>
   ```

1. 次の **titlepredicate.jsp** を追加します。

   ```xml
   <%--
   
     Sample group predicate component
   
   --%><%@ page import="java.util.Calendar" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       // A unique id is necessary in case this predicate is inserted multiple times on the same page.
       String elemId = "cq-predicate-" +  Long.toString(Calendar.getInstance().getTimeInMillis());
   
   %><div class="predicatebox">
   
       <div class="title">Image Formats</div>
   
       <%-- The wrapper for the form elements. All items will be append to this wrapper. --%>
       <div id="<%= elemId %>" class="content"></div>
   
   </div><script type="text/javascript">
   
       CQ.Ext.onLoad(function() {
   
           var predicateName = "property";
           var propertyName = "jcr:content/metadata/dc:format";
           var elemId = "<%= elemId %>";
   
           // Get the page wide available QueryBuilder.
           var qb = CQ.search.Util.getQueryBuilder();
   
           // Create a unique group ID; will return e.g. "1_group".
           var groupId = qb.createGroupId();
   
           // Hidden field that defines the property to search for  - in our case "dc:format" -
           // and declares the group of predicates. "property" in the name ("1_group.property")
           // indicates to the server to use the "property predicate"
           // (com.day.cq.search.eval.JcrPropertyPredicateEvaluator).
           qb.addField({
               "xtype": "hidden",
               "renderTo": "<%= elemId %>",
               "name": groupId + "." + predicateName, // 1_group.property
               "value": propertyName
           });
   
           // Declare to combine the multiple values using OR.
           qb.add(new CQ.Ext.form.Hidden({
               "name": groupId + ".p.or",  // 1_group.p.or
               "value": "true"
           }));
   
           // The options
           var options = [
               { "label":"JPEG", "value":"image/jpeg"},
               { "label":"PNG",  "value":"image/png" },
               { "label":"GIF",  "value":"image/gif" }
           ];
   
           // Build a checkbox for each option.
           for (var i = 0; i < options.length; i++) {
               qb.addField({
                   "xtype": "checkbox",
                   "renderTo": "<%= elemId %>",
                   // 1_group.property.0_value, 1_group.property.1_value etc.
                   "name": groupId + "." +  predicateName + "." + i + "_value",
                   "inputValue": options[i].value,
                   "boxLabel": options[i].label,
                   "listeners": {
                       "check": function() {
                           // Submit the search form when checking/unchecking a checkbox.
                           qb.submit();
                       }
                   }
               });
           }
       });
   ```

1. コンポーネントを使用できるようにするには、それを編集可能にする必要があります。コンポーネントを編集可能にするには、CRXDE で、**cq:EditConfig** プライマリ型の **cq:editConfig** ノードを追加します。段落を削除できるように、**DELETE** という 1 つの値を持つ複数値プロパティ **cq:actions** を追加します。
1. ブラウザーを開き、サンプルページ（**press.html** など）でデザインモードに切り替えて、述語段落システムの新しいコンポーネント（「**左揃え**」など）を有効にします。
1. **編集**&#x200B;モードで、新しいコンポーネントがサイドキック（**検索**&#x200B;グループ）で使用できるようになります。「**Predicates**」列にコンポーネントを挿入します。

### インストール済みの述語ウィジェット {#installed-predicate-widgets}

事前設定済みの ExtJS ウィジェットでは次の述語が使用可能です。

#### FulltextPredicate {#fulltextpredicate}

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ<br /> </strong></td>
   <td><strong>タイプ</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>predicateName</td>
   <td>文字列</td>
   <td>述語の名前。デフォルトは 'fulltext' です</td>
  </tr>
  <tr>
   <td>searchCallback</td>
   <td>Function</td>
   <td>イベント 'keyup' 発生時の検索を呼び出すためのコールバック。デフォルトは 'CQ.wcm.SiteAdmin.doSearch' です</td>
  </tr>
 </tbody>
</table>

#### PropertyPredicate {#propertypredicate}

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ<br /> </strong></td>
   <td><strong>タイプ</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>predicateName</td>
   <td>文字列</td>
   <td>述語の名前。デフォルト値は 'property' です</td>
  </tr>
  <tr>
   <td>propertyName</td>
   <td>文字列 </td>
   <td>JCR プロパティの名前。デフォルトは 'jcr:title' です</td>
  </tr>
  <tr>
   <td>defaultValue<br /> </td>
   <td>String<br /> </td>
   <td>事前設定されるデフォルト値<br /> </td>
  </tr>
 </tbody>
</table>

#### PathPredicate {#pathpredicate}

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ<br /> </strong></td>
   <td><strong>タイプ</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>predicateName</td>
   <td>文字列</td>
   <td>述語の名前。デフォルトは 'path' です</td>
  </tr>
  <tr>
   <td>rootPath</td>
   <td>文字列 </td>
   <td>述語のルートパス。デフォルトは '/content/dam' です</td>
  </tr>
  <tr>
   <td>pathFieldPredicateName</td>
   <td>文字列</td>
   <td>デフォルトは 'folder' です</td>
  </tr>
  <tr>
   <td>showFlatOption</td>
   <td>Boolean</td>
   <td>「サブフォルダーで検索」チェックボックスを表示するためのフラグ。デフォルトは true です</td>
  </tr>
 </tbody>
</table>

#### DatePredicate {#datepredicate}

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ<br /> </strong></td>
   <td><strong>タイプ</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>predicateName</td>
   <td>文字列</td>
   <td>述語の名前。デフォルトは 'daterange' です</td>
  </tr>
  <tr>
   <td>propertyname</td>
   <td>文字列</td>
   <td>JCR プロパティの名前。デフォルトは 'jcr:content/jcr:lastModified' です</td>
  </tr>
  <tr>
   <td>defaultValue </td>
   <td>文字列 </td>
   <td>事前設定されるデフォルト値 </td>
  </tr>
 </tbody>
</table>

#### OptionsPredicate {#optionspredicate}

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ<br /> </strong></td>
   <td><strong>タイプ</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>title </td>
   <td>文字列 </td>
   <td>最上部のタイトルを追加します </td>
  </tr>
  <tr>
   <td>predicateName</td>
   <td>文字列</td>
   <td>述語の名前。デフォルトは 'daterange' です</td>
  </tr>
  <tr>
   <td>propertyname</td>
   <td>文字列</td>
   <td>JCR プロパティの名前。デフォルトは 'jcr:content/metadata/cq:tags' です</td>
  </tr>
  <tr>
   <td>collapse</td>
   <td>文字列</td>
   <td>折りたたみのレベル。デフォルトは 'level1' です</td>
  </tr>
  <tr>
   <td>triggerSearch</td>
   <td>Boolean </td>
   <td>チェック時の検索を呼び出すためのフラグ。デフォルトは false です</td>
  </tr>
  <tr>
   <td>searchCallback</td>
   <td>Function</td>
   <td>検索を呼び出すためのコールバック。デフォルトは 'CQ.wcm.SiteAdmin.doSearch' です</td>
  </tr>
  <tr>
   <td>searchTimeoutTime</td>
   <td>番号</td>
   <td>タイムアウト。この時間を過ぎると searchCallback が呼び出されます。デフォルトは 800ms です</td>
  </tr>
 </tbody>
</table>
