---
title: Edge Delivery Services による DAM アセットを使用したページの公開
description: ページの DAM アセットを Edge Delivery Services にシームレスに公開するために必要な設定について説明します。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 160f0474-a72d-4183-a2b2-2f8ba177605d
index: false
hide: true
hidefromtoc: true
source-git-commit: 17c14a78c2cfa262e25c6196fa73c6c4b17e200a
workflow-type: ht
source-wordcount: '433'
ht-degree: 100%

---

# Edge Delivery Services による DAM アセットを使用したページの公開 {#dam-assets}

ページの DAM アセットを Edge Delivery Services にシームレスに公開するために必要な設定について説明します。

## ユニバーサルエディター、DAM アセットおよび Edge Delivery {#overview}

ユニバーサルエディターのコンテンツを編集する場合、DAM からアセットを選択できます。コンテンツを Edge Delivery Services に公開すると、関連する DAM コンテンツも公開されます。

この動作をシームレスに行うには、AEM と Edge Delivery Services が、公開に必要な DAM への適切なアクセス権を持っている必要があります。これには次が含まれます。

* [アセットフォルダーをアクセス可能にする](#accessible)。
* [必要に応じて、アセットフォルダーに適切な設定が割り当てられていることを確認する](#configuration)。

## アセットフォルダーへのアクセスの確保 {#accessible}

AEM から Edge Delivery Services にページを公開する場合、[テクニカルアカウント](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)が使用されます。このアカウントの名前は `<hash>@techacct.adobe.com` という形式です。このアカウントは、ユニバーサルエディターで作成されたページを最初に公開するたびに、Cloud Manager によって AEM で自動的に作成されます。

![テクニカルアカウント](/help/edge/wysiwyg-authoring/assets/dam-assets/technical-account.png)

このテクニカルアカウントは、コンテンツを公開するためにすべての DAM フォルダーへのアクセス権を持っている必要があります。次のいずれかを実行できます。

* プライベート DAM フォルダーを使用しない。
* テクニカルアカウントのユーザーに DAM フォルダーへのアクセス権を付与する。

## アセットフォルダーに適切な設定が割り当てられていることを確認する {#configuration}

通常、ページとアセットを Edge Delivery Services に公開する場合は、テクニカルアカウントが DAM のアセットにアクセスできるようにすれば十分です。

ただし、次の 2 通りの場合では、追加の設定が必要です。

* PDF やビデオなどの画像以外のアセットを含むページを Edge Delivery Services に公開する場合。
* ページから独立して画像アセットを Edge Delivery Services に公開する場合。

これらの両方のユースケースをサポートするには、[設定](/help/implementing/developing/introduction/configurations.md)を DAM フォルダーに割り当てる必要があります。

1. AEM オーサリング環境にログインします。
1. **Sites** で、アセットを公開するサイト、またはアセットを関連付けるサイトを選択します。
1. ツールバーの「**プロパティ**」をタップまたはクリックします。
1. プロパティウィンドウの「**詳細**」タブで、「**クラウド設定**」フィールドの設定をメモします。
   * この設定は、サイトを `/conf/<site-name>` の形式で作成すると自動的に作成されます。
1. プロパティウィンドウで「**キャンセル**」をタップまたはクリックし、**アセット**／**ファイル**&#x200B;に移動して、DAM フォルダーを選択します。
1. ツールバーの「**プロパティ**」をタップまたはクリックします。
1. プロパティウィンドウの「**クラウドサービス**」タブにある「**クラウド設定**」フィールドで、メモした内容と同じ設定を選択します。
1. 「**保存して閉じる**」をタップまたはクリックします。
