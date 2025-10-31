---
title: 様々なデータオプションを使用した、インタラクティブ通信エディターでのPDF プレビュー
description: 「様々なデータオプションを使用したインタラクティブ通信エディターでのPDFのプレビュー」オプションを使用すると、インタラクティブ通信を 3 つの異なる方法でプレビューできます。
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: 371838c77beafa8c67259a865b25325632bea0b0
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 14%

---


# インタラクティブ通信エディターでのPDF プレビュー

>[!NOTE]
>
> インタラクティブ通信機能は、早期導入プログラムで利用できます。 勤務先のアドレスから `aem-forms-ea@adobe.com` にメールを送信して、アクセスをリクエストします。

>[!IMPORTANT]
>
> **ドキュメントは変更される場合があります**：このプロンプトライブラリは現在製品に対してテスト中であり、更新および改訂される可能性があります。早期導入プログラム中に Forms Experience Builder が進化し続けると、プロンプト、例、ベストプラクティスが変わる可能性があります。

PDFのプレビュー機能を使用すると、インタラクティブ通信を 3 つの方法（データなし、ローカル JSON ベースのデータ、設定済みのデータモデルからのサンプルデータ）でプレビューできます。

## 主なメリット

- サンプルデータを使用したインタラクティブ通信のプレビューを表示して、通信と結合した際のライブデータの表示を視覚化します。

- バックエンドのセットアップを行わずにデータ駆動型のプレビューを生成するには、ローカルの JSON データファイルをアップロードします。

- 接続フォームデータモデル（FDM）を使用すると、設計時にサンプルデータを使用したリアルタイムデータ統合をシミュレートできます。

- データオプション（データなし、ローカルデータ、FDM）を簡単に切り替えて、レイアウト、構造、パーソナライゼーションを検証できます。

## 様々なデータオプションを使用した、インタラクティブ通信エディターでのPDF プレビュー

データ、ローカルデータ、設定済みデータモデルのサンプルデータを使用しないインタラクティブ通信のプレビューが表示されるので、柔軟なテストと検証が可能になります。

+++&#x200B;1. データのないプレビュー。

1.1. IC エディターでインタラクティブ通信を開きます。

1.2. データのない通信を表示するには、「PDF プレビュー」オプションを使用し、「**データなし**」オプションを選択します。

![IC Docu の検索 &#x200B;](/help/forms/interactive-communication/assets/nodata.png)

+++

+++&#x200B;2. ローカル JSON データを使用したプレビュー

2.1.構造化 JSON ファイルを準備する 参考までに、通信に使用される JSON スキーマ [&#x200B; （FDM）からサンプルデータをコピー &#x200B;](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/work-with-form-data-model) きます。

2.2. IC Editor で、**PDF Preview** > Using Local Data に移動します。

2.3. JSON ファイルを選択してアップロードし、提供されたデータでPDF プレビューをレンダリングする。

![IC Docu の検索 &#x200B;](/help/forms/interactive-communication/assets/localdata.png)

+++

+++&#x200B;3. データモデルを使用したプレビュー 

3.1.既に設定されている IC のフォームデータモデル（FDM）のサンプルデータを使用するには、「**データモデルの使用**」を選択します。

3.2. プレビューでは、モデルフィールドからデータが自動的に入力されます。 最初の使用時にサンプルデータが FDM に保存されていることを確認してください。保存されていない場合、プレビューがデータなしで表示されることがあります。

![IC Docu の検索 &#x200B;](/help/forms/interactive-communication/assets/datamodel.png)

+++

