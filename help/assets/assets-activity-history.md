---
title: タイムラインのアクティビティストリーム
description: この記事では、アセットのアクティビティログをタイムラインに表示する方法について説明します。
contentOwner: AG
feature: Asset Reports,Asset Management
role: Admin,User
exl-id: 8dd82c31-f88e-4407-9b6d-c87033d7a823
source-git-commit: 0d0a3247e42e0f4a9b2965104814fe6bcd8e6128
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 100%

---

# アクティビティストリームでのアセット操作ログの表示 {#activity-stream-in-timeline}

この機能は、タイムラインにアセットのアクティビティログを表示します。[!DNL Experience Manager Assets] で以下のアセット関連操作を実行すると、アクティビティストリーム機能により、タイムラインが更新され、そのアクティビティが反映されます。

アクティビティストリームでログに記録される操作は次のとおりです。

* 作成
* 削除
* ダウンロード（レンディションを含む）
* 公開
* 非公開
* 承認
* 拒否
* 移動

タイムラインに表示されるアクティビティログは、ログファイルが格納されている CRX の `/var/audit/com.day.cq.dam/content/dam` から取得されます。また、[Adobe Asset Link](https://helpx.adobe.com/jp/enterprise/using/manage-assets-using-adobe-asset-link.html) または [[!DNL Experience Manager] デスクトップアプリケーション](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html?lang=ja)により、新しいアセットがアップロードされたり、既存のアセットが変更されて [!DNL Experience Manager] にチェックインされたりすると、タイムラインアクティビティがログに記録されます。

>[!NOTE]
>
>一時的なワークフローは、履歴情報が保存されないので、タイムラインに表示されません。

アクティビティストリームを表示するには、アセットに対して 1 つ以上の操作を実行して、アセットを選択してから、グローバルナビゲーションリストから&#x200B;**[!UICONTROL タイムライン]**&#x200B;を選択します。

<!-- ![timeline-2](assets/timeline-2.png) -->

タイムラインに、アセットに対して実行した操作のアクティビティストリームが表示されます。

<!-- ![activity_stream](assets/activity_stream.png) -->

>[!NOTE]
>
>**[!UICONTROL 公開]**&#x200B;タスクと&#x200B;**[!UICONTROL 非公開]**&#x200B;タスクのデフォルトのログ保管先は `/var/audit/com.day.cq.replication/content` です。**[!UICONTROL 移動]**&#x200B;タスクの場合は、デフォルトの保管先は `/var/audit/com.day.cq.wcm.core.page` になります。
