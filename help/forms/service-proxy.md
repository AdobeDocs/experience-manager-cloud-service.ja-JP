---
title: HTML5 forms サービスプロキシ
description: HTML5 フォームサービスプロキシは、送信サービスのためのプロキシを登録する設定です。サービスプロキシを設定するには、リクエストパラメーター submissionServiceProxy を使って送信サービスの URL を指定します。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms,Mobile Forms
exl-id: 8f9b10ae-1600-49c2-a061-153a2a89c67e
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 22aeedaaf4171ad295199a989e659b6bf5ce9834
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 96%

---

# HTML5 forms サービスプロキシ{#html-forms-service-proxy}

<span class="preview"> HTML5 Forms機能は、早期アクセスプログラムの一部として提供されています。 アクセスをリクエストするには、公式（職場）メール ID からaem-forms-ea@adobe.comにメールを送信します。
</span>

HTML5 フォームサービスプロキシは、送信サービスのためのプロキシを登録する設定です。サービスプロキシを設定するには、リクエストパラメーター *submissionServiceProxy* を使って送信サービスの URL を指定します。

## サービスプロキシの利点 {#benefits-of-service-proxy-br}

サービスプロキシは次の問題点を解消します。

* HTML5 フォームワークフローでは、HTML5 フォームユーザーに対して送信サービス「//content/xfaforms/submission/default」を開く必要があります。これにより、AEM サーバーは意図しない多くのオーディエンスにさらされてしまいます。
* サービス URL は、フォームのランタイムモデルに埋め込まれます。サービス URL パスを変更することはできません。
* 送信は 2 段階のプロセスです。フォームデータを送信するには、サーバーに対して少なくとも 2 回の送信が必要です。これにより、サーバーでの負荷が増大します。
* HTML5 forms は、PDF リクエストの代わりに POST リクエストでデータを送信します。PDF と HTML5 forms の両方が関与するワークフローの場合、2 つの異なる方法による送信処理が必要となります。

### トポロジー {#topologies-br}

HTML5 フォームは、次のトポロジを使用して AEM サーバーに接続します。

* AEM サーバーまたは HTML5 フォームが POST 経由でデータをサーバーに送信するトポロジ。
* プロキシサーバーが POST データをサーバーに送信するトポロジー。

![HTML5 forms サービスプロキシのトポロジー](assets/topology.png)

HTML5 forms サービスプロキシのトポロジー

HTML5 フォームは AEM サーバーに接続して、サーバーサイドのスクリプト、web サービスおよび送信を実行します。HTML5 フォームの XFA ランタイムは、様々なパラメーターを使用して「/bin/xfaforms/submitaction」エンドポイントに対して Ajax 呼び出しを行い、AEM サーバーに接続します。HTML5 フォームは AEM サーバーに接続して、次の操作を実行します。

#### サーバーサイドスクリプトと web サービスを実行 {#execute-server-sided-scripts-and-web-services}

サーバー上で実行するようにマークされているスクリプトは、「サーバーサイドスクリプト」と呼ばれます。サーバーサイドスクリプトと web サービスで使用されるすべてのパラメーターを下表に示します。

<table>
 <tbody>
  <tr>
   <td><p><strong>パラメーター</strong></p> </td>
   <td><p><strong>説明</strong></p> </td>
  </tr>
  <tr>
   <td><p>activity</p> </td>
   <td><p>activity は、リクエストをトリガーするイベントを指定します。例：クリック、終了、変更など</p> </td>
  </tr>
  <tr>
   <td><p>contextSom</p> </td>
   <td><p>contextSom は、イベントが実行されるオブジェクトの SOM 式を指定します。</p> </td>
  </tr>
  <tr>
   <td><p>テンプレート</p> </td>
   <td><p>Template は、フォームをレンダリングするために使用するテンプレートを指定します。</p> </td>
  </tr>
  <tr>
   <td><p>contentRoot</p> </td>
   <td><p>contentRoot は、フォームをレンダリングするために使用するテンプレートルートディレクトリを指定します。</p> </td>
  </tr>
  <tr>
   <td><p>データ</p> </td>
   <td><p>Data は、フォームをレンダリングするために使用するデータバイトを指定します。</p> </td>
  </tr>
  <tr>
   <td><p>formDom</p> </td>
   <td><p>formDom は、HTML5 フォームの DOM を JSON 形式で指定します。</p> </td>
  </tr>
  <tr>
   <td><p>packet</p> </td>
   <td><p>packet は、フォームとして指定されます。</p> </td>
  </tr>
  <tr>
   <td><p>debugDir</p> </td>
   <td><p>debugDir は、フォームをレンダリングするために使用するデバッグディレクトリを指定します。</p> </td>
  </tr>
 </tbody>
</table>

#### データを送信 {#submit-data}

「送信」ボタンをクリックすると、HTML5 フォームはデータをサーバーに送信します。HTML5 フォームがサーバーに送信するすべてのパラメーターを次の表に示します。

<table>
 <tbody>
  <tr>
   <td><p><strong>パラメーター</strong></p> </td>
   <td><p><strong>説明</strong></p> </td>
  </tr>
  <tr>
   <td><p>テンプレート</p> </td>
   <td><p>フォームをレンダリングするために使用するテンプレート。</p> </td>
  </tr>
  <tr>
   <td><p>contentRoot</p> </td>
   <td><p>フォームをレンダリングするために使用するテンプレートルートディレクトリ。</p> </td>
  </tr>
  <tr>
   <td><p>データ</p> </td>
   <td><p>フォームをレンダリングするために使用するデータバイト。</p> </td>
  </tr>
  <tr>
   <td><p>formDom</p> </td>
   <td><p>JSON 形式の HTML5 フォームの DOM。</p> </td>
  </tr>
  <tr>
   <td><p>submiturl</p> </td>
   <td><p>データ XML が投稿される URL。</p> </td>
  </tr>
  <tr>
   <td><p>debugDir</p> </td>
   <td><p>フォームをレンダリングするために使用するデバッグディレクトリ。</p> </td>
  </tr>
 </tbody>
</table>

#### 送信プロキシはどのように機能しますか？ {#how-nbsp-the-nbsp-submit-proxy-works}

送信サービスプロキシは、submiturl がリクエストパラメーター内に存在しない場合に、パススルーとして機能します。これはパススルーとして機能します。これはリクエストを /bin/xfaforms/submitaction エンドポイントに送信し、応答を XFA ランタイムに送信します。

送信サービスプロキシは、submiturl がリクエストパラメーター内に存在する場合は、トポロジを選択します。

* AEM サーバーがデータを投稿する場合、プロキシサーバーはパススルーとして機能します。これはリクエストを /bin/xfaforms/submitaction エンドポイントに送信し、応答を XFA ランタイムに送信します。
* プロキシがデータを送信すると、プロキシサービスは、submitUrl を除くすべてのパラメーターを */bin/xfaforms/submitaction* エンドポイントに渡し、応答ストリームで xml バイトを受け取ります。次に、プロキシサービスはデータ xml バイトを submitUrl に投稿して処理します。

* データ（POST リクエスト）をサーバーに送信する前に、HTML5 フォームはサーバーに接続していて使用できることを確認します。接続と可用性を確認するために、HTML フォームは空の HEAD リクエストをサーバーに送信します。サーバーが使用できる場合は、HTML5 フォームはデータ（POST リクエスト）をサーバーに送信します。サーバーが使用できない場合は、エラーメッセージ「*サーバーに接続できませんでした*」が表示されます。この事前の検出により、ユーザーがフォームに再記入するなどの問題を回避できます。プロキシサーブレットがヘッドリクエストを処理し、例外をスローしません。
