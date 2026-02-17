---
title: Dynamic Media のセットアップ
description: Dynamic Media をセットアップするには、Dynamic Media を設定して、画像やビューアのプリセットを管理する必要があります。
mini-toc-levels: 3
contentOwner: Rick Brough
feature: Configuration,Viewer Presets,Image Presets,Dynamic Media
role: Admin,User
exl-id: 83b70b17-7ee3-41cb-be90-c92ca161660e
source-git-commit: bd43f86c9d3ad017a5e963800938e3ead98b7441
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 60%

---

# Dynamic Media のセットアップ {#setting-up-dynamic-media}

{{work-with-dynamic-media}}

[Dynamic Media &#x200B;](https://business.adobe.com/jp/products/experience-manager/assets/dynamic-media.html)では、マーチャンダイジングおよびマーケティング用のリッチなビジュアルアセットをオンデマンドで配信し、アセットを管理できます。これらのアセットは、Web、モバイルおよびソーシャルサイトでの利用に合わせて自動的に拡大縮小されます。Dynamic Media は、一連のプライマリソースアセットを使用し、パフォーマンスが最適化されスケーラビリティに優れたグローバルネットワーク経由で、複数のリッチコンテンツのバリエーションをリアルタイムで生成および配信します。

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


## Dynamic Media 証明書の更新に必要な DNS の一括更新 {#dns-update-dynamic-media-certificate-renewals}

ドメインで CAA （証明機関の承認） DNS レコードを使用する場合、Dynamic Media ホスト名で使用される TLS/SSL 証明書の継続的更新を許可するように DigiCert を承認する必要があります。

ドメインのルート（apex）に次の CAA レコードを追加します。

```
<yourdomain> CAA 0 issue "digicert.com"
```

これは 1 回限りの変更です。

DNS プロバイダーツールまたは [CAA ルックアップ ユーティリティ &#x200B;](https://caatest.co.uk/) を使用して、CAA レコードが存在するかどうかを確認できます。

CAA レコードが存在し、DigiCert が承認されていない場合、現在の証明書の有効期限が切れると証明書の更新が失敗し、画像およびビデオ配信のダウンタイムが発生する可能性があります。 ドメインに CAA レコードが存在しない場合は、アクションは必要ありません。
