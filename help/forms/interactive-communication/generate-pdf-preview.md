---
title: 異なるデータオプションを使用したインタラクティブ通信エディターでのPDF プレビュー
description: 異なるデータオプションを使用したインタラクティブ通信エディターでのPDF プレビューでは、インタラクティブ通信を3つの異なる方法でプレビューできます。
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
badgeSaas: label="AEM Forms" type="Positive" tooltip="AEM Formsに適用）。"
exl-id: 17b3fe2b-6a1d-4fe2-9a92-a55a50400824
source-git-commit: 53ff71c82d35b9ec9b20b521ef469d3f0abd79df
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 4%

---

# インタラクティブ通信エディターでのPDF プレビュー


PDFのプレビュー機能を使用すると、データなし、ローカル JSON ベースのデータ、または設定されたデータモデルのサンプルデータを使用して、インタラクティブ通信を3つの異なる方法でプレビューできます。

## 主なメリット

- サンプルデータを使用してインタラクティブコミュニケーションをプレビューし、ライブデータがコミュニケーションと結合されたときに表示される方法を視覚化します。

- ローカルのJSON データファイルをアップロードして、バックエンドを設定することなくデータ駆動型のプレビューを生成できます。

- 接続されたフォームデータモデル（FDM）を使用して、デザイン中にサンプルデータとリアルタイムのデータ統合をシミュレートできます。

- データオプション（データなし、ローカルデータ、FDM）を簡単に切り替えて、レイアウト、構造、パーソナライゼーションを検証できます。

## 異なるデータオプションを使用したインタラクティブ通信エディターでのPDF プレビュー

データ、ローカルデータ、または設定済みのデータモデルからのサンプルデータを使用せずに、インタラクティブ通信をプレビューし、柔軟なテストと検証を実現します。

+++&#x200B;1. データを使用せずにプレビュー。

1.1. IC エディターでインタラクティブ通信を開きます。

1.2. 「PDF プレビュー」オプションを使用し、「**データなし**」オプションを選択して、データを含まないコミュニケーションを表示します。

![IC ドキュメントを検索](/help/forms/interactive-communication/assets/nodata.png)

+++

+++&#x200B;2. ローカル JSON データを使用したプレビュー

2.1. 構造化JSON ファイルを準備します。 参照用に、通信に使用するJSON スキーマ [&#x200B; （FDM） &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/work-with-form-data-model)からサンプルデータをコピーできます。

2.2. IC エディターで、**PDF Preview** > Using Local Dataに移動します。

2.3. JSON ファイルを選択してアップロードし、提供されたデータを使用してPDF プレビューをレンダリングします。

![IC ドキュメントを検索](/help/forms/interactive-communication/assets/localdata.png)

+++

+++&#x200B;3. データモデルを使用したプレビュー 

3.1. 「**データモデルを使用**」を選択して、ICの既に設定されているフォームデータモデル（FDM）のサンプルデータを使用します。

3.2. プレビューでは、モデルフィールドからデータが自動入力されます。 サンプルデータが最初に使用するときにFDMに保存されていることを確認します。そうしないと、プレビューにデータが表示されない場合があります。

![IC ドキュメントを検索](/help/forms/interactive-communication/assets/datamodel.png)

+++

