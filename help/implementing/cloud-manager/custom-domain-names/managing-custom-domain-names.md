---
title: カスタムドメイン名の管理
description: Cloud Manager を使用して、カスタムドメイン名を表示、更新、置換、削除する方法について説明します。
exl-id: 6cab8cf2-22c0-4f4b-9c54-a1425e74ddd0
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 2d1382c84d872719332986baa5829d1623d9d9a6
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 58%

---


# カスタムドメイン名の管理 {#managing-custom-domain-names}

Cloud Managerでは、カスタムドメイン名を編集、更新、置換、削除できます。

## カスタムドメイン名設定の編集 {#view-and-update}

AdobeCloud Managerでは、次の理由により、カスタムドメイン名の設定を変更する場合があります。

* **環境の切り替え**：コンテンツをエンドユーザー（Publish）と内部ユーザー（オーサー）のどちらに提供しているかに応じて正しい設定を適用します。
* **セキュリティの更新**：セキュリティまたはコンプライアンスの強化を目的として、新しい SSL 証明書にアップグレードします。
* **デプロイメント戦略の変更**：適切な暗号化とサイトアクセスのために、正しい SSL 証明書が特定の環境に適用されることを確認します。

**カスタムドメイン名設定を編集するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、プログラムを選択します。

1. ページの左上隅にあるハンバーガーアイコンをクリックして、左側のナビゲーションメニューを表示します。
1. **サービス** 見出しの下の「**CDN 設定**」をクリックします。
1. **CDN 設定** ページで、CDN を編集する行の最後にある ![ 詳細アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックします。
1. 「**編集**」をクリックします。
1. **CDN 設定を編集** ダイアログボックスで、次の操作を行います。
   * 「**層**」ドロップダウンリストで、使用する層（Publishまたはプレビュー）を選択します。
   * **SSL 証明書** ドロップダウンリストで、使用する SSL 証明書を選択します。
1. 「**更新**」をクリックします。


## カスタムドメイン名の SSL 証明書の更新 {#update-cert}

[カスタムドメイン名を表示および更新する場合と同じ手順](#view-and-update)に従って、カスタムドメイン名の SSL 証明書を更新します。

>[!NOTE]
>
>SSL 証明書が有効で、[既に設定されており](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md)、更新するカスタムドメイン名を含んでいる必要があります。


## カスタムドメイン名の削除 {#deleting}

**ビジネスオーナー**&#x200B;または&#x200B;**デプロイメントマネージャー**&#x200B;の役割を持つユーザーが、Cloud Manager を使用してカスタムドメイン名を削除できます。

### 関連するすべての環境からカスタムドメイン名の削除 {#delete-cdn-all}

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. **概要**&#x200B;画面から&#x200B;**ドメイン設定**&#x200B;ページに移動します。

1. 削除するカスタムドメイン名の行を特定します。

1. 行の右端にある省略記号ボタンをクリックします。

1. 「**削除**」を選択します。

1. 送信を確認します。


### 特定の環境からカスタムドメイン名の削除 {#delete-cdn-specific}

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。
1. **概要**&#x200B;ページの&#x200B;**環境**&#x200B;画面に移動します。
1. **環境**&#x200B;ページから、対象となる環境の詳細画面に移動します。
1. ドメイン名のテーブルで、削除するカスタムドメイン名の行を見つけます。
1. 行の右端にある省略記号ボタンをクリックします。
1. 「**削除**」を選択します。
1. 送信を確認します。
