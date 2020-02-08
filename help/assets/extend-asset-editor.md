---
title: アセットエディタの拡張
description: カスタムコンポーネントを使用してアセットエディターの機能を拡張する方法について説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# アセットエディターの拡張 {#extending-asset-editor}

アセットエディターは、アセット共有を使用して見つけたアセットをクリックすると開くページです。アセットエディターでは、メタデータ、サムネール、タイトルおよびタグなどのアセットの特性を編集できます。

Configuration of the editor using the predefined editing components is covered in [Creating and Configuring an Asset Editor Page](https://helpx.adobe.com/experience-manager/6-5/assets/using/assets-finder-editor.html).

Adobe Enterprise Manager（AEM）開発者は、既存のエディターコンポーネントを使用するだけでなく、独自のコンポーネントを作成することもできます。

## アセットエディターテンプレートの作成 {#creating-an-asset-editor-template}

geometrixx には次のサンプルページがあります。

* Geometrixxサンプルページ： `/content/geometrixx/en/press/asseteditor.html`
* サンプルテンプレート： `/apps/geometrixx/templates/asseteditor`
* サンプルページコンポーネント： `/apps/geometrixx/components/asseteditor`

### clientlib の設定 {#configuring-clientlib}

AEM Assets コンポーネントでは、WCM 編集 clientlib の拡張が使用されます。clientlib は通常、`init.jsp` に読み込まれます。

デフォルトの（コアの `init.jsp` での）clientlib の読み込みとは異なり、AEM Assets テンプレートには以下が必要な条件となります。

* The template must include the `cq.dam.edit` clientlib (instead of `cq.wcm.edit`).

* clientlib は無効な WCM モード（例えば、「**公開**」での読み込み）でも、述語、アクション、レンズをレンダリングするために含める必要があります。

In most cases, copying the existing sample `init.jsp` (`/apps/geometrixx/components/asseteditor/init.jsp`) should meet these needs.

### JS アクションの設定 {#configuring-js-actions}

Some of the AEM Assets components require JS functions defined in `component.js`. このファイルをコンポーネントディレクトリにコピーしてリンクします。

```xml
<script type="text/javascript" src="<%= component.getPath() %>/component.js"></script>
```

The sample loads this javascript source in `head.jsp`(`/apps/geometrixx/components/asseteditor/head.jsp`).

### 追加のスタイルシート {#additional-style-sheets}

一部のAEM AssetsコンポーネントはAEMウィジェットライブラリを使用します。 コンテンツコンテキストで正常にレンダリングするには、追加のスタイルシートを読み込む必要があります。タグアクションコンポーネントでは、さらにもう 1 つのスタイルシートが必要です。

```xml
<link href="/etc/designs/geometrixx/ui.widgets.css" rel="stylesheet" type="text/css">
```

### Geometrixx スタイルシート {#geometrixx-style-sheet}

The sample page components require that all selectors start with `.asseteditor` of `static.css` (`/etc/designs/geometrixx/static.css`). Best practice: Copy all `.asseteditor` selectors to your style sheet and adjust the rules as desired.

### FormChooser：最終的に読み込まれるリソースの適用 {#formchooser-adjustments-for-eventually-loaded-resources}

アセットエディターは Form Chooser を使用しています。これにより、フォームセレクターとフォームのパスをアセットの URL に追加するだけで、同じフォームページでリソース（ここではアセット）を編集できるようになります。

次に例を示します。

* プレーンフォームページ：[http://localhost:4502/content/geometrixx/jp/press/asseteditor.html](http://localhost:4502/content/geometrixx/en/press/asseteditor.html)
* フォームページに読み込まれるアセット：[](http://localhost:4502/content/dam/geometrixx/icons/diamond.png.form.html/content/geometrixx/en/press/asseteditor.html)http://localhost:4502/content/dam/geometrixx/icons/diamond.png.form.html/content/geometrixx/jp/press/asseteditor.html

The sample handles in `head.jsp` (`/apps/geometrixx/components/asseteditor/head.jsp`) do the following:

* アセットが読み込まれるか、またはプレーンフォームが表示される必要があるかを検出します。
* アセットが読み込まれると、parsys はプレーンフォームページでしか編集できないので、WCM モードを無効にします。
* アセットが読み込まれると、フォームページのタイトルではなくアセットのタイトルを使用します。

```java
 List<Resource> resources = FormsHelper.getFormEditResources(slingRequest);
    if (resources != null) {
        if (resources.size() == 1) {
            // single resource
            FormsHelper.setFormLoadResource(slingRequest, resources.get(0));
        } else if (resources.size() > 1) {
            // multiple resources
            // not supported by CQ 5.3
        }
    }
    Resource loadResource = (Resource) request.getAttribute("cq.form.loadresource");
    String title;
    if (loadResource != null) {
        // an asset is loaded: disable WCM
        WCMMode.DISABLED.toRequest(request);

        String path = loadResource.getPath();
        Asset asset = loadResource.adaptTo(Asset.class);
        try {
            // it might happen that the adobe xmp lib creates an array
            Object titleObj = asset.getMetadata("dc:title");
            if (titleObj instanceof Object[]) {
                Object[] titleArray = (Object[]) titleObj;
                title = (titleArray.length > 0) ? titleArray[0].toString() : "";
            } else {
                title = titleObj.toString();
            }
        }
        catch (NullPointerException e) {
            title = path.substring(path.lastIndexOf("/") + 1);
        }
    }
    else {
        title = currentPage.getTitle() == null ? currentPage.getName() : currentPage.getTitle();
    }
```

HTML 部分で、先頭のタイトルセット（アセットまたはページのタイトル）を使用します。

```xml
<title><%= title %></title>
```

## シンプルなフォームフィールドコンポーネントの作成 {#creating-a-simple-form-field-component}

この例では、読み込んだアセットのメタデータを表示するコンポーネントを作成する方法を説明します。

1. Create a component folder in your projects directory, for example, `/apps/geometrixx/components/samplemeta`.
1. 次のスニ `content.xml` ペットを使用して追加します。

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Image Dimension"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Asset Editor"/>
   ```

1. 次のスニ `samplemeta.jsp` ペットを使用して追加します。

   ```xml
   <%--
   
     Sample metadata field comopnent
   
   --%><%@ page import="com.day.cq.dam.api.Asset,
                    java.security.AccessControlException" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       String value = "";
       String name = "dam:sampleMetadata";
       boolean readOnly = false;
   
       // If the form page is requested for an asset loadResource will be the asset.
       Resource loadResource = (Resource) request.getAttribute("cq.form.loadresource");
   
       if (loadResource != null) {
   
           // Determine if the loaded asset is read only.
           Session session = slingRequest.getResourceResolver().adaptTo(Session.class);
           try {
               session.checkPermission(loadResource.getPath(), "set_property");
               readOnly = false;
           }
           catch (AccessControlException ace) {
               // checkPermission throws exception if asset is read only
               readOnly = true;
           }
           catch (RepositoryException re) {}
   
           // Get the value of the metadata.
           Asset asset = loadResource.adaptTo(Asset.class);
           try {
               value = asset.getMetadata(name).toString();
           }
           catch (NullPointerException npe) {
               // no metadata dc:description available
           }
       }
   %>
   <div class="form_row">
       <div class="form_leftcol">
           <div class="form_leftcollabel">Sample Metadata</div>
       </div>
       <div class="form_rightcol">
           <%
           if (readOnly) {
               %><c:out value="<%= value %>"/><%
           }
           else {
               %><input class="text" type="text" name="./jcr:content/metadata/<%= name %>" value="<c:out value="<%= value %>" />"><%
           }%>
       </div>
   </div>
   ```

1. コンポーネントを使用できるようにするには、それを編集可能にする必要があります。To make a component editable, in CRXDE Lite, add a node `cq:editConfig` of primary type `cq:EditConfig`. 段落を削除できるよう、値を複数設定できるプロパティ `cq:actions` を追加し、値として `DELETE` のみを設定します。

1. ブラウザーを開き、サンプルページ（`asseteditor.html` など）でデザインモードに切り替え、段落システム用の新しいコンポーネントを有効にします。

1. **編集**&#x200B;モードで、新しいコンポーネント（**Sample Metadata** など）がサイドキック（**アセットエディター**&#x200B;グループ内）で使用できます。コンポーネントを挿入します。メタデータを格納できるようにするには、メタデータフォームに追加する必要があります。

## メタデータオプションの変更 {#modifying-metadata-options}

[メタデータフォーム](https://helpx.adobe.com/experience-manager/6-5/assets/using/assets-finder-editor.html)で利用可能な名前空間を変更できます。

Currently available metadata are defined in `/libs/dam/options/metadata`:

* このディレクトリの最初のレベルには名前空間が保存されています。
* 各名前空間内のアイテムは、ローカルパーツアイテムの結果などのメタデータを表します。
* メタデータの内容には、タイプと複数値の各オプションが含まれています。

The options can be overwritten in `/apps/dam/options/metadata`:

1. Copy the directory from `/libs` to `/apps`.

1. アイテムを削除、変更、または追加します。

>[!NOTE]
>
>新しい名前空間を追加した場合、リポジトリ／CRX に登録する必要があります。この作業をおこなわない場合、メタデータフォームで送信をおこなうとエラーが発生します。
