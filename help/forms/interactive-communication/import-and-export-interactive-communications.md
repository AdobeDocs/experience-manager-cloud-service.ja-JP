---
title: インタラクティブ通信の読み込みと書き出し
description: インタラクティブ通信の読み込みと書き出しを使用すると、ユーザーは、環境全体で通信をシームレスに移行、再利用、管理できます。
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
hide: true
index: false
hidefromtoc: true
source-git-commit: f772a193cce35a1054f5c6671557a6ec511671a9
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 15%

---


# インタラクティブ通信の読み込みと書き出し

>[!NOTE]
>
> インタラクティブ通信機能は、早期導入プログラムで利用できます。 勤務先のアドレスから `aem-forms-ea@adobe.com` にメールを送信して、アクセスをリクエストします。

>[!IMPORTANT]
>
> **ドキュメントは変更される場合があります**：このプロンプトライブラリは現在製品に対してテスト中であり、更新および改訂される可能性があります。早期導入プログラム中に Forms Experience Builder が進化し続けると、プロンプト、例、ベストプラクティスが変わる可能性があります。

インタラクティブ通信（IC）の読み込み/書き出し機能を使用すると、環境全体で通信をシームレスに移行、再利用、管理できます。 これにより、インタラクティブ通信（IC）を、関連するフラグメントとデータモデルと共に、ある環境から書き出して別の環境に読み込むことができるので、一貫性が確保され、デプロイメント時の作業の重複が削減されます。

## 主なメリット

- 環境間での IC の移行を合理化します。
- フラグメント、データモデルおよび依存関係を保持します。
- プロジェクト間で IC を再作成する手間を軽減します。

## インタラクティブ通信の読み込みと書き出し

インタラクティブ通信（IC）を 1 つの環境で作成し、次の手順に従って書き出しと読み込みを行って別の環境で再利用します。

+++&#x200B;1. インタラクティブ通信の書き出し方法

1.1. [&#x200B; 作成されたインタラクティブ通信 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/forms/interactive-communication/create-interactive-communication) （IC）を選択します。
1.2. 「**ダウンロード**」オプションをクリックして、ZIP ファイルとしてエクスポートします。
1.3. ダウンロードした ZIP ファイルには、選択した **template**、**fragments**、および **data model** と共に IC が含まれています。

![IC Docu の検索 &#x200B;](/help/forms/interactive-communication/assets/downloadic.png)
+++

+++&#x200B;2. インタラクティブ通信の読み込み方法

2.1. ターゲット環境に移動します。
2.2. **Forms/Formsとドキュメント/作成/ファイルのアップロード** に移動します。
2.3. IC に ZIP ファイルをアップロードし **インポート** します。

![IC Docu の検索 &#x200B;](/help/forms/interactive-communication/assets/uploadfile.png)

2.4. アップロード後、IC は関連するフラグメントおよびデータモデルと共に表示されます。

![IC Docu の検索 &#x200B;](/help/forms/interactive-communication/assets/importfragment.png)
+++

+++&#x200B;3. フラグメントの読み込みと書き出し

3.1. エクスポートするには、**Forms/Formsとドキュメント** から必要なフラグメントを選択し、「**ダウンロード**」をクリックして ZIP ファイルとしてエクスポートします。

3.2.読み込むには、対象環境に移動し、Forms/Formsとドキュメント/作成/**ファイルのアップロード** に移動して、書き出した ZIP ファイルをアップロードします。

これにより、異なる環境間でフラグメントを簡単に再利用でき、設計の一貫性を確保し、作業の重複を減らすことができます。
+++
