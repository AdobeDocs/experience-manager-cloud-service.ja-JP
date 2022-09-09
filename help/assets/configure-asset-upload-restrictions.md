---
title: アセットのアップロード制限を設定する
description: Adobe Experience Manager Assets の設定で、ユーザーがアップロードできるアセットのタイプを MIME タイプに基づいて制限します。 これにより、望ましくない形式や悪意のあるファイルが誤ってアップロードされるのを防ぐことができます。
exl-id: 094c31f3-f2e9-4b44-9995-c76fb78ca458
source-git-commit: 472b670623e77957ff9a366359ebef8c6c0604ae
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 9%

---

# アセットのアップロード制限を設定する {#configure-asset-upload-restrictions}

Adobe Experience Manager Assets を設定して、ユーザーがアップロードできるアセットのタイプを MIME タイプに基づいて制限できます。

>[!IMPORTANT]
>
>デフォルトでは、Experience Manager Assetsでは、すべての MIME タイプのアセットのアップロードが許可されます。 ただし、特定の MIME タイプのファイルのみをアップロードするようにユーザーを制限する設定を指定できます。

## 前提条件 {#prerequisites-asset-upload-restrictions}

アセットのアップロード制限を設定するには、管理者権限が必要です。

## アセットのアップロードに制限を適用する {#apply-restrictions-asset-uploadsssssss}

を設定するには、以下を実行します。 [!DNL Experience Manager] 特定の MIME タイプのファイルをアップロードするようにユーザーを制限するには：

1. **[!UICONTROL ツール／アセット／アセット設定]**&#x200B;に移動します。

1. クリック **[!UICONTROL 制限をアップロード]**.

1. クリック **[!UICONTROL 追加]** 許可する MIME タイプを定義します。

1. テキストボックスに MIME タイプを指定します。 次をクリックできます。 **[!UICONTROL 追加]** 許可する MIME タイプをさらに指定する場合に、を再度追加します。 また、 ![削除アイコン](assets/delete-icon.svg) をクリックして、MIME タイプをリストから削除します。

1. 「**[!UICONTROL 保存]**」をクリックします。

**例 1:すべての画像とPDFファイルのExperience Manager Assetsへのアップロードを許可**

すべての形式およびPDFファイルの画像をExperience Manager Assetsにアップロードできるようにするには、次の設定をおこないます。

![アセットのアップロード制限](assets/asset-upload-restrictions.png)

`image/*` を MIME タイプとして使用すると、すべての形式の画像をアップロードできます。 `application/pdf` を MIME タイプとして使用すると、PDFファイルをExperience Manager Assetsにアップロードできます。

**例 2:特定の画像形式のExperience Manager Assetsへのアップロードを許可**

許可する MIME タイプに特定の画像形式を追加し、その他すべてのアセット形式のアップロードを制限するには、次の設定を実行します。

![アセットの制限](assets/asset-restrictions.png)

画像に表示される設定に基づいて、.JPG、.PNG および。GIF形式の画像をExperience Manager Assetsにアップロードできます。
