---
title: Dynamic Media会社エイリアスアカウントの設定
description: Dynamic Mediaで会社エイリアスアカウントを設定する方法を説明します。
contentOwner: Rick Brough
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User,Admin
mini-toc-levels: 4
hide: true
hidefromtoc: true
exl-id: 886063d4-71dd-48c8-a342-884ad2c111ca
source-git-commit: 5e33aa9c18cb79d2e263224e92f866c3280b59bc
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 9%

---

# Dynamic Media会社エイリアスアカウントの設定について {#about-dm-alias-acct}

>[!NOTE]
>
>2022 年 1 月のプレリリースチャネルには、Dynamic Mediaの会社エイリアスアカウントを作成する機能があります。 この機能は 2022 年 2 月リリースで一般に利用できるようになります。

Dynamic Mediaの URL とビューアの埋め込みコードには、会社のアカウント名が含まれます。 このアカウント名は、Dynamic Mediaのプロビジョニング時に作成されました。 ビジネスが買収やリブランディングを受けた場合や、より覚えやすい名前を使用したい場合があります。 このような場合、すべての URL とビューアの埋め込みコード（標準搭載）で会社のアカウント名を手動で更新するのは簡単ではありません。 さらに、既存のDynamic Mediaリポジトリに影響を与えたり、ライブコンテンツに影響を与えたりする可能性があります。 この問題を解決するには、Dynamic Media会社エイリアスアカウントを設定します。

Dynamic Mediaの会社エイリアスアカウントを使用すると、ユーザーインターフェイスに組み込まれているすべてのDynamic Media URL とビューアの埋め込みコードが、ブランディングの変更など、ビジネスコンテキストに対する更新を反映します。 また、Dynamic Mediaの URL とビューアの埋め込みコードは新しい会社のアカウント名を反映しているので、エイリアスアカウントは SEO（検索エンジン最適化）にも良い影響を与えます。

Dynamic Mediaの会社エイリアスアカウントを設定する際は、次の点に注意してください。

* 次の場所で会社エイリアスアカウントを設定する場合： **[!UICONTROL Dynamic Media設定を編集]** ページでキャッシュの無効化を成功させるには、次の URL を無効にする必要があります： *両方* の **[!UICONTROL 会社]** アカウントおよび **[!UICONTROL 会社エイリアス]** 同時にアカウントを作成します。
* 既存のDynamic Media URL またはビューア埋め込みコード *live* デジタルプロパティは、新しいエイリアス名を反映するように手動で更新する必要があります。 ただし、元のDynamic Mediaの会社名を持つ URL やビューア埋め込みコードは、既存または新しいアセットで引き続き機能します。
* Dynamic Mediaの会社エイリアスアカウント機能は、Experience Manager Assetsオーサリングモードと配信に制限されています。 会社のエイリアス名はExperience Manager Sitesでは使用できません。 この変更では、WCM(Web Content Management) コンポーネントは更新されません。 これらのコンポーネントは、Dynamic Mediaアセットを取得する際に、元のDynamic Media会社名と引き続き連携します。
* で設定できる会社エイリアスアカウントは 1 つだけです。 **[!UICONTROL Dynamic Media設定を編集]** ページ。 ただし、サポートケースを通じて会社のエイリアスアカウントをいくつでも作成し、必要なエイリアス名をDynamic Media URL またはビューアの埋め込みコードに手動で反映させることができます。
* 標準搭載の [キャッシュの無効化](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md) Dynamic Mediaの機能は、Cloud ServicesのDynamic Media設定ページで設定された Company アカウントと Company Alias アカウントの両方を使用して URL を無効化します。

関連トピック [Cloud ServicesでのDynamic Media設定の作成](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services)

## Dynamic Media会社エイリアスアカウントの設定 {#configure-dm-alias-account}

Dynamic Mediaの会社エイリアスアカウントの設定は、まずサポートケースを送信して開始します。 この手順は必須です。

1. [Admin Console を使用して、サポートケースを作成します。](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html)
1. サポートケースには、次の情報を記入してください。

   * 使用するDynamic Mediaの会社名。 名前には次を含める必要があります *のみ* 文字（大文字と小文字を混在させることができます）、数字、ハイフン、アンダースコアを使用できます。
   * お住まいの地域。
   * いずれか [ルールセット](/help/assets/dynamic-media/using-rulesets-to-transform-urls.md) は、以前は、代替のDynamic Media会社アカウント名を通じてDynamic Mediaコンテンツの提供を実現するために使用されていました。

1. サポートがDynamic Media alias アカウントを作成したら、Experience Managerのas a Cloud Serviceのオーサーインスタンスで、Experience Managerのas a Cloud Serviceロゴを選択してグローバルナビゲーションコンソールにアクセスします。
1. コンソールの左側にあるツールアイコンを選択したあと、**[!UICONTROL Cloud Services／Dynamic Media 設定]**&#x200B;に移動します。
1. Dynamic Media 設定ブラウザーページの左側のパネルで、「**[!UICONTROL グローバル]**」を選択します（「**[!UICONTROL グローバル]**」の左側にあるフォルダーアイコンを選択しないでください）。「**[!UICONTROL 編集]**」を選択します。

   ![「Dynamic Media Company Alias 」テキストフィールド](/help/assets/assets-dm/dm-company-alias.png)

1. の **[!UICONTROL Dynamic Media設定を編集]** ページの **[!UICONTROL 会社エイリアス]** 「 」テキストフィールドに、前のサポートケースで指定したDynamic Media alias account name を入力します。
1. ページの右上で、「 **[!UICONTROL 保存]**.
これで、Dynamic Media企業エイリアスアカウントが保存され、有効になります。既存および新規アセットのすべての URL およびビューア埋め込みコードに、新しい会社エイリアス名が反映されるようになりました。