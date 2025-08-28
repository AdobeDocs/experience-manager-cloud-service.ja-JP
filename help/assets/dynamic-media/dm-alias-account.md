---
title: Dynamic Media の会社エイリアスアカウントの設定
description: Dynamic Media で会社エイリアスアカウントを設定する方法を説明します。
contentOwner: Rick Brough
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User,Admin
mini-toc-levels: 4
exl-id: 886063d4-71dd-48c8-a342-884ad2c111ca
source-git-commit: bc422429d4a57bbbf89b7af2283b537a1f516ab5
workflow-type: ht
source-wordcount: '671'
ht-degree: 100%

---

# Dynamic Media の会社エイリアスアカウントの設定について {#about-dm-alias-acct}

<!-- hide: yes
hidefromtoc: yes 
-->

<!-- 
>[!NOTE]
>
>This feature to create a Dynamic Media company alias account is in the Prerelease Channel for January 2022. See [Prerelease Channel documentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=en#enable-prerelease) for information on how to enable the feature for your environment. The feature is generally available in the February 2022 release. 
-->

Dynamic Media の URL とビューアの埋め込みコードには、会社のアカウント名が含まれます。このアカウント名は、Dynamic Media のプロビジョニング時に作成されました。ビジネスが買収やブランド変更を受けた、あるいは単にもっと記憶に残る名前を使用したいというシナリオがあるかもしれません。このようなシナリオでは、すべての URL とビューアの埋め込みコード（標準搭載）で会社のアカウント名を手動で更新するのは簡単ではありません。さらに、既存の Dynamic Media リポジトリに影響を与えたり、ライブコンテンツに影響を与えたりする可能性があります。この問題を解決するには、Dynamic Media の会社エイリアスアカウントを設定します。

Dynamic Media の会社エイリアスアカウントを使用すると、ユーザーインターフェイスに組み込まれているすべての Dynamic Media の URL とビューアの埋め込みコード（標準搭載）が、ブランド変更など、ビジネスコンテキストに対する更新を反映します。また、Dynamic Media の URL とビューアの埋め込みコードは新しい会社のアカウント名を反映しているので、エイリアスアカウントは SEO（検索エンジン最適化）にも良い影響を与えます。

Dynamic Media の会社エイリアスアカウントを設定する際は、次の点に注意してください。

* *ライブ* デジタルプロパティの既存の Dynamic Media の URL またはビューアの埋め込みコードは、新しいエイリアス名を反映するように手動で更新する必要があります。ただし、元の Dynamic Media の会社名を持つ URL やビューアの埋め込みコードは、既存または新規のアセットで引き続き機能します。
* Dynamic Media の会社エイリアスアカウント機能は、Experience Manager Assets オーサリングモードと配信に制限されています。会社のエイリアス名は、Experience Manager Sites では機能しません。この変更では、WCM（web コンテンツ管理）コンポーネントは更新されません。これらのコンポーネントは、Dynamic Media アセットを取得する際に、Dynamic Media の元の会社名で引き続き機能します。
* **[!UICONTROL Dynamic Media 設定を編集]** ページで設定できる会社エイリアスアカウントは 1 つだけです。ただし、サポートケースを通じて会社のエイリアスアカウントをいくつでも作成し、必要なエイリアス名をDynamic Media の URL またはビューアの埋め込みコードに手動で反映させることができます。
* Dynamic Media の [キャッシュの無効化](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md) 機能（標準搭載）は、Cloud Services の Dynamic Media 設定ページで設定した会社アカウントと会社エイリアスアカウントの両方で URL を無効にします。
* **[!UICONTROL Dynamic Media 設定を編集]** ページで会社のエイリアスアカウントを設定する場合、キャッシュの無効化を成功させるには、 **[!UICONTROL 会社]** のアカウントと **[!UICONTROL 会社のエイリアス]** アカウントの *両方* の URL を同時に無効にする必要があります。

[Cloud Services での Dynamic Media 設定の作成](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services) も参照してください

## Dynamic Media の会社エイリアスアカウントの設定 {#configure-dm-alias-account}

Dynamic Media の会社エイリアスアカウントの設定は、まずサポートケースを送信して開始します。この手順は必須です。

1. [Admin Console を使用して、サポートケースを作成します。](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html)
1. サポートケースには、次の情報を記入してください。

   * 使用する Dynamic Media の会社エイリアス名。名前には、文字（大文字と小文字を混在させることができます）、数字、ハイフン、アンダースコア *のみ* を含める必要があります。
   * お住まいの地域。
   * Dynamic Media の代替の会社アカウント名を通じて Dynamic Media コンテンツの提供を行うために、以前に [ルールセット](/help/assets/dynamic-media/using-rulesets-to-transform-urls.md) を使用していたかどうか。

1. サポートが Dynamic Media エイリアスアカウントを作成したら、Experience Manager as a Cloud Service のオーサーインスタンスで、Experience Manager as a Cloud Service ロゴを選択してグローバルナビゲーションコンソールにアクセスします。
1. コンソールの左側にあるツールアイコンを選択したあと、**[!UICONTROL Cloud Services／Dynamic Media 設定]**&#x200B;に移動します。
1. Dynamic Media 設定ブラウザーページの左側のパネルで、「**[!UICONTROL グローバル]**」を選択します（「**[!UICONTROL グローバル]**」の左側にあるフォルダーアイコンを選択しないでください）。「**[!UICONTROL 編集]**」を選択します。

   ![Dynamic Media の「会社エイリアス」テキストフィールド](/help/assets/assets-dm/dm-company-alias.png)

1. **[!UICONTROL Dynamic Media 設定を編集]** ページの「**[!UICONTROL 会社エイリアス]**」テキストフィールドに、前にサポートケースで指定した Dynamic Media エイリアスアカウント名を入力します。
1. ページの右上にある「**[!UICONTROL 保存]**」を選択します。
これで、Dynamic Media の会社エイリアスアカウントが保存され、有効になります。既存および新規アセットのすべての URL およびビューアの埋め込みコードに、新しい会社エイリアス名が反映されます。