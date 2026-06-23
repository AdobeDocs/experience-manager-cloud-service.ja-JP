---
title: インタラクティブ通信の読み込みと書き出し
description: インタラクティブ通信の読み込みと書き出しにより、ユーザーは環境をまたいで通信をシームレスに移行、再利用、管理できます。
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
badgeSaas: label="AEM Forms" type="Positive" tooltip="AEM Formsに適用）。"
exl-id: 7e328932-070d-4eb3-8176-500ef31581be
source-git-commit: 53ff71c82d35b9ec9b20b521ef469d3f0abd79df
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 3%

---

# インタラクティブ通信の読み込みと書き出し


インタラクティブ通信（IC）のインポートおよびエクスポート機能を使用すると、ユーザーは環境をまたいで通信をシームレスに移行、再利用、管理できます。 これにより、ある環境からインタラクティブ通信（IC）とその関連フラグメントおよびデータモデルを書き出して別の環境に読み込むことができ、一貫性を確保し、デプロイメント時の労力の重複を減らすことができます。

## 主なメリット

- 環境をまたいでICの移行を簡素化します。
- フラグメント、データモデル、依存関係を保持します。
- プロジェクトをまたいでICを再作成する労力を軽減できます。

## インタラクティブ通信の読み込みと書き出し

ある環境でインタラクティブ通信（IC）を作成し、次の手順で書き出して読み込むことで、別の環境で再利用できます。

+++&#x200B;1. インタラクティブ通信の書き出し方法

1.1. [作成したインタラクティブ通信](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/interactive-communication/create-interactive-communication) （IC）を選択します。
1.2.「**ダウンロード**」オプションをクリックして、ZIP ファイルとしてエクスポートします。
1.3. ダウンロードされたZIP ファイルには、選択した**テンプレート**、**フラグメント**、**データモデル**&#x200B;と共にICが含まれています。

![IC ドキュメントを検索](/help/forms/interactive-communication/assets/downloadic.png)
+++

+++&#x200B;2. インタラクティブ通信のインポート方法

2.1. ターゲット環境に移動します。
2.2. **Forms/Formsとドキュメント/作成/ファイルアップロード**に移動します。
2.3. ZIP ファイルを**インポート**&#x200B;にICにアップロードします。

![IC ドキュメントを検索](/help/forms/interactive-communication/assets/uploadfile.png)

2.4. アップロード後、ICは関連するフラグメントとデータモデルとともに表示されます。

![IC ドキュメントを検索](/help/forms/interactive-communication/assets/importfragment.png)
+++

+++&#x200B;3. フラグメントの読み込みと書き出し

3.1. 書き出すには、**Forms/Formsとドキュメント**&#x200B;から必要なフラグメントを選択し、**ダウンロード**&#x200B;をクリックしてZIP ファイルとして書き出します。

3.2. 読み込むには、対象の環境に移動し、Forms/Formsとドキュメント/作成/**ファイルアップロード**&#x200B;に移動し、書き出したZIP ファイルをアップロードします。

これにより、異なる環境でフラグメントを簡単に再利用でき、デザインの一貫性を確保し、作業の重複を減らすことができます。
+++

