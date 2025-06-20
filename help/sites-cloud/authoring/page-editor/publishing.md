---
title: ページエディターを使用したコンテンツの公開
description: ページエディターによるコンテンツの公開方法を説明します。
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 5871e04d3bd78bdd8df55d42e7619c98ea3f38ca
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 82%

---


# サイトエディターを使用したコンテンツの公開 {#publishing}

ページエディターによるコンテンツの公開方法を説明します。

## ページエディターからの公開 {#publishing-from-the-page-editor}

[ページエディター](/help/sites-cloud/authoring/page-editor/introduction.md)でページを編集している場合、エディターから直接ページを公開できます。

1. **ページ情報**&#x200B;アイコンを選択してメニューを開き、「**ページを公開**」オプションを選択します。

   ![ページオプションを使用したページの公開](/help/sites-cloud/authoring/assets/publishing-page-options.png)

1. 公開が必要な参照がページに含まれているかどうかに応じて、次の操作を行います。

   * 公開する参照がない場合、ページが直接公開されます。
   * 公開が必要な参照がページに含まれている場合は、それらのリストが&#x200B;**公開**&#x200B;ウィザードに表示され、ウィザードで次のいずれかを実行できます。
      * ページと一緒に公開するアセットやタグなどを指定し、「**公開**」を使用してプロセスを完了します。
      * 「**キャンセル**」を使用してアクションを中止します。

   ![ページでの参照の公開](/help/sites-cloud/authoring/assets/publishing-references.png)

1. 「**公開**」を選択して、パブリッシュ環境にページをレプリケートします。ページエディターに、公開アクションを確認する情報バナーが表示されます。

   ![公開ステータス情報バナー](/help/sites-cloud/authoring/assets/publishing-info.png)

   コンソールで同じページを表示すると、更新された公開ステータスが表示されます。

   ![サイトコンソールの列表示でのページ公開ステータス](/help/sites-cloud/authoring/assets/publishing-status-console-column.png)

>[!NOTE]
>
>ページエディターからの公開は、浅い公開です。つまり、選択したページ（1 ページまたは複数ページ）だけが公開され、子ページ（1 ページまたは複数ページ）は公開されません。

>[!NOTE]
>
>エディターで[エイリアス](/help/sites-cloud/authoring/sites-console/page-properties.md#advanced)を使用してアクセスしたページは公開できません。エディターの「公開」オプションは、実際のパスからアクセスするページでのみ使用できます。

## ページエディターから非公開にする {#unpublishing}

ページエディターを使用してページを編集する際に、そのページを非公開にする場合、**ページを公開** する際と同じように **ページ情報** メニューで [ ページを非公開 ](#publishing-from-the-editor) を選択します。

>[!NOTE]
>
>エディターで[エイリアス](/help/sites-cloud/authoring/sites-console/page-properties.md#advanced)を使用してアクセスしたページは、非公開にできません。エディターの「公開」オプションは、実際のパスからアクセスするページでのみ使用できます。

## Sites コンソールからの公開と非公開 {#publishing-sites-console}

また、[Sites コンソールから](/help/sites-cloud/authoring/sites-console/publishing-pages.md)公開することもできます。これは、複数のコンテンツページを公開する場合や、公開または非公開をスケジュールする場合に便利です。
