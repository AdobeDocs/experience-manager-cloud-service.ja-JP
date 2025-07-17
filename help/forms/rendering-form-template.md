---
title: HTML5 forms 用のフォームテンプレートのレンダリング
description: HTML5 フォームのプロファイルは、プロファイルレンダーに関連付けられています。プロファイルレンダーは、Forms OSGi サービスを呼び出してフォームの HTML 表現を生成する役割を持つ JSP ページです。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: cb75b826-d044-44be-b364-790c046513e0
feature: HTML5 Forms,Mobile Forms
exl-id: 022b9953-2d64-473f-87b7-aac1602f6a7e
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 22aeedaaf4171ad295199a989e659b6bf5ce9834
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 95%

---

# HTML5 forms 用のフォームテンプレートのレンダリング {#rendering-form-template-for-html-forms}

<span class="preview"> HTML5 Forms機能は、早期アクセスプログラムの一部として提供されています。 アクセスをリクエストするには、公式（職場）メール ID からaem-forms-ea@adobe.comにメールを送信します。
</span>

## レンダーエンドポイント {#render-endpoint}

HTML5 forms には、フォームテンプレートのモバイルレンダリングを可能にするため、REST エンドポイントとして公開される&#x200B;**プロファイル**&#x200B;の概念があります。これらのプロファイルには関連する&#x200B;**プロファイルレンダラー**&#x200B;があります。それらは Forms OSGi サービスを呼び出すことでフォームの HTML 表現を生成する役割を持つ JSP ページです。プロファイルノードの JCR パスによって、レンダーエンドポイントの URL が決定されます。「default」プロファイルを指すフォームのデフォルトのレンダーエンドポイントは、次のようになります。

https://&lt;*host*>:&lt;*port*>/content/xfaforms/profiles/default.html?contentRoot=&lt;*path of the folder containg form xdp*>&amp;template=&lt;*name of the xdp*>

例：`http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=c:/xdps&template=sampleForm.xdp`

カスタムプロファイルでは、それに応じてエンドポイントが変わります。例えば、hrforms という名前を持つカスタムプロファイルのエンドポイントは次のようになります。

`http://localhost:4502/content/xfaforms/profiles/hrforms.html?contentRoot=c:/xdps&template=sampleForm.xdp`

テンプレートが FormSubmission と呼ばれるアプリケーションの AEM リポジトリにある場合、URI は次のとおりです。

```http
http://localhost:4502/content/xfaforms/profiles/default.html?
 contentRoot=crx:///content/dam/formsanddocuments/FormSubmission/1.0
 &template=sampleForm.xdp
```

## レンダーパラメーター {#render-parameters}

次に、HTML 形式でフォームをレンダリングする場合にサポートされるリクエストパラメーターを示します。

<table>
 <tbody>
  <tr>
   <th><strong>パラメーター </strong></th>
   <th><strong>説明</strong></th>
  </tr>
  <tr>
   <td>テンプレート <br /> </td>
   <td>このパラメーターは、テンプレートファイルの名前を指定します。<br /> </td>
  </tr>
  <tr>
   <td>contentRoot<br /> </td>
   <td>このパラメーターは、テンプレートとそれに関連するリソースが存在するパスを指定します。このパスには、サーバーのファイルシステムパス、リポジトリパス、http または ftp パスを使用できます。<br /> </td>
  </tr>
  <tr>
   <td>submitUrl<br /> </td>
   <td>このパラメーターは、フォームデータの XML が投稿される URL を指定します。<br /> </td>
  </tr>
 </tbody>
</table>

### フォームテンプレートとデータを結合 {#merge-data-with-form-template}

| パラメーター | 説明 |
|---|---|
| dataRef | このパラメーターはテンプレートと結合されるデータファイルの&#x200B;**絶対パス**&#x200B;を指定します。このパラメーターには XML 形式データを返す REST サービスへの URL を使用できます。 |
| data | このパラメーターは、テンプレートと結合される UTF-8 エンコードされたデータバイトを指定します。このパラメーターが指定されている場合、HTML5 フォームは dataRef パラメーターを無視します。 |

### レンダーパラメーターの送信 {#passing-the-render-parameter}

HTML5 フォームは、3 つの方法によるレンダーパラメーターの送信をサポートしています。URL、キーと値のペアおよびプロファイルノードを使用してパラメーターを送信することができます。レンダーパラメーターでは、キーと値のペアの優先度が最も高く、次に優先度が高いのがプロファイルノードです。URL リクエストパラメーターは最低の優先度を持ちます。

* **URL リクエストパラメーター**: レンダリングパラメーターを URL で指定できます。URL リクエストパラメーターでは、パラメーターがエンドユーザーに対して表示されます。例えば送信 URL `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=/Applications/FormSubmission/1.0&template=sampleForm.xdp` には、その中にテンプレートパラメーターが含まれます。

* **SetAttribute リクエストパラメーター**: レンダリングパラメーターをキー値ペアとして指定できます。SetAttribute リクエストパラメーターでは、パラメーターがエンドユーザーに対して表示されません。リクエストを他の JSP から HTML5 フォームのプロファイルレンダ― JSP に転送し、リクエストオブジェクトで *setAttribute* を使用してすべてのレンダーパラメーターを渡すことができます。この方法が最も優先されます。

* **プロファイルノードリクエストパラメーター：**&#x200B;レンダリングパラメーターをプロファイルノードのノードプロパティとして指定できます。プロファイルノードリクエストパラメーターでは、パラメーターがエンドユーザーに対して表示されません。プロファイルノードは、リクエストが送信されるノードです。パラメーターをノードプロパティとして指定するには、CRXDE lite を使用します。

### 送信パラメーター {#submit-parameters}

HTML5 フォームはデータを送信し、サーバーサイドのスクリプトおよび web サービスを AEM サーバーで実行します。サーバーサイドのスクリプトと web サービスを AEM サーバーで実行するために使用するパラメーターについて詳しくは、[HTML5 フォームサービスプロキシ](/help/forms/service-proxy.md)を参照してください。
