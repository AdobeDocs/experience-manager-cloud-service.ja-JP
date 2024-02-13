---
title: AEM Developers 向けユニバーサルエディターの概要
description: ユニバーサルエディターの動作とプロジェクトでの使用方法に興味を持つAEM開発者の方は、WKND プロジェクトをユニバーサルエディターと連携させる方法を説明し、エンドツーエンドの紹介を提供します。
exl-id: d6f9ed78-f63f-445a-b354-f10ea37b0e9b
source-git-commit: 3dff6fa71c29da70daba80176d2fe51ef1e05200
workflow-type: tm+mt
source-wordcount: '3139'
ht-degree: 1%

---


# AEM Developers 向けユニバーサルエディターの概要 {#developer-overview}

ユニバーサルエディターの動作とプロジェクトでの使用方法に興味を持つAEM開発者の方は、WKND プロジェクトをユニバーサルエディターと連携させる方法を説明し、エンドツーエンドの紹介を提供します。

{{universal-editor-status}}

## 目的 {#purpose}

このドキュメントは、ユニバーサルエディターの機能と、アプリケーションを使用するための実装方法の両方に関する開発者の紹介として機能します。

これをおこなうには、ほとんどのAEM開発者がなじみのある標準的な例、コアコンポーネントと WKND サイト、およびユニバーサルエディターを使用して編集可能ないくつかのサンプルコンポーネントを実装します。

>[!TIP]
>
>このドキュメントでは、ユニバーサルエディターの仕組みを説明する追加の手順を実行し、開発者がエディターに対する理解を深めるためのものです。 したがって、アプリを実装するための最も直接的なルートは必要ありませんが、ユニバーサルエディターの最も示唆的なものと、その動作の仕組みを取り上げます。
>
>できるだけ早く導入したい場合は、 [AEMでのユニバーサルエディターの概要](/help/implementing/universal-editor/getting-started.md) 文書。

## 前提条件 {#prerequisites}

この概要に従うには、以下を利用できる必要があります。

* [AEM as a Cloud Serviceのローカル開発インスタンス](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=ja)
   * ローカル開発インスタンスは、 [で開発用に HTTPS で設定 `localhost`.](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/use-the-ssl-wizard.html?lang=ja)
   * [WKND デモサイトをインストールする必要があります。](https://github.com/adobe/aem-guides-wknd)
* [ユニバーサルエディターへのアクセス](/help/implementing/universal-editor/getting-started.md#onboarding)
* [ローカルユニバーサルエディターサービス](/help/implementing/universal-editor/local-dev.md) 開発目的で実行する
   * ブラウザーで [ローカルサービスの自己署名証明書を受け入れます。](/help/implementing/universal-editor/local-dev.md#editing)

このドキュメントは、Web 開発に一般に精通しているだけでなく、AEM開発に関する基本的な知識を前提としています。 AEMの開発経験がない場合は、 [続行する前の WKND チュートリアル](/help/implementing/developing/introduction/develop-wknd-tutorial.md)

## AEMを起動し、ユニバーサルエディターにログイン {#sign-in}

まだ実行していない場合は、WKND をインストールし、HTTPS を有効にしてローカルのAEM開発インスタンスを実行しておく必要があります。 [前提条件で詳しく説明しています。](#prerequisites) この概要は、インスタンスがで実行されていることを前提としています。 `https://localhost:8443`.

1. AEM Editor で WKND 英語のメインマスターページを開きます。

   ```text
   https://localhost:8443/editor.html/content/wknd/language-masters/en.html
   ```

1. Adobe Analytics の **ページ情報** エディターのメニューで、「 」を選択します。 **公開済みとして表示**. 新しいタブで同じページが開き、AEMエディターが無効になります。

   ```text
   https://localhost:8443/content/wknd/language-masters/en.html?wcmmode=disabled
   ```

1. このリンクをコピーします。

1. 次に、ユニバーサルエディターにログインします。

   ```text
   https://experience.adobe.com/#/aem/editor
   ```

1. 以前に WKND コンテンツをコピーしたリンクを、 **サイトの URL** ユニバーサルエディターのフィールドをクリックし、 **開く**.

   ![ユニバーサルエディターで WKND ページを開きます。](assets/dev-ue-open.png)

## ユニバーサルエディターがコンテンツの読み込みを試みる {#sameorigin}

ユニバーサルエディタは、フレーム内で編集するコンテンツを読み込みます。 AEMの X-Frame オプションのデフォルト設定により、この問題が回避されます。これは、WKND のローカルコピーを読み込もうとすると、ブラウザーでエラーとして表示され、コンソール出力で詳しく説明されます。

![SAMEORIGIN オプションが原因のブラウザーエラー](assets/dev-sameorigin.png)

X-Frame オプション `sameorigin` は、フレーム内でAEMページをレンダリングできません。 このヘッダーを削除して、ユニバーサルエディターでページを読み込めるようにする必要があります。

1. Configuration Manager を開きます。

   ```text
   https://localhost:8443/system/console/configMgr
   ```

1. OSGi 設定の編集 `org.apache.sling.engine.impl.SlingMainServlet`

   ![SAMEORIGIN の OSGi プロパティ](assets/dev-sameorigin-osgi.png)

1. プロパティを削除します。 `X-Frame-Options=SAMEORIGIN` プロパティの **追加の応答ヘッダー**.

1. 変更を保存します。

次に、ユニバーサルエディターを再読み込みすると、AEMページが読み込まれます。

>[!TIP]
>
>* ドキュメントを見る [AEMでのユニバーサルエディターの概要](/help/implementing/universal-editor/getting-started.md#sameorigin) を参照してください。
>* ドキュメントを見る [Adobe Experience Manager as a Cloud Service用の OSGi の設定](/help/implementing/deploying/configuring-osgi.md) を参照してください。

## 同じサイト cookie の処理 {#samesite-cookies}

ページが読み込まれると、ユニバーサルエディターがAEMのログインページに読み込まれ、変更を加えるための認証が行われていることを確認します。

ただし、正常にサインインできません。 ブラウザーコンソールを表示すると、フレーム上の入力がブロックされていることがわかります。

![入力がブロックされました](assets/dev-cross-origin.png)

ログイントークン cookie は、サードパーティドメインとしてAEMに送信されます。 したがって、AEMで同じサイトの Cookie を許可する必要があります。

1. Configuration Manager を開きます。

   ```text
   https://localhost:8443/system/console/configMgr
   ```

1. OSGi 設定の編集 `com.day.crx.security.token.impl.impl.TokenAuthenticationHandler`

   ![同じサイトの cookie の OSGi プロパティ](assets/dev-cross-origin-osgi.png)

1. プロパティを変更します。 **login-token cookie の SameSite 属性** から `None`.

1. 変更を保存します。

ユニバーサルエディターを再読み込みすると、AEMに正常にログインし、ターゲットページが読み込まれます。

>[!TIP]
>
>* ドキュメントを見る [AEMでのユニバーサルエディターの概要](/help/implementing/universal-editor/getting-started.md#samesite-cookies) を参照してください。
>* ドキュメントを見る [Adobe Experience Manager as a Cloud Service用の OSGi の設定](/help/implementing/deploying/configuring-osgi.md) を参照してください。

## リモートフレームに接続するユニバーサルエディタ {#ue-connect-remote-frame}

ユニバーサルエディターにページが読み込まれ、AEMにサインインすると、ユニバーサルエディターはリモートフレームへの接続を試みます。 これは、リモートフレームに読み込む必要がある JavaScript ライブラリを介しておこなわれます。 JavaScript ライブラリが存在しない場合、最終的にページはコンソールでタイムアウトエラーを作成します。

![タイムアウトエラー](assets/dev-timeout.png)

必要な JavaScript ライブラリを WKND アプリのページコンポーネントに追加する必要があります。

1. CRXDE Lite を開きます。

   ```text
   https://localhost:8443/crx/de
   ```

1. の下 `/apps/wknd/components/page`、ファイルを編集 `customheaderlibs.html`.

   ![customheaderlibs.html ファイルの編集](assets/dev-customheaderlibs.png)

1. ファイルの最後に JavaScript ライブラリを追加します。

   ```html
   <script src="https://universal-editor-service.experiencecloud.live/corslib/LATEST"></script>
   ```

1. クリック **すべて保存** その後、ユニバーサルエディタを再読み込みします。

これで、ページが適切な JavaScript ライブラリと共に読み込まれて、ユニバーサルエディターがページに接続できるようになり、タイムアウトエラーがコンソールに表示されなくなりました。

>[!TIP]
>
>* ライブラリは、ヘッダーまたはフッターに読み込むことができます。
>* The `universal-editor-embedded.js` ライブラリ [は NPM で使用できます。](https://www.npmjs.com/package/@adobe/universal-editor-cors) 必要に応じて自分でホストしたり、アプリケーションに直接配置したりできます。

## 変更を保持する接続の定義 {#connection}

WKND ページがユニバーサルエディターに正常に読み込まれ、JavaScript ライブラリが読み込まれてエディターがアプリに接続されるようになりました。

ただし、ユニバーサルエディターでページを操作できないことに気付いた可能性があります。 ユニバーサルエディターは、実際にページを編集することはできません。 ユニバーサルエディターでコンテンツを編集するには、コンテンツの書き込み先を知るために接続を定義する必要があります。 ローカル開発の場合は、ローカルのAEM開発インスタンス ( ) に書き戻す必要があります。 `https://localhost:8443`.

1. CRXDE Lite を開きます。

   ```text
   https://localhost:8443/crx/de
   ```

1. の下 `/apps/wknd/components/page`、ファイルを編集 `customheaderlibs.html`.

   ![customheaderlibs.html ファイルの編集](assets/dev-instrument-app.png)

1. ローカルのAEMインスタンスに接続するために必要なメタデータをファイルの末尾に追加します。

   ```html
   <meta name="urn:adobe:aue:system:aem" content="aem:https://localhost:8443">
   ```

   * ライブラリの最新バージョンを常にお勧めします。 以前のバージョンが必要な場合は、ドキュメントを参照してください。 [AEMのユニバーサルエディターの概要。](/help/implementing/universal-editor/getting-started.md#alternative)

1. ローカルユニバーサルエディターサービスへの接続に必要なメタデータをファイルの末尾に追加します。

   ```html
   <meta name="urn:adobe:aue:config:service" content="https://localhost:8000">
   ```

1. クリック **すべて保存** その後、ユニバーサルエディタを再読み込みします。

ユニバーサルエディターは、ローカルのAEM開発インスタンスからコンテンツを正常に読み込むだけでなく、ローカルのユニバーサルエディターサービスを使用して行った変更を保持する場所も把握できるようになりました。 これは、ユニバーサルエディターで編集可能なアプリを実装する最初の手順です。

>[!TIP]
>
>* ドキュメントを見る [AEMでのユニバーサルエディターの概要](/help/implementing/universal-editor/getting-started.md#connection) を参照してください。
>* ドキュメントを見る [ユニバーサルエディターのアーキテクチャ](/help/implementing/universal-editor/architecture.md#service) を参照してください。
>* ドキュメントを見る [ユニバーサルエディターを使用したローカルAEM開発](/help/implementing/universal-editor/local-dev.md) を参照してください。

## 実装コンポーネント {#instrumenting-components}

しかし、ユニバーサルエディタでは、まだ少しで済むことに気付くかもしれません。 ユニバーサルエディターで WKND ページの上部にあるティーザーをクリックしようとした場合、実際には選択できません（またはページ上のその他の要素）。

ユニバーサルエディターで編集できるようにするには、コンポーネントも実装する必要があります。 そのためには、ティーザーコンポーネントを編集する必要があります。 そのため、コアコンポーネントはの配下にあるので、コアコンポーネントをオーバーレイする必要があります `/libs`：不変。

1. CRXDE Lite を開きます。

   ```text
   https://localhost:8443/crx/de
   ```

1. ノードを選択します。 `/libs/core/wcm/components` をクリックします。 **ノードをオーバーレイ** をクリックします。

1. を使用 `/apps/` 次として選択： **オーバーレイの場所**&#x200B;をクリックし、 **OK**.

   ![ティーザーをオーバーレイ](assets/dev-overlay-teaser.png)

1. を選択します。 `teaser` の下のノード `/libs/core/wcm/components` をクリックします。 **コピー** 」と入力します。

1. オーバーレイされたノードを次の場所で選択します。 `/apps/core/wcm/components` をクリックします。 **貼り付け** 」と入力します。

1. ファイルをダブルクリックします。 `/apps/core/wcm/components/teaser/v2/teaser/teaser.html` をクリックして編集します。

   ![teaser.html ファイルの編集](assets/dev-edit-teaser.png)

1. 最初の `div` 約 26 行目で、コンポーネントの計装の詳細を追加します。

   ```text
   data-aue-resource="urn:aem:${resource.path}"
   data-aue-type="component"
   data-aue-label="Teaser"
   ```

1. クリック **すべて保存** をクリックし、ユニバーサルエディタを再読み込みします。

1. ユニバーサルエディターで、ページ上部のティーザーコンポーネントをクリックし、選択できることを確認します。

1. 次の項目をクリックした場合、 **コンテンツツリー** アイコンが表示されます。 選択したティーザーがハイライト表示されたティーザーになります。

   ![インストルメント化されたティーザーコンポーネントの選択](assets/dev-select-teaser.png)

>[!TIP]
>
>ドキュメントを見る [Adobe Experience Manager as a Cloud Serviceでの Sling Resource Merger の使用](/help/implementing/developing/introduction/sling-resource-merger.md) ノードのオーバーレイの詳細は、を参照してください。

## ティーザーのインストゥルメントサブコンポーネント {#subcomponents}

これで、ティーザーを選択できますが、編集はできません。 これは、ティーザーが画像やタイトルコンポーネントなど、様々なコンポーネントの複合であるためです。 これらのサブコンポーネントを編集するには、それらのサブコンポーネントを実装する必要があります。

1. CRXDE Lite を開きます。

   ```text
   https://localhost:8443/crx/de
   ```

1. ノードを選択します。 `/apps/core/wcm/components/teaser/v2/teaser/` をクリックし、 `title.html` ファイル。

   ![title.html ファイルの編集](assets/dev-edit-title.png)

1. の最後に次のプロパティを挿入します。 `h2` タグ（17 行目付近）に貼り付けます。

   ```text
   data-aue-prop="jcr:title"
   data-aue-type="text"
   data-aue-label="Title"
   ```

1. クリック **すべて保存** をクリックし、ユニバーサルエディタを再読み込みします。

1. ページ上部の同じティーザーコンポーネントのタイトルをクリックし、選択できることを確認します。 コンテンツツリーには、選択したティーザーコンポーネントの一部としてタイトルも表示されます。

   ![ティーザー内でタイトルを選択](assets/dev-select-title.png)

これで、ティーザーコンポーネントのタイトルを編集できます。

## これは何を意味するのでしょうか？ {#what-does-it-mean}

ティーザーのタイトルを編集できたので、ここでは、達成した操作と方法を確認します。

ティーザーコンポーネントは、実装することでユニバーサルエディターに識別されました。

* `data-aue-resource` 編集中のAEM内のリソースを識別します。
* `data-aue-type` は、項目を（コンテナとは異なり）ページコンポーネントとして扱うことを定義します。
* `data-aue-label` 選択したティーザーのわかりやすいラベルを UI に表示します。

また、ティーザーコンポーネント内にタイトルコンポーネントも実装されています。

* `data-aue-prop` は、書き込まれる JCR 属性です。
* `data-aue-type` は、属性の編集方法です。 この場合、テキストエディターはタイトル（リッチテキストエディターとは異なり）なので、これを使用します。

## 認証ヘッダーの定義 {#auth-header}

これで、ティーザーのタイトルをインラインで編集でき、変更がブラウザーに保持されます。

![ティーザーのタイトルを編集しました](assets/dev-edited-title.png)

ただし、ブラウザを再読み込みすると、前のタイトルが再読み込みされます。 これは、ユニバーサルエディターはAEMインスタンスへの接続方法を知っていますが、AEMインスタンスに対してまだ認証を行って、JCR に変更を書き戻すことができないためです。

ブラウザー開発者ツールの「ネットワーク」タブを表示し、 `update`を入力すると、タイトルを編集しようとしたときに 401 エラーが発生していることを確認できます。

![タイトルを編集しようとした際にエラーが発生しました](assets/dev-edit-error.png)

ユニバーサルエディターを使用して実稼動用AEMコンテンツを編集する場合、ユニバーサルエディターは、JCR への書き戻しを容易にするために、エディターにログオンする際に使用したのと同じ IMS トークンを使用します。

ローカルで開発している場合は、AEM ID プロバイダーを使用できません。IMS トークンはAdobeが所有するドメインにのみ渡されます。 認証ヘッダーを明示的に設定して、認証する方法を手動で指定する必要があります。

1. ユニバーサルエディターインターフェイスで、 **認証ヘッダー** アイコンをクリックします。

1. 必要な認証ヘッダーをコピーして、ローカルのAEMインスタンスに認証し、「 **保存**.

   ![認証ヘッダーの設定](assets/dev-authentication-headers.png)

1. ユニバーサルエディターをリロードし、ティーザーのタイトルを編集します。

ブラウザーコンソールで報告されるエラーはなくなり、変更内容はローカルのAEM開発インスタンスに保持されます。

ブラウザーの開発者ツールでトラフィックを調査し、 `update` イベントを編集すると、更新の詳細を確認できます。

![ティーザータイトルの編集に成功しました](assets/dev-edit-title-successfully.png)

```json
{
  "connections": [
    {
      "name": "aem",
      "protocol": "aem",
      "uri": "https://localhost:8443"
    }
  ],
  "target": {
    "resource": "urn:aem:/content/wknd/language-masters/en/jcr:content/root/container/carousel/item_1571954853062",
    "type": "text",
    "prop": "jcr:title"
  },
  "value": "Tiny Toon Adventures"
}
```

* `connections` は、ローカルのAEMインスタンスへの接続です。
* `target` は、JCR で更新される正確なノードおよびプロパティです
* `value` は、お客様がおこなった更新です。

JCR 内で変更が保持されているのを確認できます。

![JCR での更新](assets/dev-write-back-jcr.png)

>[!TIP]
>
>オンラインで使用できるツールは多数あり、テストおよび開発目的で必要な認証ヘッダーを生成できます。
>
>基本的な認証ヘッダーの例 `Basic YWRtaW46YWRtaW4=` は、次のユーザーとパスワードの組み合わせ用です： `admin:admin` は、ローカルAEM開発で一般的です。

## プロパティパネル用のアプリの実装 {#properties-rail}

これで、ユニバーサルエディターを使用して編集できる機能が実装されたアプリが作成されました。

編集は、現在、ティーザーのタイトルのインライン編集に限られています。 ただし、インプレース編集では不十分な場合があります。 ティーザーのタイトルなどのテキストは、キーボード入力を使用して編集できます。 ただし、より複雑な項目は、ブラウザーでのレンダリング方法とは別に、構造化データを表示して編集できる必要があります。 プロパティパネルはこの機能を備えています。

プロパティレールを使用して編集するようにアプリを更新するには、アプリのページコンポーネントのヘッダーファイルに戻ります。 ローカルのAEM開発インスタンスおよびローカルのユニバーサルエディターサービスへの接続を既に確立している場所です。 ここで、アプリ内で編集可能なコンポーネントとそのデータモデルを定義する必要があります。

1. CRXDE Lite を開きます。

   ```text
   https://localhost:8443/crx/de
   ```

1. の下 `/apps/wknd/components/page`、ファイルを編集 `customheaderlibs.html`.

   ![customheaderlibs.html ファイルの編集](assets/dev-instrument-properties-rail.png)

1. ファイルの最後に、コンポーネントを定義するために必要なスクリプトを追加します。

   ```html
   <script type="application/vnd.adobe.aue.component+json">
   {
     "groups": [
       {
         "title": "General Components",
         "id": "general",
         "components": [
           {
             "title": "Teaser",
             "id": "teaser",
             "plugins": {
               "aem": {
                 "page": {
                   "resourceType": "wknd/components/teaser"
                 }
               }
             }
           },
           {
             "title": "Title",
             "id": "title",
             "plugins": {
               "aem": {
                 "page": {
                   "resourceType": "wknd/components/title"
                 }
               }
             }
           }
         ]
       }
     ]
   }
   </script>
   ```

1. その下に、ファイルの最後に、モデルを定義するために必要なスクリプトを追加します。

   ```html
   <script type="application/vnd.adobe.aue.model+json">
   [
     {
       "id": "teaser",
       "fields": [
         {
           "component": "text-input",
           "name": "jcr:title",
           "label": "Title",
           "valueType": "string"
         },
         {
           "component": "text-area",
           "name": "jcr:description",
           "label": "Description",
           "valueType": "string"
         }
       ]
     },
     {
       "id": "title",
       "fields": [
         {
           "component": "select",
           "name": "type",
           "value": "h1",
           "label": "Type",
           "valueType": "string",
           "options": [
             { "name": "h1", "value": "h1" },
             { "name": "h2", "value": "h2" },
             { "name": "h3", "value": "h3" },
             { "name": "h4", "value": "h4" },
             { "name": "h5", "value": "h5" },
             { "name": "h6", "value": "h6" }
           ]
         }
       ]
     }
   ]
   </script>
   ```

1. クリック **すべて保存** 」と入力します。

## これは何を意味するのでしょうか？ {#what-does-it-mean-2}

プロパティパネルを使用して編集するには、コンポーネントをに割り当てる必要があります。 `groups`各定義は、コンポーネントを含むグループのリストとして開始されます。

* `title` はグループの名前です。
* `id` は、グループの一意の識別子です。この場合、ページレイアウトの高度なコンポーネントなどとは異なり、ページコンテンツを構成する一般的なコンポーネントです。

各グループには、 `components`.

* `title` は、コンポーネントの名前です。
* `id` は、コンポーネントの一意の識別子です。この場合はティーザーです。

次に、各コンポーネントには、コンポーネントをAEMにマッピングする方法を定義するプラグイン定義が含まれます。

* `aem` は、編集を処理するプラグインです。 これは、コンポーネントを処理するサービスと考えることができます。
* `page` は、どのようなコンポーネントかを定義します。この場合は標準ページコンポーネントです。
* `resourceType` は、実際のAEMコンポーネントへのマッピングです。

その後、各コンポーネントを `model` 個々の編集可能フィールドを定義します。

* `id` は、モデルの一意の識別子です。この識別子は、コンポーネントの ID と一致する必要があります。
* `fields` は、個々のフィールドの配列です。
* `component` は、テキストやテキスト領域などの入力の種類です。
* `name` は、フィールドのマッピング先の JCR 内のフィールド名です。
* `label` は、エディター UI に表示されるフィールドの説明です。
* `valueType` はデータのタイプです。

## プロパティレール用のコンポーネントの実装 {#properties-rail-component}

また、コンポーネントで使用するモデルをコンポーネントレベルで定義する必要があります。

1. CRXDE Lite を開きます。

   ```text
   https://localhost:8443/crx/de
   ```

1. ファイルをダブルクリックします。 `/apps/core/wcm/components/teaser/v2/teaser/teaser.html` をクリックして編集します。

   ![teaser.html ファイルの編集](assets/dev-edit-teaser.png)

1. 最初の `div` 約 32 行目で、前に追加したプロパティの後に、ティーザーコンポーネントが使用するモデルの計装の詳細を追加します。

   ```text
   data-aue-model="teaser"
   ```

1. クリック **すべて保存** をクリックし、ユニバーサルエディタを再読み込みします。

これで、コンポーネント用に実装されたプロパティパネルをテストする準備が整いました。

1. ユニバーサルエディターで、ティーザーのタイトルをクリックして、もう一度編集します。

1. プロパティレールをクリックして「プロパティ」タブを表示し、先ほど実装したフィールドを確認します。

   ![計測されたプロパティレール](assets/dev-properties-rail-instrumented.png)

ティーザーのタイトルを、以前と同じようにインラインで編集したり、プロパティレールで編集したりできるようになりました。 どちらの場合も、変更はローカルのAEM開発インスタンスに保持されます。

## プロパティパネルへの追加フィールドの追加 {#add-fields}

実装済みのコンポーネントのデータモデルの基本構造を使用して、同じモデルに従ってフィールドを追加できます。

例えば、コンポーネントのスタイルを調整するフィールドを追加できます。

1. CRXDE Lite を開きます。

   ```text
   https://localhost:8443/crx/de
   ```

1. の下 `/apps/wknd/components/page`、ファイルを編集 `customheaderlibs.html`.

   ![customheaderlibs.html ファイルの編集](assets/dev-instrument-styles.png)

1. モデル定義スクリプトで、 `fields` 「スタイル」フィールドの配列。 新しいフィールドを挿入する前に、最後のフィールドの後に必ずコンマを追加してください。

   ```json
   {
      "component": "select",
      "name": "cq:styleIds",
      "label": "Style",
      "valueType": "string",
        "multi": true,
      "options": [
        {"name": "hero", "value":"1555543212672"},
        {"name": "card", "value":"1605057868937"}
      ]
   }
   ```

1. クリック **すべて保存** をクリックし、ユニバーサルエディタを再読み込みします。

1. ティーザーのタイトルをクリックして、もう一度編集します。

1. プロパティレールをクリックし、コンポーネントのスタイルを調整する新しいフィールドがあることを確認します。

   ![スタイルフィールドを含む実装済みのプロパティレール](assets/dev-style-instrumented.png)

この方法で、コンポーネントの JCR の任意のフィールドをユニバーサルエディターに表示できます。

## 概要 {#summary}

これで完了です。独自のAEMアプリを実装して、ユニバーサルエディターを操作できるようになりました。

独自のアプリの実装を開始する際は、この例で実行した基本的な手順に注意してください。

1. [開発環境を設定します。](#prerequisites)
   * WKND がインストールされた HTTPS でローカルで実行するAEM
   * HTTPS 上でローカルに動作するユニバーサルエディターサービス
1. AEM OSGi 設定を更新し、そのコンテンツをリモートで読み込めるようにしました。
   * [&#39;org.apache.sling.engine.impl.SlingMainServlet&#39;](#sameorigin)
   * [&#39;com.day.crx.security.token.impl.impl.impl.TokenAuthenticationHandler&#39;](#samesite-cookies)
1. [次の項目を追加しました： ](#ue-connect-remote-frame)
1. [接続を定義して、 ](#connection)
   * ローカルのAEM開発インスタンスへの接続を定義しました。
   * また、ローカルのユニバーサルエディターサービスへの接続も定義しました。
1. [ティーザーコンポーネントが実装されている。](#instrumenting-components)
1. [ティーザーのサブコンポーネントを実装しました。](#subcomponents)
1. [ローカルのユニバーサルエディターサービスを使用して変更を保存できるように、カスタム認証ヘッダーを定義しました。](#auth-header)
1. [プロパティパネルを使用するアプリを実装しました。](#properties-rail)
1. [ティーザーコンポーネントを実装し、プロパティレールを使用しています。](#properties-rail-component)

次の同じ手順に従って、ユニバーサルエディターで使用する独自のアプリを実装できます。 JCR 内のプロパティは、ユニバーサルエディターに公開できます。

## その他のリソース {#additional-resources}

ユニバーサルエディタの機能の詳細と詳細については、次のドキュメントを参照してください。

* できるだけ早く導入したい場合は、 [AEMでのユニバーサルエディターの概要](/help/implementing/universal-editor/getting-started.md) 文書。
* ドキュメントを見る [AEMでのユニバーサルエディターの概要](/help/implementing/universal-editor/getting-started.md#sameorigin) 必要な OSGi 設定の詳細を参照してください。
* ドキュメントを見る [AEMでのユニバーサルエディターの概要](/help/implementing/universal-editor/getting-started.md#connection) を参照してください。
* ドキュメントを見る [ユニバーサルエディターのアーキテクチャ](/help/implementing/universal-editor/architecture.md#service) を参照してください。
* ドキュメントを見る [ユニバーサルエディターを使用したローカルAEM開発](/help/implementing/universal-editor/local-dev.md) を参照してください。
* ドキュメントを見る [Adobe Experience Manager as a Cloud Serviceでの Sling Resource Merger の使用](/help/implementing/developing/introduction/sling-resource-merger.md) ノードのオーバーレイの詳細は、を参照してください。
