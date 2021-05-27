---
title: コンテンツのプレビュー
description: AEM Preview Serviceを使用して、運用を開始する前にコンテンツをプレビューする方法を説明します。
source-git-commit: 9b4ac173c55380cbc06de64677470818aa801df4
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 0%

---


# コンテンツのプレビュー{#previewing-content}

>[!NOTE]
>
>プレビュー機能は2021.5.0リリースの一部で、今後数週間で徐々に展開される予定です。

AEMは、開発者とコンテンツ作成者が、パブリッシュ環境に到達する前にWebサイトの最終エクスペリエンスをプレビューし、公開されるように設計された、サイトプレビューサービスを提供します。

ページトランジションや他のパブリッシュ側のみのコンテンツなど、オーサー環境からは見えないページエクスペリエンスのプレビューを容易にします。

## プレビュー用のコンテンツの公開{#publishing-content-to-preview}

次のように、Managed Publication UIを使用して、プレビューサービスにコンテンツを公開できます。

1. サイトコンソールでプレビュー用に送信する1つ以上のページを選択し、「**公開を管理**」ボタンをクリックします
1. 次のウィザードで、宛先として「**プレビュー**」を選択します

   ![管理公開](/help/sites-cloud/authoring/assets/previewmanagedpublication.png)

1. 「**次へ**」をクリックし、「**公開**」をクリックして確定します。

プレビューコンテンツを確認し、実稼動インスタンスのパブリッシュURLに&#x200B;**preview**&#x200B;を追加します。 URLは、次のように記述します。

```
https://preview-p[programID]-e[environmentID].adobeaemcloud.com/pathtopage.html
```

お使いの環境のURLを取得する方法の詳細については、[環境の管理](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/manage-your-environment.html?lang=en)を参照してください。

