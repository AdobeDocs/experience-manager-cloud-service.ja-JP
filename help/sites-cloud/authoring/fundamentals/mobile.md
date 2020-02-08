---
title: モバイルデバイス用のページのオーサリング
description: モバイル用にオーサリングするときは、複数のエミュレーターを切り替えて、エンドユーザー向けの表示を見ることができます。
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# モバイルデバイス用のページのオーサリング {#authoring-a-page-for-mobile-devices}

Adobe Experience Managerページはレスポンシブレイアウトに基づいています。 レスポンシブレイアウトは、コンテンツをターゲットデバイスに合わせて自動的に調整するので、特定のデバイス向けにコンテンツを作成する必要がありません。

モバイルページをオーサリングする場合、ページはモバイルデバイスをエミュレートする方法で表示されます。ページのオーサリング時に、いくつかのエミュレーターを切り替えて、エンドユーザーがページにアクセスしたときの表示を確認できます。

ページをレンダリングするデバイスの機能に従って、デバイスはカテゴリ機能、スマートおよびタッチにグループ分けされます。エンドユーザーがモバイルページにアクセスするときは、AEM はデバイスを検出して、そのデバイスグループに対応する表現を送信します。

>[!NOTE]
>
>既存の標準サイトに基づいたモバイルサイトを作成するには、標準サイトのライブコピーを作成します詳しくは、異なるチャネル用のライブコピーの作成を参照してください。
>
>AEM開発者は新しいデバイスグループを作成できます。 「デバイス・グループ・フィルタの作成」を参照してください。
<!--
>To create a mobile site based on an existing standard site, create a live copy of the standard site. (See [Creating a Live Copy for Different Channels](/help/sites-administering/msm-livecopy.md).)
>
>AEM developers can create new device groups. (See [Creating Device Group Filters](/help/sites-developing/groupfilters.md).)
-->

次の手順を使用して、モバイルページをオーサリングします。

1. From global navigation open the **Sites** console.
1. コンテンツページを編集します。
1. Switch to the desired emulator by clicking the **Emulator** icon at the top of the page.

   ![エミュレータアイコン](/help/sites-cloud/authoring/assets/emulator.png)

1. コンポーネントブラウザまたはアセットブラウザからページにコンポーネントをドラッグ&amp;ドロップします。
1. [選択したデバイスに基づいて](/help/sites-cloud/authoring/features/responsive-layout.md) 、ページとそのコンポーネントのレスポンシブレイアウトを変更します。

ページは次のようになります。

![モバイルの例](/help/sites-cloud/authoring/assets/mobile.png)

>[!NOTE]
>
>オーサーインスタンスのページがモバイルデバイスから要求されると、エミュレーターは無効になります。
