---
title: アダプティブフォームのプレビュー方法は？
description: ユーザーは、発行またはアクティブ化する前にフォームをプレビューし、期待通りにフォームを表示できます。 プレビューオプションは、サポートされているフォームタイプによって異なる場合があります。
topic-tags: author
role: Admin, Developer, User
feature: Adaptive Forms
source-git-commit: 6511c4273ca3d394d98a61e8acb4d3cb03c243d5
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 38%

---


# フォームのプレビュー {#previewing-a-form}

## 概要 {#overview}

[!DNL AEM Forms] では、リポジトリー内にあるフォームやドキュメントをプレビューできます。プレビューを使用すると、フォームがエンドユーザーにリリースされたときの外観と動作を正確に把握できます。

フォームをプレビューすると、フォームはインタラクティブインターフェイスでレンダリングされ、ユーザーはフォームにデータを入力できます。 ドキュメントをプレビューすると、ドキュメントは非インタラクティブモードでレンダリングされ、ユーザーはドキュメントの表示のみ可能です。 フォームの場合は、カスタムプレビューの追加オプションを使用できます。 このオプションを使用すると、XML ファイルのデータを使用してフォームをプレビューできます。 プレビュー中のフォームの一部のフィールド（またはすべてのフィールド）にデータが入力されます。

次の表に、サポートされているフォームのタイプごとに使用できるプレビューオプションを示します。

<table>
 <tbody>
  <tr>
   <td><strong>アセットタイプ</strong><br /> </td>
   <td><strong>使用できるプレビューオプション</strong><br /> </td>
  </tr>
  <!--<tr>
   <td>Document</td>
   <td>PDF preview</td>
  </tr>-->
  <tr>
   <td>PDF フォーム</td>
   <td>PDF プレビューとデータを使用したプレビュー<br /> </td>
  </tr>
  <tr>
   <td>アダプティブフォーム</td>
   <td>HTML プレビューとデータを使用した HTML プレビュー</td>
  </tr>
  <!--<tr>
   <td>Form Template</td>
   <td>PDF preview, PDF preview with Data, HTML preview, HTML preview with Data<br /> </td>
  </tr>-->
 </tbody>
</table>

## フォームのプレビュー {#previewing-a-form-1}

1. プレビューするアセットを選択し、プレビューをクリックします。 ![aem6forms_preview](assets/aem6forms_preview.png) 」をクリックします。

   >[!NOTE]
   >
   >アセットを選択するには、デフォルトのカード表示をリスト表示に切り替えます。![aem6forms_viewlist](assets/aem6forms_viewlist.png) または ![aem6forms_viewcard](assets/aem6forms_viewcard.png) をクリックして、表示を切り替えます。

1. 「プレビュー」をクリックすると、選択したアセットタイプで使用できるプレビューオプションが表示されます。 目的のオプションをクリックして、選択したアセットを新しいタブでレンダリングします。

   以下のオプションがあります。

   * HTML としてプレビュー
   * データを使用したプレビュー
     <!--* Preview as PDF (available for form templates)-->

## データを使用してプレビュー {#preview-with-data}

「**データを使用したプレビュー**」を選択すると、実際のデータが入力された状態でフォームの様子を見ることができます。データを使用したプレビューオプションでは、サンプルユーザーデータを含めた XML をアップロードできます。サンプルのユーザーデータを使用して、選択した形式でプレビューフォームに入力します。

1. アセットを選択し、プレビュー ![aem6forms_preview](assets/aem6forms_preview.png) をクリックし、「**データを使用してプレビュー**」を選択します。
1. フォームをプレビューダイアログで、FormData を XML ファイルとして指定します。 XML からマージされたデータでフォームをレンダリングするには、「プレビュー」をクリックします。

