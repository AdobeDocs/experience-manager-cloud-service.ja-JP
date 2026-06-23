---
title: Runtime Interactive Communications用のアソシエイト UIの統合
description: AEM Forms Associate UIをアプリケーションと統合して、お客様向けの担当者がパブリッシュインスタンスでパーソナライズされたインタラクティブなコミュニケーションをリアルタイムに生成できるようにする方法について説明します。
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
badgeSaas: label="AEM Forms" type="Positive" tooltip="AEM Formsに適用）。"
exl-id: f946ccea-86d0-4086-8208-9583b8206244
source-git-commit: 53ff71c82d35b9ec9b20b521ef469d3f0abd79df
workflow-type: tm+mt
source-wordcount: '1142'
ht-degree: 2%

---

# アプリケーションにアソシエイト UIを統合する


この記事では、アソシエイト UIをアプリケーションと統合し、フィールドアソシエイトやサービスエージェントなどの顧客対応の担当者が、パブリッシュインスタンスでパーソナライズされたインタラクティブ通信をリアルタイムで生成できるようにする方法について説明します。

## 前提条件

アソシエイト UIをアプリケーションと統合する前に、次のことを確認してください。

- インタラクティブ通信の作成と公開
- ポップアップのサポートが有効になっているブラウザー
- アソシエイト [ ユーザーはforms-associates グループ ](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/administrator-help/setup-organize-users/creating-configuring-roles#assign-a-role-to-users-and-groups)に属している必要があります
- AEM](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/authentication/authentication)でサポートされている任意の[認証メカニズム（SAML 2.0、OAuth、カスタム認証ハンドラーなど）を使用して設定された認証

>[!NOTE]
>
>- この記事では、[Microsoft Entra ID （Azure AD）をID プロバイダー](https://learn.microsoft.com/en-us/power-pages/security/authentication/openid-settings)として使用するSAML 2.0を使用した認証設定について説明します。
>- アソシエイト UIの場合、[SAML 2.0認証](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/authentication/saml-2-0)記事で説明されている標準設定を超える追加のSAML設定が必要です。 詳細については、「アソシエイト UI](#additional-saml-configurations-for-associate-ui)の[追加のSAML設定」の節を参照してください。

### アソシエイト UIの追加のSAML設定

アソシエート UIにSAML 2.0認証を設定する場合は、OSGi設定ファイルに次の特定の設定を適用する必要があります。

#### SAML認証ハンドラー

SAML認証ハンドラーは、異なるリソースツリーに対して複数のSAML設定を可能にするOSGi ファクトリ設定です。 これにより、マルチサイト AEMのデプロイメントが有効になり、既存のSAML設定にアソシエート UI リソースを追加できます。

ファイル `com.adobe.granite.auth.saml.SamlAuthenticationHandler~saml.cfg.json`を`ui.config/src/main/content/jcr_root/apps/<project-name>/osgiconfig/config.publish`に作成します：

```json
  {
    "path": ["/libs/fd/associate"],
    "serviceProviderEntityId": "https://publish-p{program-id}-e{env-id}.adobeaemcloud.com",
    "assertionConsumerServiceURL": "https://publish-p{program-id}-e{env-id}.adobeaemcloud.com/libs/fd/associate/saml_login"
    "idpUrl": "https://login.microsoftonline.com/{azure-tenant-id}/saml2",
    "idpCertAlias": "{your-certificate-alias}",
    "idpIdentifier": "https://sts.windows.net/{azure-tenant-id}/",
    "userIDAttribute": "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name",
    "createUser": true,
    "userIntermediatePath": "saml",
    "synchronizeAttributes": [
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname=profile/givenName",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname=profile/familyName",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress=profile/email"
      ],
      "addGroupMemberships": true,
      "defaultGroups": ["forms-associates"],
      "defaultRedirectUrl": "/libs/fd/associate/ui.html",
      "idpHttpRedirect": false,
      "service.ranking": 5002
  }
```

| プロパティ | 説明 |
|----------|-------------|
| `path` | アソシエイト UIでは`/libs/fd/associate`に設定する必要があります |
| `defaultGroups` | ユーザーを必要なグループに自動的に割り当てるには、`forms-associates`に設定します |
| `defaultRedirectUrl` | 認証済みユーザーを関連付けUIにリダイレクトします |
| `idpHttpRedirect` | SPが開始するフローには`false`である必要があります |
| `idpCertAlias` | Trust Storeの証明書エイリアスと正確に一致する必要があります（大文字と小文字を区別） |

#### Sling Authenticator

Sling Authenticatorは、公開時にアソシエート UI リソースにアクセスするための認証を強制します。

`ui.config/src/main/content/jcr_root/apps/<project-name>/osgiconfig/config.publish`のファイル `org.apache.sling.engine.impl.auth.SlingAuthenticator~saml.cfg.json`を更新します：

```json
{
  "sling.auth.requirements": ["+/libs/fd/associate/ui.html"],
  "sling.auth.anonymous": false
}
```

#### Dispatcher フィルター

次のルールを追加して、インタラクティブ通信APIとアソシエート UIがパブリッシュインスタンスで正しく機能するようにします。

まだ存在しない場合は、次のルールを`dispatcher/src/conf.dispatcher.d/filters/filters.any` ファイルに追加します。

```json
  # Allow Interactive Communications APIs and Associate UI
  /XXXX { /type "allow" /method '(GET|OPTIONS)' /url "/adobe/communications" }
  /XXXX { /type "allow" /method '(GET|POST|OPTIONS)' /url "/adobe/communications/*" }
  /XXXX { /type "allow" /method "GET" /url "/content/dam/fd:fonts/*" }
  /XXXX { /type "allow" /method '(GET|OPTIONS)' /url "/libs/fd/associate/*" }
```

>[!NOTE]
>
> `XXXX`を、既存の`filters.any` ファイルで使用されている適切な数列に置き換えます。

## パブリッシュインスタンスでのアソシエイト UIの呼び出し

この節では、独自のアプリケーションからアソシエート UIを起動する方法について説明します。 すぐに使用できるサンプルのHTMLページから始め、自社の環境に合わせて設定するなど、次の手順に従ってすばやく開始できます。

### 手順1：サンプル HTML ページから始める

Associate UIの統合機能の仕組みをすばやくテストして理解するには、次のサンプル HTML ページを使用します。 このコードをHTML ファイルにコピーし、ブラウザーで開きます。

>[!NOTE]
>
> このサンプル HTMLには、IC IDと事前入力サービスが必要です。 IC IDとサンプルの事前入力サービス「FdmTestData」を使用してテストできます。

HTML サンプルでは、インタラクティブ通信の詳細を入力し、ワンクリックでアソシエート UIを起動できるシンプルなフォームインターフェイスが用意されています。

```html
<!DOCTYPE html>
<html>
<head>
  <title>Associate UI Integration</title>
  <style>
    body {
      font-family: sans-serif;
      max-width: 600px;
      margin: 50px auto;
      padding: 20px;
    }
    .form-group {
      margin: 20px 0;
    }
    label {
      display: block;
      margin-bottom: 5px;
      font-weight: bold;
    }
    input, textarea {
      width: 100%;
      padding: 8px;
      border: 1px solid #ccc;
      border-radius: 4px;
      box-sizing: border-box;
    }
    textarea {
      height: 80px;
      font-family: monospace;
    }
    button {
      padding: 10px 20px;
      margin: 5px;
      cursor: pointer;
      border-radius: 4px;
    }
    .btn-primary {
      background: #007bff;
      color: white;
      border: none;
    }
    .btn-primary:hover {
      background: #0056b3;
    }
    .error {
      color: red;
      font-size: 12px;
      display: none;
    }
  </style>
</head>
<body>
  <h1>Launch Associate UI</h1>

  <form id="form">
    <div class="form-group">
      <label>IC ID *</label>
      <input type="text" id="icId" placeholder="Enter Interactive Communication ID" required>
    </div>

    <div class="form-group">
      <label>Prefill Service</label>
      <input type="text" id="serviceName" placeholder="e.g., CustomerDataService">
    </div>

    <div class="form-group">
      <label>Service Parameters (JSON)</label>
      <textarea id="serviceParams" placeholder='{"customerId": "12345"}'>{}</textarea>
      <span id="paramsError" class="error">Invalid JSON format</span>
    </div>

    <div class="form-group">
      <label>Options (JSON)</label>
      <textarea id="options" placeholder='{"mode": "edit", "locale": "en_US"}'>{}</textarea>
      <span id="optionsError" class="error">Invalid JSON format</span>
    </div>

    <button type="button" onclick="reset()">Reset</button>
    <button type="button" class="btn-primary" onclick="launch()">Launch Associate UI</button>
  </form>

  <script>
    // Replace with your AEM Publish instance URL
    const AEM_URL = 'https://publish-p{program-id}-e{env-id}.adobeaemcloud.com/libs/fd/associate/ui.html';

    function validateJSON(str, errorId) {
      const err = document.getElementById(errorId);
      try {
        const obj = JSON.parse(str || '{}');
        err.style.display = 'none';
        return obj;
      } catch (e) {
        err.style.display = 'block';
        return null;
      }
    }

    function launch() {
      const icId = document.getElementById('icId').value.trim();
      if (!icId) {
        alert('IC ID is required');
        return;
      }

      const params = validateJSON(document.getElementById('serviceParams').value, 'paramsError');
      const opts = validateJSON(document.getElementById('options').value, 'optionsError');

      if (!params || !opts) {
        alert('Please fix JSON errors before launching');
        return;
      }

      const data = {
        id: icId,
        prefill: {
          serviceName: document.getElementById('serviceName').value.trim(),
          serviceParams: params
        },
        options: opts
      };

      const win = window.open(AEM_URL, '_blank');
      if (!win) {
        alert('Pop-up blocked. Please enable pop-ups for this site.');
        return;
      }

      const handler = (e) => {
        if (e.data && e.data.type === 'READY' && e.data.source === 'APP') {
          win.postMessage({ type: 'INIT', source: 'PORTAL', data }, '*');
          window.removeEventListener('message', handler);
        }
      };

      window.addEventListener('message', handler);

      // Fallback timeout in case READY message is missed
      setTimeout(() => {
        if (win && !win.closed) {
          win.postMessage({ type: 'INIT', source: 'PORTAL', data }, '*');
          window.removeEventListener('message', handler);
        }
      }, 1000);
    }

    function reset() {
      document.getElementById('form').reset();
      document.getElementById('serviceParams').value = '{}';
      document.getElementById('options').value = '{}';
      document.getElementById('paramsError').style.display = 'none';
      document.getElementById('optionsError').style.display = 'none';
    }
  </script>
</body>
</html>
```

### 手順2：公開インスタンス URLの設定

関連付けUIを起動する前に、サンプルをAEM Forms Cloud Service パブリッシュインスタンスに向ける必要があります。

上記のHTML サンプルで、`<script>` セクションで次の行を見つけます。

```javascript
const AEM_URL = 'https://publish-p{program-id}-e{env-id}.adobeaemcloud.com/libs/fd/associate/ui.html';
```

プレースホルダーの値を実際の環境の詳細に置き換えます。
- `{program-id}`: AEM Cloud Service プログラム ID
- `{env-id}`：環境ID

例えば、プログラム IDが`12345`、環境IDが`67890`の場合、URLは次のようになります。

```javascript
const AEM_URL = 'https://publish-p12345`-e67890.adobeaemcloud.com/libs/fd/associate/ui.html';
```

>[!NOTE]
>
> セキュリティ上の理由から、インタラクティブ通信ID、事前入力サービス、サービスパラメーターなどのパラメーターはURLを通じて渡されません。 代わりに、これらのパラメーターはJavaScriptの`postMessage` APIを使用して安全に渡されます。

### 手順3:JavaScript統合機能について

サンプル HTMLでは、次のJavaScript関数を使用してアソシエイト UIを起動します。 この関数は、IC IDの検証、データペイロードの作成、新しいブラウザーウィンドウでの関連付けUIの開き、ブラウザーの`postMessage` APIを使用したデータの送信を行います。

```javascript
function launchAssociateUI(icId, prefillService, prefillParams, options) {
  if (!icId) {
    console.error('IC ID required');
    return;
  }

  const data = {
    id: icId,
    prefill: {
      serviceName: prefillService || '',
      serviceParams: prefillParams || {}
    },
    options: options || {}
  };

  const AEM_URL = 'https://your-aem.adobeaemcloud.com/libs/fd/associate/ui.html';
  const win = window.open(AEM_URL, '_blank');

  if (!win) {
    alert('Please enable pop-ups for this site');
    return;
  }

  const readyHandler = (event) => {
    if (event.data && event.data.type === 'READY' && event.data.source === 'APP') {
      win.postMessage({ type: 'INIT', source: 'PORTAL', data: data }, '*');
      window.removeEventListener('message', readyHandler);
    }
  };

  window.addEventListener('message', readyHandler);

  // Fallback timeout in case READY message is missed
  setTimeout(() => {
    if (win && !win.closed) {
      win.postMessage({ type: 'INIT', source: 'PORTAL', data: data }, '*');
      window.removeEventListener('message', readyHandler);
    }
  }, 1000);
}
```

この関数は、IC ID （必須）、事前入力サービス名、事前入力サービスパラメーター、および追加オプションの4つのパラメーターを受け入れます。 これらのパラメーターは、以下で説明するようにデータペイロードに構造化されます。

### 手順4：データペイロード構造の理解

**ペイロード形式：**

```javascript
const data = {
  id: "your-ic-id",              // Required: Interactive Communication ID
  prefill: {                      // Optional: Data to prefill the IC
    serviceName: "YourService",
    serviceParams: { key: "value" }
  },
  options: {}                     // Optional: Additional configuration options
};
```

**ペイロードコンポーネント：**

| コンポーネント | 必須 | 説明 |
|-----------|----------|-------------|
| `id` | はい | ロードするインタラクティブ通信（IC）の識別子 |
| `prefill` | オプション | データ事前入力のサービス設定が含まれます |
| `prefill.serviceName` | オプション | データの事前入力のために呼び出すフォームデータモデルサービスの名前 |
| `prefill.serviceParams` | オプション | 事前入力サービスに渡されるキーと値のペア |
| `options` | オプション | PDF レンダリングでサポートされる追加のプロパティ（ロケール、includeAttachments、embedFonts、makeAccessible） |

#### データペイロードの例

**最小ペイロード （IC IDのみ）**

これは、事前入力データが必要ない場合に使用します。

```json
{
  "id": "12345",
  "prefill": { 
    "serviceName": "", 
    "serviceParams": {} 
  },
  "options": {}
}
```

**事前入力データ**&#x200B;を使用

これを使用して、ICに顧客データを動的に入力します。

```json
{
  "id": "12345",
  "prefill": {
    "serviceName": "IC_FDM",
    "serviceParams": {
      "customerId": "101",
      "accountNumber": "ACC-98765"
    }
  },
  "options": {}
}
```

**PDF レンダリングオプション付き**

これを使用して、追加のレンダリングオプションを指定します。

```json
{
  "id": "12345",
  "prefill": {
    "serviceName": "IC_FDM",
    "serviceParams": {
      "customerId": "101",
      "accountNumber": "ACC-98765"
    }
  },
  "options": { 
      "locale": "en_US",
      "includeAttachments": "true",
      "webOptimized": "false",
      "embedFonts": "false",
      "makeAccessible": "false"
  }
}
```

### 手順5:IC IDを入力し、アソシエイト UIを起動する

これで、サンプル HTML ページを使用してアソシエイト UIを起動する準備が整いました。

1. **IC ID**&#x200B;を入力：**IC ID** フィールドに、公開したインタラクティブ通信の識別子を入力します。 これが唯一の必須フィールドです。

1. **事前入力サービスの設定**: ICに動的データを事前入力する場合は、**事前入力サービス** フィールドにフォームデータモデルサービス名を入力します。 例えば、サンプルデータには`FdmTestData`を使用します。

   ![HTML UIの例](/help/forms/assets/samplehtmlui.png)

1. **アソシエイト UIの起動**&#x200B;をクリック：「**アソシエイト UIの起動**」ボタンをクリックします。 新しいブラウザーウィンドウが開き、インタラクティブ通信が事前に読み込まれたアソシエイト UIが表示されます。

データを入力すると、次のように関連付けUIが表示されます。

![UIの関連付け](/help/forms/assets/associateui.png)

>[!NOTE]
>
> ウィンドウが開かない場合は、このサイトのポップアップがブラウザーで許可されているか確認してください。


<!--
  **Add Service Parameters**: In the **Service Parameters (JSON)** field, enter a JSON object with the parameters your prefill service requires. For example:

   ```json
   {"customerId": "101", "accountNumber": "ACC-98765"}
   ```

  **Set PDF Options** (optional): In the **Options (JSON)** field, configure rendering options such as locale, attachments, or accessibility settings.
  -->

## トラブルシューティング

### ポップアップをブロックしました

**問題**：関連付けUI ウィンドウが開きません。

**解決策**:
- ブラウザー設定でドメインのポップアップを有効にする
- `window.open()`がユーザーアクション （ボタンのクリックなど）から呼び出されていることを確認する
- 様々なブラウザーを使用してテストし、ブロックの動作を特定します

### データが読み込まれていません

**問題**: インタラクティブ通信が開きますが、データが入力されません。

**解決策**:
- IC IDが正しく、ICが公開されていることを確認します
- ブラウザーコンソールでJavaScript エラーを確認する
- `postMessage`構造が仕様と正確に一致していることを確認します
- フォームデータモデルサービスが正しく設定されていることを確認します

### 認証エラー

**問題**：アソシエート UIを開くと、認証エラーが表示されます。

**解決策**:
- パブリッシュインスタンスでのSAML 2.0認証の設定
- ユーザーが&#x200B;**forms-associates** グループに属していることを確認します
- セッションのタイムアウト設定を確認する

### CORS エラー

**問題**: コンソールでクロスオリジン リソース共有エラーが発生しました。

**解決策**:
- 開発用：`'*'`を`postMessage`のターゲットオリジンとして使用します
- 実稼動用：アプリケーションのオリジン URLを正確に指定します
- パブリッシュインスタンス CORS設定でアプリケーションドメインが許可されていることを確認します

<!--
## Best Practices

When implementing the Associate UI integration, follow these best practices:

1. **Validation**: Always validate the IC ID and JSON payload before sending
2. **Error Handling**: Implement proper error handling for `window.open()` failures
3. **User Experience**: Display a loading indicator while the Associate UI initializes
4. **Memory Management**: Remove event listeners after initialization to prevent memory leaks
5. **Testing**: Test the integration with popup blockers enabled to ensure graceful handling
6. **User Permissions**: Verify users have appropriate access to the forms-associates group
-->

## 関連トピック

- [インタラクティブ通信エディターでのUIの関連付け](/help/forms/interactive-communication/associate-ui-in-interactive-communication-editor.md)
- [インタラクティブ通信用のアソシエート UIの有効化と設定](/help/forms/interactive-communication/enable-configure-associate-ui.md)
- [アソシエイト UIの送信ワークフロー – IC PDF出力を生成](/help/forms/interactive-communication/submission-workflow-associate-ui-ic-pdf.md)

