---
title: パブリッシュインスタンスでの関連付け UI の呼び出し
description: パブリッシュインスタンスでAEM Forms関連付け UI を統合して呼び出し、顧客対応のプロフェッショナルがパーソナライズされたインタラクティブ通信をリアルタイムで生成できるようにする方法について説明します。
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
hide: true
hidefromtoc: true
source-git-commit: 2f3badafddfdfe1dd21eb74be7189102aa0474bc
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 3%

---


# 関連付け UI を使用してパーソナライズされたコミュニケーションの生成

<span> インタラクティブ通信機能は、早期導入プログラムで利用できます。 勤務先のアドレスから `aem-forms-ea@adobe.com` にメールを送信して、アクセスをリクエストします。</span>

関連付け UI はパブリッシュインスタンスで直接呼び出すことができ、フィールド担当者やサービスエージェントなどの顧客向けのプロフェッショナルが、顧客インタラクション中にパーソナライズされたコミュニケーションをリアルタイムで生成できます。

次の表に、関連付け UI を使用して、パーソナライズされたメッセージを顧客に送信できる、実際の様々なシナリオを示します。

| 業種 | ユースケース |
|----------|----------|
| **金融サービス** | 顧客ミーティング中に、リアルタイムの融資確認レター、勘定明細書、およびリスク プロファイル概要を生成します |
| **保険** | サービスカウンターで即時保険証明カードと請求処理概要を作成 |
| **ヘルスケア** | 計算されたコピーの金額とスケジュールを使用して患者治療計画の要約を作成します |
| **政府** | その場で警察の検証報告書、市民サービスの領収書、ケースの更新要約を生成します |

## 前提条件

関連付け UI をアプリケーションに統合する前に、次のことを確認してください。

- インタラクティブ通信を作成および公開
- ポップアップサポートを有効にしたブラウザー
- 関連付け [&#x200B; ユーザーは、forms-associates グループの一部である必要があります &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/forms/administrator-help/setup-organize-users/creating-configuring-roles#assign-a-role-to-users-and-groups)
- 設定済みの認証 – [SAML 2.0](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/authentication/saml-2-0)

>[!NOTE]
>
> 関連付け UI の場合、[SAML 2.0 認証 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/authentication/saml-2-0) の記事で説明されている標準セットアップの後に、追加の SAML 設定が必要です。 詳しくは、[&#x200B; 関連 UI 用の追加の SAML 設定 &#x200B;](#additional-saml-configurations-for-associate-ui) の節を参照してください。

### 関連付け UI 用の追加の SAML 設定

関連付け UI に SAML 2.0 認証を設定する場合は、次の特定の設定を OSGi 設定ファイルに適用する必要があります。

#### SAML 認証ハンドラー

`com.adobe.granite.auth.saml.SamlAuthenticationHandler~saml.cfg.json` にファイル `ui.config/src/main/content/jcr_root/apps/<project-name>/osgiconfig/config.publish` を作成します。

```json
  {
    "path": ["/libs/fd/associate"],
    "serviceProviderEntityId": "https://publish-p{program-id}-e{env-id}.adobeaemcloud.com",
    "assertionConsumerServiceURL": "https://publish-p{program-id}-e{env-id}.adobeaemcloud.com/libs/fd/associate/saml_login",
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
| `path` | 関連付け UI では `/libs/fd/associate` に設定する必要があります |
| `defaultGroups` | `forms-associates` に設定すると、必要なグループにユーザーが自動的に割り当てられます |
| `defaultRedirectUrl` | 認証済みユーザーを関連付け UI にリダイレクト |
| `idpHttpRedirect` | SP が開始するフローでは `false` である必要があります |
| `idpCertAlias` | Trust Store の証明書エイリアスと完全に一致する必要があります（大文字と小文字を区別） |

#### Sling Authenticator

`org.apache.sling.engine.impl.auth.SlingAuthenticator~saml.cfg.json` のファイル `ui.config/src/main/content/jcr_root/apps/<project-name>/osgiconfig/config.publish` を更新します。

```json
{
  "sling.auth.requirements": ["+/libs/fd/associate/ui.html"],
  "sling.auth.anonymous": false
}
```

#### Dispatcher フィルター

まだ存在しない場合は、次のルールを `dispatcher/src/conf.dispatcher.d/filters/filters.any` ファイルに追加します。

```json
  # Allow Interactive Communications APIs and Associate UI
  /XXXX { /type "allow" /method '(GET|OPTIONS)' /url "/adobe/communications" }
  /XXXX { /type "allow" /method '(GET|POST|OPTIONS)' /url "/adobe/communications/*" }
  /XXXX { /type "allow" /method "GET" /url "/content/dam/fd:fonts/*" }
  /XXXX { /type "allow" /method '(GET|OPTIONS)' /url "/libs/fd/associate/*" }
```

>[!NOTE]
>
> `XXXX` を、既存の `filters.any` ファイルで使用されている適切な数値順に置き換えます。

## パブリッシュインスタンスでの関連付け UI の呼び出し

アプリケーションから関連付け UI を呼び出すには、パブリッシュインスタンスの URL を設定し、データペイロードを準備して、統合関数を使用して、新しいブラウザーウィンドウで関連付け UI を起動します。

### 手順 1：パブリッシュインスタンス URL の設定

関連付け UI には、AEM Forms Cloud Service パブリッシュインスタンス上の特定のエンドポイントを介してアクセスします。

```javascript
const AEM_URL = 'https://publish-p{program-id}-e{env-id}.adobeaemcloud.com/libs/fd/associate/ui.html';
```

`{program-id}` および `{env-id}` を実際の環境値に置き換えます。

### 手順 2：データペイロードの準備

次の形式を使用してデータペイロードを構築します。

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
| `prefill` | オプション | データの事前入力用のサービス設定が含まれます。 |
| `prefill.serviceName` | オプション | データの事前入力のために呼び出すフォームデータモデルサービスの名前 |
| `prefill.serviceParams` | オプション | 事前入力サービスに渡されるキーと値のペア |
| `options` | オプション | PDF レンダリングでサポートされるその他のプロパティ - locale、includeAttachments、embedFonts、makeAccessible |

### 手順 3：統合関数の実装

関連付け UI を起動し、メッセージ通信を処理するJavaScript関数を作成します。

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

### 手順 4：関数を呼び出す

適切なパラメーターを指定して関数を呼び出します。

```javascript
// Basic invocation with IC ID only
launchAssociateUI('12345', '', {}, {});

// With prefill service
launchAssociateUI('12345', 'FdmTestData', 
  { customerId: '101'}, {});

// With all parameters
launchAssociateUI('12345', 'FdmTestData', 
  { policyNumber: 'POL-123' }, 
  { locale: 'en', acrobatVersion: 'Acrobat_11' });
```

## サンプルのHTML ページを使用した統合のテスト

関連付け UI がフロントエンドにどのように表示されるかを確認し、統合をテストするために、簡単なHTMLの例を次に示します。 このサンプルページでは、パブリッシュインスタンス上で IC ID の入力、事前入力サービスパラメーターの設定、PDF オプションの設定、関連付け UI の起動を行うことができます。

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

### サンプルの仕組み

1. **IC ID フィールド**：インタラクティブ通信の識別子を入力します（必須）
2. **事前入力サービス**：データを事前入力するためのフォームデータモデルサービス名を指定します
3. **サービスパラメーター**：事前入力サービスに渡すパラメーターを含む JSON オブジェクトを入力します
4. **Options**:PDFの設定オプション（locale、includeAttachments、embedFonts、makeAccessible など）を入力します
5. **「起動」ボタン**：関連付け UI を新しいウィンドウで開き、初期化データを送信します

## データペイロードの例

### 最小ペイロード（IC のみ）

事前入力データが不要な場合に使用します。

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

### 事前入力データあり

これを使用して、IC に顧客データを動的に入力します。

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

### オプションを設定

追加のレンダリングオプションを指定する場合に使用します。

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
      locale: "en_US",
      includeAttachments: "true",
      webOptimized: "false",
      embedFonts: "false",
      makeAccessible: "false"
  }
}
```

## トラブルシューティング

### ポップアップのブロック

**問題**:UI の関連付けウィンドウが開きません。

**解決策**:
- ブラウザー設定でドメインのポップアップを有効にする
- `window.open()` をユーザーアクション（ボタンのクリックなど）から呼び出すようにします
- 異なるブラウザーでテストし、ブロック動作を特定します

### データが読み込まれない

**問題**：インタラクティブ通信が開くが、データが入力されない。

**解決策**:
- IC ID が正しく、IC がパブリッシュされていることを確認します
- ブラウザーコンソールで JavaScript エラーを確認します
- `postMessage` 構造が仕様に完全に一致することを確認します
- フォームデータモデルサービスが正しく設定されていることを確認します。

### 認証エラー

**問題**：関連付け UI が開くと、ユーザーに認証エラーが表示される。

**解決策**:
- パブリッシュインスタンスで SAML 2.0 認証を設定します
- ユーザーが **forms-associates** グループに属していることを確認
- セッションタイムアウト設定を確認

### CORS エラー

**問題**：コンソールでのクロスオリジンリソース共有エラー。

**解決策**:
- 開発の場合：`'*'` で `postMessage` をターゲットオリジンとして使用
- 実稼動環境の場合：アプリケーションの正確なオリジン URL を指定します
- パブリッシュインスタンスの CORS 設定でアプリケーションドメインが許可されていることを確認します

<!--## Best Practices

When implementing the Associate UI integration, follow these best practices:

1. **Validation**: Always validate the IC ID and JSON payload before sending
2. **Error Handling**: Implement proper error handling for `window.open()` failures
3. **User Experience**: Display a loading indicator while the Associate UI initializes
4. **Memory Management**: Remove event listeners after initialization to prevent memory leaks
5. **Testing**: Test the integration with popup blockers enabled to ensure graceful handling
6. **User Permissions**: Verify users have appropriate access to the forms-associates group-->

## 関連トピック

- [インタラクティブ通信エディターで UI を関連付け](/help/forms/interactive-communication/associate-ui-in-interactive-communication-editor.md)
- [クラウド上のインタラクティブ通信](/help/forms/early-access-ea-features.md#interactive-communications-on-cloud)
- [アーリーアクセス機能](/help/forms/early-access-ea-features.md)