---
title: Edge Delivery Services 向けに AEM Forms を公開します。
description: Edge Delivery Services Forms をすばやくシームレスに公開します。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: ba1c608d-36e9-4ca1-b87b-0d1094d978db
source-git-commit: 9ef4c5638c2275052ce69406f54dda3ea188b0ef
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 97%

---

# アダプティブフォームから Edge Delivery Services への公開

<span class="preview"> これは、アドビの <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=ja#new-features"> プレリリースチャネル </a> で利用できるプレリリース機能です。</span>


フォームが完成し、使用できる状態になったら、公開して、顧客がデータの収集と送信にアクセスできます。公開すると、フォームが Edge Delivery で使用できるようになり、ユーザーがシームレスに操作できます。このプロセスにより、顧客はフォームにリアルタイムで入力して送信できるので、効率的なデータ取得と効率化された処理が確保されます。

## 前提条件

* **Edge Delivery Services テンプレート**&#x200B;を使用して作成されたフォーム。EDS ベースのフォームの作成について詳しくは、[こちら](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)を参照してください。

## フォームの公開

次の手順に従って、**EDS ベースのアダプティブフォーム**&#x200B;を Edge Delivery に公開できます。

<!--1. Select the **Adaptive Form** that you want to publish and click the **Edit** ![edit icon](/help/forms/assets/edit.svg) icon.
   ![Select EDS-Based Form](/help/forms/assets/select-eds-based-form.png)-->

1. アダプティブフォームをエディターで開き、上部パネルの「**公開**」アイコンをクリックします。
   ![「公開」をクリック](/help/forms/assets/publish-icon-eds-form.png)

1. 「**公開**」をクリックすると、フォームのタイトルを含む公開アセットを示す画面またはポップアップが表示されます。この例では、**Wknd_Form** テンプレートが使用されています。
   ![「公開」をクリックした場合](/help/forms/assets/on-click-publish.png)

1. もう一度「**公開**」をクリックすると、フォームが公開されたことを示す確認ポップアップが表示されます。
   ![公開成功](/help/forms/assets/publish-success.png)

1. フォームの公開ステータスを確認するには、もう一度「**公開**」をクリックします。
   ![公開ステータス](/help/forms/assets/publish-status.png)

1. フォームを&#x200B;**非公開**&#x200B;にするには、エディターでフォームを開き、右上隅にある 3 つのドットのメニューをクリックして、「**非公開**」をクリックします。
   ![非公開](/help/forms/assets/unpublish--form.png)

## AEM パブリッシャーのリファラーフィルターを設定して、Edge Delivery でのフォーム送信を有効にする

フォームの安全な送信を確保するには、AEM パブリッシャーで&#x200B;**リファラーフィルター**&#x200B;を設定する必要があります。このフィルターにより、Edge Delivery からの承認されたリクエストのみが書き込み操作（POST、PUT、DELETE、COPY、MOVE）を実行できるようになり、不正な変更が防止されます。AEM パブリッシャーのリファラーフィルターを設定する手順は次のとおりです。

### Edge Delivery で AEM インスタンス URL を更新

フォームブロック内の **constant.js** ファイルで `submitBaseUrl` を変更して、AEM インスタンス URL を指定します。

**クラウド設定の場合：**

```js
export const submitBaseUrl = 'https://publish-p120-e12.adobeaemcloud.com';
```

**ローカル開発の場合：**

```js
export const submitBaseUrl = 'http://localhost:4503';
```

### CORS 設定を変更

**CORS 設定**&#x200B;を調整して、Edge Delivery ドメインからのフォーム送信リクエストを許可します。詳しくは、[CORS 設定ガイド](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/configurations/cors)を参照してください。

**サンプル CORS 設定：**

```apache
# Developer Localhost
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(http://localhost(:\d+)?$)#" CORSTrusted=true

# Franklin Stage
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.page$)#" CORSTrusted=true  

# Franklin Live
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.live$)#" CORSTrusted=true
```

ローカル開発について詳しくは、**開発 UI ホスト URL** から CORS を有効にする[ドキュメント ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/headless/deployment/referrer-filter)を参照してください。

### リファラーフィルターを設定

Cloud Manager を通じて AEM Cloud Service で&#x200B;**リファラーフィルター**&#x200B;を設定します。Cloud Manager を使用して AEM Cloud Service インスタンスでリファラーフィルターを設定する方法について詳しくは、[こちら](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing)を参照してください。

**リファラーフィルターの JSON 設定：**

```json
{
  "allow.empty": false,
  "allow.hosts": [],
  "allow.hosts.regexp": [
    "https://.*\\.hlx\\.page:443",
    "https://.*\\.hlx\\.live:443"
  ],
  "filter.methods": [
    "POST",
    "PUT",
    "DELETE",
    "COPY",
    "MOVE"
  ],
  "exclude.agents.regexp": [
    ""
  ]
}
```

この設定では、フィルタリングされる HTTP メソッド、許可されるリファラーおよびフィルターから除外されるユーザーエージェントを指定します。これらの設定を実装することで、**Edge Delivery 経由のフォーム送信**&#x200B;が保護され、承認されたソースのみに制限されます。

### 公開済みアダプティブフォームにアクセス

これで、次の URL 形式を使用して、**Edge Delivery** 経由でアダプティブフォームにアクセスできます。

```
https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>
```

例えば、**Wknd-Form** の URL は次のとおりです。

```
https://main--universaleditor--wkndforms.aem.live/content/forms/af/wknd-form
```


## 関連トピック

{{universal-editor-see-also}}

