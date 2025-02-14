---
title: Edge Delivery Services用のAEM Formsを公開します。
description: Edge Delivery Services フォームを迅速かつシームレスに公開します。
feature: Edge Delivery Services
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
exl-id: ba1c608d-36e9-4ca1-b87b-0d1094d978db
source-git-commit: d48048ab130805d2be40ac3f7ee60e4269337cb5
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 1%

---

# アダプティブフォームをEdge Delivery Servicesに公開する

フォームが完成し、使用できる状態になったら、公開することで、顧客がデータの収集や送信にアクセスできるようになります。 公開すると、フォームをEdge Deliveryで使用できるようになり、ユーザーはシームレスに操作できます。 このプロセスにより、お客様はフォームにリアルタイムで入力して送信でき、効率的なデータキャプチャと効率化された処理が可能になります。

## 前提条件

* **Edge Delivery Services（EDS）テンプレート** を使用して作成されたフォーム。 EDS ベースのフォームの作成について [ 詳細情報 ](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md) します。

## フォームを公開する

次の手順に従って、任意の **EDS ベースのアダプティブフォーム** をEdge Deliveryに公開できます。

<!--1. Select the **Adaptive Form** that you want to publish and click the **Edit** ![edit icon](/help/forms/assets/edit.svg) icon.
   ![Select EDS-Based Form](/help/forms/assets/select-eds-based-form.png)-->

1. アダプティブフォームをエディターで開き、上部パネルの **公開** アイコンをクリックします。
   ![ 「公開」をクリック ](/help/forms/assets/publish-icon-eds-form.png)

1. 「**公開**」をクリックすると、フォームのタイトルなど、公開アセットを示す画面またはポップアップが表示されます。 この例では、**Wknd_Form** テンプレートを使用します。
   ![ 「公開」をクリックします ](/help/forms/assets/on-click-publish.png)。

1. もう一度 **公開** をクリックすると、フォームが公開されたことを示す確認ポップアップが表示されます。
   ![ 公開成功 ](/help/forms/assets/publish-success.png)

1. フォームの公開ステータスを確認するには、もう一度 **公開** をクリックします。
   ![公開ステータス](/help/forms/assets/publish-status.png)

1. フォームを **非公開** するには、エディターでフォームを開き、右上隅の「。..」メニューをクリックして **非公開** をクリックします。
   ![ 非公開 ](/help/forms/assets/unpublish--form.png)

## Edge Delivery Publisher のリファラーフィルターを設定して、AEMでのフォーム送信を有効にします

フォームの安全な送信を確保するには、AEM Publisher で **リファラーフィルター** を設定する必要があります。 このフィルターを使用すると、Edge Deliveryから許可されたリクエストのみが書き込み操作（POST、PUT、DELETE、COPY、MOVE）を実行し、承認されていない変更を防ぐことができます。 AEM パブリッシャー用のリファラーフィルターを設定する手順は次のとおりです。

### Edge DeliveryでAEM インスタンス URL を更新します

フォームブロック内の **constant.js** ファイルの `submitBaseUrl` を変更して、AEM インスタンスの URL を指定します。

**クラウド設定用：**

```js
export const submitBaseUrl = 'https://publish-p120-e12.adobeaemcloud.com';
```
**ローカル開発の場合：**

```js
export const submitBaseUrl = 'http://localhost:4503';
```

### CORS 設定の変更

**CORS 設定** を調整して、Edge Delivery ドメインからのフォーム送信リクエストを許可します。 詳しくは、『 [CORS 設定ガイド ](https://experienceleague.adobe.com/en/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/configurations/cors) を参照してください。

**サンプル CORS 設定：**

```apache
# Developer Localhost
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(http://localhost(:\d+)?$)#" CORSTrusted=true

# Franklin Stage
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.page$)#" CORSTrusted=true  

# Franklin Live
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.live$)#" CORSTrusted=true
```
ローカル開発については、[ ドキュメント ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/headless/deployment/referrer-filter) を参照して、**開発 UI ホスト URL** から CORS を有効にします。

### リファラーフィルターの設定

Cloud Managerを使用して、AEM Cloud Service で **リファラーフィルター** を設定します。 Cloud Manager を使用して AEM Cloud Service インスタンスにリファラーフィルターを設定する方法については [ 詳細情報 ](https://experienceleague.adobe.com/en/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing) を参照してください。

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

この設定は、フィルタリングする HTTP メソッド、許可されるリファラーおよびフィルターから除外するユーザーエージェントを指定します。 これらの設定を実装することで、**Edge Deliveryを介したフォーム送信** が保護され、許可されたソースのみに制限されます。

### 公開済みアダプティブフォームへのアクセス

これで、アダプティブフォームに **0}Edge Delivery} から次の URL フォーマットでアクセスできるようになりました。**

```
https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>
```

例えば、**Wknd-Form** の URL は次のとおりです。

```
https://main--universaleditor--wkndforms.aem.live/content/forms/af/wknd-form
```


## 関連トピック

{{see-more-forms-eds}}
