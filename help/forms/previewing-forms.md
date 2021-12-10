---
title: フォームのプレビュー
seo-title: Previewing a form
description: 発行またはアクティベートする前にフォームをプレビューして、期待通りになっていることを確認します。プレビューのオプションは、サポートされているフォームタイプにより異なる場合があります。
seo-description: You can preview your forms before publishing or activating to ensure it meets the expectations. Preview options may vary across the supported form types.
uuid: 9ec359ea-f518-441c-9c3d-e3c1ea07a532
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 377d804d-4a75-4c93-8125-d2660cf56418
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 100%

---


# フォームのプレビュー {#previewing-a-form}

## 概要 {#overview}

[!DNL AEM Forms] では、リポジトリー内にあるフォームやドキュメントをプレビューできます。プレビューを使用すると、フォームがエンドユーザーにリリースされる際にどのように見え、作動するのかを明確に理解できます。

フォームをプレビューすると、フォームはインタラクティブインターフェイスでレンダリングされ、ユーザーはフォームにデータを入力できます。ドキュメントをプレビューすると、ドキュメントは非インタラクティブモードでレンダリングされ、ユーザーはドキュメントのみを見ることができます。フォームの場合、カスタムプレビューの追加オプションが使用できます。このオプションを使用すると、XML ファイルのデータを使用してフォームをプレビューできます。プレビューしているフォームのフィールドの一部またはすべてにデータが入力されます。

次の表に、サポートされているフォームのタイプごとに使用できるプレビューオプションを示します。

<table>
 <tbody>
  <tr>
   <td><strong>アセットタイプ</strong><br /> </td>
   <td><strong>使用できるプレビューオプション</strong><br /> </td>
  </tr>
  <tr>
   <td>ドキュメント</td>
   <td>PDF プレビュー</td>
  </tr>
  <tr>
   <td>PDF フォーム</td>
   <td>PDF プレビューとデータを使用したプレビュー<br /> </td>
  </tr>
  <tr>
   <td>アダプティブフォーム</td>
   <td>HTML プレビューとデータを使用した HTML プレビュー</td>
  </tr>
  <tr>
   <td>フォームテンプレート</td>
   <td>PDF プレビュー、データを使用した PDF プレビュー、HTML プレビュー、データを使用した HTML プレビュー<br /> </td>
  </tr>
 </tbody>
</table>

## フォームのプレビュー {#previewing-a-form-1}

1. プレビューするアセットを選択し、アクションツールバーのプレビュー ![aem6forms_preview](assets/aem6forms_preview.png) をクリックします。

   >[!NOTE]
   >
   >アセットを選択するには、デフォルトのカードビューをリストビューに切り替えます。![aem6forms_viewlist](assets/aem6forms_viewlist.png) または ![aem6forms_viewcard](assets/aem6forms_viewcard.png) をクリックして、表示を切り替えます。

1. プレビューをクリックすると、選択されているアセットタイプで使用できるプレビューオプションが表示されます。必要なオプションをクリックすると、選択されているアセットが新しいタブにレンダリングされます。

   以下のオプションがあります。

   * HTML としてプレビュー
   * データを使用したプレビュー
   * PDF としてプレビュー（フォームテンプレートから選択可能）

## データを使用したプレビュー {#preview-with-data}

「**データを使用したプレビュー**」を選択すると、実際のデータが入力された状態でフォームの様子を見ることができます。データを使用したプレビューオプションでは、サンプルユーザーデータを含めた XML をアップロードできます。サンプルユーザーデータを使用して、選択したフォーマットでプレビューフォームに自動入力します。

1. アセットを選択し、プレビュー ![aem6forms_preview](assets/aem6forms_preview.png) をクリックし、「**データを使用してプレビュー**」を選択します。
1. フォームのプレビューダイアログで、FormData を XML ファイルとして指定します。プレビューをクリックして、XML からのマージされたデータでフォームをレンダリングします。

