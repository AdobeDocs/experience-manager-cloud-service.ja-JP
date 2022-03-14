---
title: モバイルデバイス用のページのオーサリング
description: モバイル用にオーサリングするときは、複数のエミュレーターを切り替えて、エンドユーザー向けの表示を見ることができます。
exl-id: fabd4468-3304-402f-9522-342da3bbae94
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 100%

---

# モバイルデバイス用のページのオーサリング  {#authoring-a-page-for-mobile-devices}

Adobe Experience Manager ページはレスポンシブレイアウトに基づいています。[レスポンシブレイアウトは](/help/sites-cloud/authoring/features/responsive-layout.md)、コンテンツをターゲットデバイスに合わせて自動的に調整するので、特定のデバイス向けにコンテンツを作成しなくてもよくなります。

モバイルページをオーサリングする場合、ページはモバイルデバイスをエミュレートする方法で表示されます。ページのオーサリング時に、いくつかのエミュレーターを切り替えて、エンドユーザーがページにアクセスしたときの表示を確認できます。

ページをレンダリングするデバイスの機能に従って、デバイスはカテゴリ機能、スマートおよびタッチにグループ分けされます。エンドユーザーがモバイルページにアクセスするときは、AEM はデバイスを検出して、そのデバイスグループに対応する表現を送信します。

>[!NOTE]
>
>既存の標準サイトに基づいたモバイルサイトを作成するには、標準サイトのライブコピーを作成します。詳しくは、[ライブコピーの作成](/help/sites-cloud/administering/msm/creating-live-copies.md)を参照してください。
>
>AEM 開発者は、新しいデバイスグループを作成できます。「デバイスグループフィルターの作成」を参照してください。

<!--
>AEM developers can create new device groups. (See [Creating Device Group Filters](/help/sites-developing/groupfilters.md).)
-->

次の手順を使用して、モバイルページをオーサリングします。

1. グローバルナビゲーションから&#x200B;**サイト**&#x200B;コンソールを開きます。
1. コンテンツページを編集します。
1. ページ上部のエミュレーターアイコンをクリックして、目的のエミュレーターに切り替えます&#x200B;**。**

   ![エミュレーターアイコン](/help/sites-cloud/authoring/assets/emulator.png)

1. コンポーネントブラウザーまたはアセットブラウザーからページにコンポーネントをドラッグ＆ドロップします。
1. 選択したデバイスに応じて、ページとページコンポーネントの[レスポンシブレイアウトを変更](/help/sites-cloud/authoring/features/responsive-layout.md)します。

ページは次のようになります。

![モバイルの例](/help/sites-cloud/authoring/assets/mobile.png)

>[!NOTE]
>
>オーサーインスタンスのページがモバイルデバイスから要求されると、エミュレーターは無効になります。
