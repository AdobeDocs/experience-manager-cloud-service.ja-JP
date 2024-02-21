---
title: EDS Formsの「ありがとうございます」ページの設定
description: EDS Formsの「ありがとうございます」ページの設定
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 0604838311bb9ab195789fad755b0910e09519fd
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 5%

---


# フォームブロックのリダイレクトの設定

デフォルトの「thankyou」ページではなく、Web サイト上の別のページにリダイレクトするようにフォームブロックを設定することもできます。 別のページをリダイレクト先として設定するには

1. `[EDS Project]/blocks/form/form.js` ファイルを編集用に開きます。

   ![「ありがとうございます」ノードのコード](/help/edge/assets/change-thankyou-node.png)

1. 次を変更： `thankyou` ノードを次の行からノードに任意に追加します。

   ```JavaScript
   window.location.href = form.dataset?.redirect || 'thankyou';
   ```

   例：

   ```JavaScript
   window.location.href = form.dataset?.redirect || 'home';
   ```

   >[!NOTE]
   >
   > Microsoft SharePointまたはGoogleシートの Edge Delivery Service プロジェクトフォルダーに、同じ名前のドキュメントページがまだ作成されていない場合は、作成してください。


1. 更新された「form.js」フォルダーとその基になるファイルを、GitHub の Edge 配信サービスプロジェクトにチェックインします。 この更新により、フォームは更新されたノードに指定どおりにリダイレクトされるようになります。
