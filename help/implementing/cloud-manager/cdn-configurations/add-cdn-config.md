---
title: CDN 設定の追加
description: Edge Delivery サイトまたはCloud Manager環境用の CDN 設定を追加する方法について説明します。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 672513d7-ee0a-4f6e-9ef0-7a41fabbaf9a
source-git-commit: dd696580758e7ab9a5427d47fda4275f9ad7997f
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 18%

---

# CDN 設定の追加 {#add-cdn}

SSL を使用してドメインを設定するには、CDN 設定の追加を完了する必要があります。

>
>
>アドビが管理する CDN の場合、DV 証明書を使用する際は、ACME 検証済みのサイトのみが許可されます。

**CDN 設定を追加するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. 「**CDN 設定**」をクリックします。

1. CDN 設定ページの右上隅付近にある「**追加**」をクリックします。

   ![CDN を設定ダイアログボックス ](/help/implementing/cloud-manager/assets/configure-cdn-dialog.png)

1. **CDN を設定** ダイアログボックスで、必要な情報を入力します。

   * **接触チャネル** ドロップダウンリストから、次のいずれかの操作を行います。
      * **サイト：** Edge Delivery Servicesサイトを選択します。
      * **環境：** Cloud Service環境を選択します。
         * **層：** 選択した環境の **Publish** または **プレビュー** web 層を選択します。
   * CDN タイプを **Adobeが管理する CDN** または **その他の CDN プロバイダー** から選択します。
   * ドメインを選択します。
   * SSL 証明書を選択します。 CDN タイプとして **Adobe管理 CDN** を選択した場合にのみ必要です。

1. 「**保存**」をクリックします。
