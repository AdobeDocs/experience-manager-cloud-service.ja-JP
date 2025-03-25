---
title: Dynamic Media のセットアップ
description: Dynamic Media をセットアップするには、Dynamic Media を設定して、画像やビューアのプリセットを管理する必要があります。
contentOwner: Rick Brough
feature: Configuration,Viewer Presets,Image Presets,Dynamic Media
role: Admin,User
exl-id: 83b70b17-7ee3-41cb-be90-c92ca161660e
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 100%

---

# Dynamic Media のセットアップ {#setting-up-dynamic-media}

{{work-with-dynamic-media}}

[Dynamic Media ](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html)では、マーチャンダイジングおよびマーケティング用のリッチなビジュアルアセットをオンデマンドで配信し、アセットを管理できます。これらのアセットは、Web、モバイルおよびソーシャルサイトでの利用に合わせて自動的に拡大縮小されます。Dynamic Media は、一連のプライマリソースアセットを使用し、パフォーマンスが最適化されスケーラビリティに優れたグローバルネットワーク経由で、複数のリッチコンテンツのバリエーションをリアルタイムで生成および配信します。

<!-- OBSOLETE UNTIL THE INTEGRATING SCENE7 TOPIC GETS A MAJOR UPDATE

>[!NOTE]
>
>This documentation describes Dynamic Media capabilites, which are integrated directly into [!DNL Experience Manager]. If you are using Dynamic Media Classic (previously called Scene7) integrated into [!DNL Experience Manager], see [Dynamic Media Classic integration documentation](/help/sites-cloud/administering/integrating-scene7.md).
>
>See [Dual Use Scenario](/help/sites-cloud/administering/integrating-scene7.md#dual-use-scenario) for times when you may want to use [!DNL Experience Manager] integrated with Dynamic Media Classic along with Dynamic Media.

-->

Dynamic Media の管理者には、次のトピックが参考になります。

* [Dynamic Media の設定](config-dm.md)
* [画像プリセットの管理](managing-image-presets.md)
* [ビューアプリセットの管理](managing-viewer-presets.md)
* [Dynamic Media のトラブルシューティング](troubleshoot-dm.md)

次のトピックも参照してください。

* [ビデオエンコーディングとビデオプロファイル](video-profiles.md)
* [イメージプロファイル](image-profiles.md)

>[!NOTE]
>
>**アップグレードする場合：**
>
>* Adobe [!DNL Experience Manager] を実行状態にした後にアップロードしたすべてのアセットで、Dynamic Media が自動的に有効になります（システム管理者によって明示的に無効にされた場合を除く）。アップグレードされた [!DNL Experience Manager] インスタンスで Dynamic Media を新たに使用する場合、Dynamic Media を使用できるようアセットを再処理する必要が生じる可能性があります。詳しくは、[フォルダー内のアセットの再処理](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets)を参照してください。
